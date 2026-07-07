# Dimensionless Groups Governing the Physics of Continuum (Macroscopic) Models of Melt/Solution Crystal Growth

## 1. Introduction and Scope

The macroscopic (continuum) description of melt and solution crystal growth couples momentum, heat, and species transport in the melt/solution with heat conduction in the solid, radiative and convective exchange at furnace boundaries, and the free-boundary problem at the crystal–melt interface. The governing equations — continuity, Navier–Stokes (with buoyancy and, where relevant, electromagnetic forcing), energy, and species conservation — are conventionally nondimensionalized using characteristic scales for length, velocity, temperature, and concentration. The resulting dimensionless groups organize the parameter space of the problem, indicate which physical mechanisms dominate under given process conditions, and allow scaling arguments to be transferred between laboratory experiments, numerical simulations (CGSim, CrysMAS, FEMAG-CZ, CrysVUn, Cats2D), and industrial-scale furnaces.

This document catalogs the dimensionless groups that appear in the continuum modeling of Czochralski (CZ), liquid-encapsulated Czochralski (LEC), Bridgman/vertical gradient freeze (VGF), Kyropoulos (KY), and solution growth systems.

---

## 2. Choice of Characteristic Scales

Nondimensionalization requires a consistent set of reference scales:

- Length scale $L$: crucible radius, melt depth, or crystal radius
- Velocity scale $U$: either a forced scale (crystal/crucible rotation rate $\Omega R$, pull rate $V_p$) or a diffusive/convective scale $\nu/L$ or $\alpha/L$
- Temperature scale $\Delta T$: difference between crucible wall and melting point, or between hot and cold zone
- Concentration scale $\Delta C$: solutally driven systems (solution growth, doped melts)
- Time scale $\tau$: $L/U$ (advective) or $L^2/\alpha$ (diffusive)

The choice of $U$ (forced vs. natural convection scaling) changes the *form* in which buoyancy, rotation, and inertia enter the equations — this is why the literature contains multiple equivalent but differently normalized versions of the same groups (e.g., Grashof vs. Rayleigh, or rotational Reynolds vs. Ekman/Taylor numbers).

---

## 3. Momentum Transport: Viscous, Inertial, Buoyant, and Rotational Groups

### 3.1 Reynolds Number, $Re$

$$
Re = \dfrac{U L}{\nu}
$$

Ratio of inertial to viscous forces in the melt. $\nu$ is the kinematic viscosity. In crystal growth, $U$ is often taken as a rotation-driven scale $\Omega R^2/L$ or a forced-flow scale. Large $Re$ indicates a melt flow prone to instabilities and transition toward turbulence; most oxide and semiconductor melts fall in a moderate-$Re$, buoyancy- and rotation-dominated regime rather than a fully turbulent inertial regime.

### 3.2 Rotational Reynolds Number, $Re_\Omega$

$$
Re_\Omega = \dfrac{\Omega R^2}{\nu}
$$

Governs the crystal or crucible rotation-driven flow (von Kármán-type rotating-disk flow). $\Omega$ is the angular rotation rate and $R$ the characteristic radius (crystal or crucible). Determines whether the rotational boundary layer is laminar, transitional, or turbulent, and controls the thickness of the momentum boundary layer at a rotating disk, $\delta \sim R\, Re_\Omega^{-1/2}$.

### 3.3 Grashof Number, $Gr$

$$
Gr = \dfrac{g \beta_T \Delta T L^3}{\nu^2}
$$

Ratio of thermal buoyancy force to viscous force. $g$ is gravitational acceleration, $\beta_T$ the thermal volumetric expansion coefficient. $Gr$ is the natural companion of $Re$ when buoyancy rather than a forced velocity sets the flow scale; it appears directly (rather than through $Ra = Gr\,Pr$) whenever the momentum equation, not the energy equation, is used to nondimensionalize the buoyancy term.

### 3.4 Solutal Grashof Number, $Gr_C$

$$
Gr_C = \dfrac{g \beta_C \Delta C L^3}{\nu^2}
$$

Analogous to $Gr$ but driven by concentration-dependent density variations ($\beta_C$: solutal expansion coefficient). Essential in solution growth and in melt growth of doped/alloyed crystals (e.g., SiGe, dilute magnetic semiconductors), where solutal buoyancy can dominate, oppose, or reinforce thermal buoyancy, producing double-diffusive convection.

