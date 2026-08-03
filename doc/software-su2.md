# Evaluating SU2 Foundation for High-Fidelity Czochralski Crystal Growth Simulation: A Comparative Technical Assessment Against CrysMAS

**Prepared for:** Researchers and engineers in semiconductor crystal growth, CFD, heat transfer, and multiphysics simulation
**Scope:** SU2 Foundation (open-source multiphysics CFD suite) vs. CrysMAS (Fraunhofer IISB dedicated crystal-growth software)
**Date:** August 2026

---

## Executive Summary

Czochralski (CZ) crystal growth is a multiphysics problem coupling turbulent/transitional melt convection, global (furnace-scale) conductive-radiative heat transfer, electromagnetics (for magnetically stabilized or induction-heated systems), free-surface and moving-interface dynamics, species/dopant segregation, and thermoelastic stress in the growing crystal. CrysMAS was purpose-built at Fraunhofer IISB over more than two decades specifically to solve this coupled problem for industrial silicon and compound-semiconductor growth, with a deformable global mesh, weak/global-coupling solvers for melt/crystal/gas/heater domains, radiation view-factor and surface-to-surface engines, and dopant segregation post-processors validated against decades of production data.

SU2 Foundation is a general-purpose, open-source, unstructured-mesh CFD/multiphysics framework developed originally at Stanford's Aerospace Design Lab and now stewarded by the SU2 Foundation. It offers a modern finite-volume compressible/incompressible flow solver, conjugate heat transfer (CHT), an emerging radiative heat transfer (RHT) module (P1/participating-media formulation), solid mechanics (FEA) for linear/nonlinear elasticity, discrete/continuous adjoint capability, and a Python-driven multi-zone coupling architecture (multiphysics driver) — all under LGPL 2.1, with MPI/GPU-oriented HPC scaling.

**Bottom line:** SU2 Foundation is **not a drop-in substitute for CrysMAS** and cannot, out of the box, perform an industrial CZ growth simulation. It lacks a moving/deformable free melt surface and solid-liquid interface tracking, a global view-factor radiation enclosure solver tuned for furnace geometries, induction/resistive electromagnetic heating coupled to Joule heating, dopant segregation and impurity transport models, crystal/melt phase-change (Stefan problem) handling, and any built-in crystal-growth process control (pulling rate, rotation, meniscus, diameter control). All of these are, in principle, buildable on top of SU2's multiphysics architecture using its CHT/RHT infrastructure, custom solvers, and Python multi-zone coupling layer — but doing so is a multi-year software engineering program comparable in scope to re-deriving a meaningful fraction of CrysMAS's functionality from primitives. SU2's strengths — modern numerics, adjoint-based sensitivity/optimization, active open-source development, GPU/HPC scalability, and free licensing — make it attractive for **targeted CZ subproblems** (melt convection stability studies, CHT benchmarking, sensitivity analysis of furnace thermal design) and for **research groups with sustained C++/HPC development capacity**, but it is not presently suited to replace CrysMAS for **routine industrial process design and qualification**.

---

## 1. Physics Requirements of CZ Crystal Growth Simulation

A credible CZ simulation must resolve, to varying fidelity, the following coupled phenomena:

1. **Melt hydrodynamics** — buoyancy-driven (Rayleigh–Bénard-type) convection, crystal and crucible forced rotation (potentially counter-rotating), Marangoni (thermocapillary) convection at the free melt surface, and — for magnetically stabilized CZ (MCZ) — Lorentz-force damping of turbulence. Flow regimes span laminar to transitional to turbulent depending on melt Grashof/Marangoni numbers and rotation rates (Taylor number), often requiring transient 3-D simulation because axisymmetric assumptions break down under realistic asymmetric heating and rotation.
2. **Global conductive-radiative heat transfer** — heat conduction through crucible, susceptor, insulation, gas, and crystal, coupled to surface-to-surface (and volumetric, for semi-transparent crystals) thermal radiation across a geometrically complex, non-convex furnace enclosure. Radiative exchange typically dominates the global energy balance in hot-zone design.
3. **Free melt surface (meniscus) shape and dynamics** — determined by a local force balance (surface tension, gravity, pressure) at the tri-junction (melt–crystal–gas contact line), governing crystal diameter and requiring free-boundary tracking.
4. **Solid–liquid (crystal–melt) interface** — a moving Stefan problem: latent heat release/absorption at a deformable phase boundary whose shape (concave/convex/flat) is a key process quality metric.
5. **Electromagnetics** (for induction-heated furnaces or MCZ) — eddy-current/induction heating (a low-frequency, quasi-static Maxwell problem) coupled to Joule heating in the susceptor, and/or static/AC magnetic fields coupled to the melt momentum equations via the Lorentz force (magnetohydrodynamics, MHD).
6. **Dopant/impurity segregation and species transport** — advection-diffusion of dopants in the melt, segregation at the growth interface (effective segregation coefficient, often a function of interface growth rate and boundary-layer transport), and incorporation into the growing crystal, determining axial/radial resistivity uniformity.
7. **Crystal thermoelastic stress** — thermal-gradient-induced stress in the growing crystal, relevant to dislocation generation and crystal quality (particularly for compound semiconductors).
8. **Global, quasi-steady process evolution** — pulling rate, crystal/crucible rotation schedules, crucible lift, and heater power control over the full growth run (which may span tens of hours and a strongly time-varying melt volume/aspect ratio), typically requiring a pseudo-transient or fully transient global model with mesh deformation as the crystal grows and melt level drops.

