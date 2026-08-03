# Suitability of the Proteus Multiphase Transport Framework for High-Fidelity Czochralski Crystal Growth Simulation: A Comparative Assessment Against CrysMAS

**A technical evaluation for researchers and engineers in semiconductor crystal growth, CFD, heat transfer, and multiphysics simulation**

---

## Executive Summary

Proteus (`erdc/proteus`, the ERDC "Computational Methods and Simulation Toolkit") is a general-purpose, Python-orchestrated finite element framework built for continuum-mechanics PDEs — historically developed and validated for free-surface hydrodynamics, coastal/hydraulic engineering, and porous-media flow. CrysMAS is a purpose-built, finite-volume, axisymmetric "global furnace" simulator developed over more than two decades by Fraunhofer IISB specifically for melt-growth processes including Czochralski (CZ), Vertical Gradient Freeze (VGF), and related techniques.

The central finding of this report is that **Proteus is not a drop-in CZ solver and cannot substitute for CrysMAS today**, but it possesses a numerically credible foundation — a mature two-phase/free-surface Navier–Stokes stack, conservative level-set interface tracking, RANS turbulence, and a flexible physics-definition architecture — that could, with substantial custom engineering, be extended into a research-grade CZ solver. The dominant gap is not fluid mechanics but the **coupled global heat transfer physics unique to melt crystal growth**: enclosure/participating-medium radiation with specular and diffuse reflection in semi-transparent crystals, latent-heat release at a deformable crystal–melt interface tied to a pulling/rotation kinematic model, and (for many materials) magnetohydrodynamic (MHD) melt control. None of these exist in Proteus out of the box, and none are trivial additions.

**Bottom line for decision-makers:**
- For **production/industrial CZ process design and hot-zone engineering**, CrysMAS (or its commercial peers, CGSim and FEMAG-CZ) remains the appropriate tool — it is validated, supported, and purpose-fit.
- For **research groups** who need to couple CZ heat/flow physics with capabilities Proteus already does well (complex 3D free-surface dynamics, two-phase interface tracking, custom stabilized FEM formulations, or coupling with other ERDC-style multiphysics), Proteus is a viable but multi-year development investment, not a near-term substitute.
- A **hybrid strategy** — using CrysMAS (or CGSim) for global furnace/radiation/thermal-capillary analysis and Proteus (or another custom FEM/FVM code) for targeted, high-fidelity sub-models (3D melt turbulence, MHD, striation dynamics) — is the most defensible near-term path for most organizations.

---

## 1. Introduction and Scope

### 1.1 The CZ Simulation Problem

Czochralski growth is a multiphysics, multiscale, moving-boundary problem. A representative high-fidelity CZ model must resolve, simultaneously and self-consistently:

1. **Global (furnace-scale) heat transfer**: conduction in solids (crucible, susceptor, heater, insulation, shields), convection in inert/reactive cover gas, and **radiative exchange** between diffuse and/or specular surfaces in an enclosure that includes **semi-transparent solids** (the growing crystal itself, for oxide and some compound-semiconductor materials).
2. **Melt hydrodynamics**: buoyancy-driven (Rayleigh–Bénard-type) convection, forced convection from independently rotating crystal and crucible, thermocapillary (Marangoni) flow at the free melt surface, and — for silicon and many electronic materials — **magnetohydrodynamic damping** from applied axial, transverse, or cusp magnetic fields.
3. **Turbulence**: melt Reynolds/Grashof numbers in industrial-diameter (200–450 mm) silicon CZ pullers place the flow solidly in the turbulent or transitional-turbulent regime, requiring RANS, LES, or hybrid closures with rotating-frame source terms.
4. **Phase change and interface tracking**: a deformable, non-planar crystal–melt interface whose shape, position, and growth rate are governed by a **Stefan condition** (latent-heat balance) coupled to the pulling rate, and a deformable, capillarity-governed **melt–gas free surface** (the meniscus) whose shape sets the crystal diameter via the growth angle condition.
5. **Species/mass transport**: dopant segregation, oxygen and carbon incorporation (from crucible dissolution and CO transport in the gas phase), and their coupling to interface morphology (constitutional supercooling, striations).
6. **Solid mechanics**: thermal stress in the growing crystal, relevant to dislocation generation and slip.
7. **System-level control**: coupling of the above to pulling rate, rotation rates, and heater power as manipulated/controlled variables, often on process timescales orders of magnitude longer than the fluid/thermal timescales — necessitating pseudo-steady or quasi-stationary global models rather than fully transient DNS-type simulation for practical turnaround.

