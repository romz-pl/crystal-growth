# Forced Convection from Crystal and Crucible Rotation

## 1. Physical Context and Role in the Continuum Model

In the continuum (macroscopic) description of melt- and solution-growth processes (Czochralski, LEC, Kyropoulos, Bridgman/VGF variants, and solution methods), the melt is treated as a Newtonian, incompressible, viscous fluid governed by the Navier–Stokes equations coupled to heat and species transport. Rotation of the crystal and/or the crucible is one of the principal external control mechanisms — alongside buoyancy, Marangoni stress, and applied magnetic fields — used to shape the melt flow, the shape of the solid–liquid interface, dopant/solute distribution, and the thermal field near the growth front.

Rotation-driven flow is classified as **forced convection** because it is imposed by a prescribed mechanical boundary condition (an externally specified angular velocity) rather than arising spontaneously from density gradients (buoyancy-driven **natural convection**) or surface-tension gradients (**Marangoni/thermocapillary convection**). In real growth systems all three mechanisms are simultaneously present and nonlinearly coupled; forced convection due to rotation is superimposed on, and interacts strongly with, natural and Marangoni convection, as well as with any applied or self-induced magnetic damping.

The purpose of rotation in melt growth includes:
- Promoting axisymmetry of the temperature field and, hence, of the growth interface shape.
- Enhancing or suppressing radial and axial mixing to control dopant/impurity segregation.
- Counteracting or reinforcing buoyant convection cells to stabilize the flow (suppress time-dependent, oscillatory, or turbulent regimes).
- Controlling boundary-layer thickness at the crystal–melt interface, which governs effective segregation coefficients.
- Managing melt free-surface shape (meniscus) in Czochralski-type pulling.

## 2. Governing Equations of the Melt Flow

### 2.1 Continuity and Momentum (Navier–Stokes, Boussinesq approximation)

The melt is modeled in a rotating or fixed cylindrical coordinate system $(r, \varphi, z)$, generally assumed axisymmetric (2D axisymmetric approximation) unless three-dimensional effects (asymmetric heating, non-axisymmetric crucible shapes, or rotational instabilities) must be resolved.

**Continuity (incompressibility):**

$$
\nabla \cdot \mathbf{u} = 0
$$

**Momentum equation with Boussinesq buoyancy approximation:**

$$
\rho_0 \left( \frac{\partial \mathbf{u}}{\partial t} + (\mathbf{u} \cdot \nabla)\mathbf{u} \right) = -\nabla p + \mu \nabla^2 \mathbf{u} + \rho_0 \mathbf{g} \,\beta_T (T - T_{ref}) + \rho_0 \mathbf{g}\,\beta_C (C - C_{ref})
$$

where:
- $\mathbf{u} = (u_r, u_\varphi, u_z)$ is the melt velocity field,
- $p$ is the reduced pressure,
- $\mu$ is the dynamic viscosity, $\rho_0$ the reference density,
- $\beta_T$, $\beta_C$ are the thermal and solutal expansion coefficients,
- $T_{ref}$, $C_{ref}$ are reference temperature and solute concentration.

For non-axisymmetric or transient rotational instabilities, the full 3D form of the Navier–Stokes equations must be retained; for time-averaged, axisymmetric baseline flow, the swirl (azimuthal) component $u_\varphi$ is retained explicitly even under the axisymmetric assumption ($\partial/\partial\varphi = 0$), giving rise to the characteristic **meridional–swirl flow decomposition**.

### 2.2 Axisymmetric Form with Swirl

In cylindrical coordinates under the axisymmetric assumption, the momentum equations split into:

**Radial:**

$$
\rho_0\left(\frac{\partial u_r}{\partial t} + u_r \frac{\partial u_r}{\partial r} + u_z \frac{\partial u_r}{\partial z} - \frac{u_\varphi^2}{r}\right) = -\frac{\partial p}{\partial r} + \mu \left(\nabla^2 u_r - \frac{u_r}{r^2}\right)
$$

**Azimuthal (swirl):**

