# Suitability of Nek5000/NekRS for High-Fidelity Czochralski Crystal Growth Simulation: A Critical Assessment Against CrysMAS

**A technical evaluation for researchers and engineers in semiconductor crystal growth, CFD, heat transfer, and multiphysics simulation**

---

## Executive Summary

Nek5000 and its GPU-native successor NekRS are open-source, matrix-free spectral element method (SEM) solvers developed primarily at Argonne National Laboratory for high-Reynolds-number turbulent flow, conjugate heat transfer (CHT), and — increasingly — multiphysics coupling (MHD, low-Mach compressible flow) at extreme parallel scale. CrysMAS, developed by the Fraunhofer Institute for Integrated Systems and Device Technology (IISB), is a finite-volume "global furnace" simulator purpose-built over more than two decades specifically for Czochralski (CZ) and related melt-growth processes, with turnkey support for diffuse-gray radiation, moving/deformable phase interfaces, dopant segregation, and a library of validated, temperature-dependent material property databases for silicon and compound semiconductors.

The central finding of this report is that **Nek5000/NekRS is not a drop-in substitute for CrysMAS**, but rather a high-performance numerical *substrate* upon which a CZ-capable simulation environment could, in principle, be built — at substantial development cost. Nek's core strengths (spectral accuracy, extreme scalability, native support for rotating/turbulent flows, and an actively maintained ALE moving-mesh capability) map well onto the melt-convection and forced/natural-convection sub-problems that dominate 3D, time-resolved, high-Reynolds/high-Rayleigh-number CZ melt dynamics — a regime CrysMAS, being 2D-axisymmetric and RANS-oriented, cannot resolve. Conversely, CrysMAS's core value proposition — an integrated, radiation-coupled, free-boundary, industrially validated *global heat transfer* model of the entire furnace (crystal, melt, crucible, susceptor, heaters, insulation, gas, chamber) — has no out-of-the-box counterpart in Nek. Radiative heat exchange between diffuse-gray surfaces, dopant segregation with a moving solidification front, quasi-steady global thermal balancing, and a validated materials database would all need to be engineered from scratch or coupled in from external tools.

The recommended posture is **complementary, not competitive**: use CrysMAS (or an equivalent global furnace tool such as CGSim or FEMAG-CZ) for industrial process design, thermal-field optimization, and interface-shape control, and use Nek5000/NekRS for targeted, high-fidelity investigations of melt turbulence, oscillatory convection, striations, and 3D instabilities — ideally through a one-way or loosely coupled workflow in which CrysMAS (or a reduced global model) supplies boundary conditions to a Nek melt-domain simulation, and Nek results (effective heat/mass transfer coefficients, turbulence-corrected Nusselt numbers) feed back into the global model. Building a fully self-contained Nek-based CZ furnace simulator to CrysMAS's level of physics coverage and industrial maturity would represent a multi-year, multi-person software engineering effort with meaningful technical risk in several sub-systems (radiation view-factor computation on curvilinear SEM meshes, robust ALE handling of a genuinely free triple-junction meniscus, and segregation/species transport at a moving front).

---

## 1. Introduction and Scope

### 1.1 The CZ Simulation Problem

The Czochralski process pulls a single crystal from a rotating crucible of melt, held near its melting point by resistive or RF heating, inside a furnace with an inert or reactive ambient gas. Industrial-grade numerical simulation of CZ growth is a genuinely multiphysics, multiscale problem, comprising:

1. **Melt hydrodynamics**: buoyancy-driven (Rayleigh–Bénard-type) convection, forced convection from crystal and crucible rotation, and their interaction, often producing time-dependent, three-dimensional, and at industrial scale (300+ mm silicon) turbulent or transitional flow.
2. **Global furnace heat transfer**: conduction in solids (crucible, susceptor, crystal, insulation, heater), convection in the surrounding gas (often itself turbulent, low-pressure, or mixed forced/natural), and — critically — **radiative heat exchange** among all furnace surfaces, which dominates energy balance in the hot zone.
3. **Melt/crystal interface tracking**: the solid–liquid interface shape and position evolve as a free boundary determined by the local heat balance (Stefan condition), coupled to global thermal fields.
4. **Free melt surface (meniscus)**: the crystal is pulled through a free surface with a growth angle set by surface tension and wetting behavior; this triple-line region controls diameter control and defect nucleation.
5. **Species/dopant transport and segregation**: solute rejection or incorporation at the moving interface, coupled to melt convection, sets axial and radial resistivity/dopant striations.
6. **Electromagnetic effects** (for RF- or magnetically-damped growth, e.g., MCZ/EMCZ): Lorentz-force damping of melt convection under applied static or traveling magnetic fields.
7. **Point-defect and dislocation dynamics** (downstream of the thermal field, generally treated as a post-processing step via Voronkov-type criteria rather than solved simultaneously).

