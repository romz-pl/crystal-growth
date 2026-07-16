# Growth Process of ZnTe (Zinc Telluride) Single Crystals

## 1. Material Background

Zinc telluride (ZnTe) is a wide-bandgap II–VI compound semiconductor with the zinc-blende crystal structure (space group $F\bar{4}3m$), lattice constant $a \approx 6.104\ \text{Å}$, and a direct optical bandgap of approximately $2.26$–$2.39\ \text{eV}$ at room temperature. It is one of the few II–VI compounds that is naturally p-type (owing to native Zn vacancies acting as shallow acceptors), which makes it important as:

- A substrate for lattice-matched epitaxy of narrower-gap materials such as InAs ($a = 6.058\ \text{Å}$) and GaSb ($a = 6.096\ \text{Å}$).
- An active layer for green light-emitting diodes and laser diodes.
- A buffer/window layer in CdTe-based thin-film photovoltaics.
- A component of the ternary alloy $\text{Cd}_{1-x}\text{Zn}_x\text{Te}$ (CZT), used for room-temperature nuclear radiation detectors.
- A terahertz generation/detection medium via optical rectification.

The central obstacle to bulk ZnTe growth is its combination of a high melting point ($T_m \approx 1295\text{–}1300\ ^\circ\text{C}$) with a high equilibrium vapor pressure and strong preferential volatilization of Zn near the melting point. The relatively high melting point of ZnTe and serious Zn volatilization are regarded as the main problems in producing ZnTe crystals. This forces growers to choose between three broad families of technique, each trading off growth rate, crystal size, and defect content differently.

---

## 2. Overview of Growth Method Families

| Method family | Typical technique | Growth temperature | Typical crystal size | Main advantage | Main drawback |
|---|---|---|---|---|---|
| Melt growth (stoichiometric) | Vertical Bridgman / VGF, LEC/LEK | ~1300 °C | Large boules (φ 20–50 mm) | High growth rate | High Zn pressure; unsafe with quartz ampoules; high defect density |
| Solution (flux) growth | Te-flux vertical Bridgman, Traveling Solvent Method (TSM/THM) | 800–1100 °C | Medium boules (φ 20–30 mm) | Lower process temperature; improved stoichiometry control | Slower growth; solvent (Te) inclusion risk; segregation along ingot |
| Vapor growth | Physical Vapor Transport (PVT), seeded/self-seeded, sublimation–recondensation | 900–1150 °C | Smaller boules (≤ 1 inch), high purity | Lowest defect density, twin-free, high purity | Slow growth rate; not scalable to large boules |

Among these approaches, the vapor process is considered not proper for large ZnTe crystal fabrication, while ZnTe crystal grown from stoichiometric melt in an enclosed system is costly and unsafe, since the required furnace temperature exceeds the softening point of a quartz crucible. This trade-off is why Te-flux (solution) Bridgman growth has become the most widely reported compromise route for producing crystals of usable size (tens of mm) without the extreme thermal and pressure demands of stoichiometric melt growth.

---

## 3. Solution (Te-Flux) Vertical Bridgman Growth

This has become the most common approach for producing sizeable ZnTe boules and is described here in detail as the primary route.

### 3.1 Rationale for Using a Te Flux

The growth of ZnTe crystal is greatly improved by using Te as a flux, because the crystallization temperature can be sharply decreased relative to the congruent melting point of stoichiometric ZnTe. Operating on the Te-rich side of the pseudo-binary Zn–Te phase diagram allows growth from a liquidus temperature well below 1295 °C, which:

- Reduces Zn vapor pressure and hence ampoule stress/safety hazards.
- Suppresses constitutional problems associated with congruent melting.
- Permits use of standard fused-silica (quartz) ampoules rather than exotic high-pressure vessels.

### 3.2 Charge Preparation

