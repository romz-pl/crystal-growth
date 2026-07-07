# Non-Axisymmetric Flow Structures in Axisymmetric Geometries

## 1. Introduction and Scope

An axisymmetric geometry is a domain $\Omega$ invariant under rotation about a symmetry axis (typically taken as the $z$-axis), so that in cylindrical coordinates $(r, \theta, z)$ the domain boundaries depend only on $r$ and $z$. Examples central to melt-growth and rotating-flow applications include Czochralski (CZ) crucibles, cylindrical Taylor–Couette gaps, spherical/annular gaps, rotating-disk configurations, and Bridgman ampoules.

Despite geometric symmetry under $\theta \to \theta + \delta\theta$ for arbitrary $\delta\theta$, the **flow field itself need not respect this symmetry**. This document exhaustively catalogs the mechanisms, mathematical structure, classification, and physical manifestations of non-axisymmetric ($m \neq 0$) flow states that arise in such geometries, i.e., states in which fields depend explicitly on $\theta$.

---

## 2. Mathematical Framework

### 2.1 Symmetry Group and Symmetry Breaking

The governing equations (Navier–Stokes, heat, and possibly induction equations) posed on an axisymmetric domain are equivariant under the continuous symmetry group $SO(2)$ (rotations about $z$) and, when the domain is also top–bottom symmetric, under $O(2) = SO(2) \times \mathbb{Z}_2$. A base state $\mathbf{u}_0(r,z)$ that is itself $\theta$-independent is called the **axisymmetric base flow**. Non-axisymmetric structures arise when this base state loses stability to perturbations of nonzero azimuthal wavenumber $m$:

$$
\mathbf{u}(r,\theta,z,t) = \mathbf{u}_0(r,z) + \epsilon\, \hat{\mathbf{u}}(r,z)\, e^{i m \theta + \sigma t} + \text{c.c.} + O(\epsilon^2)
$$

Here $m \in \mathbb{Z}$, $m \neq 0$, is the azimuthal wavenumber, and $\sigma = \sigma_r + i\omega$ is the complex growth rate. Since $\theta$ is a periodic coordinate, normal modes are automatically of Fourier form $e^{im\theta}$, and linear stability of the axisymmetric state decomposes into independent problems for each $m$.

### 2.2 Governing Equations in Cylindrical Coordinates

For an incompressible Newtonian fluid with velocity $\mathbf{u} = (u_r, u_\theta, u_z)$:

$$
\frac{\partial u_r}{\partial t} + (\mathbf{u}\cdot\nabla) u_r - \frac{u_\theta^2}{r} = -\frac{1}{\rho}\frac{\partial p}{\partial r} + \nu\left(\nabla^2 u_r - \frac{u_r}{r^2} - \frac{2}{r^2}\frac{\partial u_\theta}{\partial \theta}\right)
$$

$$
\frac{\partial u_\theta}{\partial t} + (\mathbf{u}\cdot\nabla) u_\theta + \frac{u_r u_\theta}{r} = -\frac{1}{\rho r}\frac{\partial p}{\partial \theta} + \nu\left(\nabla^2 u_\theta - \frac{u_\theta}{r^2} + \frac{2}{r^2}\frac{\partial u_r}{\partial \theta}\right)
$$

$$
\frac{\partial u_z}{\partial t} + (\mathbf{u}\cdot\nabla) u_z = -\frac{1}{\rho}\frac{\partial p}{\partial z} + \nu \nabla^2 u_z
$$

$$
\frac{1}{r}\frac{\partial (r u_r)}{\partial r} + \frac{1}{r}\frac{\partial u_\theta}{\partial \theta} + \frac{\partial u_z}{\partial z} = 0
$$

with the scalar Laplacian

$$
\nabla^2 f = \frac{1}{r}\frac{\partial}{\partial r}\left(r \frac{\partial f}{\partial r}\right) + \frac{1}{r^2}\frac{\partial^2 f}{\partial \theta^2} + \frac{\partial^2 f}{\partial z^2}
$$

The convective operator is $(\mathbf{u}\cdot\nabla) = u_r \partial_r + \frac{u_\theta}{r}\partial_\theta + u_z \partial_z$.

### 2.3 Azimuthal Fourier Decomposition (Linear Stability)

Linearizing about the axisymmetric base flow $\mathbf{U}_0 = (U_r, U_\theta, U_z)(r,z)$ and $P_0(r,z)$, perturbations are expanded as

