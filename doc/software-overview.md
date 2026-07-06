# Software for Modeling the Crystal Growth Process

## 1. Introduction and Scope

The Czochralski (Cz) method — first described by Jan Czochralski in 1918 — remains the dominant industrial technique for producing large-diameter single-crystal ingots of silicon, germanium, gallium arsenide, indium phosphide, sapphire, and a range of oxide and halide crystals. Computer simulations of the Cz process have established themselves as a basic tool for the optimization of the growth process, allowing producers to reduce costs while maintaining high quality of the crystalline material.

The Czochralski (Cz) process involves a variety of coupled physical phenomena even on a macroscopic level: heat transfer by conduction, convection and radiation, melt and gas flows, electromagnetism, and stresses. To optimize the quality and yield of grown crystals, as well as for the development of growth processes for new materials, numerical simulations are an important tool. They give insights into the underlying physics of the growth process where measurements are often impossible, and they help to reduce both time and costs because new setups can be investigated virtually instead of experimentally.

This report comprehensively surveys the landscape of software tools used today — specialized commercial codes, general-purpose multiphysics platforms, open-source frameworks, and emerging machine-learning approaches — covering their physical models, numerical methods, validation status, and practical applicability.

---

## 2. Physical Phenomena Requiring Simulation

A complete numerical model of the Cz process must couple a set of tightly interlocked physical phenomena. Understanding these is prerequisite to evaluating any software tool.

### 2.1 Global Heat Transfer

The entire furnace — heater, crucible, melt, crystal, gas atmosphere, heat shields, and enclosures — must be treated as a radiatively and conductively coupled system. Radiation dominates at the high temperatures involved (silicon melts at 1685 K), and view-factor calculations between irregularly shaped axisymmetric surfaces are essential. Heat transfer by nonlinear anisotropic conduction and radiation as well as the analysis of thermoelastic stress are among the foundational capabilities any Cz simulator must provide. The interface between crystal, melt, and gas (the three-phase junction) is a point of special numerical sensitivity, where the crystallisation front shape is determined by the balance of latent heat release against heat extraction by the crystal.

### 2.2 Melt Convection and Turbulence

The silicon melt in a large Cz puller is a high-Rayleigh-number, high-Prandtl-number fluid subject to buoyancy-driven natural convection, crystal-rotation-driven forced convection (Taylor–Couette flow), crucible-rotation-driven forced convection (von Kármán flow), Marangoni convection at the free surface, and electromagnetic body forces when magnetic fields are applied. The resulting flow is generally turbulent. The global model of the small industrial furnace incorporates the most important physical phenomena of the Cz growth process including latent heat generation during crystallisation, crystal–melt interface deflection, turbulent heat and mass transport, and oxygen transport. Modelling the turbulent melt is among the most challenging aspects, and codes use a variety of turbulence models — k–ε, k–ω, large-eddy simulation (LES), or effective-viscosity approaches.

### 2.3 Magnetic Hydrodynamics (MHD)

Industrial silicon pullers routinely apply external magnetic fields to suppress turbulent melt convection and to control oxygen transport. Three main configurations are used: axial (AXMF), horizontal/transverse (HMCZ), and cusp (CMCZ). This study simulated the growth process of 508 mm diameter single-crystal silicon using the Magnetically Controlled Czochralski (MCZ) method, establishing a multi-field coupling model that includes a thermal field, flow field, oxygen and carbon impurity concentration field, and magnetic field. Modelling MHD requires the addition of Lorentz-force body terms in the Navier–Stokes equations and solution of Maxwell's equations for the induced current distribution.

### 2.4 Impurity Transport: Oxygen and Carbon

Oxygen incorporation is critical: SiO evaporation from the quartz crucible wall provides the dominant oxygen source, while SiO evaporation from the melt free surface is the primary sink. The resulting oxygen concentration determines mechanical properties (via oxygen precipitation and dislocation pinning) and device performance. Carbon contamination, a secondary concern, enters via graphite hot-zone components. The effects of cusp magnetic field introduction, argon inlet flow velocity, and furnace pressure on the transport of oxygen and carbon impurities are analysed, and the concentration field distribution of oxygen and carbon impurities within the furnace at the equal-diameter stage (300 mm) under different parameters is obtained.

### 2.5 Point Defect Engineering: the V/G Criterion

The dominant framework for understanding microdefect formation in Cz silicon is Voronkov's theory, which shows that whether a growing crystal becomes vacancy-rich or self-interstitial-rich depends on the ratio V/G, where V is the pull rate and G is the axial temperature gradient at the solid–liquid interface. Voronkov's Theory found that the ratio of V to G (referred to as V/G) can determine the point defect concentration in the ingot. For V/G ratios below a critical ratio, an interstitial-rich ingot is formed, while for V/G ratios above the critical ratio, a vacancy-rich ingot is formed. Simulation codes must therefore resolve not just the global temperature field but also the fine spatial structure of V/G across the crystal radius, as this determines whether the crystal contains D-defects (vacancy clusters), L/D agglomerates (interstitial clusters), or a defect-free perfect silicon zone between them.

