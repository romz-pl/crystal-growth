# Elmer FEM for High-Fidelity Czochralski Crystal Growth Simulation: A Critical Evaluation and Comparison with CrysMAS

## Executive Summary

Elmer FEM, the open-source multiphysics finite element package developed and maintained by CSC – IT Center for Science (Finland), is **not** a purpose-built crystal growth code out of the box, but it has become a credible open-source foundation for Czochralski (CZ) process modelling over the last decade, principally through the work of the NEMOCRYS project group at the Leibniz Institute for Crystal Growth (IKZ). Elmer natively provides the electromagnetic, heat transfer/phase-change, and surface-to-surface radiation solvers needed for a "global furnace" thermal model of a CZ system, and these have been independently verified against analytical solutions and validated against dedicated model experiments. However, Elmer's built-in incompressible flow solver is widely regarded — including by developers who have worked with it in this context — as inadequate for buoyancy-, rotation-, and Marangoni-driven melt convection at the Grashof/Marangoni numbers relevant to industrial CZ growth, and Elmer has **no native capability** for free-surface (meniscus) tracking, crystal-diameter control, dopant/impurity segregation, or thermoelastic dislocation-density modelling. Closing these gaps requires either substantial custom Fortran/C solver development within Elmer, or external coupling — most maturely via OpenFOAM for melt/gas flow (through the EOF-Library or preCICE) — and results in a multi-code, multi-mesh simulation environment rather than a single integrated tool.

CrysMAS, developed since the late 1990s by the Fraunhofer Institute for Integrated Systems and Device Technology (IISB) as the unification of the earlier STHAMAS and CrysVUn codes, is a dedicated, commercially licensed finite-volume crystal growth simulator with native, tightly integrated models for global furnace heat transfer (conduction, convection, view-factor-based radiation), melt/gas flow, phase change with interface tracking, quasi-steady and transient growth, dopant segregation, and (via coupled modules) thermoelastic stress and dislocation density — validated over more than two decades against industrial CZ, VGF, and related growth processes for silicon, GaAs, sapphire, and CdZnTe, among others.

**Bottom line:** Elmer is a viable and increasingly well-validated platform for **research-grade, thermally-focused** CZ simulation (heat transfer, EM heating, phase change, moving boundaries), and is an excellent choice where open-source transparency, customizability, and zero licensing cost matter more than turnkey completeness. It is **not** currently a drop-in substitute for CrysMAS's integrated, validated, industrial-grade capability set, particularly for melt convection instabilities, dopant transport, and mechanical/defect prediction. Reaching CrysMAS-equivalent capability in Elmer is achievable but requires a multi-year, multi-person software engineering effort layered on top of domain expertise — which is effectively what NEMOCRYS, the FEniCS-based "crystal-x", and related projects represent, still in progress as of 2026.

---

## 1. Introduction and Scope

### 1.1 The CZ Modelling Problem

Czochralski growth is a moving-boundary, multiphysics process in which a seed crystal is pulled from a rotating melt held in a rotating crucible, inside a furnace with resistive or inductive heaters, radiation shields, gas flow (often under partial vacuum or inert atmosphere), and, in many industrial variants, applied magnetic fields (static, cusp, or traveling/rotating fields — CZ, MCZ, or EMCZ). A high-fidelity simulation must resolve, at minimum:

- Electromagnetic heating (resistive or induction) and, where present, magnetohydrodynamic (MHD) body forces from applied magnetic fields.
- Conductive, convective, and radiative heat transfer across solid furnace parts, the crystal, the melt, and the gas/vacuum ambient, including enclosure (surface-to-surface) radiation with view factors, often with non-grey and non-diffuse effects.
- Buoyancy-driven, rotation-driven, and Marangoni (thermocapillary) melt convection, frequently at Grashof numbers where the flow is transitional or turbulent and subject to well-documented instabilities.
- A moving/deforming solid–liquid interface (crystallization front) and a moving/deforming free melt surface (meniscus), coupled to global mass and heat balance and to a diameter-control algorithm.
- Species (dopant/impurity) transport and segregation at the growing interface, governing radial and axial resistivity/doping uniformity.
- Thermoelastic stress in the growing crystal, and its relation to dislocation generation (e.g., via the Alexander–Haasen or similar models).
- Coupling of all of the above across vastly different length and time scales, with pulling-rate-driven mesh deformation (ALE) over process durations of many hours.

