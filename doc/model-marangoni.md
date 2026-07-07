# Marangoni (Thermocapillary) Convection

## 1. Physical Origin and Definition

Marangoni convection — also called thermocapillary convection, or, when solutal effects dominate, solutocapillary convection — is fluid motion driven by gradients of surface tension (interfacial tension) along a free or deformable interface. In crystal growth from the melt or from solution, the relevant interfaces are:

- The **free melt/solution surface** exposed to a gas ambient (e.g., the meniscus in Czochralski growth, the melt surface in a Bridgman crucible above the charge, the exposed liquid surface in solution growth).
- **Liquid–liquid interfaces** in encapsulated growth (e.g., Liquid Encapsulated Czochralski, LEC, where a boron oxide $B_2O_3$ layer floats on the melt).
- Bubble or droplet surfaces suspended in the melt (secondary effect, usually neglected in bulk growth models but relevant in defect/void formation studies).

Surface tension $\gamma$ is a function of temperature $T$ and, in multicomponent melts or solutions, of the local composition $C_i$ (concentration of component $i$). Whenever a temperature or concentration gradient exists along the interface, $\gamma$ varies spatially, and the resulting tangential stress imbalance drives fluid from regions of low $\gamma$ toward regions of high $\gamma$ (Marangoni flow moves fluid toward higher surface tension, dragging bulk fluid at the interface and generating a return flow in the bulk).

## 2. Constitutive Relation for Surface Tension

### 2.1 Linear (first-order) dependence

For most melt-growth systems away from critical points, a linear equation of state is used:

$$
\gamma(T, C) = \gamma_0 - \gamma_T (T - T_0) - \gamma_C (C - C_0)
$$

where:

- $\gamma_0$ is the reference surface tension at reference temperature $T_0$ and reference concentration $C_0$,
- $\gamma_T = -\dfrac{\partial \gamma}{\partial T}\Big|_{C}$ is the **temperature coefficient of surface tension** (usually $\gamma_T > 0$ for pure metals and semiconductor melts, meaning $\gamma$ decreases with increasing $T$),
- $\gamma_C = -\dfrac{\partial \gamma}{\partial C}\Big|_{T}$ is the **solutal (concentration) coefficient of surface tension**, which can be positive or negative depending on whether the solute is surface-active.

### 2.2 Surfactant-affected (nonlinear) dependence

For melts contaminated by surface-active impurities (oxygen in silicon melts, sulfur/selenium in metallic melts), $\gamma(T)$ can exhibit a **non-monotonic** dependence with a temperature of maximum surface tension $T_M$:

$$
\gamma(T) = \gamma_M + k_\gamma \left(T - T_M\right)\ln\left(\dfrac{T}{T_M}\right)
$$

or, in a simpler quadratic form used in some Marangoni-flow-reversal studies:

$$
\gamma(T) = \gamma_M - \dfrac{1}{2} k_\gamma (T - T_M)^2
$$

This nonlinearity is physically important because it produces a **sign reversal of $\partial\gamma/\partial T$** across the free surface, causing flow-reversal cells and multicellular Marangoni patterns — an effect well documented in silicon Czochralski melts contaminated with oxygen or sulfur.

## 3. Governing Equations of the Continuum Model

### 3.1 Bulk conservation equations

The melt/solution is treated as an incompressible (or Boussinesq-approximated), Newtonian, viscous fluid. The bulk field equations are:

**Continuity:**

$$
\nabla \ast \mathbf{u} = 0
$$

**Momentum (Navier–Stokes with Boussinesq buoyancy):**

$$
\rho_0 \left( \dfrac{\partial \mathbf{u}}{\partial t} + (\mathbf{u} \ast \nabla)\mathbf{u} \right) = -\nabla p + \mu \nabla^2 \mathbf{u} + \rho_0 \mathbf{g}\, \beta_T (T - T_{ref}) + \rho_0 \mathbf{g}\, \beta_C (C - C_{ref}) + \mathbf{F}_{Lorentz}
$$