### 2.6 Thermal Stress and Dislocation Generation

Thermal gradients within the solidifying crystal produce thermoelastic stresses. When these exceed the critical resolved shear stress, dislocations are generated and multiply by thermally activated glide. For compound semiconductors (GaAs, InP), achieving low etch-pit densities (EPD) across large-diameter crystals is a major objective. Simulation codes provide von Mises stress maps and, in some cases, full dislocation density evolution using Alexander–Haasen-type models.

### 2.7 Crystal Shape, Free Surface, and Capillarity

The shape of the crystal (diameter profile) is controlled through the meniscus at the three-phase line, governed by the Wulff–Jacobs–Miller equation. Thermal-capillary models (first formulated by Derby and Brown in the 1980s) couple the meniscus shape to the global heat balance, allowing prediction of diameter transients during Cz pulling. Time-dependent simulation incorporating the diameter feedback loop is essential for process control studies.

---

## 3. Specialized Commercial Simulation Codes

### 3.1 CGSim (STR Group, St. Petersburg / distributed worldwide)

**Website:** https://str-soft.com/software/cgsim/

The CGSim (Crystal Growth Simulator) code is specialised software for simulation of Czochralski (Cz), Liquid Encapsulated Czochralski (LEC), Vapour Pressure Controlled Czochralski (VCz), and Bridgman growth. The code provides information to growers on the most important physical processes responsible for crystal growth and quality. The CGSim package contains several modules: Basic CGSim, Defects, Flow Module, and CGSim View.

The practical application scope of CGSim is extensive. CGSim can be effectively applied to: control and optimisation of the crystallisation front geometry and V/G distribution by adjustment of the hot zone and growth parameters; increase of the crystallisation rate while maintaining high crystal quality; control of stress and defects in the growing crystal via accurate adjustment of heat shields; governing melt convection via crystal/crucible rotation rates and magnetic fields of various strength and orientation; stabilisation of convection in the melt while maintaining reasonable turbulent mixing; analysis of impurity transport in both the melt and gas, with prediction of oxygen and carbon-containing species concentrations in Si Cz growth.

The **Defects module** implements the Voronkov–Sinno point-defect model, computing spatial distributions of vacancies and self-interstitials from the solid–liquid interface down to the temperature range where agglomeration occurs. This is essential for growing defect-free ("perfect silicon") crystals. The **Flow Module** adds a full 3D (or axisymmetric with swirl) turbulent melt-flow solver. **CGSim View** provides post-processing with 2D/1D distributions including heat and mass fluxes, V/G maps, and 1D temperature gradient profiles along the crystallisation front, as well as 3D animation of melt convection.

CGSim 26.1 has been released as the most recent version. Recent publications employing CGSim include work on pulling rate and productivity optimisation for photovoltaic silicon crystal growth published in the *Journal of Crystal Growth* in 2023.

CGSim is widely regarded as the industry standard for large-scale silicon Cz pullers (200 mm and 300 mm diameter), and is actively used in photovoltaic silicon production, semiconductor-grade silicon, and compound semiconductor growth.

### 3.2 FEMAG/CZ (FEMAGSoft, Belgium)

**Website:** https://www.femagsoft.com/products/femag-cz.html

FEMAG, based near Louvain-la-Neuve, Belgium, was established in 2003 as a spin-off company of the Université catholique de Louvain where research activity in the field of crystal growth started in the mid-1980s. Since 1985, FEMAGSoft, and later FEMAG, develops, markets and supports process-oriented simulation software products.

The Czochralski process simulator is used to design new hot zones and recipes that match specific business requirements, including: growth of very large diameter ingots; defect-free silicon ingot growth; process yield increase; oxygen content control; carbon content decrease; ingot radial and axial resistivity variance decrease; CCZ (Continuous Czochralski) process implementation; design of the furnace hot zone by a global calculation involving radiation, conduction, and convection; anisotropic thermal stresses in the crystal; point defects in the crystal; and quasi-steady and time-dependent modelling.

A distinguishing feature of FEMAG/CZ is the **FEMAG/CZ/TMF module**, which provides the possibility to compute the effect of a Transverse Magnetic Field (TMF) on the velocity, temperature and species fields in the melt and in the crystal. FEMAG claims a leadership position in accuracy: 35 patents are referring to FEMAG simulation software, and FEMAG's leadership is accuracy of the data computed, i.e., matching the experimental predictions including the evolution of the interface shape during crystal growth with an accuracy of 5%. The FEMAG/CZ/OX module extends coverage to oxide crystal growth (notably sapphire), addressing semitransparent crystals where radiation transport inside the crystal must be modelled explicitly. FEMAG products include maintenance, user support, and personalised training.

### 3.3 CrysMAS (Fraunhofer IISB, Erlangen)

