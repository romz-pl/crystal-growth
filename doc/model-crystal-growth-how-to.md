# How Crystal Growth Can Be Modelled Numerically

Crystal growth spans an enormous range of length and time scales — from the attachment of individual atoms to a growth interface (sub-nanometer, picoseconds) up to the global heat, mass, and momentum transport in a meter-scale industrial furnace (meters, hours to weeks). No single numerical method covers this whole range, so crystal growth modelling is best understood as a **hierarchy of coupled methods**, each targeting a different scale, plus a set of **cross-cutting numerical techniques** (interface tracking, multiphysics coupling, optimization) used to connect them.

This document organizes the field by scale, then by method, and closes with a chronological bibliography.

---

## 1. Overview: The Multiscale Picture

Melt and solution crystal growth processes are conventionally described across three regimes:

- **Microscopic scale (≲ tens of nm):** ab initio and classical **molecular dynamics (MD)** resolve individual atomic motion, bonding, and attachment kinetics at the growth interface.
- **Mesoscale (hundreds of nm to tens of µm):** **kinetic Monte Carlo (kMC)** and lattice-based methods extend the accessible time and length scale beyond what MD allows, capturing step-flow, nucleation, and surface roughening.
- **Macroscopic scale (tens of µm and larger):** **continuum transport models** (heat, mass, momentum, electromagnetics, radiation) describe the furnace-scale process — this is where most industrial crystal growth simulation work is concentrated.

This scale-based decomposition, along with the observation that phenomena at the "meso-scale" bridge discrete and continuum descriptions, is explicitly laid out in review treatments of melt and solution growth modelling.

---

## 2. Continuum (Macroscopic) Models of Melt/Solution Growth

### 2.1 Governing equations
Continuum models solve coupled partial differential equations for:
- **Heat transfer** (conduction, convection, and — critically for high-temperature melt growth — **radiation**, including view-factor calculations between furnace surfaces)
- **Momentum/fluid flow** (Navier–Stokes, often with turbulence closure)
- **Species/mass transport** (dopant, solute, or impurity transport)
- **Electromagnetics** (for RF/induction heating, magnetic damping of melt flow)
- **Interface/phase-change tracking** (crystal–melt boundary position, often via a pseudo-steady or moving-mesh formulation)

### 2.2 Discretization approaches
- **Finite element method (FEM):** the dominant approach for global, quasi-steady axisymmetric (2D) models of furnace-scale heat/mass transfer, and used heavily in Czochralski (CZ) global simulations to resolve heater power, interface shape, and oxygen transport.
- **Finite volume/control-volume method:** used for coupled radiative-convective-conductive global simulations, including mixed 2D/3D domain decomposition strategies that keep 3D global CZ simulations computationally tractable.
- **Open-source multiphysics toolchains:** recent work couples **Elmer** (electromagnetics, steady-state heat transfer, phase change) with **OpenFOAM** (transient/turbulent melt flow) to build validated, reproducible 2D/3D Czochralski models — an example of combining specialized open-source solvers rather than a single monolithic code.

### 2.3 Turbulence and flow instability treatment
Because industrial melt volumes have high Rayleigh/Grashof numbers, melt convection is turbulent, and three approaches are used, roughly in order of increasing cost:
- **k–ε (RANS) turbulence models** for time-averaged thermal fields — validated against production-scale CZ silicon pullers by comparing measured and modelled temperature fluctuations with rotation rate.
- **Large-eddy simulation (LES)** combined with a 2D global heat/mass transport model, used to predict unsteady melt convection and impurity (oxygen) transport without the prohibitive cost of resolving all turbulent scales.
- **Direct numerical simulation (DNS)**, in principle the most accurate, but explicitly noted as too computationally expensive for industrial-scale Rayleigh numbers and realistic furnace geometry — largely reserved for idealized/simplified geometries.

### 2.4 Representative application: Czochralski (CZ) growth
CZ modelling has arguably the richest continuum-modelling literature of any growth method because of its industrial importance (silicon photovoltaics/microelectronics). Key modelling threads include:
- **Global heat transfer models** incorporating diffuse-gray radiation exchange, used to reproduce heater power and interface shape trends against experiment.
- **Lumped-parameter and reduced-order models** for predicting oxygen concentration, built from and validated against full 2D thermal-capillary and 3D LES models — illustrating a common pattern where expensive high-fidelity simulations are used to calibrate cheaper surrogate models for process control.
- **Magnetic field effects:** modelling of traveling magnetic fields (via internal heater-magnet modules) and cusp/axial magnetic fields to damp turbulent melt oscillations and stabilize the growth interface.
- **Hot-zone component-level detail:** e.g., 3D global models explicitly including heater electrodes (previously omitted in simpler 2D models) to quantify their contribution to heat losses.
- **Model validation** remains a persistent challenge; several papers explicitly note that many published CZ models lack sufficient in-situ measurement data for rigorous validation, motivating open-source, well-instrumented benchmark models (e.g., using tin as a validation analogue, or CsI/CaF₂ systems).

