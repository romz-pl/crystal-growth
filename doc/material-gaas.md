# Growth of GaAs Single Crystals

GaAs is the archetypal III–V compound semiconductor. Unlike elemental Si or Ge, its growth is complicated by two coupled facts: (1) it is a two-component (binary) melt with a congruently melting composition close to, but not exactly at, stoichiometry, and (2) one constituent — arsenic — has an equilibrium vapor pressure over the melt of several atmospheres at the melting point. Every industrial GaAs growth technique is built around managing this As overpressure while controlling melt stoichiometry, dopant incorporation, and thermal/convective conditions at the growth interface.

---

## 1. Material Background

- **Melting point:** $T_m \approx 1238\,^\circ\mathrm{C}$ (1511 K)
- **Crystal structure:** Zincblende (cubic, space group $F\bar{4}3m$), lattice constant $a \approx 5.653\,\text{Å}$
- **Congruent melting composition:** slightly As-rich of exact 50:50 stoichiometry
- **Arsenic vapor pressure over the melt at $T_m$:** on the order of 1 atm, rising steeply with temperature — this is the central engineering challenge
- **Key native point defect:** $\mathrm{As}_{Ga}$ antisite (EL2), whose concentration is set by the As/Ga ratio (melt stoichiometry) frozen in at the interface

Because arsenic volatilizes preferentially from the melt surface, GaAs growth methods split broadly into:

1. Methods that **pressurize the system with an inert gas** to suppress As loss while growing from a free liquid surface (LEC, HP-VCZ).
2. Methods that **physically seal the melt** so no free evaporating surface exists (VGF, VB, HB).

---

## 2. Liquid Encapsulated Czochralski (LEC)

LEC is the dominant historical method for producing large-diameter, semi-insulating GaAs boules (used for RF/microwave ICs and as substrates).

### 2.1 Principle

A layer of molten boric oxide ($\mathrm{B_2O_3}$) is floated on top of the GaAs melt inside a pressurized puller. The $\mathrm{B_2O_3}$ is chemically inert to GaAs, has low vapor pressure itself, wets both the crucible and the growing crystal, and — critically — is impermeable to As vapor. It physically seals the melt surface so arsenic cannot escape, while the crystal is pulled up through the encapsulant layer exactly as in conventional Czochralski.

### 2.2 Process Sequence

1. **Charge preparation.** Polycrystalline GaAs (pre-synthesized separately from elemental Ga and As, since direct in-situ synthesis under a seed-pulling geometry is impractical) is loaded into a pyrolytic BN (pBN) crucible along with solid $\mathrm{B_2O_3}$ encapsulant pellets.
2. **Chamber pressurization.** The growth chamber is sealed and pressurized with inert gas (typically $\mathrm{N_2}$ or Ar) to 10–100 atm — high enough to mechanically counteract the equilibrium As vapor pressure that would otherwise be reached if the melt surface were exposed. This is the origin of the term "High Pressure LEC" (HP-LEC).
3. **Melt-down.** RF or resistive heating melts the $\mathrm{B_2O_3}$ first (lower melting point), which flows to cover the GaAs charge as it subsequently melts, so the melt is never exposed to the ambient without encapsulation.
4. **Seeding.** A oriented seed crystal (commonly $\langle 100 \rangle$ or $\langle 111 \rangle$) is lowered through the $\mathrm{B_2O_3}$ layer into contact with the melt, partially dissolved back ("necking"/dash-neck technique to eliminate dislocations propagating from the seed), then withdrawn slowly while rotating.
5. **Shouldering and body growth.** Pull rate (~5–20 mm/hr) and rotation rate are adjusted to widen the crystal to target diameter (shoulder), then held to grow a constant-diameter body. Because the melt surface is not visible without special viewports/optics, diameter control in LEC relies more heavily on weighing the crystal (weight-sensing servo control) than on direct optical meniscus observation.
6. **Tailing and cool-down.** The diameter is tapered down to detach the crystal from the melt without thermal shock, followed by a slow, controlled cool of the whole furnace to room temperature to minimize thermal-stress-induced dislocations.

### 2.3 Governing Physics and Challenges

