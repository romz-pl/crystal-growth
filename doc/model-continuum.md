# History of Numerical Continuum (Macroscopic) Models of Melt/Solution Growth

## Scope and Definition

Continuum (macroscopic) models describe melt- and solution-growth crystal growth processes at length scales of tens of microns and larger, in contrast to atomistic (molecular dynamics), kinetic Monte Carlo, and phase-field/mesoscale descriptions. They are built on the classical transport equations of continuum mechanics — conservation of mass, momentum, energy, and species — coupled with:

- **Free/moving boundary conditions** at the melt/crystal interface (Stefan-type energy balance, local thermodynamic equilibrium, Gibbs–Thomson undercooling, kinetic attachment laws);
- **Free-surface (meniscus) conditions** governed by capillarity (Young–Laplace equation) for methods with a free melt surface (Czochralski, floating zone);
- **Global heat transfer** in the furnace/hot-zone, including conduction, convection (often turbulent), and radiative exchange between diffuse-gray or specular surfaces;
- **Species/solute transport and segregation**, including diffusion boundary layers and effective segregation coefficients;
- **Applied body forces**, notably buoyancy (natural convection), Marangoni (thermocapillary) stresses, crucible/crystal rotation (forced convection, Coriolis effects), and electromagnetic (Lorentz) forces from static, rotating, or traveling magnetic fields used for melt flow damping/control.

These continuum descriptions are solved numerically using finite difference (FD), finite volume (FVM), finite element (FEM), spectral, and hybrid FVM/FEM or lattice-Boltzmann methods, and constitute the physical/numerical basis of major crystal-growth simulation packages (CGSim, STHAMAS/FEMAG-CZ, CrysMAS, CrysVUn, Cats2D, and commercial CFD codes such as ANSYS Fluent, STAR-CD, and ABAQUS adapted to growth problems).

The literature below is organized chronologically and spans: (1) foundational finite-difference/finite-element continuum formulations of Czochralski (CZ) melt convection; (2) thermal-capillary and global-furnace heat-transfer models; (3) turbulence modeling in large-scale CZ melts; (4) magnetic-field-assisted continuum models; (5) Bridgman/vertical-gradient-freeze (VGF) and floating-zone continuum models; (6) solutal transport, segregation, and macrosegregation continuum theory; and (7) modern review articles and general-purpose simulation software descriptions.

---

## Chronological Bibliography

### 1975

**Kobayashi, N., Arizumi, T.** — *"Computational Analysis of the Flow in a Crucible."* *Journal of Crystal Growth*, 30, 177–184.
One of the earliest numerical (finite-difference) continuum treatments of buoyancy- and rotation-driven flow in a Czochralski crucible, establishing the axisymmetric Navier–Stokes/energy formulation later used throughout the field.

### 1980

**Kobayashi, N.** — *"Computer Simulation of Heat, Mass and Fluid Flows in a Melt during Czochralski Crystal Growth."* *Computer Methods in Applied Mechanics and Engineering*, 23, 21–33.
Extends the continuum axisymmetric formulation to coupled heat, mass (dopant), and momentum transport, an early integrated continuum model of CZ growth.

### 1981

**Kobayashi, N.** — *"Heat Transfer in Czochralski Crystal Growth,"* in W. R. Wilcox (ed.), *Preparation and Properties of Solid State Materials*, Vol. 6, Marcel Dekker, New York, pp. 119–253.
A comprehensive early review chapter establishing the continuum heat-transfer framework (conduction, convection, radiation) for CZ furnaces, widely cited as a foundational reference in subsequent numerical studies.

### 1983

**Jones, A. D. W.** — *"An Experimental Model of the Flow in Czochralski Growth."* *Journal of Crystal Growth*, 61, 235–244.
Combined experimental/continuum-modeling study validating buoyancy-driven flow predictions against physical (water/gallium) model experiments.

**Langlois, W. E., Lee, K.** — *"Digital Simulation of Magnetic Czochralski Flow under Various Laboratory Conditions for Silicon Growth."* *IBM Journal of Research and Development*, 27(3), 281–284.
Early continuum (MHD-Navier–Stokes) numerical treatment of magnetic damping of melt convection in CZ silicon growth.

### 1984

