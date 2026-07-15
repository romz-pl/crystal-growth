# Growth of Indium Phosphide (InP) Single Crystals

## 1. Material Background and Motivation

Indium phosphide (InP) is a III–V compound semiconductor with zinc-blende structure, lattice constant $a_0 = 5.8687\ \text{\AA}$ at 300 K, and a direct bandgap of $E_g \approx 1.35\ \text{eV}$. It is the substrate of choice for:

- 1.3–1.55 μm optoelectronic devices (laser diodes, photodetectors) for fiber-optic telecommunications, since InP-lattice-matched InGaAsP/InGaAs alloys cover this window
- High-electron-mobility transistors (HEMTs) and heterojunction bipolar transistors (HBTs) for high-frequency/mm-wave electronics
- Substrates for InGaAs-based infrared photodiodes and solar cell epitaxy

Because InP dissociates well below its melting point and phosphorus has very high equilibrium vapor pressure over the melt, InP is one of the most difficult III–V compounds to grow as bulk single crystal — considerably harder than GaAs.

## 2. Key Physical Properties Relevant to Growth

| Property | Value | Growth relevance |
|---|---|---|
| Melting point $T_m$ | $1062\ ^\circ\text{C}$ (1335 K) | Sets furnace/susceptor thermal design |
| Equilibrium P vapor pressure at $T_m$ | $\sim 27.5\ \text{atm}$ | Drives need for pressurized/encapsulated growth |
| Thermal conductivity (solid, near $T_m$) | Low, $\sim 0.68\ \text{W/(cm K)}$ at 300 K, decreasing with T | Limits achievable axial temperature gradients without excessive thermal stress |
| Critical resolved shear stress | Lower than GaAs/Si | High dislocation density (EPD) if thermal stress too high |
| Density (solid) | $4.81\ \text{g/cm}^3$ | Buoyancy-driven convection in melt |
| Density (liquid) | $\sim 5.6$–$5.7\ \text{g/cm}^3$ | Melt convection strength |

The dominant growth challenge is **phosphorus loss by dissociative sublimation**:
$$
\text{InP(s or l)} \longrightarrow \text{In(l)} + \tfrac{1}{4}\text{P}_4(\text{g}) \quad \text{or} \quad \text{In(l)} + \tfrac{1}{2}\text{P}_2(\text{g})
$$

Without suppression, the melt surface progressively depletes of phosphorus, driving off-stoichiometry, In droplet inclusions, and twinning.

## 3. Growth Methods

Three main bulk techniques are used industrially and in research, each addressing the P-overpressure problem differently.

### 3.1 Liquid-Encapsulated Czochralski (LEC)

The dominant historical method for InP boule production, directly adapted from GaAs LEC growth.

**Principle**: The InP melt surface is covered by a layer of molten boric oxide ($\text{B}_2\text{O}_3$), which is chemically inert, transparent (allows visual meniscus monitoring), and — critically — impermeable to phosphorus vapor when a sufficiently high inert-gas overpressure (typically high-purity $\text{N}_2$ or Ar, 40–100 atm) is applied above the encapsulant. This traps P vapor beneath the $\text{B}_2\text{O}_3$ layer and suppresses dissociation.

**Process outline**:
1. Polycrystalline InP charge (often pre-synthesized from high-purity In and P) loaded into a pBN (pyrolytic boron nitride) or quartz crucible with a $\text{B}_2\text{O}_3$ disk on top.
2. Chamber sealed and pressurized with inert gas to 40–100 atm to counter the P vapor pressure and prevent boil-off of the encapsulant itself.
3. Charge heated (RF or resistive) past $T_m$; $\text{B}_2\text{O}_3$ melts first (softening point $\sim 450\ ^\circ\text{C}$) and floats atop the InP melt as it forms.
4. A $\langle 100 \rangle$ or $\langle 111 \rangle$ seed crystal is dipped through the encapsulant layer into the melt.
5. Necking (Dash technique) is performed to eliminate seed dislocations, followed by shouldering and constant-diameter body growth by controlled pulling ($\sim$ 5–15 mm/h) and counter-rotation of seed/crucible.
6. Diameter is controlled by adjusting heater power in response to meniscus geometry (optically monitored through the transparent encapsulant) or by weighing.

**Key difficulties specific to InP-LEC**:
- **Very high dislocation density** (typical EPD $10^4$–$10^5\ \text{cm}^{-2}$) because of the large radial and axial thermal gradients needed for a stable growth interface combined with InP's low critical resolved shear stress and low thermal conductivity — thermal stresses exceed the yield stress readily.
- **Twinning**, especially at large diameters (>2 inch), due to constitutional supercooling and interface breakdown at high growth rates or poor stoichiometry control.
- To reduce dislocations, InP-LEC often uses annealing after growth, or dopant hardening — see §5.