No single open-source general-purpose CFD code addresses all eight of these natively; the question is how much of this stack SU2 already provides versus what must be engineered.

---

## 2. SU2 Foundation: Architecture and Native Capabilities

### 2.1 Overview

SU2 (current stable release series 8.x, "Harrier") is a C++/Python open-source suite for solving PDE-constrained problems on unstructured meshes, originally developed at Stanford's Aerospace Design Lab and now governed by the nonprofit SU2 Foundation. <cite index="4-1">While initially developed for aerodynamics and compressible flow, it has evolved into a general-purpose multiphysics framework capable of simulating incompressible and compressible flows across all Mach regimes, species transport, conjugate heat transfer and combustion.</cite> <cite index="9-1">The SU2 code is an open-source suite of software tools written primarily in C++ and Python for the numerical solution of partial differential equations on unstructured meshes, with a focus on multiphysics simulation and design in fields such as computational fluid dynamics, released under the LGPL 2.1 license, with the latest stable version being 8.3.0 "Harrier" as of September 2025.</cite>

### 2.2 Flow solvers

- **Compressible and incompressible finite-volume Navier–Stokes solvers**, including RANS turbulence closures (Spalart–Allmaras, SST) — the incompressible solver with buoyancy (Boussinesq) source terms is the relevant regime for CZ melt convection, since melt Mach numbers are effectively zero and buoyancy/rotation dominate.
- Structured/unstructured mesh support, dual-mesh finite-volume discretization, and standard limiters/upwind schemes (Roe, JST, etc.).

### 2.3 Heat transfer

- **Conjugate Heat Transfer (CHT):** SU2 supports coupled fluid–solid heat transfer via a dedicated multiphysics driver that exchanges temperature and heat-flux boundary data between zones at a shared interface, with both steady and unsteady formulations documented in the official tutorials <cite index="5-1">for optimization purposes, SU2 can perform discrete adjoint solutions for multiphysics simulations as well, capturing all cross dependencies from the CHT coupling at the interfaces to give accurate sensitivities</cite>, and this extends to multi-solid, multi-fluid configurations including **contact resistance between solid zones** <cite index="6-1">handling typical engineering applications involving conjugate heat transfer that concern more than a single solid material, via configuration files for each physical zone and a master configuration invoking the multiphysics run</cite>, as well as **unsteady/transient CHT** <cite index="7-1">for unsteady flows around walls transferring heat from an adjacent solid zone, where the coupling of temperature and heat-flux distributions must be resolved at every time step</cite>.
- **Radiative Heat Transfer (RHT):** SU2 includes a participating-media radiation model (P1 approximation) coupled to CHT, demonstrated in tutorials combining <cite index="2-1">a multizone, multiphysics problem involving incompressible turbulent flows, radiation, and conjugate heat transfer between a solid domain and a buoyancy-driven cavity, including coupled adjoint solutions</cite>. This P1 model is a differential (rather than view-factor/surface-to-surface) radiation approximation, well-suited to optically participating gases but **not equivalent to the enclosure/view-factor radiation solvers used for furnace hot-zone design**, where surfaces exchange radiation across large, mostly-transparent gas gaps and view factors between complex, mutually-shadowing surfaces dominate the physics.

### 2.4 Structural and multiphysics coupling

