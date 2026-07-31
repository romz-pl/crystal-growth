# Evaluating Basilisk Flow Solver for High-Fidelity Czochralski Crystal Growth Simulation: A Comparative Assessment Against CrysMAS

## Executive Summary

Basilisk is a general-purpose, open-source octree/quadtree adaptive-mesh CFD framework built around a volume-of-fluid (VOF)/embedded-boundary Navier–Stokes core, originally developed for interfacial multiphase flows (atomization, wave breaking, bubble dynamics). CrysMAS is a purpose-built, finite-volume "global furnace" simulator developed at Fraunhofer IISB specifically for Czochralski (CZ) and related melt-growth processes, with two decades of validation against industrial pullers.

The central finding of this report is that **Basilisk is not a drop-in substitute for CrysMAS**, and cannot become an industrial-grade CZ tool without a substantial custom-development program. Basilisk's adaptive-mesh Navier–Stokes/VOF core is excellent for the *melt convection and free-surface sub-problem*, but CZ growth is fundamentally a **conjugate, multi-domain, multi-physics global furnace problem** — surface-to-surface and participating-media radiation across a graphite/quartz/gas cavity, resistive or RF electromagnetic heating, conduction in multiple solids, moving/deforming solid–liquid interfaces with latent heat release, and (optionally) dopant segregation — none of which exist as first-class Basilisk modules today.

Basilisk is best positioned as a **research vehicle for high-fidelity, resolved sub-models** (transient 3D melt convection, Marangoni-driven free-surface dynamics, meniscus shape, oscillatory/turbulent transition studies) that can be coupled — in the same spirit as the published CrysMAS↔OpenFOAM coupling — to a global thermal solver, rather than as a replacement for that global solver. CrysMAS remains the appropriate tool where industrial-readiness, validated radiation/EM physics, and engineering turnaround time dominate the requirements.

---

## 1. The Physics of Czochralski Growth: A Baseline for Comparison

Before assessing either tool, it is useful to lay out what a "complete" CZ simulation must capture, since this defines the yardstick against which both codes are judged.

| Physical domain | Phenomena |
|---|---|
| Melt hydrodynamics | Buoyancy-driven convection (Ra ~ 10⁶–10⁹), forced convection from crystal/crucible rotation, Marangoni (thermocapillary) convection at the free surface, transitional/turbulent flow, possible 3D non-axisymmetric instabilities |
| Free surface / interfaces | Deformable melt meniscus (capillary statics), deformable, non-planar solid–liquid growth interface, triple line at the crystal edge |
| Heat transfer | Conduction in crystal, melt, crucible, susceptor, insulation, and chamber components; convection in melt and cover gas; **surface-to-surface radiation** in a complex enclosure with view factors, possibly semi-transparent crystal/melt (participating-media radiation) |
| Phase change | Latent heat release/absorption at a moving, curved solid–liquid interface; interface position is a solution unknown, not a prescribed boundary |
| Electromagnetics | Resistive heater or RF/inductive coil heating; for MCZ/EMCZ, Lorentz-force coupling of applied magnetic fields to melt flow (magnetohydrodynamics) |
| Mass transfer | Dopant/impurity segregation at the growth interface, oxygen/carbon transport from crucible dissolution, gas-phase species transport (Ar flow, SiO/CO removal) |
| Mechanical/geometric | Crystal pulling and rotation, crucible rise, evolving free-boundary geometry over the whole (hours-long) process |
| Multi-scale coupling | Furnace-scale ("global") 2D axisymmetric thermal fields interacting with local 3D transient melt turbulence — the "global–local" or "2D–3D" coupling paradigm |

A genuinely industrial-grade CZ code must solve most of these simultaneously, over process timescales of many hours, on geometries that change slowly as the boule grows.

---

## 2. Basilisk Flow Solver: Native Capabilities

Basilisk's design centers on an octree/quadtree Cartesian adaptive mesh with wavelet-based refinement, targeting incompressible and low-Mach flows. Confirmed native solver families include:

