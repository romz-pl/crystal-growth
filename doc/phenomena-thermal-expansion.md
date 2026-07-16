# Thermal Expansion in Crystal Growth from the Melt

## 1. Introduction and Scope

Thermal expansion — the change in dimension of a material with temperature — is not a peripheral material property in melt growth but a central driver of several coupled phenomena that determine crystal quality, yield, and process stability. In melt-growth techniques (Czochralski, Bridgman/VGF, Kyropoulos, Float Zone, EFG, Verneuil, and directional solidification generally), the crystal, the melt, and often the crucible/ampoule and seed all experience large temperature excursions — frequently several hundred to over a thousand kelvin from the melting point down to room temperature. Differential thermal expansion between phases, and gradients of expansion-driven strain within a single phase, feed into:

- Thermoelastic stress generation and dislocation multiplication
- Crystal/crucible interface mechanics (sticking, cracking, detachment)
- Melt buoyancy-driven convection (via the density–temperature relation that underlies thermal expansion)
- Interface shape evolution and its stability
- Residual strain, birefringence, and wafer bow after growth
- Point-defect and dopant/impurity distribution through stress-modified diffusion and segregation

This document surveys the physical mechanisms, the governing equations, key dimensionless groups, material-specific behavior, and modelling approaches, closing with a curated reference list.

---

## 2. Basic Definitions and the Thermal Expansion Tensor

For an isotropic solid, linear thermal expansion is described by the coefficient

$$
\alpha_L(T) = \frac{1}{L}\frac{\partial L}{\partial T}
$$

and volumetric expansion by $\alpha_V \approx 3\alpha_L$ in the isotropic limit. For anisotropic crystals (the majority of technologically important melt-grown crystals: sapphire, SiC, GaN, LiNbO₃, quartz, etc.), thermal expansion is a rank-2 tensor $\alpha_{ij}(T)$, and for crystals of trigonal, tetragonal, or hexagonal symmetry it reduces to two independent principal values, $\alpha_a$ and $\alpha_c$ (expansion perpendicular to and along the crystallographic $c$-axis). This anisotropy is itself a major source of internally generated thermal stress, independent of any externally imposed temperature gradient — a point elaborated in Section 5.

The thermal strain tensor referenced to a stress-free reference temperature $T_0$ is

$$
\varepsilon_{ij}^{\text{th}} = \alpha_{ij}\,(T - T_0)
$$

and total strain decomposes as

$$
\varepsilon_{ij} = \varepsilon_{ij}^{\text{elastic}} + \varepsilon_{ij}^{\text{th}} + \varepsilon_{ij}^{\text{plastic}}
$$

with the plastic term becoming significant once the resolved shear stress on active slip systems exceeds the critical resolved shear stress (CRSS), itself strongly temperature dependent (see Section 6).

---

## 3. Thermal Expansion and Melt Buoyancy: The Boussinesq Coupling

In the melt, thermal expansion enters directly through the buoyancy term of the momentum equation. Under the Boussinesq approximation, density variation is retained only in the buoyancy term:

$$
\rho(T) \approx \rho_0\left[1 - \beta\,(T - T_0)\right]
$$

where $\beta$ is the volumetric thermal expansion coefficient of the melt (often denoted $\beta$ rather than $\alpha_V$ in fluid-dynamics contexts to avoid clashing with the thermal diffusivity symbol $\alpha$). This term drives natural convection, characterized by the Grashof and Rayleigh numbers:

$$
Gr = \frac{g\,\beta\,\Delta T\, L^3}{\nu^2}, \qquad
Ra = Gr \cdot Pr = \frac{g\,\beta\,\Delta T\, L^3}{\nu\,\kappa}
$$

where $g$ is gravitational acceleration, $\Delta T$ a characteristic temperature difference, $L$ a characteristic length (e.g., melt depth or crucible radius), $\nu$ kinematic viscosity, $\kappa$ thermal diffusivity, and $Pr = \nu/\kappa$ the Prandtl number.

