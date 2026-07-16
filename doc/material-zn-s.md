# Growth Processes for ZnS (Zinc Sulfide) — II-VI Semiconductor Crystal

## 1. Overview

Zinc sulfide (ZnS) is a wide-bandgap II-VI compound semiconductor ($E_g \approx 3.6\ \text{eV}$ for cubic zinc-blende, $E_g \approx 3.7\ \text{eV}$ for hexagonal wurtzite) used in optoelectronics, infrared windows/domes, phosphors, and scintillators. It exhibits two principal polytypes:

- **Zinc-blende (cubic, β-ZnS)** — stable below ~1020 °C
- **Wurtzite (hexagonal, α-ZnS)** — stable above ~1020 °C, up to the melting point

This polymorphic transition, combined with a high melting point and high equilibrium vapor pressure at melting, makes melt growth of ZnS extremely difficult. As a result, most bulk single-crystal ZnS is grown by **vapor-phase** or **vapor-transport** methods rather than conventional melt techniques (Czochralski, Bridgman) used for many other semiconductors.

---

## 2. Fundamental Materials Challenges

| Property | Value / Behavior | Growth Implication |
|---|---|---|
| Melting point | $\approx 1850\ ^\circ\text{C}$ (under high pressure; sublimes at ambient pressure) | Melt growth requires very high inert-gas overpressure (tens of atm) to suppress dissociative sublimation |
| Dissociation | $\text{ZnS(s)} \rightleftharpoons \text{Zn(g)} + \tfrac{1}{2}\text{S}_2\text{(g)}$ | Congruent sublimation dominates below melting point at 1 atm |
| Polymorphism | Zinc-blende $\leftrightarrow$ wurtzite at $\sim 1020\ ^\circ\text{C}$ | Crystals grown above the transition often revert to a twinned/faulted structure on cooling |
| Stacking faults | Very low stacking-fault energy | High density of stacking faults and polytypism (extensive $ABAB\ldots/ABCABC\ldots$ mixing) common in as-grown boules |

Because of the dissociative sublimation behavior, ZnS behaves similarly to other congruently subliming compounds (CdS, ZnSe) and is amenable to **physical vapor transport (PVT)** growth, in a manner analogous to the Piper–Polich / Markov modifications of sublimation growth used for CdS and ZnSe.

---

## 3. Principal Growth Methods

### 3.1 Physical Vapor Transport (PVT) / Sublimation-Recondensation

This is the dominant industrial and laboratory method for bulk ZnS single crystals.

**Principle:** High-purity polycrystalline ZnS source material sublimes in a sealed or flowing-ambient quartz ampoule under a controlled thermal gradient; vapor species (Zn, S₂, and ZnS molecular species) recondense on a cooler seed or nucleation zone to form single-crystalline or polycrystalline boules.

**Process steps:**

1. **Source preparation** — high-purity (5N–6N) ZnS powder, often synthesized in-house by controlled reaction of Zn vapor with H₂S, or by purification/sublimation passes of commercial ZnS powder to remove oxide and carbon contamination.
2. **Ampoule sealing** — source charge loaded into a fused-silica (quartz) or, for higher-purity work, pyrolytic-BN-lined ampoule; evacuated and sealed under vacuum ($<10^{-5}$ torr) or backfilled with an inert gas/halogen transport agent.
3. **Thermal gradient establishment** — two- or three-zone furnace; source zone held at $\sim 1100$–$1200\ ^\circ\text{C}$, growth (recondensation) zone at a somewhat lower temperature, with gradient typically a few °C/cm.
4. **Nucleation and growth** — vapor species transport down the gradient and condense; growth rate is controlled by the gradient magnitude, total pressure, and residual/transport gas composition. Growth rates are typically slow (sub-mm/hr to a few mm/hr) to allow single-crystal selection and to minimize polycrystallinity.
5. **Cooldown** — slow, controlled cooldown through the cubic–hexagonal transition point ($\sim 1020\ ^\circ\text{C}$) is critical to minimize stacking-fault and twin formation.

**Variants:**
- **Piper–Polich method** — closed-ampoule sublimation-recondensation, historically used for CdS and adapted for ZnS/ZnSe.
- **Iodine (or other halogen) vapor transport** — a small partial pressure of I₂ (or other transport agent) is added to enhance mass transport via reversible gas-phase reactions such as $\text{ZnS(s)} + \text{I}_2\text{(g)} \rightleftharpoons \text{ZnI}_2\text{(g)} + \tfrac{1}{2}\text{S}_2\text{(g)}$, allowing growth at lower temperatures and improved control of transport rate and stoichiometry.
- **Seeded PVT** — a single-crystal seed of the desired polytype/orientation is placed in the cooler zone to promote single-crystal (rather than polycrystalline boule) growth, analogous to seeded sublimation growth of SiC.

### 3.2 Chemical Vapor Transport (CVT)

Similar in spirit to halogen-assisted PVT but generally run at lower overall temperatures with a transport agent (commonly I₂, or sometimes NH₄Cl) mediating the mass flux between hot source and cooler crystallization zones in a sealed ampoule. CVT is used more for platelet/whisker crystals and for doped ZnS crystals (e.g., Mn-, Cu-, or Al-doped for phosphor applications) than for large boules.

### 3.3 High-Pressure Melt Growth (Bridgman-type)