**Mihelčić, M., Wingerath, K., Pirron, C.** — *"Three-Dimensional Simulation of the Czochralski Bulk Flow."* *Journal of Crystal Growth*, 69, 473–488.
Full 3-D continuum (finite-difference) simulation of CZ melt flow, moving beyond axisymmetric approximations to capture genuinely three-dimensional buoyancy/rotation interactions.

### 1985

**Derby, J. J., Brown, R. A., Geyling, F. T., Jordan, A. S., Nikolakopoulou, G. A.** — *"Finite Element Analysis of a Thermal-Capillary Model for Liquid Encapsulated Czochralski Growth."* *Journal of the Electrochemical Society*, 132, 470–482.
A landmark finite-element continuum formulation coupling global heat transfer, capillary free-surface shape (meniscus and encapsulant), and the melt/crystal interface shape — the "thermal-capillary model" that became a standard continuum framework for LEC/CZ growth simulation.

### 1987

**Derby, J. J., Atherton, L. J., Thomas, P. D., Brown, R. A.** — *"Finite Element Methods for Analysis of the Dynamics and Control of Czochralski Crystal Growth."* *Journal of Scientific Computing*, 2, 297–343.
Develops Newton-based finite-element continuation and dynamic (transient) simulation methods for continuum thermal-capillary CZ models, enabling parametric/bifurcation studies and control analysis.

**Hurle, D. T. J.** — *"The Evolution and Modelling of the Czochralski Growth Technique."* *Journal of Crystal Growth*, 85, 1–8.
Historical and conceptual overview tracing the development of continuum modeling approaches for CZ growth from analytical approximations to numerical global models.

### 1988

**Bottaro, A., Zebib, A.** — *"Bifurcation in Axisymmetric Czochralski Natural Convection."* *Physics of Fluids*, 31, 495–501.
Continuum stability/bifurcation analysis of buoyancy-driven axisymmetric CZ melt flow, identifying transition Rayleigh numbers for onset of unsteady convection.

### 1989

**Bottaro, A., Zebib, A.** — *"Three-Dimensional Thermal Convection in Czochralski Melt."* *Journal of Crystal Growth*, 97, 50–58.
Extension of the continuum stability analysis to fully 3-D thermal convection, showing symmetry-breaking instabilities relevant to melt/crystal interface non-uniformities.

**Derby, J. J., Atherton, L. J., Gresho, P. M.** — Global analysis of heat transfer in Czochralski crystal growth (as cited widely in later "global heat transfer" literature, e.g., in oxide-crystal CZ studies).
Establishes the "global analysis of heat transfer" methodology — simultaneous continuum solution of conduction, convection, and radiation throughout the entire growth furnace rather than the melt domain alone — which became the standard approach for industrial-scale CZ simulation.

**Sackinger, P. A., Brown, R. A., Derby, J. J.** — *"A Finite Element Method for Analysis of Fluid Flow, Heat Transfer and Free Interfaces in Czochralski Crystal Growth."* *International Journal for Numerical Methods in Fluids*, 9, 453–492.
A rigorous finite-element continuum algorithm for simultaneous computation of steady axisymmetric melt flow, temperature field, and coupled crystal/melt and melt/ambient (meniscus) interface shapes; a key methodological reference for thermal-capillary continuum models.

### 1990

**Sabhapathy, P.** (and co-workers) — *"Natural Convection in Liquid Encapsulated Czochralski Growth of Gallium Arsenide."* *The Canadian Journal of Chemical Engineering*, 68, 1990.
Continuum numerical study of buoyancy-driven convection in LEC GaAs growth, examining sensitivity to crucible/crystal radii and melt height.

### 1991

**Ozoe, H., Toh, K., Inoue, T.** — *"Transition Mechanism of Flow Modes in Czochralski Convection."* *Journal of Crystal Growth*, 110, 472–480.
Continuum numerical study identifying the mechanisms of transition between axisymmetric, three-dimensional, and time-dependent flow modes in CZ melts as a function of Grashof/Reynolds numbers.

### 1992

**Hirata, H., Hoshikawa, K.** — *"Three-Dimensional Numerical Analyses of the Effect of a Cusp Magnetic Field on the Flows, Oxygen Transport and Heat Transfer in a Czochralski Silicon Melt."* *Journal of Crystal Growth*, 125, 181–207.
Continuum MHD model coupling melt convection, oxygen (solute) transport, and heat transfer under a cusp-shaped magnetic field, relevant to industrial silicon CZ growth control.