**Documentation:** https://download.iisb.fraunhofer.de/downloads/Manual/index.html

CrysMAS is the successor to the earlier CrysVUn++ and STHAMAS codes developed at the Crystal Growth Laboratory (CGL) of the Fraunhofer Institute for Integrated Systems and Device Technology (IISB) in Erlangen. The resulting software packages STHAMAS and CrysVUn and the later combined CrysMAS were licensed worldwide and used by companies and research institutes until today.

Both CrysMAS and CGSim solve the inverse problem of finding the required heater power, however in a different manner. CrysMAS uses the temperature difference at the three-phase junction and computes the latent heat required to fulfil this constraint. In cavities filled with transparent material, the wall-to-wall radiation is computed, with view factors computed once before the run. CrysMAS excels at global furnace-scale heat transfer analysis and is particularly well suited to 2D axisymmetric quasi-static calculations across a wide range of crystal types (silicon, gallium oxide, oxides, halides). It has been applied extensively to Cz growth of β-Ga₂O₃, a material of significant contemporary interest for power electronics.

### 3.4 CrysVUn++ (Fraunhofer IISB / historical, still referenced)

The program package CrysVUn++ is designed for the needs of crystal growers to have a fast and efficient computer code for the simulation of growth processes and equipment. CrysVUn++ facilitates rapid thermal analysis of crystal growth setups, significantly enhancing simulation efficiency. The software supports complex geometries through automatic grid refinement using unstructured triangular grids. CrysVUn++ introduced the "inverse problem" approach: given a desired crystal shape and growth rate, the code computes the heater temperature profile required to achieve it — an innovation that directly supports process recipe design. Although largely superseded by CrysMAS, CrysVUn++ results continue to appear in the literature for legacy process studies and VGF growth comparisons.

---

## 4. General-Purpose Multiphysics Platforms Applied to Cz Growth

### 4.1 ANSYS Fluent

ANSYS Fluent is the leading commercial CFD code and has been applied to Cz growth primarily for melt flow and oxygen transport studies. The author shows the application of the general CFD code ANSYS Fluent to solution of the static two-dimensional (2D) axisymmetric global model of the small industrial furnace for growing silicon crystals with a diameter of 100 mm. The presented numerical model incorporates the most important physical phenomena of the Cz growth process including latent heat generation during crystallisation, crystal–melt interface deflection, turbulent heat and mass transport, and oxygen transport. ANSYS Fluent is used where the melt flow modelling requirements exceed those of the specialised codes, or where users are already embedded in the ANSYS simulation ecosystem. The CrystmoNet framework, developed at the Institute for Problems in Mechanics (Russian Academy of Sciences), integrates ANSYS Fluent for fluid mechanics alongside MSC.MarcMentat for solid mechanics and Tecplot-360 for visualisation, with a problem-oriented Crystmo module for Cz-specific thermal and defect calculations.

### 4.2 COMSOL Multiphysics

COMSOL Multiphysics is used extensively for Cz simulation, particularly for MHD studies and oxygen/carbon transport, owing to its flexible multi-field coupling. COMSOL-based multi-physics field interfaces simultaneously consider interactions between thermal, flow, magnetic, and oxygen and carbon impurity concentration fields. A 2025 AIP Advances study demonstrated a full 2D axisymmetric model of 508 mm silicon Cz growth under cusp magnetic field using COMSOL, coupled to gas flow simulations for argon transport and impurity evaporation. COMSOL's advantage is in rapid model construction via its GUI and tight coupling between modules (AC/DC, CFD, Heat Transfer, Structural Mechanics); its disadvantage is computational cost relative to the specialised codes for industrial-scale production studies.

A comparative study of Cz growth of β-Ga₂O₃ employed CrysMAS, CGSim, ANSYS-CFX and COMSOL Multiphysics for the same furnace, allowing direct comparison of software predictions for the temperature field, crystallisation front shape, and thermal stress. This remains one of the most thorough published software benchmarks for Cz simulation.

### 4.3 ANSYS CFX

ANSYS CFX offers an alternative to Fluent within the ANSYS ecosystem, with stronger support for rotating reference frames, which is relevant for crystal/crucible rotation modelling. It has been used in published Cz studies, particularly for compound semiconductor growth and for comparative benchmarks.

---

## 5. Open-Source Frameworks

The dominant trend in open-source Cz simulation is the coupling of best-in-class open-source solvers — FEM codes for electromagnetics and heat transfer, FVM codes for fluid dynamics — through purpose-built Python interfaces and containerised environments.

### 5.1 opencgs / NEMOCRYS Project

**GitHub:** https://github.com/nemocrys/opencgs

The opencgs package provides an interface to set up crystal growth simulations using open-source software. Currently, the focus is set on Czochralski growth. opencgs is validated within the NEMOCRYS project using model experiments. The focus of opencgs is on 2D axisymmetric thermal simulation (including inductive heating) using the software Elmer.

