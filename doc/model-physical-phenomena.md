# Continuum (Macroscopic) Model of Melt/Solution Crystal Growth

## 1. Scope and Philosophy of the Continuum Approach

The continuum (macroscopic) model treats melt/solution crystal growth systems — Czochralski (CZ), Bridgman/Vertical Gradient Freeze (VGF), Kyropoulos (KY), Liquid-Encapsulated Czochralski (LEC), floating zone (FZ), and solution methods (TSSG, flux growth) — as domains of continuous matter governed by the classical conservation laws of continuum mechanics: mass, momentum, energy, and species. It is valid on length scales from tens of microns upward, where the discreteness of atoms is irrelevant and local thermodynamic equilibrium can be assumed within infinitesimal control volumes.

The model is inherently **multi-domain** and **multi-physics**: it couples the melt (or solution), the growing crystal, the surrounding gas/encapsulant, and often the furnace hot-zone (crucible, susceptor, heaters, insulation, chamber walls) into a single self-consistent boundary-value problem. This is frequently called a **"global model"** because the crystal/melt system cannot be solved in isolation — its boundary conditions (temperature distribution, heat fluxes, interface shape) are themselves outputs of the surrounding furnace physics.

Three nested scales are usually distinguished:

- **Macroscopic (continuum) scale** (>> 10 µm): bulk transport — the subject of this document.
- **Mesoscale** (100 nm – 10 µm): interfacial attachment kinetics, faceting, step-flow, boundary-layer phenomena — often parameterized into the continuum model rather than resolved.
- **Microscopic/atomistic scale** (< 100 nm): molecular dynamics, ab initio, kinetic Monte Carlo — supplies constitutive data (kinetic coefficients, segregation coefficients, interfacial energies) to the continuum model.

---

## 2. Governing Equations in the Bulk Phases

For each bulk phase (melt/solution, crystal, cover gas, encapsulant), the model solves the following conservation equations, generally in their transient, three-dimensional (often reduced to axisymmetric 2D) form.

### 2.1 Conservation of Mass (Continuity)

$$
\frac{\partial \rho}{\partial t} + \nabla\cdot(\rho \mathbf{u}) = 0
$$

For incompressible or Boussinesq-approximated liquids, this reduces to $\nabla\cdot\mathbf{u}=0$.

### 2.2 Conservation of Momentum (Navier–Stokes)

$$
\rho\left(\frac{\partial \mathbf{u}}{\partial t} + \mathbf{u}\cdot\nabla\mathbf{u}\right) = -\nabla p + \nabla\cdot\boldsymbol{\tau} + \rho\mathbf{g} + \mathbf{F}_{\text{body}}
$$

where $\boldsymbol{\tau} = \mu(\nabla\mathbf{u}+\nabla\mathbf{u}^T)$ for a Newtonian fluid, and $\mathbf{F}_{\text{body}}$ collects additional body forces (Lorentz force from applied magnetic fields, Coriolis/centrifugal terms in rotating frames).

**Boussinesq approximation** is standard for buoyancy: density variation is retained only in the buoyancy term,

$$
\rho \approx \rho_0\left[1 - \beta_T(T-T_0) - \beta_C(C-C_0)\right]
$$

with $\beta_T$ the thermal expansion coefficient and $\beta_C$ the solutal expansion coefficient (important in solution growth and doped-melt growth).

### 2.3 Conservation of Energy

$$
\rho c_p\left(\frac{\partial T}{\partial t} + \mathbf{u}\cdot\nabla T\right) = \nabla\cdot(k\nabla T) + Q
$$

$Q$ may include Joule heating (induction heating, resistive heating), viscous dissipation (usually negligible), or latent-heat source terms when a fixed-grid (enthalpy/apparent-heat-capacity) method is used instead of a deforming-mesh front-tracking method.

### 2.4 Conservation of Species (Solute/Dopant Transport)