### 3.5 Rayleigh Number, $Ra$

$$
Ra = Gr \cdot Pr = \dfrac{g \beta_T \Delta T L^3}{\nu \alpha}
$$

Ratio of the destabilizing buoyancy driving force to the stabilizing effects of viscous dissipation and thermal diffusion. $\alpha$ is the thermal diffusivity. $Ra$ governs the onset of Rayleigh–Bénard-type natural convection instabilities in the melt and is the primary control parameter for buoyancy-driven flow transitions in large-diameter CZ and Bridgman melts, where the critical Rayleigh number $Ra_c$ marks the onset of oscillatory or plume-driven convection.

### 3.6 Solutal Rayleigh Number, $Ra_C$

$$
Ra_C = \dfrac{g \beta_C \Delta C L^3}{\nu D}
$$

Solutal analogue of $Ra$, with mass diffusivity $D$ replacing $\alpha$. Governs solutally driven convective instability, relevant to constitutional supercooling-adjacent flow instabilities and to double-diffusive convection in doped-melt and solution growth.

### 3.7 Density Ratio (Buoyancy Ratio), $N$

$$
N = \dfrac{Gr_C}{Gr} = \dfrac{\beta_C \Delta C}{\beta_T \Delta T}
$$

Ratio of solutal to thermal buoyancy contributions. Classifies double-diffusive convection regimes: $N>0$ cooperating buoyancy forces, $N<0$ opposing (potentially fingering or layered) convection — of central importance in solution growth and in melt growth with strong dopant segregation.

### 3.8 Taylor Number, $Ta$

$$
Ta = \left(\dfrac{2\Omega L^2}{\nu}\right)^2 \quad \text{or equivalently} \quad Ta = \dfrac{4\Omega^2 L^4}{\nu^2}
$$

Ratio of Coriolis to viscous forces squared; governs the stability of rotating melt flows and the onset of Taylor–Görtler/Ekman-layer instabilities. Frequently invoked together with $Gr$ via the ratio $Gr/Ta$ or $Gr/Re_\Omega^2$ to assess whether rotation or buoyancy controls the flow.

### 3.9 Rotational Grashof Ratio (Rotational-to-Buoyancy Ratio)

$$
\dfrac{Gr}{Re_\Omega^{2}} = \dfrac{g \beta_T \Delta T L}{\Omega^2 R^4/L^2}
$$

A commonly used composite indicating whether crystal/crucible rotation (centrifugal/Coriolis effects) or buoyancy dominates the melt flow pattern — critical in CZ growth for selecting rotation rates that suppress or reinforce natural convection rolls.

### 3.10 Ekman Number, $Ek$

$$
Ek = \dfrac{\nu}{\Omega L^2}
$$

Ratio of viscous to Coriolis forces; the reciprocal-square-root companion of $Ta$. Small $Ek$ indicates rotation-dominated (geostrophic-like) flow with thin Ekman boundary layers at solid rotating boundaries, relevant to crucible-bottom boundary layers in rotated Bridgman/VGF and CZ configurations.

### 3.11 Froude Number, $Fr$

$$
Fr = \dfrac{U^2}{g L}
$$

Ratio of inertial to gravitational forces; less dominant than $Gr/Ra$ in melt growth (where flows are typically low-inertia) but relevant when assessing free-surface deformation at the melt meniscus in CZ pulling, and in meniscus-shape stability analyses.

### 3.12 Marangoni Number, $Ma$

$$
Ma = \dfrac{\left|\partial \sigma/\partial T\right| \Delta T\, L}{\mu \alpha}
$$

Ratio of thermocapillary (surface-tension-gradient-driven) forces to viscous and thermal diffusive dissipation. $\sigma$ is surface tension, $\mu$ dynamic viscosity. Governs Marangoni (thermocapillary) convection at the free melt surface, which is particularly significant in small-Prandtl-number semiconductor melts (Si, Ge) and in float-zone-adjacent CZ configurations where buoyancy-driven flow is comparatively weak. A solutal Marangoni number, $Ma_C = |\partial\sigma/\partial C|\,\Delta C\, L /(\mu D)$, plays an analogous role in solution growth with surface-active solutes.

