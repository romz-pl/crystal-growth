# Melt/Crystal (Solid–Liquid) Interface

## 1. Scope and Modeling Philosophy

In continuum (macroscopic) models of bulk crystal growth — as implemented in codes such as CGSim, CrysMAS, FEMAG-CZ, CrysVUn, and Cats2D — the solid–liquid interface is **not** resolved at the atomistic or dendritic-tip scale. Instead it is treated as a **sharp, two-dimensional (or axisymmetric one-dimensional) moving boundary** embedded in a continuum heat/mass/momentum-transfer problem. The interface is the internal free boundary separating the solid (crystal) and liquid (melt or solution) domains, and its shape and position are *a priori unknown* — they are outputs of the coupled solution, not inputs.

The interface model must simultaneously satisfy:

1. **Thermodynamic equilibrium** (or near-equilibrium) conditions at the boundary
2. **Conservation laws** (energy, species, momentum) across the moving boundary
3. **Geometric/kinematic constraints** relating interface motion to the growth process (pulling, translation, or ampoule motion)
4. **Coupling constraints** with the free melt surface, container walls, and global heat/mass transport

This document describes each physically relevant phenomenon and the corresponding mathematical treatment.

---

## 2. The Interface as a Free/Moving Boundary

### 2.1 Sharp-Interface Idealization

The continuum model assumes a mathematically sharp interface with zero thickness, across which:
- Density can jump discontinuously (solid vs. liquid density)
- Thermal conductivity, viscosity, and other properties jump discontinuously
- Temperature is continuous (in the absence of strong kinetic undercooling)
- Velocity normal component is discontinuous in the crystal reference frame (due to solidification shrinkage/expansion)

This contrasts with **diffuse-interface (phase-field) models**, which resolve a finite transition region. Continuum bulk-growth codes almost universally use the sharp-interface approach because the diffuse zone (nanometers) is many orders of magnitude smaller than the crystal (centimeters), making phase-field treatment computationally prohibitive at the reactor scale.

### 2.2 Interface Parametrization

The interface shape is represented as:
- An unknown function $z = f(r, t)$ in axisymmetric (r–z) coordinates for Czochralski (CZ), liquid-encapsulated Czochralski (LEC), Kyropoulos (KY)
- An unknown function $\Gamma(x, t)$ in 2D/3D Cartesian representations for Bridgman/vertical gradient freeze (VGF/VB) configurations
- Represented numerically via:
  - **Boundary-fitted (deforming) mesh methods** — the mesh conforms to the interface and is re-generated/deformed at each iteration (dominant approach in CGSim, FEMAG-CZ)
  - **Front-tracking methods** — explicit marker points/elements track the interface within a fixed or adaptive mesh
  - **Level-set or enthalpy/apparent-heat-capacity methods** — the interface is captured implicitly as an isotherm within a fixed mesh (more common in VB/VGF and casting-oriented codes, less common in CZ due to strong interface curvature control needs)

### 2.3 Degrees of Freedom and Iterative Determination

Because interface shape, melt/gas free-surface shape, and global temperature field are mutually coupled, the interface position is found **iteratively**:
1. Guess interface shape
2. Solve heat/momentum/species equations in solid and liquid domains
3. Evaluate residual of the interface energy balance (Stefan condition)
4. Update interface shape (e.g., via Newton iteration, relaxation, or pseudo-time evolution)
5. Repeat to convergence

This is the single most numerically demanding sub-problem in global CZ/Bridgman simulators.

---

## 3. Thermal Boundary Conditions at the Interface

### 3.1 Melting Point / Liquidus Condition

The interface temperature is pinned to the (possibly pressure- and curvature-corrected) melting/liquidus temperature:

$$
T_{\text{interface}} = T_m
$$

For solutions/melts with more than one component (doped crystals, alloys, solution growth such as LPE or flux growth), this generalizes to the **liquidus condition**:

$$
T_{\text{interface}} = T_{\text{liq}}(C_{L,\text{interface}})
$$

where $C_{L,\text{interface}}$ is the interfacial liquid-phase solute concentration and $T_{\text{liq}}$ is obtained from the phase diagram (linearized liquidus slope $m$ is commonly used: $T_{\text{liq}} = T_m + m \, C_L$).

### 3.2 Gibbs–Thomson (Curvature) Undercooling

Interface curvature shifts the equilibrium melting temperature:

$$
T_{\text{interface}} = T_m - \Gamma_{GT}\, \kappa
$$

where $\Gamma_{GT}$ is the Gibbs–Thomson coefficient (proportional to solid–liquid surface energy divided by latent heat per unit volume) and $\kappa$ is the local interface curvature (sum of principal curvatures in 3D). This effect is:
- Significant for facet edges, dendrite tips, and small-radius interface regions
- Generally small for macroscopic bulk-growth interfaces except at the triple line (crystal–melt–gas contact) and where interface curvature is locally sharp
- Often neglected in first-order global thermal models but retained in higher-fidelity or shape-stability analyses