$$
\frac{\partial C}{\partial t} + \mathbf{u}\cdot\nabla C = \nabla\cdot(D\nabla C)
$$

with $D$ the solute diffusivity. In multi-component solution growth, a full multi-component diffusion (Maxwell–Stefan or generalized Fick) formulation may be required if cross-diffusion effects are significant.

---

## 3. Interfaces and Their Governing Conditions

The distinguishing complexity of crystal-growth continuum modeling, relative to generic CFD/heat-transfer problems, is that the **positions and shapes of several interfaces are unknowns solved simultaneously with the field equations** (a free/moving-boundary or Stefan problem).

### 3.1 Melt/Crystal (Solid–Liquid) Interface

- **Stefan condition (latent heat balance):** the interface releases (or absorbs) latent heat $L$ as it advances at normal velocity $v_n$:

$$
k_s\left.\frac{\partial T}{\partial n}\right|_s - k_l\left.\frac{\partial T}{\partial n}\right|_l = \rho_s L\, v_n
$$

- **Thermodynamic equilibrium / kinetic undercooling:** the interface temperature equals the local melting point corrected for curvature (Gibbs–Thomson effect) and attachment kinetics, where $\Gamma$ is the Gibbs–Thomson coefficient, $\kappa$ the local interface curvature, and $\mu_k$ a kinetic growth coefficient (very large/fast for rough, atomically disordered interfaces; small and anisotropic for faceted interfaces):

$$
T_{\text{int}} = T_m - \Gamma\kappa - \mu_k^{-1} v_n
$$


- **Faceting:** for materials with strongly anisotropic interfacial kinetics (oxides, many semiconductors at low supercooling), flat crystallographic facets appear and coexist with rounded, kinetically rough regions on the same interface. This is modeled either by strongly anisotropic kinetic coefficients or by explicit facet-tracking algorithms, and it directly affects local dopant segregation (facet vs. non-facet segregation coefficients differ).
- **Solute rejection/incorporation:** at the interface, species conservation gives, where $k_0$ is the equilibrium segregation coefficient:

$$
\rho_l D_l \left.\frac{\partial C_l}{\partial n}\right| = v_n\,(C_l - C_s) = v_n\, C_l(1-k_0)
$$


- **Interface shape** (planar, concave, convex, or "W"-shaped) results from the competition between radial and axial heat flow and is a key predicted/controlled quantity, since it governs dislocation generation, radial segregation, and facet size.

### 3.2 Free Melt Surface (Melt–Gas Meniscus)

Relevant in CZ, KY, and FZ growth, where the meniscus shape must be solved as part of the free-boundary problem.

- **Young–Laplace equation** (normal stress balance with surface tension):

$$
p_l - p_g = \sigma\kappa_{\text{surf}}
$$

- **Marangoni (thermocapillary) stress:** tangential stress balance driven by surface-tension gradients (with temperature and, in solutions, with concentration):

$$
\mu\frac{\partial u_t}{\partial n} = \frac{\partial \sigma}{\partial T}\nabla_t T + \frac{\partial \sigma}{\partial C}\nabla_t C
$$

- **Contact-angle (growth-angle) condition** at the triple line where melt, crystal, and gas meet fixes the crystal diameter in CZ growth: the meniscus makes a fixed growth angle with the crystal surface, determined by surface-tension balance and the material's characteristic growth angle.

### 3.3 Container/Crucible Walls and Other Solid–Liquid Boundaries

No-slip velocity conditions, prescribed or computed heat flux/temperature (from the coupled furnace model), and, in Bridgman-type methods, contact-angle/wetting conditions where the melt detaches from the ampoule wall.

### 3.4 Gas/Vacuum Boundaries and Radiative Enclosure Boundaries

Radiative exchange (Section 5) and convective heat/mass exchange with flowing inert gas (Ar, N₂, forming gas) or with a controlled vapor atmosphere.

---

## 4. Fluid Flow Phenomena in the Melt/Solution