**Leister, H.-J., Perić, M.** — *"Numerical Simulation of a 3D Czochralski-Melt Flow by a Finite Volume Multigrid Algorithm."* *Journal of Crystal Growth*, 123, 567–574.
Introduces an efficient finite-volume multigrid continuum solver for 3-D CZ melt flow, improving computational tractability of large-scale transient simulations.

**Mihelčić, M., Wenzl, H., Wingerath, K.** — *"Flow in Czochralski Crystal Growth Melts,"* Technical Report, Institut für Festkörperforschung, Forschungszentrum Jülich.
Continuum flow simulation report contributing to the systematic characterization of CZ melt convection regimes.

### 1993

**(Combined FE/FV global model)** — *"Global Simulation of Heat Transport, Including Melt Convection in a Czochralski Crystal Growth Process—Combined Finite Element/Finite Volume Approach."* *Journal of Crystal Growth* / related proceedings.
Couples a finite-element (ABAQUS) global radiation–conduction continuum solver with a finite-volume (STAR-CD) melt-convection solver for LEC/CZ furnaces, validated against a graphite-dummy/gallium model experiment — an early hybrid-method global continuum model.

### 1994

**Seidl, A., McCord, G., Müller, G., Leister, H.-J.** — *"Experimental Observation and Numerical Simulation of Wave Patterns in a Czochralski Silicon Melt."* *Journal of Crystal Growth*, 137, 326–334.
Continuum (finite-volume) simulation and experimental validation of azimuthal wave instabilities in CZ silicon melt convection.

### 1995

**Sung, H. J., Jung, Y. J., Ozoe, H.** — *"Prediction of Transient Oscillating Flow in Czochralski Convection."* *International Journal of Heat and Mass Transfer*, 38, 1627–1636.
Transient continuum simulation resolving oscillatory buoyancy-driven convection in CZ melts, relevant to striation formation.

### 1997 (approx.)

**Lipchin, A., Brown, R. A., Yakhot, V.** — *"Forced and Thermocapillary Convection in Silicon Czochralski Crystal Growth in Semispherical Crucible."* *Journal of Crystal Growth* (in press per contemporaneous citation, ~2000).
Continuum RANS-based turbulence model applied to thermocapillary and forced convection in CZ silicon growth with non-standard (semispherical) crucible geometry.

### 2000

**Lipchin, A., Brown, R. A.** — *"Hybrid Finite-Volume/Finite-Element Simulation of Heat Transfer and Melt Turbulence in Czochralski Crystal Growth of Silicon."* *Journal of Crystal Growth*, 216, 192–203.
A key methodological paper combining finite-element simulation of the thermal-capillary interface/meniscus model with finite-volume solution of the low-Reynolds-number Jones–Launder k–ε turbulence model, enabling coupled global heat transfer and turbulent melt convection simulation for industrial-scale silicon CZ growth.

**Numerical Simulation of Fluid Flow and Heat Transfer in an Industrial Czochralski Melt Using a Parallel-Vector Supercomputer** (Springer proceedings chapter).
Demonstrates large-scale (720,896 control-volume), block-structured, parallel continuum simulation of an industrial CZ ellipsoidal-crucible melt, comparing k–ε turbulence-modeled versus fully time-dependent 3-D laminar/transitional results.

### 2001

**Nikitin, N., Polezhaev, V.** — *"Direct Simulations and Stability Analysis of the Gravity Driven Convection in a Czochralski Model."* *Journal of Crystal Growth*, 230, 30–39.
High-fidelity continuum direct numerical simulation (DNS) and linear stability analysis of buoyancy-driven CZ melt convection, providing benchmark data for turbulence/instability onset.

### 2002

**(Numerical study of CACRT)** — *"Numerical Simulation of Free and Forced Convection in the Classical Czochralski Method and in CACRT."* *Journal of Crystal Growth* (2002 issue, referencing Kobayashi, Langlois, Mihelčić, Scheel).
Finite-element continuum thermal-capillary simulations comparing standard CZ and Accelerated Crucible/Crystal Rotation Technique (CACRT) flow regimes for silicon-viscosity fluids.