where $\beta_T$ and $\beta_C$ are thermal and solutal expansion coefficients, and $\mathbf{F}_{Lorentz} = \mathbf{J} \times \mathbf{B}$ is included only when an external or induced magnetic field is present (magnetically damped Czochralski/Bridgman growth).

**Energy conservation:**

$$
\rho_0 c_p \left( \dfrac{\partial T}{\partial t} + (\mathbf{u} \ast \nabla) T \right) = k \nabla^2 T
$$

**Species (solute) transport (for solution growth or doped melts):**

$$
\dfrac{\partial C}{\partial t} + (\mathbf{u} \ast \nabla) C = D \nabla^2 C
$$

### 3.2 The Marangoni boundary condition at the free surface

At a free surface $\Gamma_{free}$ with unit outward normal $\mathbf{n}$ and unit tangent(s) $\mathbf{t}$, the interfacial (dynamic) stress balance requires that the jump in viscous traction across the interface equal the tangential gradient of surface tension. Neglecting gas-phase viscous stress (valid since $\mu_{gas} \ll \mu_{liquid}$), the tangential stress balance is:

$$
\mu \left( \dfrac{\partial u_t}{\partial n} \right) = \dfrac{\partial \gamma}{\partial t_{tan}} = \dfrac{\partial \gamma}{\partial T}\dfrac{\partial T}{\partial t_{tan}} + \dfrac{\partial \gamma}{\partial C}\dfrac{\partial C}{\partial t_{tan}}
$$

More generally, in vector/tensor form, the tangential projection of the interfacial stress balance is:

$$
\mathbf{t} \ast \boldsymbol{\tau} \ast \mathbf{n} = \mathbf{t} \ast \nabla_s \gamma
$$

where $\boldsymbol{\tau} = \mu \left( \nabla \mathbf{u} + (\nabla \mathbf{u})^{T} \right)$ is the viscous stress tensor and $\nabla_s = \nabla - \mathbf{n}(\mathbf{n} \ast \nabla)$ is the surface (tangential) gradient operator, so that:

$$
\nabla_s \gamma = \dfrac{\partial \gamma}{\partial T} \nabla_s T + \dfrac{\partial \gamma}{\partial C} \nabla_s C = -\gamma_T \nabla_s T - \gamma_C \nabla_s C
$$

This is the fundamental Marangoni boundary condition: **tangential surface-tension gradients directly prescribe the tangential viscous shear stress at the free surface**, in contrast to a rigid wall (no-slip) or a stress-free (zero-shear) boundary.

### 3.3 Normal stress balance and surface deformation

The normal component of the interfacial stress balance includes surface tension acting through curvature (Young–Laplace) plus viscous normal stress:

$$
p - p_{gas} + \mathbf{n} \ast \boldsymbol{\tau} \ast \mathbf{n} = \gamma \left( \nabla_s \ast \mathbf{n} \right) = 2 \gamma \kappa_{mean}
$$

where $\kappa_{mean}$ is the mean curvature of the deformed free surface. In most macroscopic Marangoni-flow models of melt growth, the meniscus/free-surface shape is either:

- Computed self-consistently from this normal-stress (capillary) balance together with hydrostatic and growth-angle conditions (as in Czochralski meniscus shape modeling), or
- Prescribed/fixed a priori (simplified planar or spherical-cap approximation) when only the tangential Marangoni-driven flow field is of interest.

## 4. Dimensionless Characterization

### 4.1 Marangoni number

The strength of thermocapillary convection relative to viscous/thermal diffusion is characterized by the **Marangoni number**:

$$
Ma = \dfrac{\gamma_T \, \Delta T \, L}{\mu \, \alpha}
$$