### 2.5 Other melt/solution growth configurations
The same continuum-modelling toolkit (FEM/FVM heat-mass-momentum solvers, radiation view factors, turbulence closures) is applied, with method-specific geometry and boundary conditions, to:
- **Bridgman / vertical gradient freeze (VGF)** growth
- **Kyropoulos and LEC (liquid-encapsulated Czochralski)** growth
- **Ammonothermal growth** (e.g., GaN), where a multi-physics model incorporating mass transport through a porous nutrient basket has been used to analyze scale-up to large-diameter crystals.
- **Protein crystallization**, where diffusive-field models (rather than convective/turbulent ones, since gravity-driven convection is largely absent in microgravity) are used to compare terrestrial vs. microgravity growth kinetics.

---

## 3. Interface-Capturing and Interface-Tracking Methods

A central numerical difficulty in crystal growth is that the solid–liquid interface **moves and deforms** as a consequence of the solution itself (a free-boundary / Stefan problem). Three broad families of numerical treatment exist.

### 3.1 Sharp-interface (front-tracking) methods
The interface is represented explicitly (e.g., as a parametrized curve/surface or an evolving mesh) and tracked directly.
- Early front-tracking work applied moving/adaptive triangulation schemes and boundary-integral formulations to resolve dendritic and unstable solidification fronts without needing to separately compute curvature and normal vectors, borrowing numerical structure from vortex methods in fluid dynamics.
- Later parametric finite-element approaches extended front-tracking to curvature-driven interface evolution, with a lineage of related work spanning explicit front-tracking, boundary-integral, and adaptive finite-element treatments of crystal growth interfaces.
- **Trade-off:** high geometric accuracy per interface point, but topological changes (merging, splitting of dendrite arms) require special handling.

### 3.2 Level-set methods
The interface is represented implicitly as the zero contour of a signed distance (or other) function defined over the whole domain, which is then advected.
- The **level-set method for Stefan problems** was formulated to handle solid/liquid boundary motion incorporating anisotropy, surface tension, molecular kinetics, and undercooling, recasting the moving-boundary problem via a history-dependent boundary integral and non-oscillatory (ENO-type) schemes to capture sharp gradients and cusps.
- A simplified, widely cited level-set scheme couples an implicit finite-difference heat equation solver with level-set front capture, validated by matching measured dendrite tip speeds (e.g., in succinonitrile) under grid refinement.
- Extensions include adaptive, non-graded Cartesian grid level-set methods for improved accuracy and efficiency, vector Stefan problems for multi-component alloy dissolution, and — most recently — **deep learning-augmented level-set methods**, where a neural network approximates the front velocity within the level-set evolution equation.
- **Key advantage over pure front-tracking:** topological changes (branch splitting/merging in dendrites) are handled naturally since the interface is not explicitly parametrized.

### 3.3 Phase-field (diffuse-interface) methods
The interface is replaced by a thin diffuse region described by a continuous order parameter (phase field) that varies smoothly between solid and liquid values, governed by a Ginzburg–Landau-type equation coupled to a heat/solute diffusion equation.
- **Foundational theory** predates numerical dendrite simulation: diffuse-interface free-boundary models were formalized in the early-to-mid 1980s, including phase-field methods for free-boundary problems and diffuse-interface models of diffusion-limited crystal growth, followed by rigorous asymptotic analyses connecting phase-field equations to sharp-interface (Stefan/Hele-Shaw) limits.
- **The breakthrough for morphological realism** came with Kobayashi's 1993 model, which introduced interface anisotropy directly into the phase-field formulation and was the first to successfully reproduce the characteristic four- and six-fold symmetric dendrite morphology in simulation; this paper is credited with triggering the subsequent exponential growth in phase-field literature.
- **Quantitative phase-field methods** (Karma and Rappel, mid-to-late 1990s) reformulated the thin-interface asymptotics so that phase-field simulations could be made computationally efficient at realistic (small) interface widths relative to the diffusion length, while still recovering the correct sharp-interface kinetics — a major advance for making phase-field simulation quantitatively predictive rather than only qualitatively correct.
- **Numerical solution strategies** for the coupled, nonlinear, anisotropic phase-field/heat (or phase-field/solute) system include:
  - Explicit and semi-implicit finite-difference schemes on regular grids
  - Adaptive mesh refinement to resolve the thin diffuse interface efficiently, since phase-field computations otherwise require very fine lattices, which historically limited practical simulations to 2D or small 3D domains
  - High-order, energy-stable time-stepping schemes, including SAV (scalar auxiliary variable)-based and BDF-based decoupled schemes designed to allow larger, stable time steps for the stiff, coupled nonlinear system
  - GPU-accelerated large-scale simulations (e.g., directional solidification of binary alloys on GPU supercomputers), needed to push phase-field simulation toward the many-dendrite, practical-microstructure regime
  - Coupling with **lattice Boltzmann methods** to include melt convection self-consistently with dendrite growth
