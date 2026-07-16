# Growth Process for Gallium Phosphide (GaP) Single Crystals

## 1. Overview

Gallium phosphide (GaP) is a III-V compound semiconductor with an indirect band gap of approximately 2.24–2.26 eV at 300 K, crystallizing in the zinc-blende (cubic) structure. Its industrial importance stems from its use as a substrate for visible LEDs, and, more recently, in optoelectronic and nonlinear-optical devices. Growing bulk single crystals of GaP is significantly more challenging than growing elemental semiconductors like silicon, because the process must overcome the very high dissociation pressure of phosphorus at the melting point.

The dominant industrial technique is **Liquid Encapsulated Czochralski (LEC)** growth, sometimes also referred to as the liquid encapsulation pulling (LEP) method. Vertical Gradient Freeze (VGF) and Liquid Encapsulated Vertical Bridgman (LEVB) methods have also been explored, particularly for reducing dislocation density, but LEC remains the workhorse method for commercial GaP boules.

## 2. The Core Challenge: Phosphorus Volatility

GaP melts at approximately 1467–1500 °C. At these temperatures, GaP dissociates and phosphorus escapes as a gas well below the melting point — dissociation becomes significant above roughly 900 °C. If grown in an open system, the melt would rapidly lose phosphorus, driving the melt off-stoichiometry and making controlled single-crystal growth impossible.

The solution, pioneered by Mullin and coworkers and first demonstrated for GaP by Bass and Oliver (1968), is to cover the melt with a layer of molten **boric oxide (B₂O₃)**, which is:

- Chemically inert with respect to the melt,
- Impermeable to phosphorus vapor when molten,
- Transparent, allowing visual monitoring of the growth interface,
- Stable over the required temperature range without decomposing.

This encapsulant layer, combined with an inert gas overpressure in the growth chamber, suppresses phosphorus loss and allows the crystal to be pulled through the encapsulant layer into the cooler ambient above.

## 3. Starting Materials and Synthesis

Because GaP cannot easily be synthesized in situ from the elements inside the puller (unlike GaAs, which more readily forms in-situ), the compound is typically **pre-synthesized separately** before crystal growth:

1. High-purity elemental gallium (6N–7N) and red phosphorus are loaded into a sealed quartz ampoule or a synthesis apparatus fitted with a graphite crucible, RF heating coil, and thermocouple.
2. The gallium is heated (often by RF induction) while phosphorus vapor, generated from a separate zone of the ampoule, reacts with the molten gallium to form polycrystalline GaP.
3. The synthesized polycrystalline GaP charge is then used as the source material for the LEC pulling step.

Boric oxide is also prepared and dried prior to use, since B₂O₃ is hygroscopic and its moisture content must be tightly controlled — residual water content affects its viscosity, encapsulating behavior, and can introduce hydroxyl-related contamination into the crystal.

## 4. LEC Growth Procedure

### 4.1 Furnace Configuration

A typical GaP LEC puller consists of:

- A high-pressure vessel (autoclave) capable of withstanding **10–100 atm** of inert gas (commonly high-purity argon or nitrogen),
- An RF-heated or resistively-heated graphite crucible (often pyrolytic boron nitride, PBN, or graphite) containing the polycrystalline GaP charge,
- A radiation shield system to control the thermal profile above the melt,
- A seed crystal holder and pulling/rotation mechanism at the top,
- Viewing optics for observing the meniscus through the transparent B₂O₃ layer.

### 4.2 Charge Melting and Encapsulation

1. The polycrystalline GaP charge and solid B₂O₃ are loaded into the crucible, with the B₂O₃ on top of (or around) the charge.
2. The chamber is evacuated and backfilled with inert gas to the operating pressure (typically on the order of 10–55+ atm for GaP, reflecting its higher dissociation pressure relative to GaAs or InP).
3. The furnace is heated until the B₂O₃ softens and melts (softening point roughly 450–500 °C) and subsequently the GaP charge melts, at approximately **1467–1500 °C**. Once molten, the B₂O₃ layer floats on top of and completely covers the denser GaP melt, sealing it from the furnace atmosphere.

### 4.3 Seeding and Pulling

1. An oriented seed crystal (commonly ⟨100⟩ or ⟨111⟩) is lowered on the pull rod, through the molten B₂O₃ layer, until it contacts the GaP melt surface beneath.
2. The seed is partially melted back to remove strain and ensure a clean, defect-free interface, then withdrawn slowly while rotating.
3. A narrow-neck seeding step is typically used to minimize propagation of dislocations from the seed into the growing crystal.
4. The crystal is then widened ("shouldered out") to the target diameter and grown at constant diameter through careful control of pull rate and applied RF/resistive power.
5. Typical pulling rates reported for GaP are on the order of **2–5 mm/hour**, with crystal rotation used to promote a stable, symmetric growth interface and to homogenize the melt thermally and compositionally.
6. As the crystal is withdrawn, it passes upward through the B₂O₃ encapsulant layer, which continues to protect both the melt and the freshly grown crystal surface from phosphorus loss and oxidation until the crystal has cooled sufficiently.