$$
\begin{pmatrix} u_r' \\ u_\theta' \\ u_z' \\ p' \end{pmatrix}(r,\theta,z,t) = \begin{pmatrix} \hat{u}_r \\ \hat{u}_\theta \\ \hat{u}_z \\ \hat{p} \end{pmatrix}(r,z)\, \exp(i m \theta + \sigma t) + \text{c.c.}
$$

Substitution converts $\partial_\theta \to im$, decoupling each azimuthal mode $m$ into a 2-D (in $r,z$) linear eigenvalue problem of the form

$$
\sigma \, \mathbf{B}\, \hat{\mathbf{q}} = \mathbf{L}_m(\mathbf{U}_0)\, \hat{\mathbf{q}}, \qquad \hat{\mathbf{q}} = (\hat{u}_r, \hat{u}_\theta, \hat{u}_z, \hat{p})^T
$$

where $\mathbf{L}_m$ contains $m$-dependent terms (curvature terms $\propto 1/r^2$, $\propto m/r^2$, and $\propto m^2/r^2$) coupling $\hat{u}_r$ and $\hat{u}_\theta$ through the Coriolis-like terms even when $U_\theta \equiv 0$. The task of stability analysis is to find, for each $m$, the critical parameter (e.g., Reynolds number $Re_c(m)$ or Grashof number $Gr_c(m)$) at which $\sigma_r$ first crosses zero, and the associated critical wavenumber $m_c = \arg\min_m Re_c(m)$.

### 2.4 Symmetry Classification of Bifurcating Solutions

Because the problem is $SO(2)$-equivariant, equivariant bifurcation theory (Golubitsky–Stewart–Schaeffer) applies directly:

- A **steady bifurcation** to a mode with wavenumber $m$ generically produces a **rotating wave** (traveling azimuthal pattern) of the form $f(r,z,\theta - \Omega_p t)$, where $\Omega_p = -\omega/m$ is the pattern (drift) rotation rate, generally incommensurate with the base rotation rate.
- If the system additionally possesses the reflection symmetry $\mathbb{Z}_2$ (e.g., $z \to -z$ in a symmetric enclosure), the full symmetry is $O(2)$, and bifurcations can produce either **standing waves** (fixed azimuthal nodes, oscillating amplitude) or **rotating waves**, with mixed-mode (**modulated rotating wave**) solutions also generically possible near mode interactions.
- **Mode interactions**: When two critical modes $m_1 \neq m_2$ (or an $m\neq0$ mode and the axisymmetric $m=0$ mode) become simultaneously marginal, the resulting codimension-2 bifurcation supports quasiperiodic and mixed-mode states, including **wavy vortices**, **modulated waves**, and, in some parameter windows, spatiotemporal chaos.

---

## 3. Physical Mechanisms Generating Non-Axisymmetric Structures

### 3.1 Centrifugal Instability with Azimuthal Modulation (Taylor–Couette-type)

In rotating annular/cylindrical gaps, the primary instability of circular Couette flow is the axisymmetric Taylor vortex ($m=0$). A **secondary instability** of the Taylor vortex state breaks axisymmetry via a wavy-vortex mode:

$$
u_r'(r,\theta,z,t) \sim A(t)\, f(r,z)\, \cos(m\theta - \omega t)
$$

producing the classical **wavy Taylor vortices**, characterized by an azimuthal wavenumber $m$ (typically 2–6 depending on radius ratio and rotation rates) and a well-defined drift frequency $\omega/m$, the *wave speed*.

### 3.2 Baroclinic and Shear-Layer Instabilities in Rotating Disk / von Kármán Flows

Flow driven by a rotating disk in an otherwise axisymmetric enclosure develops a boundary-layer profile susceptible to **crossflow (Type I) instability** and **streamline-curvature (Type II) instability**, both of which select a finite azimuthal mode number $m$, manifesting as **spiral vortices** rotating at a fraction of the disk angular velocity:

$$
m \approx \frac{2\pi r}{\lambda_\theta}, \qquad c_{\text{phase}} = \frac{\omega}{m} \Omega_{\text{disk}}
$$

where $\lambda_\theta$ is the azimuthal wavelength of the spiral pattern. This is directly relevant to CZ crystal/crucible rotation configurations.