No single physical model dominates; **CZ simulation is defined by tight two-way coupling across this list**, and software suitability must be judged on the coupling architecture as much as on any individual solver's fidelity.

### 1.2 What "Proteus" Denotes in This Report

The name "Proteus" is used for several unrelated codes in the literature (a particle/lattice-Boltzmann fluid–structure code by Feng & Michaelides; Argonne's PROTEUS-SN/MOC/NODAL neutron-transport suite; and others). This report evaluates the **US Army ERDC Proteus Computational Methods and Simulation Toolkit** (`github.com/erdc/proteus`), described by its developers as "a Python package for rapidly developing computer models and numerical methods... focused on models of continuum mechanical processes described by partial differential equations." This is the code most naturally described as a "multiphase transport framework," given its mature two-phase (VOF/level-set) Navier–Stokes capability and its lineage in coastal, hydraulic, and porous-media multiphase transport (sediment transport, variably saturated/Richards' equation flow, two-phase porous-media flow). All capability claims below are scoped to this toolkit as of its public documentation and release history.

---

## 2. Proteus: Architecture and Native Capabilities

### 2.1 Design Philosophy

Proteus is explicitly architected to **decouple physical model specification from numerical method specification** — a "physics file" (`_p.py`) defines the PDE system, coefficients, and boundary/initial conditions, while a separate "numerics file" (`_n.py`) selects the finite element space, stabilization, time integrator, and linear/nonlinear solvers. This is a deliberate departure from monolithic legacy CFD codes where physics and numerics are hard-coded together, and it is Proteus's most relevant architectural asset for a CZ extension effort: **new transport equations (e.g., a radiative transfer or MHD induction equation) can, in principle, be added as new coefficient classes without rewriting the solver infrastructure.**

### 2.2 Native Physical Models

As of the current public documentation, Proteus ships with implemented and tested models for:

| Category | Models |
|---|---|
| Scalar transport | Poisson's equation, heat equation, linear and nonlinear (singly/doubly degenerate) advection-diffusion-reaction, eikonal/signed-distance equation |
| Shallow/free-surface hydraulics | Diffusive-wave overland flow, 1D/2D shallow water equations, 2D dispersive shallow water equations |
| Porous media | Richards' equation (head- and saturation-based, mass-conservative), two-phase porous-media flow (diffuse-interface and sharp-interface/level-set formulations) |
| Incompressible flow | Stokes, Navier–Stokes, Reynolds-Averaged Navier–Stokes (RANS) |
| Two-phase free-surface flow | Two-phase Stokes/Navier-Stokes/RANS with sharp interface via level-set/VOF, including the **monolithic conservative level-set (MCLS)** method with built-in redistancing |
| Structural | Linear elasticity |

Discretizations available include classical continuous Galerkin (C₀P₁, C₀P₂, C₀Q₁, C₀Q₂) with entropy-viscosity, variational-multiscale, and algebraic stabilization; discontinuous Galerkin (P₀–P_k, Lagrange and monomial bases); and non-conforming/mixed elements including Taylor–Hood pairs. Time integration spans backward/forward Euler, θ-methods, SSP-RK, adaptive BDF, and pseudo-transient continuation. Linear algebra is provided through PETSc (via petsc4py) alongside native Jacobi, Gauss–Seidel, Schwarz, and multigrid solvers; nonlinear solvers include Newton's method and nonlinear (FAS) multigrid; interface/level-set problems use fast marching/fast sweeping for redistancing.

### 2.3 Track Record and Validation Domain

Proteus's publication record — coastal/hydraulic engineering (wave breaking, caisson breakwaters, sediment transport, fluid–vegetation interaction), variably saturated groundwater flow, and two-phase Navier–Stokes methods development (monolithic conservative level set, preconditioners for two-phase incompressible flow) — indicates a code whose validation base is **environmental and hydraulic multiphase flow**, not high-temperature melt processing. Its two-phase Navier–Stokes solver is genuinely state-of-the-art for **isothermal, near-unity-density-ratio-agnostic, free-surface water/air problems** (its MCLS method was developed partly to handle the large density/viscosity ratios of water–air interfaces robustly). This is directly relevant methodology for the CZ melt–gas meniscus, but the code has, to the reporting team's knowledge, no published validation against melt-growth thermal-capillary or radiative benchmarks.

