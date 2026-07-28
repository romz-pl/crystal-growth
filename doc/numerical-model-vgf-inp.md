# Development Roadmap: A High-Fidelity, Physics-Based Numerical Model of InP VGF/VB Crystal Growth

## 0. Purpose and Scope

This roadmap defines the multi-year technical program required to build an industrial-grade simulation tool for indium phosphide (InP) single-crystal growth by Vertical Gradient Freeze (VGF) and Vertical Bridgman (VB). It spans physics model development, numerical methods, software architecture, materials-property data acquisition, validation against experiment, and deployment for industrial design-of-experiment (DoE) use. The organizing principle is a staged buildup: **1D/0D reduced models → 2D axisymmetric continuum model → 3D transient multiphysics model → coupled thermomechanical/defect model → industrial-scale, uncertainty-quantified digital twin.**

---

## 1. Scientific Foundations and Requirements Definition

### 1.1 Process Definition and Target Fidelity
- Define furnace configurations to be modeled: multi-zone resistive VGF furnaces, VB with translating gradient, ampoule/crucible geometries (pBN, quartz, graphite susceptors), seed configurations.
- Define InP-specific constraints: high dissociation pressure of phosphorus (~27.5 atm at melting point, T_m ≈ 1062 °C), need for encapsulation (B₂O₃ LEC-style liquid encapsulation is rare in VGF/VB but boron nitride crucibles and sealed ampoules with controlled overpressure dominate).
- Specify target predictive outputs: melt/solid interface shape and velocity, temperature and stress fields, dopant/impurity segregation profiles, dislocation density (EPD), twin formation risk, polycrystal nucleation risk, void/inclusion formation.
- Define fidelity tiers explicitly (steady 2D thermal → transient 2D with convection → full 3D transient multiphysics → stochastic defect-resolved) so that project milestones map to concrete deliverables rather than an undifferentiated "full model."

### 1.2 Literature and Prior-Art Survey (Continuous Task)
- Systematic review of VGF/VB modeling literature, phase-field and front-tracking interface methods, dislocation dynamics in III-V melts, and existing commercial/academic codes (CGSim, CrysMAS, FEMAG-CZ, Cats2D, STHAMAS-VB).
- InP-specific growth literature (LEC, VGF, VB) for property data and experimental validation targets.
- Maintain a living annotated bibliography and property database (see §3) as a first-class deliverable, version-controlled alongside code.

### 1.3 Governing Physics Inventory
Enumerate all physical phenomena that must eventually be represented, even if implemented incrementally:
1. Conductive/convective/radiative heat transfer in melt, crystal, crucible, insulation, and furnace.
2. Melt convection (buoyancy-driven, residual forced convection, Marangoni if free surface present).
3. Species (dopant, impurity, stoichiometric deviation) transport and segregation at the growth interface.
4. Phase change: enthalpy method or front-tracking, latent heat release, interface curvature and morphological stability.
5. Thermoelastic and thermoplastic stress in the growing crystal; dislocation generation via Alexander–Haasen or similar plasticity models.
6. Point-defect thermodynamics (In/P vacancies, antisites, EL2-type centers in GaAs by analogy) and non-stoichiometry effects on P partial pressure and crystal properties.
7. Ampoule/crucible mechanical interaction: crystal–wall gap formation, contact pressure, wetting behavior, thermal-stress-induced cracking.
8. Radiative heat exchange in semi-transparent InP melt/crystal (participating media at near-IR/visible wavelengths) and view-factor radiation in the furnace cavity.
9. Furnace-scale electromagnetic/resistive heating and heater–load thermal coupling (for realistic boundary conditions rather than prescribed profiles).
10. Optional: melt free-surface effects if a non-encapsulated meniscus exists at any stage; internal P-vapor/void formation from stoichiometric loss.

---

## 2. Governing Equations and Mathematical Model Formulation

### 2.1 Core Continuum Equations
Formulate the coupled PDE system to be solved in each subdomain (melt, solid crystal, crucible, gas gap, furnace):

**Mass and momentum (melt, incompressible Boussinesq or low-Mach):**

$$
\nabla \cdot \mathbf{u} = 0
$$

$$
\rho_0 \left( \frac{\partial \mathbf{u}}{\partial t} + \mathbf{u}\cdot\nabla \mathbf{u} \right) = -\nabla p + \mu \nabla^2 \mathbf{u} + \rho_0 \mathbf{g}\,\beta_T (T - T_{ref}) + \rho_0 \mathbf{g}\,\beta_C (C - C_{ref})
$$