### 3.3 Thermal (Buoyancy-Driven) Non-Axisymmetric Convection

In a differentially heated axisymmetric cavity (e.g., CZ melt, Bridgman ampoule) with a purely radial or vertical temperature gradient, the axisymmetric buoyant flow can become unstable to azimuthal modes once the Grashof/Rayleigh number exceeds a critical value $Gr_c(m_c)$. Two principal sub-mechanisms are recognized:

1. **Baroclinic instability of the thermal wind**: an azimuthal shear layer analogous to atmospheric baroclinic instability, generating traveling thermal waves circulating around the axis.
2. **Rayleigh–Bénard-type instability with azimuthal periodicity**: in cavities heated from below/side with sufficient radial extent, convection rolls organize into an azimuthally periodic pattern of $m$ counter-rotating cells (often visualized as "petal" or polygonal patterns).

The resulting temperature field has the generic decomposition

$$
T(r,\theta,z,t) = T_0(r,z) + \sum_{m=1}^{\infty} \left[ A_m(t)\cos(m\theta) + B_m(t)\sin(m\theta) \right] \Theta_m(r,z)
$$

with the dominant mode $m^\ast$ (often $m^\ast = 1$ or $2$ in CZ melts) dominating the energy and producing the well-documented **thermal plume rotation / oscillation** observed in crystal growth melts.

### 3.4 Melt-Flow Instabilities Specific to Czochralski Configuration

In CZ growth, three coupled forcing agents (buoyancy $Gr$, crystal rotation $Re_{\text{cr}}$, crucible rotation $Re_{\text{cru}}$, and Marangoni stress $Ma$) interact; the combined non-axisymmetric instability is often classified by:

$$
\text{Ra} = \frac{g\beta \Delta T H^3}{\nu \alpha}, \qquad Ma = \frac{|\partial\gamma/\partial T|\, \Delta T\, L}{\mu \alpha}
$$

- **Buoyant-thermocapillary instability**: coupled Marangoni (surface-tension-driven) and buoyant convection destabilizes to azimuthal wavenumbers $m = 1$–$3$, producing rotating or oscillating hot/cold spots at the melt free surface — directly responsible for striations in the grown crystal.
- **Rotationally induced non-axisymmetric mode locking**: when crystal and crucible rotation rates are incommensurate, the non-axisymmetric mode can phase-lock to the *difference* frequency $|\Omega_{\text{cr}} - \Omega_{\text{cru}}|$, producing beat patterns in measured temperature/velocity signals at the melt surface.

### 3.5 Precessing Vortex Core / Swirl-Flow Instabilities

Confined swirling jets and vortex breakdown bubbles in axisymmetric ducts/chambers exhibit a helical, precessing instability known as the **Precessing Vortex Core (PVC)**, dominant at $m=1$:

$$
\hat{\mathbf{u}}(r,z)\, e^{i(\theta - \omega t)}
$$

The PVC arises from a global hydrodynamic instability of the swirling base flow (often associated with the presence of a stagnation point / vortex breakdown bubble on the axis) and manifests as a helically deformed, precessing recirculation zone, well documented in swirl combustors and vortex tube flows — geometrically axisymmetric but flow-wise strongly $m=1$ dominated.

### 3.6 Ekman-Layer and Boundary-Driven Non-Axisymmetric Modes

In rotating axisymmetric containers (e.g., spin-up/spin-down problems), the Ekman boundary layer on the end walls can itself become unstable to azimuthal disturbances once the local Reynolds number $Re_E = U\delta_E/\nu$ (with Ekman-layer thickness $\delta_E = \sqrt{\nu/\Omega}$) exceeds a threshold, producing **Ekman spirals with periodic azimuthal roll structures**, class A (Type I, inflectional) and class B (Type II, inertial/Coriolis-driven) instabilities distinguished by

$$
m_c \approx 4\text{–}30, \qquad \text{depending on } Re_E \text{ and the radius-to-height aspect ratio}.
$$

### 3.7 Elliptical / Tilt (Kelvin-Mode) Instabilities

Even in a perfectly axisymmetric container, if the **base flow itself possesses an elliptical streamline distortion** induced by a weak forcing (e.g., tidal/orbital forcing, or geometric imperfection), a parametric resonance between two inertial (Kelvin) waves of wavenumbers $m$ and $m\pm2$ can occur — the **elliptical instability**, requiring