No single physics module addresses all of these; a viable CZ simulation tool must integrate several coupled solvers, generally across widely disparate domains (melt scale ~ cm, furnace scale ~ 1 m, boundary/meniscus scale ~ mm).

### 1.2 Scope of This Report

This report evaluates Nek5000/NekRS against this full problem scope, focusing on:
- what is available natively within the standard Nek5000/NekRS distribution;
- what has been demonstrated in the open literature via user-contributed extensions (MHD, conjugate heat transfer, ALE);
- what is entirely absent and would require new development for CZ-specific physics (radiation enclosure view factors, free-surface meniscus with contact-line pinning, segregation at a moving interface, quasi-steady global thermal solves);
- a structured comparison against CrysMAS across physics coverage, numerics, validation, industrial readiness, scalability, extensibility, and usability;
- a realistic engineering-effort estimate for closing the gap; and
- recommendations differentiated by research, academic, and industrial use case.

---

## 2. Nek5000/NekRS: Technical Overview

### 2.1 Numerical Method

Nek5000 and NekRS are based on the spectral element method (SEM): the domain is decomposed into curvilinear hexahedral elements, and within each element the solution is represented as an Nth-order tensor-product Lagrange polynomial on Gauss–Lobatto–Legendre (GLL) points. This gives two defining properties:

- **Spectral (exponential) convergence** in polynomial order $N$ for smooth solutions, so that engineering accuracy is reached with far fewer degrees of freedom than low-order finite-volume/finite-element methods for the same smooth flow features — a significant advantage for resolving turbulent melt convection without excessive numerical dissipation.
- **Tensor-product sum factorization**, giving $O(N)$ storage and $O(N^4)$ (3D) operator-evaluation work per element, which underlies the method's efficiency and — combined with the code's matrix-free, highly regular data layout — its exceptional strong and weak scaling.

Nek5000 has been demonstrated at $P > 10^6$ MPI ranks on leadership CPU systems, and NekRS — a GPU-native rewrite sharing Nek5000's numerics but built on the OCCA portability layer (supporting CUDA, HIP, OpenCL, and SYCL back-ends) and libParanumal's high-performance kernels — has scaled to tens of thousands of GPUs (e.g., 72,000 GCDs on Frontier), with calculations reported up to 60 billion grid points on 27,648 V100 GPUs on Summit.

### 2.2 Native Physics Capabilities

Within the standard Nek5000/NekRS releases, the following are available out of the box:

- **Incompressible and low-Mach-number compressible Navier–Stokes**, in 2D, 2D-axisymmetric, or full 3D, with forced and natural (Boussinesq) convection.
- **Passive scalar / energy transport**, solved as an advection–diffusion equation for temperature (and additional passive scalars, useful for species/dopant transport under a simplified, non-interface-coupled treatment).
- **Conjugate heat transfer (CHT)**: the energy equation can be solved simultaneously across fluid and solid subdomains sharing a mesh, with continuity of temperature and flux enforced at the interface — directly relevant to crucible/crystal/susceptor conduction coupled to melt convection.
- **Arbitrary Lagrangian–Eulerian (ALE) moving-mesh capability**: demonstrated in official examples (e.g., peristaltic flow) for deforming domains with prescribed or solved boundary motion, and outflow treatments to suppress backflow instabilities — the natural starting point for a deforming melt/crystal interface or a moving free surface, though not pre-packaged for a solved Stefan condition.
- **Magnetohydrodynamics (MHD)**: an incompressible MHD extension has been developed and verified for liquid-metal flows under strong magnetic fields (motivated by fusion blanket applications), solving coupled velocity and magnetic-field Poisson-type systems across fluid and adjoining solid (electrically conducting or insulating) domains — structurally close to what magnetically damped CZ (MCZ) would require, though not validated for the CZ parameter regime.
- **RANS turbulence models** and support for LES/DNS at high Reynolds number, given the method's low numerical dissipation.
- **Two-phase flow extensions** (NEK-2P, developed for boiling-water-reactor applications) exist as a research branch, illustrating the code's extensibility but not as a production capability relevant to CZ (which is single-phase melt + separate gas domain, not two-phase within one domain).
- **User-programmable source terms and boundary conditions** via Fortran/C `usr` subroutines (Nek5000) or OKL kernels (NekRS), which is the standard mechanism by which application-specific physics (buoyancy forcing, custom BCs, property variation) is injected into the solver — as already exploited in the code's own Rayleigh–Bénard and conjugate heat transfer tutorials.