The melt flow field controls heat and solute delivery to the growth interface and is often the single most consequential (and most difficult) sub-problem.

### 4.1 Buoyancy-Driven (Natural) Convection

Driven by radial and axial temperature (and, in doped/solution systems, concentration) gradients. Characterized by the **thermal Grashof number** $Gr_T = g\beta_T\Delta T L^3/\nu^2$ and, for solution growth, the **solutal Grashof number** $Gr_C$. In many practical solution-growth and small melt-growth systems, buoyancy convection is the dominant or sole driving mechanism.

### 4.2 Forced Convection from Crystal and Crucible Rotation

- **Crystal rotation** creates a centrifugal pumping (von Kármán-type) flow that draws melt axially toward the interface and flings it radially outward — used deliberately to control interface shape and radial dopant homogeneity.
- **Crucible counter-rotation** (or co-rotation) is used to suppress or enhance specific flow structures; the ratio and sign of rotation rates are key process parameters (**Reynolds number** $Re = \Omega R^2/\nu$; **Coriolis/rotational Rayleigh number** combinations govern the transition between rotation- and buoyancy-dominated regimes).
- **Accelerated Crucible Rotation Technique (ACRT)** and other time-dependent rotation protocols are modeled as time-varying boundary conditions.

### 4.3 Thermocapillary (Marangoni) Convection

Significant at free surfaces, especially in small-diameter or microgravity/floating-zone growth where buoyancy is weak; characterized by the **Marangoni number** $Ma = -(\partial\sigma/\partial T)\Delta T L/(\mu\alpha)$.

### 4.4 Forced Convection from Gas Flow

Shear-driven flow at the melt free surface induced by the purge-gas stream; also governs convective transport of volatile species away from (or dopant vapor toward) the melt surface, and couples to gas-phase heat transfer.

### 4.5 Electromagnetically Driven Convection (when applied fields are used)

- **Induction-heating-induced flow:** in RF/induction-heated systems, the induced eddy currents themselves generate a Lorentz-force-driven stirring flow.
- **Applied static or AC magnetic fields (MCZ):** axial, transverse (cusp), or traveling magnetic fields are used to damp turbulent convection via the Lorentz force $\mathbf{F} = \mathbf{J}\times\mathbf{B}$, where $\mathbf{J}$ follows from Ohm's law $\mathbf{J} = \sigma_e(\mathbf{E}+\mathbf{u}\times\mathbf{B})$. This requires solving (or approximating via a low-magnetic-Reynolds-number simplification) the magnetohydrodynamic (MHD) equations coupled to the Navier–Stokes equations. Characterized by the **Hartmann number** $Ha = BL\sqrt{\sigma_e/\mu}$.

### 4.6 Flow Regime and Turbulence

Industrial-scale melt flows (especially Si, oxide, and metal melts at large diameters) are frequently **transitional or turbulent**, characterized by low Prandtl number for metals/semiconductors ($Pr \ll 1$) versus higher Prandtl number for oxide melts. Modeling strategies include:

- **Direct Numerical Simulation (DNS):** fully resolves all turbulent scales; computationally prohibitive for industrial geometries and long process times.
- **Large-Eddy Simulation (LES):** resolves large scales, models sub-grid scales; used for research-scale/laboratory analysis of oscillatory convection and temperature fluctuations.
- **Reynolds-Averaged Navier–Stokes (RANS)** with two-equation closure (e.g., low-Reynolds-number $k – \varepsilon$ models such as Chien's model, or $k – \omega$ models): the standard workhorse for steady/quasi-steady industrial global models due to tractable cost.
- **Partially-Averaged Navier–Stokes (PANS)**: a hybrid RANS/DNS approach with a tunable filter parameter, allowing variable resolution between full RANS and near-DNS.
- **Unsteady RANS (URANS)** and **combined 2D-axisymmetric/3D approaches**: since fully transient 3D turbulence-resolving simulation of an entire industrial process (hours of real growth time) is generally not economically justified, practice commonly combines an axisymmetric global heat-transfer model (for the whole furnace) with localized 3D transient melt-flow simulations using boundary conditions extracted from the global model.

Turbulent melt convection is directly linked to **temperature fluctuations at the growth interface**, which in turn produce **growth striations** (periodic microscale variations in dopant/impurity concentration and, in oxygen-bearing systems, growth-rate fluctuations) — a key quality metric predicted by these models.

---

## 5. Heat Transfer Phenomena

### 5.1 Conduction

Standard Fourier conduction in melt, crystal, crucible, insulation, and other solid hot-zone components, with temperature- and often anisotropy-dependent thermal conductivity (especially important for anisotropic crystals).

### 5.2 Convection

Coupled to the flow fields described in Section 4; in the melt, convective heat transport typically dominates over pure conduction except in highly viscous or strongly magnetically damped systems.

### 5.3 Radiative Heat Transfer

Radiation dominates heat exchange within the hot zone above roughly 1000–1200 °C and is essential for correctly predicting the melt/crystal interface shape and the crystal's thermal history (which governs thermal stress and point-defect/dislocation formation).

- **Diffuse-gray (or non-gray, spectral) surface-to-surface radiation** in an enclosure: requires computing **view factors** between all visible surface elements, accounting for self-shadowing by non-convex bodies (e.g., the crystal shadowing part of the melt surface, or the crucible rim shadowing the melt).
- **Net-radiation / radiosity method:** solves for the radiosity $J_i$ on each surface element $i$,

$$
J_i = \varepsilon_i \sigma_{SB} T_i^4 + (1-\varepsilon_i)\sum_j F_{ij} J_j
$$

with $\sigma_{SB}$ the Stefan–Boltzmann constant, $\varepsilon_i$ surface emissivity, and $F_{ij}$ the view factor between elements $i$ and $j$.
- **Volume (participating-medium) radiation:** required when the melt or an encapsulant (e.g., B₂O₃ in LEC growth) is semi-transparent; radiative transport within the volume must then be solved (e.g., via the P1 approximation, discrete-ordinates method, or Monte Carlo ray tracing) rather than treated as an opaque surface.
- **Semi-transparency of the crystal itself:** many oxide and some semiconductor crystals are partially transparent to the relevant thermal-radiation wavelengths, requiring internal radiative transport within the growing crystal, coupled back to the conduction equation as an internal heat source/sink.
- Correct emissivity values (melt, crystal, crucible, insulation) are frequently the single most sensitive and least well-known input parameters, directly controlling predicted interface shape and heater power.

### 5.4 Heater/Induction Heating

- **Resistive heaters:** modeled as prescribed heat-flux or fixed-temperature boundary conditions, or as Joule-heating volumetric sources if the heater itself is part of the solved domain.
- **RF/Induction heating:** requires solving the electromagnetic (Maxwell) equations for the induced eddy-current distribution in conducting parts (melt, susceptor), yielding a volumetric Joule-heating source term $Q = |\mathbf{J}|^2/\sigma_e$ that couples back into the energy equation; often solved in the low-frequency (quasi-static, eddy-current) limit.

### 5.5 Global (Whole-Furnace) Heat Transfer Model

Because radiative exchange and conduction through the hot zone are long-range and strongly coupled, the melt/crystal region cannot be given arbitrary boundary conditions — the **entire furnace assembly** (crucible, susceptor, afterheater, insulation packs, chamber walls, heaters) must generally be included in a self-consistent **global model**, iterating between:
1. electromagnetic/Joule heating (if induction-heated),
2. conduction in all solid parts,
3. surface-to-surface (and volumetric, if applicable) radiation across the enclosure,
4. convection in melt and gas,
5. the moving melt/crystal interface position and shape,
until a converged, mutually consistent steady state (or transient trajectory) is obtained. This combined 2D-axisymmetric global/3D local strategy is standard in the literature (e.g., CGSim, FEMAG-CZ, CrysMAS, STHAMAS3D-type codes).

### 5.6 Gas-Phase Heat and Mass Transfer

The inert cover-gas (or reactive/vapor) flow is generally treated with its own laminar or turbulent Navier–Stokes/energy solution, coupled to the melt and hot-zone solids through shared boundary conditions; gas flow rate and chamber pressure materially affect melt convection (via shear at the free surface), radial temperature gradients, and transport of volatile species (e.g., SiO, oxygen chemistry in CZ Si growth; As, P vapor pressure control in LEC/VGF III-V growth).

---

## 6. Mass Transfer and Solute/Dopant Phenomena

### 6.1 Species Transport

Advection–diffusion transport of dopants, impurities, or (in solution growth) solute species and solvent, per Section 2.4; coupled to the flow field, since convective delivery of solute to the boundary layer at the growth interface generally dominates over pure diffusion except at very low growth rates or in diffusion-controlled sub-regimes.

### 6.2 Segregation at the Growth Interface

- **Equilibrium segregation coefficient** $k_0 = C_s^* / C_l^*$ relates solid and liquid interfacial concentrations at equilibrium.
- **Effective segregation coefficient** (Burton–Prim–Slichter, BPS): accounts for the diffusive/convective boundary layer of thickness $\delta$ at the growing interface,

$$
k_{\text{eff}} = \frac{k_0}{k_0 + (1-k_0)e^{-v\delta/D}}
$$

which depends on growth rate $v$, boundary-layer thickness (set by the local flow field), and diffusivity — providing the crucial link between the fluid-dynamics sub-model and the resulting axial and radial dopant distribution in the grown crystal.
- **Radial segregation** results from radial non-uniformity of the boundary-layer thickness and interface shape, driven by the melt-flow pattern (rotation vs. buoyancy competition).
- **Facet-related segregation:** facets typically exhibit a different (often much higher) effective segregation coefficient than adjoining rough interface regions, producing localized compositional anomalies ("facet striations" / core effects).

### 6.3 Constitutional Supercooling and Morphological Interface Instability

When solute rejection at an advancing interface creates a region ahead of the interface where the actual temperature falls below the local liquidus temperature (set by the local, solute-depleted composition), the planar interface becomes morphologically unstable, breaking down into cells or dendrites. The classical **constitutional-supercooling criterion**,

$$
\frac{G}{v} < \frac{m\,C_0(1-k_0)}{k_0 D}
$$

(with $G$ the liquid-side temperature gradient at the interface and $m$ the liquidus slope) is evaluated from the coupled thermal/solutal continuum solution to assess stability limits on growth rate and gradient.

### 6.4 Multi-Component and Solution-Specific Effects

In solution growth (TSSG, flux methods, aqueous growth), additional phenomena include: solvent evaporation/loss at a free surface, solutal buoyancy (often dominant over thermal buoyancy since $\Delta C$ effects can be large even for small $\Delta T$), double-diffusive convection when thermal and solutal buoyancy act on different diffusive time scales (producing layered or oscillatory flow), and supersaturation-driven nucleation phenomena at the growth front.

### 6.5 Volatile-Species and Ambient Vapor Chemistry

For compound melts with a volatile constituent (e.g., As in GaAs, P in InP), the model must account for evaporation/dissociation at the melt free surface, transport through the cover-gas or through an encapsulant layer (B₂O₃ in LEC), and its influence on melt stoichiometry, requiring coupled gas-phase species transport and, in encapsulated growth, dissolved-gas transport through the encapsulant.

---

## 7. Stress, Defect, and Crystal-Quality Phenomena (Post-Interface Continuum Sub-Models)

Although the strict melt/solution transport problem ends at the growth interface, macroscopic models are almost always extended into the solid crystal to predict quality-determining phenomena, since these are the ultimate purpose of the growth simulation.

### 7.1 Thermoelastic Stress

The non-uniform temperature field frozen into the growing/cooling crystal generates thermal stresses, computed from the thermoelasticity equations (equilibrium of stress $\nabla\cdot\boldsymbol{\sigma}=0$ with the constitutive relation $\boldsymbol{\sigma} = \mathbf{C}:(\boldsymbol{\varepsilon}-\boldsymbol{\varepsilon}_{\text{th}})$, where $\boldsymbol{\varepsilon}_{\text{th}}$ is the thermal strain and $\mathbf{C}$ the (possibly anisotropic, crystal-orientation-dependent) elastic stiffness tensor). This is fully three-dimensional even for an axisymmetric crystal unless a special crystallographic orientation coincides with the growth axis.

### 7.2 Chemical (Compositional) Stress

Non-uniform dopant/solute incorporation (Section 6.2) produces local lattice-parameter variations (compositional/chemical strain), generating stresses that can dominate over thermal stress in heavily and non-uniformly doped systems, and that are directly implicated in cracking behavior — sometimes with counter-intuitive dependence on growth rate.

### 7.3 Dislocation Generation and Point-Defect Dynamics

- Excess thermal stress exceeding the critical resolved shear stress of the material drives **dislocation generation and multiplication**, modeled via continuum dislocation-density evolution equations (e.g., Alexander–Haasen-type models) coupled to the thermal-stress field.
- **Point-defect (vacancy/self-interstitial) transport and aggregation**, of particular importance in silicon growth, is modeled with its own reaction–diffusion continuum equations, driven by the pulling-rate-to-thermal-gradient ratio ($v/G$) at and behind the interface (Voronkov theory), determining the distribution of vacancy-rich, interstitial-rich, and defect-free regions.

### 7.4 Bubble/Void and Second-Phase Inclusion Formation

In some systems (e.g., voids from vacancy agglomeration, or gas-bubble entrapment in oxide/solution growth), continuum nucleation-and-growth or population-balance sub-models are coupled to the local point-defect or dissolved-gas supersaturation field.

---

## 8. Free-Boundary (Moving-Interface) Numerical Treatment

Because interface positions are unknown a priori, the numerical solution strategy is itself a defining feature of continuum crystal-growth models.

### 8.1 Interface-Tracking (Boundary-Fitted, Deforming-Mesh) Methods

The computational mesh is deformed to conform to the current (unknown) interface position, which is solved iteratively/simultaneously with the field equations (finite-element methods are dominant here, since they naturally accommodate deforming, unstructured meshes and impose interface conditions as natural boundary conditions of a weak/variational formulation). This is the standard approach in research-grade codes because it gives accurate, sharp representation of the Stefan and free-surface conditions.

### 8.2 Fixed-Grid (Interface-Capturing) Methods

The interface is represented implicitly on a fixed mesh via:
- **Enthalpy method / apparent heat capacity method:** latent heat is folded into an effective heat capacity or source term active over a (numerically) mushy temperature interval.
- **Level-set or phase-field methods:** an auxiliary field (signed distance function, or a continuous order parameter) implicitly locates the interface and evolves with the flow and thermal field; phase-field methods additionally regularize the sharp-interface Stefan problem to allow natural treatment of morphological instabilities, dendritic growth, and topology changes that boundary-fitted meshes handle poorly.

### 8.3 Slice / Quasi-1D and Quasi-2D Reduced Models

For rapid design-stage or long-time-horizon (whole-process) simulations, simplified models integrate a 1D (axial) or 2D energy balance along the crystal (a "slice model"), using view-factor-based radiation and empirical/semi-analytical convective correlations rather than a full field solution — trading spatial fidelity for the ability to simulate an entire pulling sequence (diameter control, seed-to-tail) at low computational cost. These are frequently coupled to full 2D/3D global models to supply calibrated boundary conditions or growth-rate/diameter control logic.

### 8.4 Coupling Strategy Across Scales and Domains

Typical practice (e.g., in CGSim, FEMAG-CZ, CrysMAS, Cats2D, CrysVUn) is a staged/segregated coupling:
1. Solve global (often axisymmetric, steady or quasi-steady) heat transfer for the whole hot zone including radiation and conduction, obtaining melt/crystal interface shape and furnace temperature field.
2. Extract boundary/initial conditions for a higher-fidelity (often 3D, transient, turbulence-resolving) local melt-flow simulation.
3. Feed refined heat-transfer-coefficient or time-averaged flux information from the local model back into the global model, iterating to self-consistency.
4. Post-process the converged thermal/flow field through segregation, stress, and defect sub-models.

---

## 9. Key Dimensionless Groups Governing the Physics

| Group | Definition | Governs |
|---|---|---|
| Grashof, $Gr$ | $g\beta\Delta T L^3/\nu^2$ | Buoyancy-driven flow strength |
| Rayleigh, $Ra = Gr\cdot Pr$ | — | Onset of buoyant convection/instability |
| Prandtl, $Pr$ | $\nu/\alpha$ | Momentum vs. thermal diffusion (≪1 for metals/semiconductors) |
| Reynolds, $Re$ | $\Omega R^2/\nu$ or $UL/\nu$ | Rotational/forced-flow strength, transition to turbulence |
| Marangoni, $Ma$ | $-(\partial\sigma/\partial T)\Delta T L/(\mu\alpha)$ | Thermocapillary flow strength |
| Hartmann, $Ha$ | $BL\sqrt{\sigma_e/\mu}$ | Magnetic damping of convection |
| Schmidt, $Sc$ | $\nu/D$ | Momentum vs. solutal diffusion |
| Péclet (thermal/solutal), $Pe$ | $UL/\alpha$ or $UL/D$ | Advection vs. diffusion dominance |
| Biot, $Bi$ | $hL/k$ | Surface vs. internal thermal resistance |
| Stefan, $Ste$ | $c_p\Delta T/L$ | Sensible vs. latent heat |

---

## 10. Summary Table of Coupled Physical Phenomena

| Domain | Governing Physics |
|---|---|
| Melt/solution bulk | Mass, momentum (Navier–Stokes, possibly turbulent/MHD), energy, species transport |
| Crystal bulk | Conduction (possibly anisotropic, semi-transparent), thermoelastic stress, point-defect/dislocation dynamics |
| Melt/crystal interface | Stefan condition, Gibbs–Thomson/kinetic undercooling, faceting, solute partitioning, morphological stability |
| Free melt surface | Young–Laplace shape, Marangoni stress, growth-angle/contact-line condition |
| Furnace hot zone | Conduction, surface-to-surface and volumetric radiation, induction/Joule heating, global energy balance |
| Cover gas/encapsulant | Laminar/turbulent flow, convective heat transfer, volatile-species transport, dissolved-gas transport |
| Numerical treatment | Deforming-mesh (FEM) vs. fixed-grid (enthalpy, level-set, phase-field) interface handling; staged multi-domain coupling |

---

*This reference synthesizes the standard continuum-transport framework as developed and applied in the crystal-growth-modeling literature (Derby and coworkers; the IKZ/Leibniz-Institut group — Müller, Friedrich; Dupret and coworkers; and related global-heat-transfer/melt-convection modeling work), covering melt-growth methods including Czochralski, Bridgman/VGF, Kyropoulos, LEC, floating zone, and solution-growth techniques.*

---

> [!NOTE]
> 
> Generated by Claude.ai
>
> Model: Sonet 5
>
> Prompt: Provide an exhaustive description of numerical Continuum (Macroscopic) Model of Melt/Solution Growth. Provide description of all physical relevant phenomena. Show the output in Markdown format. Do not copy the output of the exported files into the chat.