- **Extensions:** binary/multicomponent alloy solidification (coupling temperature and solute fields), eutectic growth, high-velocity solute trapping, fracture-coupled phase-field models, and pore-scale freezing/thawing problems.

### 3.4 Comparative assessment
Direct comparisons of phase-field versus parametric front-tracking approaches have examined accuracy and computational efficiency trade-offs; broadly, front-tracking/level-set methods offer sharper, more geometrically precise interfaces at the cost of handling topological change and curvature computation explicitly, while phase-field methods trade some sharpness (and finer mesh requirements near the interface) for natural handling of complex, changing dendrite topology and easier coupling to additional physics (elasticity, convection, multiple order parameters).

---

## 4. Atomistic and Mesoscale Methods

### 4.1 Molecular dynamics (MD)
- Ab initio and classical-potential MD resolve atomic-scale attachment/detachment kinetics at the growth interface, including solvation effects for growth from solution.
- **Fundamental limitation:** direct MD simulation of crystal growth is impractical beyond a few thousand atoms and a few nanoseconds — far short of the size and time scales needed to observe morphologically meaningful growth, since even the fastest-growing molecular crystals require much larger ensembles and longer times than MD can directly reach.
- MD's practical role in the multiscale hierarchy is therefore usually to **parametrize** faster coarse-grained methods (e.g., extracting attachment/detachment rate constants for kinetic Monte Carlo), rather than to simulate bulk crystal growth directly.

### 4.2 Kinetic Monte Carlo (kMC)
kMC advances a lattice (or off-lattice) representation of the crystal surface stochastically, using precomputed or MD-derived rate constants for elementary events (adsorption, desorption, surface diffusion, edge diffusion), allowing access to micrometer length scales and millisecond-or-longer timescales unreachable by MD.
- **Solution growth:** kMC parametrized by atomistic MD has been used to study organic/molecular crystal growth and dissolution from solvent (e.g., urea from water/methanol), capturing solvation effects on growth kinetics while reaching experimentally relevant length and time scales.
- **Surface/step models:** solid-on-solid lattice models with explicit surface reconstruction have been used to study crystal growth mechanisms, including the transition between two-dimensional nucleation-dominated growth and multi-nucleation regimes as a function of supersaturation.
- **Epitaxial and heteroepitaxial growth:** off-lattice kMC has been applied to strained heteroepitaxial growth, and specialized kMC formulations handle long-range Coulomb interactions for ordering in ferroelectric alloy growth, or vdW epitaxy of 2D transition-metal-dichalcogenide layers where conventional epitaxial growth theory does not directly apply.
- **Coupling to first-principles methods:** DFT-derived energetics are increasingly used to parametrize kMC rate catalogs, particularly for novel/2D materials where empirical potentials are not well established.

---

## 5. Cross-Cutting Numerical Considerations

- **Multiphysics coupling architecture:** most modern global furnace models are not single-code monoliths but couple specialized solvers — e.g., electromagnetics + heat transfer + phase change in one tool, coupled to a CFD solver for turbulent melt flow in another — requiring careful interface/boundary-condition exchange between codes.
- **Model reduction / surrogate modelling:** because full 3D transient global simulations remain very expensive, physically-based lumped-parameter and reduced-order models (calibrated against full simulations) are used for near-real-time process monitoring and control, e.g., of oxygen incorporation in CZ silicon.
- **Validation methodology:** a recurring theme across the continuum-modelling literature is the scarcity of well-instrumented in-situ experimental data for validating global furnace models, motivating dedicated model experiments (e.g., transparent low-melting-point analog materials) and open-source, reproducible model codes.
- **Machine learning augmentation:** recent numerical crystal-growth modelling increasingly incorporates data-driven components — deep-learning-augmented level-set velocity fields, and broader calls (e.g., in dedicated journal special issues) to extend classical numerical methods with big-data/ML approaches for optimization of industrial growth processes.