### 2.3 What Is Absent Natively

Critically for CZ applications, the following are **not** part of the standard Nek5000/NekRS capability set and have no first-class support:

- **Surface-to-surface (enclosure) radiative heat transfer** with view-factor computation among diffuse-gray (or spectrally/directionally resolved) surfaces. This is arguably the single largest capability gap: in a real CZ hot zone, radiative exchange between heaters, crucible, crystal, and insulation dominates the energy balance, and no view-factor/radiosity solver ships with Nek.
- **A solved Stefan (moving solid–liquid interface) condition** coupling interface energy balance, latent heat release, and interface velocity to mesh motion — the ALE infrastructure exists, but the physics of a phase-change front with a growth-rate-dependent boundary condition must be implemented by the user.
- **Free-surface (meniscus) dynamics with a pinned or dynamic contact line**, governed by capillarity/surface tension and a prescribed growth angle — again, ALE and level-set-style building blocks exist in the broader Nek ecosystem (e.g., free-surface channel-flow examples, and free-surface/level-set work reported for related induction-melting problems using ALE), but a CZ-specific meniscus model with correct triple-junction physics does not exist off the shelf.
- **Solute/dopant segregation at a moving interface** (effective segregation coefficient, constitutional supercooling checks) as a packaged model.
- **Crystal/crucible/gas radiative-conductive-convective global coupling as a single integrated "furnace" solve** — Nek is a CFD/heat-transfer *solver*, not a furnace-scale process simulation environment; it has no concept of a parameterized furnace geometry library, heater power/temperature control loops, or automated meshing for arbitrary hot-zone configurations.
- **A materials property database** for CZ-relevant melts (Si, Ge, GaAs, sapphire, etc.) and furnace construction materials (graphite, quartz, insulation) with validated temperature-dependent viscosity, density, thermal conductivity, emissivity, and electrical conductivity.
- **A graphical pre/post-processing environment** oriented toward furnace geometry construction, process parameter sweeps, and crystal-growth-specific visualization (interface shape, striations, resistivity maps) — Nek's ecosystem (genbox/Gmsh-based meshing, VisIt/ParaView post-processing) is general-purpose CFD tooling, not domain-specialized.

---

## 3. CrysMAS: Technical Overview

### 3.1 Origin and Purpose

CrysMAS (Crystal Mass and heat transfer Analysis System), with its axisymmetric core historically also referred to as STHAMAS/STHAMAS-3D, was developed by the Crystal Growth Laboratory of Fraunhofer IISB in Erlangen specifically for **global, coupled simulation of bulk crystal growth furnaces**, with a strong historical emphasis on Czochralski, vertical gradient freeze (VGF), and related melt-growth configurations. It is a finite-volume-based code, purpose-built rather than adapted from general CFD, and has been continuously developed and applied within Fraunhofer IISB's crystal growth research and industrial consulting programs for more than two decades.

### 3.2 Physics Coverage

CrysMAS's design center is the **global furnace model**: rather than resolving only the melt, it simultaneously solves, on a single coupled axisymmetric (2D, with 3D extensions for non-axisymmetric effects) domain spanning the entire hot zone:

- Conductive heat transfer in all solid furnace components (crucible, susceptor, crystal, heaters, insulation, chamber walls).
- Convective (and, where relevant, turbulent) heat and momentum transport in the melt and in the surrounding process gas.
- **Diffuse-gray surface-to-surface radiative heat exchange**, computed via view factors across the full furnace enclosure — including reflective/absorptive multi-surface effects — and, in extended versions, coupling to induction/resistive heater electromagnetics.
- **Latent heat release and a solved, deformable melt/crystal interface**, tracked as the process evolves (quasi-steady or time-dependent), consistent with the global thermal balance.
- **Free melt surface (meniscus) shape**, including surface-tension effects relevant to growth-angle and diameter-control modeling.
- **Dopant/impurity segregation**, tracking solute transport and rejection at the moving interface for resistivity/striation prediction.
- Coupling to **inductive or resistive heating models**, including electromagnetic field solutions for RF-heated furnaces, relevant to both Si and compound semiconductor (e.g., GaAs, InP) growth configurations historically studied at IISB.

