# Convective Transport and Instability Phenomena

## 1. Scope and Physical Context

The continuum (macroscopic) model treats the melt, solution, and crystal as interpenetrating continua governed by conservation laws for mass, momentum, energy, and species, coupled through a moving solid–liquid interface. Convective transport — the advection of momentum, heat, and solute by fluid motion — dominates over diffusion in essentially all industrially relevant melt- and solution-growth configurations (Czochralski, Bridgman, LEC, Kyropoulos, floating zone, solution/flux growth). Convection determines the shape and stability of the growth interface, the uniformity of dopant/solute incorporation, the formation of growth striations, and the onset of parasitic melt/solution instabilities that can destroy crystal quality.

This document treats:
1. The governing continuum equations for convective transport in the melt.
2. The physical driving mechanisms of convection (buoyancy, forced/rotational, Marangoni, electromagnetic).
3. Dimensionless groups controlling the convective regime.
4. Instability mechanisms (Rayleigh–Bénard, rotational, Marangoni–Bénard, solutal, double-diffusive, baroclinic/shear).
5. Linear stability theory formulation.
6. Interaction of convection with the moving interface (morphological/constitutional coupling).
7. Numerical/modeling considerations specific to crystal growth simulators (CGSim, CrysMAS, FEMAG-CZ, CrysVUn, Cats2D-type codes).

---

## 2. Governing Continuum Equations

### 2.1 Conservation of Mass

For an incompressible melt (the standard assumption away from the Boussinesq buoyancy term):

$$
\nabla \cdot \mathbf{u} = 0
$$

where $\mathbf{u}$ is the fluid velocity field.

### 2.2 Conservation of Momentum (Navier–Stokes with Boussinesq Approximation)

$$
\rho_{0}\left(\frac{\partial \mathbf{u}}{\partial t} + \mathbf{u}\cdot\nabla\mathbf{u}\right) = -\nabla p + \mu \nabla^{2}\mathbf{u} + \rho_{0}\,\mathbf{g}\,\beta_{T}\left(T - T_{0}\right) + \rho_{0}\,\mathbf{g}\,\beta_{C}\left(C - C_{0}\right) + \mathbf{F}_{L} - 2\rho_{0}\,\boldsymbol{\Omega}\times\mathbf{u} - \rho_{0}\,\boldsymbol{\Omega}\times\left(\boldsymbol{\Omega}\times\mathbf{r}\right)
$$

where:
- $\rho_{0}$ — reference density,
- $p$ — dynamic pressure,
- $\mu$ — dynamic viscosity,
- $\beta_{T} = -\frac{1}{\rho_{0}}\left(\frac{\partial \rho}{\partial T}\right)_{p}$ — thermal expansion coefficient,
- $\beta_{C} = -\frac{1}{\rho_{0}}\left(\frac{\partial \rho}{\partial C}\right)_{p}$ — solutal expansion coefficient,
- $\mathbf{F}_{L} = \mathbf{J}\times\mathbf{B}$ — Lorentz body force (relevant under applied magnetic fields, e.g. MCZ, EMCZ),
- $\boldsymbol{\Omega}$ — angular velocity vector of the rotating frame (crystal and/or crucible rotation),
- the terms $-2\rho_{0}\boldsymbol{\Omega}\times\mathbf{u}$ and $-\rho_{0}\boldsymbol{\Omega}\times(\boldsymbol{\Omega}\times\mathbf{r})$ are the Coriolis and centrifugal contributions in a rotating reference frame.

### 2.3 Conservation of Energy

$$
\rho_{0} c_{p}\left(\frac{\partial T}{\partial t} + \mathbf{u}\cdot\nabla T\right) = k \nabla^{2}T + \dot{q}
$$

where $c_{p}$ is specific heat, $k$ thermal conductivity, and $\dot{q}$ accounts for volumetric sources (Joule heating from induction currents, radiative exchange terms lumped as boundary conditions, latent heat release handled at the interface).

### 2.4 Conservation of Species (Solute/Dopant Transport)

$$
\frac{\partial C}{\partial t} + \mathbf{u}\cdot\nabla C = D \nabla^{2}C
$$