The NEMOCRYS project (Next Generation Multiphysical Models for Crystal Growth Processes), funded by an ERC Starting Grant (agreement No. 851768) and led at the Leibniz-Institut für Kristallzüchtung (IKZ) in Berlin, has produced the most comprehensive open-source Cz simulation infrastructure currently available. The NEMOCRYS project aims at profoundly validated numerical models for crystal growth. These processes involve a variety of coupled physical phenomena such as heat transfer including radiation and phase change, electromagnetism, melt- and gas flows and thermal stresses.

The most current version of the framework couples:

- **Elmer FEM** — for global time-harmonic electromagnetic induction, steady-state heat transfer (including radiative transfer via view factors), and phase-change (crystallisation front position)
- **OpenFOAM** — for transient or steady-state melt flow (via modified `buoyantBoussinesqPimpleFoam` and `buoyantBoussinesqSimpleFoam` solvers with additional Lorentz force and Joule heating terms, collected in the `nemoFoam-utils` repository)
- **Gmsh** — for FEM mesh generation, with support for moving-boundary mesh updates as the crystal grows
- **preCICE** — as the inter-solver coupling library for data exchange between Elmer and OpenFOAM meshes
- **ParaView** and Python packages — for post-processing and visualisation

A new 2D and 3D Cz growth model has been developed using these open-source tools, with Elmer for global time-harmonic electromagnetism, steady-state heat transfer and phase change modelling, coupled with OpenFOAM for transient or steady-state melt flow modelling. The framework is distributed as a Docker image (`nemocrys/opencgs:v1.0.1`), significantly lowering the barrier to reproducible deployment. Example simulations cover 2D and 3D Cz growth of CsI, Si (including with KristMAG travelling magnetic field), and Sn (the model material used in the NEMOCRYS experimental validation rig).

A key contribution of the NEMOCRYS group is systematic validation. In this work, a new 2D open-source thermal Cz growth model is introduced, verified with analytical solutions, and validated using dedicated model experiments with tin and hence easy access for the required measurements. A three-step procedure is applied to identify critical modelling parameters, make adjustments, and evaluate the resulting modelling accuracy. Comparison of measured temperatures in the crucible shows good agreement. The validation PhD thesis (Wintzer, 2024, TU Berlin) constitutes the most detailed published validation dataset for open-source Cz models.

### 5.2 FEniCS for Cz Growth

A new and extendable model has been developed using the open-source software FEniCS. Basic equations for electromagnetic induction, heat conduction and radiation as well as phase change are thoroughly derived up to a finite element form. FEniCS (now FEniCSx) is attractive for implementing novel mathematical models (e.g., phase-field methods for the moving crystallisation front, arbitrary Lagrangian–Eulerian formulations for moving boundaries) without the constraints imposed by finite-volume codes. The NEMOCRYS group has also explored FEniCS for specialised dynamic problems with moving phase boundaries as a complement to Elmer.

### 5.3 Elmer FEM (standalone)

