# NEPTUNE_CFD + SYRTHES for High-Fidelity Czochralski Crystal Growth Simulation: A Technical Evaluation Against CrysMAS

**A comparative assessment for researchers and engineers in semiconductor crystal growth, CFD, heat transfer, and multiphysics simulation**

---

## Executive Summary

NEPTUNE_CFD and SYRTHES are both EDF/CEA-developed, open-source-adjacent simulation tools built for the nuclear thermal-hydraulics domain. NEPTUNE_CFD is a three-dimensional, multifield (Euler–Euler) CFD solver purpose-built for two-phase and single-phase reactor thermal-hydraulics, sharing its numerical kernel, finite-volume discretization, and GUI/SALOME infrastructure with EDF's general-purpose code, code_saturne. SYRTHES is EDF's finite-element/finite-volume conduction and radiation solver, most commonly deployed as a conjugate-heat-transfer (CHT) and radiative-enclosure partner coupled to code_saturne or NEPTUNE_CFD via the SALOME/CWIPI coupling stack.

Neither tool contains any built-in representation of the physics that define Czochralski (CZ) growth: there is no free/deformable melt–crystal interface, no crystal pulling/rotation kinematics, no phase-change (Stefan problem) tracking, no dopant segregation model, no electromagnetic (Lorentz force) solver for magnetic-field-assisted growth, and no view-factor radiation enclosure logic tailored to furnace geometries with moving parts. NEPTUNE_CFD's multifield architecture is a poor conceptual match for the single-phase, buoyancy/Marangoni/rotation-driven melt flow of CZ growth — its two-phase machinery (interfacial drag, boiling closures, bifluid turbulence) is irrelevant baggage for this application, and it would in practice be used in its single-phase-flow mode, at which point it is essentially a heavier, less flexible substitute for code_saturne itself. SYRTHES supplies only the conductive/radiative half of the problem and needs the melt-flow solver as a partner regardless of which one is chosen.

By contrast, **CrysMAS** (Fraunhofer IISB) is a dedicated, closed-source CZ/VGF/Bridgman growth simulator built from the ground up around a global-furnace, quasi-steady/transient axisymmetric model with an ALE-tracked melt/crystal interface, coupled electromagnetic and radiative-enclosure solvers, segregation and dislocation-density post-processing, and 25+ years of validation against silicon, GaAs, and oxide crystal-growth experiments.

**Bottom line:** NEPTUNE_CFD+SYRTHES is **not a viable near-term platform** for industrial CZ simulation without a multi-year, multi-person custom development program that essentially re-derives most of what CrysMAS already provides — and even after that investment, NEPTUNE_CFD's two-phase-oriented architecture makes it a strictly worse foundation than using code_saturne+SYRTHES directly (which was evaluated in a companion report in this series). For industrial CZ process design, CrysMAS (or CGSim/FEMAG-CZ) remains the correct tool. NEPTUNE_CFD+SYRTHES may have narrow research value only where genuine two-phase phenomena inside the CZ system must be resolved (e.g., inert-gas/argon flow with entrained bubbles, gas–melt interaction at the free surface, or bubble defects in the melt), or where an institution already possesses deep in-house NEPTUNE_CFD/SYRTHES/SALOME expertise and wishes to reuse it rather than adopt a new toolchain.

---

## 1. Introduction and Scope

### 1.1 The Czochralski Process and Its Simulation Requirements

Czochralski growth pulls a single crystal from a rotating crucible of melt, held in a furnace with radiative heating (resistive heaters or RF induction), often assisted by applied or cusp magnetic fields (MCZ/EMCZ) to damp turbulent melt convection. A predictive CZ simulation must resolve, in a coupled and typically nonlinear fashion:

1. **Global furnace heat transfer**: conduction in solid components (crucible, susceptor, insulation, heaters, crystal, pull rod), radiative exchange across cavities with non-trivial view factors (including through the optically semi-transparent crystal in some materials), and heater-power/temperature control.
2. **Melt hydrodynamics**: buoyancy-driven convection, forced convection from crucible and crystal rotation, and Marangoni (thermocapillary) convection at the free melt surface — often transitional/turbulent at industrial scale (Grashof/Reynolds/Marangoni numbers span many orders of magnitude across the process).
3. **Melt/crystal interface tracking**: a moving, deformable, non-planar solid–liquid phase boundary (Stefan problem) whose shape is dictated by the local heat balance and which must be solved self-consistently with the flow and thermal fields — this is the crux of CZ modeling and the single largest development gap versus dedicated tools.
4. **Free melt surface (meniscus)**: capillary-controlled surface shape linking crystal diameter to pull conditions, coupled to Marangoni stress and radiative/convective heat loss.
5. **Dopant/impurity transport and segregation**: solute transport in the melt, interfacial segregation (effective segregation coefficient, often via a boundary-layer or Burton–Prim–Slichter type closure), and micro/macro-segregation striae relevant to resistivity uniformity.
6. **Electromagnetic effects** (for MCZ/EMCZ): Lorentz-force damping of melt turbulence from static or cusp magnetic fields, or induction heating from RF coils — requiring a magnetohydrodynamic (MHD) or full Maxwell-equation coupling.
7. **Crystal-scale thermal stress and defect formation**: thermoelastic stress in the growing crystal (relevant to dislocation generation, especially in GaAs) and, in advanced use cases, point-defect (vacancy/interstitial) transport models (Voronkov theory) for grown-in defect prediction.
8. **Free-boundary/moving-mesh kinematics**: the crystal pulls upward and rotates, the melt level drops as material is consumed, and the crucible may translate to maintain melt-level position relative to the heaters — all of which require an ALE (Arbitrary Lagrangian–Eulerian) or equivalent moving-mesh formulation, not a fixed-mesh CFD assumption.

