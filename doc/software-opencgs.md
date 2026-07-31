# NEMOCRYS/opencgs for High-Fidelity Czochralski Simulation: A Critical Technical Assessment and Comparison with CrysMAS

**Scope.** This report evaluates whether the open-source NEMOCRYS/opencgs software stack can serve as a viable platform for industrial-grade numerical simulation of the Czochralski (CZ) crystal growth process, identifies which physical phenomena it currently supports natively versus requires custom development, and benchmarks it against CrysMAS, the dedicated finite-volume crystal-growth code developed at Fraunhofer IISB. It is written for researchers and engineers working in semiconductor crystal growth, CFD, heat transfer, and multiphysics simulation who are considering either platform for a new modeling effort.

---

## 1. Background and Software Identities

### 1.1 NEMOCRYS/opencgs

NEMOCRYS ("Next Generation Multiphysical Models for Crystal Growth Processes") is an ERC-funded research project (Horizon 2020, grant agreement No. 851768) carried out at the Leibniz Institute for Crystal Growth (IKZ), Berlin, principally by A. Enders-Seidlitz, K. Dadzis, and collaborators. **opencgs** is the Python software layer produced by that project: it is *not* a monolithic crystal-growth solver but an orchestration framework that wires together several independent open-source components into a CZ (and, secondarily, floating-zone, FZ) simulation workflow:

- **Gmsh** — mesh generation, wrapped through the companion package `objectgmsh` (object-oriented geometry/mesh construction in Python).
- **Elmer FEM** — the finite-element multiphysics solver that actually computes heat conduction/convection boundary models, electromagnetic induction heating, and (via `PhaseChangeSolve`/`SteadyPhaseChange` and `MeshSolve`) phase-boundary tracking through mesh deformation.
- **pyelmer** — a Python interface that programmatically generates Elmer `.sif` (Solver Input File) configurations, avoiding hand-editing of Elmer's native text format.
- **ParaView** — post-processing/visualization.
- **opencgs** itself — the orchestration and "control" layer (`opencgs.control`) that ties meshing, solving, iterative crystal-diameter computation, parameter studies, and result harvesting into a repeatable simulation pipeline, largely configured through YAML files (`config_geo.yml`, `config_sim.yml`, `config_mat.yml`, `config_di.yml`).

The entire stack is distributed as source on GitHub (`nemocrys/opencgs`, `nemocrys/pyelmer`, `nemocrys/objectgmsh`) and as a maintained Docker image (`nemocrys/opencgs`), which is the recommended installation route given the number of interdependent components (Elmer, Gmsh, Python bindings) that must otherwise be built or installed separately. A growing set of worked examples exists in `nemocrys/opencgs_examples` and process-specific repositories (`nemocrys/test-cz-induction`, `nemocrys/vertical-gradient-freeze`), several of which are tied directly to peer-reviewed publications and two PhD theses (Enders-Seidlitz's foundational CZ thermal model paper in *Journal of Crystal Growth* 593 (2022) 126750, and A. Wintzer's 2024 TU Berlin thesis "Validation of multiphysical models for Czochralski crystal growth").

A parallel, more experimental line of development, `nemocrys/crystal-x`, explores a steady-state CZ implementation directly in **FEniCS/DOLFINx** rather than Elmer, motivated explicitly by Elmer/Gmsh's limitations in handling strongly deforming meshes and tightly coupled moving-boundary problems. This signals that even within the NEMOCRYS group, Elmer-based opencgs is understood as a first-generation tool with known architectural ceilings.

### 1.2 CrysMAS

CrysMAS ("Crystal Growth Modeling Analysis System" — commonly cited simply as CrysMAS) is a proprietary, commercially and academically licensed finite-volume code developed over roughly three decades by the Crystal Growth Laboratory of Fraunhofer IISB (Erlangen, Germany), under the long-term technical leadership of researchers including Jochen Friedrich and Georg Müller. It is a **purpose-built, domain-specific application** for furnace-scale and crystal-scale simulation of melt- and vapor-based crystal growth processes (CZ, VGF, HEM, DS, and related variants), rather than a general PDE toolkit repurposed for the domain.

