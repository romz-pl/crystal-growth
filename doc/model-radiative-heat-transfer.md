# Radiative Heat Transfer

## 1. Scope and Role Within the Global Heat-Transfer Model

In continuum ("global") models of melt and solution growth (Czochralski, CZ; Liquid-Encapsulated Czochralski, LEC; Kyropoulos; Bridgman/Vertical Gradient Freeze, VGF; and related configurations), the furnace is treated as an axisymmetric (or fully 3D) assembly of opaque and semi-transparent continuous media — melt, crystal, crucible, susceptor, heaters, insulation, gas ambient, and radiation shields. The governing macroscopic energy equation in each solid/liquid domain is

$$
\rho c_p \left( \frac{\partial T}{\partial t} + \mathbf{u}\cdot\nabla T \right) = \nabla\cdot\left(k\nabla T\right) + Q_{\text{Joule}} - \nabla\cdot \mathbf{q}_r
$$

where $\rho$ is density, $c_p$ specific heat, $k$ thermal conductivity, $\mathbf{u}$ the melt velocity field, $Q_{\text{Joule}}$ the induction/resistive heating source, and $\mathbf{q}_r$ the **radiative heat flux vector**, whose divergence, $\nabla\cdot\mathbf{q}_r$, acts as a volumetric radiative source/sink term. Radiation enters the model in two fundamentally different ways depending on whether the medium is treated as opaque or semi-transparent:

1. **Surface (boundary) radiation** — exchange of radiative energy between the bounding surfaces of opaque bodies (crucible, susceptor, heater, shields, opaque melt surface).
2. **Volumetric (participating-medium) radiation** — absorption, emission, and scattering occurring *within* semi-transparent solids (most oxide and some semiconductor crystals) as the radiation field propagates through the bulk.

Because typical growth furnaces operate at temperatures of 1000–2500 K, radiative fluxes scale as $T^4$ and are frequently the dominant, or at least comparable, mode of heat transport relative to conduction and convection — thermal modeling of Czochralski processes is understood as a challenging coupling of conduction, convection, radiation, fluid flow and other transport phenomena, and accurate treatment of radiative exchange is essential to predicting the crystal-melt interface shape and pulling parameters correctly.

---

## 2. Physical Fundamentals of Thermal Radiation

### 2.1 Blackbody Emission and the Stefan–Boltzmann Law

Every surface element at temperature $T$ emits electromagnetic radiation. For an ideal blackbody, the spectral (monochromatic) hemispherical emissive power is given by Planck's law:

$$
e_{b\lambda}(T) = \frac{2\pi h c_0^2}{\lambda^5}\frac{1}{\exp\!\left(\dfrac{h c_0}{\lambda k_B T}\right)-1}
$$

with $h$ Planck's constant, $c_0$ the speed of light in vacuum, $k_B$ Boltzmann's constant, and $\lambda$ wavelength. Integrating over all wavelengths yields the total blackbody emissive power:

$$
e_b(T) = \int_0^\infty e_{b\lambda}(T)\,d\lambda = \sigma T^4
$$

where $\sigma = 5.670 \times 10^{-8}\ \mathrm{W\,m^{-2}K^{-4}}$ is the Stefan–Boltzmann constant. This $T^4$ dependence is the reason radiation dominates over conduction/convection at crystal-growth temperatures and why radiative boundary conditions are strongly nonlinear.

### 2.2 Real Surfaces: Emissivity, Absorptivity, Reflectivity

Real surfaces are not black. The **spectral, directional emissivity** $\varepsilon_\lambda(\hat{\Omega}, T)$ relates actual emitted intensity to the blackbody intensity:

$$
\varepsilon_{\lambda}(\hat{\Omega},T) = \frac{I_\lambda(\hat{\Omega},T)}{I_{b\lambda}(T)}
$$

By Kirchhoff's law of thermal radiation, at thermal equilibrium the spectral directional emissivity equals the spectral directional absorptivity:

$$
\varepsilon_\lambda(\hat{\Omega},T) = \alpha_\lambda(\hat{\Omega},T)
$$

Reflectivity follows from energy conservation on an opaque surface ($\tau = 0$):