$$
\rho_0\left(\frac{\partial u_\varphi}{\partial t} + u_r \frac{\partial u_\varphi}{\partial r} + u_z \frac{\partial u_\varphi}{\partial z} + \frac{u_r u_\varphi}{r}\right) = \mu \left(\nabla^2 u_\varphi - \frac{u_\varphi}{r^2}\right)
$$

**Axial:**

$$
\rho_0\left(\frac{\partial u_z}{\partial t} + u_r \frac{\partial u_z}{\partial r} + u_z \frac{\partial u_z}{\partial z}\right) = -\frac{\partial p}{\partial z} + \mu \nabla^2 u_z + \rho_0 g \,\beta_T (T - T_{ref})
$$

The term $-u_\varphi^2/r$ in the radial equation is the **centrifugal term**, and the term $u_r u_\varphi / r$ in the azimuthal equation represents **Coriolis-like coupling** between meridional and swirl flow. This coupling is the mathematical origin of the classic **Ekman pumping** phenomenon central to rotating flows.

## 3. Boundary Conditions Representing Rotation

### 3.1 Crystal Rotation

At the crystal–melt interface (typically $z = z_{int}(r)$, the possibly curved solidification front), a no-slip condition is imposed with a prescribed rigid-body rotation of angular velocity $\omega_{cr}$:

$$
u_r = 0, \qquad u_\varphi = \omega_{cr}\, r, \qquad u_z = V_{gr}
$$

where $V_{gr}$ is the crystal pulling/growth velocity (normal to the interface, typically small compared to convective velocity scales), and $\omega_{cr}$ is the crystal angular rotation rate, taken positive or negative depending on rotation sense.

### 3.2 Crucible Rotation

At the crucible wall (side and bottom, $r = R_{cr}(z)$ or $z = z_{bottom}(r)$), the no-slip condition imposes:

$$
u_r = 0, \qquad u_\varphi = \omega_{cru}\, r, \qquad u_z = 0
$$

with $\omega_{cru}$ the crucible angular velocity (in Czochralski systems this may differ in magnitude and sign from $\omega_{cr}$, giving rise to **counter-rotation** ($\omega_{cr}\,\omega_{cru} < 0$) or **co-rotation** ($\omega_{cr}\,\omega_{cru} > 0$) configurations, or time-dependent/oscillatory rotation schedules known as **Accelerated Crucible Rotation Technique, ACRT**).

### 3.3 Free Surface (Meniscus) Boundary

At the free melt surface (in CZ-type growth), a stress-balance (dynamic) boundary condition applies, combining viscous shear from Marangoni stress with the kinematic requirement of a traction-free or surfactant-affected surface:

$$
\mu \frac{\partial u_\varphi}{\partial z}\bigg|_{surface} = 0 \quad \text{(if Marangoni effects on swirl are neglected)}
$$

while radial/axial components are coupled to the thermocapillary (Marangoni) shear:

$$
\mu \frac{\partial u_t}{\partial n} = \frac{\partial \sigma}{\partial T}\frac{\partial T}{\partial t}
$$

where $u_t$ is the tangential surface velocity, $\sigma(T)$ the temperature-dependent surface tension, and $n$, $t$ denote normal and tangential directions along the free surface.

## 4. Dimensionless Parameters Governing Rotational Forced Convection

### 4.1 Rotational Reynolds Number

The primary dimensionless group characterizing forced convection from rotation is the **rotational Reynolds number**:

$$
Re_\omega = \frac{\omega R^2}{\nu}
$$

where $\omega$ is the relevant angular velocity (crystal or crucible), $R$ a characteristic radius (crystal radius $R_{cr}$ or crucible radius $R_{cru}$), and $\nu = \mu/\rho_0$ the kinematic viscosity of the melt. $Re_\omega$ quantifies the ratio of inertial (rotational) to viscous forces and determines whether the rotationally-driven boundary layer is laminar, transitional, or turbulent.

### 4.2 Ekman Number

$$
Ek = \frac{\nu}{\omega L^2}
$$

with $L$ a characteristic length scale (e.g., melt depth). The Ekman number measures the ratio of viscous to Coriolis forces and controls the thickness of the rotational (Ekman) boundary layer.