Key architectural facts, drawn from the code's technical literature and third-party usage reports:

- CrysMAS solves the governing conservation equations (energy, momentum, species) using the **finite volume method**, historically on an **unstructured triangular grid** for the global furnace domain and a **structured, boundary-fitted grid** for the melt/crystal/ampoule region where flow, phase change, and interface tracking occur.
- **Radiative heat transfer** is computed via a view-factor/enclosure (surface-to-surface) method, appropriate for the large cavity radiation problems that dominate high-temperature crystal-growth furnaces.
- The interface between crystal and melt is computed as part of a coupled thermal–flow solution; furnace heater set-point temperatures are prescribed as boundary conditions and the corresponding **heater powers are solved as unknowns** — a global inverse-type coupling that is central to how growers actually operate CZ pullers (they command power, but process design is usually expressed in temperature targets).
- Global nonlinear convergence uses a **quasi-Newton iterative scheme**.
- CrysMAS is explicitly designed to be coupled with companion codes for different sub-domains: it typically supplies the **global furnace-scale heat transfer** while a specialized crystal/ampoule-scale code (e.g., **Cats2D**, developed by J. Yeckel and colleagues) handles the detailed melt flow, phase-change position, and solute segregation inside the crucible/ampoule — a "zoom-in" coupled-code strategy that has been used in numerous published VGF, HEM, and gradient-freeze studies.

CrysMAS' three-decade validation record spans silicon CZ, sapphire HEM, CdZnTe EDG/VGF, and other systems, published extensively by both the Fraunhofer IISB group and external academic users (notably the Derby group, University of Minnesota).

---

## 2. Physical Phenomena Coverage: What Each Platform Handles Natively

The central technical question for a prospective user is not "which is better" in the abstract but "which physical effects are already implemented, tested, and documented, versus which require new solver development." The table below is organized around the physics that a rigorous CZ model must eventually address.