### 3.3 Numerical Approach

CrysMAS employs a finite-volume discretization on body-fitted, typically axisymmetric structured/block-structured grids, with implicit time-stepping suited to the quasi-steady character of most industrial CZ process simulations (the crystal grows slowly relative to thermal and flow time scales, so many practical furnace-design studies are performed as sequences of steady or quasi-steady solutions at successive crystal lengths, rather than fully time-resolved DNS/LES of melt turbulence). This is a deliberate and defensible engineering trade-off: for furnace/process design (heater power schedules, hot-zone geometry, pull-rate/rotation-rate optimization), the quasi-steady global thermal field is the primary design driver, and fully resolved unsteady 3D melt turbulence is a secondary refinement.

### 3.4 Validation and Industrial Status

CrysMAS is explicitly cited in the crystal-growth literature (alongside CGSim from STR Group and FEMAG-CZ from FEMAGSoft) as one of a small number of **commercially available, industrially validated global CZ furnace simulation codes**, with a substantial publication record from Fraunhofer IISB and external users spanning silicon photovoltaic ingot growth, compound semiconductor bulk growth, and coupled furnace/crystal-scale modeling (e.g., coupling to Cats2D for crystal-scale defect and segregation modeling in VGF/CZ-adjacent processes). It has a track record of **cross-validation against experiment** (thermal model validation using instrumented model experiments) and against other global simulation codes, which is a maturity level Nek5000/NekRS has not been established at for this specific application domain.

---

## 4. Physics-by-Physics Comparison

| Physical phenomenon | Nek5000/NekRS (native) | Nek5000/NekRS (achievable with development) | CrysMAS |
|---|---|---|---|
| Incompressible/low-Mach melt convection | Yes — spectral accuracy, full 3D, transient | — | Yes — typically 2D axisymmetric, steady/quasi-steady |
| Turbulent/transitional 3D melt flow, oscillatory convection | Yes (native strength: LES/DNS-capable, low dissipation) | — | Limited — RANS-type closures on 2D axisymmetric mesh; 3D turbulence not natively resolved |
| Crystal/crucible rotation (forced convection) | Yes, via rotating frame/BC formulation | — | Yes, via effective/parameterized rotation-driven convection or coupled rotating-frame solve |
| Conjugate heat transfer (solid conduction + fluid convection) | Yes, native CHT capability | — | Yes — core capability, whole-furnace conduction network |
| Surface-to-surface radiative exchange (view factors, diffuse-gray) | No | Requires new module: view-factor computation on curvilinear SEM surface mesh + radiosity solve, coupled to energy equation as a BC | Yes — core, validated capability |
| Solved moving solid–liquid interface (Stefan condition) | ALE infrastructure exists; interface physics absent | Requires custom interface-tracking/level-set or ALE front-tracking implementation with latent-heat coupling | Yes — core capability |
| Free melt surface / meniscus with growth angle | Free-surface examples exist (channel flow); no CZ-specific triple-junction model | Requires meniscus-specific ALE/level-set model with capillary BC and pinned contact line | Yes — core capability |
| Dopant/solute segregation at moving interface | No | Requires custom scalar-transport model coupled to interface velocity and segregation coefficient | Yes — core capability |
| Magnetohydrodynamic damping (MCZ/EMCZ) | Yes — verified incompressible MHD extension (fusion-blanket-motivated) | Requires re-validation in CZ parameter regime (geometry, field strength, Hartmann number range) | Available in extended/coupled configurations at some furnace codes; not a universal CrysMAS core feature |
| Electromagnetic (RF) heater coupling | No | Requires new electromagnetics module or external coupling (e.g., to an EM solver) | Yes — supported for inductively heated furnaces |
| Point-defect/dislocation post-processing (Voronkov-type) | No | Requires custom post-processing on Nek thermal-field output | Available as established post-processing workflow in the broader IISB/CrysVUn ecosystem |
| Materials property database (Si, GaAs, graphite, quartz, insulation, etc.) | No | Requires building/importing a validated database | Yes — built-in, validated over decades of use |
| Automated furnace geometry/mesh generation for parametric hot-zone studies | No (general-purpose external meshing only) | Requires domain-specific geometry/meshing front end | Yes — purpose-built pre-processor for furnace configurations |

