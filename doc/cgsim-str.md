# CGSim — Crystal Growth Simulation Software by STR Group

**Prepared:** June 2026  
**Subject:** Comprehensive Technical Assessment of the CGSim Software Package  
**Source:** STR Group Ltd. (str-soft.com)

---

## Table of Contents

1. [Executive Summary](#1-executive-summary)
2. [Background: STR Group](#2-background-str-group)
3. [CGSim Overview and Positioning](#3-cgsim-overview-and-positioning)
4. [Software Architecture and Module Structure](#4-software-architecture-and-module-structure)
5. [Physical Models and Governing Equations](#5-physical-models-and-governing-equations)
6. [Supported Crystal Growth Methods](#6-supported-crystal-growth-methods)
7. [Supported Materials](#7-supported-materials)
8. [Application Domains and Practical Use Cases](#8-application-domains-and-practical-use-cases)
9. [Numerical Methods and Computational Approaches](#9-numerical-methods-and-computational-approaches)
10. [User Interface and Workflow](#10-user-interface-and-workflow)
11. [Visualization: CGSim View](#11-visualization-cgsim-view)
12. [Version History and Recent Releases](#12-version-history-and-recent-releases)
13. [Validation and Industrial Verification](#13-validation-and-industrial-verification)
14. [Competitive Landscape](#14-competitive-landscape)
15. [Industrial and Academic Reach](#15-industrial-and-academic-reach)
16. [Integration with the STR Software Ecosystem](#16-integration-with-the-str-software-ecosystem)
17. [Strengths, Limitations, and Open Questions](#17-strengths-limitations-and-open-questions)
18. [Summary and Conclusions](#18-summary-and-conclusions)
19. [References and Further Reading](#19-references-and-further-reading)

---

## 1. Executive Summary

CGSim (Crystal Growth Simulator) is a specialized commercial simulation package developed and maintained by STR Group Ltd. for the numerical modelling of bulk single-crystal and multicrystalline growth processes from the melt and from solution. It is the flagship product of STR Group's melt-growth product line and is used by more than 170 industrial companies and academic institutions worldwide.

The software addresses the full physical complexity of industrial crystal growth furnaces: global radiative and convective heat transfer, turbulent and laminar melt convection under the action of magnetic fields, species transport and impurity segregation, point-defect dynamics, thermal stresses, and crystal-shape evolution. Its modular design — comprising the 2D global heat-transfer core (Basic CGSim), the 3D turbulent-flow solver (Flow Module), the defect-physics engine (Defects module), and the post-processing visualiser (CGSim View) — allows users to select the level of fidelity required for a given task without running unnecessarily expensive full 3D transient simulations.

As of mid-2026 the current release is **CGSim 26.2**, which introduced 3D anisotropic thermoelastic stress computation. The preceding major release, CGSim 26.1 (December 2025), added quasi-unsteady dopant modelling for Czochralski silicon, gas-phase doping chemistry for phosphorus and boron, Continuous Czochralski (CCz) support, and a twin-formation criterion for GaAs and InP.

---

## 2. Background: STR Group

STR Group Ltd. (Semiconductor Technology Research) is a privately held scientific software and consulting company with offices in multiple countries including an active engineering team in STR Belgrade. The company is focused exclusively on modelling of crystal growth, epitaxy, and semiconductor devices. Its product portfolio spans four product lines:

- **Crystal growth from the melt and solution** — CGSim
- **Bulk crystal growth from the vapour phase** — Virtual Reactor (VR)
- **Deposition and epitaxy** — CVDSim3D, PolySim, DiaDeMo, STREEM
- **Optoelectronic and electronic devices** — SiLENSe, SimuLED, SpeCLED, RATRO, FETIS, BESST, PVcell

STR participates actively in the major international conferences in the crystal-growth and compound-semiconductor communities: ICCGE, ICSCRM, ISMCG/IWMCG, CGCT, CS International, CS ManTech, and others. The company also has a presence under the name STR Japan for the Asian market, where CGSim has been used commercially in SiC solution-growth (TSSG) processes.

---

## 3. CGSim Overview and Positioning

### 3.1 Design Philosophy

CGSim is purpose-built for the crystal growth engineer rather than for a generic CFD or finite-element analyst. The software is designed so that users do not need deep computational expertise: problem setup, geometry definition, and boundary conditions are automated to the maximum practical extent. Geometry can be imported from AutoCAD, and the auto-grid generator supports mismatched block interfaces. The software reconstructs crystal, melt, and encapsulant geometries automatically as the crystal position changes during a growth sequence, enabling serial parametric computations across different growth stages without manual remeshing.

### 3.2 Role in the Design-to-Production Chain

CGSim sits at the intersection of process R&D and production engineering. Its principal function is to replace or augment costly physical trials with numerical experiments on the following categories of questions:

- Hot-zone design: selection and configuration of heaters, heat shields, insulation, and crucibles.
- Pull-rate optimisation: maximising growth rate while keeping the crystalline structure intact.
- Doping and impurity control: achieving target resistivity uniformity along the crystal axis and across the boule diameter.
- Defect engineering: understanding and controlling vacancy/interstitial populations, void formation, and oxygen precipitation.
- Energy efficiency: reducing heater power consumption and shortening thermal cycle time.
- Crystal quality during cooling: managing residual stresses and dislocation generation during the post-growth cool-down.

---

## 4. Software Architecture and Module Structure

CGSim consists of four main components, each addressing a distinct level of physical detail.

### 4.1 Basic CGSim (2D Global Heat Transfer)

This is the foundational module and the starting point for virtually all simulations. It performs 2D axisymmetric global heat transfer calculations across the entire furnace domain — heaters, thermal insulation, crucible, melt, crystal, gas atmosphere, and encapsulant. Heat is transported by conduction, convection (approximated by effective conductivity turbulence models in 2D), and radiation. Semi-transparent materials (silicon crystal, quartz, sapphire, YAG, BGO, etc.) require special treatment of internal radiation, which is handled by advanced multi-band spectral models.

The 2D steady-state approach is computationally inexpensive and is therefore the primary tool for parametric sweeps over hot-zone geometry, heater power profiles, crystal pull rates, and rotation rates. It outputs temperature distributions, melt-crystal interface shapes, heat flux maps, and V/G (ratio of pull velocity to axial temperature gradient) distributions — the key control parameter for intrinsic point-defect type in silicon.

### 4.2 Flow Module (3D Turbulent and Laminar Convection)

The Flow Module is the high-fidelity 3D solver for melt and gas convection. It couples the full 3D Navier-Stokes equations (in rotating frames where appropriate) with the global heat-transfer computation, so that the crystallization front shape evolves self-consistently with the 3D flow field.

Key capabilities of the Flow Module include:

- **Turbulence modelling:** RANS (Reynolds-Averaged Navier-Stokes), LES (Large-Eddy Simulation), DNS (Direct Numerical Simulation), and quasi-DNS approaches are available. The turbulence model has been specially adapted for high-Prandtl-number and high-Reynolds-number melt flows.
- **Magnetic field effects:** Vertical (axial), horizontal, and cusp DC magnetic field configurations are natively supported. AC (travelling or rotating) magnetic field configurations can be implemented in customised versions. The solver accounts for conjugate electric current flow in both the melt and the solid crystal, enabling quantitative prediction of MHD flow damping and electromagnetic stirring.
- **3D grid generation:** An automatic 3D grid generator extrudes 2D grids by rotation and supplements the central axis domain with structured quadrilateral blocks to avoid singularity artefacts on the rotation axis. This provides high-quality grids for the crystallisation zone without manual intervention.
- **Parallel computing:** A parallel version of the Flow Module solver is available for deployment on Linux clusters and on Windows-based multi-PC networks.
- **Impurity and species transport:** The module solves scalar transport equations for oxygen, carbon, dopants, and other species simultaneously with the flow equations, giving fully coupled concentration fields.

### 4.3 Defects Module

The Defects module implements a quantitative model of intrinsic point-defect dynamics in the growing crystal. It tracks:

- **Vacancy (V) and self-interstitial (I) concentrations** as functions of position and time, with initial boundary conditions at the melt-crystal interface given by Voronkov's theory.
- **Convective and diffusive transport** of V and I in the solid phase, accounting for the steep temperature gradient in the crystal.
- **Clusterisation** (void formation from vacancy clusters, dislocation loops from interstitial clusters) and **V-I recombination**.
- **V/G mapping** along and across the crystallisation front — the central engineering indicator for controlling whether the crystal will be vacancy-rich, interstitial-rich, or in the transition (OSF-ring) regime.
- **Oxygen precipitation** and **carbon segregation** modelling.
- **Thermal stresses** — via thermoelastic constitutive models — whose coupling to point-defect equilibrium concentrations is essential for accurate prediction in heavily doped or large-diameter crystals.

### 4.4 CGSim View

CGSim View is the post-processing and visualisation environment. It provides:

- 2D colour maps and contour plots of all computed fields (temperature, velocity, species concentration, stress components, V/G ratio, defect concentrations, etc.)
- 1D distribution plots along any boundary or internal line, with export to hard disk
- Heat flux and mass flux visualisations
- Temperature gradient maps along the crystallisation front
- Animation tools for time-varying 3D flow fields
- Movie generation for transient simulations

---

## 5. Physical Models and Governing Equations

### 5.1 Global Heat Transfer

The global simulation domain encompasses all solid and fluid regions of the furnace. The governing equation for thermal energy transport in solid regions is the steady or time-dependent heat conduction equation with temperature-dependent thermal conductivity. In fluid regions (melt, gas, encapsulant), the full energy equation with convective transport is solved.

**Radiative heat transfer** is a dominant mechanism in high-temperature crystal growth and receives special treatment in CGSim:

- Radiative exchange between diffuse or specular surfaces is modelled using view-factor methods for opaque surfaces.
- In semi-transparent materials — silicon at near-infrared wavelengths, sapphire, quartz, YAG — radiation penetrates the bulk and is absorbed and re-emitted volumetrically. CGSim implements multi-band spectral models for internal radiation, accounting for specular reflectivity at boundaries and wavelength-dependent absorption and scattering coefficients.
- Marangoni (thermocapillary) convection at free melt surfaces is modelled through surface-tension-gradient boundary conditions.

### 5.2 Melt and Gas Flow

Melt flow in Czochralski and related configurations is driven by:

- **Thermal buoyancy** (natural convection, Grashof number dominated)
- **Forced convection** from crystal and crucible rotation (Taylor-Couette instabilities, Ekman pumping)
- **Marangoni forces** at the free melt surface
- **Electromagnetic Lorentz forces** when a magnetic field is applied

In large-diameter silicon growth (300 mm and above), the melt Reynolds number is high enough that the flow is turbulent. CGSim's RANS models use turbulence closures adapted to rotating systems with stratification, and the LES/quasi-DNS approaches resolve large turbulent structures responsible for non-uniform crystallisation rates. The 3D unsteady approach has been validated against experimental crystallisation-rate distributions in industrial 300 mm pullers.

Argon gas flow above the melt surface is modelled as a separate laminar or turbulent domain, depending on the local Reynolds number. Gas flow affects both the temperature distribution in the upper crystal and the transport of volatile species (SiO, CO in silicon growth; AsO and related species in GaAs growth).

### 5.3 Species Transport and Chemical Models

CGSim implements detailed chemical models for impurity and dopant transport:

- **Oxygen in silicon:** SiO evaporation from the melt surface, dissolution from the quartz crucible wall, transport in the melt and gas, and incorporation into the crystal at the solidification front.
- **Carbon in silicon:** CO gas-phase generation, dissolution into the melt, and incorporation — directly relevant to multicrystalline silicon photovoltaic ingots where carbon leads to quality-limiting inclusions.
- **Phosphorus and boron doping (CGSim 26.1+):** An enhanced unsteady chemical model accounts for incorporation of P and B dopants into the silicon melt from gas-phase species, enabling gas-phase doping process design.
- **GaN from solution:** The Ga-Na-Li ternary solvent system (as of CGSim 23.1, expanding the earlier Ga-Na model) is supported for ammonothermal and flux-based GaN solution growth.
- **Ga₂O₃ growth:** A chemical model applicable to arbitrary Ar-O₂-CO₂ gas-mixture compositions enables simulation of β-Ga₂O₃ Czochralski growth, an important emerging wide-bandgap semiconductor.
- **SiC from solution (TSSG):** Metal solvents Cr, Ti, Al, and Fe are available in the chemical database for top-seeded solution growth of SiC. The model includes RF heating, Lorentz forces, ACRT (Accelerated Crucible Rotation Technique), and SiC dissolution/crystallisation kinetics.

### 5.4 Thermal Stress and Mechanical Models

Thermal stresses arise from non-uniform temperature distributions in the growing crystal and are a primary source of dislocation generation and structural defects. CGSim implements:

- **Thermoelastic stress computation** in 2D (axisymmetric) and 3D (since CGSim 26.2).
- **Anisotropic elasticity (CGSim 26.2):** The most recent release (May 2026) introduced 3D anisotropic thermoelastic stress computation, enabling the stress field to be analysed as a function of the crystal growth direction — e.g. ⟨100⟩ vs. ⟨111⟩ — and facet geometry. This is significant because the elastic stiffness tensor of cubic crystals (Si, GaAs, InP) is orientation-dependent, and accurate dislocation-density predictions require correctly resolving shear stresses on specific slip systems.
- **Dislocation density modelling** via Alexander-Haasen or similar constitutive laws, coupling the resolved shear stress to the evolution of dislocation density during growth and cooling.
- **Structure-loss probability:** The anisotropic 3D stress model feeds directly into assessments of the probability of monocrystalline structure loss during neck formation and seeding phases.

### 5.5 Point-Defect Dynamics

The quantitative V/G criterion established by Voronkov for silicon is directly implemented. The Defects module solves coupled diffusion-advection-reaction equations for vacancy and interstitial concentrations in the crystal, with:

- Equilibrium concentrations at the melt-crystal interface as a function of local temperature gradient and interface velocity.
- Recombination reactions between V and I.
- Clustering terms for void (COPs: Crystal-Originated Particles) and dislocation loop (LPITs) formation.
- Interaction with oxygen impurity (oxygen retards clustering and modifies the V/I equilibrium).
- The position of the OSF (Oxidation-Induced Stacking Fault) ring as a function of process parameters.

In recent versions this model has been extended to account for the effect of thermal stress on the equilibrium concentrations of point defects, which is critical for predicting defect distributions in heavily doped wafers.

---

## 6. Supported Crystal Growth Methods

CGSim explicitly supports — with purpose-built models for geometry, boundary conditions, and relevant physics — the following growth techniques:

### 6.1 Czochralski Method (Cz)

The primary and most thoroughly developed application domain. Features supported:

- Standard Cz with resistive (Joule) heating
- Magnetic-field-assisted Cz: vertical magnetic field (VMF), horizontal magnetic field (HMF), cusp magnetic field (CMF) — all DC; AC fields in customised versions
- Large-diameter Cz (300 mm silicon, 400 mm silicon demonstrated)
- Solar-grade Cz for photovoltaic silicon (100 mm to large-diameter)
- **Continuous Czochralski (CCz):** a configuration relevant to photovoltaic silicon mass production in which granular silicon feedstock is continuously fed into the crucible to maintain a near-constant melt level. CGSim 26.1 added analysis of dopant contribution from feedstock and the thermal/flow impact of granular feeding.

### 6.2 Liquid-Encapsulated Czochralski (LEC) and Vapour-Pressure Controlled Czochralski (VCz)

These variants are used for III-V semiconductors (GaAs, InP, GaP) where the high vapour pressure of the group-V element (As, P) must be suppressed during growth. CGSim models:

- Boric oxide (B₂O₃) encapsulant layer: its turbulent flow, heat transport, and viscosity
- High-pressure gas atmosphere (N₂ at up to ~60 bar for InP)
- Gas-phase composition control in VCz (Ar + As₄/P₄ overpressure)

### 6.3 Bridgman and Vertical Gradient Freeze (VGF)

The Bridgman technique involves directional solidification by translating a melt-filled ampoule through a temperature gradient. VGF achieves the same result by programming time-dependent heater-power profiles in a multi-zone furnace, without ampoule movement. CGSim models:

- Full thermal field evolution in multi-zone furnaces
- Melt and gas convection in the ampoule
- Interface shape evolution and velocity
- Impurity redistribution (segregation coefficients)
- Stress and dislocation dynamics in III-V crystals (GaAs, InP, GaP) during growth and cool-down
- Optimisation of heater-power sequences to achieve desired interface flatness

### 6.4 Kyropoulos Method

Used primarily for large-mass sapphire (Al₂O₃) boule growth. In this method, a seed crystal is slowly withdrawn from a crucible of melt while the melt level remains largely constant and the crystal grows into the melt bulk rather than being pulled out of it. CGSim capabilities include:

- Turbulent sapphire melt flow
- Laminar gas flow in the furnace atmosphere
- Marangoni forces on the melt surface
- Radiative heat exchange in the semi-transparent crystal with specular reflectivity at boundaries, internal absorption, and scattering
- Fully unsteady computations for hot-zone design and process recipe optimisation
- Application to other optical crystals (lithium niobate, BGO) beyond sapphire

### 6.5 Heat Exchanger Method (HEM)

HEM is another technique for large-boule sapphire growth in which a heat exchanger positioned at the bottom of a pedestal in the melt centre serves as the nucleation and crystal growth zone. CGSim addresses the complex three-dimensional flow and thermal field in this geometry, including the interaction between the cooled pedestal and the natural convection roll structures in the melt.

### 6.6 Top-Seeded Solution Growth (TSSG) of SiC

TSSG is a solution-based alternative to PVT for SiC, using a metallic Si-C solvent at temperatures around 1700-2000 °C. It offers advantages for defect control (particularly basal-plane dislocation reduction) compared to PVT. CGSim's TSSG model covers:

- **RF induction heating** with eddy-current-based power deposition calculation
- **Lorentz forces** acting on the electrically conducting melt under the RF magnetic field
- **Solution flow** including natural convection, forced convection from crystal/crucible rotation, and Lorentz-force-driven flow; ACRT (step-change rotation profiles) can be modelled
- **Chemical species transport:** SiC dissolution at the crucible walls and precipitation at the crystal seed
- **Available solvents:** Cr, Ti, Al, Fe as metallic additives to the Si-C base
- Stress and dislocation predictions in the growing SiC boule

### 6.7 Directional Solidification (DS) for Multicrystalline Silicon

CGSim can simulate the casting and directional solidification of multicrystalline silicon ingots used in photovoltaic applications. The model addresses:

- Thermal field evolution during the full melt-hold-solidify-anneal-cool cycle
- Crystallisation front shape and velocity
- Impurity (oxygen, carbon) transport and segregation
- Grain size prediction (qualitative)
- Thermal stresses and the risk of crack formation during cool-down

### 6.8 Hydrothermal Autoclave Growth (Quartz)

Quartz (SiO₂) single crystals are grown by hydrothermal synthesis in pressurised autoclaves over weeks. CGSim models the flow of the supercritical aqueous mineraliser solution and the associated heat and mass transfer that drives SiO₂ dissolution in the nutrient zone and deposition on the seed crystals.

---

## 7. Supported Materials

CGSim's material database and physical models cover an extensive range of crystals, grouped below by category:

### 7.1 Elemental Semiconductors
- **Silicon (Si):** Electronic-grade Cz, solar-grade Cz, multicrystalline DS, CCz. Supported dopants: boron (p-type), phosphorus, arsenic, antimony (n-type). Oxygen and carbon as principal impurities.
- **Germanium (Ge):** Czochralski growth, used for high-efficiency multijunction solar cells and IR optics substrates.
- **Silicon-Germanium (SiGe):** Alloy growth for strain-engineering substrates.

### 7.2 III-V Compound Semiconductors
- **Gallium Arsenide (GaAs):** LEC, VCz, VGF/Bridgman. Semi-insulating and n-type. Twin formation criterion introduced in CGSim 26.1.
- **Indium Phosphide (InP):** High-pressure LEC (HPLEC). Twin formation criterion (CGSim 26.1).
- **Gallium Phosphide (GaP):** Bridgman/VGF.
- **Indium Arsenide (InAs)** and other III-V compounds in customised configurations.

### 7.3 Wide-Bandgap and Ultra-Wide-Bandgap Semiconductors
- **Gallium Oxide (β-Ga₂O₃):** Czochralski growth with Ar-O₂-CO₂ gas chemistry (CGSim 23.1 extended this to arbitrary gas-mixture compositions). Highly relevant for power electronics.
- **Gallium Nitride (GaN) from solution:** Ga-Na and Ga-Na-Li solvents (expanded in CGSim 23.1).

### 7.4 Optical and Laser Crystals
- **Sapphire (Al₂O₃):** Kyropoulos and HEM techniques. Full semi-transparent radiation model including specular reflectivity. Production of large boules (150 kg and above addressed).
- **Yttrium Aluminium Garnet (YAG, Y₃Al₅O₁₂):** Laser gain medium; Czochralski growth modelled with semi-transparent radiation.
- **Bismuth Germanate (BGO, Bi₄Ge₃O₁₂):** Scintillator crystal.
- **Lithium Niobate (LiNbO₃):** Electro-optic and acousto-optic applications.
- Other oxide scintillators and laser hosts on a project basis.

### 7.5 Solar Silicon (Upgraded/Multicrystalline)
- **Upgraded Metallurgical Grade Silicon (UMG-Si):** Directional solidification modelling with impurity purification analysis (boron, phosphorus, metallic impurities).
- Multicrystalline Si (mc-Si) for photovoltaic production.

---

## 8. Application Domains and Practical Use Cases

Based on STR's published application examples and documented industrial use, the principal engineering problems solved with CGSim are:

### 8.1 Hot-Zone Design and Optimisation

The shape, position, and configuration of heaters, heat shields, and insulation materials govern the temperature field in the furnace, which in turn controls the crystallisation front curvature, the temperature gradient at the interface (G), and therefore the V/G ratio. CGSim parametric studies allow:

- Comparison of alternative heat-shield geometries to reduce radial temperature gradients in the crystal (reducing dislocation density)
- Tuning of heater-power distribution to maintain a flat or slightly convex crystallisation front
- Analysis of multiple heater-zone configurations for VGF/Bridgman furnaces
- Quantitative prediction of power consumption as a function of design choices

### 8.2 Process Recipe Optimisation

Time-dependent control sequences — heater power ramp, crystal pull rate, crystal and crucible rotation rates, and cool-down schedule — can be optimised using serial computations across multiple growth stages. Objectives include:

- Maximising the fraction of the crystal in the defect-free (perfect-crystal) regime (neither vacancy-dominated nor interstitial-dominated)
- Shortening the growth cycle without quality penalties
- Reducing structure-loss risk during seeding and shouldering phases

### 8.3 Magnetic Field Design for Silicon

Magnetic fields (Cusp, Horizontal, Vertical) are routinely applied in 300 mm silicon Cz pullers to dampen melt turbulence and reduce oxygen incorporation. CGSim's 3D MHD simulations allow:

- Optimisation of field strength and field configuration to achieve target melt-flow suppression
- Prediction of oxygen content as a function of magnetic field parameters
- Analysis of residual flow structures and their effect on oxygen inhomogeneity

### 8.4 Impurity and Doping Uniformity

- **Axial resistivity uniformity** in Cz silicon: controlled by the effective segregation coefficient of the dopant, which depends on the boundary-layer thickness at the melt-crystal interface, itself governed by melt convection intensity.
- **Radial resistivity uniformity:** Affected by 3D turbulent fluctuations in the melt. CGSim's 3D unsteady simulations directly resolve these non-uniformities.
- **Quasi-unsteady dopant modelling (CGSim 26.1):** This new method provides faster and more accurate computation of the axial dopant profile along the crystal without running a full time-domain integration across the entire growth cycle, using a dedicated GUI for setup.

### 8.5 Defect Engineering

- Positioning of the OSF ring as a function of pull rate and magnetic field
- Prediction of void (COP) and interstitial-cluster (LPIT) distributions across the crystal cross-section
- Oxygen precipitate nucleation zones in relation to the thermal history during cool-down
- The effect of heat-shield adjustments on the V/G map: defect engineering in production contexts

### 8.6 Stress and Dislocation Control

- Prediction of etch-pit density (EPD) distributions in GaAs and InP crystals from VGF/LEC furnaces
- Design of thermal annealing schedules to reduce residual stress in the cooled crystal
- 3D anisotropic stress analysis (CGSim 26.2) for orientation-dependent dislocation behaviour in cubic crystals

### 8.7 Continuous Czochralski (CCz)

CCz technology, in which granular or chunk silicon is continuously replenished to the melt, is increasingly important for photovoltaic silicon manufacturing at scale because it allows longer crystal pulls and more stable resistivity control. CGSim 26.1 added:

- Analysis of the thermal impact of granular silicon feeding on melt temperature distribution and convection
- Dopant contribution from the feedstock to the melt, enabling resistivity profile prediction in CCz

---

## 9. Numerical Methods and Computational Approaches

### 9.1 Grid Generation

CGSim uses a structured multi-block approach with body-fitted curvilinear coordinates. Key features:

- **AutoCAD import** of furnace cross-sections enables rapid geometry setup from engineering drawings.
- **Auto-grid generation:** Meshes are automatically reconstructed for each crystal position in a series of pull-stage computations, allowing automated parametric studies over the full growth cycle without manual remeshing.
- **3D grid extrusion:** For the Flow Module, the 2D grid is extruded azimuthally with special treatment of the central axis (quadrilateral blocks rather than degenerate triangular cells at the singularity).
- **Mismatched block interfaces** are handled natively, permitting different mesh densities in different regions.

### 9.2 Discretisation Schemes

- Finite-volume discretisation for the governing transport equations on the body-fitted structured meshes.
- **Advanced approximations of convective terms:** High-order upwind or blended convection schemes reduce numerical diffusion on coarser grids, enabling accurate simulations on meshes that are feasible within engineering time constraints.
- Implicit time integration for transient simulations, with adaptive or user-specified time-stepping.

### 9.3 Turbulence Modelling Options

- **RANS:** Standard two-equation models (k-ε and variants) adapted for melt flows in rotating systems. The adaptation ensures physical turbulent Prandtl number behaviour under the strong stable stratification (hot core, cooler crystal) typical of silicon Cz growth.
- **LES (Large-Eddy Simulation):** Resolves large turbulent structures (Taylor columns, spoke patterns from Marangoni instabilities) explicitly; sub-grid-scale contribution modelled with Smagorinsky-type closure.
- **DNS / quasi-DNS:** For research-level studies of turbulence structure at moderate Reynolds numbers in specific crystallisation-zone regions.
- **URANS:** Unsteady RANS for intermediate fidelity in strongly time-varying configurations.

### 9.4 Radiation Models

- **Opaque-surface exchange:** View-factor method for furnace elements that are optically opaque.
- **Semi-transparent volume radiation:** Radiative transfer equation (RTE) discretisation inside semi-transparent crystal and melt domains. Multi-band spectral treatment captures the transition from transparent at short wavelengths to absorbing at long wavelengths in silicon and oxide crystals.
- **Specular boundaries:** Reflected radiation at polished crystal surfaces (sapphire, YAG) requires distinction between diffuse and specular components.

### 9.5 Parallel Computing

The Flow Module includes a parallelised solver for distributed-memory systems, addressing the significantly higher computational cost of 3D transient MHD simulations compared to 2D steady-state runs. Deployment options include Linux MPI clusters and Windows network parallelism.

---

## 10. User Interface and Workflow

### 10.1 Graphical User Interface

CGSim provides a dedicated GUI that removes the need for low-level input file editing for standard Cz, LEC, and Bridgman configurations:

- **Problem definition wizards** guide the user through furnace geometry specification, material assignment, and boundary condition setup.
- **Geometry import:** AutoCAD DXF/DWG import of furnace cross-sections.
- **Material database:** Temperature-dependent thermal, optical, and mechanical properties for all supported materials are pre-loaded.
- **Boundary condition templates** for common furnace configurations reduce setup errors.
- **Serial computation manager:** Automated serial runs for multiple crystal positions (from seeding through end-of-run), eliminating manual restart procedures.

### 10.2 Computation Manager

An integrated Computation Manager provides real-time monitoring of running simulations:

- Convergence residuals for all equations
- Averaged crystallisation rate as a function of simulation time or iteration
- Live view of crystallisation front shape and crystallisation-rate distribution along the melt-crystal interface
- Distributions of key computed variables (temperature, velocity magnitude) for qualitative monitoring

### 10.3 Dedicated GUI for Quasi-Unsteady Dopant Modelling (CGSim 26.1)

A new dedicated GUI introduced in CGSim 26.1 supports the quasi-unsteady dopant analysis workflow, making it easier to set up and interpret axial resistivity uniformity computations without navigating the full transient-solver parameter space.

---

## 11. Visualization: CGSim View

CGSim View is the post-processor and serves as the primary engineering analysis environment after a simulation completes:

- **2D field maps:** Full colour plots of temperature, velocity components, species concentration, V/G ratio, stress components, point-defect concentrations, and other scalars and vectors across arbitrary cross-sections.
- **1D boundary distributions:** Plots of any field quantity along any furnace boundary (e.g., temperature gradient along the melt-crystal interface, oxygen flux along the crucible wall). These can be exported as numerical data.
- **Heat and mass flux visualisation:** Vector plots and streamline displays.
- **V/G and temperature gradient along the crystallisation front:** Critical for defect-type prediction in silicon.
- **Animation:** Time sequences of transient 3D flow computations can be assembled into animations and saved to disk.
- **3D rendering tools** for the Flow Module outputs: volumetric temperature and velocity visualisation, iso-surface plots.

---

## 12. Version History and Recent Releases

The following is a summary of noteworthy CGSim releases over recent years, reconstructed from public announcements on str-soft.com:

| Version | Approximate Date | Key New Capabilities |
|---|---|---|
| CGSim 22.0 | April 2022 | Major restructuring; updated flow solver |
| CGSim 23.1 | May 2023 | GaN growth from Ga-Na-Li solution; Ga₂O₃ with arbitrary Ar-O₂-CO₂ gas mixture |
| CGSim 25.x | October–November 2025 | Incremental improvements (exact features not published in detail) |
| **CGSim 26.1** | **December 2025** | Quasi-unsteady dopant modelling; gas-phase P and B doping; CCz support; twin-formation criterion for GaAs/InP |
| **CGSim 26.2** | **May 2026** | 3D anisotropic thermoelastic stress; orientation-dependent structure-loss prediction |

The rapid succession of 26.x releases (26.1 in December 2025, 26.2 in May 2026) indicates an accelerating cadence of improvements, particularly in the areas of dopant transport and mechanical analysis.

---

## 13. Validation and Industrial Verification

Confidence in CGSim's predictions rests on a body of published validation work conducted in collaboration with industrial partners and academic groups:

### 13.1 Temperature Field Validation

A key validation was conducted in collaboration with **Siltronic AG**, comparing CGSim-predicted temperature distributions in a 300 mm silicon Cz puller against thermocouple measurements taken inside the growing crystal and inside lateral and bottom insulations. The agreement demonstrated that CGSim can adequately predict industrial-scale temperature distributions including the crystal interior, which is otherwise experimentally inaccessible during growth.

### 13.2 Crystallisation Front Geometry

Multiple publications compare computed melt-crystal interface shapes with post-mortem measurements (e.g., etch reveals on rapidly quenched samples). Agreement between CGSim's 3D unsteady simulations and experimental interface geometries for 300 mm silicon has been reported.

### 13.3 Marangoni Convection Patterns

CGSim has been shown to reproduce the spoke-like temperature oscillation patterns at the melt free surface — a manifestation of Marangoni (thermocapillary) convection — that are observed experimentally via infrared thermography. This is a qualitatively demanding test of the surface boundary condition implementation.

### 13.4 Carbon Reduction in Multicrystalline Silicon

In a reported industrial application, CGSim-guided redesign of the directional solidification furnace hot zone and process recipe led to a **10% reduction in carbon concentration** in the grown crystal, verified by secondary ion mass spectrometry (SIMS) measurements. This is a direct demonstration of production-level process optimisation enabled by the software.

### 13.5 Oxygen and Doping Predictions

Oxygen concentration predictions in the silicon melt and at the crystal surface, together with dopant (e.g., phosphorus) axial profiles, have been validated against experimental data in multiple published studies, including by the STR group itself and by independent researchers.

### 13.6 SiC TSSG — Japan Patent Applications

Multiple Japanese patent applications (filed by companies including Sumitomo Electric and others) cite CGSim (STR Japan, Ver. 14.1) as the simulation tool used to optimise temperature gradients and crucible geometry for SiC TSSG processes, providing independent corroboration of the software's industrial uptake in the SiC market.

---

## 14. Competitive Landscape

CGSim operates in a small niche market. The three commercially available 2D/3D Czochralski simulation codes recognised in the scientific literature are:

| Software | Developer | Key Characteristics |
|---|---|---|
| **CGSim / Flow Module** | STR Group Ltd. | 2D global heat transfer + 3D turbulent flow; broadest material coverage including optical crystals, Ga₂O₃, TSSG SiC, solution growth; active commercial development |
| **CrysMAS / STHAMAS** | Fraunhofer IISB (Germany) | 2D axisymmetric; strong in oxide crystals and photovoltaic Cz Si; academic/institute origin; widely cited |
| **FEMAG-CZ** | FEMAGSoft S.A. | 2D axisymmetric Cz Si focus; used by European silicon wafer manufacturers |

All three codes provide broadly equivalent functionality for 2D axisymmetric simulation of global heat and mass transport in Czochralski processes: turbulent melt and gas convection in rotating geometries, conjugate radiative/convective/conductive/advective heat transport, latent-heat release, crystal-melt interface deformation. They differ in numerical approaches for grid generation, radiation modelling, turbulence models, and species transport.

CGSim's distinguishing characteristics relative to competitors include:

1. **Broader material scope** — extensive compound semiconductor (GaAs, InP, GaN solution, Ga₂O₃), optical crystal (sapphire Kyropoulos/HEM, YAG), and solution-growth (TSSG SiC, hydrothermal quartz) coverage.
2. **3D turbulent MHD capability** — the Flow Module's LES/quasi-DNS 3D MHD solver for large-diameter magnetic-field-assisted silicon growth is more advanced than what is available in CrysMAS or FEMAG.
3. **Active commercial roadmap** — frequent versioned releases with documented new features indicate ongoing investment in R&D.
4. **Widest industrial user base** (>170 users per LinkedIn) among the three.

General-purpose CFD codes (ANSYS Fluent, COMSOL, OpenFOAM) are also used for crystal growth simulation, as demonstrated by published work using Fluent for Cz silicon. However, these require substantially more expert effort for problem setup (no crystal-growth-specific geometry automation, no built-in semi-transparent radiation, no automated crystal-position series) and are generally used by research groups rather than production engineers.

---

## 15. Industrial and Academic Reach

STR Group reports that **over 170 industrial companies and academic institutions** worldwide are end-users of its software. CGSim's user base spans:

- **Silicon wafer manufacturers:** Companies producing 300 mm electronic-grade Cz silicon wafers for logic and memory chips (verified collaboration with Siltronic AG).
- **Photovoltaic silicon producers:** Companies growing solar-grade Cz and directional-solidification multi-silicon.
- **III-V semiconductor substrate suppliers:** GaAs and InP substrate manufacturers using LEC and VGF furnaces.
- **SiC substrate companies:** Japanese and Korean SiC TSSG research groups and production companies.
- **Sapphire producers:** LED substrate and optical sapphire boule growers using Kyropoulos and HEM techniques.
- **Oxide crystal producers:** YAG laser crystal growers, BGO scintillator crystal producers.
- **University and national laboratory research groups:** Crystal growth groups working on fundamental process understanding, typically using CGSim alongside experimental validation work.

CGSim has also been cited in technical training and educational contexts: STR delivered a practical hands-on CGSim session at the **1st International School on Modelling in Crystal Growth (ISMCG 1)** in Timisoara, Romania (September 2024), alongside the IWMCG 11 workshop.

---

## 16. Integration with the STR Software Ecosystem

CGSim is one product in STR's integrated suite of simulation tools covering the full crystal growth-to-device design chain:

- **Virtual Reactor (VR):** Companion product for bulk crystal growth from the gas phase (PVT SiC, PVT AlN, HVPE GaN/AlN, HTCVD SiC). VR and CGSim together cover the complete bulk semiconductor substrate production space.
- **CVDSim3D:** 3D epitaxial reactor simulation for MOCVD (III-Nitrides, III-Vs), Si/SiGe CVD, ALD, SiC CVD, HVPE.
- **PolySim:** Polysilicon deposition via the Siemens CVD process — directly relevant to the silicon feedstock used in Cz pullers.
- **DiaDeMo:** MPCVD diamond growth simulator.
- **SiLENSe / SimuLED / SpeCLED / RATRO / BESST / FETIS / PVcell:** Device-level simulation of LEDs, laser diodes, HEMTs, and photovoltaic cells.
- **STREEM AlGaN / InGaN:** Stress engineering simulators for epitaxial nitride structures.

In a complete semiconductor manufacturing workflow, a user could:
1. Model polysilicon deposition (PolySim)
2. Simulate Cz silicon crystal growth (CGSim)
3. Model epitaxial layer deposition (CVDSim3D / VR)
4. Simulate device electrical characteristics (SiLENSe, FETIS, etc.)

This vertical integration of simulation tools across the manufacturing chain is a significant differentiator for STR's portfolio as a whole.

---

## 17. Strengths, Limitations, and Open Questions

### 17.1 Strengths

**Physical completeness at the process level.** CGSim covers all physical phenomena that matter in industrial crystal growth — global heat transfer including semi-transparent radiation, 3D turbulent MHD melt flow, species transport, defect dynamics, thermoelastic stresses — within a single integrated package, without requiring the user to couple multiple third-party codes.

**Validated against industrial production.** Documented collaboration with Siltronic AG for 300 mm silicon, independent Japanese patent citations for SiC TSSG, and published validation data for multiple materials give confidence in the quality of predictions.

**Broad material portfolio.** No competing commercial tool covers as many crystal growth techniques and material systems within a single software package.

**Automation and ease of use.** The auto-grid generator, AutoCAD import, and serial computation manager make CGSim accessible to crystal growth engineers who are not CFD specialists.

**Active development.** The cadence of releases (26.1 in December 2025, 26.2 in May 2026) demonstrates that STR continues to invest in the code.

**3D MHD capability.** The 3D unsteady LES/quasi-DNS solver with magnetic field for 300–400 mm silicon Cz growth is technically ahead of what is available in CrysMAS or FEMAG.

### 17.2 Limitations and Caveats

**Closed-source commercial software.** CGSim is not open-source, which limits the ability of users to inspect, modify, or extend the physical models. Academic users who need highly specialised models (e.g., novel alloy chemistries, custom defect reactions) may need to request custom versions or use in-house codes.

**2D default for global heat transfer.** The Basic CGSim core is 2D axisymmetric, relying on effective thermal conductivity models to approximate convective heat transfer in the melt. While the Flow Module adds genuine 3D turbulence, running a full 3D unsteady simulation across a complete growth cycle (which can last many hours) remains computationally expensive and is not routinely done.

**Computational cost of full 3D transient MHD.** Although parallelised, the most accurate 3D LES simulations with magnetic fields for large-diameter silicon remain computationally intensive. This limits the practical depth of parametric studies at full 3D fidelity.

**Licensing model not publicly disclosed.** STR does not publish pricing or licensing terms on its website. Academic access and commercial licensing conditions are not transparent, which can be a barrier for smaller users or cost-sensitive academic groups.

**Limited information on uncertainty quantification.** Published applications generally present point estimates of computed quantities. Systematic uncertainty quantification (sensitivity to material property uncertainties, numerical discretisation errors) is not prominently featured in public documentation.

**Emerging materials still maturing.** While coverage of Ga₂O₃ and GaN solution growth has been added in recent versions, these models are newer and have had less validation than the silicon and GaAs models.

### 17.3 Open Questions and Emerging Directions

The following areas represent natural directions for CGSim's continued development, based on trends in the semiconductor substrate market:

- **Machine learning integration:** Surrogate modelling or ML-assisted process optimisation on top of CGSim simulation databases, enabling faster design space exploration.
- **Coupled 3D stress–flow–defect simulations:** Currently, thermoelastic stress and 3D MHD flow are often run in separate passes. Tighter coupling would improve accuracy for orientation-dependent defect predictions in large-diameter crystals.
- **Extended Ga₂O₃ modelling:** β-Ga₂O₃ is a leading candidate for next-generation ultra-wide-bandgap power devices; its Czochralski growth presents specific challenges (incongruent melting, faceted growth, spiral growth) that may require additional model refinement.
- **GaN ammonothermal growth:** While Ga-Na-Li solution growth is supported, the higher-pressure ammonothermal (acidic or basic ammonia mineraliser) process for bulk GaN is a distinct technique that could benefit from targeted modelling.
- **Integration with process control:** Real-time or near-real-time use of CGSim results as a model-predictive control tool for industrial pullers, potentially closing the loop between simulation and furnace automation.
- **Continuous Czochralski deeper modelling:** As CCz gains importance in photovoltaic silicon production, further refinement of the granular-feeding thermal models and the resistivity control algorithms will be commercially valuable.

---

## 18. Summary and Conclusions

CGSim is the leading commercially available software package for numerical simulation of bulk single-crystal and multicrystalline growth from the melt and from solution. Developed by STR Group Ltd. over a period spanning at least two decades, it has reached a high degree of physical completeness and numerical maturity, and is actively used by more than 170 industrial and academic organisations worldwide.

Its modular architecture allows a spectrum of simulation fidelity from inexpensive 2D steady-state global heat-transfer sweeps (for rapid parametric studies of furnace geometry and process recipes) to full 3D unsteady LES/MHD simulations of turbulent melt flow with magnetic fields (for the most demanding large-diameter silicon applications). The Defects module provides a quantitatively grounded treatment of intrinsic point-defect dynamics in silicon — the V/G framework and its extensions — while the 3D thermoelastic stress solver (anisotropic, as of CGSim 26.2) addresses the mechanical quality of both silicon and compound semiconductor crystals.

The most recent releases (CGSim 26.1, December 2025; CGSim 26.2, May 2026) demonstrate that STR continues to push the boundary of the software's capabilities, with notable additions in gas-phase doping chemistry, Continuous Czochralski support, twin-crystal formation criteria for III-V compounds, and orientation-dependent 3D anisotropic stress computation.

Against a backdrop of strong demand for high-quality substrates in power electronics (SiC, Ga₂O₃), photonics (GaAs, InP, GaN), and mainstream silicon (300 mm electronic-grade, solar-grade PV), CGSim occupies an essential position in the design toolchain of crystal growth manufacturing. Its breadth of material coverage and depth of physical modelling, combined with a purpose-built user interface that does not demand CFD expertise from the crystal grower, make it the reference tool for the crystal growth simulation community.

---

## 19. References and Further Reading

### STR Group Primary Sources
- STR Group CGSim product page: https://str-soft.com/software/cgsim/
- Flow Module page: https://str-soft.com/software/cgsim/flow-module/
- CGSim 26.1 release announcement: https://str-soft.com/2025/12/16/cgsim-26-1-released/
- CGSim 26.2 update announcement: https://str-soft.com/2026/05/15/cgsim-update-26-2/
- Crystal Growth application pages: https://str-soft.com/crystal-growth/
- STR Group LinkedIn: https://www.linkedin.com/company/str-group-semiconductor-technology-research/

### Key Published Validations and Applications
- Kalaev, V.V. et al., "Calculation of bulk defects in CZ Si growth: impact of melt turbulent fluctuations," [*J. Crystal Growth*, 250/1-2 (2003) pp. 203-208](https://doi.org/10.1016/S0022-0248(02)02240-6).
- Lukanin, D.P. et al., "Advances in the simulation of heat transfer and prediction of the melt-crystal interface shape in silicon CZ growth," [*J. Crystal Growth*, 266/1-3 (2004) pp. 20-27](https://doi.org/10.1016/j.jcrysgro.2004.02.025).
- Wu, B. et al., "Bulk multicrystalline silicon growth for photovoltaic (PV) application", [*J. Crystal Growth*, 310/7-9 (2008) pp. 2178-2184](https://doi.org/10.1016/j.jcrysgro.2007.11.194).
- Teng, Y.Y. et al., "The carbon distribution in multicrystalline silicon ingots grown using the directional solidification process", [*J. Crystal Growth*, 312/8 (2010) pp. 1282-1290](https://doi.org/10.1016/j.jcrysgro.2009.11.020).
- Li, Z. and Smirnov, A., "Application of computer modeling to pulling rate and productivity of Czochralski pullers in PV Si crystal growth," [*J. Crystal Growth*, 611 (2023) 127178](https://doi.org/10.1016/j.jcrysgro.2023.127178).

### Competitive Context
- Kirpo, M. et al., "Global simulation of the Czochralski silicon crystal growth in ANSYS FLUENT," [*J. Crystal Growth* 371 (2013) pp. 60-69](https://doi.org/10.1016/j.jcrysgro.2013.02.005). [Comparison of CGSim, CrysMAS/STHAMAS, FEMAG-CZ]
- Rost, H.-J. et al., "Validation, verification, and benchmarking of crystal growth simulations," [*J. Crystal Growth* 474 (2016) pp. 171-177](https://doi.org/10.1016/j.jcrysgro.2016.12.091).
- Plötner, M. et al., "Development and validation of a thermal simulation for the Czochralski crystal growth process using model experiments," [*J. Crystal Growth* 593 (2022) 126750](https://doi.org/10.1016/j.jcrysgro.2022.126750). [References CGSim, CrysMAS, FEMAG]

### Patent Citations (CGSim as Simulation Tool)
- US Patent 9,822,468 (SiC single crystal production; CGSim STR Japan Ver. 14.1 cited for ΔT simulation in TSSG)
- US Patent 10,094,044 (SiC single crystal, solution growth; CGSim STR Japan Ver. 14.1)



---

*End of Report*

*Prepared on the basis of publicly available information from STR Group's official website, peer-reviewed publications, patent literature, and conference proceedings, current as of June 2026.*

---

> [!NOTE]
> 
> Generated by Claude.ai
>
> Model: Sonet 4.6
>
> Prompt: Prepare a thorough and detailed technical report on the CGSim software from the STR Group.
> The technical report must comprehensively address the current state of affairs.
> It must be exhaustive and wide-ranging.
> Show output in Markdown format.