1. **Raw materials**: high-purity (typically 99.99%+) elemental Zn and Te.
2. **Off-stoichiometric loading**: a Te-rich mole ratio is deliberately chosen — reported compositions include an initial Zn/Te mole ratio of 3:7 for the flux route.
3. **Presynthesis**: the elements are reacted in a rocking (rotating) furnace prior to the actual growth run. ZnTe polycrystalline material combined with excess Te is fabricated via a rocking technique at approximately 1100 °C, ensuring homogeneous pre-reaction and outgassing of the charge before directional solidification.
4. **Ampoule**: a fused-silica ampoule, typically conical- or pointed-bottom to promote single-nucleus selection, evacuated and sealed under vacuum (or with a small inert gas overpressure in some variants).

### 3.3 Directional Solidification (Bridgman) Run

The sealed ampoule is translated through a two- (or multi-) zone furnace with a fixed axial temperature gradient, so that the solid–liquid interface advances through the melt from the cold (seed or spontaneous-nucleation) end toward the hot end.

Representative process parameters reported in the literature:

- Axial temperature gradient: on the order of 40 °C·cm⁻¹ at the growth interface.
- Translation (growth) rate: on the order of 5 mm·day⁻¹.
- Resulting boule dimensions: boules of order φ 25 mm × 65 mm have been reported by this route; other reports describe boules of order 50 mm in length and 19 mm in diameter from related two-zone tubular-furnace Bridgman configurations.

### 3.4 Accelerated Crucible Rotation Technique (ACRT)

Because excess Te is present as a flux, the melt composition becomes progressively more dilute in Zn as growth proceeds, making solute (Zn) transport to the growth interface the rate-limiting and homogeneity-limiting step. Since excess Te is added, crystal growth proceeds in an ever-diluting system, making solute transfer a key issue. To address this:

- ACRT is applied to introduce forced convection, enhancing mass transfer and improving interface morphology.
- Sub-grain formation and inclusion defects are also suppressed by the resulting convective mixing.
- ACRT-grown boules of 30 mm in diameter and about 60 mm in length have been reported, with undoped-crystal resistivity reaching up to about 700 Ω·cm.

### 3.5 Compositional/Quality Trends Along the Ingot

- Single crystals formed in the earlier stage of growth show better quality than material solidified later, consistent with progressive solute depletion and constitutional supercooling risk as the Te-rich melt is consumed.
- Post-growth characterization typically includes optical transmission microscopy, EDS, SEM, EPMA, UV–Vis and FTIR spectroscopy, and electrical (resistivity) measurement to map composition and property homogeneity along the boule axis. These techniques together allow discussion of the phase/composition distribution across the whole ingot.

### 3.6 Alternative Two-Zone Tubular-Furnace Bridgman Variant

A related but distinct implementation uses direct solid-state reaction synthesis followed by growth in a two-zone tubular furnace rather than a dedicated multi-zone Bridgman stack:

- Synthesis is carried out by solid-state reaction of 99.99%-pure Zn and Te, and the resulting single crystal (~50 mm long, ~19 mm diameter) is grown by Vertical Bridgman Technique using a two-zone tubular furnace.
- Resulting crystal properties reported for this route: an optical band gap of approximately 2.26 eV, good crystalline perfection as assessed by HRXRD and chemical etching, and an etch-pit dislocation density of about 4 × 10³ cm⁻².
- Dielectric properties were also measured across a wide frequency range (100 Hz to 10 MHz) at room temperature.

---

## 4. Physical Vapor Transport (PVT) Growth

PVT (sublimation–recondensation) growth exploits the high vapor pressure that is problematic for melt growth, turning it into the transport mechanism itself.

### 4.1 Principle

A polycrystalline ZnTe source charge is held at a higher temperature at one end of a sealed, evacuated ampoule; the vapor species (dominantly Zn and Te₂, by analogy with the well-studied ZnSe system) sublime from the source, diffuse/convect across the ampoule, and recondense at a cooler seed or self-nucleated growth front at the other end. Calculations for the ZnTe system indicate that the Stefan flux dominates the flow field and that gravity effects are generally small, owing to the reduced difference in molecular weights between the transported vapor species.

### 4.2 Source Preparation

Following practice established for the closely related ZnSe system:

- Starting materials are baked out or vacuum-distilled to obtain a near-congruently subliming composition.
- Source materials are heat-treated (e.g., H₂ reduction) to remove surface oxides, then baked under dynamic vacuum to adjust the source composition toward congruent sublimation.

### 4.3 Growth Configuration