---

## 5. Structured Comparison: Nek5000/NekRS vs. CrysMAS

### 5.1 Numerical Methods

Nek's spectral element method offers markedly higher accuracy per degree of freedom for smooth, well-resolved flow and thermal fields, and is the clear choice when the physics of interest is inherently 3D and unsteady — e.g., resolving baroclinic/rotational instabilities, oscillatory melt convection linked to striation formation, or transition-to-turbulence phenomena that a 2D axisymmetric RANS-type model cannot represent by construction. CrysMAS's finite-volume method on structured axisymmetric grids is well suited to the quasi-steady, radiation-dominated global energy balance that governs furnace-scale thermal design, where the axisymmetric approximation is often a reasonable engineering simplification and where implicit, robust convergence to a converged global thermal state (across strongly different material conductivities and radiative couplings) is paramount. Neither method is intrinsically "better" — they are optimized for different points in the accuracy/scope trade-off space.

### 5.2 Physics Coverage

CrysMAS is comprehensive for the *furnace-scale, industrially relevant* physics set (radiation, conduction network, quasi-steady melt/gas convection, segregation, interface tracking) but comparatively coarse for melt turbulence itself. Nek is comprehensive and best-in-class for the *fluid dynamics* of the melt (and, by extension, the gas domain) but has essentially none of CrysMAS's furnace-level multiphysics coupling out of the box. This is the report's central asymmetry.

### 5.3 Validation Status

CrysMAS benefits from decades of use, publication, and — importantly — validation against instrumented model experiments and industrial process outcomes specifically in the CZ/VGF domain. Nek5000/NekRS is exceptionally well validated as a general-purpose CFD/thermal-fluids solver (nuclear thermal-hydraulics, turbulent channel/pipe flow, MHD benchmarks) but has **no established validation record for the CZ crystal growth application specifically** — melt Prandtl number regimes, furnace radiative environments, and interface-tracking scenarios relevant to CZ would need dedicated verification and validation (V&V) work before results could be trusted for industrial decision-making.

### 5.4 Industrial Readiness

CrysMAS is a commercially supported, industrially deployed tool with a defined user workflow (geometry input, materials database, solver, specialized post-processing) targeted at process engineers who are not necessarily CFD specialists. Nek5000/NekRS is a research-grade, expert-oriented HPC code; running it productively requires strong background in the SEM, Fortran/C `usr`-file or OKL-kernel programming, and HPC job management. It is not, in its current form, usable by a process engineer without significant software-engineering investment to wrap it in a domain-specific front end.

### 5.5 Scalability

This is Nek5000/NekRS's decisive advantage. Nek5000 and NekRS scale to $10^5$–$10^6$-way parallelism on leadership-class CPU and GPU systems respectively, whereas CrysMAS, as a 2D axisymmetric (or modestly 3D) finite-volume furnace code, is designed to run efficiently on modest workstation-class or small-cluster hardware — appropriate to its physics scope, but it is not architected for, nor does it need, exascale-class parallelism. For any CZ study requiring genuinely 3D, time-resolved turbulence-resolving melt simulation (e.g., DNS/LES studies of striation-relevant instabilities at industrial crystal diameters), Nek/NekRS is essentially the *only* viable numerical substrate among the tools discussed here.

### 5.6 Extensibility

Nek5000/NekRS is open source (Fortran/C core, OKL kernels for NekRS) with a documented `usr`-file/kernel extension mechanism and an active development community (Argonne, DOE Exascale Computing Project legacy, university groups); it has already been extended for MHD, two-phase flow, and conjugate heat transfer by third parties, evidencing real extensibility. CrysMAS's extensibility to end users is more constrained — as commercial/institutional software it exposes configuration and materials-database extension points but not the same level of open-source solver-internals access; new physics modules are typically added by Fraunhofer IISB itself or via negotiated collaboration, and third-party low-level modification is not the intended usage model.

### 5.7 Usability

CrysMAS wins decisively on usability for its intended audience (crystal growth process engineers): furnace geometry construction, materials selection, and process parameter definition are supported by a dedicated interface and workflow. Nek5000/NekRS usability is CFD-expert-oriented: case setup is via text-based parameter files and compiled user subroutines/kernels, meshing is via general tools (e.g., Gmsh, genbox), and there is no crystal-growth-specific abstraction layer.