A tool intended for industrial-grade CZ simulation must, at minimum, close the loop between (1)–(4) self-consistently; (5)–(8) are increasingly expected in state-of-the-art academic and industrial practice.

### 1.2 Tools Under Evaluation

- **NEPTUNE_CFD**: a 3-D multifield (Euler–Euler two-phase) CFD solver, jointly developed by EDF, CEA, Framatome (formerly AREVA), and IRSN (formerly ASNR) under the NEPTUNE nuclear thermal-hydraulics platform. Built on the code_saturne numerical kernel (finite-volume, co-located, unstructured/hybrid mesh, pressure-correction algorithm) and sharing its GUI, so that a single interface can switch between code_saturne and NEPTUNE_CFD case setups.
- **SYRTHES**: EDF's conduction/radiation solver, typically deployed in conjugate-heat-transfer coupling with code_saturne (or, less commonly, NEPTUNE_CFD) via the SALOME platform's coupling infrastructure (historically the internal PLE/FVM coupling library, now largely superseded by CWIPI for code-to-code exchange).
- **CrysMAS** (reference comparator): Fraunhofer IISB's dedicated crystal-growth simulator, purpose-built for CZ, VGF, and related bulk growth methods, with an integrated global-furnace model, ALE interface tracking, electromagnetics, and segregation modules.

This report addresses NEPTUNE_CFD+SYRTHES specifically (as opposed to code_saturne+SYRTHES, which is the subject of a separate, closely related evaluation in this reference series). Where NEPTUNE_CFD's multifield architecture materially changes the analysis relative to code_saturne, this is flagged explicitly.

---

## 2. NEPTUNE_CFD: Architecture and Relevance to CZ Melt Flow

### 2.1 What NEPTUNE_CFD Actually Is

NEPTUNE_CFD's defining feature is its **Eulerian multifield (multifluid) formulation**: separate transport equations for mass, momentum, energy, and turbulence quantities are solved for each of several phases/fields (e.g., liquid, vapor, dispersed droplets/bubbles), coupled through interfacial transfer terms (drag, heat and mass transfer at interfaces, condensation/evaporation). Its physical model library — wall vapor condensation, spray modelling, boiling-crisis (departure from nucleate boiling, DNB) closures, cavitation, dispersed bubbly/droplet flow closures — is aimed squarely at pressurized-water-reactor (PWR) and boiling-water-reactor (BWR) safety analysis: hydrogen risk, boiling crisis, pressurized thermal shock (PTS), sub-channel void-fraction prediction, and similar. It has been validated against large experimental databases (OECD/NRC PSBT, BFBT) that are specific to nuclear fuel-assembly two-phase flow, and its verification/validation record has essentially no overlap with the melt-convection or free-surface phenomenology relevant to crystal growth.

NEPTUNE_CFD does support a genuine **single-phase mode** (validated, for example, against single-phase natural-convection benchmarks with imposed temperature/heat flux on flat plates across laminar-to-turbulent Rayleigh-number ranges), and in that mode it inherits code_saturne's general-purpose incompressible/weakly-compressible Navier–Stokes solver, RANS and LES turbulence closures, and scalar-transport capability. This is the only mode in which NEPTUNE_CFD is even nominally applicable to CZ melt convection, since the CZ melt pool is a single-phase liquid domain (silicon or compound-semiconductor melt) with, at most, a free surface to an inert cover gas rather than a genuine dispersed or separated two-phase flow of the kind NEPTUNE_CFD's models target.

### 2.2 Why the Multifield Architecture Is a Poor Fit

Three considerations argue against choosing NEPTUNE_CFD over its own parent code, code_saturne, for CZ melt modeling:

1. **No physics is gained.** CZ melt convection is a single-phase buoyancy/rotation/Marangoni-driven flow problem. None of NEPTUNE_CFD's differentiating capabilities (interfacial drag laws, boiling closures, bifluid turbulence models, condensation/cavitation) apply. Running NEPTUNE_CFD in single-phase mode uses exactly the code_saturne kernel underneath, so no unique modeling capability is obtained by choosing NEPTUNE_CFD over code_saturne directly.
2. **Overhead and complexity are added.** The multifield solver architecture, input structure, and GUI options carry the conceptual and computational overhead of a general two-phase framework (field definitions, interfacial exchange term bookkeeping) even when degenerated to one phase. This complicates case setup, increases the surface area for configuration errors, and adds maintenance burden for user-developed extensions (see §2.4) that must track a more complex code structure.
3. **Free-surface / Marangoni relevance is coincidental, not designed-in.** One might hope that NEPTUNE_CFD's interfacial-transfer machinery (built for gas–liquid interfaces in reactor contexts) could be repurposed to represent the CZ melt free surface and its Marangoni stress. In practice this is not how CZ free-surface/meniscus modeling is done even in dedicated codes — the meniscus is normally treated as a prescribed or ALE-tracked capillary boundary, not as a resolved two-phase gas–liquid interface with interpenetrating-continua closures designed for bubbly flows. Attempting to shoehorn NEPTUNE_CFD's two-phase interface models onto the CZ meniscus would be a research project in itself, with no guarantee of a physically appropriate result, and no published precedent to build from.