$$
\omega_1(m) + \omega_2(m\pm 2) = 0
$$

for resonance, and producing exponentially growing $m=1$ or $m=2$ vortical structures superimposed on the mean swirl.

---

## 4. Classification of Non-Axisymmetric Structures by Azimuthal Wavenumber

| $m$ | Common name | Typical physical origin | Symmetry of resulting pattern |
|---|---|---|---|
| $1$ | Tilt mode / precessing core / single-plume oscillation | PVC, elliptical instability, buoyant plume drift | Single azimuthal maximum, whole-pattern precession |
| $2$ | Elliptical mode / two-cell pattern | Elliptical instability, baroclinic wave, thermocapillary wave | Two-fold pattern, may be standing or traveling |
| $3$–$6$ | Wavy vortex modes, polygonal convection cells | Centrifugal (Taylor–Couette) secondary instability, RBC-type azimuthal cells | $m$-fold rotational symmetry, often traveling at fixed phase speed |
| $\gtrsim 10$ | Short-wavelength boundary layer spirals | Crossflow (Type I) rotating-disk instability, Ekman-layer instability | Fine spiral pattern confined to boundary layer |

---

## 5. Nonlinear Saturation and Temporal Behavior

### 5.1 Amplitude Equations (Landau/Ginzburg–Landau Description)

Near the onset of an $m\neq0$ bifurcation from an $SO(2)$-symmetric base state, the weakly nonlinear evolution of the complex mode amplitude $A(t)$ (with the pattern $\propto \text{Re}[A(t) e^{im\theta}]$) is governed by the normal form (complex Landau equation)

$$
\frac{dA}{dt} = \sigma A - l\, |A|^2 A + O(|A|^4)
$$

where $\sigma = \sigma_r + i\omega$ is the complex linear growth rate and $l = l_r + i l_i$ is the (complex) Landau coefficient. The real part $l_r > 0$ corresponds to a *supercritical* (forward) bifurcation saturating to a finite-amplitude rotating wave with $|A|_{\text{sat}} = \sqrt{\sigma_r/l_r}$; $l_r < 0$ signals a *subcritical* bifurcation requiring higher-order (quintic) terms.

### 5.2 Mode Interactions and Spatiotemporal Complexity

When multiple azimuthal modes are simultaneously near-critical (e.g., $m$ and $m+1$, or $m=0$ and $m\neq0$), coupled amplitude equations of the form

$$
\frac{dA_1}{dt} = \sigma_1 A_1 - (l_{11}|A_1|^2 + l_{12}|A_2|^2) A_1
$$
$$
\frac{dA_2}{dt} = \sigma_2 A_2 - (l_{21}|A_1|^2 + l_{22}|A_2|^2) A_2
$$

govern competition or coexistence between the modes. Depending on the sign/magnitude of the cross-coupling coefficients $l_{12}, l_{21}$, the system exhibits:

- **Winner-take-all mode selection** (pure rotating wave of one $m$),
- **Mixed-mode / quasiperiodic states** (both amplitudes finite, producing beating patterns with frequency $|\omega_1 - \omega_2|$ or a rationally/irrationally related pair),
- **Heteroclinic cycling** between states dominated alternately by $m_1$ and $m_2$, producing intermittent, seemingly irregular switching — a well-known route from an axisymmetric flow through non-axisymmetric patterns to spatiotemporal chaos.

### 5.3 Drift and Phase Dynamics

Because $\theta$ is a continuous (Goldstone) symmetry direction, the phase of a rotating-wave solution is neutrally stable (marginal), and the pattern as a whole can be advected/drifted by any residual symmetry-breaking imperfection (geometric asymmetry, off-center heating, non-uniform rotation). This produces the commonly observed **slow drift or intermittent pinning** of otherwise steadily rotating patterns in experiments, distinguishable from genuine intrinsic frequency dynamics.

---

## 6. Diagnostic and Analysis Techniques

### 6.1 Azimuthal Fourier Decomposition of Simulation/Experimental Data

Given a field $f(r,\theta,z,t)$ sampled on a cylindrical grid, the non-axisymmetric content is extracted via

$$
\hat{f}_m(r,z,t) = \frac{1}{2\pi}\int_0^{2\pi} f(r,\theta,z,t)\, e^{-im\theta}\, d\theta
$$