---

## 6. Chronological Bibliography

1. Fix, G. (1983). *Phase field methods for free boundary problems.* In: Fasano, A., Primicerio, M. (Eds.), *Free Boundary Problems: Theory and Applications*, Pitman, London.
2. Collins, J.B., Levine, H. (1985). *Diffuse interface model of diffusion-limited crystal growth.* Physical Review B, 31(9), 6119.
3. Caginalp, G. (1986). *An analysis of a phase field model of a free boundary.* Archive for Rational Mechanics and Analysis, 92(3), 205–245.
4. Caginalp, G. (1989). *Stefan and Hele-Shaw type models as asymptotic limits of the phase-field equations.* Physical Review A, 39(11), 5887.
5. Sethian, J.A., Strain, J. (1992). *Crystal growth and dendritic solidification* [analysis of the Stefan problem with a level-set/boundary-integral method]. Journal of Computational Physics.
6. Kobayashi, R. (1993). *Modeling and numerical simulations of dendritic crystal growth.* Physica D: Nonlinear Phenomena, 63(3–4), 410–423.
7. Wheeler, A.A., Murray, B.T., Schaefer, R.J. (1993). *Phase-field model for isothermal phase transitions in binary alloys.* Physica D, 66, 243–262.
8. Kobayashi, R. (1994). *A numerical approach to three-dimensional dendritic solidification.* Experimental Mathematics, 3(1), 59–81.
9. Boettinger, W.J., Warren, J.A. (1996). *The phase-field method: simulation of alloy dendritic solidification during recalescence.* Metallurgical and Materials Transactions A.
10. Karma, A., Rappel, W.-J. (1996). *Numerical simulation of three-dimensional dendritic growth.* Physical Review Letters, 77, 4050–4053.
11. Chen, S., Merriman, B., Osher, S., Smereka, P. (1997). *A simple level set method for solving Stefan problems.* Journal of Computational Physics, 135(1), 8–29.
12. Karma, A., Rappel, W.-J. (1998). *Quantitative phase-field modeling of dendritic growth in two and three dimensions.* Physical Review E, 57(4), 4323.
13. Karma, A., Rappel, W.-J. (1999). *Phase-field model of dendritic sidebranching with thermal noise.* Physical Review E, 60(4), 3614.
14. Kim, Y.-T., Provatas, N., Goldenfeld, N., Dantzig, J. (1999). *Universal dynamics of phase-field models for dendritic growth.* Physical Review E, 59(3), R2546.
15. Derby, J.J., et al. (2002). *Radiative heat exchange in Czochralski crystal growth* [review of hot-zone design, active growth control, and morphological simulation in CZ modelling]. International Journal of Heat and Mass Transfer.
16. Vartak, B.J., et al. (2005). *A mixed 2D/3D global simulation method for Czochralski furnace heat transfer.* (3D global CZ silicon simulation with mixed-dimension discretization.)
17. Kotake, Y., et al. (2005–2006). *Kinetic Monte Carlo simulation of the growth kinetics and morphology of crystal growth from solution.* Journal of Crystal Growth.
18. Piana, S., Reyhani, M., Gale, J.D. (2006). *Three-dimensional kinetic Monte Carlo simulation of crystal growth from solution.* Journal of Crystal Growth / related communications, using MD-derived rate parameters for urea crystallization kinetics.
19. Sanaki, T., et al. (2007). *Numerical model of protein crystal growth in a diffusive field such as the microgravity environment.*
20. Miller, W., Rudolph, P., et al. (2008–2009). *Numerical simulation of Czochralski crystal growth under the influence of a traveling magnetic field generated by an internal heater-magnet module.* Journal of Crystal Growth; Magnetohydrodynamics.
21. Dreyer, W., Druet, P.-É., Klein, O., Sprekels, J. (2012). *Mathematical modeling of Czochralski type growth processes for semiconductor bulk single crystals.* Milan Journal of Mathematics, 80, 311–332.
22. Barrett, J.W., Garcke, H., Nürnberg, R. (2013–2014). *Parametric finite element approximations of curvature-driven interface evolutions* [including surveys of front-tracking approaches to crystal growth]. 
23. Steinbach, I. (2013). *Why solidification? Why phase-field?* JOM, 65(9), 1096–1102.
24. Sanal, R. (2014). *Numerical simulation of dendritic crystal growth using phase field method and investigating the effects of different physical parameters on the growth of the dendrite.* arXiv:1412.3197.
25. Takaki, T., Rojas, R., Ohno, M. (2015). *A phase-field-lattice Boltzmann method for modeling motion and growth of a dendrite for binary alloy solidification in the presence of melt convection.* Journal of Computational Physics, 298, 29–40.
26. Nguyen, V.T., et al. (2016). *A kinetic Monte Carlo simulation method of van der Waals epitaxy for atomistic nucleation-growth processes of transition metal dichalcogenides.* Scientific Reports.
27. Aoki, T., et al. (2014, published 2016). *Phase-field modeling and simulations of dendrite growth* [review including GPU-accelerated large-scale directional solidification simulations]. ISIJ International, 54(2), 437.
28. Zhou, X., et al. (2018). *Global model of Czochralski silicon growth to predict oxygen content and thermal fluctuations at the melt–crystal interface* [2D global model coupled with LES of turbulent melt flow]. Journal of Crystal Growth.
29. Zhao, D., et al. (2018). *Second order front tracking algorithm for Stefan problem on a regular grid.* arXiv:1804.06107.
30. Głowinski, R., et al. (2019). *Thin interface limit for phase-field models of solidification with local mobility correction.* arXiv:1905.02965.
31. Guo, Y., Azaïez, M., Xu, C. (2023). *An efficient numerical method for the anisotropic phase field dendritic crystal growth model.* arXiv:2310.10506.
32. Li, X., et al. (2021). *Physically-based, lumped-parameter models for the prediction of oxygen concentration during Czochralski growth of silicon crystals.* Journal of Crystal Growth.
33. Su, K., et al. (2022). *Large-sized GaN crystal growth analysis in an ammonothermal system based on a well-developed numerical model.* Materials (MDPI), PMC9231043.
34. Engineering with Computers review (2022). *Modeling of dendritic solidification and numerical analysis of the phase-field approach to model complex morphologies in alloys.* Engineering with Computers.
35. Neubauer, A., et al. (2022). *Development and validation of a thermal simulation for the Czochralski crystal growth process using model experiments.* Journal of Crystal Growth.
36. Zhang, L., et al. (2024). *Three-dimensional phase-field simulations of water freezing and thawing at pore-scale.* arXiv:2401.01672.
37. Berthier, F., et al. (2024). *Deep level-set method for Stefan problems.* Journal of Computational Physics.
38. Neubauer, A., et al. (2025). *Validation of a numerical model for Czochralski growth of cesium iodide and calcium fluoride* [open-source Elmer + OpenFOAM coupled model]. Journal of Crystal Growth.
39. Wang, H., et al. (2025). *Investigation of the effect of heater electrode heat transfer on heat losses in Czochralski silicon crystal growth based on 3D global numerical simulation.* Journal of Crystal Growth.
40. Guo, Y., Azaïez, M., Xu, C. (2026, arXiv preprint). *A fully-decoupled arbitrarily high-order time-stepping scheme based on matrix diagonalization for the anisotropic phase-field dendritic crystal growth model.* arXiv:2606.25345.