Elmer (http://www.elmerfem.org), an open-source multiphysics FEM suite developed by CSC in Finland, is the backbone of the NEMOCRYS Cz framework. Its `StatMagSolve` module handles time-harmonic inductive heating, and `HeatSolve` handles coupled conduction–radiation heat transfer. Elmer's modular architecture makes it well suited to adding crystal-growth-specific solvers (e.g., the capillary meniscus equation), and it has been used in standalone Cz studies beyond the opencgs framework.

### 5.4 OpenFOAM

OpenFOAM (https://www.openfoam.com) is used within the NEMOCRYS framework for melt and gas-phase flow, but has also been applied to Cz problems independently — notably for turbulent melt convection studies and for verification against commercial codes. The `nemoFoam-utils` repository provides the MHD boundary conditions and modified solvers needed for Cz applications.

---

## 6. Comparison of Codes: Physical Model Coverage

The following table summarises the physical phenomena coverage of the principal codes, as verified against vendor documentation and peer-reviewed benchmark studies.

| Capability | CGSim | FEMAG/CZ | CrysMAS | COMSOL | ANSYS Fluent | opencgs/Elmer+OFoam |
|---|---|---|---|---|---|---|
| Global 2D axisymmetric heat transfer (conduction + radiation) | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ |
| Melt convection (laminar) | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ |
| Melt convection (turbulent) | ✓ (Flow Module) | ✓ | Limited | ✓ | ✓ | ✓ (OpenFOAM) |
| Axial magnetic field (AXMF) | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ |
| Cusp / transverse magnetic field | ✓ | ✓ (TMF module) | ✓ | ✓ | ✓ | ✓ |
| Oxygen transport | ✓ | ✓ | ✓ | ✓ | ✓ | Partial |
| Carbon transport | ✓ | ✓ | ✓ | ✓ | ✓ | No |
| Point defect (V/G) modelling | ✓ (Defects module) | ✓ | ✓ | Custom UDF | Custom UDF | No |
| Thermoelastic stress | ✓ | ✓ (anisotropic) | ✓ | ✓ | Via Mechanical | Planned |
| 3D melt flow | ✓ | Limited | ✓ | ✓ | ✓ | ✓ (3D OFoam) |
| Semi-transparent crystal (radiative transfer) | ✓ (discrete ordinate) | ✓ | ✓ | ✓ | ✓ | Partial |
| Inverse problem (heater power) | ✓ | ✓ | ✓ | Manual | Manual | No |
| Time-dependent / transient pulling | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ |
| Open-source / reproducible | No | No | No | No | No | ✓ (GPLv3) |
| Validated against experiment | Industrial (unpublished) | Industrial | Industrial | Peer-reviewed | Peer-reviewed | Published model experiments |

---

## 7. Material Systems Covered

### 7.1 Silicon (Semiconductor and Photovoltaic Grade)

Silicon dominates Cz simulation activity. Semiconductor-grade silicon requires tight control of the V/G ratio to achieve "perfect silicon" or to engineer specific vacancy/interstitial profiles for device applications. Photovoltaic silicon has more relaxed defect specifications but requires maximising pull rate and ingot weight to minimise cost per watt. Key simulation parameters include: the oxygen content (target: 10–20 ppma for semiconductor use), carbon content (< 1 ppma), resistivity radial uniformity (< 10% for large-diameter wafers), and crystallisation front convexity. Large-diameter (300 mm, 450 mm) silicon simulation is computationally intensive because the large melt volume (> 100 kg) produces high-Reynolds-number turbulent flow that requires 3D transient computation or carefully validated turbulence models.

### 7.2 Compound Semiconductors: GaAs, InP, GaSb

Liquid Encapsulated Czochralski (LEC) and Vapour Pressure Controlled Czochralski (VCz) variants are used for III–V semiconductors. The CGSim package provides adequate account of encapsulant, turbulent gas flow, and convective heat transport in liquid encapsulated growth. The primary simulation challenges are: (1) the high vapour pressure of the group-V component (arsenic, phosphorus), requiring pressurised chambers; (2) the strong anisotropy of thermal expansion and elastic constants, producing complex stress fields; (3) the difficulty of achieving low EPD (< 500 cm⁻²) at large diameters.

### 7.3 Oxide Crystals: Sapphire (Al₂O₃), YAG, Gadolinium Gallium Garnet

Sapphire Cz growth is a major industrial process for LED substrates and optical windows. The dominant simulation challenge is the high optical absorption and scattering of the melt combined with the semitransparency of the crystal, requiring a full radiative transport treatment (discrete ordinates or Monte Carlo). CGSim, FEMAG/CZ (via the FEMAG/CZ/OX module), and COMSOL all address this.

### 7.4 β-Ga₂O₃

Gallium oxide has attracted intense recent interest as an ultrawide-bandgap semiconductor for power electronics. Numerical modelling of the Czochralski growth of single crystalline β-Ga₂O₃ starts at the 2D heat transport analysis within the crystal growth furnace, proceeds with the 3D heat transport and fluid flow analysis in the crystal–melt–crucible arrangement and targets the 3D thermal stress analysis within the β-Ga₂O₃ crystal. Its monoclinic crystal symmetry introduces strong anisotropy in both thermal and elastic properties, requiring fully 3D stress calculations with off-diagonal tensor components.

### 7.5 Halides: CsI, CaF₂

Caesium iodide and calcium fluoride are grown for scintillation detector and optical applications. A 2025 paper in the Journal of Crystal Growth reports the validation of a numerical model for Czochralski growth of caesium iodide and calcium fluoride, comparing it with experimental results and numerical data from a similar model. The opencgs framework has been applied to CsI Cz growth as one of its primary validation cases.

### 7.6 Germanium

Germanium Cz growth is important for high-efficiency photovoltaic cells (multi-junction), infrared optics, and gamma-ray detectors. A study evaluated the potential of the machine learning technique of decision trees to understand the relationships among furnace design, process parameters, crystal quality, and yield in the case of the Czochralski growth of germanium. Training data were provided by CFD modelling. The results showed that the process parameters, particularly the pulling rate, had a substantially greater impact on the crystal quality and yield than the design parameters of the furnace hot zone.

---

## 8. Numerical Methods

### 8.1 Spatial Discretisation

Cz simulation codes use either finite element methods (FEM) or finite volume methods (FVM). FEM is dominant in codes handling complex geometries and radiation view factors (CrysVUn++, Elmer, FEniCS, COMSOL). FVM is preferred for turbulent fluid flow (ANSYS Fluent, OpenFOAM). Hybrid approaches couple FEM codes for heat transfer to FVM codes for melt flow (the NEMOCRYS Elmer–OpenFOAM coupling is the canonical open-source example).

Meshes are almost universally 2D axisymmetric for the global furnace model (adequate for steady-state and quasi-steady computations), with 3D full-furnace models reserved for magnetic-field studies, asymmetric thermal boundary conditions, or time-dependent flow that breaks axisymmetry (e.g., baroclinic oscillations).

### 8.2 Radiation Transport

Radiation is the dominant heat transfer mode between hot zone components. Methods used include:

- **Discrete Exchange Factor (DEF) method** — used in several commercial codes; view factors are computed once and stored, making radiation computationally cheap after setup
- **Discrete Ordinates Method (DOM/S_N)** — used in CGSim for semi-transparent crystal treatment; more accurate for optically thick media
- **P-N approximations** — used for fast engineering estimates in semi-transparent media

### 8.3 Phase-Change and Moving Boundary

The crystal–melt interface is a free boundary: its position is part of the solution. Methods include:

- **Stefan condition tracking** — the classic approach; at each iteration the interface position is updated to satisfy latent heat balance
- **Inverse problem formulation** — as in CrysMAS and CrysVUn++, where heater power (rather than interface position) is the unknown, and the interface constraint fixes the solution
- **Level-set methods** — used in research codes for dynamic simulation of crystal diameter changes
- **Phase-field methods** — used in FEniCS-based research models for fundamental studies of solidification microstructure

### 8.4 Turbulence Modelling for Melt Flow

The silicon melt in a production Cz puller has a Rayleigh number of order 10⁸–10⁹, placing it firmly in the turbulent regime. Modelling options in use include:

- **k–ε and k–ω RANS** — industry standard; computationally affordable but known to over-predict turbulent diffusion
- **Large Eddy Simulation (LES)** — more accurate; applied in academic studies of 3D melt oscillations
- **Effective thermal conductivity / effective viscosity** — simplest approach; calibrated against experimental measurements; used in 2D models where full turbulence resolution is impractical

### 8.5 Electromagnetic Modelling

For magnetic Cz (MCZ), the magnetic field source (coils, permanent magnets) and its interaction with the conducting melt must be computed. The low magnetic Reynolds number of silicon melts (Rm << 1) allows decoupling: the magnetic field is computed independently (from Biot–Savart or finite element magnetostatics), and the Lorentz force is then introduced as a body force in the Navier–Stokes equations. For inductively heated Cz furnaces (used for some oxides and the tin model experiments), the time-harmonic magnetic field must be solved via the eddy-current approximation.

---

## 9. Machine Learning and Data-Driven Approaches

A rapidly growing body of work applies machine learning (ML) to Cz process optimisation and control, operating either alongside or as a replacement for physical simulation. Machine learning has become an increasingly powerful tool in crystal growth research, enabling new ways to model processes, optimise growth conditions, and automate characterisation of crystalline materials. Recent advances include deep learning for defect detection, surrogate modelling for process optimisation, and reinforcement learning for autonomous control.

### 9.1 Surrogate Models / Metamodels

Physics-based Cz simulation is computationally expensive: a single 3D transient run may take hours to days. ML surrogate models trained on simulation data dramatically accelerate this. A 2025 study proposes a data-driven approach for optimising the Czochralski process using a finite element model combined with a machine learning analysis, enabling rapid evaluation of large parameter spaces that would be prohibitive with full numerical simulation alone. Neural networks, Gaussian processes, and gradient-boosted tree ensembles have all been used as surrogates.

### 9.2 Hybrid Physics–Data Models

A hybrid model for semiconductor silicon monocrystalline quality prediction in the Cz process proposes a data-driven model (JITLSAE-ELM, based on just-in-time learning fine-tuning strategy) to solve the nonlinear and time-varying relationship of the process. These hybrid approaches use physical equations to constrain the solution space while using data-driven components to compensate for model inadequacy (e.g., unknown material properties, unmodelled furnace asymmetries).

### 9.3 Diameter Control and Process Optimisation

A 2025 study constructs a neural network–genetic algorithm collaborative optimisation framework through a data-driven approach to break the challenge of diameter fluctuation control under multi-parameter coupling. Based on real-time data from the isothermal stage of industrial single crystal furnaces, the Grey Wolf Optimisation algorithm is used to dynamically optimise the weights and hyperparameters of the Multi-Layer Perceptron. A high-precision surrogate model of the relationship between process parameters (heater power, crystal pulling speed, crucible lift speed) and diameter fluctuation is established.

### 9.4 Decision Trees and Feature Importance

A study evaluated the potential of decision trees to understand the relationships among furnace design, process parameters, crystal quality, and yield in the case of Czochralski growth of germanium. Training data were provided by CFD modelling. The variety of data was ensured by the Design of Experiments method. The results showed that the process parameters, particularly the pulling rate, had a substantially greater impact on the crystal quality and yield than the design parameters of the furnace hot zone. This use of ML not just for prediction but for feature importance analysis is a powerful complement to physics-based understanding.

### 9.5 Reinforcement Learning

Reinforcement learning for autonomous control of Cz pulling has emerged as a research topic, with agents trained in simulation environments. The long-term vision is a closed-loop Cz puller that autonomously adjusts pull rate, heater power, and rotation rates to maintain target crystal quality metrics.

### 9.6 Limitations of ML Approaches

ML approaches to Cz optimisation face structural challenges. Training data from simulation inherits whatever errors exist in the physical model. Real furnace data is proprietary and sparse relative to the dimensionality of the process. Crystal quality cannot be measured in situ during growth; most quality indicators (defect density, oxygen content, resistivity) are measured only after the ingot is sliced, introducing latency. Physical simulation codes remain necessary as the ground truth, and the most productive near-term application of ML is as an accelerator of simulation-based optimisation rather than as a replacement for physical models.

---

## 10. Validation: Current State and Challenges

Validation of such models is mostly insufficient due to the lack of in-situ measurement data, and open-source models are hardly available. To address these issues, a new 2D and 3D Cz growth model has been developed, providing a comparison with experimental results and numerical data from a similar model, achieving good agreement and showing opportunities for further improvement of melt flow modelling.

The validation problem in Cz simulation is structural: the interior of a production silicon puller at 1685 K is inaccessible to direct measurement. Temperature measurements inside the melt are destructive and difficult; the crystal–melt interface position can be inferred indirectly from crystal weight or laser reflectometry; oxygen content is measured post-growth by FTIR or SIMS. The NEMOCRYS group's approach — building a scaled model experiment with a low-melting-point material (tin), extensive thermocouple arrays, and traceable calibration — represents the current best practice for open validation datasets.

For commercial codes, validation is largely performed against production data from crystal growers under non-disclosure agreements. This creates a reproducibility gap between academic open-source work and industrial practice.

---

## 11. Emerging Materials and Novel Process Variants

### 11.1 Continuous Czochralski (CCz)

The CCz process replenishes melt from a secondary crucible during growth, maintaining constant melt level and composition. It is of major interest for photovoltaic silicon production. FEMAG/CZ explicitly lists CCz process implementation as a use case. The additional complexity (two crucible volumes, a feed channel, oxygen transport between them) requires extension of standard Cz models.

### 11.2 KristMAG Technology

KristMAG (developed at IKZ) applies a travelling magnetic field to stabilise and control melt convection without the hardware complexity of conventional solenoids. The opencgs framework includes example simulations (`kristmag-si_2D-3D`) of Si Cz growth using a TMF based on KristMAG technology, making it one of the few open-source implementations of this variant.

### 11.3 Large-Diameter Silicon (> 300 mm)

The semiconductor roadmap requires 450 mm silicon wafers for next-generation fabs. Simulation challenges scale adversely with diameter: the melt mass exceeds 300 kg, the Rayleigh number increases, and 3D transient simulations become extraordinarily expensive. GPU-accelerated CFD and adaptive mesh refinement are active research directions for this size regime.

---

## 12. Software Ecosystem and Toolchain Summary

The landscape can be organised into three tiers based on deployment context:

**Tier 1 — Industrial-grade dedicated Cz codes:** CGSim, FEMAG/CZ, CrysMAS. These are the tools used by major silicon wafer manufacturers (Shin-Etsu, SUMCO, Siltronic, SK Siltron) and compound semiconductor producers for production process optimisation. They are not publicly available, are licensed on a per-seat annual basis, and their validation is against proprietary industrial data. CGSim is the most widely cited in the academic literature. FEMAG/CZ holds the largest patent citation footprint.

**Tier 2 — General-purpose multiphysics platforms:** COMSOL Multiphysics, ANSYS Fluent, ANSYS CFX. These are used both in industry and academia for specific sub-problems (e.g., MHD, impurity transport), for materials where dedicated codes lack support, and for research into novel growth configurations. They offer the most flexibility in physical model definition but require significantly more effort to set up a Cz model from scratch.

**Tier 3 — Open-source research frameworks:** opencgs (Elmer + OpenFOAM, Docker-deployed, GPLv3), FEniCS-based models (Leibniz Institute work). These are the frontier of transparent, reproducible simulation, with the most rigorous published validation datasets. They are suitable for academic research, model development, and as a basis for novel solver development, but do not yet match Tier 1 codes in the breadth of built-in Cz-specific physics.

---

## 13. Key Research Groups and Institutions

The following centres have made sustained contributions to Cz simulation methodology:

- **Leibniz-Institut für Kristallzüchtung (IKZ), Berlin** — NEMOCRYS project, opencgs, model experiment validation (Dadzis, Wintzer, Enders-Seidlitz)
- **Fraunhofer IISB, Erlangen** — CrysVUn++, STHAMAS, CrysMAS (Friedrich, Jung, Hainke, Müller)
- **STR Group (str-soft.com)** — CGSim commercial development and maintenance
- **FEMAGSoft / UCLouvain, Belgium** — FEMAG/CZ (Dupret group)
- **University of Kyushu / Kyushu University** — Kakimoto group; large body of work on 3D transient silicon Cz simulation and point defect modelling
- **Institute for Problems in Mechanics, Russian Academy of Sciences** — Prostomolotov, Verezub; CrystmoNet framework
- **University of Minnesota (Derby group)** — Cats2D, GSMAC-FEM; foundational thermal-capillary models
- **University of Latvia (Virbulis, Sabanskis group)** — FZ and Cz modelling; point defect simulations using published parameter sets

---

## 14. Conclusions and Outlook

Cz simulation software has matured to a point where global 2D axisymmetric heat transfer models with turbulent melt convection, oxygen transport, and V/G-based defect prediction are routine capabilities in the industrial codes. The principal remaining challenges are:

1. **Turbulent melt flow in large-diameter pullers** — LES is too expensive for production use; better RANS closures validated against experiment remain an open problem.
2. **Full 3D transient simulation** — required for accurate MHD studies and crystal diameter control, but computationally prohibitive at production scale without HPC resources.
3. **Validation with in-situ data** — the NEMOCRYS model-experiment approach is a partial solution; extending it to silicon remains difficult owing to temperature and opacity constraints.
4. **Open reproducibility** — the gap between industrial validation (proprietary) and academic validation (public) remains large. The opencgs framework is narrowing this gap but has not yet reached feature parity with commercial Tier 1 codes.
5. **Integration of ML with physics** — the most promising near-term path is hybrid models where physics-based simulation generates training data for fast surrogate models, with online ML used for real-time diameter and quality control.

The publication activity in the *Journal of Crystal Growth*, *Journal of Physics: Conference Series*, and *AIP Advances* through 2024–2025 shows no sign of saturation, driven by the expanding material palette (β-Ga₂O₃, halide perovskites, wide-bandgap nitrides) and by the continuing demand for larger, more defect-free silicon ingots for advanced semiconductor nodes.

---

## References and Further Reading

The following sources were consulted in preparing this report and represent the current primary literature:

- STR Group. *CGSim: Crystal Growth Simulator*. https://str-soft.com/software/cgsim/ (v26.1, 2025)
- FEMAGSoft. *FEMAG/CZ Product Page*. https://www.femagsoft.com/products/femag-cz.html (2025)
- Fraunhofer IISB. *CrysMAS Documentation*. https://download.iisb.fraunhofer.de/downloads/Manual/index.html
- NEMOCRYS / IKZ Berlin. *opencgs*. https://github.com/nemocrys/opencgs (v1.0.1)
- NEMOCRYS / IKZ Berlin. *nemoFoam-utils*. https://github.com/nemocrys/nemoFoam-utils
- Wintzer, A. et al. (2025). "Validation of a numerical model for Czochralski growth of caesium iodide and calcium fluoride." *Journal of Crystal Growth*, 661, 128155.
- Wintzer, A. (2024). "Validation of multiphysical models for Czochralski crystal growth." PhD thesis, TU Berlin. DOI: 10.14279/depositonce-20957
- Enders-Seidlitz, A. et al. (2022). "Development and validation of a thermal simulation for the Czochralski crystal growth process using model experiments." *Journal of Crystal Growth*, 593, 126750.
- Zhang, W. et al. (2025). "Simulation of oxygen and carbon impurity transport during magnetically controlled Czochralski silicon growth." *AIP Advances*, 15(1), 015103.
- Dezfoli, A.R.A. et al. (2025). "Data-driven approach for optimizing the Czochralski process and predictive modeling: A finite element and machine learning analysis." *International Journal of Advanced Manufacturing Technology*.
- Friedrich, J. et al. (2020). "Erlangen — An Important Center of Crystal Growth and Epitaxy." *Crystal Research and Technology*, 55. DOI: 10.1002/crat.201900053
- Li, Z. & Smirnov, A. (2023). "Application of computer modeling to pulling rate and productivity of Czochralski pullers in PV Si crystal growth." *Journal of Crystal Growth*, 611, 127178.
- Mukaiyama, Y. et al. (2024). *Journal of Crystal Growth*, 646, 127861.
- Lou, Z. et al. (2022). *Journal of Crystal Growth*, 595, 126814.
- Voronkov, V.V. (1982). "The mechanism of swirl defects formation in silicon." *Journal of Crystal Growth*, 59, 625–643. [Foundational V/G theory]
- Derby, J.J. & Brown, R.A. (1986). "Thermal-capillary analysis of Czochralski and liquid encapsulated Czochralski crystal growth." *Journal of Crystal Growth*, 74, 605–624. [Foundational thermal-capillary model]

---

> [!NOTE]
> 
> Generated by Claude.ai
>
> Model: Sonet 4.6
>
> Prompt: Prepare a thorough, detailed technical report on the software for modeling the Czochralski crystal growth process.
> The technical report must comprehensively address the current state of affairs.
> It must be exhaustive and wide-ranging.
> Before writing, use a web search to verify the current names of products, apps, announcements, and documentation URLs.
> Show output in Markdown format.