with the axisymmetric (mean) component being $\hat{f}_0(r,z,t)$ and the non-axisymmetric energy content quantified via

$$
E_{m}(t) = \int_\Omega |\hat{f}_m(r,z,t)|^2\, r\, dr\, dz, \qquad m \geq 1
$$

### 6.2 Symmetry-Reduction / Template Fitting

Because rotating-wave solutions are steady in a co-rotating frame, they can be identified numerically via the reduced (template-fitted) frame

$$
\tilde{\theta} = \theta - \Omega_p t, \qquad \partial_t \big|_{\tilde\theta} = 0 \text{ for a pure rotating wave}
$$

allowing continuation methods (e.g., Newton–Krylov on the rotating-wave equations, with $\Omega_p$ solved as an unknown eigenvalue) to directly compute non-axisymmetric branches without time integration.

### 6.3 Cross-Correlation / Autocorrelation Spectra

The drift frequency $\omega/m$ and pattern coherence are typically extracted from time series at fixed $(r,z)$ but varying $\theta$ via cross-correlation:

$$
C(\Delta\theta, \tau) = \left\langle f(r,\theta,z,t)\, f(r,\theta+\Delta\theta,z,t+\tau) \right\rangle_t
$$

whose peak locus in the $(\Delta\theta,\tau)$ plane gives the phase speed $\Delta\theta/\tau = \omega/m$.

---

## 7. Representative Governing Nondimensional Parameters

| Parameter | Definition | Role in azimuthal symmetry breaking |
|---|---|---|
| Reynolds number | $Re = \Omega R^2/\nu$ | Controls centrifugal / shear instabilities (Taylor–Couette, rotating disk) |
| Taylor number | $Ta = \dfrac{4\Omega^2 R^4}{\nu^2}\left(\dfrac{d}{R}\right)$ | Governs onset of Taylor vortices and their wavy secondary instability |
| Grashof / Rayleigh number | $Gr = \dfrac{g\beta \Delta T H^3}{\nu^2}$, $Ra = Gr\cdot Pr$ | Controls buoyant azimuthal convective modes |
| Marangoni number | $Ma = \dfrac{|\gamma_T| \Delta T L}{\mu \alpha}$ | Controls thermocapillary azimuthal oscillation in free-surface melts |
| Rossby number | $Ro = U/(2\Omega L)$ | Governs inertial-wave and elliptical-instability azimuthal coupling |
| Ekman number | $Ek = \nu/(\Omega H^2)$ | Governs Ekman-layer instability azimuthal wavenumber selection |

---

## 8. Summary of Structural Taxonomy

Non-axisymmetric flow structures in axisymmetric geometries arise generically whenever a control parameter drives the axisymmetric base state past a linear-stability threshold associated with a nonzero azimuthal wavenumber $m$. The equivariant structure of the governing equations under $SO(2)$ (or $O(2)$) guarantees that:

1. Each unstable mode is characterized by an integer $m$ and complex growth rate $\sigma_m = \sigma_r(m) + i\omega(m)$;
2. Generic bifurcations produce **rotating waves** $\propto e^{i(m\theta - \omega t)}$, with **standing waves** possible only under additional reflection symmetry;
3. The saturated pattern's *shape* is fixed by the base-state physics (centrifugal, buoyant, capillary, Ekman, or elliptical mechanisms as enumerated in Section 3), while its *rotation/drift rate* $\Omega_p = \omega/m$ is generically incommensurate with any externally imposed rotation rate, reflecting the underlying continuous rotational symmetry of the domain;
4. Higher-order mode competition and interaction generically lead to quasiperiodic, mixed-mode, or spatiotemporally chaotic states as the governing parameter is increased further past the primary $m\neq0$ bifurcation.

This taxonomy underlies observed phenomena across Taylor–Couette flow, rotating-disk boundary layers, Czochralski/Bridgman melt convection, swirling combustor flows, and geophysical/astrophysical rotating flows, all sharing the common feature of an axisymmetric container hosting a flow that spontaneously and robustly breaks that symmetry.

---

> [!NOTE]
> 
> Generated by Claude.ai
>
> Model: Sonet 5
>
> Prompt: Provide an exhaustive description of the non-axisymmetric flow structures  in  axisymmetric geometries. For equation formulation use latex symbols and $$ delimiter. In equations use command \ast instead of the literal *. Show the output in Markdown format. Do not copy the output of the exported files into the chat.