where $\Delta T$ is a characteristic temperature difference across the free surface of characteristic length $L$, $\mu$ is dynamic viscosity, and $\alpha = k/(\rho_0 c_p)$ is thermal diffusivity. Equivalently, $Ma$ can be written as the product of the thermal Reynolds/Peclet-type ratio:

$$
Ma = \dfrac{\gamma_T \, \Delta T \, L}{\mu \, \alpha} = Re_{Ma} \, Pr
$$

with $Pr = \nu/\alpha$ the Prandtl number and $\nu = \mu/\rho_0$ the kinematic viscosity.

### 4.2 Solutal Marangoni number

For solution growth or solutally driven surface-tension gradients:

$$
Ma_C = \dfrac{\gamma_C \, \Delta C \, L}{\mu \, D}
$$

with $D$ the solutal diffusivity.

### 4.3 Dynamic Bond number

The relative importance of Marangoni (surface-tension-driven) convection versus buoyancy-driven convection is quantified by the **dynamic Bond number**:

$$
Bd = \dfrac{Gr}{Ma} = \dfrac{\rho_0 \, g \, \beta_T \, \Delta T \, L^2}{\gamma_T \, \Delta T} = \dfrac{\rho_0 \, g \, \beta_T \, L^2}{\gamma_T}
$$

where $Gr = g \beta_T \Delta T L^3 / \nu^2$ is the Grashof number. Small $Bd$ (small length scale $L$, microgravity, or small melt volume) indicates Marangoni-dominated convection; large $Bd$ indicates buoyancy-dominated convection. This is why thermocapillary convection is of primary concern in:

- **Small-diameter crystal growth** (thin rods, fiber growth, floating-zone growth of small crystals),
- **Microgravity/space-based crystal growth experiments**, where buoyancy convection is suppressed and Marangoni flow becomes the dominant or sole convective mechanism,
- **Shallow melt pools** with a large free-surface-area-to-volume ratio.

### 4.4 Capillary and Crispation numbers

Additional dimensionless groups used when surface deformation is significant:

$$
Ca = \dfrac{\mu \, U_{ref}}{\gamma_0}, \qquad Cr = \dfrac{\mu \, \alpha}{\gamma_0 \, L}
$$

where $Ca$ (Capillary number) measures viscous-to-surface-tension forces and $Cr$ (Crispation number) measures the surface's deformability under thermal/viscous stress; both are typically small in melt growth (nearly non-deformable, "rigid" free surface approximation), except near menisci and thin liquid films.

## 5. Application to Specific Growth Configurations

### 5.1 Czochralski (CZ) growth

In CZ growth, the free melt surface between the crucible wall and the growing crystal (the meniscus region) is subject to a strong radial temperature gradient (hot crucible wall, cooler crystal/melt interface near the triple point). Since $\gamma_T > 0$ for most semiconductor and oxide melts, surface tension is higher at the cooler crystal edge, and Marangoni flow is directed **along the free surface from the hot crucible wall toward the cold crystal edge**, then descending near the crystal and returning along the bottom of the melt — a flow structure that can either reinforce or oppose buoyancy-driven and forced (rotation-driven) convection cells, depending on rotation rate, crucible geometry, and melt depth. This interaction governs radial dopant segregation, striations, and the shape of the melt/crystal interface.

### 5.2 Floating Zone (FZ) growth

In FZ growth, the entire lateral surface of the molten zone is a free surface (no crucible contact), making the process **the canonical configuration for Marangoni-convection studies**, since there is no crucible wall to dampen or complicate the flow. The zone is heated non-uniformly (typically hottest at the mid-height inductive/optical heating band, cooler at the melting and freezing interfaces at each end), producing two counter-rotating axisymmetric Marangoni cells directed from the hot equator toward each cooler solid–liquid interface. At sufficiently high $Ma$, this steady axisymmetric flow undergoes a hydrodynamic instability to **oscillatory, three-dimensional flow** — the classical Marangoni/hydrothermal-wave transition extensively studied both computationally and in reduced-gravity FZ experiments, and is a principal source of dopant striations in FZ silicon.