### 3.13 Bond Number, $Bo$

$$
Bo = \dfrac{g \beta_T \Delta \rho \, L^2}{\sigma} \quad \text{(or, in capillary-shape form,} \; Bo = \dfrac{\Delta \rho\, g\, L^2}{\sigma} \text{)}
$$

Ratio of gravitational (hydrostatic) forces to surface-tension (capillary) forces, governing the equilibrium shape of the free melt surface and meniscus in CZ and Kyropoulos growth, where $\Delta\rho$ is a characteristic density difference across the meniscus.

### 3.14 Capillary Number, $Ca$

$$
Ca = \dfrac{\mu U}{\sigma}
$$

Ratio of viscous to surface-tension forces at the free surface; relevant, together with $Bo$, to meniscus dynamics and the stability of the growth-angle condition at the triple-phase (solid–liquid–vapor/ambient) line in CZ pulling.

---

## 4. Heat Transport Groups

### 4.1 Prandtl Number, $Pr$

$$
Pr = \dfrac{\nu}{\alpha}
$$

Ratio of momentum to thermal diffusivity — a material property (function of the melt/solution only), not of the flow geometry. Oxide melts (e.g., $\mathrm{Al_2O_3}$, $\mathrm{LiNbO_3}$, garnets) typically have $Pr \sim 1$–$10$, while semiconductor melts (Si, Ge, GaAs) have $Pr \sim 10^{-2}$, meaning thermal diffusion is much faster than momentum diffusion — a key reason why semiconductor melt flows are comparatively more susceptible to inertial/convective instabilities at lower $Ra$.

### 4.2 Péclet Number, $Pe$

$$
Pe = \dfrac{U L}{\alpha} = Re \cdot Pr
$$

Ratio of advective to diffusive heat transport. Large $Pe$ indicates that convective heat transport dominates over conduction in the melt, requiring the energy equation's advective term to be resolved carefully in the numerical scheme; small $Pe$ (as in slow, viscous Bridgman growth) permits conduction-dominated approximations.

### 4.3 Nusselt Number, $Nu$

$$
Nu = \dfrac{h L}{k}
$$

Ratio of total (convective + conductive) heat transfer to pure conductive heat transfer across a boundary layer of thickness $\sim L$; $h$ is the convective heat transfer coefficient and $k$ the thermal conductivity of the melt. Used to characterize heat transfer at crucible walls, the melt free surface, and the growth interface, and to correlate simulation output against simplified boundary-layer models.

### 4.4 Biot Number, $Bi$

$$
Bi = \dfrac{h L}{k_s}
$$

Ratio of internal conductive resistance (in the solid crystal or crucible wall, conductivity $k_s$) to external convective/radiative resistance at its boundary. Governs whether temperature gradients within the growing crystal (needed for thermal-stress and dislocation-density estimates) can be resolved with a lumped-capacitance approximation ($Bi \ll 1$) or require the full conduction problem ($Bi \gtrsim 1$) — highly relevant to CZ and KY crystal cooling and to VGF ampoule-wall conduction.

### 4.5 Stefan Number, $Ste$

$$
Ste = \dfrac{c_p \Delta T}{L_f}
$$

Ratio of sensible heat to latent heat of fusion $L_f$ ($c_p$: specific heat capacity). Governs the strength of coupling between the moving-interface (Stefan) latent-heat release/absorption and the sensible heat transport in the melt and solid; central to the interface-tracking energy balance in all melt-growth methods (CZ, Bridgman, LEC, KY) and to interface-shape stability analysis.

### 4.6 Radiation–Conduction Parameter (Stark Number / Boltzmann Number), $Bo_{rad}$ (also denoted $N_{rc}$ or $Sk$)

$$
Sk = \dfrac{k}{4\,\sigma_{SB}\, \varepsilon\, L\, T_{ref}^3}
$$

Ratio of conductive to radiative heat transport, where $\sigma_{SB}$ is the Stefan–Boltzmann constant, $\varepsilon$ the surface emissivity, and $T_{ref}$ a reference (e.g., melting-point) temperature. Because radiative heat exchange with the furnace hot zone and crucible dominates the thermal boundary conditions in most oxide and semiconductor CZ/LEC/KY furnaces (which operate at high $T_{ref}$), $Sk$ (or its inverse, sometimes called the radiation number) is essential in coupling the melt/crystal continuum model to the view-factor-based global furnace thermal model.