---

## 6. Effort Assessment: Building a CZ-Capable Environment in Nek5000/NekRS

Approaching (not necessarily matching) CrysMAS's scope using Nek5000/NekRS as the numerical core would require, at minimum, the following work packages. Rough relative-effort estimates (not calendar-time commitments, since parallelizable across a team) are given assuming a small team (2–4 senior CFD/numerical-methods engineers) with working familiarity with the Nek codebase.

1. **Radiative heat transfer module (high effort, high risk).** Implementing surface-to-surface diffuse-gray radiation exchange on Nek's curvilinear, high-order surface meshes requires view-factor computation (itself nontrivial on non-planar, high-order-mapped surfaces), a radiosity (or discrete ordinates / Monte Carlo, if higher fidelity or non-gray/non-diffuse behavior is needed) solve, and coupling of the resulting net radiative flux into the energy equation's boundary condition — recomputed as the interface and free-surface geometry evolve. This is likely the single largest and riskiest work package, since it has no analog anywhere in the existing Nek ecosystem and directly determines whether the global thermal balance (dominant driver of interface shape) can be captured at all.

2. **Interface-tracking / Stefan condition on the ALE framework (high effort, medium-high risk).** Extending Nek's existing ALE moving-mesh machinery to solve a genuine phase-change front — latent heat release, interface energy balance setting local interface velocity, and mesh motion consistent with that velocity while preserving mesh quality over the (potentially large) excursions of a growing boule — is a substantial numerical-methods undertaking, though it builds on infrastructure Nek already has (unlike radiation, which starts from zero).

3. **Free-surface meniscus model with growth-angle/contact-line physics (medium-high effort, medium-high risk).** A CZ-specific meniscus model requires a capillary boundary condition, a moving/pinned triple line, and coupling to diameter-control logic — conceptually related to, but more specialized than, the free-surface and level-set work already demonstrated for other ALE-based melt/liquid-metal free-surface problems in the literature, which provides a useful methodological starting point rather than a ready-made solution.

4. **Segregation and species transport at the moving front (medium effort, low-medium risk).** Given CHT and passive-scalar transport already exist natively, adding a segregation-coefficient boundary condition at the (now-tracked) interface is a comparatively modest incremental extension once work packages 1–2 are in place.

5. **Materials property database and furnace-geometry/meshing front end (medium effort, low risk, but high "invisible" cost).** Curating validated temperature-dependent properties for melts and furnace materials, and building even a modest parametric geometry/meshing front end for hot-zone configurations, is unglamorous but essential engineering that determines whether the tool is usable by anyone beyond its original developers.

6. **Verification and validation against CZ-specific benchmarks (high effort, ongoing).** Every new module above requires dedicated V&V — ideally against the same instrumented model experiments and benchmark comparisons already used to validate CrysMAS and peer codes — before results can be considered industrially credible. This is not a one-time cost but an ongoing commitment as the tool evolves.

**Overall assessment:** closing the gap to CrysMAS-equivalent physics coverage is a multi-year effort (order of several person-years of specialized numerical-methods and CFD development, plus sustained V&V), with the radiation module and interface-tracking/free-surface physics as the dominant cost and risk drivers. This is a realistic undertaking for a well-resourced national laboratory, large industrial R&D group, or multi-institution consortium — not a side project. A partial build-out (e.g., CHT + ALE interface tracking + a simplified radiative boundary condition, without full furnace-scale radiosity) is a substantially lower-effort, still-valuable target for melt-turbulence-focused research use.

---

## 7. Recommendations

### 7.1 For Academic Research

Nek5000/NekRS is an excellent — arguably the best currently available open-source — platform for **fundamental studies of melt convection instabilities, transition to turbulence, and 3D flow structures** in CZ-relevant geometries (rotating cylinder with differentially heated boundaries, approximating the melt domain), particularly where the research question concerns flow physics rather than furnace-scale thermal design. Recommended approach: use simplified, prescribed boundary conditions (imposed wall temperatures or heat fluxes derived from a companion CrysMAS/CGSim global model, or from published experimental/numerical benchmarks) rather than attempting to build full radiative/interface-tracking capability in-house, unless the research program specifically targets numerical-methods development for crystal growth.

### 7.2 For Industrial Process Engineering