**Energy (all domains, with phase change via enthalpy formulation):**

$$
\rho c_p \frac{\partial T}{\partial t} + \rho c_p\, \mathbf{u}\cdot \nabla T = \nabla\cdot(k \nabla T) + \dot{q}_{rad} + L\,\rho\,\frac{\partial f_s}{\partial t}
$$

where $f_s$ is solid fraction and $L$ latent heat of fusion.

**Species/solute transport (dopant or intrinsic stoichiometry deviation):**

$$
\frac{\partial C}{\partial t} + \mathbf{u}\cdot\nabla C = \nabla\cdot(D \nabla C)
$$

with interface segregation condition (Burton–Prim–Slichter or local equilibrium with effective distribution coefficient $k_{eff}$):

$$
k_{eff} = \frac{k_0}{k_0 + (1-k_0)\exp(-v_g \delta / D)}
$$

**Stefan interface condition at the solid–liquid front (position $\mathbf{x}_i(t)$, normal velocity $v_n$):**

$$
\rho L\, v_n = \Big( k_s \nabla T_s - k_l \nabla T_l \Big)\Big|_{\text{interface}}\cdot \mathbf{n}
$$

**Thermoelastic stress (quasi-static, small-strain):**

$$
\nabla \cdot \boldsymbol{\sigma} = 0, \qquad \boldsymbol{\sigma} = \mathbf{C} : \big(\boldsymbol{\varepsilon} - \boldsymbol{\varepsilon}^{th} - \boldsymbol{\varepsilon}^{pl}\big), \qquad \boldsymbol{\varepsilon}^{th} = \alpha(T)(T - T_{ref})\,\mathbf{I}
$$

**Dislocation density evolution (Alexander–Haasen–Kubin-type plasticity):**

$$
\frac{d N}{dt} = K_1 N \Big(\frac{\tau_{eff}}{\tau_0}\Big)^m \exp\!\left(-\frac{Q}{k_B T}\right), \qquad \tau_{eff} = \tau_{res} - K_2 \sqrt{N}
$$

**Radiative transfer (participating media, if semi-transparency retained):**

