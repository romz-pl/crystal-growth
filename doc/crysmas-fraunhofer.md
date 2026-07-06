# CrysMAS from Fraunhofer Institute for Integrated Systems and Device Technology

**Software developed by:** Crystal Growth Laboratory (CGL), Fraunhofer Institute for Integrated Systems and Device Technology (IISB), Erlangen, Germany  
**Report date:** June 2026  
**Classification:** Technical Overview — Numerical Simulation Software for Crystal Growth

---

## Table of Contents

1. [Introduction and Background](#1-introduction-and-background)
2. [Institutional Context: Fraunhofer IISB and the Crystal Growth Laboratory](#2-institutional-context)
3. [Historical Development: From STHAMAS and CrysVUn to CrysMAS](#3-historical-development)
4. [Software Architecture and User Interface](#4-software-architecture-and-user-interface)
5. [Numerical Foundations](#5-numerical-foundations)
6. [Physical Models and Simulation Capabilities](#6-physical-models-and-simulation-capabilities)
   - 6.1 [Heat Transfer — Conduction](#61-heat-transfer--conduction)
   - 6.2 [Radiative Heat Transfer: View Factors and the Enclosure Method](#62-radiative-heat-transfer-view-factors-and-the-enclosure-method)
   - 6.3 [Radiative Heat Transfer: Ray Tracing Method](#63-radiative-heat-transfer-ray-tracing-method)
   - 6.4 [Fluid Flow and Melt Convection](#64-fluid-flow-and-melt-convection)
   - 6.5 [Turbulence Modelling](#65-turbulence-modelling)
   - 6.6 [Solid–Liquid Interface and Phase Change](#66-solidliquid-interface-and-phase-change)
   - 6.7 [Electromagnetic Field Simulation and Magnetohydrodynamics (MHD)](#67-electromagnetic-field-simulation-and-magnetohydrodynamics-mhd)
   - 6.8 [Inductive Heating](#68-inductive-heating)
   - 6.9 [Species Transport and Chemical Reactions](#69-species-transport-and-chemical-reactions)
   - 6.10 [Thermoelastic Stress Analysis](#610-thermoelastic-stress-analysis)
   - 6.11 [Inverse Simulation — Heater Power Optimisation](#611-inverse-simulation--heater-power-optimisation)
   - 6.12 [Time-Dependent and Moving-Region Simulations](#612-time-dependent-and-moving-region-simulations)
7. [Meshing Strategy](#7-meshing-strategy)
8. [Solver Technology and Convergence](#8-solver-technology-and-convergence)
9. [Growth Process Coverage](#9-growth-process-coverage)
10. [Material Systems Supported](#10-material-systems-supported)
11. [Post-Processing and Visualisation](#11-post-processing-and-visualisation)
12. [Characteristic Numbers Module](#12-characteristic-numbers-module)
13. [Batch Mode and Automation](#13-batch-mode-and-automation)
14. [Software Ecosystem and Integration with External Tools](#14-software-ecosystem-and-integration-with-external-tools)
15. [Licensing, Distribution, and Documentation](#15-licensing-distribution-and-documentation)
16. [Validation and Benchmarking](#16-validation-and-benchmarking)
17. [Representative Applications from the Literature](#17-representative-applications-from-the-literature)
18. [Competitive Landscape](#18-competitive-landscape)
19. [Strengths and Limitations](#19-strengths-and-limitations)
20. [Current Status and Outlook (as of 2026)](#20-current-status-and-outlook-as-of-2026)
21. [Summary](#21-summary)
22. [References and Further Reading](#22-references-and-further-reading)

---

## 1. Introduction and Background

CrysMAS is a purpose-built, commercially licensed numerical simulation package for modelling the global heat and mass transport phenomena that occur inside high-temperature crystal growth furnaces. It is developed and maintained by the Department of Materials (formerly the Department of Crystal Growth, and before that the Crystal Growth Laboratory, CGL) at the Fraunhofer Institute for Integrated Systems and Device Technology (IISB), located in Erlangen, Bavaria, Germany.

The primary mission of CrysMAS is to give crystal growers, furnace designers, and process engineers a quantitative, physics-based picture of what happens inside a growth furnace under a prescribed set-point schedule — information that is otherwise largely inaccessible through in-situ measurement at the extreme temperatures (often 1000–2000 °C) involved. Specifically, CrysMAS targets the coupled prediction of:

- Global temperature distributions throughout the entire furnace assembly (insulation, heaters, susceptors, crucibles, melt charge, and growing crystal);
- Thermal radiation exchange between furnace surfaces and, where relevant, within semi-transparent solid or melt regions;
- Natural and forced convection in the melt and in surrounding process gases;
- The location and shape of the solid–liquid interface at which crystallisation occurs;
- Electromagnetic Lorentz forces induced by applied magnetic fields and their effect on melt flow;
- Dopant and impurity species distributions (segregation and transport);
- Thermoelastic stress fields inside the growing crystal;
- Optimal heater power schedules derived by inverse modelling against prescribed temperature targets.

CrysMAS is primarily a two-dimensional (2D axisymmetric) code, with 3D extensions available for specific electromagnetic and flow calculations. This focus on 2D global simulation reflects the practical reality that comprehensive furnace-scale models in 3D remain computationally demanding for routine industrial use, while the axisymmetric approximation is well suited to the majority of industrial bulk crystal growth equipment, which features rotational or near-rotational symmetry.

---

## 2. Institutional Context

Fraunhofer IISB, founded in 1985 under director Heiner Ryssel and headquartered at Schottkystrasse 10, 91058 Erlangen, is one of the institutes within the Fraunhofer-Gesellschaft, Germany's largest applied-research organisation. IISB specialises in applied research on semiconductor technologies, with two major business areas: Power Electronic Systems, and Semiconductors. Within the semiconductor strand, the institute maintains a comprehensive capability spanning materials science through device processing to module integration.

The crystal growth activities that spawned CrysMAS originate in the Crystal Growth Laboratory (CGL), an independent research unit established at the University of Erlangen by Georg Müller in 1974. In 1996, a working group under Müller was established at Fraunhofer IISB; by 1999 this had become a full department. Since 2004 the department has been led by Dr.-Ing. Jochen Friedrich, a former PhD student of Müller. From 2005, activities expanded via a branch laboratory in Freiberg (Saxony) — the Technology Centre Semiconductor Materials (THM). In 2014, the department was renamed from "Crystal Growth" to "Materials" to reflect its broadened remit, which now encompasses GaN, AlN, SiC, and other wide-bandgap compound semiconductors as well as oxides, halides, and II-VI compounds.

The IISB Equipment Simulation team currently employs CrysMAS in conjunction with OpenFOAM and ANSYS (Fluent/CFX) on an in-house high-performance computing (HPC) cluster, applying these tools to processes including Czochralski (Cz), Vertical Gradient Freeze (VGF), Directional Solidification (DS), Floating Zone (FZ), Edge-defined Film-fed Growth (EFG), Liquid Phase Epitaxy (LPE), Travelling Heater Method (THM), Chemical Vapour Deposition (CVD), Physical Vapour Transport (PVT), Hydride Vapour Phase Epitaxy (HVPE), and wafer annealing, across materials systems spanning Si, Ge, GaAs, InP, GaN, AlN, SiC, CdZnTe, halides, and oxides.

---

## 3. Historical Development: From STHAMAS and CrysVUn to CrysMAS

### 3.1 Early Codes: STHAMAS and CrysVUn++

The intellectual lineage of CrysMAS traces back to two predecessor codes developed at CGL:

**STHAMAS** (Simulation of THermal processes in crystal growth Apparatus for MAterial Scientists) was designed for global thermal simulation of Czochralski growth furnaces. It modelled heat conduction and radiative exchange within the furnace enclosure using finite volume methods on structured grids. A 3D variant, STHAMAS 3D, was subsequently developed.

**CrysVUn++** (Crystal growth — Vertical Unidirectional growth) was oriented toward directional solidification processes such as VGF and Bridgman growth. The code supported non-linear anisotropic heat conduction, enclosure radiation, thermoelastic stress calculation, and inverse modelling for heater control — essentially the feature set that characterises CrysMAS today. Both packages were developed through the PhD work and contributions of Thomas Jung, Hans-Jörg Leister, Jakob Fainberg, Matthias Kurz, Michael Metzger, Marc Hainke, and Johannes Dagner, with important collaboration from Daniel Vizman, Artur Pusztai, and Gheorghe Ardelean of the University of Timișoara.

### 3.2 Merger into CrysMAS

CrysMAS emerged as the unified successor that merged the functionality of STHAMAS and CrysVUn into a single, integrated platform addressing both Czochralski and directional solidification configurations, as well as EFG, FZ, and other techniques. The version number documented in the publicly available online manual is **4.3.21**, indicating several years of active evolution. The manual was initially prepared with financial support from ESA/ESTEC under contract No. 16462/02/NL/JS, reflecting early use in the microgravity crystal growth research community.

The name change from the earlier two-package offering to the unified CrysMAS also coincided with the extension of the code's physics scope — most importantly the inclusion of full MHD modelling for magnetic field effects, turbulence modelling on unstructured meshes, ray tracing radiation, and chemical species transport.

By 2007, IISB was licensing three simulation tools — CrysVUn, STHAMAS, and STHAMAS 3D — and the combined CrysMAS package. All have since been licensed to companies and research institutes worldwide.

---

## 4. Software Architecture and User Interface

CrysMAS runs natively on **Linux** and **Windows** environments. The user interacts through a graphical interface that integrates four distinct operating modes into one application:

### 4.1 Geometry Mode

The geometry mode provides a 2D CAD-like drawing environment. Users construct the cross-sectional geometry of their furnace by placing and connecting points to form lines, which bound regions. Tools include:

- Zooming and scrolling navigation.
- Drawing, selecting, moving, and copying points and lines.
- Merging, splitting, and intersecting geometric elements.
- Rotating, mirroring, flipping, and scaling the drawing.
- Import of external CAD geometry in DXF format.
- Symmetry settings for axisymmetric models.
- Block-based organisation for structured geometry editing.

### 4.2 Materials Mode

In this mode the user assigns material properties to the geometric regions defined in geometry mode. A material database is maintained separately and can be configured, extended, and updated. Materials carry:

- General properties (density, melting temperature, latent heat).
- Thermal properties (thermal conductivity — isotropic or anisotropic, specific heat).
- Optical properties (spectral emissivity, absorptivity, refractive index, multi-band parameters).
- Fluid properties (dynamic viscosity, thermal expansion coefficient).
- Species transport coefficients (diffusivities, reaction parameters).
- Mechanical properties (Young's modulus, Poisson's ratio, thermal expansion coefficient).

### 4.3 Simulation Mode (Settings)

The settings sub-mode is where the numerical and physical setup is assembled:

- Unstructured and structured mesh generation and adjustment.
- Assignment of boundary conditions (temperature, velocity, pressure, turbulence, species, vector potential).
- Definition of heaters (electric resistive or inductive) and their spatial distribution.
- Definition of control points for inverse simulation.
- Definition of moving regions (e.g., the crystal or the sample cartridge assembly, SCA).
- Configuration of shaped anisotropy (for anisotropic thermal conductivity).
- Species and chemical reaction definition.
- Physical phenomena selection (which equations are active).
- Initial value assignment.

### 4.4 Simulation Mode (Computation)

The computation sub-mode controls the solver:

- Time model selection (pseudo-stationary or full transient).
- Process parameters specific to Czochralski (crystal rotation, crucible rotation, pull velocity) or magnetic field configurations (rotating, alternating, travelling, stationary).
- Numerical parameters (relaxation factors, iteration counts, convergence criteria).
- Radiation parameters (view factor quality, ray tracing settings).
- Convection parameters (turbulence model selection, mesh settings for convection on structured mesh).
- Solver selection.
- Start, stop, and monitoring of the computation.
- Parallel execution (multi-process support).

### 4.5 Visualisation and Post-Processing Mode

Scalar field visualisation, isoline extraction, profile monitoring and writing, export of data, interface shape output, and total heat flux diagnostics are all accessible from within this mode. The entire workflow — from geometry drawing to results inspection — is thus contained within a single application.

---

## 5. Numerical Foundations

### 5.1 Finite Volume Method (FVM)

CrysMAS is fundamentally a **finite volume code**. It solves the governing conservation equations for energy, momentum, species concentration, and electromagnetic vector potential by integrating these equations over discrete control volumes and enforcing conservation in a cell-wise sense. This approach is well suited to complex geometries typical of industrial furnace assemblies and is robust for strongly coupled nonlinear problems.

### 5.2 Dual Mesh Strategy

CrysMAS employs a characteristic **dual-mesh architecture**:

**Unstructured mesh:** An unstructured triangular grid covers every computational region. This mesh is generated first and is the primary grid for heat conduction, radiation (surface-to-surface view factors), and unstructured-mesh convection. The unstructured grid accommodates arbitrary region shapes without geometric restrictions. Mesh density is controlled by user-specified edge lengths on lines and inside regions, modulated by a "fit slope" parameter that governs how rapidly the element size transitions from a fine boundary layer to a coarser interior. A "respect edge length" function allows forcing larger element sizes along specific lines, which is exploited both to reduce computational cost in low-gradient zones and to limit the number of radiative facets in the view factor calculation (since the cost of the view factor matrix scales quadratically with the number of radiating edges).

**Structured mesh:** A body-fitted, structured mesh is created as a second layer overlapping the unstructured mesh in user-designated regions. This mesh is used for the convection solver (melt flow, gas flow), where structured grids are more effective for boundary-layer-sensitive convection problems. The two meshes communicate by interpolation.

### 5.3 Solution Algorithm

CrysMAS employs a **quasi-Newton iterative method** (Newton-like nonlinear iterations with an approximate Jacobian update strategy) to converge the coupled nonlinear system. The outer loop iterates over the nonlinear residual; inner linear-system solves use an appropriate linear solver selected by the user. This choice of a quasi-Newton approach, as opposed to a Picard or simple fixed-point iteration, provides faster convergence rates in the proximity of a solution — particularly important for the strongly coupled, highly nonlinear problem of high-temperature furnace simulation where radiation and conduction are simultaneously active.

For time-dependent problems, a **fully implicit time model** is available, providing unconditional stability for stiff problems where very different physical time scales coexist (e.g., fast thermal diffusion and slow growth-rate evolution).

---

## 6. Physical Models and Simulation Capabilities

### 6.1 Heat Transfer — Conduction

CrysMAS solves the energy conservation equation in the solid and fluid regions of the furnace, accounting for:

- **Non-linear thermal conductivity:** Temperature-dependent conductivities are supported, critical at the extreme temperatures (800–2200 °C) typical of semiconductor and oxide crystal growth.
- **Anisotropic conductivity:** For materials with directional thermal properties (e.g., graphite, SiC, certain crystal orientations), shaped anisotropy can be configured.
- **Latent heat release:** At the solid–liquid interface, the latent heat of fusion is incorporated as a source term or through an enthalpy-based formulation, ensuring energy conservation during solidification.
- **Conjugate heat transfer:** Continuity of temperature and heat flux is enforced at all material interfaces, enabling the true coupled simulation of heat flowing through the multi-component furnace assembly.

### 6.2 Radiative Heat Transfer: View Factors and the Enclosure Method

Radiation is a dominant heat transfer mechanism in high-temperature crystal growth furnaces. CrysMAS's primary radiation model is based on the **Gebhart view factor method with an enclosure formulation**:

- Every opaque surface in the furnace is treated as a diffuse emitter and reflector characterised by its emissivity.
- View factors $F_{ij}$ describe the geometric fraction of radiation leaving surface $i$ that is intercepted by surface $j$. CrysMAS computes these view factors including hidden-surface detection (only directly visible surfaces exchange radiation directly).
- The Gebhart factors $B_{ij}$ account for multiple reflections, describing the fraction of emission from surface $i$ that is ultimately absorbed by surface $j$ — the radiation network is thus fully coupled even for geometries with complex reflection paths.
- The radiative exchange matrix is assembled as a dense linear system (hence the quadratic scaling with the number of radiating tiles that makes mesh coarsening along radiating surfaces desirable for computational efficiency).
- The view factor quality can be tested within the software to verify numerical consistency.

For **semi-transparent materials** (e.g., sapphire, CaF₂, certain fluoride and oxide crystals, and semiconductor melts at near-infrared wavelengths), CrysMAS supports volume radiation within the participating medium. The optical properties are characterised using an **n-band spectral model**, in which the spectrum is divided into several bands, each with its own absorption/emission characteristics. This allows the code to represent the transition from optically thin (transparent) to optically thick (opaque) behaviour across the spectrum, as occurs in many oxide and fluoride crystals.

### 6.3 Radiative Heat Transfer: Ray Tracing Method

In addition to the view-factor enclosure approach, CrysMAS provides a **ray tracing radiation module** as an alternative or complementary method. Ray tracing tracks individual rays emitted from surfaces or volume elements, following their paths through reflections, refractions, and absorption events. This approach:

- Is physically rigorous for geometries with specular reflectors or complex refractive interfaces.
- Captures volumetric absorption within semi-transparent crystals without the need to pre-define a multi-band model.
- Has a higher computational cost per degree of freedom than the view factor method but is less sensitive to geometric complexity.
- Can be run independently or in combination with the enclosure model in a hybrid configuration.

Ray tracing in CrysMAS was documented and made available via tutorials, and the method is particularly valued for modelling radiation inside sapphire, fluoride crystals, and other infrared-transparent materials.

### 6.4 Fluid Flow and Melt Convection

CrysMAS solves the **Navier–Stokes equations** (with the Boussinesq approximation for buoyancy-driven flows) coupled to the energy equation to model convection in the melt and in the surrounding process gas. The governing equations are:

- **Continuity equation** (mass conservation).
- **Momentum equations** (Navier–Stokes, including Coriolis terms when crystal or crucible rotation is present in Czochralski configurations).
- **Energy equation** (advection-diffusion of temperature, coupled to the conduction solution in the solid regions).

The melt convection solver operates on the structured mesh. Boundary conditions for velocity include no-slip at solid walls, symmetry conditions on the axis, and rotating-wall conditions for the crystal–melt interface and crucible bottom/wall (Czochralski setup). Pressure boundary conditions are also configurable.

For Czochralski setups, the software includes dedicated **process parameters** for crystal rotation rate (rpm), crucible rotation rate (rpm), and crystal pull velocity, which feed into the appropriate rotating boundary conditions and centrifugal source terms.

Quasi-stationary (steady-state) convection computations allow prediction of the steady melt flow pattern for a given thermal and geometric configuration. Time-dependent convection simulations resolve the transient evolution of flow, including oscillatory or turbulent flow regimes.

### 6.5 Turbulence Modelling

For configurations where the Reynolds number or the Rayleigh number is sufficiently high to render the flow turbulent — typical of large-diameter silicon Czochralski growth (300 mm wafers) and large industrial VGF furnaces — CrysMAS provides turbulence models including:

- Standard turbulence models applicable on the unstructured mesh.
- **Turbulent gas convection on unstructured mesh:** A dedicated capability for modelling turbulent gas flow (e.g., argon cover gas in a Czochralski puller) with appropriate turbulence models.
- **Turbulent convection on structured mesh** for melt flow.

The turbulence model settings (e.g., turbulent viscosity, turbulent Prandtl number, turbulent Schmidt number) are user-configurable in the numerical parameters menu.

### 6.6 Solid–Liquid Interface and Phase Change

A key output of any crystal growth simulation is the shape and position of the **solid–liquid interface** — the melt–crystal boundary at which solidification (or melting) occurs. In CrysMAS:

- The interface is determined as the **melting-point isotherm** of the material, found by iterating the temperature solution until the isotherm coincides with the assigned phase boundary location.
- Latent heat is released locally at the interface and is included in the energy balance.
- The interface shape affects both the stress state of the growing crystal and the segregation of dopants/impurities (via the local growth rate normal to the interface).
- For pseudo-stationary simulations, the interface is tracked in a quasi-Newton framework alongside the thermal field. For time-dependent simulations, moving-region capabilities allow the interface to advance as the crystal grows.

### 6.7 Electromagnetic Field Simulation and Magnetohydrodynamics (MHD)

CrysMAS includes a comprehensive electromagnetic simulation capability, most prominently applied in the context of the KRISTMAG® heater-magnet module (HMM) technology developed at Fraunhofer IISB. The MHD models supported include:

**Rotating Magnetic Field (RMF):** An alternating magnetic field rotating in the horizontal plane, which drives an azimuthal Lorentz force and consequently a toroidal melt flow that can either supplement or oppose buoyancy-driven natural convection. CrysMAS computes the induced Lorentz force density and incorporates it as a body force in the Navier–Stokes equations.

**Travelling Magnetic Field (TMF):** A magnetic field wave propagating axially along the furnace axis, generated by phasing alternating current through coils arranged at different vertical positions. CrysMAS includes a dedicated TMF computation module that:
- Solves the electromagnetic induction problem for the vector potential distribution (MHD1 and MHD2 models for axial and CUSP field geometries respectively).
- Computes the resulting Lorentz force density as a function of current amplitude, frequency, and phase shift between coil segments.
- The AC amplitude, frequency, and phase shift can be parametrically varied and optimised to achieve a desired melt flow pattern (e.g., a nearly flat or slightly convex solid–liquid interface).
- Validated experimentally by comparing computed Lorentz forces against those measured using dummy weights in model experiments.

The 3D CrysMAS code has been used specifically for TMF optimisation during Ge VGF growth under the KRISTMAG® HMM, and the results were validated by striation analysis on as-grown crystals.

**Stationary Magnetic Field (SMF):** Static (DC) magnetic fields (axial, transverse, or CUSP configurations) that damp melt flow through Lorentz braking. CrysMAS can compute these fields and their damping effects on convection for both MHD1 (simplified) and MHD2 (full vector potential) models.

**Alternating Magnetic Field (AMF):** Used for contactless inductive stirring and heating, AMF can also be addressed within CrysMAS's electromagnetic framework.

The TMF boundary condition specification, including the definition of inductors and their electrical parameters, is accessible through a dedicated dialog in the computation menu.

### 6.8 Inductive Heating

CrysMAS supports the modelling of **inductive (RF) heating**, which is used in floating zone (FZ) silicon growth, some SiC sublimation furnaces, and other configurations. The inductive heating module:

- Solves Maxwell's equations in the quasi-static (eddy current) approximation for the distribution of induced currents in electrically conducting furnace components.
- Computes the resulting Joule heating distribution as a volumetric heat source term.
- Supports both **fixed power** and **controlled power** inductive heating configurations.
- Physical background, prerequisites, and step-by-step tutorial tasks are documented in the CrysMAS manual.

### 6.9 Species Transport and Chemical Reactions

Beyond the thermal and fluid physics, CrysMAS can model **species (dopant/impurity) transport**:

- **Concentration equation:** A convection–diffusion equation is solved for each species of interest, with user-defined diffusivities in each phase.
- **Segregation:** The discontinuity of concentration at the solid–liquid interface, governed by the equilibrium segregation coefficient, is enforced as an interface condition.
- **Species boundary conditions:** Prescribed concentration, flux, or zero-flux conditions can be assigned on domain boundaries.
- **Supersaturation:** A dedicated mode computes the local supersaturation field, of interest for nucleation modelling and defect formation.
- **Chemical reactions:** A multi-species chemical reaction model is available, supporting the definition of gas-phase and surface reaction networks. This capability is of particular relevance for CVD and HVPE epitaxy simulations, and for modelling reactive atmospheres (e.g., CO gas transport in silicon Czochralski growth, oxygen/nitrogen in semiconductor melts).

The chemical model hierarchy allows progressive inclusion of complexity, from simple transport of a single inert dopant to multi-species reactive gas-phase systems with surface deposition reactions.

### 6.10 Thermoelastic Stress Analysis

The temperature non-uniformity inside a growing crystal, resulting from the imposed thermal gradients needed to drive growth, generates **thermoelastic stress** that, if it exceeds the critical resolved shear stress (CRSS) of the material, nucleates and multiplies dislocations. CrysMAS includes a thermoelastic stress solver that:

- Takes the computed temperature field in the crystal as input.
- Solves the static thermoelastic equilibrium equations (Lamé equations with a thermal body-force term proportional to the temperature gradient).
- Returns the full stress tensor distribution — normal stresses, shear stresses, von Mises equivalent stress, and principal stresses.
- Supports anisotropic elastic constants (relevant for crystals with cubic or hexagonal symmetry, such as GaAs, InP, SiC, or sapphire).
- The results provide the crystal grower with an estimate of where and by how much the stress exceeds the CRSS, informing modifications to the temperature profile or interface shape to reduce dislocation density (EPD).
- Stress computation is initiated through the "Computing Thermoelastic Stress" module in the computation menu.

### 6.11 Inverse Simulation — Heater Power Optimisation

One of CrysMAS's most industrially important features is its **inverse modelling (inverse simulation) capability**. In conventional (forward) simulation, heater powers are prescribed and the resulting temperature distribution is computed. In inverse simulation, the desired temperature distribution (e.g., the location and shape of the solid–liquid interface, or target temperatures at control points measured by thermocouples) is prescribed, and the heater powers needed to achieve those conditions become the unknowns:

- **Control points** are defined at locations where target temperatures are specified (typically corresponding to thermocouple positions in the real furnace).
- An arbitrary number of heaters, each with independently adjustable power, can be included.
- The algorithm iteratively adjusts heater powers to minimise the discrepancy between computed and target temperatures at all control points simultaneously.
- The inverse procedure is implemented within the same quasi-Newton framework as the forward solver.
- Practically, this allows crystal growers to design optimal heater profiles for flat interface shapes, low thermal gradients in the crystal, and reduced dislocation densities — then validate these designs experimentally against a pre-optimised set-point schedule.
- Inverse simulation for visualisation of results includes dedicated analysis tools (profile writing, isoline output, total heat flux calculation).

### 6.12 Time-Dependent and Moving-Region Simulations

Pseudo-stationary simulations assume that the thermal and flow fields reach a true steady state at each point along the growth trajectory, which is valid when the growth timescale far exceeds the thermal equilibration time. When this assumption breaks down — for fast transients, ramping, or processes where the growth timescale and the thermal diffusion timescale are comparable — CrysMAS provides:

- **Full transient (time-dependent) simulation** with a fully implicit time integration scheme for both the temperature field and, optionally, the convection field.
- **Moving region support:** Geometric regions (e.g., the crystal as it grows, or the sample cartridge assembly in a Bridgman furnace) can be defined to translate or change shape over time, allowing the simulation to follow the evolving geometry throughout a complete growth run.
- Time-dependent ramp parameters for heater power schedules can be specified, enabling simulation of the entire growth process from charge melting through crystal growth to cool-down.
- Monitoring files record the time evolution of temperatures at specified monitor points, useful for comparison against thermocouple measurements.

---

## 7. Meshing Strategy

The meshing architecture of CrysMAS reflects a deliberate balance between flexibility (for complex geometries) and efficiency (for convection on structured grids):

**Unstructured mesh generation** is performed automatically from the geometric model. Key parameters:
- **Edge length** (for lines and regions): Controls the target element size. Smaller values yield finer meshes and higher resolution at the cost of computational time.
- **Fit slope:** Controls how rapidly the mesh transitions from fine (near boundaries) to coarse (in the interior). Values around 0.3 give a natural refinement gradient; values as low as 0.1 are used when the default produces triangles with very small angles (poor aspect ratios) causing numerical issues.
- **Respect edge length function:** Forces the mesh to honour a specified edge length along designated lines, preventing unnecessary refinement and directly reducing the number of radiating tiles and hence the cost of the view factor computation.

**Structured mesh generation** is automated from the unstructured mesh. For complex geometries, a block-structured approach is available, including manual mesh improvement tools and a tutorial on structured mesh generation in complex regions.

The manual emphasises that **mesh quality is critical to solution accuracy**, and recommends iterating on mesh parameters to improve results for specific furnace configurations.

---

## 8. Solver Technology and Convergence

The solver technology in CrysMAS includes:

- **Multiple solver options** selectable by the user for the linear subsystems arising from the discretised equations.
- **Quasi-Newton outer iteration** for the full nonlinear coupled system.
- **Forward relaxation factors** that can be adjusted per equation to improve convergence stability in poorly conditioned problems (e.g., reducing relaxation when starting from a poor initial guess).
- **Abortion parameters** to define stopping criteria based on residual norms.
- **Solver information display** during computation to monitor convergence in real time.
- **Multi-process execution** (parallel computation) is accessible through the "Number of processes" option, leveraging multi-core workstations for faster throughput.
- **Batch mode operation** (see Section 13) allows unattended parametric studies.

The combination of a robust quasi-Newton method, adjustable relaxation, and the dual-mesh strategy makes CrysMAS competitive in convergence behaviour for the strongly coupled, radiation-dominated problems typical of crystal growth furnaces.

---

## 9. Growth Process Coverage

The official IISB Equipment Simulation page lists the following **growth processes explicitly supported** by CrysMAS within IISB's simulation service:

| Process Code | Full Name |
|---|---|
| Cz | Czochralski |
| VGF | Vertical Gradient Freeze |
| DS | Directional Solidification |
| FZ | Floating Zone |
| EFG | Edge-defined Film-fed Growth |
| LPE | Liquid Phase Epitaxy |
| THM | Travelling Heater Method |
| CVD | Chemical Vapour Deposition |
| PVT | Physical Vapour Transport |
| HVPE | Hydride Vapour Phase Epitaxy |
| Annealing | Wafer / bulk annealing |

The Czochralski setup includes dedicated parameter dialogs for crystal rotation, crucible rotation, pull velocity, and all magnetic field variants. The VGF/Bridgman workflow is the oldest and most mature. EFG growth has been modelled for sapphire ribbon pulling. FZ growth involves the additional complexity of a free melt zone sustained by surface tension, which requires the surface tension / capillary model capabilities. PVT is the primary growth method for SiC bulk crystals and involves vapour-phase transport at high temperatures — a regime in which CrysMAS's radiation and species transport solvers are both active. CVD and HVPE are epitaxial processes for which CrysMAS's gas-flow, species transport, and chemical reaction capabilities are most relevant.

The **micro-pulling-down (μPD) method** for sapphire fibre crystals has also been studied with CrysMAS, with results including identification of dominant Marangoni convection in the melt and the prediction of a convex crystal–melt interface shape.

---

## 10. Material Systems Supported

Based on documented usage at IISB and in the published literature, CrysMAS has been applied to the following material systems:

**Elemental semiconductors:**
- Silicon (Si) — Czochralski, floating zone, directional solidification
- Germanium (Ge) — VGF under travelling magnetic field (KRISTMAG® approach)

**III-V Compound Semiconductors:**
- Gallium arsenide (GaAs) — VGF, LEC, VCz
- Indium phosphide (InP)

**Wide-bandgap semiconductors:**
- Silicon carbide (SiC) — PVT sublimation growth
- Gallium nitride (GaN) — HVPE, high-pressure solution growth
- Aluminium nitride (AlN) — PVT

**II-VI Semiconductors:**
- Cadmium zinc telluride (CdZnTe / CZT) — EDG (electrodynamic gradient freeze), Bridgman; CZT is one of the most extensively published CrysMAS applications

**Oxides:**
- Sapphire (Al₂O₃) — EFG, HEM (Heat Exchanger Method), μPD
- BGO (Bi₄Ge₃O₁₂)

**Halides and Fluorides:**
- Calcium fluoride (CaF₂) — Bridgman–Stockbarger; recent (2024) papers document CrysMAS use for CaF₂–TmF₃ solid solutions with semi-transparent radiation treatment
- Other halide compounds

The material database within CrysMAS can be extended by users to accommodate any material for which thermal, optical, fluid, and mechanical properties are available.

---

## 11. Post-Processing and Visualisation

CrysMAS's built-in post-processing environment provides:

- **Scalar field visualisation** of all computed variables (temperature, velocity components, pressure, turbulence quantities, species concentrations, stress components, electromagnetic quantities) as colour maps on the mesh.
- **Options for scalar field display** (colour scale selection, range clipping, overlays).
- **Grid visualisation** (unstructured and structured mesh display).
- **Isoline writing** — extraction of contour lines for any variable (e.g., the melting isotherm to identify the interface position) and export to files.
- **Monitor/Write Profile** — extraction of 1D profiles along polylines (e.g., axial or radial temperature profiles comparable to thermocouple data).
- **Write Interface** — dedicated export of the solid–liquid interface geometry.
- **Total Heat Flux computation** — integration of heat fluxes across specified surfaces.
- **Crystal data output** — summary of crystal growth parameters.
- **Write Entire File** — full field export for post-processing in third-party tools.
- **Export Data** — structured data output in formats compatible with external analysis or plotting environments.

For three-dimensional computations or for complementary visualisation, results can be exported and processed in tools such as ParaView.

---

## 12. Characteristic Numbers Module

CrysMAS includes an integrated **Characteristic Numbers Dialog** that computes dimensionless numbers relevant to the transport regime in the melt and gas phases:

- **Prandtl number (Pr):** Ratio of momentum to thermal diffusivity; determines the relative thickness of velocity and thermal boundary layers.
- **Rayleigh number (Ra):** Governs the onset and intensity of buoyancy-driven natural convection.
- **Grashof number (Gr):** Ratio of buoyancy to viscous forces.
- **Reynolds number (Re):** Ratio of inertial to viscous forces; relevant for assessing whether flow is laminar or turbulent.
- **Marangoni number (Ma):** Quantifies the thermocapillary (Marangoni) convection driven by surface tension gradients at the free melt surface.
- Other relevant dimensionless groups as defined in the characteristic number definitions within the manual.

This module is of direct scientific value for order-of-magnitude analysis of transport phenomena, assessment of whether the Boussinesq approximation is valid, and identification of the dominant flow mechanism in a given configuration — consistent with the CGL's long tradition of using dimensionless analysis to classify crystal growth configurations.

---

## 13. Batch Mode and Automation

CrysMAS supports **batch (non-interactive) execution** for parametric studies and automated simulation campaigns. Key features:

- A command-line interface allows CrysMAS to be invoked without the GUI, reading problem definitions from saved `.crys` input files and writing outputs to log and monitoring files.
- **Automatic generation of Czochralski geometries** is available, enabling programmatic construction of furnace models for parametric variation (e.g., varying crystal diameter, crucible geometry, or heat shield position) without manual GUI interaction.
- Batch mode is essential when CrysMAS is run on an HPC cluster for large parametric studies or when integrated into a design-of-experiments (DoE) workflow.

---

## 14. Software Ecosystem and Integration with External Tools

CrysMAS is positioned within IISB's broader simulation toolchain as the **primary global furnace heat transfer code**, complemented by:

- **OpenFOAM:** Used for higher-fidelity, fully 3D flow simulations (large-eddy simulation, turbulent pipe flows, gas dynamics in CVD reactors) where CrysMAS's 2D axisymmetric approximation is insufficient.
- **ANSYS (Fluent / CFX):** Applied for 3D conjugate heat transfer, structural analysis, and multi-physics problems beyond CrysMAS's scope, particularly for non-axisymmetric furnace elements or 3D crystal shapes (e.g., nearly square silicon crystals for quasi-mono wafer production).
- **Cats2D (University of Minnesota / Jeffrey Derby group):** A finite-element local model for the melt zone. In several published coupled studies, CrysMAS provides global thermal boundary conditions to Cats2D, which then solves the local melt flow and solute transport problem at higher resolution within the crucible.
- **NAVIER / WIAS-HiTNIHS:** Other specialised codes used in the German crystal growth community that have been coupled or compared with CrysMAS results.
- **ParaView:** Open-source visualisation for exported 3D data.
- **HPC cluster:** IISB operates an in-house computing cluster on which CrysMAS, OpenFOAM, and ANSYS are all deployed. The cluster enables parametric studies that would be impractical on a single workstation.

The pairing of CrysMAS with OpenFOAM and ANSYS reflects the recognition that no single code captures all phenomena at all scales — CrysMAS excels at global furnace-scale thermal modelling (its intended design space), while OpenFOAM and ANSYS address 3D and higher-fidelity scenarios.

---

## 15. Licensing, Distribution, and Documentation

### 15.1 Licensing Model

CrysMAS is a **commercially licensed software** distributed by Fraunhofer IISB. It has been licensed to companies and research institutes worldwide — including major semiconductor manufacturers, crystal growth equipment builders, and university research groups in Europe, North America, and Asia. The licensing is handled directly by Fraunhofer IISB; interested parties contact the institute (primary contact: Dr.-Ing. Jochen Friedrich, Head of Department Materials, phone +49 9131 761–269) to discuss terms.

The software is classified in the literature as a commercial simulation tool alongside its main competitors CGSim (STR Group) and FEMAG (FEMAGSoft S.A.).

### 15.2 Online Manual and Documentation

The **CrysMAS User Manual and Tutorial** is publicly accessible at:

```
https://download.iisb.fraunhofer.de/downloads/Manual/index.html
```

The documented software version is 4.3.21. The manual is comprehensive, covering:
- Geometry construction, materials assignment, and boundary condition setup.
- Mesh generation (unstructured and structured), including guidance on fit slope and edge length parameters.
- All physical phenomena: conduction, radiation (view factors and ray tracing), convection (laminar and turbulent), electromagnetic fields (RMF, TMF, AMF, SMF), inductive heating, species transport, chemical reactions, thermoelastic stress, inverse simulation.
- Process-specific parameter dialogs for Czochralski, VGF, and magnetic field configurations.
- Complete quick-start tutorials covering thermal analysis, inverse simulation, time-dependent simulations, convection, turbulent gas convection, thermoelastic stress, inductive heating, magnetic field computations, concentration transport, and chemical reactions.
- A Frequently Asked Questions (FAQ) appendix addressing general problems, furnace model preparation, and computation performance.
- A bibliography (Appendix D) providing references to the underlying physics and numerical methods.
- Technical appendices on units of measurement, file formats, log files, and keyboard/mouse shortcuts.

The initial version of the documentation was prepared with ESA/ESTEC financial support, and the manual itself was made available online, making it an unusually transparent resource for a commercial code.

---

## 16. Validation and Benchmarking

Validation of CrysMAS has been performed through multiple independent pathways documented in the peer-reviewed literature:

### 16.1 Experimental Validation

- **Model experiments for Czochralski growth** (Enders-Seidlitz et al., 2022): A dedicated model furnace with extensive instrumentation — including 44 thermocouples and an optical interface position detector — was used to validate CrysMAS predictions of the temperature field and crystallisation front position across a range of operating conditions. Steady-state heat transfer and melt convection were benchmarked.

- **Lorentz force validation for TMF (KRISTMAG®):** Lorentz forces computed by CrysMAS for travelling magnetic field configurations were directly compared against measured forces obtained by monitoring the weight response of electrically conducting dummy specimens inserted into the TMF coil assembly. Good agreement between computation and experiment was reported.

- **VGF GaAs interface shape and EPD:** Inverse simulation with CrysVUn++ (predecessor to CrysMAS) was used to design a VGF GaAs growth process. The resulting crystals grown under the computed optimised schedule showed flat phase boundaries and very low etch pit densities (EPD < 100 cm⁻²) throughout the crystal, validating the inverse model predictions against crystal quality metrics.

- **EDG growth of CZT:** CrysMAS thermal models for electrodynamic gradient freeze (EDG) furnaces were validated by comparing computed heater powers against measured values needed to achieve a desired temperature profile in the furnace under calibration conditions (all heaters at 1273 K set point).

### 16.2 Code-to-Code Benchmarking

CrysMAS has been included in comparative benchmarking exercises against other specialist codes:

- The 2016 Validation, Verification, and Benchmarking study (Dadzis et al., *Journal of Crystal Growth*, 2016) explicitly identifies CrysMAS, CGSim, and FEMAG as the three commercially available dedicated crystal growth simulation packages, and discusses the importance of systematic V&V for results from all three.

- A 2013 global Czochralski simulation study (Kirpo, 2013) compared CrysMAS/STHAMAS, CGSim, and FEMAG, concluding that all three codes offer "approximately the same functionality to the end user" for the conjugate heat and mass transport problem in the CZ process, including global temperature distributions, flow structure, interface position, and required heater power — with differences in grid generation, radiation modelling approach, numerical schemes, and turbulence models.

---

## 17. Representative Applications from the Literature

The following examples, drawn from the peer-reviewed literature, illustrate the breadth and depth of CrysMAS usage:

### 17.1 CZT Growth by Electrodynamic Gradient Freeze (EDG)

CrysMAS has been extensively applied to model CZT growth in multi-zone EDG furnaces. Studies by Reed, Derby, and collaborators at the University of Minnesota and Pacific Northwest National Laboratory (PNNL) employed CrysMAS to predict temperature fields, heater power requirements, and crucible material effects (graphite versus PBN) on the solid–liquid interface shape. Results showed that PBN crucibles produce much steeper axial thermal profiles and convex interface shapes compared to graphite, under identical furnace set points. CrysMAS was also used to study ampoule support modifications and their effects on heat flow and interface shape in CZT EDG furnaces.

### 17.2 Sapphire Growth by Heat Exchanger Method (HEM)

Brandon (University of Minnesota / Israel) and Park (Korea Polytechnic University) employed CrysMAS to model heat transfer and melt convection during sapphire growth in a small-scale modified HEM system. Quasi-steady-state computations with a simple conduction model gave qualitatively correct interface predictions; inclusion of internal radiation in the crystal (important for sapphire's semi-transparency in the infrared) and Marangoni convection at the melt surface were found to significantly improve accuracy.

### 17.3 Sapphire Micro-Pulling-Down (μPD)

CrysMAS was used to study the fundamental heat transfer, fluid flow, melt–crystal interface shape, and electromagnetic field distribution in the μPD process for sapphire fibre crystal growth. Results identified Marangoni convection as the dominant melt convection mechanism, buoyancy convection as negligible, and strong gas convection driven by large temperature differences in the surrounding furnace. A hot spot near the top of the crucible was identified, and a ring design modification was proposed to obtain a more uniform temperature field.

### 17.4 VGF Silicon and GaAs Growth

CrysMAS has been used (under both the CrysMAS name and the earlier STHAMAS designation) for systematic investigation of hot zone designs for photovoltaic-grade Czochralski silicon growth, and for 4-inch GaAs VGF growth with and without travelling magnetic fields. In the GaAs TMF case, CrysMAS (in 3D mode) was used to optimise the AC amplitude, frequency, and phase shift of the KRISTMAG® HMM to achieve a slightly convex interface shape, with striation analysis on as-grown crystals confirming the numerical predictions.

### 17.5 VGF Germanium Growth under KRISTMAG® TMF

Four-inch Ge single crystals were grown under VGF with a KRISTMAG® HMM for the first time. CrysMAS (3D) optimised the electromagnetic parameters to achieve a nearly flat, slightly convex interface throughout growth. Comparison of striation patterns in as-grown crystals against predicted flow patterns confirmed the modelling approach.

### 17.6 CaF₂–TmF₃ Bridgman Growth (2024)

A 2024 study (Nunes et al., *Journal of Crystal Growth*) on Bridgman–Stockbarger growth of CaF₂-rich TmF₃ solid solutions used CrysMAS for numerical modelling of the entire growth experiment. The code's semi-transparent radiation module, using the Gebhart view factor formulation and n-band spectral model with CaF₂ treated as transparent between 0.15–9 μm, was used alongside convection modelling to study melt convection patterns, interface shape evolution, and the effects of temperature gradient under different solidified fractions. This application illustrates CrysMAS's continued usage in published research as recently as late 2024.

### 17.7 Czochralski Silicon Model Validation (2022)

Enders-Seidlitz et al. (2022) used CrysMAS as one of three codes (alongside ANSYS/CFX and CGSim) in a systematic validation study for Czochralski silicon growth, comparing computed temperature distributions and crystallisation front positions against a heavily instrumented model furnace. CrysMAS was used for steady-state heat transfer and transient melt flow computations.

---

## 18. Competitive Landscape

CrysMAS competes in the niche market of dedicated commercial crystal growth simulation software. The primary competitors in the same segment are:

| Software | Vendor | Primary Focus |
|---|---|---|
| CGSim | STR Group Ltd. (Russia/international) | Czochralski, LEC, VCz, Bridgman; modular (Basic + Defects + Flow) |
| FEMAG / FEMAG-CZ | FEMAGSoft S.A. (Belgium) | Cz, Ky, FZ, DS, VB/VGF, HEM, PVT; semiconductor/solar/LED |
| CrysMAS | Fraunhofer IISB (Germany) | Broad process coverage; strong VGF/Bridgman, magnetic field (KRISTMAG®) |

All three codes are described in the literature as providing "approximately the same functionality" for the conjugate heat and mass transport problem in global 2D axisymmetric simulations: temperature distributions, flow structure, interface position, and required heater power. The key differentiators are:

- **CrysMAS** is distinguished by its tight integration with the KRISTMAG® heater-magnet module technology, its particularly deep support for TMF/RMF/SMF modelling, its inverse simulation capability, and its institutional backing from a major applied research institute that simultaneously develops novel crystal growth processes.
- **CGSim** (STR Group) offers a modular product with dedicated point-defect and dislocation density models (via the Defects module) as a first-class feature, and has extensive documentation of CZ silicon applications.
- **FEMAG** (FEMAGSoft) is widely used in the European photovoltaic and sapphire industries, and supports Kyropoulos and other process variants.

General-purpose multi-physics codes (ANSYS Fluent, COMSOL, Elmer, OpenFOAM) are used as complementary tools for 3D and higher-fidelity computations, but are not direct competitors in the "ready-to-use crystal growth simulator" category — they require substantially more setup effort and expertise to apply to crystal growth problems.

---

## 19. Strengths and Limitations

### 19.1 Strengths

**Physics breadth:** CrysMAS covers a uniquely comprehensive set of coupled physics for a single domain-specific code: conduction, view-factor radiation, ray-tracing radiation, semi-transparent media, natural and forced convection (laminar and turbulent), MHD with TMF/RMF/SMF/AMF, inductive heating, species transport, chemical reactions, thermoelastic stress, and inverse heater control — all within one integrated application.

**Ease of use for crystal growers:** The GUI integrates geometry drawing, material assignment, meshing, boundary condition setup, computation control, and results visualisation in one application. Process-specific dialogs (Czochralski parameters, magnetic field parameters) reduce the barrier to entry for non-simulation specialists.

**KRISTMAG® integration:** CrysMAS is the reference simulation tool for the KRISTMAG® HMM technology, providing a unique capability for groups working with travelling and rotating magnetic field equipment sourced from IISB or designed with IISB guidance.

**Inverse simulation:** The inverse heater power optimisation capability is mature and well-documented, enabling direct derivation of growth schedules from target interface shapes or thermocouple readings.

**Dual mesh strategy:** The combination of unstructured triangles (flexibility for geometry) and structured body-fitted grids (efficiency for convection) is a well-engineered solution to competing numerical demands.

**Semi-transparent radiation:** The n-band model and the alternative ray tracing module give CrysMAS strong capabilities for materials like sapphire, fluorides, and compound semiconductors where volumetric radiation is significant.

**Batch mode and automation:** Support for unattended batch runs and automatic geometry generation enables systematic parametric studies.

**Publicly accessible manual:** Unusually for a commercial code, the full user manual with tutorials is publicly accessible online, providing transparency into capabilities and aiding academic users.

### 19.2 Limitations

**Primarily 2D axisymmetric:** The core solver operates in 2D axisymmetry. Three-dimensional effects (non-symmetric heater arrangements, crystal rotation combined with asymmetric flow, rectangular or square crucibles for mc-Si solidification, asymmetric defects) require coupling with external 3D codes (ANSYS CFX, OpenFOAM). While 3D CrysMAS electromagnetic computations are documented for TMF, the full 3D multi-physics solver scope appears limited.

**No integrated dislocation density model:** Unlike CGSim's Defects module, CrysMAS does not appear to include a first-principles dislocation density evolution model (e.g., based on the Alexander–Haasen model). Thermoelastic stress is computed, but mapping stress to dislocation density requires post-processing or coupling with external models.

**Radiation cost scales quadratically:** The view factor matrix computation scales quadratically with the number of radiating surface tiles. For furnaces with many radiating surfaces, mesh coarsening along radiating lines is necessary, which can reduce spatial resolution in critical areas.

**Commercial licensing barrier:** As a commercially licensed product, CrysMAS is not freely accessible to academic groups with limited budgets, in contrast to open-source alternatives like Elmer FEM (with crystal growth extensions) or OpenFOAM.

**Documentation version:** The publicly available manual documents version 4.3.21. The current internal development version and any features added since the last public manual update are not publicly described.

**Domain specificity:** CrysMAS is highly specialised for melt-growth crystal growth furnaces; for significantly different problem types (e.g., molecular beam epitaxy, ion implantation, electrochemical deposition) it is not the appropriate tool.

---

## 20. Current Status and Outlook (as of 2026)

Based on the most recent available information (IISB website updated May 2026; peer-reviewed literature through late 2024; CrysMAS manual version 4.3.21 referenced in 2022 publications):

**Active tool:** CrysMAS remains an active, maintained simulation tool at IISB. It is listed as one of the three primary software tools in the Equipment Simulation service offering alongside OpenFOAM and ANSYS (accessed June 2026 from the IISB website).

**Continued publication:** Peer-reviewed publications using CrysMAS continue to appear in the crystal growth literature through at least 2024 (CaF₂–TmF₃ Bridgman study) and 2022 (Czochralski model validation study). This indicates that the code remains scientifically productive and that its results are accepted as reliable by the crystal growth community.

**Widening material scope:** IISB's materials research has expanded significantly into SiC, GaN, and AlN (all wide-bandgap materials critical for power electronics), and CrysMAS is used alongside OpenFOAM and ANSYS for CVD, PVT, and HVPE simulations in these material systems. The equipment simulation service explicitly lists these materials and processes as current offerings.

**SiC scale-up activities:** IISB is actively engaged in the scale-up of SiC epitaxy and substrate manufacturing to 200 mm diameter wafers within the European TRANSFORM project. CrysMAS-based thermal simulations of PVT reactors support this technology development.

**KRISTMAG® technology:** The KRISTMAG® heater-magnet module continues to be a key differentiator for IISB; the tight integration of CrysMAS with TMF/RMF simulation ensures CrysMAS remains the preferred design tool for KRISTMAG®-based furnaces.

**HPC deployment:** CrysMAS is deployed on IISB's in-house HPC cluster, suggesting that multi-core parallel computation is exploited for parametric studies and high-resolution simulations.

**Potential developments (inferred):** Given IISB's expanding focus on machine learning and AI (the institute has a dedicated "Modeling and Artificial Intelligence" research area), integration of CrysMAS-generated training data with surrogate modelling or data-driven inverse design approaches is a plausible future development direction, though no public documentation of this exists as of the report date.

---

## 21. Summary

CrysMAS is a mature, physics-rich, commercially licensed simulation package occupying a specialised and well-defined niche: **global numerical simulation of high-temperature melt and vapour crystal growth furnaces**. Developed over more than three decades at the Crystal Growth Laboratory and then the Materials Department of Fraunhofer IISB in Erlangen, Germany, it evolved from the predecessor codes STHAMAS and CrysVUn++ into a unified platform that couples conduction, multi-mode radiation (view factor and ray tracing, opaque and semi-transparent media), laminar and turbulent melt and gas convection, full MHD for static and dynamic magnetic fields, inductive heating, species transport with chemical reactions, thermoelastic stress, and inverse heater power optimisation within one integrated application.

Its primary distinguishing features relative to competitors are its tight coupling with the KRISTMAG® heater-magnet module technology for travelling and rotating magnetic fields, its well-developed inverse simulation capability, the breadth of physical phenomena included in a single code, and the institutional environment that continuously validates and applies it to real crystal growth processes across a wide range of materials (Si, Ge, GaAs, InP, SiC, GaN, AlN, CZT, sapphire, fluorides, and oxides) and techniques (Czochralski, VGF, Bridgman, EFG, FZ, PVT, CVD, HVPE, THM).

As of 2026, CrysMAS remains an active, continuously applied simulation tool at IISB and in the broader international crystal growth community, as evidenced by continued citations in peer-reviewed publications and its listing as a primary simulation service tool on the IISB Equipment Simulation webpage.

---

## 22. References and Further Reading

### Key Primary Sources

- Fraunhofer IISB, Department of Materials — Equipment Simulation. Official webpage: https://www.iisb.fraunhofer.de/en/research_areas/materials/equipment_simulation.html (accessed June 2026).

- CrysMAS User Manual and Tutorial, version 4.3.21. Fraunhofer IISB. Available online: https://download.iisb.fraunhofer.de/downloads/Manual/index.html

- J. Friedrich, G. Müller. "Erlangen — An Important Center of Crystal Growth and Epitaxy: Major Scientific Results and Technological Solutions of the Last Four Decades." [*Crystal Research and Technology*, 55, 1900053 (2020)](https://doi.org/10.1002/crat.201900053).

- K. Dadzis, et al. "Validation, Verification, and Benchmarking of Crystal Growth Simulations." [*Journal of Crystal Growth*, 474, 14–26 (2016)](https://doi.org/10.1016/j.jcrysgro.2016.12.091).

- A. Enders-Seidlitz et al. "Development and Validation of a Thermal Simulation for the Czochralski Crystal Growth Process Using Model Experiments." [*Journal of Crystal Growth*, 593, 126757 (2022)](https://doi.org/10.1016/j.jcrysgro.2022.126750).

- M. Hainke, T. Jung, J. Friedrich, B. Fischer, M. Metzger, G. Müller. "Equipment and Process Modelling of Industrial Crystal Growth Using the Finite Volume Codes CrysVUn and STHAMAS." In: [*Progress in Industrial Mathematics at ECMI 2000*, Mathematics in Industry vol. 1, Springer (2002)](https://doi.org/10.1007/978-3-662-04784-2_29).

### Representative CrysMAS Application Publications

- M.D. Reed et al. "On crucible effects during the growth of cadmium zinc telluride in an electrodynamic gradient freeze furnace." [*Journal of Crystal Growth* 311 (2009), pp. 2327-2335](https://doi.org/10.1016/j.jcrysgro.2009.01.141).

- R. Backofen, M. Kurz, G. Müller. "Process modeling of the industrial VGF growth process using the software package CrysVUN++." [*Journal of Crystal Growth*, 211 (2000), pp. 202-206](https://doi.org/10.1016/S0022-0248(99)00792-7).

- S. Brandon, J.J. Derby et al. "Simulation of Heat Transfer and Convection During Sapphire Crystal Growth in a Modified Heat Exchanger Method." [*Journal of Crystal Growth* 367 (2013), pp. 27-34](https://doi.org/10.1016/j.jcrysgro.2013.01.011).

- T. Jung et al. "Numerical Simulation of Czochralski Crystal Growth under the Influence of a Traveling Magnetic Field Generated by an Internal Heater-Magnet Module (HMM)." [*Journal of Crystal Growth* 310 (2008), pp. 1523-1532](https://doi.org/10.1016/j.jcrysgro.2007.12.031).

- M. Kirpo. "Global Simulation of the Czochralski Silicon Crystal Growth in ANSYS FLUENT." [*Journal of Crystal Growth*, 371 (2013) pp. 60-69](https://doi.org/10.1016/j.jcrysgro.2013.02.005).

- Nunes et al. "Single Crystal Growth by the Bridgman–Stockbarger Technique of CaF₂-rich – TmF₃ Solid Solutions: Evidence of Mixed Valence Tm²⁺ and Tm³⁺ Cations." [*Journal of Crystal Growth* 1010 (2024) 177784](https://doi.org/10.1016/j.jallcom.2024.177784)

- Various CZT EDG papers: J.J. Derby group (University of Minnesota), Pacific Northwest National Laboratory, *Journal of Crystal Growth* and SPIE proceedings (2008–2015).

### Competing Software (for context)

- STR Group. CGSim — Crystal Growth Simulator. https://str-soft.com/software/cgsim/

- FEMAGSoft S.A. FEMAG Software. https://www.femagsoft.com/

- Fraunhofer IISB Crystal Growth Brochure (2012). https://www.iisb.fraunhofer.de/content/dam/iisb/de/documents/presse_publikationen/prospekte/Brochure_CrystalGrowth_2012_www.pdf


---

## Further Reading

+ [Peer-Reviewed Journal Articles on CrysVUn / CrysVUN++](./reference-crysvun.md)
+ [Peer-Reviewed Journal Articles Describing the CrysMAS Crystal Growth Simulation Software](./reference-crysmas.md)
+ [Bibliography of Peer-Reviewed Application Papers Using CrysVUn / CrysVUn++](./applications-crysvun.md)
+ [Customers of CrysMAS Family](./users-crysmas.md)

---

*Report prepared June 2026. All information is based on publicly available documentation, peer-reviewed literature, and official Fraunhofer IISB web resources.*

---

> [!NOTE]
> 
> Generated by Claude.ai
>
> Model: Sonet 4.6
>
> Prompt: Prepare a thorough and detailed technical report on the CrysMAS software from Fraunhofer IISB (Germany).
> The technical report must comprehensively address the current state of affairs.
> It must be exhaustive and wide-ranging.
> Show output in Markdown format.
> Do not copy the output of the exported files into the chat.