The practical conclusion is that **NEPTUNE_CFD offers no capability for CZ melt-flow modeling beyond what code_saturne already offers**, while adding architectural complexity that works against custom-development efforts. Any serious effort to build a CZ capability on the EDF code_saturne/SYRTHES family should be based on code_saturne directly, not NEPTUNE_CFD, unless the specific research question genuinely requires resolving dispersed gas bubbles or a true two-phase melt/cover-gas interaction (see §6.3).

### 2.3 Turbulence, Buoyancy, and Rotation in Single-Phase Mode

In its single-phase mode, NEPTUNE_CFD/code_saturne offers:
- RANS closures (k–ε, k–ω SST, Reynolds-stress models) with buoyancy production terms, applicable to the transitional/turbulent melt convection regimes seen in industrial-scale CZ (melt Grashof numbers commonly exceed 10⁹).
- LES capability, of interest for research-grade resolution of oscillatory/turbulent CZ melt convection and its coupling to striations, though at a computational cost that is generally prohibitive for routine industrial process design given the long (hours-to-days) physical timescales of a CZ pull.
- Rotating reference frame / moving reference frame handling adequate for representing crucible and crystal rotation in idealized, non-deforming-mesh contexts, but not a native rotating-crystal-with-shrinking-melt-domain ALE capability (see §2.5).

These are useful, general-purpose CFD building blocks, but they are no different from — indeed identical in origin to — what is already available in code_saturne, and none of them addresses the phase-change interface, free-surface, segregation, or electromagnetic modeling gaps that dominate CZ-specific development effort.

### 2.4 Radiative Heat Transfer Within NEPTUNE_CFD/code_saturne

code_saturne (and by inheritance NEPTUNE_CFD) includes a semi-transparent-medium radiative transfer module (P-1 or discrete-ordinates type approaches) intended primarily for combustion applications (participating gases, soot radiation). This is **not** a view-factor/surface-to-surface radiative enclosure solver of the kind needed for a CZ furnace, where the dominant radiative exchange is between opaque or semi-transparent solid surfaces (heaters, crucible, crystal, insulation, chamber walls) with strongly non-convex, occluding geometry and, in some materials (sapphire, some oxides), volumetric semi-transparency of the crystal itself. Furnace-scale, multi-surface, occlusion-aware radiative enclosure calculations are exactly the kind of capability that SYRTHES is meant to supply (§3), not NEPTUNE_CFD.

### 2.5 Mesh Motion and the Interface-Tracking Gap

Neither NEPTUNE_CFD nor code_saturne possesses a native, general free/deformable phase-interface tracking capability of the kind CZ growth requires. code_saturne does provide an ALE (Arbitrary Lagrangian–Eulerian) capability for boundary-driven mesh deformation (used, for example, in fluid–structure interaction and free-surface problems in its usual application domains), which is a necessary building block, but no ready-made Stefan-problem (solid–liquid phase-change front tracking with latent-heat balance) implementation exists. This must be custom-built: a user-level implementation that (a) computes the local interface velocity from the Stefan condition using conductive fluxes on each side of the interface (and any additional terms, e.g. from radiative absorption at a semi-transparent interface), (b) moves interface mesh nodes accordingly, (c) re-generates or re-deforms the volume mesh in the melt and crystal domains at every time step or pseudo-time iteration, and (d) iterates this coupled to the flow, thermal, and (if present) segregation solutions until a converged, self-consistent interface shape and pull rate are obtained. This is a substantial, well-understood but nontrivial computational-geometry and multiphysics-coupling task — CrysMAS, CGSim, FEMAG-CZ and other dedicated tools all have mature, internally validated implementations of exactly this; NEPTUNE_CFD/code_saturne have none.

### 2.6 Electromagnetics

NEPTUNE_CFD/code_saturne have no native magnetohydrodynamic (MHD, Lorentz-force-coupled Navier–Stokes) or induction-heating (eddy-current/RF) solver. code_saturne does support user-defined source terms that could, in principle, be populated with an externally computed Lorentz-force field (e.g., from a separately solved reduced Maxwell-equation problem, possibly via a coupled tool or a simplified analytical/axisymmetric induction model), but there is no built-in electromagnetic field solver, and none is inherited by using NEPTUNE_CFD instead. For magnetic-field-assisted CZ (MCZ, EMCZ) or RF-induction-heated furnaces (common for compound semiconductors and for some silicon growth configurations), this is a hard capability gap requiring either external EM-solver coupling (e.g., a general-purpose FEM electromagnetics code) or a from-scratch in-house implementation.