with $D$ the solutal diffusivity, typically $D \sim 10^{-5}\ \text{cm}^{2}/\text{s}$ in melts — several orders of magnitude smaller than thermal diffusivity $\alpha = k/(\rho_{0}c_{p})$, which is the root cause of double-diffusive phenomena (Section 6.4).

### 2.5 Interfacial (Stefan) Conditions at the Solid–Liquid Boundary

Latent heat balance (normal component, interface velocity $V_{n}$, latent heat $L$):

$$
k_{s}\left(\nabla T_{s}\cdot\mathbf{n}\right) - k_{l}\left(\nabla T_{l}\cdot\mathbf{n}\right) = \rho_{s} L\, V_{n}
$$

Solute rejection/segregation at the interface (mass conservation of species with segregation coefficient $k_{0}$):

$$
D\left(\nabla C\cdot\mathbf{n}\right) = V_{n}\left(1 - k_{0}\right)C_{i}
$$

Local interface temperature including curvature (Gibbs–Thomson) and kinetic undercooling:

$$
T_{i} = T_{m} - \Gamma \kappa - \mu_{k}\, V_{n} + m_{L}\left(C_{i} - C_{0}\right)
$$

where $\Gamma$ is the Gibbs–Thomson coefficient, $\kappa$ interface curvature, $\mu_{k}$ the kinetic coefficient, and $m_{L}$ the liquidus slope.

### 2.6 Free-Surface (Marangoni) Boundary Condition

At a free melt surface (meniscus in CZ, free surface in solution growth), the tangential stress balance includes thermocapillary (and solutocapillary) shear:

$$
\mu \frac{\partial u_{t}}{\partial n} = \frac{\partial \sigma}{\partial T}\nabla_{t}T + \frac{\partial \sigma}{\partial C}\nabla_{t}C
$$

where $\sigma$ is surface tension, $\nabla_{t}$ the tangential (surface) gradient operator, and $u_{t}$ tangential velocity.

---

## 3. Physical Driving Mechanisms of Convection

### 3.1 Buoyancy-Driven (Natural) Convection
Arises from density gradients due to temperature (thermal buoyancy) and/or concentration (solutal buoyancy) differences in the gravitational field. Dominant in Bridgman, VGF, and unforced regions of Czochralski melts. Characterized by the **Grashof number**:

$$
Gr_{T} = \frac{g\,\beta_{T}\,\Delta T\, L^{3}}{\nu^{2}}, \qquad Gr_{C} = \frac{g\,\beta_{C}\,\Delta C\, L^{3}}{\nu^{2}}
$$

with $\nu = \mu/\rho_{0}$ the kinematic viscosity and $L$ a characteristic length (melt depth, crucible radius).

### 3.2 Forced/Rotational Convection
Imposed by crystal and/or crucible rotation (CZ, LEC) or by pulling/translation (Bridgman). Characterized by the **rotational Reynolds number**:

$$
Re_{\Omega} = \frac{\Omega R^{2}}{\nu}
$$

and the **Ekman number**:

$$
Ek = \frac{\nu}{\Omega L^{2}}
$$

Rotation induces Ekman boundary layers at the crystal/crucible surfaces and can suppress or enhance buoyant convection depending on the relative rotation direction (co- or counter-rotation of crystal and crucible — the CRC configuration).

### 3.3 Marangoni (Thermocapillary/Solutocapillary) Convection
Surface-tension-gradient-driven flow along free surfaces, dominant in small-scale melts, microgravity, and floating-zone growth. Characterized by the **Marangoni number**:

$$
Ma = \frac{\left|\partial \sigma/\partial T\right|\, \Delta T\, L}{\mu\,\alpha}
$$

### 3.4 Electromagnetically Driven / Damped Convection
Applied static, alternating, cusp, or traveling magnetic fields exert a Lorentz force that can either damp turbulent buoyant flow (via magnetic braking, static axial/transverse fields) or drive controlled stirring (rotating/traveling fields). Characterized by the **Hartmann number**:

$$
Ha = B_{0} L \sqrt{\frac{\sigma_{e}}{\mu}}
$$

where $\sigma_{e}$ is electrical conductivity of the melt and $B_{0}$ the applied field strength. Magnetic damping suppresses velocity fluctuations approximately as $u \sim u_{0}/(1+Ha)$ in the diffusive limit.