### 3.3 Kinetic Undercooling

For finite attachment kinetics, the actual interface temperature departs from equilibrium by an amount proportional to growth velocity:

$$
T_{\text{interface}} = T_m - \frac{v_n}{\mu_k}
$$

where $v_n$ is the normal growth velocity and $\mu_k$ is the kinetic growth coefficient. This is:
- Negligible for most metals and many oxide/semiconductor melt growth systems (fast atomic attachment, effectively isothermal interface)
- **Not negligible** for faceted growth (e.g., some oxides, semiconductors growing on singular low-index facets, and many solution-growth systems) where anisotropic, orientation-dependent kinetic coefficients control facet formation and step-flow growth
- Modeled via anisotropic kinetic laws $\mu_k(\theta)$ dependent on crystallographic orientation relative to the interface normal

### 3.4 Stefan (Latent Heat) Energy Balance

The core interface condition is the jump in normal heat flux balancing latent heat release/absorption:

$$
k_S \left(\frac{\partial T}{\partial n}\right)_S - k_L \left(\frac{\partial T}{\partial n}\right)_L = \rho_S \, L \, v_n
$$

where:
- $k_S, k_L$ — thermal conductivities of solid and liquid (often strongly temperature- and, for semi-transparent crystals, radiation-dependent)
- $L$ — latent heat of fusion
- $\rho_S$ — solid density
- $v_n$ — normal interface velocity (positive for growth)

This single equation is what actually **determines the interface shape**: at each point, the imbalance between conductive heat extraction (through the crystal, typically) and heat supplied from the melt fixes the local growth rate, and the requirement of a consistent, continuous interface shape over the whole domain closes the problem.

Physically relevant contributions to $k_S(\partial T/\partial n)_S$ and $k_L(\partial T/\partial n)_L$:
- Pure conduction in opaque crystals/melts
- **Radiative conduction contribution** in semi-transparent crystals (oxides such as sapphire, YAG, and many optical/laser crystals) — treated via a Rosseland diffusion approximation or discrete-ordinates radiative transfer that augments the effective thermal conductivity near and within the crystal
- Convective heat delivery in the melt via buoyancy, forced (crucible/crystal rotation), Marangoni, and (for larger systems) turbulent transport — see Section 5

---

## 4. Species (Solute) Transport and Segregation at the Interface

Relevant for doped crystals (e.g., CZ silicon with dopants, oxide crystals with dopants/stoichiometry deviations) and solution growth (LPE, flux, hydrothermal, THM) where a solvent/solute system governs growth.

### 4.1 Solute Conservation (Interfacial Mass Balance)

At the moving interface, solute rejected or absorbed during solidification must balance diffusive/convective flux in the liquid:

$$
D_L \left(\frac{\partial C_L}{\partial n}\right)_ {\text{interface}} = v_n \, (C_L - C_S)_ {\text{interface}} = v_n\, C_L (1 - k_{eff})
$$

where $D_L$ is the liquid-phase solute diffusivity, $C_L, C_S$ are interfacial liquid and solid concentrations, and $k_{eff}$ is the effective segregation coefficient.

### 4.2 Segregation Coefficient

- **Equilibrium segregation coefficient** $k_0 = C_S/C_L$ from the phase diagram
- **Effective (Burton–Prim–Slichter, BPS) segregation coefficient**:

$$
k_{eff} = \frac{k_0}{k_0 + (1-k_0)\exp(-v_n \delta / D_L)}
$$

where $\delta$ is the solute boundary-layer thickness, itself a function of melt convection strength (rotation rate, buoyancy). This couples segregation directly to the fluid-dynamic solution — a key reason global CZ models solve fluid flow even when only average axial dopant profiles are of interest.

### 4.3 Constitutional Supercooling and Morphological Stability

If the liquidus temperature gradient ahead of the interface (driven by the rejected solute buildup) exceeds the actual thermal gradient, the melt ahead of the interface becomes constitutionally supercooled, destabilizing the planar interface (Mullins–Sekerka-type instability). Continuum global models typically:
- Evaluate the **constitutional supercooling criterion** as a post-processing stability check
- Do not resolve the resulting cellular/dendritic microstructure themselves (this requires separate microscale/phase-field modeling), but flag operating windows (pulling rate vs. thermal gradient) where planar/faceted interfaces remain stable

---

## 5. Coupling with Melt Convection

The interface is a boundary condition for, and is itself controlled by, the melt flow field. Relevant convective phenomena:

### 5.1 Buoyancy-Driven (Natural) Convection
Density variations from temperature (and solutal) gradients drive Rayleigh–Bénard-type flow in the melt, governed by the Boussinesq approximation in the momentum equation. This is typically the dominant flow mode in large-diameter CZ and VGF/VB melts and strongly affects interface shape (via local heat delivery) and dopant distribution.

### 5.2 Forced Convection
Crystal and crucible rotation (CZ, KY) impose forced convection (rotational Couette-type flow, Ekman/Taylor-Proudman layers near the rotating interface). This is modeled via rotating-frame Navier–Stokes equations with the interface as a rotating, permeable-to-heat (but impermeable-to-mass, except for the density-change normal velocity) rigid/moving boundary.

### 5.3 Marangoni (Thermocapillary) Convection
Surface-tension gradients along the free melt surface (not the solid–liquid interface itself, but strongly coupled to it thermally) drive near-surface flow that can dominate in small-Prandtl-number melts (e.g., silicon) or low-gravity/space-processing conditions.

### 5.4 Magnetohydrodynamic (MHD) Damping
In semiconductor CZ growth, externally applied static, cusp, or traveling magnetic fields are used to damp turbulent/oscillatory melt convection, indirectly stabilizing the interface shape and dopant striations. Modeled via the induction equation or low-magnetic-Reynolds-number Lorentz-force approximation added as a body force in the melt momentum equation.

### 5.5 Turbulence
For larger melt volumes (industrial-diameter CZ, VB furnaces), the melt flow can be transitional or turbulent. RANS turbulence closures (k-ε, low-Reynolds variants), large-eddy simulation, or direct time-dependent laminar solutions (for smaller/lower-Grashof-number cases) are used; the choice affects the *time-averaged* interface shape and the amplitude of unsteady interface perturbations (relevant to growth striations).

### 5.6 Velocity Boundary Conditions at the Interface
- **No-slip** tangential velocity condition on the liquid side (melt does not slip relative to the moving/rotating solid surface)
- **Kinematic condition**: normal liquid velocity relative to the moving interface accounts for the density change upon solidification:

$$
\rho_L (v_{L,n} - v_{int,n}) = \rho_S (v_{S,n} - v_{int,n})
$$

commonly simplified to a normal mass-conservation jump when $\rho_S \neq \rho_L$ (important for materials with significant solidification shrinkage/expansion, e.g., water/ice, silicon, germanium)

---

## 6. Interface Shape, Curvature, and Its Global Consequences

### 6.1 Radial Shape Classification
The macroscopic interface shape (in axisymmetric growth) is classified by its deviation from flat:
- **Convex-into-the-melt** (typical of most CZ growth with axial heat extraction upward through the crystal)
- **Concave-into-the-crystal**
- **Flat**
- **Inflected/S-shaped** (can arise from competing radial heat flux contributions, e.g., strong sidewall heating combined with central seed cooling)

Interface shape is a primary design/process target because it directly governs:
- **Dopant/impurity radial distribution** (curved interfaces produce radially varying local growth angle relative to isotherms, altering local $v_n$ and hence local $k_{eff}$)
- **Thermal stress and dislocation generation** in the growing crystal (interface curvature couples to von Mises stress fields near the interface)
- **Facet formation** (locally flat, low-index crystallographic regions can appear at interface regions aligned with low-index planes, particularly pronounced for oxide crystals)