---

## 3. SYRTHES: Capabilities and Fit for the Furnace Thermal Problem

SYRTHES is architecturally well-suited to *part* of the CZ problem — the furnace-scale conduction and radiation half — independent of which flow solver it is paired with.

### 3.1 Conduction

SYRTHES solves transient or steady heat conduction in solid domains via finite elements (or, in some configurations, finite volumes), on unstructured 3-D (or axisymmetric 2-D) meshes, with temperature-dependent material properties, internal heat sources, and standard boundary condition types (fixed temperature, fixed flux, convective/Robin conditions, and radiative conditions). This maps directly onto the CZ furnace's solid components: crucible, susceptor, afterheater, insulation packs, heaters (as prescribed or coupled heat sources), pull rod/seed holder, chamber walls, and the growing crystal itself (as a conducting solid once past the interface-tracking machinery described in §2.5).

### 3.2 Radiative Enclosure Modeling

SYRTHES's radiative transfer capability is based on surface-to-surface (view-factor) radiative exchange among a set of opaque, diffuse-grey (or, with more setup effort, spectrally-banded/directional) surfaces — this is architecturally the right category of solver for a CZ furnace's radiative environment (multiple heaters, crucible, crystal shoulder, insulation, chamber). This is a substantive advantage over NEPTUNE_CFD/code_saturne's participating-media radiation module, which targets a different physical regime (semi-transparent gas/soot mixtures) entirely irrelevant to furnace enclosure radiation.

Two caveats apply, however, relative to what dedicated crystal-growth codes provide out of the box:
- **View-factor computation with moving/shrinking geometry.** As the crystal grows and the melt level drops, the furnace's radiative enclosure geometry changes continuously. SYRTHES computes view factors for a given mesh/geometry; re-computing them as the geometry evolves during a transient pull simulation requires either re-meshing and re-computing view factors at intervals (computationally expensive, and requiring custom orchestration script/workflow) or accepting a quasi-steady, frozen-geometry approximation for each pseudo-time step of a pulling sequence — a modeling simplification that dedicated CZ tools handle more gracefully via built-in moving-boundary/re-meshing logic tied directly to the growth kinematics.
- **Semi-transparency of the crystal.** For materials where the crystal itself is optically semi-transparent to thermal radiation at growth temperatures (sapphire, some oxide and fluoride crystals; less critical for silicon, which is largely opaque in the relevant infrared band at typical wafer thicknesses but can matter for large-diameter or specific dopant conditions), an opaque-surface view-factor treatment is inadequate and a volumetric radiative transport model (e.g., discrete ordinates or P-N approximation within the crystal) is needed. This is not SYRTHES's standard mode of operation and would require additional, non-trivial extension or coupling to a different radiation solver for such materials.

### 3.3 Conjugate Coupling Mechanics

SYRTHES is designed from the outset to couple to a companion CFD solver (conventionally code_saturne, but the same SALOME-based coupling infrastructure — historically PLE/FVM-based, more recently CWIPI — extends to NEPTUNE_CFD) for conjugate heat transfer: SYRTHES solves the solid conduction/radiation problem, the CFD code solves the fluid-side convection problem, and the two exchange wall temperatures/heat fluxes at the fluid–solid interface at each coupling time step. This coupling pattern is mature, validated in nuclear thermal-hydraulics contexts (e.g., core barrel, vessel, and structure conjugate heat transfer in reactor safety studies), and directly reusable for a CZ furnace's solid-structure/melt conjugate problem — **provided** the melt-side flow solver used is the one actually carrying the buoyancy/Marangoni/rotation physics, i.e. code_saturne (or NEPTUNE_CFD in single-phase mode, which, per §2.2, buys nothing extra).

### 3.4 What SYRTHES Does Not Provide

SYRTHES has no dopant transport, no segregation model, no phase-change/interface-tracking logic of its own (it is a fixed-domain conduction solver; the moving solid–liquid boundary must be managed by the orchestrating workflow, as discussed in §2.5), no electromagnetics, and no stress/defect modeling. It is exactly and only a conduction+radiation solver, which is an appropriate and reusable building block for one part of the CZ problem, not a crystal-growth code in its own right.

---

## 4. Coupled NEPTUNE_CFD+SYRTHES System: What Would Have to Be Built

Table 1 inventories the physics required for industrial-grade CZ simulation and states, for each, whether NEPTUNE_CFD+SYRTHES (as a coupled pair) provides native support, partial/adaptable support, or requires ground-up custom development.

**Table 1 — Physics Coverage Gap Analysis**