### 2003

**Global Simulation of Heat Transport (LEC furnace, hybrid FE/FV)** — *Journal of Crystal Growth*, 1993 study as referenced/expanded in later reviews (see 1993 entry); continued development through early 2000s hybrid global models is documented in review chapters of this period.

### 2004

**Derby, J. J., Xiao, Q. (and colleagues)** — Referenced in oxide-crystal CZ global-analysis literature as extending the "global analysis of heat transfer" (Derby, Atherton & Gresho, 1989) methodology.
Continued development of the global continuum heat-transfer analysis approach for oxide and semiconductor CZ systems, incorporating internal radiation effects in semi-transparent crystals.

**Simulation of Global Heat Transfer in the Czochralski Process for BGO Sillenite Crystals.** *Journal of Crystal Growth* (2004).
Continuum global heat-transfer and melt-convection model applied to bismuth germanate (BGO) oxide CZ growth using CGSim software, validated against experimental process data; also documents lattice-Boltzmann-based continuum approaches to 3-D faceted-interface CZ growth as an alternative numerical continuum method.

### 2004 (Modeling of Crystal Growth Processes — Derby et al., overview chapter)

**Derby, J. J. et al.** — *"Modeling of Crystal Growth Processes,"* chapter overview (widely cross-referenced 2004–2015 editions).
A comprehensive review establishing the multiscale hierarchy (atomistic MD → kinetic Monte Carlo → continuum) and providing the canonical statement of the continuum transport-equation framework, numerical solution strategies (FD/FVM/FEM), and modeling challenges (moving boundaries, free surfaces, turbulence, radiation) for melt and solution crystal growth. This chapter (and its subsequent re-editions, e.g., 2015) is a central reference point for the entire continuum-modeling literature summarized here.

### 2007–2008

**(Directional Solidification for PV Silicon Purification)** — *"Directional Solidification Processes for Photovoltaic Silicon Purification: Numerical Simulation of Mechanical Stirring."* *ScienceDirect* chapter (~2007).
Continuum 3-D transient simulation (sliding-mesh finite volume) of forced convection induced by mechanical stirring in directional solidification, coupled to solute (impurity) transport in a quasi-steady approximation; validated by Particle Image Velocimetry (PIV) on a water-model analog — an important continuum model bridging melt-growth fluid dynamics and solute segregation for silicon purification.

**Global Heat Transfer Model for Czochralski Crystal Growth Based on Diffuse-Gray Radiation.** *Journal of Crystal Growth* (2008).
Introduces a new view-factor calculation method integrated into a global continuum heat-transfer model for CZ growth; validated against heater-power experimental data. Includes companion studies of turbulence modeling (k–ε) effects on crucible-rotation-dependent melt temperature fluctuations in production-scale silicon CZ pullers.

### 2008 (companion, thermal stress/oxide HEM)

**Numerical Simulation of the Czochralski Growth Process of Oxide Crystals with a Relatively Thin Optical Thickness.**
Extends the global heat-transfer analysis (per Derby, Atherton & Gresho, 1989) using a finite-volume method (FVM) solution of the radiative transfer equation, accounting for internal radiation in optically thin oxide crystals and its effect on melt/crystal interface shape and thermal stress.

### 2009

**Raabe, D.** — *"Lattice Boltzmann Modeling of Dendritic Growth in a Forced Melt Convection."* *Acta Materialia*, 57(6), 1755–1767.
Though rooted in a mesoscale (lattice-Boltzmann) framework, this paper is frequently cited alongside continuum macroscopic models for its coupling of forced melt convection with interface/dendritic growth dynamics, illustrating the interface between continuum-scale flow solvers and interface-tracking growth models.

### 2012

**Effective Simulation of the Effect of a Transverse Magnetic Field (TMF) in Czochralski Silicon Growth.** *Journal of Crystal Growth*, 360, 18–24.
Continuum MHD model examining transverse (as opposed to axial or cusp) magnetic-field damping of melt convection and its effect on global heat and mass transport in CZ silicon growth.

### 2014