### 2.4 Software Engineering Posture

Proteus is MIT-licensed, Python/C++/Fortran, distributed via conda-forge and GitHub, with Docker images for evaluation. It is under active but modest-scale open-source development (in the tens of contributors, low hundreds of GitHub stars/forks), driven primarily by a US Army Corps of Engineers research mission rather than a commercial or crystal-growth-specific roadmap. This has two practical consequences: (a) the code is fully inspectable and extensible without vendor gatekeeping — a genuine advantage for a research group wanting to add novel physics — and (b) there is **no vendor support, no crystal-growth domain expertise embedded in the tool, and no guarantee of long-term maintenance priorities aligned with semiconductor applications.**

---

## 3. CrysMAS: Architecture and Native Capabilities

### 3.1 Origin and Purpose

CrysMAS ("Crystal Growth Modeling Analysis System") is developed by the Crystal Growth Laboratory of Fraunhofer IISB (Erlangen, Germany) specifically for **global, furnace-scale simulation of melt and vapor crystal growth processes**, with Czochralski, Vapor-Pressure-Controlled Czochralski (VCz), Vertical Gradient Freeze (VGF), and related bulk-growth techniques as primary targets. It succeeds and incorporates methodology from Fraunhofer IISB's earlier STHAMAS and CrysVUn codes, and is licensed commercially worldwide, with an established base of academic and industrial users spanning several decades of continuous development.

### 3.2 Native Physical Models

CrysMAS is a **finite-volume**, predominantly **axisymmetric (2D r–z)** global furnace code (with 3D extensions for specific effects) purpose-built around the coupled physics of melt growth:

- **Conjugate heat transfer**: simultaneous solution of conduction in all solid furnace components, convection in the cover-gas domain, and convection in the melt, coupled at every interface.
- **Enclosure and volumetric thermal radiation**: view-factor/exchange-factor-based radiative heat transfer between diffuse (and configurable specular) surfaces in complex, shadowing, axisymmetric geometries, extended to **radiation within semi-transparent solids** (essential for oxide crystals such as sapphire, YAG, and for some compound semiconductors) via spectral or banded radiative-transfer coupling.
- **Melt convection**: buoyancy, forced (rotation-driven), and thermocapillary (Marangoni) flow, with turbulence closures suited to the melt Reynolds/Grashof regimes encountered in industrial crucible sizes.
- **Magnetohydrodynamics**: coupling of applied magnetic fields (axial, cusp, traveling) to melt flow via Lorentz-force source terms — a standard requirement for industrial silicon CZ.
- **Phase-change interface tracking**: coupled solution of the Stefan condition at the crystal–melt interface with a deformable, self-consistent interface shape, and the meniscus/free-surface shape from the thermal-capillary (Young–Laplace + growth-angle) model, both moving self-consistently with the pulling process.
- **Species and dopant transport**: segregation, oxygen/carbon transport from crucible dissolution and gas-phase CO chemistry, relevant to resistivity and defect engineering.
- **Thermoelastic stress**: post-processing or coupled computation of thermal stress in the crystal for dislocation-risk assessment.
- **Process-level parameterization**: built-in workflows for pulling rate, rotation rates, heater power, and gas flow as configurable process variables, with quasi-steady global solution modes suited to production hot-zone design iteration.

### 3.3 Validation and Industrial Standing

CrysMAS (with its predecessors STHAMAS/CrysVUn) has been used and cited across several decades of crystal-growth literature for silicon, GaAs, CZT, β-Ga₂O₃, sapphire, and other systems, including comparative benchmarking studies against CGSim, FEMAG, and general-purpose codes (ANSYS/COMSOL) run by independent groups. It is explicitly identified in the crystal-growth community's own validation/verification/benchmarking literature as one of the small set of "specialized 2D/3D ready-to-use software tools dedicated to coupled crystallization furnace simulations," alongside CGSim (STR Group) and FEMAG (FEMAGSoft). This places CrysMAS in a class of software with an established, community-recognized validation track record specific to melt growth — a status Proteus does not share for this application domain.