### 5.3 Liquid Encapsulated Czochralski (LEC)

In LEC growth (e.g., GaAs, InP), the encapsulant layer (molten $B_2O_3$) introduces a **liquid–liquid interface** in addition to the encapsulant's own free surface with the ambient gas. Marangoni stresses act at both interfaces, and the encapsulant's own convection is coupled to, and can partially decouple or damp, thermocapillary stresses transmitted to the underlying melt, an effect exploited to stabilize growth interfaces in low-thermal-conductivity III-V melts.

### 5.4 Bridgman/VGF (Vertical Gradient Freeze) and vapor-phase or solution growth

In Vertical Bridgman and VGF configurations, the free surface is typically restricted to a small region above the charge (or absent entirely if the ampoule is fully sealed and liquid-filled), so Marangoni effects are generally of secondary importance relative to buoyancy convection, except during the initial melt-back stage or in partially filled ampoules with a gas bubble. In solution growth (e.g., aqueous or high-temperature solution growth of oxide crystals), solutal Marangoni convection ($Ma_C$) can be significant at the free solution surface when strong concentration gradients develop due to evaporation or growth-driven depletion.

## 6. Coupling with Other Transport Phenomena

### 6.1 Interaction with buoyancy convection

Marangoni and buoyancy-driven natural convection generally coexist in ground-based (1-g) melt growth. Their relative strength is set by $Bd$ (Section 4.3). The two mechanisms may be **co-rotating** (reinforcing a single convective cell) or **counter-rotating** (producing a double- or multi-cell flow structure with an internal stagnation/separation surface), with important consequences for the effective segregation coefficient and interface shape.

### 6.2 Interaction with forced convection (crystal/crucible rotation)

Imposed rotation (crystal rotation $\omega_{cr}$, crucible counter-rotation $\omega_{cru}$) generates centrifugally-driven (Ekman-type) flow that interacts with the Marangoni cell near the free surface. The rotational Reynolds number:

$$
Re_{\Omega} = \dfrac{\omega \, R^2}{\nu}
$$

competes with $Ma$ to determine whether the near-surface flow is Marangoni-dominated (radially outward/inward along the surface as described above) or rotation-dominated (Ekman pumping toward or away from the rotation axis).

### 6.3 Interaction with magnetic damping

In electrically conducting melts (silicon, metals, some oxide melts), applied static or rotating/traveling magnetic fields introduce a Lorentz force $\mathbf{F}_{Lorentz} = \mathbf{J} \times \mathbf{B}$ in the momentum equation (Section 3.1) that damps bulk buoyancy-driven flow more effectively than it damps the near-surface Marangoni flow, since the Marangoni cell is confined to a thin region near the free surface where the Hartmann-layer damping is less effective; consequently, under strong magnetic fields, Marangoni convection can become the **relatively dominant** residual flow even though its absolute magnitude is also reduced.

### 6.4 Hydrothermal wave instability

At supercritical Marangoni number, the steady thermocapillary flow along a free surface with an imposed horizontal temperature gradient becomes linearly unstable to a traveling oscillatory instability known as a **hydrothermal wave**, propagating obliquely to the temperature gradient. The critical Marangoni number $Ma_{cr}$ and wave characteristics (frequency, propagation angle, wavelength) depend on the Prandtl number of the melt and the depth-to-length aspect ratio of the liquid layer. This instability is the principal driver of **dopant striations** in Marangoni-affected melt growth (particularly FZ silicon), since the oscillatory surface flow periodically perturbs the growth-interface boundary layer and hence the local growth rate and dopant incorporation.

### 6.5 Interaction with evaporation and surfactants