### 6.2 Interface Curvature and the Triple Point
The **triple point** — where crystal, melt, and (for CZ/KY) the ambient gas/meniscus meet — is a singular region requiring special treatment:
- Its radial position is *the crystal radius*, and its evolution over time determines the diameter (used for growth-rate/diameter control)
- The **growth angle** (angle between the meniscus and the crystal side surface at the triple point, set by the material's characteristic growth angle) is imposed as a boundary condition coupling the free-melt-surface (meniscus) shape to the interface/crystal-shape solution
- This is central to the classical Tsivinskii/Voronkov/Surek meniscus theory used to compute the pulling-rate–thermal-gradient relationship controlling diameter in CZ growth

---

## 7. Growth-Process Kinematics

### 7.1 Reference Frame and Pulling/Translation
Depending on technique, the interface is embedded in different global kinematic settings:
- **Czochralski/Kyropoulos**: crystal pulled upward (CZ) or crystal grown in place with progressive cooling (KY, no/slow pulling); interface position tracked in a frame translating with the crystal at the (time-varying) pulling rate
- **Bridgman/VGF/VB**: ampoule or furnace thermal profile translated relative to a stationary crucible, or the crucible is translated through a fixed thermal gradient; interface advances according to the imposed cooling/translation rate
- **LEC**: analogous to CZ but with a molten encapsulant layer (e.g., B₂O₃) covering the melt, adding an additional interface (encapsulant/melt) and its own thermal/flow coupling

### 7.2 Pseudo-Steady-State vs. Fully Transient Treatment
- Many global CZ models solve a **quasi-steady-state** interface problem at each instant (crystal length treated as a slowly varying parameter), justified by the large disparity between thermal diffusion time and crystal growth time
- Bridgman/VGF models more commonly require **fully transient** solution because the imposed furnace/ampoule translation continuously changes boundary conditions at a rate comparable to thermal relaxation

### 7.3 Global Mass Balance / Diameter Control
The interface's radial extent (crystal diameter) is linked to global mass conservation: crystal pulling rate, melt level drop (crucible surface descent), and interface growth rate must be mutually consistent, and diameter-control (ADC) algorithms in real furnaces are modeled by feedback loops adjusting pulling rate or heater power to maintain the target triple-point radius.

---

## 8. Coupling with Global Heat Transfer (Furnace-Scale Effects)

The interface's energy balance (Section 3.4) depends on heat delivered/extracted well beyond the melt itself:

### 8.1 Conduction Through the Growing Crystal
Axial and radial conduction through the crystal (with temperature-dependent thermal conductivity, and radiative augmentation for semi-transparent crystals) sets $(\partial T/\partial n)_S$.

### 8.2 Radiative Heat Exchange
- Surface-to-surface radiative exchange between crystal, melt free surface, crucible, heaters, and insulation (view-factor-based or ray-tracing/Monte Carlo radiative solvers)
- Internal (volumetric) radiative transport in semi-transparent crystal bodies, coupled to the conduction equation via the Rosseland or P1 approximation, or full radiative transfer equation solution for more accurate treatment near the interface region

### 8.3 Induction/Resistive Heating Coupling
For RF-induction-heated systems (common in oxide and semiconductor CZ furnaces), electromagnetic (Joule heating) field solutions in the susceptor/crucible are coupled to the thermal problem, indirectly setting the heat flux boundary conditions that ultimately control interface position.

### 8.4 Crucible and Melt-Level Effects
As the melt is progressively consumed, the melt volume and its free-surface elevation change, altering the thermal environment seen by the interface over the course of a growth run — a slow but cumulative effect requiring the interface sub-model to be re-solved at each discretized time/length step of the full growth process.

---

## 9. Facsimile of the Full Interface Boundary-Condition Set

At every point of the (unknown) interface $\Gamma$, the continuum model simultaneously enforces:

| # | Condition | Physical meaning |
|---|---|---|
| 1 | $T = T_m - \Gamma_{GT}\kappa - v_n/\mu_k(\theta)$ (or liquidus form with $C_L$) | Local phase equilibrium ± curvature/kinetic corrections |
| 2 | $k_S \partial_n T_S - k_L \partial_n T_L = \rho_S L v_n$ | Stefan energy balance → determines $v_n$, hence shape evolution |
| 3 | $D_L \partial_n C_L = v_n C_L(1-k_{eff})$ | Solute rejection/incorporation balance |
| 4 | No-slip + kinematic mass-jump velocity condition | Momentum coupling, shrinkage/expansion accommodation |
| 5 | Triple-point growth-angle condition | Fixes crystal radius / links to meniscus shape |
| 6 | Global mass balance (pulling rate, melt-level drop) | Closes the kinematic/geometric system |

These are solved **simultaneously and iteratively** with the bulk melt (Navier–Stokes + energy + species), bulk crystal (conduction/radiation), free-surface meniscus shape, and furnace-scale heat transfer (radiation, induction/resistive heating) sub-models, making the solid–liquid interface the central coupling hub of the entire continuum growth simulation.

---

## 10. Summary of Physically Relevant Phenomena at the Interface

- Local thermodynamic (melting-point/liquidus) equilibrium
- Gibbs–Thomson curvature undercooling
- Kinetic (attachment-rate) undercooling and facet formation
- Latent heat release/absorption (Stefan condition)
- Radiative heat conduction augmentation in semi-transparent crystals
- Solute segregation (equilibrium and effective/BPS coefficients)
- Constitutional supercooling and morphological (Mullins–Sekerka) stability limits
- Density-change (shrinkage/expansion) kinematic jump condition
- No-slip coupling to buoyancy-, rotation-, Marangoni-, and MHD-influenced melt convection
- Turbulence effects on time-averaged interface shape and striations
- Interface curvature effects on radial dopant/stress distribution
- Triple-point growth-angle condition linking interface to meniscus/free-surface shape
- Global mass balance (pulling rate, melt-level descent) and diameter control
- Coupling to furnace-scale radiative, conductive, and electromagnetic (induction) heat transfer
- Quasi-steady vs. fully transient treatment depending on growth technique (CZ/KY vs. Bridgman/VGF/VB)