### 4.7 Radiation Number (alternative form), $Rd$

$$
Rd = \dfrac{4 \sigma_{SB} \varepsilon T_{ref}^3 L}{k}
$$

The reciprocal of $Sk$; used interchangeably in the literature depending on whether radiation or conduction is treated as the reference transport mechanism. Large $Rd$ (small $Sk$) signals a radiation-dominated thermal environment, typical of high-temperature oxide crystal growth (e.g., sapphire, YAG) where radiative losses from the crystal shoulder and melt surface control the axial temperature gradient at the interface — a key determinant of thermal stress and dislocation generation.

---

## 5. Mass Transport (Solute/Species) Groups

### 5.1 Schmidt Number, $Sc$

$$
Sc = \dfrac{\nu}{D}
$$

Ratio of momentum to mass diffusivity — the solutal analogue of $Pr$. In melt growth of doped crystals, $Sc$ is typically large ($Sc \sim 10$–$100$), meaning the solutal boundary layer at the growth interface is much thinner than the momentum boundary layer, which underlies the classical Burton–Prim–Slichter (BPS) segregation analysis.

### 5.2 Lewis Number, $Le$

$$
Le = \dfrac{\alpha}{D} = \dfrac{Sc}{Pr}
$$

Ratio of thermal to mass diffusivity. Governs the relative thickness of thermal versus solutal boundary layers at the growth front and controls the character of double-diffusive convection (thermosolutal instabilities, layering) in doped-melt and solution growth systems.

### 5.3 Solutal Péclet Number, $Pe_C$ (Mass-Transfer Péclet Number)

$$
Pe_C = \dfrac{U L}{D} = Re \cdot Sc
$$

Ratio of advective to diffusive solute transport. In interface-attached form, using the growth (pull) velocity $V_g$ and boundary-layer thickness $\delta_C$,

$$
Pe_C^{\ast} = \dfrac{V_g\, \delta_C}{D}
$$

directly parametrizes the Burton–Prim–Slichter effective segregation coefficient,

$$
k_{eff} = \dfrac{k_0}{k_0 + (1-k_0)\, e^{-Pe_C^{\ast}}}
$$

relating growth-front solute transport to the equilibrium segregation coefficient $k_0$; this is one of the most practically important dimensionless-group results in the macroscopic modeling of doped and alloy melt growth (CZ Si, SiGe, oxide crystals with dopants) as well as in solution-growth segregation.

### 5.4 Damköhler Number, $Da$ (where interfacial/bulk reaction kinetics matter)

$$
Da = \dfrac{k_r L}{D}
$$

Ratio of a characteristic reaction (attachment-kinetics) rate $k_r$ to diffusive mass transport rate. Relevant in solution growth (and vapor-transport-adjacent methods) where interface attachment kinetics, rather than pure diffusion, can be rate-limiting; less commonly dominant in melt growth of elemental/simple compound semiconductors but essential in complex-oxide solution growth (flux growth, hydrothermal analogues) modeled at the continuum level.

---

## 6. Interface Morphological Stability Groups

### 6.1 Morphological Stability (Constitutional Supercooling) Parameter

$$
\mathcal{M} = \dfrac{m_L\, G_C}{G_T}
$$

where $m_L$ is the liquidus slope, $G_C$ the solute concentration gradient ahead of the interface, and $G_T$ the thermal gradient. Values $\mathcal{M} > 1$ (or, in the classical criterion, $G_T < m_L G_C$) signal constitutional supercooling and morphological (cellular/dendritic) instability of the growth front — a central design constraint in both melt and solution growth used to set pull rate and thermal gradient.

### 6.2 Mullins–Sekerka Stability Parameter

$$
\Omega_{MS} = \dfrac{V_g\, d_0}{D}
$$

Combines the growth velocity $V_g$, the capillary length $d_0 = \gamma T_m c_p /L_f^2$ (with $\gamma$ the solid–liquid interfacial energy and $T_m$ the melting point), and the solute diffusivity $D$; governs the wavelength and growth rate of morphological perturbations at the crystal–melt interface in the linear stability framework that extends the constitutional-supercooling criterion.

### 6.3 Capillary (Gibbs–Thomson) Number