- **Stoichiometry control.** Because the encapsulant seals the melt, the As/Ga ratio in the melt drifts as growth proceeds (Ga is depleted preferentially into the growing solid relative to As, given the phase diagram near the congruent point). This directly sets EL2 concentration and hence the semi-insulating behavior needed for GaAs ICs.
- **Thermal stress and dislocation density.** LEC boules are grown with a large axial and radial temperature gradient (needed for interface stability and for keeping the $\mathrm{B_2O_3}$ molten) but this gradient is precisely what generates high thermal stress, and hence high dislocation densities ($10^4 - 10^5\,\mathrm{cm}^{-2}$), typically arranged in a characteristic W-shaped or cellular dislocation pattern across the wafer. This is LEC's principal disadvantage relative to sealed-ampoule methods.
- **Melt convection.** Buoyancy-driven convection, combined with forced convection from crystal/crucible rotation, governs heat and (in principle) dopant transport to the interface. The interface shape (convex/concave/flat) is a direct outcome of the competition between these flows and is actively controlled via rotation rate and pull rate to keep facets and defect nucleation under control.
- **$\mathrm{B_2O_3}$ water content.** Dissolved water (as OH groups) in the boric oxide affects its viscosity and its effectiveness at suppressing As outgassing; encapsulant is typically pre-dried/baked before use.
 
---

## 3. Vertical Gradient Freeze (VGF) and Vertical Bridgman (VB)

VGF/VB methods are the dominant modern approach for high-quality, low-dislocation-density semi-insulating and semiconducting GaAs, now largely displacing LEC for substrate production.

### 3.1 Principle

Instead of pulling a crystal from a free melt surface, the entire charge is sealed in an ampoule (or, in modern practice, a pBN crucible inside a sealed pressure vessel) and crystallization proceeds by **moving a temperature gradient along a stationary melt**, rather than moving the crystal through the furnace (as in horizontal/vertical Bridgman) or pulling material out (as in Czochralski).

- **VB (Vertical Bridgman):** the crucible/furnace assembly is translated relative to a fixed thermal gradient.
- **VGF (Vertical Gradient Freeze):** the crucible is stationary; instead, the furnace's temperature profile itself is ramped down progressively (via multi-zone heater control) so that the melting isotherm sweeps through the charge from bottom to top. This avoids all mechanical vibration associated with translating the crucible, which is one of VGF's chief attractions for dislocation reduction.

### 3.2 Process Sequence

1. **Sealed synthesis or pre-synthesized charge.** Either elemental Ga and As are reacted in situ under controlled As overpressure inside the sealed ampoule/crucible assembly, or pre-synthesized polycrystalline GaAs is loaded directly.
2. **Seed crystal.** A single-crystal seed is placed at the bottom of the crucible (typically a conical or pointed bottom to encourage single-grain necking from a small initial contact area).
3. **Melt-back.** The furnace is heated so the charge melts entirely while the seed tip is only partially melted back, preserving crystallographic registry with the seed.
4. **Controlled solidification.** In VGF, multi-zone resistance heaters are ramped down in a programmed sequence so the solid–liquid interface — nominally horizontal — advances slowly upward (typically fractions of a mm/hr to a few mm/hr) through the melt. In VB, the whole furnace/ampoule assembly is instead translated downward relative to a fixed axial gradient to achieve the same effect.
5. **Post-growth anneal.** Because the compound is grown in a sealed system, an As overpressure zone (either a separate As source region in the ampoule, held at a temperature controlling the equilibrium overpressure, or a pressurized inert-gas-backed sealed crucible) is maintained throughout growth to prevent As loss from the melt — this is the sealed-system analogue of the LEC encapsulant.

### 3.3 Governing Physics and Advantages