- **Solid mechanics (FEA) solver:** linear and nonlinear elasticity, usable for structural/thermoelastic problems.
- **Fluid–Structure Interaction (FSI):** <cite index="4-1">static and dynamic coupling between fluid and structural solvers</cite>, built on the same multi-zone driver as CHT.
- **Discrete and continuous adjoint solvers** with algorithmic differentiation, giving SU2 a distinctive capability among open-source multiphysics codes: <cite index="4-1">exact discrete adjoint sensitivities for complex multiphysics chains, including fluid-structure interaction and conjugate heat transfer</cite>. This is directly reusable for CZ furnace **design sensitivity and optimization** (e.g., heater power distribution vs. interface shape) once a forward model exists.
- **Species transport and combustion:** <cite index="4-1">reacting flow modeling using the Flamelet Generated Manifold (FGM) method</cite> and general species transport — reusable, with substantial reformulation, as a starting point for dopant/impurity transport, though CZ segregation physics (partition coefficients at a moving solidification front) is qualitatively different from combustion species transport and is not natively supported.
- **Hypersonics/NEMO module:** <cite index="4-1">simulation of high-enthalpy flows including thermo-chemical non-equilibrium and ionization with detailed chemistry modeling</cite> — not directly relevant to CZ but demonstrates the code's extensibility to specialized physics via a plugin-like solver architecture.

### 2.5 What SU2 does *not* natively provide

- No moving/deformable free-surface (meniscus) solver with surface-tension force balance and tri-junction (contact-line) tracking.
- No solid–liquid phase-change (Stefan problem) formulation with latent heat and a deformable, sharp interface — SU2's mesh deformation capabilities (used for FSI and shape optimization) are a necessary but far from sufficient building block.
- No electromagnetic (induction heating / Lorentz force / MHD) solver. There is no Maxwell equation solver or magnetic vector potential formulation in mainline SU2.
- No view-factor/enclosure radiation solver for the geometrically complex, largely transparent-gas hot-zone radiative exchange that dominates CZ furnace thermal design (the P1 participating-media model targets a different regime).
- No dopant segregation, effective segregation coefficient, or crystal-growth process control (pulling rate/rotation/diameter control loop) logic.
- No crystal-growth-specific material property database (temperature-dependent viscosity, radiative properties, emissivity tables for silicon melt/solid, quartz, graphite, etc.) — SU2's fluid property models are aerodynamics/combustion-oriented (ideal/real gas, incompressible with simple property laws) and would need a custom property module.
- No pre/post-processing tooling for crystal-growth-specific outputs (interface deflection, striations, dopant radial/axial profile, thermal stress maps referenced to crystallographic orientation).

---

## 3. CrysMAS: Architecture and Native Capabilities

CrysMAS ("Crystal Growth Modelling Analysis System") is developed and maintained by Fraunhofer IISB (Erlangen) specifically for bulk crystal growth from the melt — Czochralski, Bridgman, VGF, and related processes — for silicon, compound semiconductors (GaAs, InP, GaN substrates), and oxide crystals. Its design center is the **global furnace model**: a single coupled simulation spanning melt, crystal, crucible, susceptor, insulation, heaters, gas/vacuum ambient, and (optionally) coils, solved together rather than as isolated CFD or heat-transfer subproblems.

Key native capabilities, consistent with the technical literature on the code and its predecessor/sibling tools (STHAMAS, CrysVUn lineage) developed at Fraunhofer IISB and associated groups (Müller, Friedrich et al.):

- **Deformable global mesh with automatic remeshing** as the crystal grows, the melt level drops, and the crystal/melt interface deflects — enabling quasi-steady or fully transient simulation of an entire growth run.
- **Coupled melt convection** (laminar, transitional and turbulence-modeled regimes), **crystal/crucible rotation**, and **Marangoni convection** at the free melt surface, with the free surface shape computed from a local force balance rather than assumed flat.
- **Solid–liquid interface tracking** as a genuine moving boundary (Stefan problem) with latent heat release, allowing prediction of interface deflection (a key process quality/facet/dislocation indicator) as a direct simulation output.
- **Global radiative heat exchange solver** using view-factor/enclosure (surface-to-surface) methods appropriate to the largely non-participating gas ambient typical of CZ hot zones, including diffuse-gray and (in more advanced configurations) spectral/band radiation and specular reflection at select surfaces (important for polished crucibles/heat shields).
- **Electromagnetic (induction heating) coupling** for RF/induction-heated furnaces, solving the eddy-current problem in the susceptor/coil system and feeding the resulting Joule heating distribution into the global thermal model — and, in MCZ variants, coupling static/AC magnetic fields to melt momentum via Lorentz-force damping.
- **Dopant/impurity segregation modules**, computing species transport in the melt and incorporation at the growth interface via an effective segregation coefficient formulation, producing axial/radial dopant (and hence resistivity) profile predictions that can be compared directly against production wafer maps.
- **Thermoelastic stress post-processing** in the growing crystal from the computed thermal field, used to flag conditions likely to nucleate dislocations.
- **Process-oriented UI and workflow**: parameterized hot-zone geometry construction, material property databases curated for crystal-growth-relevant materials (silicon melt/solid, quartz, graphite, various insulation and susceptor materials), and process-schedule definition (pulling rate, rotation profiles, power ramps) as first-class simulation inputs — rather than generic boundary condition files.
- **Validation pedigree**: CrysMAS and its predecessor STHAMAS/CrysVUn-family tools have been validated over roughly two decades against industrial Czochralski silicon growth (including large-diameter, e.g., 300 mm and 450 mm-class hot-zone studies conducted with/for industrial partners), VGF/Bridgman compound-semiconductor growth, and published comparisons of predicted vs. measured interface shape, temperature fields, and dopant distribution.