### 3.5 Interface-Shape-Induced (Baroclinic) Flow
Non-planar (curved) melting/growth interfaces combined with rotation generate baroclinic torques because isotherms and constant-density surfaces are misaligned, contributing secondary flow structures superimposed on the primary buoyant/rotational circulation.

---

## 4. Governing Dimensionless Groups (Summary Table)

| Group | Definition | Physical Ratio |
|---|---|---|
| Grashof (thermal) | $Gr_{T} = g\beta_{T}\Delta T L^{3}/\nu^{2}$ | buoyancy / viscous |
| Grashof (solutal) | $Gr_{C} = g\beta_{C}\Delta C L^{3}/\nu^{2}$ | solutal buoyancy / viscous |
| Rayleigh (thermal) | $Ra_{T} = Gr_{T}\, Pr$ | buoyancy / (viscous $\times$ thermal diffusion) |
| Rayleigh (solutal) | $Ra_{C} = Gr_{C}\, Sc$ | solutal buoyancy / (viscous $\times$ solutal diffusion) |
| Prandtl | $Pr = \nu/\alpha$ | momentum diffusivity / thermal diffusivity |
| Schmidt | $Sc = \nu/D$ | momentum diffusivity / solutal diffusivity |
| Lewis | $Le = \alpha/D = Sc/Pr$ | thermal / solutal diffusivity |
| Marangoni | $Ma = |\partial\sigma/\partial T|\Delta T L/(\mu\alpha)$ | thermocapillary / viscous-thermal diffusion |
| Reynolds (rotational) | $Re_{\Omega} = \Omega R^{2}/\nu$ | rotational inertia / viscous |
| Ekman | $Ek = \nu/(\Omega L^{2})$ | viscous / Coriolis |
| Hartmann | $Ha = B_{0}L\sqrt{\sigma_{e}/\mu}$ | Lorentz / viscous |
| Taylor | $Ta = 4\Omega^{2}L^{4}/\nu^{2}$ | Coriolis$^{2}$ / viscous$^{2}$ |

Since $Le \gg 1$ typically (thermal diffusion much faster than solutal diffusion in melts), thermal and solutal fields evolve on very different timescales — the essential ingredient for double-diffusive instabilities.

---

## 5. Instability Mechanisms

### 5.1 Rayleigh–Bénard (Thermal Buoyant) Instability
Onset of convective rolls/plumes when a fluid layer heated from below (or with unstable radial/axial temperature gradient) exceeds a critical Rayleigh number. For an idealized horizontal layer with rigid–rigid boundaries:

$$
Ra_{T,c} \approx 1708
$$

For rigid–free boundaries, $Ra_{T,c}\approx 1101$; for free–free, $Ra_{T,c}=657.5\pi^{4}/16 \approx 657.5$ (classical Rayleigh result). In crystal growth geometries (cylindrical crucibles with radial and axial gradients, curved interfaces), the critical value is geometry-dependent and obtained numerically via linear stability analysis (Section 6).

### 5.2 Solutal (Rayleigh) Instability
Analogous instability driven by an unstable solute gradient (e.g., rejected solute accumulating at the growth interface with $k_{0}<1$ producing a destabilizing solutally light or heavy layer depending on sign of $\beta_{C}$):

$$
Ra_{C} = \frac{g\,\beta_{C}\,\Delta C\, L^{3}}{\nu D}
$$

Because $D \ll \alpha$, the solutal Rayleigh number can be enormous even for small $\Delta C$, making solutal convection typically far more vigorous and harder to suppress than thermal convection alone.

### 5.3 Double-Diffusive Convection
When both thermal and solutal gradients are present with opposing effects on density (e.g., stabilizing thermal gradient but destabilizing solutal gradient near the interface, or vice versa), the system can be linearly stable in the classical single-diffusive sense yet unstable to **double-diffusive** modes (salt-fingering or diffusive-layering analogues), because the fast-diffusing component (heat) can locally stabilize while the slow-diffusing component (solute) still drives overturning. The stability boundary depends jointly on $Ra_{T}$, $Ra_{C}$, and $Le$:

$$
R_{\rho} = \frac{\beta_{C}\,\Delta C}{\beta_{T}\,\Delta T}
$$