- Both **horizontal** self-seeded/contactless and **seeded, closed-ampoule** configurations are used. A simple, horizontal, low-temperature PVT technique has been used to grow large (1-inch-diameter), twin-free crystals of ZnTe and Cd₁₋ₓZnₓTe suitable for MBE substrates.
- In self-seeded/contactless growth, crystals grow away from the ampoule wall, with large facets tending to align parallel to the gravity direction, which minimizes wall-induced strain relative to melt growth in contact with a crucible.
- Seeded growth on oriented CdZnTe or ZnTe seeds is also reported for the related ternary: crystals of Cd₁₋ₓZnₓTe were grown on monocrystalline seeds by closed-ampoule PVT, with or without excess (Cd + Zn) present in the vapor phase, followed by controlled post-growth cool-down.

### 4.4 Advantages and Limitations

**Advantages:**
- Substantially lower process temperature than stoichiometric melt growth.
- The reduced temperature also helps avoid twins and dislocations, which are easily produced in II–VI semiconductors at higher growth temperatures because of their low stacking-fault energy.
- No physical contact with a crucible wall over most of the growth interface (in self-seeded/contactless configurations), lowering thermally induced strain.
- Compatible with in-situ optical diagnostics: partial vapor pressures of the transported species can be measured in situ via optical absorption at characteristic wavelengths, allowing direct monitoring of the transport flux during growth.

**Limitations:**
- The time required to transport sufficient material to grow large crystals by the vapor phase is quite long, which is the principal reason PVT is not favored for large-boule production.
- Achievable boule sizes are correspondingly modest — on the order of 1 inch in diameter for the best-optimized systems — versus tens of millimeters routinely reached by Bridgman/solution methods.

### 4.5 Purity and Impurity Signatures

Comparative photoluminescence studies distinguish PVT material from solution/THM-grown material: copper is identified by photoluminescence as a major impurity in both PVT- and THM-grown ZnTe, forming a substitutional acceptor, but THM-grown crystals are found to contain more Cu than PVT-grown crystals. Correspondingly, infrared absorption spectra of vapor-grown ZnTe are typically featureless, whereas THM samples show several sets of distinct peaks attributable to Cu²⁺ impurities.

---

## 5. Traveling Heater Method (THM) / Traveling Solvent Growth

THM is a solution-growth variant in which a narrow molten zone (rich in Te solvent) is translated through a stationary polycrystalline (or seeded) column of source material, dissolving source material at the leading edge and depositing single-crystalline material at the trailing edge as the zone advances.

- ZnTe crystals have been produced by a Te-solution vertical traveling heater method, in parallel with horizontal PVT growth, for direct comparison of crystal orientation and electrical properties via X-ray Laue diffraction and Hall measurements.
- THM offers continuous purification (zone-refining character) and lower operating temperature than stoichiometric melt growth, similar in spirit to the Te-flux Bridgman approach, but with continuous solvent-zone translation rather than bulk solidification of a fixed Te-rich charge.
- As noted above, THM-grown ZnTe tends to retain more Cu impurity than PVT material, an important consideration when selecting a growth route for detector- or optics-grade material.

---

## 6. Phase Equilibrium and Stoichiometry Considerations

Precise control of the Zn:Te ratio in the growth environment is critical because the single-phase homogeneity range of ZnTe is extremely narrow:

- P–T–X phase equilibrium studies show that the stoichiometric plane (X = 50 at.% Te) lies completely outside the single-phase volume of ZnTe.
- The Te-rich phase boundary exhibits retrograde solubility, with a maximum Te non-stoichiometry of 0.0186 at.% found at 1344 K.
- For the related solid solution: the Zn-rich boundary of the ZnTe solidus lies at 50.004–50.005 at.% Te over the range 826–1153 K, and increasing ZnTe content in Cd₁₋ₓZnₓTe solid solutions shifts the solidus further toward the Te-rich side, so that even modest Zn incorporation (x ≈ 0.15) removes the stoichiometric plane from the solidus entirely.

These extremely narrow homogeneity ranges explain why (a) small deviations in charge composition or furnace temperature profile can shift the growth regime from single-phase to two-phase (Te precipitate–containing) material, and (b) Te-flux approaches, which deliberately operate off the stoichiometric plane, are often more forgiving of composition control than attempts at strictly congruent, stoichiometric melt growth.