CrysMAS is proprietary/licensed software (available under license from Fraunhofer IISB, historically also distributed for a period via STR Group under the name "CGSim" lineage relationship — note CGSim and CrysMAS are related but distinct commercial offerings with overlapping IISB heritage); it is not open source, and its internal numerics (mesh generation, linear solvers, coupling schemes) are not fully disclosed in the way an open-source code's are, though the underlying physical models are documented in the peer-reviewed crystal-growth literature by the IISB group and collaborators.

---

## 4. Side-by-Side Comparison

| Dimension | SU2 Foundation (native) | CrysMAS |
|---|---|---|
| **Primary design intent** | General-purpose aerodynamics/multiphysics CFD, adjoint-based design optimization | Purpose-built global furnace model for melt crystal growth |
| **Melt convection (buoyancy, rotation)** | Yes — incompressible RANS/laminar solver with Boussinesq buoyancy; rotation via moving reference frame / rotating mesh | Yes — native, tuned for CZ regimes (Gr, Ta, Ma numbers), decades of validation |
| **Free melt surface / meniscus** | Not available; would require custom ALE/level-set/VOF development | Native, force-balance-based free-surface solver |
| **Solid–liquid interface (Stefan problem)** | Not available natively | Native, deformable interface with latent heat |
| **Global conductive heat transfer** | Yes, via CHT multizone driver | Yes, native, integrated with radiation and EM |
| **Furnace-scale radiation** | P1 participating-media model only; not a view-factor/enclosure solver | Native view-factor/enclosure radiation solver, diffuse-gray and spectral options, specular surfaces |
| **Electromagnetics (induction heating, MHD)** | Not available | Native induction heating and MHD (MCZ) coupling |
| **Dopant/impurity segregation** | Not available; species transport exists but not segregation-at-interface physics | Native segregation modules validated against production resistivity maps |
| **Thermoelastic stress in crystal** | Solid mechanics (FEA) solver exists but not pre-integrated with the thermal/growth workflow | Native, integrated post-processing |
| **Mesh deformation for growth evolution** | General mesh-deformation infrastructure (built for FSI/shape optimization), not growth-specific | Native automatic remeshing tied to interface motion and melt-level drop |
| **Numerical methods** | Modern finite-volume, unstructured mesh, extensive limiter/scheme library, strong verification suite | Finite-volume/finite-element hybrid tuned to crystal-growth geometries; less publicly documented numerics |
| **Adjoint / sensitivity / optimization** | Strong native discrete & continuous adjoint via AD — a genuine differentiator | Not a general design-optimization framework; parametric studies via repeated runs |
| **HPC/GPU scalability** | Strong, actively developed MPI/GPU support, demonstrated on large aerospace cases | Adequate for furnace-scale problems; not benchmarked for extreme-scale HPC (not the target use case) |
| **Validation status for CZ** | None — no published CZ validation studies for mainline SU2 | Extensive — peer-reviewed validation against industrial Si and compound-semiconductor growth over ~20 years |
| **Industrial readiness for CZ** | Not ready; a research prototype at best without substantial extension | Industrial-grade; used in production hot-zone design |
| **Licensing / cost** | Free, open source, LGPL 2.1 | Commercial license from Fraunhofer IISB (cost, support agreement) |
| **Extensibility / source access** | Full source access, active public GitHub development, large community | Source generally not open; extension paths mediated by Fraunhofer IISB |
| **Usability for crystal growers** | Requires CFD/C++/Python expertise; no crystal-growth-specific UI or material database | Domain-specific UI, curated material databases, process-schedule-driven workflow |
| **Community & long-term support** | Active open-source community, SU2 Foundation governance, university-driven development | Institutional support from Fraunhofer IISB; continuity tied to institute funding/roadmap |

---

## 5. Physical Phenomena: Native vs. Custom-Development Requirement in SU2