**Lin, G., Bao, J., Xu, Z.** — *"A Three-Dimensional Phase Field Model Coupled with a Lattice Kinetics Solver for Modeling Crystal Growth in Furnaces with Accelerated Crucible Rotation and Traveling Magnetic Field."* *Computers & Fluids*, 103, 204–214.
Couples a continuum lattice-kinetics (Boltzmann-type) melt-flow solver with a phase-field interface model, applied to accelerated-crucible-rotation and traveling-magnetic-field CZ configurations — representative of modern hybrid continuum/interface methodologies.

**Modelling of Heat Transfer in Single Crystal Growth** (review article, arXiv:1410.1674).
A broad review synthesizing decades of continuum heat-transfer modeling literature for CZ and related melt-growth methods, covering turbulence modeling approaches (RANS, DNS, LES), radiation modeling, and global furnace-scale simulation strategies; extensively cross-references foundational works listed above (Lipchin & Brown 2000; Nikitin & Polezhaev 2001; and others).

### 2015

**Derby, J. J. et al.** — *"Modeling of Crystal Growth Processes"* (updated edition/re-publication, Experts@Minnesota / ScienceDirect, October 2015).
Updated restatement of the canonical multiscale-modeling overview chapter (see 2004 entry), reaffirming the continuum transport-equation framework as the standard approach at the macroscopic (tens-of-microns-and-larger) scale, situated between mesoscale (kinetic Monte Carlo) and microscopic (molecular dynamics) descriptions.

### 2016

**Younsi, A., Cartalade, A.** — *"On Anisotropy Function in Crystal Growth Simulations Using Lattice Boltzmann Equation."* *Journal of Computational Physics*, 325, 1–21.
Develops anisotropic continuum lattice-Boltzmann formulations for crystal growth interface simulation, extending the applicability of continuum-based numerical methods to anisotropic growth morphologies.

### 2018