### 3.4 Software Engineering Posture

CrysMAS is proprietary, commercially licensed software with a graphical pre/post-processing environment, structured process-parameter input, and vendor (Fraunhofer IISB) support and documentation. This trades extensibility for usability and reliability: a process engineer can set up and interpret a CZ hot-zone simulation without writing solver code, but adding genuinely novel physics (a new transport mechanism, a non-standard turbulence closure, coupling to an external structural or electromagnetic solver) is constrained by what the vendor exposes and is not a research-code-style extension exercise.

---

## 4. Physics-by-Physics Capability Comparison

| Physical phenomenon | CrysMAS | Proteus (native) | Proteus (with extension) |
|---|---|---|---|
| Conduction in multi-material solids | ✅ Native, mature | ✅ Heat equation supported; multi-domain conjugate coupling requires manual setup | ✅ Achievable with moderate effort |
| Melt convection (buoyancy + forced) | ✅ Native, validated for CZ regimes | ✅ Navier–Stokes/RANS present | ✅ Directly usable, needs rotating-frame source terms |
| Turbulence (RANS) | ✅ Native, melt-tuned closures | ⚠️ RANS present but not validated/tuned for high-Pr, rotating, buoyant melt flows | ⚠️ Requires closure re-calibration and validation |
| Thermocapillary (Marangoni) free-surface flow | ✅ Native | ⚠️ Two-phase NS/level-set present; Marangoni stress boundary condition **not a standard model** | 🔧 Custom BC implementation required |
| Enclosure radiative heat transfer (diffuse/specular, view factors) | ✅ Native, mature | ❌ **Not implemented** | 🔧 Major custom development (view-factor or ray-tracing/Monte Carlo module) |
| Radiation in semi-transparent solids (crystal) | ✅ Native | ❌ Not implemented | 🔧 Major custom development (radiative transfer equation coupling) |
| Magnetohydrodynamics (Lorentz force coupling) | ✅ Native | ❌ Not implemented | 🔧 Custom induction/Lorentz-force module; substantial effort |
| Crystal–melt interface tracking with Stefan condition, coupled to pulling kinematics | ✅ Native, purpose-built | ⚠️ Level-set/VOF interface tracking exists; no latent-heat Stefan coupling or pulling-rate kinematics | 🔧 Substantial custom coupling |
| Free-surface meniscus shape (growth-angle/thermal-capillary model) | ✅ Native | ⚠️ Free-surface capability exists (from hydraulic applications) but no growth-angle condition | 🔧 Custom boundary condition and moving-mesh/ALE logic |
| Dopant/impurity species transport & segregation | ✅ Native | ✅ Advection-diffusion-reaction framework directly applicable | ✅ Achievable, moderate effort |
| Oxygen/carbon incorporation (crucible dissolution, gas-phase CO chemistry) | ✅ Native | ❌ Not implemented | 🔧 Custom reactive transport + gas-phase chemistry model |
| Thermoelastic stress in crystal | ✅ Native (coupled or post-processed) | ✅ Linear elasticity present | ✅ Achievable, needs thermal-stress coupling |
| Axisymmetric (2D r–z) reduced-order global mode | ✅ Native, primary mode of use | ⚠️ Proteus is inherently 3D/unstructured; 2D axisymmetric solves possible but not a first-class specialized mode | 🔧 Moderate — requires care in mesh/BC setup for axisymmetric efficiency |
| Full 3D transient melt turbulence / striation-scale dynamics | ⚠️ Possible but computationally heavy; not the primary design target | ✅ **Native strength** — unstructured 3D FEM, parallel, designed for this class of problem | ✅ Proteus's most credible relative advantage |
| Process-level control-variable workflows (pulling rate, power, rotation as design parameters) | ✅ Native, GUI-driven | ❌ Not present | 🔧 Custom scripting layer (straightforward — Python-native) |