### 4.3 Grashof and Rayleigh Numbers (for comparison with buoyancy)

$$
Gr = \frac{g \beta_T \Delta T\, L^3}{\nu^2}, \qquad Ra = Gr \cdot Pr
$$

where $Pr = \nu/\alpha$ is the Prandtl number ($\alpha$ = thermal diffusivity), and $\Delta T$ the characteristic temperature difference across the melt.

### 4.4 Rotational-to-Buoyancy Ratio

The relative strength of forced (rotational) versus natural (buoyant) convection is characterized by:

$$
\frac{Gr}{Re_\omega^2}
$$

- $Gr/Re_\omega^2 \gg 1$: buoyancy-dominated (natural convection regime).
- $Gr/Re_\omega^2 \ll 1$: rotation-dominated (forced convection regime).
- $Gr/Re_\omega^2 \sim O(1)$: mixed convection, most technologically relevant and most difficult to model, since flow instabilities (oscillatory, three-dimensional) are most prevalent in this regime.

### 4.5 Marangoni Number (for completeness in coupled systems)

$$
Ma = \frac{|\partial \sigma/\partial T|\, \Delta T\, L}{\mu \alpha}
$$

## 5. Physical Mechanisms of Rotationally-Driven Forced Convection

### 5.1 von Kármán Rotating-Disk-Type Flow (Crystal Rotation)

Crystal rotation about the vertical (growth) axis induces a flow analogous to the classical **von Kármán rotating-disk problem**. The rotating crystal acts as a centrifugal pump:
- Melt near the disk (crystal) surface is flung radially outward by centrifugal action.
- This radial outflow is compensated by axial inflow of melt from the bulk toward the crystal (upward toward the crystal in a bottom-fed configuration, i.e., melt is drawn axially upward toward the growth interface).
- Continuity is satisfied by return flow that recirculates in the crucible bulk.

The self-similar von Kármán solution gives characteristic velocity profiles:

$$
u_r = \omega r\, F(\zeta), \qquad u_\varphi = \omega r\, G(\zeta), \qquad u_z = \sqrt{\omega \nu}\, H(\zeta)
$$

where $\zeta = z\sqrt{\omega/\nu}$ is the similarity variable, and $F$, $G$, $H$ are the classical von Kármán functions satisfying a coupled nonlinear ODE system. The boundary-layer thickness scales as:

$$
\delta_{rot} \sim \sqrt{\frac{\nu}{\omega}}
$$

This defines the **rotational (von Kármán) boundary layer** at the crystal–melt interface, a region of intensified shear and enhanced radial/axial transport that directly governs the local mass-transfer boundary layer for dopant segregation.

### 5.2 Ekman Layer Physics

At solid rotating boundaries (crystal, crucible bottom) in a rotating bulk fluid, viscous stresses generate a thin **Ekman layer** in which the balance of centrifugal, Coriolis, viscous, and pressure-gradient forces produces a net radial (secondary) flow distinct from the bulk geostrophic-like flow. The classical Ekman layer thickness is:

$$
\delta_{Ek} \sim \sqrt{\frac{\nu}{\omega}}
$$

**Ekman pumping/suction**: axial flow is pumped into or out of the Ekman layer to satisfy mass conservation, coupling the boundary layer dynamics to the interior meridional flow. This mechanism is central to how crystal and crucible rotation control the overall melt recirculation pattern, and is highly sensitive to the rotation direction and rate at each boundary.

### 5.3 Crucible Rotation and Secondary Flow

Independent rotation of the crucible generates an analogous, but oppositely structured, near-wall boundary layer at the crucible walls and bottom:
- Crucible rotation alone (crystal stationary) tends to entrain melt into rigid-body-like rotation in the bulk, with weaker secondary meridional circulation.
- Counter-rotation (crystal and crucible spinning in opposite senses) creates a strong shear layer in the melt interior, which can stabilize or destabilize the flow depending on the ratio $\omega_{cr}/\omega_{cru}$ and the Reynolds numbers involved; this shear layer is often associated with enhanced radial mixing and improved dopant homogeneity, but can also trigger flow instabilities.
- Co-rotation tends to produce more uniform, rigid-body-like rotation of the bulk melt with weaker secondary flow and reduced mixing.