Because ZnS decomposes below its true melting point at atmospheric pressure, melt growth requires:

- **Sealed, high-pressure crucibles** (e.g., graphite or BN crucibles inside a high-pressure vessel) with inert gas (Ar) overpressures of tens of atmospheres to suppress sulfur/zinc loss.
- **Bridgman–Stockbarger configuration**: crucible translated through a fixed axial temperature gradient across the melting isotherm ($\sim 1850\ ^\circ\text{C}$ under pressure).
- Because of the cubic-hexagonal phase transition on cooling through $\sim 1020\ ^\circ\text{C}$, boules grown from the melt nearly always undergo a solid-solid transformation, generating high densities of stacking faults, twins, and polytype boundaries — a major limitation compared to sublimation-grown material.

This route is much less common than PVT for ZnS specifically (it is more commonly associated with CdTe/ZnTe growth), owing to the severe pressure and containment requirements and the unavoidable phase-transition-induced defects.

### 3.4 Hot-Pressing / Chemical Vapor Deposition (CVD) — Polycrystalline Bulk ZnS

For optical-grade polycrystalline ZnS (e.g., FLIR-grade windows and domes), the dominant industrial process is **not single-crystal growth** but rather:

1. **CVD deposition** — ZnS is deposited from the gas-phase reaction of Zn vapor with H₂S:
$$\text{Zn(g)} + \text{H}_2\text{S(g)} \rightarrow \text{ZnS(s)} + \text{H}_2\text{(g)}$$
onto a mandrel or substrate held at $\sim 650$–$750\ ^\circ\text{C}$ in a CVD reactor, building up thick polycrystalline plates or dome shapes directly to net or near-net shape.
2. **Hot Isostatic Pressing (HIPing)** — as-deposited CVD ZnS ("raw" or "green" ZnS, wurtzite-rich with residual porosity/stress) is subsequently HIPed at elevated temperature ($\sim 950$–$1100\ ^\circ\text{C}$) and high pressure (~200 MPa Ar) to convert it to the cubic phase and eliminate voids, producing water-clear, low-scatter multispectral-grade ZnS.

This CVD + HIP route is the industrially dominant process for optical ZnS (e.g., "Cleartran"/multispectral ZnS), even though it produces polycrystalline rather than single-crystal material — worth distinguishing clearly from single-crystal boule growth methods above.

### 3.5 Solution and Flux Growth

- **Hydrothermal growth**: ZnS crystallizes from aqueous solution under moderate hydrothermal conditions (a few hundred °C, elevated pressure) using mineralizers (e.g., NH₄Cl, NH₄I solutions); produces small single crystals, historically used to study wurtzite/zinc-blende nucleation behavior.
- **Flux growth**: molten salt fluxes (e.g., alkali halides) used at lower temperatures to grow small ZnS single crystals or platelets, primarily for research rather than device-grade bulk material.

---

## 4. Comparative Summary

| Method | Typical Product | Crystal Form | Key Advantage | Key Limitation |
|---|---|---|---|---|
| PVT (sublimation-recondensation) | Bulk boules, platelets | Single crystal (seeded) or polycrystalline | Avoids melt/dissociation problem; established route for II-VI sublimers | Slow growth rate; polytype/stacking-fault control needed at 1020 °C transition |
| Halogen-assisted CVT/PVT | Boules, doped crystals | Single crystal | Lower growth temperature, better transport control | Halogen incorporation/purity control |
| High-pressure Bridgman melt growth | Boules | Polycrystalline/twinned single crystal | Faster growth than vapor methods | Extreme pressure/containment needs; phase-transition defects |
| CVD + HIP | Optical windows/domes | Polycrystalline (cubic after HIP) | Industrially mature, large net-shape optics | Not single-crystal; grain boundaries limit some applications |
| Hydrothermal / flux | Small crystals, platelets | Single crystal | Lower-temperature route; good for fundamental studies | Small crystal size, slow |

---

## 5. Key Process Control Parameters

- **Thermal gradient** in the growth zone: governs supersaturation and hence nucleation density vs. single-crystal selection.
- **Total ambient pressure / inert gas backfill**: suppresses excess dissociative sublimation and controls transport-species partial pressures.
- **Transport agent partial pressure** (halogens): tunes growth rate and can affect n-type/p-type behavior via unintentional doping.
- **Cooldown rate through the $\sim 1020\ ^\circ\text{C}$ cubic–hexagonal transition**: the single most critical parameter for minimizing stacking faults, twins, and microcracking in as-grown boules.
- **Source material purity/stoichiometry**: oxide and carbon contamination in starting ZnS powder strongly affects vapor transport behavior and final crystal purity.

---

## 6. References for Further Reading

- Piper, W. W. & Polich, S. J., *Vapor-phase growth of single crystals of II-VI compounds*, J. Appl. Phys. (1961).
- Markov, E. V. & Davydov, S. A., sublimation growth studies of CdS/ZnS analogues.
- Fang, X. et al., review articles on ZnS nanostructure and bulk crystal growth (various, 2000s–2010s).
- Raytheon/Rohm & Haas technical literature on CVD ZnS + HIP processing for multispectral optics.
- Klein, C. A., *Optical and mechanical properties of chemically vapor-deposited ZnS and ZnSe*, in various SPIE proceedings.