*Note on dating:* Several entries (particularly early front-tracking, level-set, and CZ global-model papers) are dated from citation context within later works rather than from direct access to the original publication, since not every original source was independently retrievable during research; years should be treated as best-available estimates for ordering purposes, and cross-checked against original journal records where precision matters.

---

## 7. Practical Takeaway

If the goal is to **simulate a specific furnace/growth run** (CZ, Bridgman, LEC, ammonothermal, etc.), the relevant toolkit is continuum multiphysics: FEM/FVM heat-mass-momentum solvers, radiation view factors, and a turbulence closure (RANS/LES/DNS depending on budget) — often assembled from coupled open-source tools (Elmer, OpenFOAM) rather than one monolithic code.

If the goal is **microstructure/morphology prediction** (dendrite shape, sidebranching, alloy segregation patterns), phase-field methods are the current standard, with level-set and front-tracking as sharper-interface alternatives, chosen based on whether topological change (branch merging) or interface sharpness matters more for the application.

If the goal is **understanding atomic-scale attachment kinetics or novel-material nucleation** (2D materials, epitaxy, growth from solution), MD (for rate parametrization) feeding into kinetic Monte Carlo is the standard multiscale bridge.

---

> [!NOTE]
> 
> Generated by Claude.ai
>
> Model: Sonet 5
>
> Prompt: Create an exhaustive and detailed answer on the following question: "How can crystal growth be modelled numerically?". Show the output in Markdown format and sort the articles chronologically. Do not copy the output of the exported files into the chat.