### 5.4 Competition Between Forced (Rotational) and Natural (Buoyant) Convection

In practical melt-growth systems, radial and axial temperature gradients (from crucible heating and heat extraction through the growing crystal) drive buoyant convection cells that would exist independent of rotation. Forced convection from rotation:
- **Suppresses buoyant cells** when $Re_\omega$ is large relative to $Gr^{1/2}$: strong crystal rotation "spins down" and stabilizes buoyancy-driven plumes, replacing multicellular, potentially oscillatory buoyant flow with a more organized, single-cell, centrifugally-pumped flow pattern.
- **Interacts constructively or destructively** with natural convection depending on rotation sense: crystal rotation-induced upward flow beneath the crystal can oppose or reinforce the natural upward buoyant plume rising from the hot crucible wall/bottom, depending on geometry and thermal boundary conditions.
- **Governs the transition to time-dependent, three-dimensional, or turbulent flow regimes**: at high $Re_\omega$, rotational shear can itself become unstable, producing spiral vortices, and at high $Gr$ with weak rotation, buoyant plumes can become oscillatory (a major source of growth striations).

### 5.5 Coupling to Heat Transfer at the Interface

Rotation modifies the effective **thermal boundary layer** thickness at the growth interface through enhanced convective heat transport, altering the local Nusselt number:

$$
Nu = f(Re_\omega, Pr)
$$

Empirical/semi-analytical correlations from rotating-disk theory (e.g., Cochran-type solutions) give the local heat-transfer coefficient scaling as:

$$
h \sim \frac{k}{\delta_{th}}, \qquad \delta_{th} \sim \delta_{rot}\, Pr^{-1/3}
$$

where $k$ is the melt thermal conductivity and $\delta_{th}$ the thermal boundary-layer thickness (Cochran/von Kármán-Pohlhausen scaling with Prandtl number exponent commonly $-1/3$). This directly affects the shape and curvature of the solid–liquid interface (facet formation, interface deflection), since local heat extraction rates set the local growth rate via the Stefan condition.

### 5.6 Coupling to Species (Dopant) Transport

Rotation-driven convection controls the **solutal (concentration) boundary layer** thickness at the growth interface, which determines the **effective segregation coefficient** via the Burton–Prim–Slichter (BPS) relation:

$$
k_{eff} = \frac{k_0}{k_0 + (1 - k_0)\exp(-V_{gr}\,\delta_C / D)}
$$

where $k_0$ is the equilibrium segregation coefficient, $D$ the solute diffusivity in the melt, and $\delta_C$ the concentration boundary-layer thickness, which itself scales with rotation rate analogously to the thermal layer:

$$
\delta_C \sim \delta_{rot}\, Sc^{-1/3}, \qquad Sc = \frac{\nu}{D}
$$

($Sc$ = Schmidt number). Because $\delta_{rot} \sim \sqrt{\nu/\omega}$, increasing crystal rotation rate **thins** the solutal boundary layer, drives $k_{eff}$ toward $k_0$, and improves radial dopant homogeneity — a key practical motivation for rotation control in industrial crystal growth (e.g., Czochralski silicon, oxide, and semiconductor growth).

## 6. Coupled Multi-Physics Field Equations

### 6.1 Energy Equation

$$
\rho_0 c_p \left( \frac{\partial T}{\partial t} + \mathbf{u}\cdot \nabla T \right) = k \nabla^2 T
$$

with $c_p$ the specific heat, $k$ the thermal conductivity (and where radiative heat transfer and latent heat release at the interface enter as separate boundary/source terms in the full model, not detailed here).

### 6.2 Species Transport Equation

$$
\frac{\partial C}{\partial t} + \mathbf{u} \cdot \nabla C = D \nabla^2 C
$$

Both energy and species equations are advected by the same velocity field $\mathbf{u}$ computed from the rotation-influenced Navier–Stokes system above, making rotation an indirect but powerful control lever over both heat and mass transfer despite not directly appearing in these transport equations except through $\mathbf{u}$.

## 7. Flow Regimes and Instabilities Associated with Rotation