$$
\Gamma^{\ast} = \dfrac{\gamma T_m}{L_f\, L}
$$

Ratio of the Gibbs–Thomson capillary undercooling scale to the characteristic thermal driving force over the system length scale $L$; controls the strength of curvature-dependent melting-point depression at the interface and its coupling to interface-shape evolution in phase-field-adjacent and sharp-interface continuum models alike.

---

## 7. Electromagnetic Groups (for EMCZ / Magnetically Damped or Stirred Growth)

### 7.1 Hartmann Number, $Ha$

$$
Ha = B_0 L \sqrt{\dfrac{\sigma_{el}}{\mu}}
$$

Ratio of electromagnetic (Lorentz) damping force to viscous force, where $B_0$ is the applied magnetic flux density and $\sigma_{el}$ the electrical conductivity of the melt. Large $Ha$ indicates strong magnetic damping of convective flow — the basis for magnetic-field-assisted CZ (MCZ) growth used to suppress turbulent/oscillatory melt convection in silicon and other conducting melts.

### 7.2 Magnetic Reynolds Number, $Re_m$

$$
Re_m = \mu_0 \sigma_{el} U L
$$

Ratio of advective to diffusive transport of magnetic field lines ($\mu_0$: magnetic permeability of free space). In virtually all crystal-growth applications $Re_m \ll 1$ (the low-magnetic-Reynolds-number/quasi-static approximation), justifying the simplified electromagnetic model in which the induced field is neglected relative to the applied field — a standard simplifying assumption in FEMAG-CZ-type coupled electromagnetic–thermal–flow solvers.

### 7.3 Stuart Number (Magnetic Interaction Parameter), $N_{EM}$

$$
N_{EM} = \dfrac{Ha^2}{Re} = \dfrac{\sigma_{el} B_0^2 L}{\rho U}
$$

Ratio of electromagnetic (Lorentz) force to inertial force; used alongside $Ha$ to characterize the relative importance of magnetic damping versus convective inertia, particularly in cusp-field and traveling-magnetic-field CZ configurations.

---

## 8. Stress and Defect-Related Groups

### 8.1 Thermal Stress Parameter (Biot-modulated thermoelastic number)

$$
\Sigma_{th} = \dfrac{E \beta_{s} \Delta T}{\sigma_y}
$$