---

## 7. Post-Growth Characterization Methods

Across all growth routes, the following characterization suite is standard for assessing crystalline quality and composition:

- **Structural**: single-crystal and powder X-ray diffraction (XRD), high-resolution XRD (HRXRD), synchrotron X-ray topography (reflection, transmission, and Laue back-reflection).
- **Defect assessment**: chemical etching and etch-pit density (EPD) counting; identification of twins, dislocations, precipitates, and slip bands via topography; transmission electron microscopy (TEM) for microstructure.
- **Compositional**: energy-dispersive spectroscopy (EDS), electron probe microanalysis (EPMA).
- **Optical**: UV–Vis transmission/absorption for bandgap determination; FTIR transmission; low-temperature photoluminescence (PL) for impurity/defect identification (e.g., Cu-related acceptor complexes).
- **Electrical**: resistivity and Hall-effect measurements; dielectric measurements over a wide frequency range.
- **Morphological**: atomic force microscopy (AFM) of as-grown or polished surfaces.

---

## 8. Summary Comparison

| Aspect | Stoichiometric melt Bridgman | Te-flux Bridgman (± ACRT) | PVT (vapor transport) | THM (Te-solution zone) |
|---|---|---|---|---|
| Approx. growth temperature | ~1295–1300 °C | ~800–1100 °C | ~900–1150 °C (source) | Similar to flux Bridgman, zone-local |
| Typical growth rate | Faster | ~5 mm/day (reported) | Slow (vapor-flux limited) | Slow (zone-translation limited) |
| Typical boule size | Large, but hazardous to produce | φ 25–30 mm, tens of mm long | Up to ~1 inch diameter | Comparable to flux Bridgman |
| Dominant defects | Zn-vacancy-related, high dislocation density, ampoule stress | Sub-grains/inclusions (mitigated by ACRT), axial compositional gradient | Twins/dislocations minimized; Cu often lower than THM | Cu impurity incorporation tends to be higher |
| Key risk | Ampoule failure from Zn vapor pressure; softening of quartz | Progressive Zn depletion of melt; solute-transport control | Very slow growth; boule size limited | Compositional homogeneity along translated zone |

---

## 9. Key References

1. Jin, M., Yang, W.-H., Wang, X.-H., Li, R.-B., Xu, Y.-D., Xu, J.-Y., "Growth and characterization of ZnTe single crystal via a novel Te flux vertical Bridgman method," *Rare Metals*, 40 (2021) 858–864.
2. Shkir, Mohd., Bhagavannarayana, G., Wahab, M. A., "Characterization of ZnTe single crystal grown by Vertical Bridgman Technique using two zone tubular furnace," *Optics & Laser Technology* (2012).
3. "Growth of ZnTe single crystals from Te solution by vertical Bridgman method with ACRT," *Journal of Crystal Growth* (2014).
4. Volz, M. P., Gillies, D. et al., "Growth of ZnTe by Physical Vapor Transport and Traveling Heater Method," NASA Marshall Space Flight Center, NTRS 19970012894.
5. "Photoluminescence of vapor and solution grown ZnTe single crystals" (PL/AFM comparative study of PVT vs. THM ZnTe).
6. Palosz, W., George, M., "Mass flux of ZnSe by physical vapor transport," *Journal of Crystal Growth* (1995) — vapor-species and PVT modeling methodology directly extended to ZnTe.
7. Su, Ching-Hua, *Vapor Crystal Growth and Characterization: ZnSe and Related II–VI Compound Semiconductors*, Springer (2020) — covers ZnTe, CdS, CdTe, ZnSeTe, ZnSeS PVT growth in depth.
8. "Seeded physical vapor transport of cadmium-zinc telluride crystals: growth and characterization," *Journal of Crystal Growth* (1998).
9. "Comparison of cadmium zinc telluride crystals grown by horizontal and vertical Bridgman and from the vapor phase," *Journal of Crystal Growth* — THM/Bridgman/vapor comparative review, directly relevant to ZnTe-containing CZT.