In systems where evaporation of a volatile component occurs at the free surface (e.g., some oxide melts, solution growth with solvent evaporation), the resulting surface concentration gradient adds a solutal Marangoni contribution ($Ma_C$) that can reinforce or oppose the thermal Marangoni flow, depending on the sign of $\gamma_C$ and the direction of net mass transfer. Surface-active trace impurities (Section 2.2) can furthermore reverse the sign of $\gamma_T$ locally, producing flow reversal and multicellular structures even under a monotonic imposed temperature field.

## 7. Numerical/Computational Treatment in Continuum Growth Models

In practice, continuum (macroscopic) melt-growth simulation codes (e.g., global growth-furnace models used for CZ, FZ, VGF simulation) implement the Marangoni condition as a **Neumann-type (natural) boundary condition on the tangential velocity/shear stress** at the free-surface boundary of the melt domain, evaluated using the locally computed surface temperature field from the coupled heat-transfer solution:

$$
\mu \dfrac{\partial u_t}{\partial n}\bigg|_{\Gamma_{free}} = -\gamma_T \dfrac{\partial T}{\partial s}\bigg|_{\Gamma_{free}}
$$

with $s$ the arc-length coordinate along the free surface. This is solved simultaneously (fully coupled) or in a segregated iterative manner with:

- The global heat transfer model (conduction, convection, and radiative exchange with furnace/ambient boundaries) that determines the surface temperature distribution $T(s)$,
- The free-surface (meniscus) shape equation, when surface deformation is not neglected,
- The bulk Navier–Stokes/energy/species system (Section 3.1),
- Turbulence or transitional-flow closure models, when the local Reynolds/Marangoni number indicates a turbulent or oscillatory regime rather than laminar steady flow, since direct numerical resolution of hydrothermal-wave and higher instabilities is computationally demanding in full 3D furnace-scale simulations, and Reynolds-averaged or large-eddy approaches are frequently substituted.

## 8. Summary of Key Physical Consequences for Crystal Quality

- **Radial and axial dopant/impurity segregation**: Marangoni flow alters the effective boundary-layer thickness at the growth interface, changing the effective segregation coefficient (Burton–Prim–Slichter-type framework).
- **Growth striations**: time-dependent (oscillatory or unsteady) Marangoni flow, particularly via hydrothermal-wave instability, imprints periodic dopant/impurity striations correlated with the flow's characteristic frequency.
- **Interface shape**: the additional momentum injected at the free surface changes the melt flow pattern and hence the shape and stability of the solid–liquid growth interface.
- **Microgravity relevance**: since Marangoni convection persists in the absence of gravity while buoyancy convection is suppressed, it is the dominant (often only) convective transport mechanism in space-based/microgravity melt-growth experiments, motivating dedicated theoretical and experimental study of thermocapillary flow independent of buoyancy effects.

## 9. Key Governing Non-Dimensional Groups (Consolidated Reference)

$$
Ma = \dfrac{\gamma_T \Delta T L}{\mu \alpha}, \qquad
Ma_C = \dfrac{\gamma_C \Delta C L}{\mu D}, \qquad
Pr = \dfrac{\nu}{\alpha}, \qquad
Gr = \dfrac{g \beta_T \Delta T L^3}{\nu^2}
$$

$$
Bd = \dfrac{Gr}{Ma}, \qquad
Ca = \dfrac{\mu U_{ref}}{\gamma_0}, \qquad
Cr = \dfrac{\mu \alpha}{\gamma_0 L}, \qquad
Re_\Omega = \dfrac{\omega R^2}{\nu}
$$

---

> [!NOTE]
> 
> Generated by Claude.ai
>
> Model: Sonet 5
>
> Prompt: Provide an exhaustive description of the Marangoni (thermocapillary) convection phenomena in the Continuum (Macroscopic) Model of Melt/Solution Growth. Provide description of all physical relevant phenomena. For equation formulation use latex symbols and $$ delimiter. In equations use command \ast instead of the literal *. Show the output in Markdown format. Do not copy the output of the exported files into the chat.