| Physical Phenomenon | NEPTUNE_CFD+SYRTHES Native Support | Effort Required |
|---|---|---|
| Melt buoyant/turbulent convection | Partial (via NEPTUNE_CFD's inherited code_saturne single-phase RANS/LES; the two-phase machinery is unused overhead) | Low–Medium: validate turbulence closures for CZ Grashof/Rayleigh range; confirm single-phase-mode performance parity with plain code_saturne |
| Crucible/crystal rotation-driven flow | Partial (rotating reference frame in single-phase mode) | Medium: implement/validate for CZ-relevant Reynolds/rotation numbers; reconcile with mesh deformation from interface tracking |
| Marangoni (thermocapillary) convection | None | High: custom free-surface stress boundary condition, coupled to local surface temperature gradient |
| Furnace solid conduction | Yes (SYRTHES) | Low: standard SYRTHES setup |
| Furnace surface-to-surface radiation (opaque) | Yes (SYRTHES) | Low–Medium: setup and validation for CZ furnace geometry; workflow for view-factor updates under moving/shrinking geometry |
| Semi-transparent crystal radiation | None | High: volumetric radiation model extension or external coupling |
| Melt/crystal phase-change interface (Stefan problem) | None | Very High: ALE interface-tracking, latent-heat balance, mesh regeneration, coupling to flow+thermal+radiation solution |
| Free melt surface (meniscus) shape | None | High: capillary boundary model coupled to pull/diameter control logic |
| Crystal pulling/rotation kinematics + diameter control | None | High: process-control logic (PID-type diameter control from meniscus angle or weighing-signal proxy) layered on top of the interface-tracking module |
| Dopant transport and segregation | None (scalar transport exists generically in code_saturne/NEPTUNE_CFD, but no interfacial segregation closure) | Medium–High: implement Burton–Prim–Slichter or boundary-layer segregation model at the tracked interface |
| Electromagnetics (MCZ/EMCZ, RF induction) | None | Very High: external EM solver coupling or from-scratch Maxwell/induction implementation |
| Crystal thermoelastic stress | None (would require coupling to a structural solver such as Code_Aster) | High: additional code coupling (Code_Aster is the natural EDF-family partner) plus constitutive/defect-criterion development |
| Point-defect (vacancy/interstitial) transport | None | Very High: novel model development, largely research-grade even in dedicated tools |
| Global furnace/melt coupled iteration to steady growth state | None as an integrated workflow (each piece exists as a separate code) | High: orchestration layer (scripting, likely Python via SALOME/YACS or custom drivers) to iterate NEPTUNE_CFD/code_saturne, SYRTHES, and any bolt-on interface/EM/segregation modules to a self-consistent solution at each pulling step |

### 4.1 Estimate of Overall Development Effort

Cross-referencing against the equivalent gap analyses performed for other general-purpose CFD/multiphysics frameworks in this reference series (Nek5000/NekRS, Kratos, Albany, DUNE, MFEM, deal.II, libMesh/MOOSE, and the closely related code_saturne+Code_Aster+SYRTHES combination), the NEPTUNE_CFD+SYRTHES gap profile is **essentially identical to the code_saturne+SYRTHES case** for every genuinely CZ-specific item (interface tracking, Marangoni, segregation, electromagnetics, meniscus/diameter control), since none of those capabilities exist in either code family and all would need the same custom development regardless of which EDF flow solver anchors the melt-side physics. The only material difference is that choosing NEPTUNE_CFD instead of code_saturne **adds** the overhead of the multifield architecture (§2.2) without removing any of the required custom-development items. A defensible order-of-magnitude estimate, consistent with the parallel evaluations in this series:

- **Minimum viable single-crystal-orientation, single-geometry demonstrator** (fixed idealized interface shape, no segregation, no EM, radiative enclosure via SYRTHES, melt convection via NEPTUNE_CFD single-phase mode or — preferably — plain code_saturne): **12–24 person-months** for a team with existing SALOME/code_saturne/SYRTHES coupling expertise.
- **Genuinely predictive CZ capability** (ALE interface tracking with Stefan condition, meniscus/diameter control, dopant segregation, validated against at least one experimental or CrysMAS/CGSim benchmark case): **3–6 person-years**, contingent on nontrivial numerical-methods research risk (interface-tracking robustness, mesh regeneration quality, coupled-solver convergence) rather than pure engineering effort.
- **Feature parity with CrysMAS** (adding electromagnetics for MCZ/EMCZ, thermoelastic stress via Code_Aster coupling, and a mature, GUI-driven, production workflow): **multiple additional person-years**, and even then the result would be a bespoke, single-institution research code rather than a broadly validated, supported product — CrysMAS's decades of accumulated validation and process-engineering knowledge are not something that can be purchased with development time alone.

This estimate assumes the custom development targets code_saturne (not NEPTUNE_CFD) as the flow-solver anchor; using NEPTUNE_CFD proper would add integration and maintenance overhead without offsetting benefit, effectively lengthening these timelines rather than shortening them.

---

## 5. Detailed Comparison with CrysMAS

**Table 2 — Head-to-Head Comparison**

| Dimension | NEPTUNE_CFD + SYRTHES | CrysMAS |
|---|---|---|
| **Primary design intent** | Nuclear reactor two-phase thermal-hydraulics (NEPTUNE_CFD) + general conduction/radiation (SYRTHES) | Purpose-built bulk crystal growth (CZ, VGF, Bridgman, related methods) |
| **Melt convection physics** | General-purpose single-phase RANS/LES (via inherited code_saturne kernel); two-phase machinery irrelevant and adds overhead | Buoyancy, forced (rotation), and Marangoni convection natively integrated into the global furnace model, validated against decades of CZ-specific experiments |
| **Interface (Stefan problem) tracking** | Not implemented; would require full custom ALE development | Native, mature ALE-based sharp-interface tracking, core to the tool's design |
| **Free melt surface/meniscus** | Not implemented | Native meniscus/capillary model tied to diameter control |
| **Furnace radiative enclosure** | Native via SYRTHES (opaque, diffuse-grey view-factor method); semi-transparent crystal radiation not supported without extension | Native, including (in relevant material cases) treatment of semi-transparent radiative transport in the crystal |
| **Electromagnetics (MCZ/EMCZ, RF induction)** | Not implemented; external coupling or from-scratch development required | Native EM/induction-heating and Lorentz-force coupling |
| **Dopant transport/segregation** | Generic scalar transport exists; no interfacial segregation closure | Native segregation models (e.g., effective segregation coefficient formulations) integrated with the tracked interface |
| **Crystal thermoelastic stress/defects** | Not implemented; would require coupling to a separate structural solver (e.g., Code_Aster) | Native or closely integrated stress and (in advanced configurations) point-defect modeling |
| **Numerical method** | Finite volume, unstructured/hybrid 3-D mesh (NEPTUNE_CFD/code_saturne); FE/FV conduction+radiation (SYRTHES) | Predominantly axisymmetric (2-D) finite-element/finite-volume global model, reflecting the strong axisymmetry of most industrial CZ furnaces; 3-D extensions exist for specific non-axisymmetric effects but are not the default mode |
| **Validation status for CZ** | None — zero published CZ validation cases for this specific toolchain | Extensive — validated against silicon, GaAs, and oxide/other CZ growth experiments over multiple decades, used in industrial process design |
| **Industrial readiness** | Not industrially deployed for crystal growth in any known capacity | Industrially deployed; used by crystal-growth manufacturers and research institutes worldwide |
| **Scalability** | Strong MPI-parallel scalability for large 3-D meshes (nuclear thermal-hydraulics use cases routinely run on large HPC clusters) | Adequate for its axisymmetric or modestly-3-D global model scale; not designed for, nor does it need, large-scale HPC parallelism given the reduced dimensionality of its primary model |
| **Extensibility** | Open, user-function-based extensibility (C/Fortran user subroutines in code_saturne/NEPTUNE_CFD; user routines in SYRTHES), full source access for research groups with a license/access agreement | Extensibility is comparatively limited and mediated through Fraunhofer IISB; not intended as an open research platform for arbitrary new physics, though it supports parameterized process/material configuration extensively |
| **Usability for crystal-growth engineers** | Low without substantial in-house CFD/multiphysics coupling expertise; requires comfort with general-purpose CFD case setup, SALOME coupling workflows, and (for any real CZ capability) custom code development | High — GUI and workflow are built around crystal-growth process parameters (pull rate, rotation rates, heater power, crucible/gas geometry) familiar to process engineers, not general CFD practitioners |
| **Licensing/access model** | EDF open-source-adjacent distribution (code_saturne is GPL-licensed; NEPTUNE_CFD access terms are more restrictive as part of the NEPTUNE consortium) | Commercial/institutional licensing via Fraunhofer IISB |
| **Community and support** | Active EDF-maintained user/developer community for nuclear thermal-hydraulics; essentially no crystal-growth user community or support channel | Dedicated support from Fraunhofer IISB, embedded in a research group with deep crystal-growth domain expertise |

### 5.1 Where NEPTUNE_CFD+SYRTHES Could, in Principle, Exceed CrysMAS

Two areas favor the EDF toolchain, conditional on the very substantial development investment of §4 being made:

- **True 3-D, fully turbulent (LES-resolved) melt convection at industrial Grashof numbers**, where CrysMAS's axisymmetric default formulation cannot capture genuinely 3-D, non-axisymmetric flow instabilities (e.g., certain Kelvin–Helmholtz or baroclinic instabilities in the melt, off-axis thermal plumes, or asymmetric striation patterns) that some research questions specifically target. NEPTUNE_CFD/code_saturne's mature 3-D unstructured-mesh, MPI-parallel, RANS/LES infrastructure is well-suited to this class of problem in principle, if the interface-tracking and coupling gaps were closed.
- **Large-scale HPC parallelism** for very fine 3-D meshes, where CrysMAS's design does not target (and does not need to target) large distributed-memory clusters given its reduced-dimensionality default model.

Neither advantage is available today without the multi-year development program described above, and both could equally (indeed more efficiently) be realized by building on code_saturne directly rather than NEPTUNE_CFD, since NEPTUNE_CFD's differentiating machinery contributes nothing to either strength.

---

## 6. Practical Implementation Challenges

### 6.1 Toolchain and Coupling Complexity

A working NEPTUNE_CFD+SYRTHES CZ simulation, even at the "minimum viable demonstrator" level, requires operating SALOME (or an equivalent coupling orchestration layer), managing mesh generation and mesh-matching across the melt (NEPTUNE_CFD) and solid (SYRTHES) domains, configuring the CHT coupling time-stepping and interpolation, and — since neither code natively tracks the moving interface — externally orchestrating mesh deformation/regeneration at each pseudo-time step of the growth sequence. This is a materially more complex workflow than a dedicated tool's single, integrated project file and solve button.

### 6.2 Verification and Validation Burden

Any custom-developed interface-tracking, Marangoni, segregation, or electromagnetic module would need independent verification (method-of-manufactured-solutions or analytical benchmark comparison) and validation against experimental or trusted-code (CrysMAS/CGSim/FEMAG-CZ) reference cases before any confidence could be placed in production use. This V&V burden is substantial and is *in addition to* the raw development effort estimated in §4.1 — a common failure mode in general-purpose-code-to-domain-specific adaptation projects is underestimating V&V relative to implementation effort.

### 6.3 Where Genuine NEPTUNE_CFD Two-Phase Capability Could Matter

A narrow, legitimate niche exists in which NEPTUNE_CFD's actual multifield strength (as opposed to its single-phase mode, which offers nothing code_saturne lacks) is relevant to CZ growth research: modeling **cover-gas (argon) flow with entrained bubbles, or gas–melt interaction phenomena at the free surface**, such as bubble incorporation defects, argon flow pattern effects on oxygen/dopant transport near the melt surface, or particulate transport in the gas phase above the melt. If a research program specifically requires resolving dispersed-phase gas–melt or gas-particulate interaction in the furnace atmosphere (as opposed to the melt-side single-phase convection problem), NEPTUNE_CFD's genuine two-phase closures (validated primarily in a different physical regime, so still requiring adaptation and validation) become a more defensible choice than code_saturne. This is a specialized research question, not a substitute for industrial CZ process simulation, and does not change the overall unsuitability conclusion for whole-process CZ modeling.

### 6.4 Human Capital and Institutional Fit

Effective use of this toolchain presumes staff with combined expertise in nuclear-thermal-hydraulics-style CFD (NEPTUNE_CFD/code_saturne), finite-element conduction/radiation (SYRTHES), SALOME-based code coupling, and crystal-growth physics — a combination more commonly found at EDF/CEA-affiliated institutions or their close academic collaborators than in typical semiconductor-industry or crystal-growth-research groups. Organizations already invested in the EDF code ecosystem (e.g., for other multiphysics work) face a materially lower marginal cost of entry than those starting from zero.

---

## 7. Recommendations

### 7.1 For Industrial CZ Process Engineering

**Use CrysMAS** (or a comparable dedicated tool such as CGSim or FEMAG-CZ). No credible case exists for NEPTUNE_CFD+SYRTHES as an industrial CZ design tool today or within a normal product-development timeframe; the gap-closing investment (§4.1) would produce, at best, a research-grade internal capability lagging CrysMAS's validated feature set and decades of process-engineering knowledge, at a cost far exceeding CrysMAS licensing.

### 7.2 For Academic/Research Use

- If the research question is fundamentally about **CZ-specific phenomena** (interface morphology, Marangoni-driven instabilities, segregation, striations, MCZ/EMCZ electromagnetics), a dedicated tool (CrysMAS, CGSim, FEMAG-CZ) or a general-purpose framework already evaluated in this reference series with stronger native ALE/interface-tracking or multiphysics capability (e.g., Nek5000/NekRS for high-fidelity turbulent melt convection with custom interface coupling, or a finite-element multiphysics framework like MOOSE/libMesh or Code_Aster-coupled workflows for the structural/segregation side) is likely to be a more productive starting point than NEPTUNE_CFD+SYRTHES.
- If the research question specifically concerns **furnace-scale conjugate heat transfer and radiative enclosure behavior in isolation** (e.g., heater design optimization, insulation studies, or thermal-field sensitivity studies that do not require a self-consistent melt interface), **SYRTHES coupled to plain code_saturne** (not NEPTUNE_CFD) is a defensible, already-capable-enough choice, since this sub-problem does not require interface tracking, segregation, or electromagnetics — it is a conjugate heat transfer and radiation problem SYRTHES/code_saturne genuinely solve well.
- If the research question specifically concerns **two-phase gas–melt or bubble/particulate phenomena** in the furnace atmosphere or at the melt free surface (§6.3), NEPTUNE_CFD's native multifield capability is uniquely relevant among the EDF-family codes and may justify its added complexity over code_saturne.
- In all other CZ-modeling research contexts, **prefer code_saturne over NEPTUNE_CFD** as the flow-solver anchor: it provides identical single-phase capability with less architectural overhead, is more widely used and documented outside the nuclear domain, and avoids maintenance burden tied to NEPTUNE_CFD's more restrictive access/consortium terms.

### 7.3 For Institutions Already Invested in the EDF/SALOME Ecosystem

If an organization already operates SYRTHES/code_saturne (or NEPTUNE_CFD) for other multiphysics work (e.g., nuclear, industrial thermal-hydraulics) and wishes to explore crystal growth as an adjacent capability, a staged approach is reasonable: (1) build and validate the conjugate heat transfer/radiative enclosure sub-model first (code_saturne+SYRTHES, low-risk, high reuse of existing expertise), (2) treat the melt/crystal interface as fixed or externally prescribed (e.g., imported from a CrysMAS or CGSim run) to validate the thermal-field and convection sub-models against a trusted reference before attempting self-consistent interface tracking, and (3) only then commit to the multi-year investment in native interface-tracking, segregation, and (if needed) electromagnetics — treating this as a genuine, risk-managed R&D program rather than a tool-adoption exercise. In this staged path, there remains no reason to route the melt-convection sub-model through NEPTUNE_CFD rather than code_saturne unless the two-phase niche of §6.3 is specifically in scope.

### 7.4 General Guidance

Treat "can this general-purpose code, in principle, represent the physics" as a necessary but far from sufficient condition. The determining factors for CZ simulation suitability are: (a) native or near-native interface-tracking and free-surface capability, (b) accumulated validation specific to crystal growth, and (c) a workflow usable by process/crystal-growth engineers rather than only by CFD specialists. CrysMAS satisfies all three; NEPTUNE_CFD+SYRTHES satisfies none without substantial custom investment, and even then only partially.

---

## 8. Key References

1. Guelfi, A., et al. (2007). "NEPTUNE: A New Software Platform for Advanced Nuclear Thermal Hydraulics." *Nuclear Science and Engineering*, 156(3), 281–324.
2. Mimouni, S., et al. (2017). "Dispersed Two-Phase Flow Modelling for Nuclear Safety in the NEPTUNE_CFD Code." *Science and Technology of Nuclear Installations*, 2017, Article 3238545.
3. Validation of NEPTUNE_CFD Two-Phase Flow Models Using the OECD/NRC BFBT Benchmark Database (includes coupled NEPTUNE_CFD–SYRTHES conjugate heat transfer application to heater-rod thermal modeling).
4. Validation of NEPTUNE_CFD two-phase flow models against OECD/NRC PSBT subchannel experiments. *Nuclear Engineering and Design* (ScienceDirect).
5. Validation of NEPTUNE_CFD for single-phase natural convection. *Nuclear Engineering and Design* (ScienceDirect, 2025) — the primary published evidence for NEPTUNE_CFD's single-phase buoyancy-driven flow capability, relevant to assessing its melt-convection applicability.
6. EDF R&D. code_saturne documentation and source (https://www.code-saturne.org / GitHub: code-saturne/code_saturne) — the shared numerical kernel underlying NEPTUNE_CFD.
7. EDF R&D. SYRTHES documentation (distributed alongside code_saturne; EDF R&D publications on conjugate heat transfer and radiative enclosure coupling methodology).
8. Fraunhofer IISB. CrysMAS software documentation and publication list (https://www.iisb.fraunhofer.de) — including validation studies against silicon and compound-semiconductor CZ growth experiments.
9. Companion evaluation in this reference series: "Code_Saturne, Code_Aster, and SYRTHES (EDF codes, coupled via SALOME/MED) against CrysMAS for Czochralski Crystal Growth Simulation" — the closely related assessment of the pure code_saturne-anchored EDF toolchain, whose physics-gap analysis (Table 1 of that report) is directly applicable to NEPTUNE_CFD's single-phase mode.
10. Derby, J.J., and Brown, R.A., and successors (Minnesota group); Dupret, F. (UCLouvain); Müller, G. and Friedrich, J. (Fraunhofer IISB) — foundational and ongoing literature on global furnace modeling, ALE interface tracking, and Marangoni/buoyancy convection in CZ growth, forming the physical-modeling baseline against which any EDF-toolchain custom development would need to be validated.

---

*This report is part of a systematic comparative series evaluating general-purpose CFD, finite-element, and multiphysics simulation frameworks against CrysMAS for Czochralski crystal growth simulation.*

---

> [!NOTE]
> 
> Generated by Claude.ai
>
> Model: Sonet 5
>
> Prompt: Write a comprehensive, technically rigorous report evaluating the suitability of NEPTUNE_CFD and SYRTHES together for high-fidelity numerical simulation of the Czochralski (CZ) crystal growth process. The report should critically assess NEPTUNE_CFD and SYRTHES's capabilities, limitations, required extensions, and practical implementation challenges. It should also provide a detailed comparison with CrysMAS, the dedicated crystal-growth simulation software developed by the Fraunhofer Institute for Integrated Systems and Device Technology (Fraunhofer IISB). The report should be written for researchers and engineers involved in semiconductor crystal growth, computational fluid dynamics (CFD), heat transfer, and multiphysics simulation.
> Objectives
> Determine whether NEPTUNE_CFD and SYRTHES can serve as a viable platform for industrial-grade CZ crystal growth simulation.
> Identify which physical phenomena can be modeled using standard NEPTUNE_CFD and SYRTHES capabilities and which require custom development.
> Compare NEPTUNE_CFD and SYRTHES with CrysMAS regarding physics coverage, numerical methods, validation status, industrial readiness, scalability, extensibility, and usability.
> Assess the effort required to build a CZ simulation environment in NEPTUNE_CFD and SYRTHES that approaches the capabilities of CrysMAS.
> Provide recommendations for research, academic, and industrial use cases.
> Provide key references. Show the output in Markdown format.