$$
\alpha_\lambda + \rho_\lambda = 1 \qquad \Rightarrow \qquad \rho_\lambda = 1 - \varepsilon_\lambda
$$

For a semi-transparent surface, the general spectral balance is

$$
\alpha_\lambda + \rho_\lambda + \tau_\lambda = 1
$$

where $\tau_\lambda$ is the transmissivity.

**Simplifying assumptions commonly invoked in continuum growth models:**

- **Gray surface**: radiative properties independent of wavelength, $\varepsilon_\lambda = \varepsilon$.
- **Diffuse surface**: radiative properties independent of direction (Lambertian emission/reflection).
- **Diffuse-gray model**: the combination of both, is the workhorse assumption for global CZ/Kyropoulos/LEC simulations, since exact spectral-directional data for furnace materials (graphite, quartz, metals) are rarely available with sufficient accuracy.
- **Specular reflection**: mirror-like reflection at a well-defined angle equal to the incidence angle; important for polished crystal side-surfaces and crucible walls, and shown to substantially affect the interface shape (e.g., strong convexity in BGO/sillenite growth) compared to diffuse-only treatments.

### 2.3 Semi-Transparent Media: Spectral Absorption Bands

Many oxide crystals (sapphire, YAG, BGO, LiNbO₃, garnets) and some melts are partially transparent to thermal radiation in certain wavelength bands and effectively opaque in others (due to phonon and electronic absorption edges). This is modeled with a **multi-band (banded-gray) approximation**: the spectrum is divided into $N$ bands $[\lambda_{j}, \lambda_{j+1}]$, each assigned a constant absorption coefficient $\kappa_j$ and refractive index $n_j$, since spectral transmittance of a real crystal (e.g. YAG) can vary by orders of magnitude between bands. A three-band model has been used, for instance, to approximate the spectral absorptivity of BGO crystals with an opaque UV/far-IR region and a transparent visible/near-IR window.

---

## 3. The Radiative Transfer Equation (RTE)

### 3.1 General Form

The propagation of radiative intensity $I_\lambda(\mathbf{r},\hat{\Omega})$ along a direction $\hat{\Omega}$ through an absorbing, emitting, and scattering medium is governed by the **Radiative Transfer Equation**:

$$
\frac{dI_\lambda(\mathbf{r},\hat{\Omega})}{ds} = -\kappa_\lambda I_\lambda(\mathbf{r},\hat{\Omega}) - \sigma_{s,\lambda} I_\lambda(\mathbf{r},\hat{\Omega}) + \kappa_\lambda I_{b\lambda}(T) + \frac{\sigma_{s,\lambda}}{4\pi}\int_{4\pi} I_\lambda(\mathbf{r},\hat{\Omega}')\,\Phi(\hat{\Omega}',\hat{\Omega})\,d\Omega'
$$