$$
\mu \frac{\partial I}{\partial s} = -(\kappa_a + \kappa_s) I + \kappa_a I_b(T) + \frac{\kappa_s}{4\pi}\int_{4\pi} I\, \Phi(\mathbf{\Omega}',\mathbf{\Omega})\, d\Omega'
$$

### 2.2 Dimensionless Groups and Regime Mapping
- Derive and tabulate the governing dimensionless numbers for the VGF/VB regime: Grashof ($Gr$), Prandtl ($Pr$), Rayleigh ($Ra$), Marangoni ($Ma$, where relevant), Peclet ($Pe$), Biot ($Bi$), Stefan ($Ste$), segregation Peclet ($v_g\delta/D$).
- Establish expected operating ranges for InP VGF/VB (low convection regime relative to Czochralski; Bridgman geometries suppress but do not eliminate buoyancy-driven flow) and identify which terms can be legitimately neglected at each fidelity tier, with explicit justification and sensitivity checks rather than assumption.

### 2.3 Boundary and Initial Conditions
- Furnace-wall temperature profiles (measured or modeled from heater power), radiative view-factor coupling to furnace insulation, ampoule contact resistance (temperature- and pressure-dependent, includes gap formation history), free surface conditions if applicable, symmetry/axisymmetry assumptions and their limits of validity.
- Formal statement of assumptions at each fidelity tier (e.g., axisymmetric vs. fully 3D; rigid vs. deformable crucible; local equilibrium segregation vs. full P-vacancy point-defect kinetics).

---

## 3. Materials Property Database (Critical-Path, Parallel Workstream)

InP-specific properties are the single largest source of predictive uncertainty and must be tracked as rigorously as the numerics.

| Property class | Required data | Notes / Risk |
|---|---|---|
| Thermophysical (melt) | $\rho$, $\mu$, $c_p$, $k$, $\beta_T$ vs. $T$ | Sparse high-temperature melt viscosity/conductivity data; large literature scatter |
| Thermophysical (solid) | $\rho$, $c_p$, $k(T)$ anisotropy (zinc-blende, effectively isotropic) | Better constrained than melt values |
| Phase equilibrium | $T_m$, liquidus/solidus for doped systems (S, Zn, Sn, Fe), P-vapor pressure vs. T | P dissociation pressure curve is central to ampoule design constraints |
| Segregation | Equilibrium distribution coefficients $k_0$ for relevant dopants; diffusivities $D$ in melt | Often extrapolated from GaAs analogs — flag as a validation risk |
| Mechanical/elastic | $\mathbf{C}_{ijkl}(T)$, thermal expansion $\alpha(T)$ | Reasonably well characterized for InP |
| Plasticity | Alexander–Haasen parameters ($K_1,K_2,m,Q,\tau_0$) for InP | **Major gap**: most CRSS/dislocation-mobility data is for Si, GaAs, InSb; InP-specific fits are scarce and must be partially inferred/calibrated |
| Radiative | Absorption coefficient $\kappa_a(\lambda,T)$, emissivity of melt/crystal/crucible surfaces | Semi-transparency of InP melt near band edge is nontrivial |
| Point defects | Native defect formation energies, In/P vacancy concentrations vs. stoichiometry and T | Needed only for advanced (Tier 4) point-defect/EPD models |
| Interfacial | Crucible/melt contact angle, wetting, interfacial energy pBN–InP | Governs gap formation and stress transfer to crystal |

**Tasks:**
- Build a version-controlled, unit-tested property database (temperature-dependent correlations with documented provenance and uncertainty bounds) rather than hardcoded constants.
- Explicitly flag properties requiring first-principles estimation (DFT) or bespoke experimental measurement campaigns (e.g., high-temperature viscometry, in-situ dislocation mobility) as a funded sub-task, not an assumption.
- Maintain a Bayesian/hierarchical uncertainty model for poorly constrained parameters (e.g., plasticity constants) to be tightened via inverse modeling in later phases (§8).

---

## 4. Numerical Methods Development

### 4.1 Discretization Strategy
- **Spatial discretization:** Finite element method (FEM) recommended for stress/geometry flexibility and mesh conformity to curved crucible/interface geometries; alternatively finite volume (FVM) for strict conservation in convection-dominated melt flow — evaluate hybrid FEM(solid mechanics)/FVM(fluid-thermal) coupling vs. unified FEM (e.g., via FEniCS/MFEM) for code maintainability.
- **Interface tracking:** deformable/moving mesh (ALE — Arbitrary Lagrangian-Eulerian) for sharp-interface tracking of the solid–liquid front, preferred for VGF/VB where the interface is not extremely convoluted; evaluate fixed-grid enthalpy/apparent-heat-capacity methods as a lower-fidelity fallback and phase-field methods for morphological instability studies (facet formation, interface breakdown).
- **Time integration:** implicit (backward Euler / BDF2) for the stiff thermal-diffusion-dominated system; adaptive time-stepping tied to interface velocity and Courant constraints in the melt.
- **Mesh management:** automated remeshing/mesh deformation as the interface migrates over the full ampoule length (large cumulative displacement — a major robustness challenge specific to VGF/VB vs. Czochralski/floating-zone).

### 4.2 Coupling Architecture
- Monolithic vs. partitioned (staggered) coupling between: melt flow–energy–species (tightly coupled), interface tracking (tightly coupled to energy), stress/plasticity (can be weakly/loosely coupled, solved on the frozen solid domain post- or intra-step), radiation (either full participating-media solve or precomputed view-factor matrix updated at coarser cadence).
- Define a formal coupling schedule (operator-splitting scheme) with documented order of accuracy and stability analysis — this is a common source of unphysical results in published VGF models and must be treated rigorously.

### 4.3 Solver and HPC Architecture
- Linear solvers: preconditioned Krylov methods (GMRES/BiCGStab) with algebraic multigrid preconditioning for the pressure-Poisson/energy systems; direct solvers for smaller 2D verification cases.
- Nonlinear solvers: Newton–Raphson with line search/trust region for the coupled nonlinear (temperature-dependent property, plasticity) system.
- Parallelization: domain decomposition (MPI) for 3D transient runs; given the team's prior experience with large-scale MPI FEM solvers (BlueGene-class scaling), architect the code from the outset for distributed-memory scalability rather than retrofitting parallelism later.
- Consider PETSc/Trilinos as the linear-algebra backend to avoid reinventing solver infrastructure; leverages existing scalable Newton-Krylov-Multigrid ecosystems.

### 4.4 Verification (Numerics-Focused, Distinct from Validation)
- Method of Manufactured Solutions (MMS) for each physics module independently (heat conduction with phase change, Boussinesq flow, linear thermoelasticity, species transport) to confirm formal order of accuracy before any physical validation is attempted.
- Mesh/time-step convergence studies (Richardson extrapolation) at each fidelity tier.
- Benchmark against published canonical test cases: differentially heated cavity (de Vahl Davis benchmark) for buoyancy convection, Stefan problem analytical solutions for phase change, standard thermoelasticity benchmarks (e.g., NAFEMS suite).

---

## 5. Staged Model Build-Out (Fidelity Ladder)

### Stage 1 — 1D/0D Reduced Models (Months 1–6)
- 1D axial heat conduction with moving phase boundary (quasi-steady Stefan problem) to establish thermal gradient/growth-rate relationships and furnace profile requirements.
- 0D segregation model (Scheil/BPS) for dopant incorporation trends.
- Purpose: sanity-check property data, establish baseline process windows, produce quick-turnaround engineering estimates while the full model is built.

### Stage 2 — 2D Axisymmetric Steady/Quasi-Steady Continuum Model (Months 4–14)
- Axisymmetric melt convection + conduction + radiation (view-factor) + moving interface (ALE) in a representative VGF/VB furnace geometry.
- Coupled segregation model with interface-tracked $k_{eff}$.
- Deliverable: interface shape vs. furnace translation rate/heater profile; first thermal-stress post-processing (uncoupled, using frozen temperature history).

### Stage 3 — 2D/3D Transient Multiphysics Model (Year 1–2.5)
- Full transient coupling of melt convection–energy–species–moving interface.
- Fully coupled thermoelastic stress solve with Alexander–Haasen plasticity for in-situ dislocation density evolution.
- 3D extension to capture non-axisymmetric effects: furnace asymmetry, gravity-driven 3D convection cells, crucible tilt, non-axisymmetric heater zones.
- Ampoule/crucible mechanical contact model: gap formation, contact-pressure-dependent thermal boundary resistance.

### Stage 4 — Defect-Resolved and Point-Defect-Coupled Model (Year 2–3.5)
- Point-defect thermodynamics coupling (In/P vacancy concentration fields, non-stoichiometry transport) feeding back into effective properties and dislocation nucleation.
- Twin-formation and polycrystal-nucleation risk criteria (interface undercooling/facet stability analysis).
- Void/inclusion formation from local stoichiometric deviation and P-vapor pocket modeling in partially sealed ampoules.

### Stage 5 — Industrial-Scale, Uncertainty-Quantified Digital Twin (Year 3–4+)
- Full furnace-scale 3D model including heater elements, insulation, and thermal inertia of real hardware (not idealized boundary conditions).
- Surrogate/reduced-order model (ROM) generation (POD, neural operator, or Gaussian-process-based) trained on the high-fidelity 3D solves to enable near-real-time DoE and furnace-recipe optimization.
- Uncertainty quantification (UQ) pipeline: forward UQ (polynomial chaos / Monte Carlo on uncertain material properties) and inverse UQ/parameter calibration against experimental data (Bayesian calibration, §8).
- Software hardening: automated regression test suite, containerized deployment, GUI/scripting API for process engineers, licensing/IP packaging if commercialized.

---

## 6. Software Architecture and Engineering Practices

- **Modular design:** independent, testable modules for mesh/geometry, material properties, each physics solver, coupling orchestration, and post-processing/visualization — enforce clean interfaces (e.g., via abstract solver base classes) to allow swapping discretization schemes (FEM/FVM) or solver backends (PETSc/Trilinos) without rewriting physics code.
- **Language/framework choice:** C++ core (leveraging existing HPC/MPI/FEM expertise) with Python bindings for scripting, pre/post-processing, and ROM/UQ workflows; consider building atop or interfacing with FEniCS/MFEM/deal.II for FEM infrastructure rather than writing a discretization framework from scratch, reserving custom development effort for the InP-specific physics (plasticity, segregation, radiative coupling) and performance-critical kernels.
- **Version control and CI/CD:** full test-driven development; continuous integration running the MMS/benchmark suite on every commit; nightly full-scale regression runs.
- **Documentation:** theory manual (equations, assumptions, discretization) maintained in lockstep with code — critical for scientific defensibility and for onboarding future team members.
- **Extensibility:** architect from Stage 2 onward so that Stage 4/5 physics (point defects, twin criteria, ROM/UQ) can be added as new modules rather than requiring core rewrites — this is the primary justification for early investment in clean module boundaries even though early stages don't need them.
- **Data management:** structured storage (HDF5/XDMF) for field data, with metadata capturing every material property version and solver configuration used to produce a given run, to ensure reproducibility.

---

## 7. Experimental Validation Program (Must Run in Parallel, Not Sequentially After Modeling)

Simulation without a matched validation program produces an uncalibrated model of unknown accuracy — this is the most common failure mode in crystal-growth modeling projects and must be resourced from Year 1.

- **In-situ/ex-situ thermal validation:** thermocouple arrays in furnace/crucible (as geometry allows) to validate the thermal boundary conditions and furnace model independent of the crystal growth physics itself.
- **Interface shape validation:** post-growth interface demarcation (dopant striation revealed by etching, or in-situ techniques where feasible) compared against simulated interface shape/curvature.
- **Segregation validation:** SIMS/Hall/resistivity profiling along grown boules compared against simulated axial/radial dopant profiles — this is a high-value, relatively low-cost validation dataset.
- **Defect density validation:** EPD (etch pit density) mapping and X-ray topography compared against simulated dislocation density fields.
- **Stress validation:** synchrotron X-ray or infrared photoelasticity (where applicable to InP) for direct residual stress comparison.
- **Iterative model calibration:** formal inverse-modeling/Bayesian calibration loop (§8) using this experimental data to refine the highest-uncertainty parameters (plasticity constants, effective segregation coefficients, radiative properties) rather than treating validation as a terminal checkbox.

---

## 8. Uncertainty Quantification, Calibration, and Predictive Confidence

- Formal sensitivity analysis (Sobol indices or Morris screening) across the materials property database to identify which uncertain parameters actually drive output uncertainty in interface shape, segregation, and dislocation density — prioritize experimental/DFT effort on the high-sensitivity parameters identified here rather than uniformly refining all properties.
- Bayesian calibration framework: use experimental validation data (§7) to update prior distributions on poorly constrained parameters (esp. Alexander–Haasen plasticity constants and segregation coefficients), producing posterior predictive distributions rather than single-point "best fit" predictions.
- Report all industrial-facing predictions (interface shape, EPD maps, yield estimates) with quantified confidence intervals, not deterministic point values — this is what distinguishes an "industrial-grade" tool from an academic demonstration code.

---

## 9. Industrial Deployment and Productization

- Reduced-order/surrogate model layer for rapid (seconds-to-minutes) furnace-recipe screening, with the full 3D model reserved for final design verification and periodic ROM retraining.
- User interface for process engineers: parametrized furnace/recipe input, automated meshing for standard ampoule geometries, standardized report generation (interface evolution, stress hotspots, predicted EPD map, dopant profile).
- Integration hooks for optimization workflows (recipe/heater-profile optimization against yield/quality objectives) — likely via the ROM layer for tractable turnaround.
- IP, licensing, and data-provenance management if the property database and calibrated parameters constitute proprietary competitive advantage.
- Long-term maintenance plan: property database updates as new data becomes available, regression suite to prevent silent degradation, versioned model releases tied to validated furnace configurations.

---

## 10. Program Timeline Summary (Indicative, 4-Year Horizon)

| Phase | Duration | Key Milestone |
|---|---|---|
| Foundations, property DB, 1D/0D models | Months 0–6 | Verified thermal/segregation baseline models |
| 2D axisymmetric continuum model | Months 4–14 | Validated interface-shape and segregation predictions |
| 3D transient multiphysics + stress/plasticity | Year 1–2.5 | Coupled dislocation-density predictions, first EPD validation |
| Defect-resolved model (point defects, twinning, voids) | Year 2–3.5 | Full defect-risk simulation capability |
| Industrial digital twin (ROM, UQ, furnace-scale) | Year 3–4+ | Deployed tool with quantified predictive confidence |

Experimental validation (§7) and materials property acquisition (§3) run continuously across all phases, not as discrete downstream stages.

---

## 11. Key References

**VGF/VB and III-V Bulk Growth Modeling**
- Duffar, T. (Ed.), *Crystal Growth Processes Based on Capillarity: Czochralski, Floating Zone, Shaping and Crucible Techniques*, Wiley, 2010.
- Dost, S., Lent, B., *Single Crystal Growth of Semiconductors from Melts*, Crystal Growth & Materials Processing series, Elsevier.
- Rudolph, P., "Non-stoichiometry related defects at the melt growth of semiconductor compound crystals — a review," *Crystal Research and Technology*, 2005.
- Rudolph, P., "Dislocation formation and propagation in melt-grown compound semiconductor crystals," *Journal of Crystal Growth*, 2006.
- Yeckel, A., Derby, J.J., "Effect of steady-state interface shape and melt convection on dopant segregation in vertical Bridgman growth," *Journal of Crystal Growth*, 2000.
- Kakimoto, K. et al., numerical studies on VB/VGF thermal-fluid modeling (multiple papers, *Journal of Crystal Growth*, 1990s–2000s).

**InP-Specific Growth and Properties**
- Bliss, D.F. et al., "Vertical gradient freeze growth of InP," *Journal of Crystal Growth*, various years.
- Bachmann, K.J., Buehler, E., "The growth and characterization of high-purity InP for device applications," *Journal of Electronic Materials*, 1974.
- Rudolph, P., Jurisch, M., "Bulk growth of GaAs — an overview" (methodological analog widely used for InP defect modeling due to sparser InP-specific plasticity data), *Journal of Crystal Growth*, 1999.

**Continuum Transport and Convection in Melt Growth**
- Derby, J.J., Brown, R.A., "Thermal-capillary analysis of Czochralski and liquid encapsulated Czochralski crystal growth," *Journal of Crystal Growth*, 1986 (methodology transfers to VGF/VB thermal-convective analysis).
- Adornato, P.M., Brown, R.A., "Convection and segregation in directional solidification of dilute and non-dilute binary alloys," *Journal of Crystal Growth*, 1987.

**Segregation Theory**
- Burton, J.A., Prim, R.C., Slichter, W.P., "The distribution of solute in crystals grown from the melt," *Journal of Chemical Physics*, 1953.

**Dislocation Dynamics / Thermoplasticity**
- Alexander, H., Haasen, P., "Dislocations and plastic flow in the diamond structure," *Solid State Physics*, 1968.
- Jordan, A.S., Von Neida, A.R., Caruso, R., "The theory and practice of dislocation reduction in GaAs and InP," *Journal of Crystal Growth*, 1984.
- Miyazaki, N. et al., finite-element thermal-stress/dislocation modeling of III-V crystal growth (multiple papers, *Journal of Crystal Growth*, 1990s–2000s).

**Radiative Transfer in Semi-Transparent Melts**
- Siegel, R., Howell, J.R., *Thermal Radiation Heat Transfer*, Taylor & Francis (standard reference for participating-media formulation adapted to crystal growth furnaces).

**Numerical Methods**
- Voller, V.R., Prakash, C., "A fixed grid numerical modelling methodology for convection-diffusion mushy region phase-change problems," *International Journal of Heat and Mass Transfer*, 1987.
- Donea, J., Huerta, A., Ponthot, J.-P., Rodríguez-Ferran, A., "Arbitrary Lagrangian–Eulerian Methods," in *Encyclopedia of Computational Mechanics*, Wiley, 2004.
- Roache, P.J., *Verification and Validation in Computational Science and Engineering*, Hermosa Publishers, 1998.

**Simulation Software / Prior Art**
- STR Group, CGSim technical documentation and application bibliography (industrial VB/VGF/Cz simulation software).
- Müller, G., Friedrich, J., "Crystal growth, bulk: methods (Bridgman, Czochralski, VGF)," in *Encyclopedia of Materials: Science and Technology*, Elsevier.

---

*This roadmap is intended as a living document. Section 3 (materials property database) and Section 7 (experimental validation) should be treated as the highest-risk, highest-priority parallel workstreams, since numerical and software sophistication (Sections 4–6) cannot compensate for an uncalibrated or unvalidated physical model.*

---

> [!NOTE]
> 
> Generated by Claude.ai
>
> Model: Sonet 5
>
> Prompt: I want to develop a high-fidelity, physics-based numerical model of indium phosphide (InP) single-crystal growth using the Vertical Gradient Freeze (VGF) and Vertical Bridgman (VB) process. Please prepare an extensive, structured development roadmap that identifies every major scientific, engineering, computational, and validation task required to build such a model from first principles through industrial-scale simulation. The roadmap should be sufficiently detailed to serve as the basis for a multi-year research and software development project aimed at producing an industrial-grade simulation tool for InP crystal growth. Emphasize scientific completeness, numerical robustness, extensibility, and predictive accuracy. Provide key references. Show the output in Markdown format.