No single "one-click" open-source tool covers this entire scope with industrial validation. The question this report addresses is how close **Elmer** — a general-purpose multiphysics FEM package — can get, and at what cost, relative to the dedicated tool **CrysMAS**.

### 1.2 Method

This assessment draws on Elmer's solver documentation and source structure, the published NEMOCRYS body of work (thermal CZ models in Elmer, verification/validation studies, EOF-Library and preCICE coupling to OpenFOAM, and the parallel FEniCS-based "crystal-x" effort), published CrysMAS application papers across silicon, sapphire, and CdZnTe growth, and the broader crystal growth simulation literature (CGSim, FEMAG-CZ, CrysVUn) for context on what "industrial-grade" capability looks like.

---

## 2. Elmer: Architecture and Native Capabilities Relevant to CZ Growth

### 2.1 General Architecture

Elmer is a Fortran-based, MPI-parallel finite element multiphysics solver with a modular "solver" architecture: each physical field (heat equation, Navier–Stokes, electrostatics/magnetodynamics, elasticity, etc.) is implemented as a separate solver module that can be coupled at the level of the global equation system or through a Gauss–Seidel-type outer iteration. Meshing is external (commonly Gmsh, with Elmer's own `ElmerGrid` for format conversion and partitioning), and case setup is driven by the Solver Input File (`.sif`), a text-based keyword format, or via the graphical ElmerGUI. A Python interface, **pyelmer**, developed specifically for crystal growth work at IKZ, wraps `.sif` generation in an object-oriented layer that manages dependencies between bodies, boundaries, materials, and solvers, substantially reducing setup error rates for multi-body CZ geometries.

### 2.2 Electromagnetics

Elmer provides a time-harmonic (frequency-domain) magnetodynamics solver suitable for induction heating calculations, which is directly applicable to CZ furnaces with RF or line-frequency induction coils. This has been independently verified: NEMOCRYS verification cases compare Elmer's inductive heating solution for a cylinder in an infinitely long coil against an analytical solution, and separately verify heat conduction and radiation between concentric spherical shells, with deviations below roughly 1% (in some reported cases as low as 0.02%). This gives reasonable confidence that Elmer's core EM and heat-conduction/radiation discretizations are numerically correct for the axisymmetric geometries typical of CZ furnace models. Elmer's EM solver handles resistive (Joule) heating and induction heating; it does not natively provide the Lorentz-force body-force coupling into a melt-flow solver in a validated, turnkey way for CZ-scale applied fields — this coupling has to be constructed by the user, and is one of the items still listed as "in progress" in NEMOCRYS's own verification roadmap (impedance boundary conditions, Lorentz forces).

### 2.3 Heat Transfer and Phase Change

Elmer's heat equation solver supports:
- Conduction with temperature-dependent material properties.
- Surface-to-surface (enclosure) radiation with automatic or user-supplied view factors, suitable for the radiation-dominated heat exchange typical of high-temperature CZ furnaces (temperature-dependent emissivity is explicitly listed by NEMOCRYS as a verification case still being finalized).
- Phase change (latent heat release/absorption) via an enthalpy or effective-heat-capacity formulation, coupled to a moving mesh so that the crystallization front is tracked as a genuine moving interface rather than a fixed-position approximation.

The 2022 NEMOCRYS study by Enders-Seidlitz, Pal, and Dadzis (*Journal of Crystal Growth* 593, 126750) is the most rigorous open validation of this capability to date: a full axisymmetric CZ thermal model — time-harmonic EM for inductive heating, steady-state heat transfer with surface-to-surface radiation and phase change, convective gas cooling via heat transfer coefficients, and melt convection approximated by an **effective thermal conductivity** rather than solved flow — was built in Elmer and validated against a dedicated tin model-growth experiment with in-situ measurements. Critically, this validation showed that the treatment of gas convection (via HTCs) and melt convection (via effective conductivity) were the parameters most sensitive to matching experimental accuracy, i.e., the very phenomena Elmer does not natively resolve as real flow fields. A 2025 follow-on (*Computer Methods in Applied Mechanics and Engineering*, also NEMOCRYS-linked, and the parallel FEniCS-based "Multiphysics simulation of crystal growth with moving boundaries in FEniCS" paper, *J. Cryst. Growth* 661, 128155) extended this to a 2D/3D model coupling Elmer (EM, heat transfer, phase change) with OpenFOAM (melt flow), validated with a CsI model experiment, explicitly targeting oxide/fluoride growth systems.

**Assessment:** Elmer's thermal/EM/phase-change core is genuinely strong, independently verified, and validated against real experiments for CZ-relevant geometries. This is the part of the CZ problem where Elmer is closest to industrial-grade dedicated tools.

### 2.4 Fluid Flow (Melt and Gas Convection)

This is Elmer's principal weak point for CZ applications, and it is acknowledged as such by the developers of the EOF-Library coupling tool, who state plainly that although Elmer has a CFD solver, they "found it incapable to solve flows" at the regimes relevant to their industrial MHD/free-surface problems. Elmer's native incompressible Navier–Stokes solver is general-purpose (used across many non-crystal-growth applications) and lacks:
- Mature turbulence closures validated for the transitional, buoyancy- and rotation-driven regimes seen in CZ melts (Grashof numbers commonly 10⁶–10⁹, with oscillatory and non-axisymmetric instabilities well documented in the crystal growth literature — Kelvin–Helmholtz-type shear instabilities, baroclinic and centrifugal instabilities from crucible/crystal counter-rotation, and Marangoni-driven surface flow).
- Native free-surface tracking suitable for a deforming melt meniscus under surface tension, wetting-angle, and growth-angle constraints.
- Validated LES/RANS treatments comparable to what has been developed and applied specifically for CZ silicon growth with traveling magnetic fields in the literature (e.g., Krauze et al.'s LES applicability studies), which were performed using dedicated crystal growth codes and academic in-house solvers rather than Elmer.

As a direct consequence, the NEMOCRYS strategy — and the most credible published route to date — has been to **not** attempt melt/gas flow inside Elmer, and instead couple Elmer (EM + heat transfer + phase change) to **OpenFOAM** (flow) via either the EOF-Library (an MPI-based, mesh-to-mesh interpolating coupler originally built for MHD-with-free-surface problems at the University of Latvia) or the more general **preCICE** coupling library (used in a Dirichlet–Neumann surface-coupling scheme for 2D steady-state heat transfer/gas flow coupling, benchmarked against both Elmer–OpenFOAM and FEniCS–OpenFOAM implementations).

**Assessment:** For any CZ simulation in which melt convection detail (thermal striations, interface deflection from flow, dopant mixing, oscillatory transitions) matters — which is essentially all industrially relevant CZ modelling — Elmer alone is insufficient, and a coupled Elmer+OpenFOAM (or Elmer+FEniCS+OpenFOAM) architecture is currently the state of the art in the open-source ecosystem, not a mature single-code solution.

### 2.5 Free Surface / Moving Boundary Treatment

Elmer supports Arbitrary Lagrangian–Eulerian (ALE) mesh movement and has been used for moving-boundary problems (e.g., ice-sheet modelling, one of Elmer's most mature application domains, which is mesh-deformation-heavy). For CZ growth, ALE is used in the NEMOCRYS models to track the crystallization front as it advances, and to move the crystal/melt boundary consistently with a prescribed or computed pulling rate. However, a full **free melt surface** (meniscus) solution — coupling surface tension, hydrostatic pressure, growth angle, and diameter feedback control into the moving mesh — is not a standard, packaged Elmer feature; it must be implemented via custom boundary conditions and mesh-update logic, or handled by the flow solver in the OpenFOAM side of a coupled scheme (which does have VOF/interface-capturing methods, though these still need CZ-specific configuration for the crystallization meniscus rather than a generic free surface).

### 2.6 Structural/Thermoelastic and Defect Modelling

Elmer includes a linear elasticity solver, and thermoelastic stress from a computed temperature field is, in principle, straightforward to compute as a *sequential* (one-way coupled) post-processing step. This has precedent in the broader FEM crystal-growth literature (e.g., thermal stress studies in Ge CZ growth using Elmer, referenced in the FEniCS moving-boundary paper's bibliography). However, Elmer has **no native dislocation-density or defect model** (no Alexander–Haasen-type plasticity/dislocation solver as a packaged module); any such capability requires custom solver development, typically as a user-defined Fortran solver module compiled against Elmer's solver API.

### 2.7 Species Transport and Segregation

Elmer's general advection–diffusion solver can, in principle, be configured for dopant transport, but there is **no packaged, validated segregation model** for CZ growth (e.g., effective segregation coefficient models linking interface growth rate, boundary-layer thickness, and melt flow, of the kind long established in the crystal growth literature and packaged in dedicated codes). This is squarely in "requires custom development" territory for Elmer.

### 2.8 Summary Table: Elmer Native Capability vs. Requirement

| Physical phenomenon | Elmer native capability | Status |
|---|---|---|
| Resistive/induction EM heating | Time-harmonic magnetodynamics solver | Native, verified |
| Conduction heat transfer | Heat equation solver, temp.-dependent properties | Native, verified |
| Surface-to-surface radiation | View-factor enclosure radiation | Native, verified (some edge cases, e.g., T-dependent emissivity, still being finalized in verification suites) |
| Phase change / moving crystallization front | Enthalpy/effective-Cp method + ALE | Native, validated against model experiments |
| Melt/gas buoyant & rotational convection | Generic incompressible N-S solver | Native but inadequate at relevant Gr/Ma; requires external CFD (OpenFOAM) coupling |
| MHD body forces (applied fields) | Not a packaged coupling | Requires custom Lorentz-force coupling (in progress in verification suites) |
| Free melt surface / meniscus tracking | ALE mesh movement primitive | No packaged CZ meniscus model; custom or via OpenFOAM VOF |
| Diameter control | None | Custom control-loop development required |
| Dopant/impurity segregation | Generic advection-diffusion solver | No packaged segregation model; custom development required |
| Thermoelastic stress | Linear elasticity solver | Native (one-way coupled), usable with custom setup |
| Dislocation density / defect prediction | None | Requires custom solver module |
| Turbulence closures for transitional convection | Standard RANS options, limited validation for this regime | Largely inadequate; best routed to OpenFOAM |

---

## 3. CrysMAS: Architecture and Capabilities

### 3.1 Origins and Positioning

CrysMAS is developed by the Crystal Growth Laboratory (Materials department) of Fraunhofer IISB, Erlangen, as the unification of two earlier, separately licensed IISB codes — **STHAMAS** (global furnace/heat transfer) and **CrysVUn** (crystal growth-specific solidification/flow) — brought together into one package and licensed worldwide to industry and research institutes. Its development is tied to specific, named contributors (Leister, Fainberg, Kurz, Metzger, Hainke, Dagner, and collaborators at the University of Timișoara) and continues under Jochen Friedrich's leadership at IISB, whose long-term modelling work spans Czochralski silicon, GaAs and CaF₂ vertical gradient freeze, and other systems, and who received the DGKK Prize in 2024 in part for this body of work.

### 3.2 Numerics

CrysMAS solves the energy conservation (and related transport) equations using the **finite volume method**, with an **unstructured triangular grid** for the global furnace domain (enabling complex, multi-part furnace geometries with heaters, insulation, crucibles, and shields) and a **structured grid** specifically for the heat transfer, fluid flow, and phase-change computations within the growth ampoule/crucible region itself — a hybrid meshing strategy tuned for the different geometric and physical demands of "the whole furnace" versus "the growth cell." Radiative heat transfer is computed via **view factors with an enclosure method**, directly comparable in principle to Elmer's approach but embedded natively rather than as a general-purpose add-on. A key operational feature is that CrysMAS is typically run in an **inverse/control mode**: furnace **setpoint temperatures** are specified as boundary data, and the corresponding **heater powers are solved as unknowns**, using a quasi-Newton iterative method to converge — a workflow that matches how industrial furnaces are actually operated and controlled, and is not a standard mode of operation for Elmer.

### 3.3 Physics Coverage

Published applications document CrysMAS handling:
- Full furnace-scale heat transfer, convection, and radiation for CZ, VGF, EDG, and heat-exchanger-method growth.
- Melt and gas flow (thermal and forced/rotational convection) within the growth cell.
- Solid–liquid interface tracking and phase change, including for high-melting-point and optically semi-transparent materials (sapphire).
- Dopant/impurity distribution studies (documented across CdZnTe and related II–VI/III–V growth work).
- Coupled or follow-on thermoelastic stress analysis for crystal quality assessment (part of the broader IISB modelling toolchain around CrysMAS).
- Quasi-steady-state (QSS) time-dependent growth simulation, in which the process is decomposed into a sequence of steady-state solves along a growth-rate ramp — an efficient, validated approach for practical process-length simulations, used, for example, in heat-exchanger-method sapphire growth studies.

### 3.4 Validation and Industrial Track Record

CrysMAS's validation record is extensive and spans more than two decades of peer-reviewed application papers across multiple material systems and growth methods (CZ silicon, VGF GaAs and CdZnTe, heat-exchanger-method sapphire, EDG CZT), authored both by Fraunhofer IISB staff and by external academic collaborators (e.g., University of Minnesota, Washington State University, Korea Polytechnic University) who were given access to the code for specific studies. This breadth of independent, cross-institutional application is a meaningfully different validation profile from Elmer's CZ usage, which — while methodologically rigorous — is concentrated in a smaller number of groups (principally IKZ/NEMOCRYS) and a shorter track record specific to crystal growth (roughly since 2019–2020, versus CrysMAS's lineage stretching back to the 1990s).

### 3.5 Licensing and Access Model

CrysMAS is proprietary, commercially licensed software; access requires a license from Fraunhofer IISB, and the source code is not open for inspection or modification by licensees in the way Elmer's is. This has direct implications for extensibility (Section 5) and for suitability in contexts requiring source-level transparency, reproducibility by third parties, or integration into fully open research pipelines.

---

## 4. Head-to-Head Comparison

| Dimension | Elmer (+ required extensions) | CrysMAS |
|---|---|---|
| **Numerical method** | Finite element method (FEM), MPI-parallel | Finite volume method (FVM); unstructured triangular grid (global furnace) + structured grid (growth cell) |
| **Electromagnetics** | Native time-harmonic magnetodynamics, verified | Native, integrated for induction/resistive heating |
| **Radiation** | Native surface-to-surface / view-factor enclosure radiation | Native view-factor enclosure method |
| **Phase change / moving interface** | Native (enthalpy method + ALE), validated | Native, long-established, validated across materials |
| **Melt/gas convection** | Not natively adequate; requires OpenFOAM coupling (EOF-Library or preCICE) | Native, integrated within the growth-cell solver |
| **MHD (applied magnetic fields)** | Custom Lorentz-force coupling required; not fully packaged | Historically addressed in IISB's broader toolchain for CZ with magnetic fields |
| **Free surface / meniscus tracking** | Not packaged; custom or via external CFD VOF | Native to growth-cell solidification model |
| **Diameter control** | Not packaged; custom control loop | Native to CZ process modelling logic |
| **Dopant segregation** | Not packaged; custom advection-diffusion setup | Native, validated across multiple material systems |
| **Thermoelastic stress** | Native linear elasticity (one-way coupled), usable with setup | Available via coupled/follow-on modules in the IISB toolchain |
| **Dislocation density / defects** | Not available; custom solver module needed | Available via associated IISB modelling capability |
| **Furnace operation mode** | Boundary-condition-driven (user sets BCs/HTCs directly) | Native inverse mode: setpoints in, heater powers solved as unknowns (quasi-Newton) — matches real furnace control |
| **Time-dependent growth** | Transient/ALE possible but computationally heavy for full-length process; largely research-scale demonstrations to date | Native QSS (quasi-steady-state) ramping strategy, validated as an efficient practical approach |
| **Validation breadth** | Verified numerics (analytical benchmarks); validated against model experiments (Sn, CsI) at IKZ; concentrated in one research group, since ~2019 | Validated over 20+ years across CZ, VGF, EDG, heat-exchanger-method growth, multiple materials (Si, GaAs, CdZnTe, sapphire, CaF₂), multiple institutions |
| **Industrial readiness** | Emerging; not yet demonstrated for full 3D industrial-scale CZ with all coupled physics in one workflow | Established; licensed and used by industry and research institutes worldwide |
| **Scalability (HPC)** | MPI-parallel FEM; scalability is a core Elmer strength (used at large scale in, e.g., ice-sheet modelling) | Scalable within its FVM framework; typically deployed on institutional HPC clusters (e.g., at Fraunhofer IISB) but scaling characteristics are less publicly documented |
| **Extensibility** | Fully open source (Fortran/C, GPL-family license); custom solver modules can be written and compiled against the solver API; Python front end (pyelmer) available | Closed source; extensibility limited to whatever configuration options and coupled modules IISB exposes to licensees |
| **Usability / setup workflow** | Text-based `.sif` case files or ElmerGUI; substantially improved by pyelmer's object-oriented Python layer for crystal-growth-specific setups, but still requires the user to assemble multiphysics coupling manually | Purpose-built GUI and workflow for crystal growth furnace setup; heater/setpoint-driven configuration matches process engineers' mental model directly |
| **Cost** | Free, open source | Commercial license fee (cost not publicly listed; contact Fraunhofer IISB) |
| **Transparency/reproducibility** | Full source visibility; independent verification/reproduction is possible and has been explicitly cited as a motivation for the NEMOCRYS open-source effort | Proprietary; reproduction of results by third parties without a license is not possible |
| **Community / ecosystem** | General multiphysics FEM community (large, but crystal-growth-specific subset is small); active NEMOCRYS GitHub organization with verification cases, example models (test-cz-induction), and a parallel FEniCS-based effort (crystal-x) | Focused user community of licensees; tied to IISB's own research and consulting activities (equipment simulation services) |

---

## 5. Effort Required to Reach CrysMAS-Equivalent Capability in Elmer

Bringing Elmer to a capability level approaching CrysMAS for CZ growth is not a configuration exercise; it is a **multi-year software and validation program**, and the ongoing NEMOCRYS/crystal-x work is a reasonable real-world estimate of its scope and pace. The main work packages are:

1. **Melt and gas flow solver integration.** Adopt a coupled Elmer+OpenFOAM (or Elmer+FEniCS+OpenFOAM) architecture via EOF-Library or preCICE, since Elmer's native flow solver is not considered adequate by the tool's own crystal-growth-focused developers. This requires building and maintaining mesh-interpolation and coupling infrastructure, handling two separate meshing/pre-processing pipelines, and validating the coupled solution against experiment — a task already substantially (but not completely) done by NEMOCRYS as of the 2025 published moving-boundary/coupled works.
2. **Free surface and diameter-control logic.** Implement meniscus tracking (surface tension, growth angle, hydrostatic balance) and a diameter-control feedback loop, either as custom Elmer boundary conditions/mesh-update code or via the flow solver's interface-capturing (VOF) capability, adapted specifically for crystallization physics rather than a generic two-fluid interface.
3. **MHD body-force coupling.** Complete and validate Lorentz-force coupling from the EM solver into the flow solver for systems with applied static or traveling magnetic fields (relevant to industrial MCZ/EMCZ) — explicitly flagged as still "in progress" in Elmer verification work.
4. **Dopant transport and segregation model.** Implement and validate a segregation model tied to local growth rate and boundary-layer/flow conditions at the interface — currently absent as a packaged capability.
5. **Thermoelastic stress and defect prediction.** Extend the existing linear elasticity solver with a validated dislocation-density (e.g., Alexander–Haasen-type) model as a custom solver module, and establish a one-way or iterative coupling to the thermal/flow solution.
6. **Transient, full-process-length simulation performance.** Either adopt and validate a quasi-steady-state (QSS) ramping strategy analogous to CrysMAS's, or invest in the HPC/algorithmic work (adaptive time-stepping, mesh adaptivity for the moving interfaces) needed to make full transient 3D simulation of an entire pull cycle computationally tractable.
7. **Workflow and usability layer.** Extend pyelmer/opencgs-style tooling to abstract away multi-code coupling, multi-mesh management, and iterative/inverse (setpoint-to-heater-power) solution modes, so that a process engineer can operate the environment without deep FEM/solver expertise — mirroring CrysMAS's setpoint-driven usability.
8. **Verification and validation program.** Systematically verify each new solver/coupling against analytical or benchmark solutions (as NEMOCRYS has begun doing), and validate against a broad set of model experiments and, ideally, industrial data across multiple materials — the multi-decade, multi-institution validation base that underpins confidence in CrysMAS today.

**Realistic assessment:** items 1–3 are substantially underway (NEMOCRYS, EOF-Library, preCICE coupling, crystal-x/FEniCS parallel effort) and represent perhaps 3–5 years of a small specialized team's work to reach solid 2D/3D validated status; items 4–6 are largely not yet started in the open literature for Elmer specifically and would add further years; item 7 is an ongoing, incremental software engineering task; item 8 is continuous and never fully "complete," but needs to reach a critical mass of independent validation before industrial users would trust it in place of an established code. In aggregate, a **5–10 year effort by a dedicated, well-funded research group** (which is essentially the trajectory NEMOCRYS is on) is a realistic estimate to approach — not necessarily match — CrysMAS's current integrated capability and validation base, and even then, licensing/support/industrial-track-record parity is a separate, non-technical hurdle.

---

## 6. Recommendations

### 6.1 For Academic Research

Elmer (optionally coupled to OpenFOAM/FEniCS via EOF-Library or preCICE) is a strong choice when:
- The research question centers on furnace-scale heat transfer, induction heating, or phase-change/interface dynamics, where Elmer's native solvers are verified and validated.
- Open-source transparency and reproducibility are important (e.g., for publishing a fully inspectable, third-party-reproducible model, as NEMOCRYS explicitly motivates).
- The group has, or is willing to build, in-house FEM/solver development capability, since the CZ-specific gaps (free surface, segregation, MHD coupling, defects) require custom code.
- Budget constraints preclude commercial licensing.

CrysMAS remains preferable for academic groups whose research questions concern melt convection instabilities, dopant distribution, or thermoelastic/defect prediction directly, and who can obtain a license, since these capabilities are native and validated rather than requiring in-house development.

### 6.2 For Industrial Use

CrysMAS (or comparable dedicated commercial tools such as CGSim or FEMAG-CZ) remains the more defensible choice for **production process development and qualification** today, given its integrated physics coverage, setpoint-driven operational mode that matches how furnaces are actually run, and multi-decade validation track record across materials and growth methods. Elmer-based workflows are not yet demonstrated at a comparable level of integrated, validated, industrial-scale 3D capability for CZ growth specifically, and adopting them for production decisions would currently mean absorbing the R&D risk described in Section 5 in-house.

A pragmatic middle path for industrial R&D groups: use Elmer for **specific, decoupled sub-studies** where its native strengths apply directly (e.g., induction coil/heater design and furnace thermal-field optimization, where EM+radiation+conduction dominate and melt-flow detail is secondary), while continuing to rely on CrysMAS or another dedicated tool for full coupled-physics production simulation.

### 6.3 For Groups Considering Building an Elmer-Based CZ Environment

- Start from and contribute to the existing NEMOCRYS open-source assets (elmer-verification, test-cz-induction, opencgs/pyelmer) rather than starting from scratch; this is by far the most mature Elmer-for-CZ codebase publicly available.
- Prioritize the Elmer–OpenFOAM (EOF-Library) or Elmer/FEniCS–OpenFOAM (preCICE) coupling path for melt/gas flow rather than attempting to extend Elmer's native flow solver, in line with the explicit assessment of Elmer's own crystal-growth-focused developers.
- Treat free-surface/diameter-control, segregation, and defect modelling as dedicated, separately staffed development work packages, not incidental additions.
- Build validation into the plan from day one, using model experiments (as IKZ has done with tin and CsI systems) rather than relying solely on cross-code or literature comparison.

---

## 7. Key References

1. Enders-Seidlitz, A., Pal, J., Dadzis, K. (2022). *Development and validation of a thermal simulation for the Czochralski crystal growth process using model experiments.* Journal of Crystal Growth, 593, 126750. https://doi.org/10.1016/j.jcrysgro.2022.126750
2. NEMOCRYS project (Leibniz Institute for Crystal Growth, IKZ). *Next Generation Multiphysical Models for Crystal Growth Processes* — software repositories including `elmer-verification`, `test-cz-induction`, `crystal-x`, `pyelmer`, `opencgs`. https://nemocrys.github.io/software/software.html
3. (2025). *Multiphysics simulation of crystal growth with moving boundaries in FEniCS.* Journal of Crystal Growth, 661, 128155; and companion work on coupled Elmer/FEniCS + OpenFOAM CZ modelling. https://doi.org/10.1016/j.jcrysgro.2025.128155 (see also the related Computer Methods in Applied Mechanics and Engineering publication on the same coupled model, ScienceDirect S0045782525000556).
4. Vencels, J., Jakovics, A., Geza, V., Scepanskis, M. (2017). *EOF Library: Open-Source Elmer and OpenFOAM Coupler for Simulation of MHD With Free Surface.* arXiv:1707.04080; and *EOF-Library: Open-source Elmer FEM and OpenFOAM coupler for electromagnetics and fluid dynamics*, SoftwareX / ScienceDirect S2352711018302164.
5. Dadzis, K., et al. *Coupled heat transfer and gas flow simulation in Czochralski crystal growth* (preCICE-based Elmer/FEniCS–OpenFOAM surface coupling), ECCOMAS Congress 2022 contribution.
6. Friedrich, J. (2020). *Erlangen — An Important Center of Crystal Growth and Epitaxy: Major Scientific Results and Technological Solutions of the Last Four Decades.* Crystal Research and Technology. https://doi.org/10.1002/crat.201900053 (history and development of STHAMAS, CrysVUn, and CrysMAS).
7. Fraunhofer IISB. *CrysMAS Manual.* https://download.iisb.fraunhofer.de/downloads/Manual/index.html
8. Fraunhofer IISB, Crystal Growth Laboratory / Equipment Simulation group page. https://www.iisb.fraunhofer.de/en/research_areas/materials/equipment_simulation.html
9. Applications of CrysMAS across materials/processes: heat-exchanger-method sapphire growth (ScienceDirect S0022024813000481); CdZnTe by EDG process (Modeling the growth of CZT by the EDG process, ResearchGate 241196530); *Modeling the Crystal Growth of Cadmium Zinc Telluride: Accomplishments and Future Challenges* (ResearchGate 232025178).
10. Krauze, A., Jēkabsons, N., Muižnieks, A., Sabanskis, A., Lācis, U. (2010). *Applicability of LES turbulence modeling for CZ silicon crystal growth systems with traveling magnetic field.* Journal of Crystal Growth, 312, 3225–3234. https://doi.org/10.1016/j.jcrysgro.2010.07.048 (context on melt convection instability/turbulence modelling demands not natively met by Elmer).
11. Elmer FEM documentation and source (CSC – IT Center for Science, Finland). https://www.elmerfem.org

---

*This report reflects the published, verifiable state of Elmer- and CrysMAS-based CZ modelling as of mid-2026. Given the active pace of NEMOCRYS and related open-source crystal-growth simulation development, readers intending to make platform decisions for new projects should check the cited GitHub repositories and journal databases for more recent releases and validation studies before finalizing a choice.*

---

> [!NOTE]
> 
> Generated by Claude.ai
>
> Model: Sonet 5
>
> Prompt: Write a comprehensive, technically rigorous report evaluating the suitability of Elmer for high-fidelity numerical simulation of the Czochralski (CZ) crystal growth process. The report should critically assess Elmer's capabilities, limitations, required extensions, and practical implementation challenges. It should also provide a detailed comparison with CrysMAS, the dedicated crystal-growth simulation software developed by the Fraunhofer Institute for Integrated Systems and Device Technology (Fraunhofer IISB). The report should be written for researchers and engineers involved in semiconductor crystal growth, computational fluid dynamics (CFD), heat transfer, and multiphysics simulation.
> Objectives
> Determine whether Elmer can serve as a viable platform for industrial-grade CZ crystal growth simulation.
> Identify which physical phenomena can be modeled using standard Elmer capabilities and which require custom development.
> Compare Elmer with CrysMAS regarding physics coverage, numerical methods, validation status, industrial readiness, scalability, extensibility, and usability.
> Assess the effort required to build a CZ simulation environment in Elmer that approaches the capabilities of CrysMAS.
> Provide recommendations for research, academic, and industrial use cases.
> Provide key references. Show the output in Markdown format.