| Physical phenomenon | NEMOCRYS/opencgs (current, as of published work) | CrysMAS |
|---|---|---|
| Conductive heat transfer (crystal, melt, crucible, insulation) | **Native**, via Elmer `HeatSolver`; the core capability and the best-validated part of the stack | **Native**; core capability, three decades of use |
| Global cavity/surface radiative heat transfer | **Native**, via Elmer's radiation/view-factor handling, validated against the Test-CZ model furnace | **Native**, purpose-built view-factor/enclosure method; long-standing strength of the code |
| Induction heating / electromagnetics | **Native**, via Elmer's `StatMagSolver`/harmonic EM solvers, validated for the NEMOCRYS Test-CZ inductive furnace | Supported (EM heating modeling is part of the furnace-scale solve); mature but less publicly documented in method detail |
| Resistive heating | **Native**, demonstrated (`sn-resistance_2D` example) | Native |
| Phase change / solid–liquid interface tracking | **Native but limited**: single, sharp interface tracked isothermally via mesh deformation (`PhaseChangeSolve`/`MeshSolve`), loosely coupled iterative scheme; validated in 2D axisymmetric steady state | **Native**, more mature: interface computed as part of coupled thermal-flow-phase-change solution within the crucible/ampoule sub-model, with a longer track record across multiple materials systems |
| Crystal diameter computation / meniscus | **Native, simplified**: iterative diameter control implemented in opencgs (`config_di.yml`), validated against Test-CZ experiments; free meniscus shape itself is *not* solved from first principles (Young–Laplace) in the published implementations reviewed | Native, more complete free-boundary/meniscus treatment as part of its long-standing CZ capability |
| Melt convection (buoyancy-driven) | **Not yet natively solved by the FEM heat-transfer model.** Published CZ work to date treats melt/gas convection via **effective heat transfer coefficients and an effective (enhanced) thermal conductivity, calibrated against experiment**, rather than a resolved Navier–Stokes solve in the melt. Full CFD (via Elmer's flow solver or coupled OpenFOAM) is discussed as future/ongoing work, not delivered production capability | **Native**: resolved melt convection (buoyancy, forced via rotation) is part of the coupled crucible-scale model, historically via structured-grid finite volume; long-validated |
| Marangoni (thermocapillary) convection | Not implemented in current CZ examples; theoretically addressable if/when melt flow is added, but no published validated case | Supported within the code's melt-flow capability (documented capability of the broader Fraunhofer IISB simulation toolchain, alongside OpenFOAM/Ansys, for Marangoni-relevant free-surface flows) |
| Forced convection (crystal/crucible rotation) | Not yet in published CZ opencgs cases (would require a resolved momentum solve; current models are thermal-only or thermal + EM) | Native — rotation-driven forced convection is a standard, long-used capability |
| Magnetohydrodynamic (MHD) damping of melt flow (for magnetic CZ, MCZ) | Not implemented; would require coupled EM + resolved melt flow, which the platform does not yet deliver end-to-end | Not CrysMAS's own core strength either (MHD flow control is more the territory of CGSim/STR or dedicated OpenFOAM MHD solvers used alongside CrysMAS at IISB) — but IISB's broader toolchain (CrysMAS + OpenFOAM + Ansys) explicitly covers MHD flow simulation as an institutional capability |
| Turbulence modeling (gas or melt) | Not implemented in the reviewed CZ examples (thermal/EM focus only); FZ-side work uses OpenFOAM separately for flow-oriented validation experiments, suggesting the group intends turbulence/CFD work to live in OpenFOAM rather than Elmer | Available as part of the IISB toolchain (flow simulations "including turbulence" are explicitly listed institutional capability, though this may lean on OpenFOAM/Ansys alongside CrysMAS rather than CrysMAS alone) |
| Dopant/impurity segregation | Not present in published NEMOCRYS CZ work reviewed here | Native / long-established (segregation modeling is one of CrysMAS's classic use cases, e.g., in CZT and doped-Si studies) |
| Species transport with chemical reactions (e.g., oxygen/carbon transport, SiC-relevant chemistry) | Not implemented | Explicitly listed IISB institutional capability ("simulation of species transport including chemical reactions"), though this may again involve companion tools rather than CrysMAS in isolation |
| Thermal stress / dislocation density in the growing crystal | **Available via a separate, coupled tool**: NEMOCRYS-adjacent work computes thermal stress and dislocation density (e.g., for HPGe) by post-processing Elmer's thermal field through a **coupled stress/dislocation-density model**, not as an opencgs built-in | Stress simulation is a listed IISB institutional capability, historically achieved through coupling CrysMAS thermal fields to dedicated stress solvers (a similar "coupled tool" pattern to NEMOCRYS's approach) |
| Transient (time-dependent) growth simulation | **Native**, Elmer supports transient solves and this is explicitly part of the NEMOCRYS roadmap/validation ("modeling the global and local heat transfer both in steady and transient states"); production-grade transient CZ pulling (moving free surface + growing crystal + evolving melt volume) is not yet demonstrated as a fully coupled, validated capability in public examples | Native and mature — transient/quasi-steady-state (QSS) growth-cycle simulation, including set-point ramps consistent with realistic pulling schedules, is a standard, decades-old capability |
| 3D geometry | Elmer is inherently 3D-capable, and NEMOCRYS/opencgs examples exist in 2D axisymmetric form (the norm for CZ) with 3D extensions demonstrated for non-axisymmetric heater configurations in related work; 3D thermal-stress work (Li₂MoO₄) exists in the broader ecosystem | Native 2D axisymmetric and 3D capability, long-established |
| Model-parameter sensitivity analysis / validation methodology | **A stated core project goal and genuine strength**: NEMOCRYS has published an explicit three-step validation methodology (sensitivity analysis → parameter adjustment against in-situ/model-experiment data → global accuracy estimation), executed rigorously for Sn model-experiment CZ growth | Validation is extensive but based on decades of accumulated industrial/academic case studies rather than a single codified, published methodology; less emphasis on formal sensitivity-analysis workflows in the public literature |

**Reading the table.** NEMOCRYS/opencgs, as of the published literature through 2024, is best characterized as **a validated global thermal + electromagnetic (+ simplified phase-change) solver for CZ furnaces**, deliberately using *effective* transport coefficients to stand in for melt and gas convection rather than resolving them from first principles. CrysMAS is a **mature, resolved multiphysics solver** (thermal, flow, phase change, segregation) purpose-built for the same class of problem, with three decades of validation across multiple crystal systems. The gap is not marginal: melt convection, forced/rotational flow, segregation, and free-meniscus mechanics are central to what most practitioners mean by "high-fidelity CZ simulation," and these are precisely the areas where opencgs's public CZ capability is thinnest.

---

## 3. Numerical Methods: A Direct Comparison

| Aspect | NEMOCRYS/opencgs (via Elmer) | CrysMAS |
|---|---|---|
| Discretization | Finite Element Method (FEM), Elmer's general-purpose multiphysics FEM kernel | Finite Volume Method (FVM), purpose-built for crystal-growth cavity/melt geometries |
| Mesh type | Unstructured, Gmsh-generated; body-fitted; deformable via `MeshSolve` for interface tracking | Unstructured triangular (global furnace) + structured boundary-fitted (melt/crystal region), historically | 
| Interface/free-boundary handling | Iterative isotherm detection + Arbitrary Lagrangian–Eulerian-style mesh deformation, loosely coupled to the thermal solve (up to ~10 outer iterations to convergence in published work) | Coupled solution of interface position within the flow/thermal/phase-change system, developed and tuned specifically for melt-growth free boundaries over decades |
| Global nonlinear solution strategy | Loosely coupled, sequential solver calls orchestrated by opencgs/pyelmer (heat → source term → phase boundary update → mesh update, iterated) | Quasi-Newton iteration on the coupled system, with heater power computed as an unknown to match prescribed set-point temperatures — a more directly "process-engineering-native" solution strategy |
| Radiation method | View-factor-based radiation within Elmer, validated for the Test-CZ geometry | Dedicated enclosure/view-factor method, refined over many furnace geometries |
| Parallelization / HPC scalability | Elmer supports MPI-parallel execution and has been used at extreme scale in unrelated FEM contexts (e.g., BlueGene/P-class Schrödinger-equation solvers demonstrate Elmer's underlying ecosystem is HPC-capable in principle); however, published NEMOCRYS CZ cases are 2D axisymmetric, run in ~100 s on a single CPU core, and there is no published evidence of parallel scaling studies for the CZ workflow specifically | Historically developed and used primarily as a desktop/workstation engineering tool for practical furnace design iteration; not marketed around HPC scalability, though coupled global+local (CrysMAS+Cats2D) workflows partition problem size manageably |
| Verification | A dedicated `nemocrys/elmer-verification` repository provides 2D axisymmetric verification cases for Elmer FEM — a genuinely good practice, though verification is distinct from experimental validation | Verification is implicit in a long commercial/academic deployment history rather than published as a standalone open verification suite |
| Validation | Explicit, published, quantitative validation against dedicated model experiments (Sn CZ growth, Test-CZ furnace) with stated accuracy/deviation bounds; validation methodology itself is a research output | Extensive validation across real industrial and laboratory growth systems (Si, sapphire, CdZnTe, and others) published by both Fraunhofer IISB and independent groups (e.g., University of Minnesota) over ~25+ years |

---

## 4. Software Engineering, Usability, and Ecosystem

### 4.1 Licensing and access

- **NEMOCRYS/opencgs**: fully open source (GitHub, permissive licensing consistent with Elmer's GPL/LGPL heritage and typical academic Python tooling), free to use, modify, and redistribute. This is a first-order strategic advantage for academic groups, cost-sensitive users, and anyone requiring source-level auditability or the ability to embed the solver in a larger automated pipeline (e.g., ML-driven design optimization).
- **CrysMAS**: proprietary, licensed by Fraunhofer IISB (with documented manual/download portal access implying a controlled licensing process). Cost, license administration, and vendor dependency are real considerations; source code is not available for inspection or modification by licensees in the way opencgs is.

### 4.2 Maturity and documentation

- opencgs's own documentation is explicitly noted by its developers as "still under construction," with support channels being GitHub issues and direct contact with the lead developer — typical of an active academic project but not yet at the level of a polished commercial product. Independent third-party blog accounts of first-time use confirm real friction: missing modules, undocumented multi-repository dependencies (opencgs *and* test-cz-induction *and* pyelmer must be cloned/installed together), and a learning curve around the YAML-configuration/Python-API pattern.
- CrysMAS benefits from a maintained user manual (hosted at Fraunhofer IISB's download portal) and decades of accumulated institutional documentation, training, and support as part of a commercial/quasi-commercial product offering.

### 4.3 Extensibility

This is where opencgs's architecture is a genuine asset. Because the stack is Python-orchestrated and built on Elmer (itself extensible via user-defined Fortran/C solvers and Elmer's modular solver architecture) plus Gmsh (fully scriptable meshing) and is openly coupled to a large scientific Python ecosystem (NumPy, SciPy, PyVista, and — per the FEniCS-based `crystal-x` sibling project — DOLFINx), a research group with in-house FEM/CFD development capability can:

- add new physics (segregation, resolved melt flow, MHD, stress/dislocation coupling) as new Elmer solver modules or as external solvers coupled through a framework such as **preCICE** (which NEMOCRYS has already piloted for coupled heat-and-gas-flow simulation, per their 2022 ECCOMAS and preCICE workshop contributions);
- integrate machine-learning-based surrogate modeling, automated parameter sweeps, or optimization loops directly in Python around the simulation, without vendor API constraints;
- version-control the entire simulation setup (geometry, mesh scripts, material data, solver configuration) as code, enabling reproducibility practices that are difficult to achieve with GUI-driven commercial tools.

CrysMAS, by contrast, is extensible primarily through its vendor's own development roadmap and through its established pattern of *external* coupling to other specialized codes (Cats2D for ampoule-scale detail, OpenFOAM/Ansys within the IISB toolchain for MHD/turbulence/species transport). End users without access to CrysMAS's internals cannot add new physics to the core code themselves; they can only orchestrate CrysMAS alongside other tools at the workflow level, much as opencgs orchestrates Elmer/Gmsh.

### 4.4 Practical usability for non-specialists

CrysMAS, as a domain-specific application with (presumably) GUI/pre- and post-processing support tailored to crystal-growth engineers, is likely to be considerably more approachable for a process engineer without a strong FEM/CFD or Python-scripting background. opencgs, by design, requires competence in Python scripting, Docker or manual multi-package installation, Gmsh geometry definition, and at least a working understanding of Elmer's solver architecture and `.sif` file semantics (even though pyelmer abstracts most direct `.sif` editing). This is a meaningful practical barrier for industrial adoption outside groups that already have computational-science staff.

---

## 5. Effort Required to Bring opencgs to CrysMAS-Comparable Capability

To approach CrysMAS's current CZ capability set, a NEMOCRYS/opencgs-based effort would need to close the following gaps, roughly ordered by both necessity and estimated effort:

1. **Resolved melt (and ideally gas) convection.** This is the single largest gap. It requires either (a) activating and validating Elmer's Navier–Stokes solver for the melt domain, coupled to the existing heat-transfer/phase-change loop, including buoyancy (Boussinesq) and free-surface Marangoni stress boundary conditions, or (b) a coupled Elmer–OpenFOAM approach (already piloted by NEMOCRYS for FZ validation and prototyped via preCICE) extended to CZ. Either route is a substantial, multi-year solver-development and validation program, not a configuration change — it directly parallels what CrysMAS already has validated across many material systems.
2. **Forced convection from crystal/crucible rotation**, coupled self-consistently with the (currently absent) resolved melt flow — needed jointly with (1), since rotation-driven flow only matters once flow is resolved at all.
3. **A first-principles free meniscus / triple-point model** (Young–Laplace-based meniscus shape and pull-rate/diameter feedback), replacing or augmenting the current empirically tuned diameter-control approach, to reach CrysMAS's more complete free-boundary treatment.
4. **Dopant/impurity segregation modeling**, requiring a coupled species-transport (advection–diffusion, with distribution-coefficient interface conditions) solve, contingent on (1) since segregation is flow-dependent.
5. **Turbulence modeling** for both gas and (at higher Reynolds/Grashof numbers, or with agitation such as accelerated crucible rotation) melt flow, if the target application involves industrial-scale (large-diameter, e.g., 300 mm Si) crystals rather than small model-experiment or laboratory-scale systems — this is where NEMOCRYS's own model-experiment validation strategy (small-scale Sn, Test-CZ) is explicitly *not yet* representative of industrial-scale CZ.
6. **A robust, validated fully transient pulling simulation** (evolving melt volume, moving crystal, coupled free-surface and phase-boundary tracking over the full growth cycle) rather than the steady/quasi-steady snapshots currently demonstrated.
7. **3D capability with equivalent robustness** for non-axisymmetric configurations (asymmetric heater layouts, magnetic fields in MCZ), which CrysMAS already supports as production capability.
8. **Engineering hardening**: documentation, regression/verification test suites beyond the current `elmer-verification` cases, packaging/versioning discipline (note that example repositories already show version-pinning friction, e.g., `test-cz-induction` warning that future opencgs versions "may require changes to the code"), and ideally a GUI or higher-level configuration layer for non-specialist users.

**Overall assessment of effort**: this is realistically a **multi-year program requiring dedicated CFD/FEM developers with domain expertise in melt convection and free-boundary crystal growth**, not an incremental extension a single user could complete alongside applied simulation work. This assessment is consistent with the fact that NEMOCRYS itself, as a well-funded (ERC-backed) multi-year project with dedicated PhD-level staff, has after several years of work reached primarily the thermal/EM/simplified-phase-change stage for CZ, with resolved-flow and coupled-CFD work still described as ongoing/future development in its own publications (the FZ-side OpenFOAM validation work is the most advanced flow-resolving line, and even that is explicitly a "first example," not yet extended with phase boundaries).

---

## 6. Comparative Summary Table

| Criterion | NEMOCRYS/opencgs | CrysMAS |
|---|---|---|
| Physics coverage for CZ (current, public) | Thermal + EM + simplified phase change; melt/gas convection via calibrated effective coefficients | Thermal + EM + resolved melt convection + phase change + segregation; broad, mature |
| Numerical method | FEM (Elmer), unstructured deformable mesh | FVM, unstructured/structured hybrid, purpose-tuned |
| Validation status | Rigorous but narrow: small-scale model experiments (Sn), one furnace geometry class (Test-CZ), formalized methodology | Broad and deep: decades, multiple materials (Si, sapphire, CdZnTe, others), industrial and academic use |
| Industrial readiness (as delivered) | Not yet — research/validation-stage tool for CZ; more mature for global thermal design studies than for flow-sensitive predictions | Yes — established industrial and academic engineering tool |
| Scalability (large industrial crystal diameters, e.g., 300 mm Si) | Unproven in public CZ work (model-experiment scale demonstrated) | Proven across industrially relevant scales |
| Extensibility (adding new physics) | High, in principle — open source, modular, Python-orchestrated, scriptable; requires in-house FEM/CFD development capability | Low for end users (closed source); extension mainly via external code coupling at the workflow level |
| Cost / licensing | Free, open source | Commercial/licensed |
| Usability for non-specialist process engineers | Low–moderate; requires scripting/Docker/FEM literacy | Higher; purpose-built application, longer support/documentation history |
| Reproducibility / auditability | High — version-controllable, scriptable, source-inspectable | Lower — proprietary internals |
| HPC/parallel scalability evidence for CZ specifically | Not demonstrated in public CZ examples (2D axisymmetric, single-core runs) | Not primarily marketed on HPC scaling either; workflow partitioning (global + local coupled codes) is the traditional scalability strategy |
| Ecosystem coupling | Elmer, Gmsh, OpenFOAM (FZ side), preCICE (piloted), FEniCS/DOLFINx (sibling project) | Cats2D, OpenFOAM, Ansys (as part of the broader Fraunhofer IISB toolchain) |

---

## 7. Recommendations

**For academic/research groups** whose goals include method development, coupling novel physics (e.g., ML-augmented modeling, new sensor-driven validation workflows, or FZ/CZ model-experiment research consistent with NEMOCRYS's own mission), and who have or can hire FEM/CFD development capability: **NEMOCRYS/opencgs is a strong and appropriate choice**, particularly for thermal/electromagnetic furnace design studies, model-experiment validation research, and as a foundation for further solver development. Its open-source nature, Python-native architecture, and demonstrated rigorous validation methodology are genuine strengths that align well with academic research objectives (publishability, reproducibility, extensibility). Groups should budget realistically for the substantial development effort (Section 5) if resolved melt convection, segregation, or industrial-scale predictive accuracy are required, and should consider whether coupling to OpenFOAM (already piloted for FZ) or preCICE-based multi-code coupling is a faster path than extending Elmer's own flow solver.

**For industrial process engineering teams** requiring predictive, validated, flow-resolving CZ simulation today — for hot-zone design, pull-rate/diameter control optimization, dopant segregation prediction, or defect (e.g., oxygen, dislocation) engineering at production scale — **CrysMAS (or a comparably mature commercial code such as CGSim) remains the more suitable tool as of now**. Its resolved convection, segregation modeling, and decades of validated industrial use directly address the physics that dominate real CZ process outcomes, and its usability profile is better matched to engineering teams without dedicated computational-science staff.

**A hybrid strategy** is worth serious consideration for organizations with both research and production needs: use CrysMAS (or another mature commercial tool) for production-relevant, flow-resolved predictive work, while using NEMOCRYS/opencgs — given its zero licensing cost and full extensibility — as a research and development sandbox for new physics, novel heater/furnace concepts, sensitivity-analysis-driven validation methodology, and eventual technology transfer of successfully developed sub-models back into a production context. This mirrors the existing pattern at Fraunhofer IISB itself, which already runs CrysMAS alongside OpenFOAM and Ansys rather than relying on any single tool for all physics.

**A note of caution on independent validation**: prospective users should not assume that opencgs's published validation for small-scale tin model experiments generalizes to industrial silicon CZ at production diameters, temperatures, and Grashof/Reynolds/Marangoni regimes, where melt turbulence, strong buoyancy-driven instabilities, and rotation-modulated flow structures — none of which are yet resolved in the public opencgs CZ implementation — are known (from the broader crystal-growth CFD literature) to materially affect interface shape, dopant/oxygen distribution, and defect formation. Any decision to deploy opencgs for industrially consequential predictions should include an explicit, scoped validation campaign against the target material system and scale, not an assumption of transferability from published Sn/Test-CZ results.

---

## 8. Key References

1. A. Enders-Seidlitz, J. Pal, K. Dadzis, "Development and validation of a thermal simulation for the Czochralski crystal growth process using model experiments," *Journal of Crystal Growth*, 593 (2022) 126750. https://doi.org/10.1016/j.jcrysgro.2022.126750
2. A. Wintzer, "Validation of multiphysical models for Czochralski crystal growth," PhD thesis, Technische Universität Berlin, 2024. https://doi.org/10.14279/depositonce-20957
3. A. Enders-Seidlitz, "Development of an open-source-based framework for multiphysical crystal growth simulations," FEniCS 2021 Conference. https://fenics2021.com/talks/enders-seidlitz.html
4. NEMOCRYS project software and publications listings, Leibniz-Institut für Kristallzüchtung (IKZ) / NEMOCRYS ERC project. https://nemocrys.github.io
5. NEMOCRYS/opencgs, NEMOCRYS/pyelmer, NEMOCRYS/objectgmsh, NEMOCRYS/opencgs_examples, NEMOCRYS/elmer-verification, NEMOCRYS/crystal-x, NEMOCRYS/test-cz-induction, NEMOCRYS/vertical-gradient-freeze repositories. https://github.com/nemocrys
6. Next Generation Multiphysical Models for Crystal Growth Processes (NEMOCRYS), CORDIS project record, European Commission, Grant Agreement No. 851768. https://cordis.europa.eu/project/id/851768
7. J. Pal, A. Enders-Seidlitz, K. Dadzis, "Model experiments for heater concepts in Czochralski crystal growth processes," Electromagnetic Processing of Materials 2021, Riga.
8. Fraunhofer IISB, "Equipment Simulation," Crystal Growth Laboratory capability overview (CrysMAS, OpenFOAM, Ansys toolchain description). https://www.iisb.fraunhofer.de/en/research_areas/materials/equipment_simulation.html
9. CrysMAS software manual/download, Fraunhofer IISB. https://download.iisb.fraunhofer.de/downloads/Manual/index.html
10. H.G. Park (and co-authors incl. J. Derby), "Simulation of heat transfer and convection during sapphire crystal growth in a modified heat exchanger method," *Journal of Crystal Growth*, 2013. https://doi.org/10.1016/j.jcrysgro.2013.01.017 (illustrative of CrysMAS use and validation practice at University of Minnesota in collaboration with Fraunhofer IISB)
11. "Modeling the growth of CZT by the EDG process," (Derby group / Fraunhofer IISB collaboration), describing CrysMAS's finite-volume method, view-factor radiation, and quasi-Newton solution strategy in detail.
12. "Process modeling of the industrial VGF growth process using the software package CrysVUN++," describing the CrysMAS + Cats2D coupled global/local modeling strategy characteristic of the Fraunhofer IISB approach.
13. Elmer FEM open-source multiphysics solver, CSC – IT Center for Science, Finland. https://www.csc.fi/web/elmer
14. C. Geuzaine, J.-F. Remacle, "Gmsh: A 3-D finite element mesh generator with built-in pre- and post-processing facilities," *International Journal for Numerical Methods in Engineering*, 79 (2009) 1309–1331.
15. A. Sabanskis et al., "A Coupled Approach to Compute the Dislocation Density Development during Czochralski Growth and Its Application to the Growth of High-Purity Germanium (HPGe)," *Crystals*, 13 (2023) 1440 — example of NEMOCRYS-ecosystem coupling to stress/dislocation modeling. https://doi.org/10.3390/cryst13101440
16. STR Group, "CGSim — Software for Modeling of Crystal Growth, Epitaxy, and Semiconductor Devices" (referenced for third-party benchmarking context). https://str-soft.com/software/cgsim/


---

> [!NOTE]
> 
> Generated by Claude.ai
>
> Model: Sonet 5
>
> Prompt: Write a comprehensive, technically rigorous report evaluating the suitability of NEMOCRYS/opencgs for high-fidelity numerical simulation of the Czochralski (CZ) crystal growth process. The report should critically assess NEMOCRYS/opencgs's capabilities, limitations, required extensions, and practical implementation challenges. It should also provide a detailed comparison with CrysMAS, the dedicated crystal-growth simulation software developed by the Fraunhofer Institute for Integrated Systems and Device Technology (Fraunhofer IISB). The report should be written for researchers and engineers involved in semiconductor crystal growth, computational fluid dynamics (CFD), heat transfer, and multiphysics simulation.
> Objectives
> Determine whether NEMOCRYS/opencgs can serve as a viable platform for industrial-grade CZ crystal growth simulation.
> Identify which physical phenomena can be modeled using standard NEMOCRYS/opencgs capabilities and which require custom development.
> Compare NEMOCRYS/opencgs with CrysMAS regarding physics coverage, numerical methods, validation status, industrial readiness, scalability, extensibility, and usability.
> Assess the effort required to build a CZ simulation environment in NEMOCRYS/opencgs that approaches the capabilities of CrysMAS.
> Provide recommendations for research, academic, and industrial use cases.
> Provide key references. Show the output in Markdown format.