- **Steady axisymmetric flow**: at low-to-moderate $Re_\omega$ and $Gr$, flow remains laminar, steady, and axisymmetric — the regime assumed by most 2D axisymmetric macroscopic growth simulators.
- **Taylor–Görtler and spiral vortex instabilities**: at sufficiently high $Re_\omega$, the rotating boundary layer over the crystal or crucible can become unstable to spiral vortices, breaking axisymmetry.
- **Baroclinic/buoyant-rotational oscillatory instabilities**: in the mixed-convection regime ($Gr/Re_\omega^2 \sim O(1)$), time-periodic or quasi-periodic flow oscillations arise from the competition between Coriolis and buoyancy forces, a well-documented source of dopant **striations** in as-grown crystals.
- **Three-dimensional turbulence**: at industrially large melt volumes (e.g., large-diameter Czochralski silicon growth), $Re_\omega$ and $Gr$ can both be large enough that the melt flow is genuinely turbulent, requiring turbulence closure models (e.g., RANS with $k$–$\varepsilon$ or Reynolds-stress models, or, less commonly in production codes, large-eddy simulation) superimposed on the rotating-boundary-condition framework described above.

## 8. Summary of Key Non-Dimensional Control Parameters

| Parameter | Definition | Physical meaning |
|---|---|---|
| $Re_\omega = \omega R^2/\nu$ | Rotational Reynolds number | Inertial vs. viscous forces under rotation |
| $Ek = \nu/(\omega L^2)$ | Ekman number | Viscous vs. Coriolis forces |
| $Gr = g\beta_T \Delta T L^3/\nu^2$ | Grashof number | Buoyancy vs. viscous forces |
| $Ra = Gr\cdot Pr$ | Rayleigh number | Buoyancy-driven convection strength |
| $Gr/Re_\omega^2$ | Rotation–buoyancy ratio | Relative dominance of forced vs. natural convection |
| $Pr = \nu/\alpha$ | Prandtl number | Momentum vs. thermal diffusivity |
| $Sc = \nu/D$ | Schmidt number | Momentum vs. solutal diffusivity |
| $Ma$ | Marangoni number | Thermocapillary vs. viscous/thermal diffusive forces |

## 9. Practical Modeling Implementation Notes (Continuum Codes)

In macroscopic melt-growth simulation codes (e.g., CGSim, FEMAG-CZ, CrysMAS, CrysVUn, Cats2D), forced convection from rotation is implemented through:
1. Prescribed rotational boundary conditions ($u_\varphi = \omega r$) at crystal and crucible surfaces, as given in Section 3.
2. Solution of the full (or axisymmetric with retained swirl) Navier–Stokes system, typically via finite-volume or finite-element discretization, often in a coordinate frame co-rotating with one of the boundaries to simplify boundary condition implementation.
3. Coupling to global heat transfer (including furnace-scale radiative exchange and conduction in the crystal, crucible, and surrounding hot-zone components) and, where relevant, to global electromagnetic fields (induction heating currents, applied static or cusp magnetic fields for magnetically-damped convection).
4. Iterative or time-dependent (transient) solution to capture both steady operating states and startup/transient effects such as ACRT rotation schedules.
5. Interface tracking/deformation (moving-boundary, Stefan-type problem) so that the rotational flow field is solved self-consistently with the evolving, generally non-flat, solid–liquid interface shape.

Rotation thus enters the continuum model not as an isolated phenomenon but as a boundary-condition-driven forcing term that propagates, through the coupled momentum–energy–species system, into essentially every macroscopically observable feature of the grown crystal: interface shape, striation pattern, radial and axial dopant distribution, and defect-relevant thermal gradients.


---

> [!NOTE]
> 
> Generated by Claude.ai
>
> Model: Sonet 5
>
> Prompt: Provide an exhaustive description of the Forced Convection from Crystal and Crucible Rotation in the Continuum (Macroscopic) Model of Melt/Solution Growth. Provide description of all physical relevant phenomena. For equation formulation use latex symbols and $$ delimiter. Show the output in Markdown format. Do not copy the output of the exported files into the chat.