Melt thermal expansion therefore does double duty in melt growth:
1. It sets the strength of buoyant convection, which controls heat and dopant transport to the growth interface, hence axial and radial segregation.
2. Combined with forced convection (crucible/crystal rotation) and Marangoni convection (surface-tension-driven flow, governed by $d\gamma/dT$, a related but distinct thermophysical property), it determines whether the melt flow is steady, oscillatory, or turbulent — see the coverage of Kelvin–Helmholtz and other instabilities in the broader library.

For semiconductor melts (Si, Ge, GaAs) $\beta$ is modest ($\sim 10^{-4}\,\text{K}^{-1}$) but $\Delta T$ across the melt and the large $L^3$ scaling in $Gr$ still yield high Grashof numbers, so buoyant convection is essentially always significant in large-diameter Czochralski growth, motivating the use of applied magnetic fields (MCZ) specifically to damp the buoyancy-driven flow — the Hartmann number $Ha$ competes directly against the thermally-driven $Gr$ in these configurations.

---

## 4. Differential Thermal Expansion at Solid–Solid and Solid–Container Interfaces

### 4.1 Crystal–crucible/ampoule interaction (Bridgman, VGF, HEM)

In Bridgman-type and related confined growth, the crystal grows in contact with a crucible (fused silica, graphite, pBN, etc.). Because $\alpha$ of the crystal and $\alpha$ of the crucible material generally differ, cooling from the growth temperature to room temperature produces:

- **Sticking/high contact stress** when the crystal's contraction is smaller than the crucible's (crystal is "squeezed"), which can generate high stresses, slip, and even fracture, particularly near the ampoule tail/tip and any local geometric constriction.
- **Detachment/gap formation** when the crystal contracts more than the crucible, changing the local heat transfer coefficient at the wall (a gap introduces a resistive, often radiation-dominated, heat path) and feeding back into interface shape.
- **Crucible cracking** in the reverse case, especially for brittle crucible materials, since crucibles are typically much less compliant than the crystal at high temperature.

This differential-expansion problem is why "detached" or crucible-less variants (VGF with intentionally engineered gaps, or fully detached Bridgman) were developed, and why crucible material selection (matching $\alpha$ where possible, or deliberately mismatching it to promote clean detachment) is a first-order design decision.

### 4.2 Seed–crystal and grain-boundary considerations

In Czochralski and Kyropoulos growth, the seed crystal, held at a much lower temperature than the melt at the moment of dipping, undergoes rapid differential expansion relative to the growing crystal body, which is one classical source of the "necking" requirement — a thin, dislocation-filtering neck is grown specifically to arrest dislocations nucleated by the thermal shock of seeding before they propagate into the bulk boule.

---

## 5. Thermoelastic Stress from Temperature Gradients and Anisotropic Expansion

### 5.1 Governing equations

Within the growing crystal, treated as a linear thermoelastic solid, the stress field satisfies mechanical equilibrium

$$
\nabla \cdot \boldsymbol{\sigma} + \mathbf{f} = 0
$$

with the constitutive relation (isotropic case, for compactness)

$$
\sigma_{ij} = 2\mu\,\varepsilon_{ij}^{\text{elastic}} + \lambda\,\varepsilon_{kk}^{\text{elastic}}\,\delta_{ij}
$$

where $\varepsilon_{ij}^{\text{elastic}} = \varepsilon_{ij} - \alpha\,(T-T_0)\,\delta_{ij}$, and $\lambda, \mu$ are the Lamé parameters. Even in the complete absence of external mechanical loading, any *non-uniform* temperature field $T(\mathbf{x})$ within the crystal produces non-zero thermoelastic stress unless the resulting thermal strain field happens to be compatible (which, except in trivial geometries such as a 1-D rod with linear $T(x)$, it generally is not).

### 5.2 The classical result: radial temperature profile in a growing cylinder

For an axisymmetric crystal growing with a radially parabolic temperature profile — the canonical simplification used since the earliest analyses of Czochralski thermal stress —

$$
T(r) = T_c + (T_s - T_c)\left(\frac{r}{R}\right)^2
$$