where $s$ is the path length along $\hat{\Omega}$, $\kappa_\lambda$ the spectral absorption coefficient, $\sigma_{s,\lambda}$ the scattering coefficient, and $\Phi(\hat{\Omega}',\hat{\Omega})$ the scattering phase function. The four terms on the right represent, respectively: **attenuation by absorption**, **attenuation by out-scattering**, **augmentation by local emission**, and **augmentation by in-scattering** from all other directions.

The **extinction coefficient** is $\beta_\lambda = \kappa_\lambda + \sigma_{s,\lambda}$, and the **single-scattering albedo** is $\omega_\lambda = \sigma_{s,\lambda}/\beta_\lambda$. In most melt-growth crystals, scattering is weak relative to absorption (clear single crystals), so the RTE reduces to a purely absorbing–emitting form:

$$
\frac{dI_\lambda}{ds} = \kappa_\lambda\left(I_{b\lambda}(T) - I_\lambda\right)
$$

### 3.2 Optical Thickness and Limiting Regimes

The **optical thickness** of a medium of characteristic dimension $L$ is

$$
\tau_\lambda = \int_0^L \kappa_\lambda\, ds
$$

- **Optically thin limit** ($\tau_\lambda \ll 1$): radiation traverses the medium with negligible self-absorption; volumetric emission/absorption is a small perturbation and surface-to-surface (transparent-medium) treatments are adequate.
- **Optically thick (diffusion) limit** ($\tau_\lambda \gg 1$): radiation is absorbed and re-emitted many times over path $L$, and transport can be approximated locally by a diffusion-like process (Rosseland approximation, §4.3).
- **Intermediate (moderate) optical thickness**: neither limit applies; the full RTE (or a discrete/finite-volume/exchange-factor solution) must be used. This is the practically relevant regime for many oxide crystals — e.g., simulations of Czochralski oxide growth with crystal optical thickness $\kappa_s \sim 0.01$–$0.1$ have shown that internal radiative transfer measurably alters the curvature of the melt/crystal interface, becoming more convex toward the melt as optical thickness decreases, though the sensitivity weakens once $\kappa_s < 0.1$.

### 3.3 Refraction at Semi-Transparent Interfaces (Fresnel Effects)

At an interface between two media of different refractive index $n_1, n_2$ (e.g., crystal/gas or crystal/melt), an incident ray partially reflects and partially refracts according to **Snell's law**:

$$
n_1 \sin\theta_1 = n_2 \sin\theta_2
$$

with reflectivity given by the **Fresnel equations** (averaged over polarization for unpolarized radiation):

$$
\rho(\theta_1) = \frac{1}{2}\left[ \left(\frac{n_1\cos\theta_1 - n_2\cos\theta_2}{n_1\cos\theta_1 + n_2\cos\theta_2}\right)^2 + \left(\frac{n_1\cos\theta_2 - n_2\cos\theta_1}{n_1\cos\theta_2 + n_2\cos\theta_1}\right)^2 \right]
$$

Beyond the critical angle $\theta_c = \arcsin(n_2/n_1)$ (going from higher to lower index), **total internal reflection** occurs, trapping radiation inside the crystal and creating internal "light-pipe" effects that couple distant regions of the crystal radiatively — a phenomenon of particular importance in transparent crystal side-surfaces, where Fresnel-specular reflection models have been shown to produce qualitatively different interface shapes than purely diffuse-reflection models.

---

## 4. Solution Methods for the RTE in Continuum Growth Models

### 4.1 Surface-to-Surface (Diffuse-Gray Enclosure) Radiation — Opaque Boundaries

When the enclosure gas is transparent and all bounding surfaces are opaque, diffuse, and gray, radiative exchange reduces to a **view-factor (configuration-factor) formulation**. The view factor $F_{i \to j}$ between two surface elements $A_i, A_j$ is

$$
F_{i\to j} = \frac{1}{A_i}\int_{A_i}\int_{A_j} \frac{\cos\theta_i \cos\theta_j}{\pi r^2}\, V_{ij}\, dA_j\, dA_i
$$

where $r$ is the distance between area elements, $\theta_i, \theta_j$ the angles between the line connecting them and each surface normal, and $V_{ij} \in \{0,1\}$ a visibility (shadowing) function accounting for obstruction by intervening geometry — an essential feature for the geometrically complex, irregularly shaped, shadowed axisymmetric enclosures typical of CZ furnaces (heater, shields, crucible lip, crystal shoulder, meniscus). View factors satisfy the **reciprocity relation**

$$
A_i F_{i\to j} = A_j F_{j\to i}
$$

and the **summation (closure) relation** for an enclosure of $N$ surfaces,

$$
\sum_{j=1}^{N} F_{i\to j} = 1
$$

Because numerically computed view factors often violate these constraints, rectification (e.g., least-squares) algorithms are applied to restore reciprocity and closure before use in the enclosure calculation.

The **radiosity method** defines, for each gray-diffuse surface $i$ at temperature $T_i$ with emissivity $\varepsilon_i$, the radiosity $J_i$ (total outgoing flux = emitted + reflected):

$$
J_i = \varepsilon_i \sigma T_i^4 + (1-\varepsilon_i)\sum_{j=1}^N F_{i\to j} J_j
$$

and the net radiative heat flux leaving surface $i$:

$$
q_{r,i} = \frac{\varepsilon_i}{1-\varepsilon_i}\left(\sigma T_i^4 - J_i\right) = \sigma T_i^4 - \sum_{j=1}^N F_{i\to j}J_j
$$

This linear (in $J$) system is solved simultaneously with the conduction/convection energy equation at each surface node, coupling temperature and radiosity fields globally around the enclosure. When surfaces additionally exhibit **specular reflection**, the exchange-factor formulation is extended: the reflectance is split into diffuse and specular fractions, and radiative paths are traced (or partition-ratio coefficients computed) to account for mirror images of the enclosure, a method developed for enclosures combining specular and diffuse walls (e.g., concentric spheres/cylinders, cube faces) and specifically relevant to polished quartz/graphite surfaces in the growth furnace.

### 4.2 Discrete Exchange Factor (DEF) / Zonal Methods

For furnaces with participating (semi-transparent) volumes as well as opaque surfaces, the enclosure is discretized into surface and volume zones, and a **unified exchange factor** $\bar{F}_{i\to j}$ is defined between every pair of zones (surface-surface, surface-volume, volume-volume), incorporating multiple internal reflection and scattering within the semi-transparent crystal. This Discrete Exchange Factor method handles irregularly shaped axisymmetric geometries and shadowing while linking a spectral, volume, and surface thermal-radiation algorithm to the finite-volume conduction/convection solver, and has been used, for example, to simulate YAG Czochralski growth including multiple reflection/scattering of radiation within the crystal medium.

### 4.3 Rosseland (Diffusion) Approximation — Optically Thick Media

For optically thick semi-transparent media, the radiative flux can be approximated as a diffusive process analogous to Fourier conduction. The **Rosseland approximation** gives

$$
\mathbf{q}_r = -\frac{16\sigma n^2 T^3}{3\kappa_R}\nabla T = -k_r \nabla T, \qquad k_r \equiv \frac{16\sigma n^2 T^3}{3\kappa_R}
$$

where $n$ is the refractive index and $\kappa_R$ the **Rosseland mean absorption coefficient**:

$$
\frac{1}{\kappa_R} = \frac{\displaystyle\int_0^\infty \frac{1}{\kappa_\lambda}\frac{\partial e_{b\lambda}}{\partial T}\,d\lambda}{\displaystyle\int_0^\infty \frac{\partial e_{b\lambda}}{\partial T}\,d\lambda}
$$

This lets radiative transport be folded into an effective conductivity $k_{\text{eff}} = k + k_r$ inside the energy equation, which is computationally the cheapest radiation model (no transport equation solved) but is valid **only** when the medium is optically thick everywhere, a condition frequently violated near boundaries and in thin crystals, limiting its applicability in melt growth where crystals commonly present a small-to-moderate optical thickness.

### 4.4 Finite-Volume Method (FVM) for the RTE

For crystals of relatively thin optical thickness (where diffusion/Rosseland fails) the RTE is solved directly by discretizing the angular ($\hat{\Omega}$) and spatial domains, dividing the total solid angle $4\pi$ into discrete control angles and integrating the RTE over each spatial control volume and control angle. This finite-volume radiative solver has been coupled to global CZ heat-transfer models to resolve the radiative exchange in crystals with optical thickness as low as $\kappa_s \sim 0.01$, showing that interface convexity increases as the crystal becomes more transparent.

### 4.5 Ray-Tracing / Ray-Emission Methods

A more general approach traces individual rays (Monte-Carlo or deterministic) emitted from surface and volume elements through the 3D enclosure, accounting for absorption, scattering, refraction, and diffuse/specular reflection at each interaction — the **generalized view factor / ray-tracing method**, which is free of the discretization ("ray effect") artifacts inherent to methods based on a finite set of directions, at the cost of high computational and memory demand. A refined **Ray Emission Model** was subsequently developed to correct the failure of the original ray-tracing emission treatment for media with large absorption coefficients, and extended to multi-band spectral computations, broadening applicability to strongly absorbing semi-transparent crystals.

### 4.6 Discrete Ordinates Method (DOM)

The discrete ordinates method replaces the continuous angular integral in the RTE with a quadrature sum over a finite set of ordinate directions $\hat{\Omega}_m$ with weights $w_m$, converting the integro-differential RTE into a set of coupled partial differential equations solved along each ordinate — used, e.g., in semi-transparent spherical-annulus enclosures with specularly reflecting walls, where the diffuse (medium-emission) part of the intensity is solved by DOM while the directly transmitted/specularly reflected part is treated analytically.

---

## 5. Coupling of Radiation to the Global Continuum Energy Balance

### 5.1 Volumetric Radiative Source Term

Inside a semi-transparent solid, the divergence of the radiative flux enters the energy equation as a local source/sink:

$$
\nabla\cdot\mathbf{q}_r = \int_0^\infty \kappa_\lambda\left(4\pi I_{b\lambda}(T) - \int_{4\pi} I_\lambda\, d\Omega\right) d\lambda = \kappa_p\left(4\sigma T^4 - \int_0^\infty \kappa_\lambda G_\lambda\, d\lambda \Big/ \kappa_p \right)
$$

commonly written in terms of the incident radiation $G_\lambda(\mathbf{r}) = \int_{4\pi} I_\lambda\, d\Omega$:

$$
\nabla\cdot\mathbf{q}_r = \int_0^\infty \kappa_\lambda\left(4\pi I_{b\lambda}(T) - G_\lambda\right)d\lambda
$$

This term is added directly to the right-hand side of the continuum energy equation given in §1, coupling the temperature field to the radiative intensity field self-consistently: the local temperature determines the local blackbody emission $I_{b\lambda}(T)$, which sources the RTE, whose solution ($G_\lambda$) feeds back into $\nabla\cdot\mathbf{q}_r$ and hence the temperature.

### 5.2 Boundary Conditions at Opaque and Semi-Transparent Interfaces

At an **opaque** boundary (crucible wall, heater, susceptor, shield) the net radiative flux computed by the enclosure/exchange-factor method (§4.1–4.2) enters as a Robin-type boundary condition on the conduction equation:

$$
-k\left.\frac{\partial T}{\partial n}\right|_{\text{surface}} = q_{r,\text{net}} + q_{\text{conv}}
$$

where $q_{\text{conv}} = h(T_s - T_\infty)$ represents convective loss to the ambient gas (often modeled with an empirical or CFD-derived heat-transfer coefficient $h$ on surfaces exposed to gas cooling flow.

At a **semi-transparent** boundary (crystal free surface, crystal/gas or crystal/melt interface for a transparent crystal), the boundary condition for the RTE itself must specify the incoming intensity from outside (emitted by the furnace enclosure, transmitted through the interface per Fresnel's law) plus the reflected component of the internal intensity, coupling the internal volumetric radiation field to the external surface-to-surface enclosure calculation — this coupling is precisely what is required, for instance, in modeling the internally radiating crystal bounded by a diffuse/specular reflecting side wall and immersed in a furnace whose other walls (crucible, susceptor) are opaque diffuse-gray radiators.

### 5.3 Coupling at the Crystallization Front (Melt/Crystal Interface)

The moving solid–liquid interface is subject to a **Stefan condition** incorporating the latent heat of fusion $L$ and both conductive and radiative flux jumps:

$$
k_s \left.\frac{\partial T}{\partial n}\right|_{s} - k_l \left.\frac{\partial T}{\partial n}\right|_{l} + \left[ q_{r,s} - q_{r,l}\right]\cdot\hat{n} = \rho_s L\, v_n
$$

where subscripts $s,l$ denote solid and liquid sides, $v_n$ is the normal interface velocity (pulling/growth rate), and the interface temperature is fixed at (or near) the melting point $T_m$, generally corrected for interface curvature via the Gibbs–Thomson effect. Since the melt is normally treated as **opaque** (radiation is absorbed within a very thin layer at its free surface) while the crystal may be **semi-transparent**, radiation reaching the interface from within the crystal (internal emission/transmission) directly affects the local heat balance and hence the predicted curvature of the interface — internal radiation and conduction are what governs transport in the crystalline phase, while melt transport is dominated by convection and conduction because the melt is opaque.

### 5.4 Radiative Heating Sources

External heating (resistive or RF/induction heaters) is coupled into the same enclosure radiation network as an additional emitting surface or volumetric Joule-heating source $Q_{\text{Joule}}$ solved from a coupled electromagnetic (time-harmonic Maxwell/eddy-current) model; the induced heat and the surface-to-surface radiative exchange are solved together with conduction and phase change in a fully coupled steady-state or transient system.

---

## 6. Key Physical Phenomena Captured by the Model

1. **Blackbody-like emission scaling as $T^4$**, making radiative exchange the dominant heat-loss mechanism at typical growth temperatures and strongly nonlinear in temperature.
2. **Diffuse and specular reflection** at crucible, shield, and crystal surfaces, with specular reflection at crystal side/shoulder surfaces shown to induce pronounced interface convexity and cool "dark core" regions near the crystal axis, arising from the interplay of moderate conductivity and appreciable absorption in materials such as sillenite (BSO/BGO).
3. **Shadowing and view obstruction** in geometrically complex, irregularly shaped enclosures (heater coils, shoulders, shields), requiring visibility functions in the view-factor integral.
4. **Volumetric absorption, emission, and (weak) scattering** inside semi-transparent crystals, governed by the full RTE, with strong dependence on the crystal's spectral absorption bands (multi-band/banded-gray treatment).
5. **Optical-thickness-dependent behavior of the interface shape** — thinner (more transparent) crystals allow deeper radiative penetration and a systematically different (more convex) crystallization front than optically thick crystals, though this sensitivity saturates once optical thickness exceeds roughly 0.1.
6. **Fresnel reflection/refraction and total internal reflection** at semi-transparent interfaces (crystal/gas, crystal/melt), trapping and redistributing radiative energy within the crystal ("light-piping").
7. **Coupling between global furnace radiation and internal crystal radiation**, requiring exchange-factor or ray-tracing methods that simultaneously resolve surface-to-surface, surface-to-volume, and volume-to-volume radiative interactions.
8. **Radiative-conductive-convective-latent heat coupling at the moving crystallization front**, where the balance of these fluxes sets the local growth rate and interface curvature via the generalized Stefan condition.
9. **Material- and growth-technique-specific effects**: comparisons across CZ, Kyropoulos, and Heat Exchanger Method (HEM) growth (e.g., of sapphire, Ti:sapphire) show that internal radiation's effect on heat transfer and interface shape differs meaningfully between these related melt-growth configurations, driven by differences in furnace radiative environment and crystal geometry/aspect ratio.
10. **Sensitivity of global energy balance to radiative material properties** — surface emissivities of the crystal and its facing surfaces (e.g., crucible/susceptor material) and the internal absorption/emission behavior of the melt and solid phases are among the most influential parameters controlling predicted crystal diameter and required heater power in validated global thermal models.

---

## 7. Summary of Modeling Hierarchy

| Regime / Component | Governing Description | Typical Method |
|---|---|---|
| Opaque furnace surfaces (crucible, susceptor, heater, shields) | Diffuse-gray or diffuse+specular surface-to-surface exchange | View factors, radiosity method, exchange factors |
| Optically thin/moderate semi-transparent crystal | Full spectral RTE (absorption + weak scattering) | Finite-volume RTE, discrete ordinates, ray tracing / DEF |
| Optically thick semi-transparent medium | Diffusion (Rosseland) approximation | Effective radiative conductivity $k_r$ |
| Crystal/gas, crystal/melt semi-transparent interfaces | Fresnel reflection/refraction, total internal reflection | Interface boundary conditions on RTE |
| Melt (opaque) | Surface emission/absorption only; internal transport by convection/conduction | Boundary condition on opaque free surface |
| Crystallization front | Coupled conductive + radiative flux balance with latent heat | Generalized Stefan condition |
| External heating | Electromagnetic induction / resistive heating coupled to radiative enclosure | Time-harmonic EM + radiation + conduction coupling |

This layered treatment — spanning Planck/Kirchhoff surface radiation physics, the full radiative transfer equation for participating semi-transparent crystals, and their numerical solution via view-factor, exchange-factor, diffusion, finite-volume, and ray-tracing methods — constitutes the complete radiative heat transfer component of the continuum (macroscopic) model of melt/solution crystal growth.

---

> [!NOTE]
> 
> Generated by Claude.ai
>
> Model: Sonet 5
>
> Prompt: Provide an exhaustive description of the Radiative Heat Transfer in the Continuum (Macroscopic) Model of Melt/Solution Growth. Provide description of all physical relevant phenomena. For equation formulation use latex symbols and $$ delimiter. Show the output in Markdown format. Do not copy the output of the exported files into the chat.