($R_{\rho}$ is the density ratio); instability can occur even when the net density stratification is nominally stable if $R_{\rho}$ lies in a critical range set by $Le$. This mechanism is directly responsible for layered convective structures and growth striations in doped melt growth (Czochralski, Bridgman) and in solution growth (e.g., high-temperature solution/flux growth with strong solutal gradients).

### 5.4 Marangoni–Bénard Instability
Thermocapillary analogue of Rayleigh–Bénard: onset when the surface-tension-driven Marangoni number exceeds a critical value,

$$
Ma_{c} \approx 79.6 \quad \text{(idealized flat, non-deformable free surface, no gravity)}
$$

with the critical value modified by the Biot number (surface heat loss), aspect ratio, and presence of a simultaneous buoyancy contribution (combined Rayleigh–Marangoni instability), often expressed through the **dynamic Bond number**:

$$
Bd = \frac{Ra_{T}}{Ma} = \frac{g\,\beta_{T}\,\rho_{0}\, L^{2}}{\left|\partial \sigma/\partial T\right|}
$$

which measures the relative importance of buoyancy versus thermocapillarity; $Bd \ll 1$ (small scale, microgravity) favors Marangoni-dominated instability, $Bd \gg 1$ favors classical buoyant Rayleigh–Bénard behavior.

### 5.5 Rotationally Induced Instabilities
- **Taylor–Görtler / centrifugal instability**: destabilization of boundary-layer flow along curved rotating surfaces when the Taylor number exceeds a critical value $Ta_{c}$, generating streamwise vortices.
- **Baroclinic (rotating stratified) instability**: arises when rotation and an unstable or even stable density stratification interact under a non-planar interface, producing oscillatory or traveling-wave secondary flows.
- **Ekman layer instability**: instability of the thin viscous boundary layer at rotating solid surfaces, generating spiral vortices when the local Reynolds number based on Ekman layer thickness $\delta_{E} = \sqrt{\nu/\Omega}$ exceeds a threshold.

### 5.6 Shear (Kelvin–Helmholtz-type) Instability
At interfaces between counter-rotating flow regions (e.g., counter-rotating crystal/crucible in CZ growth, or opposing forced/buoyant flow cells), strong velocity shear can generate Kelvin–Helmholtz-type instabilities superimposed on the buoyant/rotational base flow, contributing to time-dependent, often 3D, non-axisymmetric flow structures even in nominally axisymmetric geometries.

### 5.7 Oscillatory Transition and Route to Turbulence
As the controlling Rayleigh/Grashof number is increased beyond several critical thresholds, melt convection typically transitions:

$$
\text{steady axisymmetric} \;\rightarrow\; \text{steady 3D (symmetry-breaking)} \;\rightarrow\; \text{periodic oscillatory} \;\rightarrow\; \text{quasi-periodic} \;\rightarrow\; \text{chaotic/turbulent}
$$

Oscillatory convection is of particular technological concern because it produces time-periodic temperature fluctuations at the growth interface, directly causing **growth striations** (periodic dopant banding) when the oscillation period is commensurate with or shorter than the crystal pulling/rotation timescale.

---

## 6. Linear Stability Analysis Formulation

The standard approach: decompose all fields into a steady (or quasi-steady) base state plus infinitesimal perturbations,

$$
\mathbf{u} = \mathbf{U}_{0} + \mathbf{u}', \qquad T = T_{0} + T', \qquad C = C_{0} + C', \qquad p = P_{0} + p'
$$

Substitute into the governing equations, linearize (drop products of primed quantities), and seek normal-mode solutions:

$$
\left(\mathbf{u}', T', C', p'\right) \sim \left(\hat{\mathbf{u}}(z), \hat{T}(z), \hat{C}(z), \hat{p}(z)\right)\exp\left(i\,\mathbf{k}\cdot\mathbf{x}_{\parallel} + \sigma t\right)
$$

where $\mathbf{k}$ is the horizontal (or azimuthal) wavenumber and $\sigma = \sigma_{r} + i\sigma_{i}$ the complex growth rate. The system reduces to a generalized eigenvalue problem of Orr–Sommerfeld type; e.g., for the simplified Boussinesq Rayleigh–Bénard problem the vertical velocity perturbation $\hat{w}(z)$ satisfies:

$$
\left(\frac{d^{2}}{dz^{2}} - k^{2} - \frac{\sigma}{\nu}\right)\left(\frac{d^{2}}{dz^{2}} - k^{2}\right)\hat{w} = -\frac{g\beta_{T} k^{2}}{\nu}\hat{T}
$$

$$
\left(\frac{d^{2}}{dz^{2}} - k^{2} - \frac{\sigma}{\alpha}\right)\hat{T} = -\frac{\Delta T}{L}\hat{w}
$$

**Marginal stability** corresponds to $\sigma_{r}=0$: solving the resulting eigenvalue problem for each $k$ and minimizing over $k$ yields the critical Rayleigh number $Ra_{c}$ and critical wavenumber $k_{c}$. For $\sigma_{i}=0$ at marginal stability the instability is a **stationary** (steady) mode; for $\sigma_{i}\neq 0$ it is an **oscillatory** mode — this bifurcation type ($\sigma_{i}=0$ vs. $\sigma_{i}\neq 0$) is precisely what differentiates classical Rayleigh–Bénard onset from oscillatory double-diffusive or rotating-system onset.

In realistic crystal-growth geometries (cylindrical, non-planar interface, rotating frame, non-uniform base flow $\mathbf{U}_ {0}(r,z)$ obtained itself from a nonlinear 2D/axisymmetric steady-state solve), the linearized perturbation equations are solved numerically (spectral or finite-element global stability analysis) rather than analytically, yielding a critical control parameter (rotation rate, $\Delta T$, or field strength) at which the leading eigenvalue crosses $\sigma_ {r}=0$, and the corresponding critical azimuthal mode number $m$ (since perturbations in a cylindrical geometry are expanded as $\exp(im\theta)$ rather than plane waves).

---

## 7. Coupling Between Convection and the Growth Interface

### 7.1 Interface Shape and Convective Heat Transport
The interface shape (deflection, curvature) is set by the balance of conductive and convective heat fluxes on both sides. Strong convective flow impinging on the interface flattens or deforms it; the local interface-normal heat flux balance is:

$$
\rho_{s}L\,V_{n} = k_{s}\left(\nabla T_{s}\cdot\mathbf{n}\right) - k_{l}\left(\nabla T_{l}\cdot\mathbf{n}\right)_{\text{convective + conductive}}
$$

where the liquid-side gradient now reflects the convective thermal boundary layer thickness $\delta_{T} \sim L/Nu$ rather than the pure conduction length scale, with **Nusselt number** $Nu$ quantifying convective enhancement of heat transport:

$$
Nu = \frac{q_{\text{conv+cond}}}{q_{\text{cond only}}}
$$

### 7.2 Constitutional Supercooling and Morphological Instability
Convective transport controls the solute boundary-layer thickness $\delta_{C}$ ahead of the interface, which in turn controls the actual concentration gradient driving the classical **constitutional supercooling criterion** (Mullins–Sekerka / Tiller criterion) for interface morphological (cellular/dendritic) instability:

$$
\frac{G_{L}}{V} < \frac{m_{L}\, C_{0}\left(1-k_{0}\right)}{D\, k_{0}}
$$

where $G_{L}$ is the liquid-side temperature gradient at the interface and $V$ the growth velocity. Convection thins $\delta_{C}$ (effectively raising the apparent segregation coefficient toward $k_{0}$, via the Burton–Prim–Slichter relation below), thereby *stabilizing* the interface against constitutional supercooling — one of the principal reasons forced/rotational stirring is deliberately used in practice.

### 7.3 Effective Segregation Coefficient (Burton–Prim–Slichter, BPS)
Convective boundary-layer thickness $\delta$ modifies the effective segregation coefficient:

$$
k_{\text{eff}} = \frac{k_{0}}{k_{0} + \left(1-k_{0}\right)\exp\left(-V\delta/D\right)}
$$

with $\delta$ decreasing as convective stirring intensity (rotation rate, forced flow) increases; $k_{\text{eff}} \to k_{0}$ in the well-mixed (strong convection) limit and $k_{\text{eff}}\to 1$ in the diffusion-controlled (stagnant) limit. Time-dependent (oscillatory) convection produces a time-varying $\delta(t)$ and hence time-varying $k_{\text{eff}}$, directly producing **growth striations** — periodic, often ring-like, dopant concentration bands frozen into the crystal.