- **Low thermal gradients.** VGF/VB furnaces are operated with much smaller axial and (especially) radial temperature gradients than LEC, since diameter control does not depend on a meniscus/thermal-gradient balance the way Czochralski does — diameter is fixed by the crucible wall. Lower gradients directly translate into lower thermal stress and dislocation densities, routinely below $10^3\,\mathrm{cm}^{-2}$ and in optimized processes reaching near-dislocation-free material.
- **No free melt surface, no mechanical pulling/rotation.** This removes surface-tension-driven (Marangoni) convection contributions from the free surface (there isn't one) and removes vibration from crystal rotation/translation mechanisms, both of which are dislocation and micro-defect sources in LEC.
- **Interface shape control.** The solid–liquid interface shape (which strongly affects radial dopant/stoichiometry segregation and defect distribution) is controlled purely thermally, via the multi-zone heater profile, rather than via a rotation-convection balance — generally allowing flatter, more reproducible interfaces.
- **Segregation.** Because growth rates are much lower and interfaces flatter than in LEC, radial and axial dopant segregation (governed by the effective segregation coefficient $k_{eff}$, itself set by the interplay of the equilibrium segregation coefficient and boundary-layer transport at the interface) is generally more uniform in VGF/VB boules.
- **Cast shape constraint.** A structural tradeoff: crystals take the shape of the crucible, so complex or reduced-diameter seed/neck transitions (as used in Cz to filter dislocations) are harder to implement; wafer diameter is set by crucible diameter directly.

---

## 4. Horizontal Bridgman (HB)

Historically important for producing very low dislocation density GaAs (a horizontal ampoule allows the crystal to solidify against only a partial crucible wall contact, reducing stress from differential thermal contraction between crystal and crucible). It largely gave way to VGF/VB because it produces D-shaped rather than round boules, complicating wafer processing, but the underlying sealed-ampoule, moving-gradient physics is essentially the same as vertical Bridgman.

---

## 5. Common Cross-Cutting Physics

Across all these methods, several coupled physical mechanisms govern crystal quality:

$$
\text{Growth rate control:} \qquad v_{\text{growth}} \sim \frac{k \, \nabla T}{\rho \, \Delta H_f}
$$

where $k$ is thermal conductivity, $\nabla T$ the temperature gradient at the interface, $\rho$ the density, and $\Delta H_f$ the latent heat of fusion — i.e., interface advance is fundamentally a Stefan (moving-boundary) heat-conduction problem, modulated in Cz/LEC by convective heat transport from rotation and buoyancy.

- **Segregation at the interface** follows (in the diffusion-limited/boundary-layer picture) the Burton–Prim–Slichter relation, where $k_0$ is the equilibrium segregation coefficient, $v$ the growth velocity, $\delta$ the diffusion boundary layer thickness (set by convection strength), and $D$ the solute diffusivity in the melt:
  
$$
k_{\text{eff}} = \frac{k_0}{k_0 + (1-k_0)\exp(-v\,\delta/D)}
$$

- **Convective regime** (buoyancy vs. rotation vs. Marangoni, where applicable) sets $\delta$ and hence dopant/stoichiometry uniformity; this is the direct link to the fluid-dynamics/instability literature (Kelvin–Helmholtz transitions, oscillatory convection routes to turbulence) relevant to melt growth generally.

- **Dislocation generation** is predominantly thermal-stress-driven, following resolved shear stress on the relevant slip systems (for zincblende, primarily $\{111\}\langle 110\rangle$) exceeding the critical resolved shear stress at growth temperature — this is why gradient minimization (VGF/VB) outperforms LEC on dislocation density despite LEC's advantage in producible boule diameter and historical maturity.

---

## 6. Method Comparison Summary

| Aspect | LEC | VGF / VB |
|---|---|---|
| As containment | $\mathrm{B_2O_3}$ liquid encapsulant + high ambient pressure | Sealed ampoule/crucible, controlled As overpressure zone |
| Melt surface | Free (encapsulated) | None (fully sealed) |
| Diameter control | Weight-sensing servo, pull/rotation rate | Fixed by crucible geometry |
| Typical thermal gradients | High | Low |
| Dislocation density | $10^4 - 10^5\,\mathrm{cm^{-2}}$ | $<10^3\,\mathrm{cm^{-2}}$, near-zero achievable |
| Boule cross-section | Round, large diameter achievable | Round (VGF/VB) constrained by crucible |
| Maturity / historical role | Original industrial workhorse | Current dominant method for substrate-grade GaAs |