| Phenomenon | SU2 status | Development effort to reach CrysMAS-comparable fidelity |
|---|---|---|
| Turbulent/laminar melt convection with buoyancy | Native (incompressible solver + Boussinesq) | Low–moderate: property model tuning, verification against CZ benchmark cases (e.g., published benchmark melt flows) |
| Crystal/crucible rotation | Native (rotating reference frame; sliding mesh for counter-rotation) | Low–moderate: validating counter-rotating configurations and Ekman/Stewartson layer resolution |
| Marangoni (thermocapillary) convection | Not native | Moderate: requires implementing a temperature-dependent surface-tension boundary condition on a *moving* free surface — coupled to the free-surface problem below |
| Free melt surface / meniscus tracking | Not native | High: full ALE or interface-tracking (level-set/VOF) implementation with surface-tension force balance and dynamic contact-line/tri-junction handling; SU2's existing mesh-deformation infrastructure (built for FSI/shape optimization) is a partial building block but the physics (surface energy minimization, meniscus angle) must be added from scratch |
| Solid–liquid interface (Stefan problem) | Not native | High: latent-heat-release moving-boundary formulation, mesh topology changes as crystal grows, interface-shape solution coupled to the thermal field on both sides |
| Global conductive heat transfer (crucible/susceptor/insulation/gas) | Native (CHT) | Low: mainly a matter of building the multizone case (multiple solid + fluid zones, correct BCs) |
| Furnace-scale (enclosure) radiation | Partial (P1 participating media only) | High: implement a view-factor/surface-to-surface radiation solver appropriate for largely transparent, geometrically complex, mutually shadowing hot-zone surfaces — a substantially different numerical approach from P1 |
| Induction heating / Joule heating coupling | Not native | High: implement a low-frequency (quasi-static) electromagnetic solver (e.g., A-V or A-phi formulation) and couple its Joule-heating output into the thermal model |
| MHD (Lorentz-force damping in MCZ) | Not native | High: implement magnetic field coupling into the momentum equations; requires either a resolved EM solve or, more practically, prescribed/analytic magnetic field with a Lorentz-force source term |
| Dopant/impurity segregation | Partial (generic species transport exists) | Moderate–high: implement moving-interface segregation boundary conditions (effective segregation coefficient dependent on interface velocity and boundary-layer transport) tied into the moving solid–liquid interface development above |
| Thermoelastic stress in the growing crystal | Partial (linear elasticity FEA solver exists) | Moderate: coupling the existing solid solver's thermal-stress capability to the transient thermal field from the growth simulation, plus crystallographic anisotropy if needed |
| Process control (pulling rate, diameter control, power ramps as simulation drivers) | Not native | Moderate: scripting layer atop SU2's Python multiphysics driver to impose time-varying boundary motion/heater power as a function of a simulated or prescribed control law |
| Transient, growth-run-length simulation with evolving geometry | Partial (mesh deformation exists for FSI) | High: combining moving free surface + moving Stefan interface + shrinking melt volume + growing crystal length into one coherent transient mesh-topology-evolving simulation is the single largest integration challenge |

**Aggregate assessment:** of the roughly dozen physical/numerical building blocks required, SU2 provides strong native support for perhaps 2–3 (melt convection, rotation, conductive CHT), partial/adjacent support for another 2–3 (species transport, solid mechanics, general mesh deformation), and no native support at all for the remainder — including the two hardest and most CZ-specific items: the deformable free melt surface and the moving solid–liquid interface. These two, plus furnace-scale radiation and electromagnetics, constitute the physics that makes CZ simulation a specialized discipline in the first place, and they are precisely what CrysMAS was built to solve.

---

## 6. Numerical Methods Comparison

- **Discretization:** SU2 uses a modern, well-verified unstructured finite-volume method with a broad library of upwind schemes, limiters, and time-integration strategies (implicit dual-time-stepping for unsteady problems), backed by an active verification/validation test suite maintained by the open-source community. CrysMAS's numerics are less publicly documented (as is typical for a licensed institutional code) but are purpose-tuned for the specific combination of natural/mixed convection, conjugate radiation-conduction, and moving-boundary problems characteristic of crystal growth; published IISB papers describe finite-volume/finite-element formulations for the coupled melt–radiation–EM system.
- **Coupling strategy:** SU2's multizone driver performs a Gauss–Seidel-type (or Jacobi, configurable) block coupling between zones at each outer iteration — a general-purpose approach adequate for CHT/FSI but not purpose-tuned for the very different time/length scales present in CZ (fast melt turbulence vs. slow crystal growth vs. even slower thermal quasi-equilibrium of the hot zone). CrysMAS's coupling is specifically designed around this multi-scale structure, typically exploiting quasi-steady-state assumptions for melt flow within a slowly evolving global thermal/geometric state.
- **Adjoint/sensitivity methods:** This is SU2's clearest numerical advantage. Its algorithmic-differentiation-based discrete adjoint, already demonstrated across CHT and FSI multiphysics chains, would — once a forward CZ model existed — enable gradient-based hot-zone design optimization (e.g., minimizing interface deflection or maximizing thermal uniformity with respect to heater geometry/power) far more efficiently than the parametric sweep approach typically used with CrysMAS. This is a genuine research opportunity but presupposes the forward model already described as a multi-year undertaking.
- **Mesh deformation:** SU2's mesh-deformation module (linear elasticity or IDW-based) is built for shape-optimization and FSI use cases involving *bounded* deformation of a largely fixed topology — not for the essentially unbounded, topology-changing deformation of a shrinking melt volume and growing crystal over a multi-hour process. CrysMAS's remeshing is purpose-built for exactly this scenario.