### 7.4 Rotationally Driven Interface Stabilization (CRC Effect)
In Czochralski growth, crystal/crucible counter-rotation (CRC) generates an Ekman-layer-driven flow that actively suppresses buoyant plume penetration to the interface, damping temperature/concentration oscillations and reducing striation amplitude — an example of using one convective mechanism (forced rotational) to counteract another (buoyant thermal/solutal).

---

## 8. Modeling and Numerical Considerations in Continuum Melt-Growth Simulators

Global furnace-scale simulators (CGSim, CrysMAS, FEMAG/FEMAG-CZ, CrysVUn, Cats2D) solve the coupled system above together with:

- **Global heat transport**: conduction in all solid furnace components (crucible, susceptor, insulation, heater), radiative exchange between diffuse–gray or spectral surfaces (view-factor or Monte-Carlo radiosity methods), and induction heating (solved via the magnetic vector potential / eddy-current equations) or resistive heating, all coupled to the melt convection–diffusion problem.
- **Free/deformable interfaces**: both the melt free surface (meniscus) and the solid–liquid interface are unknown, curved, moving boundaries determined iteratively (front-tracking, ALE moving-mesh, or level-set/phase-field approaches) as part of the global thermal-convective solution — not prescribed a priori.
- **Turbulence closure**: at high $Ra$ (industrial-scale CZ silicon melts routinely reach $Ra \sim 10^{9}$–$10^{12}$), transitional/turbulent closure models (low-Reynolds-number $k$–$\varepsilon$, RANS variants, or time-dependent large-eddy-resolving axisymmetric/3D transient solves) are required since direct laminar steady-state solution is not physically valid.
- **Reduced-dimensionality trade-off**: 2D axisymmetric models capture mean buoyant/rotational circulation efficiently but cannot capture $m\neq 0$ non-axisymmetric instability modes (Section 6); fully 3D transient simulation is required to capture oscillatory striation-inducing convection, at substantially higher computational cost.
- **Magnetic field coupling**: for MCZ/EMCZ configurations, the induction/Lorentz-force problem is two-way coupled to the melt momentum equation (Section 3.4), often requiring sub-cycling between electromagnetic and fluid-thermal solvers due to disparate time scales.

---

## 9. Summary of Key Non-Dimensional Stability Criteria

$$
Ra_{T} = \frac{g\,\beta_{T}\,\Delta T\, L^{3}}{\nu\,\alpha} \;>\; Ra_{T,c}\ \left(\approx 657\text{–}1708,\ \text{geometry-dependent}\right) \;\Rightarrow\; \text{buoyant instability}
$$

$$
Ma = \frac{\left|\partial\sigma/\partial T\right|\Delta T L}{\mu \alpha} \;>\; Ma_{c}\ \left(\approx 80,\ \text{idealized}\right) \;\Rightarrow\; \text{thermocapillary instability}
$$

$$
Ta = \frac{4\Omega^{2}L^{4}}{\nu^{2}} \;>\; Ta_{c} \;\Rightarrow\; \text{centrifugal/rotational instability}
$$

$$
R_{\rho} = \frac{\beta_{C}\Delta C}{\beta_{T}\Delta T} \in \left[R_{\rho,\min}(Le),\, R_{\rho,\max}(Le)\right] \;\Rightarrow\; \text{double-diffusive instability window}
$$

Together, these criteria — evaluated via global linear stability analysis on the actual nonlinear base flow computed from the full continuum model — define the operating windows (rotation rate, applied field strength, thermal gradient, growth rate) within which melt/solution growth can be run without triggering time-dependent convective instabilities that degrade crystal quality through striations, interface faceting, or macroscopic inclusion of secondary phases.


---

> [!NOTE]
> 
> Generated by Claude.ai
>
> Model: Sonet 5
>
> Prompt: Provide an exhaustive description of the Convective Transport and Instability Phenomena in the Continuum (Macroscopic) Model of Melt/Solution Growth. For equation formulation use latex symbols and $$ delimiter. In equations use command `\ast` instead of the literal `*`. Show the output in Markdown format. Do not copy the output of the exported files into the chat.