CrysMAS (or an equivalent mature global furnace code such as CGSim or FEMAG-CZ) remains the appropriate primary tool for **hot-zone design, heater power scheduling, pull/rotation-rate optimization, and interface-shape control** — the day-to-day work of CZ process engineering — given its validated radiation and segregation models, materials database, and usability for non-CFD-specialist engineers. Nek5000/NekRS is not recommended as a replacement for this workflow given current capability gaps and the absence of CZ-specific V&V.

### 7.3 For Coupled/Hybrid Workflows (Recommended Middle Path)

The most cost-effective near-term path for organizations wanting the accuracy benefits of Nek without the full multi-year development investment is a **loosely coupled, one-way or iteratively coupled workflow**:
- Use CrysMAS (or equivalent) to compute the global quasi-steady thermal/radiative field and interface shape for a given process point.
- Extract melt-domain boundary conditions (crucible wall temperature distribution, interface temperature/shape, free-surface conditions) from the CrysMAS solution.
- Run a high-fidelity, time-resolved 3D Nek5000/NekRS melt simulation with these boundary conditions to resolve turbulent/oscillatory flow structures, striation-relevant temperature fluctuations, or MHD damping effects at a level of detail CrysMAS's 2D axisymmetric model cannot provide.
- Feed back effective heat- and mass-transfer coefficients (turbulence-corrected Nusselt/Sherwood-type correlations) from the Nek simulation into the CrysMAS global model to improve its melt-convection closure for subsequent design iterations.

This hybrid approach captures most of the practical value of both tools without requiring the full CrysMAS-equivalent physics stack to be rebuilt inside Nek, and is consistent with how coupled/multi-code approaches (e.g., CrysMAS + Cats2D, or global-model + CFD-specialist-code pairings) are already used elsewhere in the crystal growth simulation literature.

### 7.4 For Organizations Considering the Full Build-Out

If an organization's strategic need genuinely requires a fully self-contained, 3D, time-resolved, radiation-and-interface-coupled CZ simulation environment at exascale-relevant parallel efficiency (e.g., very large-diameter silicon ingots, novel furnace geometries far outside CrysMAS's validated envelope, or research into inherently 3D phenomena like non-axisymmetric radiative environments), then investment in the Nek5000/NekRS extension path outlined in Section 6 is justified — but should be scoped and staffed as a multi-year software/numerical-methods program with dedicated V&V, not as an incremental addition to existing CFD work.

---

## 8. Conclusion

Nek5000/NekRS and CrysMAS occupy genuinely different, largely complementary positions in the CZ crystal growth simulation landscape. Nek's spectral accuracy and extreme scalability make it the superior tool for resolving the 3D, unsteady, turbulent melt-flow physics that a global 2D axisymmetric furnace code structurally cannot capture; CrysMAS's integrated, validated, radiation-coupled global furnace model — accumulated over decades of dedicated Fraunhofer IISB development — has no equivalent in standard Nek and would require a substantial, multi-year engineering effort to approximate, with radiative heat transfer and moving-interface/free-surface physics as the principal technical risks. Organizations should not view this as a choice between the two tools, but as an opportunity for a coupled workflow that uses each where it is strongest, reserving the considerable investment of building CrysMAS-equivalent physics into Nek for cases where the strategic need for a fully integrated, exascale-capable, high-fidelity CZ environment clearly outweighs the engineering cost.

---

## Key References