---

## 7. Validation Status

- **SU2:** Extensively validated for its core aerospace/automotive CFD, CHT, and FSI use cases (documented in the AIAA Journal reference publication and a large body of peer-reviewed applications) <cite index="8-1">demonstrated on a number of applications, solving both the flow and adjoint systems of equations to provide a high-fidelity predictive capability and sensitivity information usable for optimal shape design, goal-oriented adaptive mesh refinement, or uncertainty quantification</cite>. However, **no published validation of SU2 against Czochralski (or any melt crystal growth) benchmark or production data exists** in the mainstream literature at the time of writing. Any CZ application would need to be validated essentially from zero, against classical melt-convection benchmark problems (e.g., the well-known CZ/oxide-melt benchmark flows used in the crystal-growth CFD literature) before any claim of predictive fidelity could be made.
- **CrysMAS:** Validated over roughly two decades against industrial silicon CZ growth (multiple diameter classes), VGF/Bridgman compound semiconductor growth, and published comparisons of simulated vs. measured thermal fields, interface shapes, and dopant profiles, by the Fraunhofer IISB group and academic/industrial collaborators. This validation pedigree is arguably CrysMAS's single most important asset relative to any general-purpose CFD code, since crystal-growth process design decisions (hot-zone geometry, heater power schedules, pulling rate profiles) are made against simulation predictions with real financial and yield consequences.

---

## 8. Scalability, Extensibility, and Usability

**Scalability:** SU2's MPI/domain-decomposition and (increasingly) GPU-accelerated architecture is designed for large-scale HPC problems (hundreds to thousands of cores for aerospace external-flow cases) and would, in principle, scale a CZ global model well beyond what CrysMAS's typical deployment targets (workstation/small-cluster scale, since furnace-scale meshes are modest by aerospace CFD standards, generally O(10^5)–O(10^7) cells). This SU2 advantage is real but largely irrelevant to CZ simulation: furnace-scale meshes rarely require extreme-scale HPC, so SU2's scalability headroom is unlikely to be a decisive factor unless very high-resolution transient turbulent melt convection (fully resolved LES/DNS, rather than RANS) becomes a specific research goal.

**Extensibility:** SU2's open architecture (full C++ source, documented solver/interface base classes, an active plugin-style pattern already used for its hypersonics/NEMO and combustion/FGM modules) is a genuine advantage for a research group prepared to build the missing CZ physics as new SU2 solver modules, following the same pattern used to add those existing specialized capabilities. CrysMAS's extensibility, by contrast, is mediated by Fraunhofer IISB — external groups cannot generally add fundamentally new physics modules themselves, though the institute has historically been open to collaborative extension for specific research partnerships.

**Usability:** This is where the gap is starkest in the opposite direction. CrysMAS provides a domain-specific graphical workflow: parameterized hot-zone construction, curated material property databases for crystal-growth-relevant materials, process-schedule input as a first-class concept, and outputs formatted for direct comparison to production metrics (resistivity maps, interface shape). SU2 provides none of this for CZ; every aspect — geometry, meshing strategy, material properties, boundary condition schedules, post-processing — would need to be built and maintained by the user as a bespoke case setup, with no crystal-growth-specific tooling to draw on. For a production engineer needing rapid hot-zone design iteration, this usability gap alone is often decisive.

---

## 9. Effort Estimate: Building a CrysMAS-Comparable CZ Capability in SU2

Based on the phenomenon-by-phenomenon assessment in Section 5, a realistic program to bring SU2 to approximate CrysMAS-level CZ capability would involve, at minimum:

1. **Free-surface/meniscus solver** (ALE or interface-tracking with surface-tension force balance and contact-line handling) — the single largest new solver development, likely 12–24 person-months for a robust, general implementation, informed by existing ALE literature in crystal growth (e.g., the finite-element ALE approaches used by academic groups such as Derby/Minnesota or Dupret/UCLouvain) but requiring substantial original implementation work within SU2's finite-volume architecture, which was not designed with sharp moving interfaces as a first-class concept.
2. **Solid–liquid interface / Stefan problem solver**, coupled to the free-surface solver and to global mesh topology evolution as the crystal grows — comparable or greater effort, likely 12–24 person-months, and the two (free surface + solid-liquid interface) are not cleanly separable since both drive the same evolving mesh.
3. **Furnace-scale (view-factor/enclosure) radiation solver** as an alternative/complement to the existing P1 model — 6–12 person-months, informed by well-established view-factor and radiosity methods, but requiring implementation and verification against a nontrivial existing solver base.
4. **Electromagnetic (induction heating) solver** and/or MHD Lorentz-force coupling for MCZ — 6–12 person-months depending on whether a fully resolved quasi-static EM solve or a prescribed/analytic-field approximation is acceptable.
5. **Dopant segregation module**, built once the moving interface exists — 3–6 person-months.
6. **Material property database and process-schedule/control scripting layer** — 3–6 person-months, largely software-engineering rather than solver-physics work, but essential for usability.
7. **Integration, verification against classical CZ/melt-convection benchmarks, and validation against at least one industrial or well-documented published CZ case** — 6–12 person-months, and arguably never fully "complete" in the way CrysMAS's two-decade validation record is.

**Aggregate estimate:** on the order of **4–8 person-years of specialized CFD/multiphysics software development**, assuming a team with existing SU2 internals expertise, strong crystal-growth physics background, and access to validation data — realistically a **multi-year (3–5 calendar year) program** even with a small dedicated team, before reaching a capability set that industrial CrysMAS users would consider comparable. This is consistent with the general pattern seen when general-purpose open-source CFD frameworks are extended toward other specialized moving-boundary multiphysics domains (e.g., welding, casting, additive manufacturing melt-pool simulation), where such extension efforts typically span years and are usually undertaken by dedicated academic groups or national laboratories rather than as incidental additions.

It is worth noting explicitly: this effort estimate is **not** a criticism of SU2, which was never designed for this application domain. It reflects the genuine specialization embedded in CrysMAS, accumulated over roughly twenty years of Fraunhofer IISB development specifically targeted at crystal growth.

---

## 10. Recommendations by Use Case

### 10.1 Academic / fundamental fluid dynamics research
**Recommended:** SU2 is well suited to **isolated melt-convection subproblems** — studying transition to turbulence, Rayleigh–Bénard/Taylor–Couette-type instabilities in idealized CZ-like geometries, rotation effects, or verification of new turbulence/transition models — especially where the free surface can be reasonably approximated as flat/rigid (a common simplifying assumption in fundamental melt-convection studies) and where the research question does not require furnace-scale radiation or a moving solid-liquid interface. SU2's adjoint capability is additionally attractive for sensitivity studies (e.g., which boundary condition or geometric parameter most strongly influences melt flow stability). CrysMAS is generally not designed as an open research testbed for this kind of fundamental numerical-methods work, and its license terms may restrict this use.

### 10.2 CHT/RHT benchmarking and furnace-component-level studies
**Recommended:** For sub-problems that isolate conductive-radiative heat transfer in a *fixed* (non-growing, non-deforming) geometry — e.g., evaluating a candidate heat-shield or insulation design's thermal performance in isolation — SU2's existing CHT and P1 RHT infrastructure is directly usable with modest case-setup effort, and the discrete adjoint enables efficient design sensitivity studies unavailable in CrysMAS. This is a genuinely practical near-term use case that does not require the multi-year development program of Section 9.

### 10.3 Industrial process design and qualification (full CZ growth simulation)
**Not recommended on SU2 in its current form.** CrysMAS (or comparable dedicated tools such as CGSim/STR Group, FEMAG-CZ, or CrysVUn) remains the appropriate choice for production hot-zone design, pulling-schedule optimization, dopant uniformity prediction, and any use case where validated, production-comparable predictions are required on an industrially relevant timeline. The absence of native free-surface, moving-interface, furnace-scale radiation, and electromagnetics support in SU2 makes any attempt to use it directly for this purpose both under-resourced relative to the physics required and unvalidated relative to CrysMAS's two-decade track record.

### 10.4 Long-horizon strategic development (open-source CZ simulation capability)
**Conditionally recommended**, for organizations (national laboratories, university consortia, or industrial R&D groups with sustained multi-year software investment appetite) specifically motivated by the goal of an **open-source, license-free, adjoint-enabled alternative to CrysMAS** — for instance to enable broader academic access, gradient-based hot-zone optimization at a scale CrysMAS's workflow does not support, or integration with SU2's broader HPC/GPU roadmap. This is a legitimate and valuable research program, but sponsors should enter it with the effort estimate of Section 9 (multi-year, several person-years) as a realistic planning baseline, not as an incremental extension project. A staged approach — starting with the CHT/RHT benchmarking use case (10.2), then the free-surface solver, then the moving Stefan interface, then electromagnetics and segregation — allows incremental validation and de-risking rather than a single large integration effort.