Ratio of thermally induced elastic stress ($E$: Young's modulus, $\beta_s$: solid thermal expansion coefficient) to the critical resolved shear stress $\sigma_y$ for dislocation generation; used in coupling the continuum thermal-field solution to von Mises stress and dislocation-density (Alexander–Haasen-type) post-processing in CZ and KY crystal-quality prediction.

### 8.2 Péclet Number for Interface Motion (Growth Péclet Number), $Pe_g$

$$
Pe_g = \dfrac{V_g L}{\alpha}
$$

Ratio of advective heat transport associated with interface motion itself to conductive transport; governs whether the quasi-steady (frozen-temperature-field) approximation is valid for the moving-boundary problem, relevant to both the melt-side and solid-side energy balance across the Stefan condition in CZ, Bridgman, and VGF.

---

## 9. Composite and Regime-Classification Numbers

### 9.1 Rotational Rayleigh Number Ratio

$$
\dfrac{Ra}{Ta^{1/2}}
$$

Used to classify convective regimes in rotating CZ/KY melts as buoyancy-dominated, rotation-dominated, or mixed, guiding the choice of crystal/crucible rotation rates to control interface shape and dopant striations.

### 9.2 Elasser Number / Interaction Parameter combinations

Combinations such as $Ha^2/Ta$ or $N_{EM}/Ro$ (with $Ro = \Omega L/U$ the Rossby number) are used in EMCZ and traveling-magnetic-field designs to jointly classify the relative strength of rotation, buoyancy, and electromagnetic damping — since no single group captures the three-way competition relevant to large-diameter, magnetically controlled industrial CZ pullers.

---

## 10. Summary Table

| Symbol | Name | Physical Ratio | Governs |
|---|---|---|---|
| $Re$ | Reynolds | Inertial / viscous | Flow regime, transition to turbulence |
| $Re_\Omega$ | Rotational Reynolds | Rotational inertial / viscous | Rotating boundary-layer regime |
| $Gr$ | Grashof | Thermal buoyancy / viscous | Natural convection strength |
| $Gr_C$ | Solutal Grashof | Solutal buoyancy / viscous | Solutal convection strength |
| $Ra$ | Rayleigh | Buoyancy / (viscous $\times$ thermal diffusion) | Onset of thermal convective instability |
| $Ra_C$ | Solutal Rayleigh | Buoyancy / (viscous $\times$ mass diffusion) | Onset of solutal convective instability |
| $N$ | Buoyancy (density) ratio | Solutal / thermal buoyancy | Double-diffusive convection regime |
| $Ta$ | Taylor | Coriolis$^2$ / viscous$^2$ | Rotational flow stability |
| $Ek$ | Ekman | Viscous / Coriolis | Rotational boundary-layer thickness |
| $Fr$ | Froude | Inertial / gravitational | Free-surface deformation |
| $Ma$ | Marangoni | Thermocapillary / (viscous $\times$ thermal diffusion) | Surface-tension-driven convection |
| $Bo$ | Bond | Gravitational / capillary | Meniscus shape |
| $Ca$ | Capillary | Viscous / surface tension | Meniscus/contact-line dynamics |
| $Pr$ | Prandtl | Momentum / thermal diffusivity | Material transport character |
| $Pe$ | Péclet (thermal) | Advective / conductive heat transport | Convective vs. conductive heat regime |
| $Nu$ | Nusselt | Total / conductive heat transfer | Boundary-layer heat transfer |
| $Bi$ | Biot | Internal / external thermal resistance | Lumped vs. distributed thermal model |
| $Ste$ | Stefan | Sensible / latent heat | Interface latent-heat coupling |
| $Sk$ / $Rd$ | Stark / Radiation number | Conductive / radiative transport | Furnace radiative thermal coupling |
| $Sc$ | Schmidt | Momentum / mass diffusivity | Solutal boundary-layer thickness |
| $Le$ | Lewis | Thermal / mass diffusivity | Double-diffusive layering |
| $Pe_C$ | Péclet (solutal) | Advective / diffusive solute transport | Segregation ($k_{eff}$, BPS relation) |
| $Da$ | Damköhler | Reaction rate / diffusive transport | Interface-kinetics-limited growth |
| $\mathcal{M}$ | Morphological stability | Solutal / thermal gradient (scaled) | Constitutional supercooling |
| $Ha$ | Hartmann | Magnetic damping / viscous | Magnetic flow damping (MCZ) |
| $Re_m$ | Magnetic Reynolds | Advective / diffusive field transport | Validity of quasi-static EM approximation |
| $N_{EM}$ | Stuart / interaction parameter | Lorentz / inertial force | Magnetic vs. convective dominance |

---

## 11. Concluding Remarks

No single dimensionless group governs melt/solution growth; rather, the continuum model is characterized by a *hierarchy* of competing ratios spanning momentum ($Re$, $Gr$, $Ra$, $Ta$, $Ha$), heat ($Pr$, $Pe$, $Nu$, $Bi$, $Ste$, $Sk$), mass ($Sc$, $Le$, $Pe_C$, $Da$), and interface-morphology/capillarity ($\mathcal{M}$, $\Gamma^\ast$, $Bo$, $Ca$) physics. Practical furnace and process design in CZ, LEC, Bridgman/VGF, and Kyropoulos growth — and the calibration of macroscopic simulation codes such as CGSim, CrysMAS, FEMAG-CZ, CrysVUn, and Cats2D — proceeds by identifying which subset of these groups is order-one or dominant for a given melt (via $Pr$, $Sc$), geometry ($L$, aspect ratio), and operating condition (rotation rates, pull rate, applied magnetic field, furnace thermal boundary conditions), thereby reducing the full multi-physics continuum problem to a tractable, regime-specific balance of forces.

---

> [!NOTE]
> 
> Generated by Claude.ai
>
> Model: Sonet 5
>
> Prompt: Provide an exhaustive description of the Dimensionless Groups Governing the Physics in the Continuum (Macroscopic) Model of Melt/Solution Growth. Provide the extensive description of Dimensionless Group. For equation formulation use latex symbols and $$ delimiter. In equations use command \ast instead of the literal *. Show the output in Markdown format. Do not copy the output of the exported files into the chat.