- **Incompressible Navier–Stokes** (centered, projection-method formulation) with adaptive mesh refinement (AMR), documented and validated across a wide range of interfacial-flow problems.
- **Volume-of-Fluid (VOF)** interface tracking with a momentum-conserving, geometric (PLIC/height-function) reconstruction — the standard approach for capturing sharp, topology-changing free surfaces, extensively validated for bubbles, drops, jets, and breakup phenomena.
- **Surface tension**, via the Continuum/Continuous Surface Force or Continuous Surface Stress formulations, including well-balanced schemes that minimize parasitic currents — directly relevant to meniscus and Marangoni physics.
- **Saint-Venant / shallow-water and multilayer solvers**, of limited direct relevance to CZ.
- **Electrohydrodynamics (EHD)** module — solves electric-field-coupled interfacial flows, but this targets electrostatically stressed interfaces (e.g., electrospray, EHD atomization), not resistive/inductive Joule heating or magnetohydrodynamic Lorentz forcing.
- **Viscoelasticity** module — not relevant to silicon/oxide melts, but indicates the framework's extensibility pattern.
- **Embedded boundaries** for representing solid obstacles/complex geometry on the Cartesian octree grid, an alternative to body-fitted meshing.
- **MPI-parallel tree decomposition** giving good scalability on distributed-memory clusters, and GPU-oriented developments for the multigrid Poisson solver in newer releases.
- A **fourth-order-accurate variant** of the incompressible solver exists (published, quadtree-based), useful for high-Reynolds-number transitional/turbulent melt-flow studies where numerical dissipation must be minimized.