**Interpretation.** CrysMAS covers essentially the entire CZ physics stack natively because it was purpose-built for it. Proteus covers the **generic continuum-mechanics substrate** (heat conduction, incompressible flow, free-surface tracking, species transport, linear elasticity) well, but **every phenomenon that is specific to melt crystal growth — enclosure/participating-medium radiation, MHD, the Stefan-condition crystal–melt interface, and the growth-angle meniscus condition — is absent and would need to be built from scratch.** These are not minor gaps: radiative heat transfer and the coupled interface kinematics are typically the *dominant* physics governing interface shape and thermal gradients in real CZ furnaces, so their absence is not a peripheral limitation but a central one.

---

## 5. Numerical Methods Comparison

| Aspect | CrysMAS | Proteus |
|---|---|---|
| Discretization | Finite volume | Finite element (continuous Galerkin, discontinuous Galerkin, mixed) |
| Mesh topology | Primarily structured/block-structured axisymmetric; some 3D | Fully unstructured simplicial meshes, native 3D |
| Interface representation | Body-fitted, deforming mesh (ALE-style) tied to Stefan/meniscus conditions | Level-set/VOF (implicit, non-body-fitted) for two-phase flow; no ALE moving-mesh infrastructure tied to phase-change kinematics |
| Turbulence closures | Melt-growth-tuned RANS models (validated against CZ experiments) | Generic RANS; no melt-specific tuning or validation |
| Radiative transfer solver | Dedicated view-factor / exchange-factor and spectral radiation solvers | None |
| Linear/nonlinear solvers | Vendor-integrated, tuned for the coupled furnace problem | PETSc-backed, general-purpose (SuperLU, multigrid, Newton) — powerful but requires problem-specific tuning |
| Parallelism | Primarily targeted at practical hot-zone design turnaround (workstation-to-modest-cluster scale) | MPI-parallel via PETSc/petsc4py; designed for HPC-scale unstructured problems — a genuine strength for large 3D transient runs |
| Stabilization for advection-dominated transport | Standard FV upwinding/TVD schemes | Rich set: entropy viscosity, VMS, algebraic stabilization, flux-corrected transport — more numerically sophisticated options available |