### 4.4 Diameter and Interface Control

Because GaP LEC growth involves both a molten encapsulant and a high-pressure ambient, heat transfer is more complex than in ordinary Czochralski growth:

- Early in growth (small crystal length), **radiative heat transfer** dominates the thermal balance at the growth interface.
- As the crystal lengthens, **convective heat transfer** (buoyancy-driven and forced convection from rotation) becomes increasingly important.
- Diameter control is achieved by adjusting heater power in response to observed meniscus angle and crystal weight/diameter signals, since the balance of heat transfer mechanisms shifts throughout the run.
- Large-diameter GaP boules are especially prone to spontaneous cracking and diameter instabilities, a consequence of the thermal stresses generated by the steep temperature gradients needed to keep the encapsulant molten while maintaining a stable solid-liquid interface.

### 4.5 Cooling and Post-Growth

After the crystal has been fully pulled, it is generally left attached to the melt briefly and then slowly withdrawn further from the hot zone, or the whole furnace is cooled gradually, to minimize thermal shock and reduce dislocation generation from thermal stress. The dominant mechanism of dislocation generation in LEC-grown III-V crystals (GaP, GaAs, InP alike) is **thermal-stress-induced slip**, arising from the steep radial and axial temperature gradients inherent to the LEC configuration.

## 5. Dislocation Density Reduction Strategies

Because of the high melting point and steep gradients required, GaP LEC crystals tend to have relatively high dislocation densities compared to, e.g., silicon. Common mitigation strategies include:

- **Impurity hardening**: doping with elements that increase the critical resolved shear stress of the lattice (e.g., silicon), which raises the crystal's resistance to dislocation multiplication under thermal stress.
- **Reduced ambient temperature gradients**: achieved through improved radiation shielding and hot-zone design, lowering the thermal stress driving slip.
- **Low-gradient/low-stress LEC variants and VGF/VB methods**: since VGF and Vertical Bridgman growth impose a much lower axial gradient than LEC (the crucible, not a pulled boule, defines the geometry), they can produce lower dislocation density material, at the cost of more complex crucible/ampoule design to prevent sticking and cracking during cooling.

## 6. Doping

Following growth, or more commonly by adding dopants directly to the melt prior to/during growth:

- **n-type** conductivity: typically achieved with sulfur or tellurium doping.
- **p-type** conductivity: typically achieved with zinc doping.
- Semi-insulating or nominally undoped crystals are also grown for specific device applications.

## 7. Post-Growth Processing

Once the boule has cooled to room temperature:

1. The B₂O₃ residue is removed from the crystal surface (often by dissolution or mechanical cleaning).
2. The boule is oriented via X-ray diffraction and cut into wafers along the desired crystallographic plane.
3. Wafers are lapped, polished, and often prepared to "epi-ready" specification for downstream epitaxial growth (LPE, MOCVD, or MBE).

## 8. Summary Table

| Parameter | Typical Value / Note |
|---|---|
| Melting point | ~1467–1500 °C |
| Encapsulant | Molten B₂O₃ |
| Ambient gas | High-purity Ar or N₂, ~10–100 atm |
| Growth method | Liquid Encapsulated Czochralski (LEC) |
| Alternative methods | VGF, Liquid Encapsulated Vertical Bridgman (LEVB) |
| Typical pull rate | 2–5 mm/hour |
| Seed orientation | ⟨100⟩ or ⟨111⟩ |
| Crystal structure | Zinc-blende (cubic) |
| Dominant defect mechanism | Thermal-stress-induced slip/dislocations |
| n-type dopants | S, Te |
| p-type dopant | Zn |
| Dislocation mitigation | Impurity (e.g., Si) hardening, reduced gradients |

## 9. Key References

- Bass, S. J. & Oliver, P. E. (1968). *Pulling of Gallium Phosphide crystals in liquid encapsulation*, Journal of Crystal Growth 3–4, 286–290.
- Mullin, J. B. et al. (1965) — identification of B₂O₃ as encapsulant for III-V LEC growth.
- Nygren, S. F. et al. (1971); De Kock, A. J. R. et al. (1977); Roksnoer, P. J. et al. (1977) — LEC growth studies of GaP.
- Blum, S. E. & Chicotka, R. J. (1973); Woodbury, H. H. (1976); Gault, W. A. et al. (1986) — VGF growth of GaP.
- US Patent 4,303,464 — *Method of manufacturing gallium phosphide single crystals with low defect density.*
- Wikipedia: *Gallium phosphide* — general properties and LEC overview.