**What is native and strong for CZ purposes:** transient, adaptively resolved, 3D (or 2D-axisymmetric via Basilisk's own axisymmetric metric) melt convection with a deformable free surface, Marangoni stress, and rotation-driven flow (via a rotating reference frame or explicit Coriolis/centrifugal source terms the user adds). This is a non-trivial and genuinely valuable capability — it addresses exactly the sub-problem (melt turbulence, meniscus dynamics, interface deformation under flow) that dedicated global codes such as CrysMAS traditionally under-resolve because they run coarser, more empirical turbulence closures at furnace scale.

**What is absent natively:**
- No surface-to-surface or participating-media **radiative heat transfer** solver (no view-factor, radiosity, discrete-ordinates, or Monte Carlo radiation module) — a hard requirement for the furnace enclosure.
- No **electromagnetic/induction heating** solver (no eddy-current, vector-potential, or coupled EM-thermal module) — required for RF-heated CZ pullers and for any magnetic-field (MCZ) studies.
- No **solid-region multi-material conduction network** abstraction of the kind furnace codes use (heater, insulation, crucible, susceptor, gas cavity, chamber wall as distinct conjugate solid domains) — Basilisk can represent solids via embedded boundaries or as very-high-viscosity/zero-velocity "fluid" domains, but this is a workaround, not a designed capability.
- No **explicit solidification/latent-heat (enthalpy or Stefan-condition) module** — phase change with a moving, curved solid–liquid front and latent heat release is not part of the standard distribution and must be implemented (e.g., via an enthalpy-porosity or level-set/VOF-based Stefan condition analogous to what exists in the melting/solidification literature built on similar codes).
- No **dopant/impurity segregation model** (segregation coefficient, interface rejection/incorporation, boundary-layer transport) as a packaged tracer/scalar module — though Basilisk's general advection-diffusion tracer infrastructure could be adapted.
- No **quasi-steady process-scale time integration** framework for the slowly evolving geometry (crystal length growth, crucible rise, melt volume depletion) over an hours-long pull; Basilisk's timestep and mesh-adaptation machinery is designed for resolving fast interfacial dynamics, not for efficiently marching a multi-hour industrial process.
- No **furnace-level 2D axisymmetric global thermal solver with a graphical pre/post-processing environment** analogous to CrysMAS's engineering-oriented GUI, materials database, and hot-zone CAD import.

---

## 3. CrysMAS: Native Capabilities and Positioning

CrysMAS is a finite-volume code developed by the Crystal Growth Laboratory at Fraunhofer IISB, explicitly targeted at **global furnace simulation** of CZ (and related Bridgman/VGF-type) processes. Its defining characteristics, as documented in the crystal-growth literature:

- **Coupled global 2D axisymmetric solvers** for turbulent melt and gas convection in the rotating geometry.
- **Conjugate radiative, convective, conductive, and advective heat transport** across the entire furnace — heater, insulation, crucible, susceptor, melt, crystal, gas, and chamber — via a validated radiation/view-factor treatment integrated with the conduction/convection solve.
- **Latent heat release and solid–liquid interface tracking/deformation** as first-class, validated capabilities — the growth interface shape is a direct simulation output, compared routinely against experimental interface (striation-revealed) shapes.
- **Materials database and hot-zone/equipment-oriented pre-processing**, letting engineers build up a furnace geometry from standard component types (heaters, insulation rings, crucibles, pull rods) rather than authoring PDE code.
- **Demonstrated global-2D/local-3D coupling**, e.g., with OpenFOAM providing a local, transient 3D LES melt-flow model whose turbulent heat fluxes are fed back into the CrysMAS global thermal field — precisely the "resolved sub-model coupled to global furnace solver" architecture that this report recommends as Basilisk's natural role.
- Long **validation history** against model experiments (e.g., Fraunhofer IISB's own inductively/resistively heated model furnaces) and industrial silicon CZ practice, published continuously since the early 2000s.
- Used alongside, and interoperable in research pipelines with, other Fraunhofer/partner tools (e.g., Cats2D for VGF-type ampoule-scale modeling), reflecting an ecosystem built around global-furnace thermal analysis.

CrysMAS's principal limitation, relative to a general CFD framework like Basilisk, is that its melt-convection treatment is **historically coarser and more empirical at furnace scale** (RANS-type or even simplified turbulence closures, 2D-axisymmetric by default) — precisely why global-2D/local-3D coupling strategies (CrysMAS+OpenFOAM) were developed by its own user community to recover high-fidelity transient/turbulent melt behavior.

---

## 4. Side-by-Side Comparison

| Dimension | Basilisk Flow Solver | CrysMAS |
|---|---|---|
| **Design intent** | General-purpose adaptive-mesh CFD for interfacial/multiphase flows | Purpose-built global furnace simulator for melt crystal growth |
| **Mesh** | Octree/quadtree Cartesian AMR, embedded boundaries; excellent for sharp free-surface/interface resolution | Body-fitted finite-volume mesh for furnace geometry; standard for engineering hot-zone design |
| **Melt convection fidelity** | High — transient 3D, high-order options, minimal numerical dissipation, well suited to instability/transition studies | Typically coarser/RANS or steady approximations by default; improved via external 3D coupling |
| **Free surface / meniscus** | Native, sharp VOF/embedded-boundary tracking with validated surface-tension schemes | Present but generally simplified/prescribed relative to Basilisk's interface-resolving approach |
| **Radiative heat transfer** | **Absent** — no native module | **Native, validated, conjugate** with conduction/convection across the whole furnace |
| **Electromagnetic (resistive/inductive) heating** | **Absent** — EHD module addresses a different physics regime | **Native**, standard input for hot-zone design |
| **Magnetohydrodynamics (for MCZ)** | Not native; would require custom Lorentz-force source-term development | Available/extended in the broader IISB/partner tool ecosystem for MCZ studies |
| **Solidification / latent heat / moving interface** | **Absent as packaged module**; must be built (enthalpy method or Stefan condition atop VOF/level-set) | **Native and validated**, core capability |
| **Dopant/impurity segregation** | Not packaged; general tracer/advection-diffusion infrastructure could be adapted | Native or closely integrated with companion tools |
| **Multi-domain conjugate conduction (solids)** | Workaroundable via embedded boundaries/zero-flow regions; not a designed capability | Native, multi-material, database-driven |
| **Process-scale (hours) time integration with evolving geometry** | Not designed for this; AMR/timestep machinery targets fast interfacial dynamics | Native — this is the code's raison d'être |
| **Validation status for CZ** | None published for full CZ process; validation exists for the underlying NS/VOF/surface-tension numerics in unrelated multiphase-flow contexts | Extensive, published, industrial and model-experiment validation over ~20 years |
| **Industrial readiness** | Not industrial-ready for CZ without a large custom-development program | Industrial-ready; used by/licensed to crystal-growth industry |
| **Usability / GUI / workflow** | Code-centric (Basilisk C, a C99 dialect with a domain-specific preprocessor); no GUI; steep learning curve outside the CFD-research community | Engineering GUI, materials database, hot-zone builder; usable by process engineers without CFD/coding expertise |
| **Extensibility / openness** | Fully open-source, active academic community, transparent source, easy to bolt on new physics modules following existing patterns (EHD, viscoelastic modules as templates) | Proprietary/licensed; extension paths controlled by Fraunhofer IISB; not user-extensible in the same open sense |
| **Scalability** | Strong MPI parallel tree decomposition; some GPU support emerging | Adequate for 2D-axisymmetric global problems; 3D or coupled local models rely on external tools (e.g., OpenFOAM) for HPC-scale melt turbulence |
| **Cost / licensing** | Free, open-source | Commercial/licensed (research and industrial licensing via Fraunhofer IISB) |
| **Best-fit role** | Research tool for resolved sub-models: melt turbulence, meniscus/interface dynamics, instability studies, method development | Engineering tool for full-process, multi-physics, industrial hot-zone design and optimization |

---

## 5. What It Would Take to Bring Basilisk to CrysMAS-Level CZ Capability

Constructing a Basilisk-based environment that *approaches* CrysMAS's scope is a multi-year, multi-person research-software-engineering effort, not a modeling exercise. The major work packages:

1. **Radiative heat transfer module.** Implement (or couple externally, e.g., via a view-factor/radiosity library or a Monte Carlo ray-tracer) surface-to-surface radiation exchange across the furnace enclosure, with temperature-dependent emissivities and, ideally, semi-transparency for the crystal/melt in the near-infrared. This is arguably the single largest gap, since radiation typically dominates furnace-scale heat transport in CZ hot zones.

2. **Electromagnetic heating module.** For resistive heaters, a straightforward volumetric Joule-heating source coupled to an electrical conduction solve suffices. For RF/inductive heating (common in industrial and MCZ pullers), a full eddy-current (harmonic vector-potential) EM solver coupled to the thermal field is needed — nontrivial numerically and not analogous to Basilisk's existing EHD module.

3. **Solidification/Stefan-problem module.** Extend VOF or add a level-set representation of the solid–liquid interface with an enthalpy method or explicit Stefan boundary condition, including latent heat release, interface-normal velocity from the local heat-flux jump, and coupling to the (typically much slower) mesh-adaptation and pulling kinematics. Basilisk's existing two-phase VOF infrastructure is a reasonable starting point, but melt–crystal solidification is a different physical regime from liquid–gas interface capture (density/velocity discontinuities, interface motion governed by heat flux rather than material transport).

4. **Multi-material conjugate solid domains.** A general, efficient way to represent several concentric/adjacent solid regions (crucible, susceptor, insulation, crystal) with distinct thermal properties, likely via embedded boundaries or a hybrid solid/fluid formulation, with robust conjugate boundary coupling to the melt/gas flow solvers.

5. **Process-scale time-stepping and evolving geometry.** A quasi-steady/multi-timescale integration strategy that can advance the (slow) crystal length, crucible lift, and melt depletion over a multi-hour pull without re-resolving every fast eddy at full cost — likely requiring a hybrid strategy (e.g., periodic quasi-steady global solves with intermittent high-fidelity local transients, echoing the CrysMAS+OpenFOAM approach).

6. **Dopant/impurity transport and segregation.** Add scalar transport with a segregation boundary condition at the moving interface, validated against known effective segregation coefficient behavior (Burton–Prim–Slichter-type boundary-layer models) for consistency checks.

7. **Rotation and free-surface pinning/triple-line handling.** Robust handling of the crystal-rotation/crucible-rotation kinematics and the contact-line/meniscus pinning at the crystal edge, an area where even mature codes require careful numerical treatment.

8. **Validation program.** Systematic validation against published CZ benchmark cases (e.g., the well-known Derby/Brown thermal-capillary benchmarks, IISB model-furnace experiments, or CrysMAS's own published cases) — without this, any new code has no credibility for industrial use regardless of physics completeness.

9. **Usability layer.** At minimum, parameterized case templates and post-processing scripts; a true GUI/materials-database layer (as CrysMAS provides) is a separate, substantial software-engineering undertaking generally out of scope for an academic group.

**Realistic effort estimate:** Items 1–4 alone represent the work of a dedicated computational-physics PhD or postdoc effort over 2–4 years each if done rigorously (radiation and EM modules are themselves substantial standalone solvers in codes like MOOSE or COMSOL). A credible "CrysMAS-lite" Basilisk environment — covering conjugate heat transfer, radiation, latent heat, and one heating mechanism, validated on a benchmark CZ case — is a realistic 3–5 year research program for a small team, not a side project.

---

## 6. Where Basilisk Genuinely Adds Value Over CrysMAS

It would be a mistake to read this report as purely negative for Basilisk. There are specific niches where Basilisk's native strengths exceed what global furnace codes typically deliver:

- **Resolved, transient, 3D melt turbulence and instability studies.** Because CrysMAS and its peers (CGSim, FEMAG-CZ) run global 2D-axisymmetric models with simplified turbulence treatment for tractability, they systematically under-resolve 3D, non-axisymmetric, oscillatory melt instabilities that are known to cause striations and dopant inhomogeneity. Basilisk's adaptive, momentum-conserving, low-dissipation Navier–Stokes solver is well suited to exactly this sub-problem, mirroring the motivation behind the published CrysMAS+OpenFOAM local-3D coupling — Basilisk could serve the same role as (or an improvement on) OpenFOAM in such a hybrid pipeline, potentially with better efficiency in resolving thin thermal/momentum boundary layers via AMR.

- **Free-surface and meniscus dynamics.** Basilisk's sharp VOF interface capture and validated surface-tension treatment (with attention to spurious/parasitic currents) is more rigorous than the simplified or prescribed free-surface treatments typical of furnace-scale global codes.

- **Marangoni-convection-dominated regimes and method development.** For research questions specifically about thermocapillary flow, contact-line dynamics, or interface-shape sensitivity, a dedicated interfacial-flow solver is the right tool class regardless of furnace-scale radiation fidelity.

- **Open-source transparency and reproducibility.** For academic research requiring full algorithmic transparency, custom numerical experiments, or novel method development (e.g., new AMR criteria, new interface-capturing schemes), Basilisk's open codebase is a genuine asset that a licensed, closed-source tool like CrysMAS cannot offer.

- **Cost.** For groups without an existing CrysMAS license, Basilisk's zero licensing cost is material, particularly for exploratory or student research.

---

## 7. Recommendations by Use Case

**Industrial process/hot-zone design (heater layout, insulation optimization, thermal-budget studies, interface-shape control for yield):** Use CrysMAS (or equivalent global codes such as CGSim/FEMAG-CZ). The radiation, EM heating, and validated solidification physics are non-negotiable requirements that Basilisk does not provide out of the box, and the multi-year development cost of replicating them is not justified when mature, validated, supported tools already exist.

**Academic research into melt-flow instabilities, 3D turbulence, striation mechanisms, or free-surface/Marangoni dynamics:** Basilisk is an excellent and arguably superior choice for the *resolved local sub-model*, provided it is coupled to (or its boundary conditions are informed by) a global thermal solution from a tool like CrysMAS — following the published global-2D/local-3D coupling paradigm. Standalone use of Basilisk for full CZ process simulation, without a global thermal/radiation model supplying realistic furnace boundary conditions, risks producing melt-flow results that are numerically excellent but thermally unrealistic.

**Method development / new numerical schemes for crystal growth CFD:** Basilisk's open, extensible, well-documented C-preprocessor framework, existing embedded-boundary and VOF infrastructure, and active user community make it a reasonable platform for developing and testing new solidification-front-tracking or conjugate-radiation algorithms in isolation, ahead of integration into a production tool.

**Building a full Basilisk-native CZ capability from scratch as a CrysMAS replacement:** Not recommended as a near-term goal for most groups. The physics gaps (radiation, EM heating, solidification, process-scale time integration) are each substantial standalone solver-development efforts; a multi-year, adequately resourced project is required, and even then the resulting tool would likely remain a research code rather than an industrially validated, supported product. A hybrid strategy — Basilisk for the resolved melt/interface sub-domain, coupled to CrysMAS (or an open alternative such as OpenFOAM/Elmer with added radiation modules) for the global thermal/EM/radiation solve — offers better return on effort.

---

## 8. Key References

- Popinet, S. (2009). "An accurate adaptive solver for surface-tension-driven interfacial flows." *Journal of Computational Physics*, 228(16), 5838–5866.
- Popinet, S. (2018). "Numerical Models of Surface Tension." *Annual Review of Fluid Mechanics*, 50, 49–75.
- van Hooft, J. A., et al. (2018). Wavelet-based adaptive mesh refinement criteria for the Basilisk solver.
- Basilisk source documentation: "Solvers" — Saint-Venant, Navier–Stokes, Electrohydrodynamics, Viscoelasticity modules, https://basilisk.fr/src/README
- Popinet, S. (2020). Description of the layered/multilayer solver, relevant to the free-surface/shallow-flow formulation lineage used in Basilisk.
- Derby, J. J., & Brown, R. A. (1986). "Thermal-capillary analysis of Czochralski and liquid encapsulated Czochralski crystal growth: I. Simulation." *Journal of Crystal Growth*, 74, 605–624.
- Derby, J. J., & Brown, R. A. (1987). "On the dynamics of Czochralski crystal growth." *Journal of Crystal Growth*, 83, 137–151.
- Müller, G., & Friedrich, J. (2004). "Challenges in modeling of bulk crystal growth." *Journal of Crystal Growth*, 266, 1–19.
- Lan, C. W. (2004). "Recent progress of crystal growth modeling and growth control." *Chemical Engineering Science*, 59, 1437–1457.
- Vizman, D., et al. — Global 2D–local 3D coupled modeling of industrial Czochralski silicon crystal growth using CrysMAS and OpenFOAM. *Journal of Crystal Growth* (2013).
- Global simulation of Czochralski silicon crystal growth in ANSYS FLUENT — comparative discussion of CGSim, CrysMAS/STHAMAS, and FEMAG-CZ as commercially available global CZ codes. *Journal of Crystal Growth* (2013).
- Enders-Seidlitz, A., Pal, J., & Dadzis, K. (2022). "Development and validation of a thermal simulation for the Czochralski crystal growth process using model experiments." *Journal of Crystal Growth*, 593, 126750.
- Enders-Seidlitz, A., Pal, J., & Dadzis, K. (2022). "Model experiments for Czochralski crystal growth processes using inductive and resistive heating." *IOP Conf. Series: Materials Science and Engineering*, 1223, 012003.
- Friedrich, J. (2020). "Erlangen — An Important Center of Crystal Growth and Epitaxy: Major Scientific Results and Technological Solutions of the Last Four Decades." *Crystal Research and Technology*, 55.
- Fraunhofer IISB, "Equipment Simulation" and CrysMAS manual/download portal, https://www.iisb.fraunhofer.de and https://download.iisb.fraunhofer.de/downloads/Manual/index.html
- Dupret, F., & Van den Bogaert, N., et al. — work on effective simulation of traveling magnetic fields and related CZ/MCZ modeling (UCLouvain group), as cited in CrysMAS-adjacent literature.

---

*Prepared as a technical assessment for researchers and engineers evaluating open-source CFD platforms against dedicated crystal-growth process simulators.*

---

> [!NOTE]
> 
> Generated by Claude.ai
>
> Model: Sonet 5
>
> Prompt: Write a comprehensive, technically rigorous report evaluating the suitability of Basilisk Flow Solver for high-fidelity numerical simulation of the Czochralski (CZ) crystal growth process. The report should critically assess Basilisk Flow Solver's capabilities, limitations, required extensions, and practical implementation challenges. It should also provide a detailed comparison with CrysMAS, the dedicated crystal-growth simulation software developed by the Fraunhofer Institute for Integrated Systems and Device Technology (Fraunhofer IISB). The report should be written for researchers and engineers involved in semiconductor crystal growth, computational fluid dynamics (CFD), heat transfer, and multiphysics simulation.
> Objectives
> Determine whether Basilisk Flow Solver can serve as a viable platform for industrial-grade CZ crystal growth simulation.
> Identify which physical phenomena can be modeled using standard Basilisk Flow Solver capabilities and which require custom development.
> Compare Basilisk Flow Solver with CrysMAS regarding physics coverage, numerical methods, validation status, industrial readiness, scalability, extensibility, and usability.
> Assess the effort required to build a CZ simulation environment in Basilisk Flow Solver that approaches the capabilities of CrysMAS.
> Provide recommendations for research, academic, and industrial use cases.
> Provide key references. Show the output in Markdown format.