### 3.2 Vapor Pressure Controlled Czochralski (VCZ) / High-Pressure LEC variants

A refinement of LEC where the *entire growth chamber* (not just a local gas blanket) is held at a phosphorus-vapor overpressure close to the equilibrium value, sometimes without any $\text{B}_2\text{O}_3$ encapsulant, or with a thinner encapsulant layer. A separate phosphorus source is heated to generate the controlling vapor pressure, and the main growth chamber temperature/pressure is servo-controlled to track it. This reduces the need for very high inert gas pressure and can improve stoichiometry control, but adds substantial engineering complexity (hot-wall high-pressure vessel).

### 3.3 Vertical Gradient Freeze (VGF) and Vertical Bridgman (VB)

Now the industrially preferred method for high-quality, low-dislocation-density InP substrates (analogous to the shift seen in GaAs).

**Principle**: Instead of pulling a crystal from a free melt surface, the melt is contained in a shaped (often conical-bottom) crucible, and a pre-existing seed at the bottom initiates solidification. Growth proceeds by translating an axial temperature gradient through the crucible (moving furnace zones, or programmed multi-zone heater power ramp-down) rather than by mechanical crystal pulling — hence **no free melt/gas meniscus**, no rotation-induced or pulling-induced thermal transients, and much lower thermally induced stress.

**Process outline**:
1. Polycrystalline InP charge plus a seed crystal loaded into a pBN crucible, sealed in a quartz ampoule under P overpressure (or with a $\text{B}_2\text{O}_3$ encapsulant layer plus inert gas, similar rationale to LEC) to suppress dissociation — since the melt is still hot and P-rich vapor control is still required.
2. Multi-zone resistance furnace establishes an axial gradient straddling $T_m$ at the seed location.
3. Growth interface is advanced through the melt either by:
   - **VGF**: keeping the ampoule/crucible stationary and slowly lowering the furnace temperature profile (via programmed multi-zone power control) so the melting isotherm sweeps upward through the charge; or
   - **VB**: physically translating the crucible downward through a fixed axial gradient furnace.
4. Growth rates are slow, typically < 5 mm/h, to maintain a stable, nearly planar solid–liquid interface and minimize constitutional supercooling.

**Advantages over LEC**:
- Dramatically lower dislocation densities (EPD can be reduced by 1–2 orders of magnitude, approaching $10^2$–$10^4\ \text{cm}^{-2}$ or lower with dopant hardening) because axial/radial gradients are much smaller and more axially symmetric, and there is no pulling-induced or free-surface thermal perturbation.
- Better diameter uniformity and less thermal shock, since the crystal shape is defined by the crucible rather than a dynamically controlled meniscus.
- Reduced twinning tendency.

**Disadvantages**:
- Crystal is in contact with the crucible wall throughout growth, so wall-induced stress and possible contamination/wetting issues must be managed (pBN crucibles are preferred as InP does not wet pBN well).
- In-situ visual/optical monitoring of the growth interface is impossible (opaque furnace) — control is essentially open-loop, relying on precise thermal modeling and thermocouple feedback.
- Post-growth crystal removal from the shaped crucible can introduce additional handling-related defects if not carefully engineered (tapered crucible design/release layers).

### 3.4 Synthesis prior to growth

Because elemental In and P cannot simply be melted together safely (uncontrolled exothermic reaction, "P flash," explosive risk from high P vapor pressure), the polycrystalline InP charge is typically pre-synthesized in a separate, controlled step before either LEC or VGF/VB growth:
- **Horizontal Bridgman synthesis-and-growth**: In boat reacted with P vapor from a separately heated red-P source in a two-zone horizontal furnace, historically also used for full horizontal Bridgman (HB) crystal growth of InP, though HB is largely obsolete for InP due to D-shaped cross-section and higher dislocation density from asymmetric (gravity-driven) thermal gradients.
- **In-situ synthesis in the VGF/VCZ vessel**: a controlled, slow reaction between molten In and P vapor (from a solid P source at controlled temperature) directly inside the pBN crucible, immediately followed by growth in the same run, avoiding an extra transfer step and associated contamination risk.

## 4. Governing Physics During Growth

### 4.1 Segregation and dopant distribution

Dopant (S, Sn, Zn, Fe for semi-insulating, etc.) incorporation is governed by the effective segregation coefficient $k_{\text{eff}}$, related to the equilibrium coefficient $k_0$ via the Burton–Prim–Slichter relation:
$$
k_{\text{eff}} = \frac{k_0}{k_0 + (1-k_0)\exp\!\left(-\dfrac{v\delta}{D}\right)}
$$
where $v$ is the growth rate, $\delta$ the diffusion boundary layer thickness (set by melt convection strength), and $D$ the dopant diffusivity in the melt. Axial dopant (and hence resistivity/carrier concentration) uniformity is a first-order figure of merit for InP substrates used in epitaxial device layers.