(with $T_c$ the centerline and $T_s$ the surface temperature, $R$ the crystal radius), the resulting thermoelastic stresses in an infinite cylinder (plane-strain, free-surface boundary condition at $r=R$) are classically:

$$
\sigma_{rr}(r) = \frac{E\,\alpha\,(T_s - T_c)}{4(1-\nu)}\left[\left(\frac{r}{R}\right)^2 - 1\right]
$$

$$
\sigma_{\theta\theta}(r) = \frac{E\,\alpha\,(T_s - T_c)}{4(1-\nu)}\left[3\left(\frac{r}{R}\right)^2 - 1\right]
$$

$$
\sigma_{zz}(r) = \frac{E\,\alpha\,(T_s - T_c)}{2(1-\nu)}\left[2\left(\frac{r}{R}\right)^2 - 1\right]
$$

where $E$ is Young's modulus and $\nu$ Poisson's ratio. This result (essentially the Timoshenko thermal-stress solution specialized to a parabolic radial profile, and widely cited via Jordan, Caruso, and von Neida's application to Czochralski Si and GaAs) shows the stress magnitude scales linearly with $\alpha$ and with the radial temperature difference, and quadratically with $r/R$ — hence stress is maximal in tension at the surface for a center-hot profile and grows with crystal diameter for a fixed radial gradient (or, since larger diameter typically requires a *larger* $\Delta T$ to maintain the same axial heat flux, stress grows faster than linearly with diameter in practice). This is the central quantitative link between "thermal expansion coefficient" as a material constant and "dislocation density" as a growth outcome.

### 5.3 From thermal stress to plastic deformation: the Jordan–Alexander–Sandhu / Alexander–Haasen framework

Thermoelastic stress alone would be irrelevant to crystal quality if crystals behaved as perfectly elastic solids down to room temperature. They do not: at growth temperature, semiconductors and many other crystals deform plastically once the resolved shear stress on the softest slip system exceeds the CRSS $\tau_c(T)$, which drops steeply with increasing temperature (often modelled via an Arrhenius-type or power-law dislocation velocity relation, $v_d \propto \tau^m \exp(-E_a/kT)$). The **Jordan–Parsey–Caruso / Alexander–Haasen (JPC/AH) model**, and its many extensions (Miyazaki, Tsivinsky, Völkl), couple:

1. The thermoelastic stress field (driven by $\alpha$ and $\nabla T$),
2. The temperature- and stress-dependent dislocation velocity and multiplication law,
3. A self-consistent reduction of the effective stress as generated dislocations relax it,

to predict the actual dislocation density generated during growth, rather than just the elastic stress that would exist in a perfectly elastic crystal. This is the standard modelling chain used in commercial CZ/FZ simulation packages (see Section 7) to optimize the axial and radial temperature gradient (the "hot zone" design) for low dislocation density, and it is precisely why $\alpha(T)$ — not just $\alpha$ at one reference temperature — must be known accurately over the full growth-to-room-temperature range: the CRSS and $\alpha$ both vary strongly with $T$, and their product integrated along the cooling path sets the final dislocation density and residual stress.

### 5.4 Anisotropic thermal expansion as an *intrinsic* stress source

For non-cubic crystals — sapphire (trigonal), SiC polytypes (hexagonal), GaN (wurtzite), LiNbO₃/LiTaO₃ (trigonal), and many oxide scintillator and laser-host crystals — $\alpha_a \neq \alpha_c$, sometimes substantially (sapphire: $\alpha_a \approx 5.0 \times 10^{-6}\,\text{K}^{-1}$, $\alpha_c \approx 6.7\times 10^{-6}\,\text{K}^{-1}$ near room temperature, with the ratio itself varying with $T$). Even in a spatially *uniform* temperature field, cooling such a crystal from growth temperature generates internal stress wherever grain orientation varies (irrelevant for a single crystal boule with uniform orientation, but critical at any residual sub-grain boundary, twin, or inclusion) and, more importantly, this anisotropy amplifies the stresses from any superimposed *radial* temperature gradient because the effective "elastic thermal expansion mismatch" driving stress depends on crystallographic direction relative to the growth axis. This is a major reason why large-diameter sapphire (Kyropoulos, EFG, HEM) and SiC (PVT, but analogous physics in solution/melt variants) boules are so prone to cracking during cool-down, and why growth-axis selection (c-axis vs. a-axis vs. r-axis growth) is a deliberate lever to manage this anisotropic thermal-expansion stress.

---

## 6. Thermal Expansion Mismatch in Heteroepitaxial and Seeded Growth

Beyond bulk melt growth, thermal expansion mismatch $\Delta\alpha = \alpha_{\text{film}} - \alpha_{\text{substrate}}$ (or, in melt-growth terms, $\alpha_{\text{seed}} - \alpha_{\text{crystal}}$) is a standard driver of curvature and cracking on cooldown, quantified by the Stoney-type relation for thin-film curvature or, for bulk mismatch, by treating the seed/crystal boundary as a bonded bimaterial interface subject to the classical Timoshenko bimetallic-strip analysis. In melt growth this matters most when:

- A seed of different composition or slightly different lattice/thermal-expansion behavior is used (e.g., compositionally graded seeds in mixed-crystal growth, or seed crystals from a different growth run with different point-defect/dopant content that shifts $\alpha$ slightly),
- Encapsulant layers (LEC growth of GaAs/InP under B₂O₃) have very different $\alpha$ from the crystal, so the encapsulant's contraction during and after growth interacts mechanically with the boule surface.

---

## 7. Numerical Treatment in Melt-Growth Simulation Codes

The commercial/academic global-growth simulators covered elsewhere in this reference library (CGSim, CrysMAS, FEMAG/FEMAG-CZ, CrysVUn, Cats2D) all include a thermoelastic stress solver as a standard post-processing (and in some cases in-the-loop) module, because:

- The Boussinesq/buoyancy term ($\beta$, i.e., melt thermal expansion) is one input to the global heat-and-mass-transfer solve that fixes the temperature field everywhere, including at the crystal/melt interface, which then supplies the boundary/initial condition for the solid-crystal thermoelastic stress calculation.
- The stress solve itself uses temperature-dependent $\alpha(T)$, $E(T)$, $\nu(T)$ tables (often the single largest source of material-property uncertainty in these codes, since high-temperature elastic and expansion data are far sparser than room-temperature data), coupled to a CRSS/dislocation-velocity law for the JPC/AH-type plastic relaxation described in Section 5.3.
- Because the thermal field, melt flow (via $\beta$), and stress field are two-way coupled only weakly in most implementations (the crystal shape and interface deflection feed back into the global thermal solve, but the reverse coupling — stress affecting the thermal field — is usually neglected), most codes use a **sequential** rather than fully monolithic solution: global heat/flow/interface solve first, thermoelastic stress solve as a follow-on step using the resulting $T(\mathbf{x})$ field.

---

## 8. Practical Design Implications Summarized

| Phenomenon | Thermal-expansion-related driver | Practical lever |
|---|---|---|
| Melt convection strength/pattern | $\beta$ (melt) via $Gr$, $Ra$ | Magnetic field (MCZ), crucible/crystal rotation, crucible geometry |
| Dislocation density | $\alpha(T)$ crystal + radial $\nabla T$ + CRSS$(T)$ | Hot-zone (afterheater) design, pull rate, ambient gas conductivity |
| Crucible sticking/cracking | $\Delta\alpha$ crystal–crucible | Crucible material choice, engineered gap (VGF), release coatings |
| Boule cracking on cooldown | Anisotropic $\alpha_a$ vs. $\alpha_c$ | Growth-axis orientation, controlled cooldown rate/profile |
| Wafer bow / residual stress | Integrated thermoelastic history | Post-growth anneal, slow controlled cooldown schedule |
| Segregation/striations | Convection strength (via $\beta$) coupling to interface | Rotation rate, magnetic damping, growth rate modulation |

---

## 9. Key References

**Foundational thermoelastic stress theory in melt-grown crystals**
- Jordan, A. S., Caruso, R., & von Neida, A. R. (1980). *A thermoelastic analysis of dislocation generation in pulled GaAs crystals.* Bell System Technical Journal, 59(4), 593–637.
- Jordan, A. S. (1980). *An evaluation of the thermal and elastic constants affecting GaAs crystal growth.* Journal of Crystal Growth, 49(4), 631–642.
- Jordan, A. S., Parsey, J. M., & Caruso, R. (1987). *Dislocation generation in GaAs crystals: theoretical and experimental critique.* Journal of Crystal Growth, 79(1–3), 243–252.

**Dislocation dynamics / Alexander–Haasen framework**
- Alexander, H., & Haasen, P. (1968). *Dislocations and plastic flow in the diamond structure.* Solid State Physics, 22, 27–158.
- Miyazaki, N., Uchida, H., Fujiyama, T., et al. (1993). *Thermal stress analysis of silicon single crystal during Czochralski growth.* Journal of Crystal Growth, 125(3–4), 213–223.

**Melt convection, buoyancy, and dimensionless groups**
- Müller, G., & Ostrogorsky, A. (1994). *Convection in melt growth.* In: Handbook of Crystal Growth, Vol. 2b, D.T.J. Hurle (Ed.), North-Holland.
- Langlois, W. E. (1985). *Buoyancy-driven flows in crystal-growth melts.* Annual Review of Fluid Mechanics, 17, 191–215.

**Anisotropic thermal expansion in non-cubic crystals**
- Wachtman, J. B., Scuderi, T. G., & Cleek, G. W. (1962). *Linear thermal expansion of aluminum oxide and thorium oxide from 100 to 1100 K.* Journal of the American Ceramic Society, 45(7), 319–323. (Classic sapphire $\alpha_a/\alpha_c$ dataset.)
- Slack, G. A., & Bartram, S. F. (1975). *Thermal expansion of some diamondlike crystals.* Journal of Applied Physics, 46(1), 89–98.
- Li, Z., & Bradt, R. C. (1986). *Thermal expansion of the hexagonal (6H) polytype of SiC.* Journal of the American Ceramic Society, 69(12), 863–866.

**Crucible/ampoule interaction, Bridgman/VGF stress**
- Brown, R. A. (1988). *Theory of transport processes in single crystal growth from the melt.* AIChE Journal, 34(6), 881–911.
- Duffar, T. (Ed.) (2010). *Crystal Growth Processes Based on Capillarity: Czochralski, Floating Zone, Shaping and Crucible Techniques.* Wiley. (Extensive treatment of crystal–crucible contact and detachment phenomena.)

**Comprehensive handbook treatment**
- Hurle, D. T. J. (Ed.) (1993–1994). *Handbook of Crystal Growth*, Vols. 2a/2b: Bulk Crystal Growth. North-Holland/Elsevier. (Chapters on thermal stress, convection, and defect generation across all major melt-growth methods.)
- Scheel, H. J., & Capper, P. (Eds.) (2008). *Crystal Growth Technology: From Fundamentals and Simulation to Large-scale Production.* Wiley-VCH.

**Simulation-oriented reviews (linking $\alpha(T)$ data to global growth models)**
- Dupret, F., & Van Den Bogaert, N. (1994). *Modelling Bridgman and Czochralski growth.* In: Handbook of Crystal Growth, Vol. 2b, D.T.J. Hurle (Ed.).
- Derby, J. J., & Brown, R. A. (1986). *Thermal-capillary analysis of Czochralski and liquid encapsulated Czochralski crystal growth.* Journal of Crystal Growth, 74(3), 605–624.

---

*Prepared as part of the crystal-growth technical reference library; cross-references material property tables, continuum model physics, and simulation-software documentation covered elsewhere in that collection.*

---

> [!NOTE]
> 
> Generated by Claude.ai
>
> Model: Sonet 5
>
> Prompt: Provide an extensive overview of the role of thermal expansion in crystal growth from the melt. Provide key references. Show the output in Markdown format.