Proteus's numerical toolbox is, in the abstract, more sophisticated and modern in several respects (unstructured 3D meshing, high-order stabilized FEM, monolithic conservative level-set methods, flux-corrected transport). CrysMAS's numerics are less exotic but are **integrated end-to-end around the specific coupled system of equations that governs CZ growth**, including the moving-mesh/body-fitted treatment of the crystal–melt and melt–gas interfaces that is arguably the more natural and robust choice for the *quasi-steady, slowly deforming* interfaces typical of CZ (as opposed to the topologically complex, rapidly evolving interfaces — breaking waves, sediment beds — for which Proteus's implicit interface-capturing methods were designed).

---

## 6. Required Extensions for a CZ-Capable Proteus Implementation

Building a Proteus-based CZ solver that approaches CrysMAS's capability envelope would require, at minimum, the following development workstreams. Each is listed with an approximate relative effort tier (Low / Medium / High / Very High), calibrated against typical multiphysics-code development timelines for a team with strong finite-element and Python/C++ skills but no prior Proteus internals experience.

### 6.1 Conjugate multi-domain heat conduction with radiative boundary coupling — **High**
Proteus's heat equation model must be extended to (a) handle multiple abutting material domains with different conductivities and interface continuity conditions (largely a mesh/domain-decomposition and coefficient-class exercise — moderate), and (b) accept **radiative flux boundary conditions computed by an external or embedded radiation solver** — the harder part.

### 6.2 Enclosure radiation solver (view-factor or Monte Carlo ray tracing) — **Very High**
This is likely the single largest development item. Two viable strategies:
- **View-factor/radiosity method** (matches CrysMAS's approach): requires geometric view-factor computation for axisymmetric or 3D shadowing geometries, assembly of a (dense) radiosity linear system, and coupling into the global nonlinear iteration. This is a substantial standalone numerical-methods project even before crystal semi-transparency is considered.
- **Monte Carlo ray tracing / participating-medium radiative transfer**: more general (handles semi-transparent crystals naturally) but computationally expensive and statistically noisy, complicating convergence of the coupled nonlinear system — a known difficulty in the broader CZ modeling literature, where hybrid spectral/discrete-exchange-factor methods have specifically been developed to manage this cost.

Neither exists in Proteus today; both require new solver modules, not configuration.

### 6.3 Crystal–melt interface tracking with Stefan condition and pulling kinematics — **Very High**
Proteus's level-set/VOF machinery tracks interfaces well for capturing topology, but CZ requires an interface whose **normal velocity is set by a latent-heat balance** (Stefan condition) coupled to a **prescribed pulling rate** and to crystal/crucible rotation — a fundamentally different physical closure than free-surface water/air interfaces. This likely requires either (a) adapting the level-set velocity extension to solve the Stefan condition at each interface point, or (b) moving toward a body-fitted ALE (Arbitrary Lagrangian–Eulerian) mesh strategy that does not currently exist in Proteus's architecture, which is a major structural addition.

### 6.4 Thermocapillary meniscus with growth-angle condition — **High**
The melt–gas free surface must satisfy a **Young–Laplace balance with a specified growth angle** at the triple line (crystal edge), which sets the crystal diameter dynamically. This is a specialized moving-boundary condition not present in Proteus's free-surface flow models (which are tuned to hydraulic free surfaces, not capillary-controlled solidification menisci).

### 6.5 Magnetohydrodynamics (Lorentz force coupling) — **High**
Required for most industrial silicon CZ (and increasingly other materials) where magnetic fields are used to damp/control melt turbulence. This requires either a low-magnetic-Reynolds-number quasi-static approximation (solving for induced currents/Lorentz force as a source term, moderate-high effort) or full MHD induction equation coupling (high effort). Neither exists in Proteus.

### 6.6 Reactive/multi-species transport for oxygen and dopant incorporation — **Medium**
Proteus's advection-diffusion-reaction infrastructure is directly reusable for bulk species transport; the harder part is implementing the **crucible-dissolution and gas-phase CO reaction boundary conditions** specific to oxygen incorporation modeling, which is domain knowledge rather than a numerical-methods problem.

### 6.7 Turbulence closure validation for high-Prandtl, rotating, buoyant melt flows — **Medium**
Proteus's RANS models would need re-parameterization and validation against melt-growth benchmark data (e.g., published silicon CZ melt flow experiments/DNS) before results could be trusted quantitatively — closure constants tuned for hydraulic engineering flows are not expected to transfer directly.

### 6.8 Process-workflow and GUI/usability layer — **Medium**
CrysMAS's usability advantage (parametrized process setup, GUI-driven meshing/post-processing) has no Proteus counterpart. Since Proteus is Python-native, a scripting/configuration layer for CZ-specific process parameters (pulling rate schedules, rotation profiles, heater power) is comparatively tractable to build, but a genuine GUI matching CrysMAS's usability would be a further, separate investment.

### 6.9 Verification and validation against published CZ benchmarks — **High, and continuous**
Even after the above physics modules exist, the resulting code has **no track record**. A credible V&V campaign against published thermal-capillary CZ benchmarks (e.g., silicon CZ interface-shape and temperature-field data from the literature) would be required before results could be used for anything beyond internal research exploration — and this validation burden recurs with each significant physics addition.

**Aggregate assessment**: sections 6.1–6.5 alone represent the core "hard physics" of CZ and collectively constitute a multi-year (realistically 2–5 person-years, depending on target fidelity and 2D vs. 3D scope) development program even for a team with strong computational science skills, before matching CrysMAS's two-decade-plus accumulated validation base. This is a standard finding whenever a general-purpose CFD/FEM toolkit is proposed as a substitute for a mature domain-specific tool.

---

## 7. Comparative Summary Table

| Dimension | Proteus | CrysMAS |
|---|---|---|
| **Physics coverage (CZ-specific)** | Low out-of-the-box; broad continuum-mechanics substrate | High; purpose-built for melt growth |
| **Numerical methods** | Modern, flexible, unstructured 3D FEM; strong two-phase/free-surface methods | Mature, melt-growth-tuned FV; body-fitted moving-mesh interface treatment |
| **Validation status (for CZ)** | None published | Extensive, multi-decade, cross-validated against CGSim/FEMAG/experiment |
| **Industrial readiness** | Not industrial-ready for CZ; industrial-grade for its native domains (coastal/hydraulic) | Industrial-ready; commercially licensed and supported |
| **Scalability** | Strong (MPI/PETSc, unstructured 3D, HPC-oriented) | Adequate for its design point (2D global + selective 3D); not architected for large-scale 3D transient turbulence |
| **Extensibility** | High — open source, explicit physics/numerics separation, Python-native | Low — proprietary, vendor-controlled feature set |
| **Usability** | Low for non-specialists — requires FEM/Python expertise, no domain-specific GUI | High — GUI-driven, process-parameter-oriented workflow for engineers |
| **Cost model** | Free/open-source (MIT license) | Commercial license fee |
| **Support** | Community/mailing-list, best-effort | Vendor-supported (Fraunhofer IISB) |
| **Best-fit use case** | Novel research physics, 3D transient melt turbulence studies, coupling to other custom multiphysics, method development | Production hot-zone design, industrial process optimization, rapid parametric studies, regulatory/qualification-grade thermal analysis |

---

## 8. Recommendations

### 8.1 For industrial semiconductor manufacturers
**Do not replace CrysMAS (or CGSim/FEMAG-CZ) with Proteus for production hot-zone design or process qualification.** The absence of validated radiation, MHD, and Stefan-interface physics in Proteus represents an unacceptable risk for decisions with direct capital and yield consequences. CrysMAS's validation history and vendor support are precisely what industrial use requires. If 3D transient melt-turbulence or striation phenomena beyond CrysMAS's practical scope are of specific interest, consider a **hybrid workflow**: use CrysMAS for the global thermal/radiative/interface solution and export its temperature/velocity boundary data to drive a targeted high-fidelity 3D sub-model in Proteus or another research CFD code, rather than attempting a full CZ re-implementation.

### 8.2 For academic and national-laboratory research groups
Proteus is a **credible platform for a multi-year research program** aimed at novel CZ-relevant physics or numerics — for example: high-fidelity 3D transient turbulent melt convection studies, new stabilized finite-element formulations for phase-change/Stefan problems, or research into MHD control strategies where the open, modifiable solver stack is itself the point (e.g., coupling to adjoint-based optimization or uncertainty quantification, which is more natural in an open Python framework than in a closed commercial tool). Groups pursuing this path should budget realistically for the extension items in Section 6, prioritize radiation and Stefan-interface coupling first (they gate everything else), and plan an explicit, incremental V&V campaign against published CZ benchmarks rather than treating validation as a final step.

### 8.3 For CFD/multiphysics tool developers and method researchers
Proteus's architecture (physics/numerics separation, unstructured 3D FEM, PETSc-backed solvers, MIT license) makes it a reasonable **substrate** on which to prototype new numerical methods for phase-change and radiative-conductive-convective coupling that could eventually inform either an open CZ code or feed back into commercial tools. This is a methods-research use case, distinct from — and more realistic than — using Proteus as a near-term CrysMAS replacement.

### 8.4 General recommendation
Treat "Proteus vs. CrysMAS" not as a like-for-like software selection decision but as a **build-vs-buy** decision under the specific condition that "build" requires reconstructing, from a general-purpose substrate, physics that a domain-specific vendor has already spent decades validating. The decision should hinge on whether the organization's core need is (a) **production-grade CZ answers now** (favors CrysMAS/CGSim/FEMAG-CZ decisively), or (b) **a long-horizon, open, extensible research platform** where CZ is one of several target applications and in-house numerical-methods expertise is a strategic asset (favors an investment in Proteus or a comparable open FEM toolkit).

---

## 9. Key References

**Proteus toolkit**
- ERDC/Proteus development team. *Proteus: A Computational Methods and Simulation Toolkit* — documentation and capabilities list. https://github.com/erdc/proteus
- Quezada de Luna, M., Collins, J.H., Kees, C.E. (2020). "An Unstructured Finite Element Model for Incompressible Two-Phase Flow Based on a Monolithic Conservative Level Set Method." *International Journal for Numerical Methods in Fluids*.
- Quezada de Luna, M., Kuzmin, D., Kees, C.E. (2019). "A Monolithic Conservative Level Set Method with Built-In Redistancing." *Journal of Computational Physics*, 379, 262–278.
- Bootland, N., Kees, C.E., Wathen, A., Bentley, A. (2019). "Preconditioners for Two-Phase Incompressible Navier-Stokes Flow." *SIAM Journal on Scientific Computing*.
- Kees, C.E., Akkerman, I., Bazilevs, Y., Farthing, M.W. (2011). "A Conservative Level Set Method for Variable-Order Approximations and Unstructured Meshes." *Journal of Computational Physics*, 230(12), 4536–4558.
- Kees, C.E., Farthing, M.W. (2011). "Parallel Computational Methods and Simulation for Coastal and Hydraulic Applications Using the Proteus Toolkit." *PyHPC11 Workshop Proceedings*.
- Kees, C.E., Farthing, M.W., Dawson, C.N. (2008). "Locally Conservative, Stabilized Finite Element Methods for Variably Saturated Flow." *Computer Methods in Applied Mechanics and Engineering*, 197, 4610–4625.

**CrysMAS and Fraunhofer IISB crystal growth software**
- Fraunhofer IISB, Crystal Growth Laboratory. *CrysMAS Manual*. https://download.iisb.fraunhofer.de/downloads/Manual/index.html
- Friedrich, J. (2020). "Erlangen—An Important Center of Crystal Growth and Epitaxy: Major Scientific Results and Technological Solutions of the Last Four Decades." *Crystal Research and Technology*.
- Reimann, C. et al. (2022). "Development and validation of a thermal simulation for the Czochralski crystal growth process using model experiments." *Journal of Crystal Growth*.
- Galazka, Z. et al. (2017). "Numerical Modelling of the Czochralski Growth of β-Ga₂O₃." *Crystals*, 7(1), 26.
- Dadzis, K. et al. — comparative and validation studies referenced in the crystal-growth V&V literature (see next entry).

**CZ simulation physics, benchmarking, and comparative codes**
- Various authors (2016). "Validation, verification, and benchmarking of crystal growth simulations." *Journal of Crystal Growth* — community overview identifying CrysMAS, CGSim, and FEMAG as the principal dedicated CZ/furnace simulation tools.
- Smirnova, O. et al. — "Global simulation of the Czochralski silicon crystal growth in ANSYS FLUENT," *Journal of Crystal Growth* — discusses CGSim, CrysMAS/STHAMAS, and FEMAG-CZ as the established dedicated CZ codes and their coupled-physics scope.
- STR Group. *CGSim — Software for Modeling of Crystal Growth*. https://str-soft.com/software/cgsim/
- Miyazawa, H. et al. "Hybrid finite-volume/finite-element simulation of heat transfer and melt turbulence in Czochralski crystal growth of silicon." *Journal of Crystal Growth* — representative example of coupled radiative/turbulent melt modeling methodology.
- Representative volume-radiation modeling literature for CZ furnaces (discrete exchange factor / spectral radiation coupling for YAG and related oxide growth), illustrating the scope of the radiation sub-model required for a semi-transparent-crystal-capable solver.

---

*This report is a technical evaluation based on publicly available documentation, source repositories, and peer-reviewed literature current as of early August 2026. Organizations considering either tool for a specific process or material system should conduct a focused proof-of-concept before committing significant engineering resources.*

---

> [!NOTE]
> 
> Generated by Claude.ai
>
> Model: Sonet 5
>
> Prompt: Write a comprehensive, technically rigorous report evaluating the suitability of Proteus multiphase transport framework for high-fidelity numerical simulation of the Czochralski (CZ) crystal growth process. The report should critically assess Proteus multiphase transport framework's capabilities, limitations, required extensions, and practical implementation challenges. It should also provide a detailed comparison with CrysMAS, the dedicated crystal-growth simulation software developed by the Fraunhofer Institute for Integrated Systems and Device Technology (Fraunhofer IISB). The report should be written for researchers and engineers involved in semiconductor crystal growth, computational fluid dynamics (CFD), heat transfer, and multiphysics simulation.
> Objectives
> Determine whether Proteus multiphase transport framework can serve as a viable platform for industrial-grade CZ crystal growth simulation.
> Identify which physical phenomena can be modeled using standard Proteus multiphase transport framework capabilities and which require custom development.
> Compare Proteus multiphase transport framework with CrysMAS regarding physics coverage, numerical methods, validation status, industrial readiness, scalability, extensibility, and usability.
> Assess the effort required to build a CZ simulation environment in Proteus multiphase transport framework that approaches the capabilities of CrysMAS.
> Provide recommendations for research, academic, and industrial use cases.
> Provide key references. Show the output in Markdown format.