### 4.2 Melt convection

Both LEC and VGF/VB melts experience:
- **Buoyancy-driven (natural) convection**, scaling with the thermal Grashof number $Gr = g\beta\Delta T L^3/\nu^2$
- **Forced convection** from crystal/crucible rotation in LEC (Reynolds/Ekman number regimes)
- **Marangoni (thermocapillary) convection** at the free InP/$\text{B}_2\text{O}_3$ or $\text{B}_2\text{O}_3$/gas interfaces in LEC, generally of secondary importance compared to GaAs LEC because the encapsulant damps surface-tension-driven flow at the melt surface itself

VGF/VB, lacking a free surface and rotation, generally operates at lower effective Grashof/Reynolds numbers, yielding more diffusive (less oscillatory) transport — one more reason for its superior compositional/thermal uniformity relative to LEC.

### 4.3 Thermal stress and dislocation generation

Thermoelastic stress in the growing crystal is estimated from the radial/axial temperature gradients via standard thermoelastic models (e.g., the Jordan–Von Neumann–Parasnis / Indenbom-type analyses used extensively for LEC GaAs and InP), giving a resolved shear stress $\tau$ that must be compared against the material's critical resolved shear stress $\tau_c(T)$, which itself falls sharply with increasing temperature. Because $\tau_c$ for InP is significantly lower than for GaAs at the same homologous temperature, InP-LEC crystals are intrinsically more prone to dislocation multiplication unless axial gradients are kept low — which conflicts with the need for gradients steep enough to maintain interface stability against constitutional supercooling from any local stoichiometric or dopant fluctuation. This tension is the core reason VGF/VB (which decouples interface stability control from a free-surface pulling process) has displaced LEC for InP.

## 5. Dislocation Reduction Strategies

- **Dopant hardening**: Isoelectronic or high-concentration dopants (notably S, or codoping strategies) increase the critical resolved shear stress by solid-solution strengthening, allowing higher thermal gradients to be tolerated without dislocation multiplication — used in both LEC and VGF InP.
- **Low-gradient furnace design**: multi-zone heaters (VGF) engineered to minimize radial gradients across the growing crystal.
- **Post-growth annealing**: controlled slow cooldown or dedicated anneal steps to relax residual thermal stress before the boule is removed from the furnace.
- **Seed and neck design**: careful necking (LEC) or seed selection (VGF/VB) to minimize propagation of seed-derived dislocations into the bulk of the crystal.

## 6. Post-Growth Processing

1. Boule characterization: X-ray diffraction (orientation, mosaic spread), etch pit density (EPD) mapping, resistivity/Hall mapping, IR transmission for inclusion/precipitate detection.
2. Wafering: ID (inner-diameter) saw or wire saw slicing to target orientation (typically (100), often with a few degrees offset toward (111) for epitaxial growth optimization) and thickness.
3. Lapping, polishing (mechanical + chemo-mechanical), and cleaning to epi-ready surface finish.
4. Final inspection: surface defect density, warp/bow, and particle counts against substrate specifications for downstream MOVPE/MBE epitaxy.

## 7. Comparative Summary

| Aspect | LEC | VGF / VB |
|---|---|---|
| Melt confinement | Free surface, $\text{B}_2\text{O}_3$ encapsulated | Fully enclosed in shaped crucible |
| P-loss suppression | Encapsulant + high inert gas overpressure | Encapsulant and/or controlled P vapor overpressure |
| Typical EPD | $10^4$–$10^5\ \text{cm}^{-2}$ | $10^2$–$10^4\ \text{cm}^{-2}$ (dopant-hardened) |
| Growth rate | Moderate (pulling-rate limited, ~5–15 mm/h) | Slow (<5 mm/h) |
| Diameter/shape control | Dynamic (meniscus/weight feedback) | Fixed by crucible geometry |
| In-situ monitoring | Optical (through encapsulant) | None (thermal/model-based only) |
| Throughput / cost | Historically established, flexible diameters | Slower cycle, but higher yield of usable low-defect material |
| Industrial status | Largely legacy / niche today | Dominant for modern semi-insulating and semiconducting InP substrates |

## 8. References for Further Study

- Standard reviews of LEC and VGF InP growth appear in *Journal of Crystal Growth* and in compilations from groups working on III-V bulk growth (e.g., Freiberger Compound Materials, AXT, and academic groups such as Rudolph, Jacob, Müller at IISB/IKZ).
- Rudolph, P., "Fundamentals and engineering of defects" — general treatment of dislocation generation in compound semiconductor melt growth, directly applicable to InP thermal-stress analysis.
- For continuum modeling of the melt (buoyancy, Marangoni, dopant segregation) consult the general melt-growth modeling references already compiled in the crystal growth reference library (CGSim/CrysMAS/FEMAG technical documentation and the Derby/Dupret/Kakimoto bibliographies).