**Numerical Modeling of Czochralski Silicon Crystal Growth** (industrial furnace study, EKZ 1300 furnace).
Presents an axisymmetric, steady-state, moving-grid continuum model for an industrial CZ silicon furnace incorporating melt turbulence (Chien's low-Reynolds k–ε model), inert-gas flow, solid-region conduction, and radiative heat transfer — a comprehensive contemporary "global model" implementation.

**Computer Simulations: Essential Tools for Crystal Growth Studies** (special issue overview, *Crystals*, MDPI, 8(8), 314).
Reviews the full spectrum of simulation methods for crystal growth — Monte Carlo, molecular dynamics, first-principles, multiscale, and continuum — with particular attention to multiscale frameworks (e.g., Elts et al.) that couple molecular dynamics and kinetic Monte Carlo data to continuum-scale predictions of macroscopic crystal morphology and growth/dissolution rates.

### 2022

**Development and Validation of a Thermal Simulation for the Czochralski Crystal Growth Process Using Model Experiments.** *Journal of Crystal Growth* (2022).
A modern global continuum heat-transfer and transport model validated against dedicated model experiments, cross-referencing the historical global-modeling lineage (Collet, Magotte, Van den Bogaert, Rolinsky, Loix, Jacot, Regnier, Marchal, Dupret — transverse magnetic field CZ silicon studies; Prostomolotov, Verezub, Falster — integrated heat transfer/microdefect global modeling).

**Global Simulation of a Czochralski Furnace for Silicon Crystal Growth against the Assumed Thermophysical Properties.**
Continuum global-furnace simulation study examining sensitivity of predicted melt/crystal interface shape, axial temperature gradients, oxygen concentration, and heater power to uncertainty in thermophysical property data — highlighting a persistent practical challenge in continuum melt-growth modeling.

**Three-Dimensional Modeling of Segregation Behavior during Solidification of a Sn–6 wt.% Pb Alloy.**
A representative modern continuum (Bennon–Incropera-type mixture/continuum) model for 3-D macrosegregation during alloy solidification, situated within the broader continuum solute-transport modeling tradition (Bennon and co-workers; Hebditch) applied originally to castings and directly relevant to solute/dopant segregation modeling in melt crystal growth.

### 2024 (retrospective/registry citations)

**A Volume Radiation Heat Transfer Model for Czochralski Crystal Growth Processes** (communicated by J. J. Derby; ResearchGate listing, cross-referenced October 2024).
Couples a multi-zone adaptive finite-volume phase-change/free-surface solver with a spectral/discrete-exchange-factor thermal radiation algorithm, addressing shadowing and multiple reflection/scattering in irregular axisymmetric CZ furnace geometries (applied to YAG crystal growth) — representative of state-of-the-art radiative continuum sub-modeling within global CZ simulations.

---

## Thematic Summary of Continuum Sub-Models

| Sub-model | Representative Physics | Key Numerical Method | Representative References |
|---|---|---|---|
| Global heat transfer | Conduction + convection + diffuse-gray/specular radiation across entire furnace | FEM (ABAQUS-type) / FVM global solvers, view-factor and discrete-exchange-factor radiation | Derby, Atherton & Gresho (1989); Derby & Xiao; global BGO/oxide CZ studies (2004, 2008) |
| Thermal-capillary interface model | Coupled melt/crystal interface (Stefan condition) + meniscus (Young–Laplace) | FEM with Newton continuation, moving/deforming mesh | Derby, Brown, Geyling, Jordan & Nikolakopoulou (1985); Sackinger, Brown & Derby (1989); Derby, Atherton, Thomas & Brown (1987) |
| Melt convection (laminar/turbulent) | Buoyancy, forced (rotation), thermocapillary (Marangoni) flow | FD/FVM/FEM Navier–Stokes; RANS k–ε (Jones–Launder, Chien); DNS | Kobayashi & Arizumi (1975); Bottaro & Zebib (1988, 1989); Lipchin & Brown (2000); Nikitin & Polezhaev (2001) |
| Magnetohydrodynamic (MHD) damping | Static/cusp/transverse/traveling magnetic fields, Lorentz force | Continuum MHD-Navier–Stokes | Langlois & Lee (1983); Hirata & Hoshikawa (1992); TMF CZ silicon study (2012); Lin, Bao & Xu (2014) |
| Solute/species transport & segregation | Dopant/impurity boundary layers, effective segregation coefficient, macrosegregation | Coupled species-convection-diffusion continuum equations | PV silicon stirring/segregation study (2007–2008); Bennon-type macrosegregation models; Sn–Pb alloy segregation study (2022) |
| Interface/morphology coupling | Faceting, dendritic growth, anisotropic interface kinetics | Lattice-Boltzmann + interface-tracking; phase-field/continuum hybrids | BGO sillenite lattice-Boltzmann faceted CZ study (2004); Raabe (2009); Younsi & Cartalade (2016); Lin, Bao & Xu (2014) |
| Multiscale/overview frameworks | Bridging MD → KMC → continuum scales | Review/synthesis | Derby et al., "Modeling of Crystal Growth Processes" (2004, 2015); *Crystals* special issue (2018); Modelling of Heat Transfer in Single Crystal Growth review (2014) |

---

## Notes on Coverage and Limitations

- This bibliography emphasizes **Czochralski (CZ) and related pulling/encapsulated (LEC) methods**, since the majority of foundational and contemporary continuum macroscopic modeling literature retrieved centers on this technique; Bridgman/VGF- and floating-zone-specific continuum studies are comparatively less represented in the sources surveyed here and would benefit from a dedicated follow-up search.
- Several entries are drawn from **secondary citations** within review articles and industry papers (e.g., Mihelčić et al. 1992; Sung, Jung & Ozoe 1995; TMF CZ silicon 2012) where the primary source's full bibliographic detail was available through citing-context excerpts rather than direct retrieval of the original article; publication years are reported as documented in the citing sources.
- Granular-media and porous-media "continuum models" (e.g., particle-size segregation in bedload transport, double-continuum porous transport models) surfaced during search but are **outside the scope** of melt/solution crystal growth and have been excluded from this bibliography.
- The **Derby et al. "Modeling of Crystal Growth Processes"** chapter appears in multiple citation records spanning 2004–2015, suggesting successive editions/reprints of the same core review; both are listed to reflect the citation trail found, but they likely represent the same foundational work.

---

> [!NOTE]
> 
> Generated by Claude.ai
>
> Model: Sonet 5
>
> Prompt: Provide an exhaustive description of numerical Continuum (Macroscopic) Models of Melt/Solution Growth. Show the output in Markdown format and sort the articles chronologically. Do not copy the output of the exported files into the chat.