1. Fischer, P., Lottes, J., Kerkemeier, S., Marin, O., Heisey, K., Obabko, A., Merzari, E., Peet, Y. *Nek5000: User's Manual.* Technical Report ANL/MCS-TM-351, Argonne National Laboratory, 2015.
2. Fischer, P. F. "An overlapping Schwarz method for spectral element solution of the incompressible Navier–Stokes equations." *Journal of Computational Physics*, 133(1), 84–101, 1997.
3. Fischer, P., et al. "NekRS, a GPU-Accelerated Spectral Element Navier–Stokes Solver." *arXiv:2104.05829*, 2021.
4. "Towards Exascale for Wind Energy Simulations" (Nek5000/RS overview). *arXiv:2210.00904*, 2022.
5. "Spectral Element Simulation of Liquid Metal Magnetohydrodynamics." *arXiv:2410.00202*, 2024.
6. "Direct Numerical Simulation of High Prandtl Number Fluid Flow in the Downcomer of an Advanced Reactor." *arXiv:2203.14157* and *arXiv:2304.04085*.
7. "A comprehensive framework to enhance numerical simulations in the spectral-element code Nek5000." *Computer Physics Communications*, ScienceDirect, 2024.
8. Karp, M., et al. "Neko: A Modern, Portable, and Scalable Framework for High-Fidelity Computational Fluid Dynamics." *arXiv:2107.01243*, 2021.
9. Nek5000 documentation: "Conjugate Heat Transfer" tutorial, nek5000.github.io/NekDoc.
10. Nek5000/NekExamples repository (free-surface channel flow, ALE peristaltic flow examples), GitHub: Nek5000/NekExamples.
11. Vegendla, P., Tentner, A., Shaver, D., Obabko, A., Merzari, E. "Development and Validation of a Conjugate Heat Transfer Model for the Two-Phase CFD Code NEK-2P." Argonne National Laboratory publication.
12. "Nek5000: Improvements in the Available RANS..." ANL/NSE-21/79, Argonne National Laboratory.
13. Fraunhofer IISB, Equipment Simulation research page: iisb.fraunhofer.de/en/research_areas/materials/equipment_simulation.html.
14. Friedrich, J. "Erlangen — An Important Center of Crystal Growth and Epitaxy: Major Scientific Results and Technological Solutions of the Last Four Decades." *Crystal Research and Technology*, Wiley, 2020.
15. "Global simulation of the Czochralski silicon crystal growth in ANSYS FLUENT." *Journal of Crystal Growth*, ScienceDirect, 2013 (contains comparative survey of CGSim, CrysMAS/STHAMAS, FEMAG-CZ).
16. "Validation, verification, and benchmarking of crystal growth simulations." *Journal of Crystal Growth*, ScienceDirect, 2017.
17. "Development and validation of a thermal simulation for the Czochralski crystal growth process using model experiments." *Journal of Crystal Growth*, ScienceDirect, 2022.
18. CrysMAS Manual, Fraunhofer IISB: download.iisb.fraunhofer.de/downloads/Manual/index.html.
19. "Process modeling of the industrial VGF growth process using the software package CrysVUN++" (references CrysMAS/Cats2D coupling), ResearchGate.
20. "Numerical Simulation of Free Surface Deformation and Melt Stirring in Induction Melting Using ALE and Level Set Methods." PMC/NCBI, 2024 (methodologically relevant ALE/level-set free-surface precedent).
21. Derby, J. J., Brown, R. A. "Thermal-capillary analysis of Czochralski and liquid encapsulated Czochralski crystal growth: I. Simulation." *Journal of Crystal Growth*, 74, 605–624, 1986.
22. Müller, G., Friedrich, J. "Challenges in modeling of bulk crystal growth." *Journal of Crystal Growth*, 266, 1–19, 2004.
23. Lan, C. W. "Recent progress of crystal growth modeling and growth control." *Chemical Engineering Science*, 59, 1437–1457, 2004.

---

*Report prepared for CZ crystal growth / CFD / multiphysics research and engineering audiences. Delivered as Markdown per standard technical documentation conventions.*

---

> [!NOTE]
> 
> Generated by Claude.ai
>
> Model: Sonet 4.6
>
> Prompt: Write a comprehensive, technically rigorous report evaluating the suitability of NEK fast high-order scalable CFD for high-fidelity numerical simulation of the Czochralski (CZ) crystal growth process. The report should critically assess NEK fast high-order scalable CFD's capabilities, limitations, required extensions, and practical implementation challenges. It should also provide a detailed comparison with CrysMAS, the dedicated crystal-growth simulation software developed by the Fraunhofer Institute for Integrated Systems and Device Technology (Fraunhofer IISB). The report should be written for researchers and engineers involved in semiconductor crystal growth, computational fluid dynamics (CFD), heat transfer, and multiphysics simulation.
> Objectives
> Determine whether NEK fast high-order scalable CFD can serve as a viable platform for industrial-grade CZ crystal growth simulation.
> Identify which physical phenomena can be modeled using standard NEK fast high-order scalable CFD capabilities and which require custom development.
> Compare NEK fast high-order scalable CFD with CrysMAS regarding physics coverage, numerical methods, validation status, industrial readiness, scalability, extensibility, and usability.
> Assess the effort required to build a CZ simulation environment in NEK fast high-order scalable CFD that approaches the capabilities of CrysMAS.
> Provide recommendations for research, academic, and industrial use cases.
> Provide key references. Show the output in Markdown format.