### 10.5 Hybrid workflows
A pragmatic middle path for organizations already invested in both ecosystems: use **CrysMAS for the global, validated, production-relevant CZ process simulation**, and use **SU2 as a high-fidelity companion tool for targeted subproblems** — e.g., resolving melt turbulence at higher fidelity (LES) than CrysMAS's typical RANS-class melt models in a fixed-geometry snapshot extracted from a CrysMAS solution, or performing adjoint-based sensitivity studies on a simplified sub-geometry to guide CrysMAS parametric studies. This leverages each tool's genuine strength without requiring either a multi-year SU2 extension program or abandoning CrysMAS's validated global model.

---

## 11. Key References

1. Economon, T. D., Palacios, F., Copeland, S. R., Lukaczyk, T. W., & Alonso, J. J. (2016). "SU2: An Open-Source Suite for Multiphysics Simulation and Design." *AIAA Journal*, 54(3), 828–846. https://doi.org/10.2514/1.J053813
2. SU2 Foundation. SU2 official documentation and tutorials, including "Static Conjugate Heat Transfer (CHT)," "Solid-to-Solid Conjugate Heat Transfer with Contact Resistance," "Unsteady Conjugate Heat Transfer," and "Turbulent CFD-RHT-CHT including Adjoint Sensitivities." https://su2code.github.io/tutorials/
3. SU2 Foundation project website. https://su2code.github.io/
4. SU2 source repository and release notes (v8.x "Harrier" series). https://github.com/su2code/SU2
5. Fraunhofer IISB. CrysMAS product documentation and technical descriptions (Fraunhofer IISB, Erlangen, Germany). https://www.iisb.fraunhofer.de/
6. Müller, G., & Friedrich, J. (and associated Fraunhofer IISB / Erlangen-Nürnberg publications). Numerous peer-reviewed papers on global furnace modeling, Czochralski melt convection, and dopant segregation simulation, published primarily in the *Journal of Crystal Growth* and at the International Conference on Crystal Growth (ICCG) proceedings over the past two decades.
7. Derby, J. J., and coworkers (University of Minnesota). Publications on finite-element and ALE methods for melt crystal growth free-boundary and moving-interface problems, *Journal of Crystal Growth* and *Journal of Computational Physics*.
8. Dupret, F., and coworkers (Université catholique de Louvain). Publications on global thermal modeling and free-boundary methods for Czochralski growth.
9. Kakimoto, K. (Tohoku University) and coworkers. Publications on turbulent melt convection and magnetic field effects (MCZ) in Czochralski silicon growth.
10. General crystal-growth-simulation-software literature comparing CGSim, CrysMAS, FEMAG/FEMAG-CZ, and CrysVUn — see the crystal-growth simulation software reference compendium (internal reference library) for detailed per-code technical assessments.

---

*This report is a technical assessment based on publicly documented SU2 capabilities as of mid-2026 and the published technical/scientific literature describing CrysMAS's design and validation history. Where SU2's exact current feature set is time-sensitive (an actively developed open-source project), readers should consult the current SU2 documentation (https://su2code.github.io/) to confirm capability details before committing to a development program.*

---

> [!NOTE]
> 
> Generated by Claude.ai
>
> Model: Sonet 5
>
> Prompt: Write a comprehensive, technically rigorous report evaluating the suitability of SU2 Foundation for high-fidelity numerical simulation of the Czochralski (CZ) crystal growth process. The report should critically assess SU2 Foundation's capabilities, limitations, required extensions, and practical implementation challenges. It should also provide a detailed comparison with CrysMAS, the dedicated crystal-growth simulation software developed by the Fraunhofer Institute for Integrated Systems and Device Technology (Fraunhofer IISB). The report should be written for researchers and engineers involved in semiconductor crystal growth, computational fluid dynamics (CFD), heat transfer, and multiphysics simulation.
> Objectives
> Determine whether SU2 Foundation can serve as a viable platform for industrial-grade CZ crystal growth simulation.
> Identify which physical phenomena can be modeled using standard SU2 Foundation capabilities and which require custom development.
> Compare SU2 Foundation with CrysMAS regarding physics coverage, numerical methods, validation status, industrial readiness, scalability, extensibility, and usability.
> Assess the effort required to build a CZ simulation environment in SU2 Foundation that approaches the capabilities of CrysMAS.
> Provide recommendations for research, academic, and industrial use cases.
> Provide key references. Show the output in Markdown format.
