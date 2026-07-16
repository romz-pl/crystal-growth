# Growth of ZnSe (Zinc Selenide) Single Crystals

ZnSe is a wide-bandgap ($E_g \approx 2.7\ \text{eV}$ at 300 K) II-VI compound semiconductor with the zincblende (3C, sphalerite) structure as its thermodynamically stable form at room temperature. It is technologically important for blue-green optoelectronics, mid-infrared nonlinear optics (orientation-patterned ZnSe for frequency conversion), IR windows/lenses, and as a substrate for II-VI epitaxy. Bulk single-crystal growth of ZnSe is unusually difficult compared with other zincblende semiconductors (GaAs, InP) because of a combination of a high melting point, a solid-solid phase transformation close to the melting point, and a strong intrinsic tendency toward twinning. This document surveys the two dominant families of growth technique — vapor-phase growth and melt growth — along with the underlying materials-physics obstacles that shape process design.

---

## 1. Why ZnSe Is Difficult to Grow

Three material properties dominate all process choices for ZnSe:

1. **High melting point.** The congruent melting point of ZnSe has been measured at $T_m = 1522 \pm 2\,^{\circ}\text{C}$ in Bridgman-type differential thermal analysis studies, consistent with other literature values around 1520–1525 °C (some sources quote $T_m \approx 1797\ \text{K}$, i.e. ≈1524 °C, in a closed double-crucible configuration).

2. **A solid-solid phase transition near the melting point.** A 2H (wurtzite) to 3C (zincblende) solid-solid phase transformation occurs at 1411 ± 2 °C, only about 100–110 °C below the melting point. This phase transition, roughly 100 °C below the melting temperature, is a primary cause of twinning along {111} planes during stoichiometric melt growth, which effectively rules out cutting usable (100) wafers from as-grown boules unless the transition is avoided or suppressed.

3. **Incongruent, non-stoichiometric vaporization/evaporation.** ZnSe does not evaporate or melt with a fixed vapor composition matching the solid; source material composition drifts with temperature and processing history, requiring active compositional control (e.g., H₂ reduction and vacuum bakeout of source charges) before growth.

Because of these three factors, melt growth of ZnSe is impaired by its high melting point, deviation from stoichiometry from incongruent evaporation, and a pronounced tendency toward twinning, this last property being the most limiting. Extensive efforts in the late 1990s to develop ZnSe melt growth for blue-green diode applications were largely abandoned both because of severe twinning and because GaN-based devices superseded ZnSe diodes commercially. Interest in ZnSe growth was subsequently revived by its exceptional mid-IR nonlinear-optical properties. ZnSe offers a high nonlinear figure of merit, an extremely wide transparency range from about 0.48 to 22 μm, low dispersion favoring wide-bandwidth frequency conversion, and very low optical absorption losses, motivating renewed effort on physical vapor transport as an alternative to melt growth.

---

## 2. Vapor-Phase Growth Methods

Because melt growth is complicated by twinning and the near-coincident phase transition, vapor transport techniques have historically been the more successful route to optically and structurally high-quality ZnSe, particularly for substrate and detector applications.

### 2.1 Physical Vapor Transport (PVT)

In PVT, polycrystalline ZnSe source material sublimes at the hot end of a sealed ampoule and re-condenses as single crystal at a cooler zone, transported purely by the vapor-pressure gradient of the constituent species (no chemical transport agent).

**Source preparation.** Source materials are heat-treated by H₂ reduction to remove surface oxide, followed by baking under dynamic vacuum to shift the source composition toward that of congruent sublimation. This step is critical: an oxide-contaminated or off-stoichiometric charge produces poor crystal quality and irreproducible transport rates.

**Self-seeded (unseeded) horizontal PVT.** ZnSe crystals have been grown by self-seeded PVT in a horizontal ampoule configuration. Crystals grown "contactless" (away from the ampoule wall) develop large (110) facets that tend to align parallel to gravity, with SEM and AFM images showing large (110) terraces and growth steps dominating the as-grown facet surfaces. Residual gas analysis of processed ampoules shows the leftover gas is predominantly CO and H₂, at similar pressure and composition regardless of which source preparation was used, indicating outgassing (not source-composition variation) is the main residual-gas contributor. A one-dimensional multi-species diffusion model of ampoule mass flux has been used to define the conditions needed for contactless (non-wall-nucleated) growth.

**Seeded PVT (SPVT).** Deliberate seeding gives better control over crystal orientation and reduces spurious nucleation.
- A ZnSe crystal was grown by seeded PVT in the horizontal configuration at a growth temperature of 1120 °C with the furnace translated at 3 mm/day.
- In-situ optical absorption measurements of Se₂ partial pressure were taken at three positions along the ampoule at 90-minute intervals during growth, using a specially built furnace with side viewing windows and a fused-silica ampoule fitted with a square optical-path section. Measured Se₂ partial pressures ranged from about $2.0$ to $6.5\times10^{-3}$ atm, and did not match a simple 1-D diffusion transport model, indicating the source composition drifted toward Se-rich as growth proceeded — direct evidence of the incongruent-vaporization problem discussed in Section 1.
- Seeded PVT (SPVT) ZnSe grown for homoepitaxial substrate use is highly crystalline and high-resistivity as-grown; post-growth Zn-extraction anneals can convert it n-type, reaching resistivities as low as 3.82 Ω·cm and free-carrier densities near $1.5\times10^{15}\ \text{cm}^{-3}$. Residual conductivity is limited by unwanted acceptor impurities, chiefly Cu and Li, underscoring the need for high-purity source charges and ampoule materials.

**Vertical (stabilized) PVT and doped crystals.** Cr-doped ZnSe has been grown by self-seeded PVT in both stabilized-vertical and horizontal ampoule configurations, using ZnSe + CrSe source mixtures, at growth temperatures of 1140–1150 °C and furnace translation rates of 1.9–2.2 mm/day. SEM/AFM surface studies show that vertically and horizontally grown crystals exhibit distinctly different as-grown surface morphology, implying different dominant growth mechanisms between the two orientations; Cr concentrations of $1.8$–$8.3\times10^{19}\ \text{cm}^{-3}$ were achieved, relevant to Cr:ZnSe mid-IR laser gain media.

**Crystalline quality assessment.** Impurity and defect content in PVT-grown ZnSe has been characterized by glow-discharge mass spectrometry (GDMS) and low-temperature photoluminescence (PL), with PL results consistent with the low impurity levels found by GDMS. Crystalline perfection has been assessed by synchrotron white-beam X-ray topography (SWBXT) and high-resolution triple-axis X-ray diffraction (HRTXD); apart from twinning, the contactless-grown regions show quite high crystalline quality by both techniques, and HRTXD results on chemically-mechanically polished versus cleaved surfaces are in agreement.

**Practical throughput limitation.** Despite good crystalline quality, PVT and CVT approaches have not been able to deliver large-diameter ingots — boules greater than about 50 mm in diameter are not accessible by vapor transport, which is the principal reason melt-growth alternatives continue to be pursued for large-aperture optical components.

### 2.2 Chemical Vapor Transport (CVT)

CVT uses a transport agent (classically iodine) to mediate reversible gas-phase reactions that carry Zn and Se species from the hot source zone to the cooler growth zone, rather than relying on direct sublimation/condensation.

- A thermodynamic model has been developed for CVT growth of ZnSe single crystals using iodine as the transport agent, and optimum growth conditions have been predicted from calculated partial pressures of the various gas-phase species in the ZnSe–I₂ system.
- Historically, high-structural-quality ZnSe single crystals for LED substrates have also been produced by iodine transport and by direct sublimation methods, in addition to melt growth, indicating CVT and PVT have coexisted as complementary routes depending on the required crystal size, purity, and orientation.
- I₂-mediated CVT tends to run at somewhat lower source temperatures than pure PVT sublimation, at the cost of iodine incorporation as a potential impurity/dopant that must be controlled or annealed out.

### 2.3 Motivation for Vapor Growth over Melt Growth

For high-melting-point II-VI compounds such as ZnTe, CdS, ZnSe, and ZnS, vapor growth techniques offer significant advantages over melt growth precisely because of these compounds' high melting points. Vapor growth avoids the need to hold a large ionic-covalent melt above 1500 °C in contact with a crucible, sidestepping crucible-melt reactivity, gross constitutional supercooling, and much (though not all) of the twinning associated with the near-$T_m$ 2H↔3C phase transition. Its principal drawback remains the practical ceiling on boule diameter and growth rate (typically ≤ few mm/day translation), which limits wafer/optic sizes relative to melt-grown material.

---

## 3. Melt-Growth Methods

Melt growth is pursued mainly where larger apertures (multi-cm diameter) are required, e.g. for bulk optics and orientation-patterned nonlinear crystals, despite the twinning risk described in Section 1.

### 3.1 Vertical Bridgman under Inert Gas Overpressure

Because ZnSe has significant equilibrium vapor pressure near its melting point, an inert overpressure (commonly argon) is used to suppress dissociative vaporization and control stoichiometry during Bridgman growth.

- Crystals have been grown by the Bridgman technique at crucible lowering rates of 0.8–10.1 mm/h under an argon pressure of 100 kg/cm².
- **Grain-boundary defect formation is orientation-dependent.** The formation of rod-like low-angle grain boundaries depends on the angle $\theta$ between the growth axis and the (111) twin-plane normal: for $75^\circ < \theta < 90^\circ$ these boundaries form, while for $\theta < 75^\circ$ crystals free of them can be grown at the lowering rates used. Void formation, separately, depends on the crucible lowering rate, and many crystals free of both voids and grain boundaries were obtained over the range 0.8–2.5 mm/h. This is a key practical design rule: **seed/growth-axis orientation relative to {111} matters as much as thermal gradient control** for defect-free Bridgman ZnSe.
- **Twin-free growth window.** Twin-free undoped ZnSe crystals up to 25 mm in diameter by 25 mm in length have been grown by vertical Bridgman. Macro-defects (voids and twins) were suppressed by controlling both the crucible downward velocity and the crucible cone half-angle: large twin-free crystals resulted when velocity did not exceed 4 mm/h and the cone angle was either 30° or 45°; above 4 mm/h only polycrystalline material formed. High-purity ingots grown this way showed most impurities below 1 ppm or below detection limits.
- **Melt superheating and structural memory.** Inadequate superheating of a stoichiometric melt prior to growth can leave "associated melt complexes" (structural memory of the solid) intact in the liquid, which then influences nucleation mode, substructure, and twinning tendency, as well as growth orientation, once solidification begins. Non-stoichiometric melts with excess Te (an analogous II-VI system) show markedly increased and more transient supercooling, and holding time in the molten state further affects the degree of supercooling observed — the general principle (superheat above $T_m$, and hold time at temperature, control the "memory" of the melt structure) transfers directly to ZnSe process design.

### 3.2 Closed Double-Crucible Bridgman (Twin-Free, Large-Diameter)

To suppress compositional drift of the melt (a major driver of twinning and grain-boundary defects), a two-chamber crucible design has been used to physically decouple the growing crystal from bulk melt composition changes.

- A closed double-crucible was adopted specifically to prevent deviation from stoichiometric melt composition during Bridgman growth, and optimum growth conditions were determined for it.
- The optimized recipe used an overheating temperature 76 K above the melting point (i.e. roughly 1523 + 76 ≈ 1599 °C locally, referencing $T_m = 1797\ \text{K}$), an axial temperature gradient of 30 K/cm at the growth interface, and a growth rate of 3.6 mm/h.
- Under these conditions, twin-free, high-quality ZnSe single crystals were grown reproducibly using a polycrystalline seed. Etch-pit density (EPD) measured on cleaved (110) faces averaged about $2.0\times10^{5}\ \text{cm}^{-2}$, a useful benchmark figure for dislocation density in melt-grown ZnSe.

### 3.3 High-Pressure Bridgman (HPB) and High-Pressure Vertical Zone Melting (HPVZM)

For larger, plate/tape-form crystals (relevant to detector-grade material), high-pressure variants have been used.

- HPB and HPVZM processes have produced Cd₁₋ₓZnₓTe, CdSe, and ZnSe crystal "tapes" up to 120 × 120 × 12 mm in size. The effect of process parameters on crystal quality and material properties has been characterized, along with how inclusion (bubble) content depends on the melt's deviation from stoichiometry, and a method for growing plates with reduced inclusion content has been described. Undoped high-resistivity ZnSe tapes with resistivity greater than $10^{11}\ \Omega\cdot\text{cm}$ were achieved, alongside CdZnTe ($10^{10}\ \Omega\cdot\text{cm}$) and CdSe ($10^{11}\ \Omega\cdot\text{cm}$).
- Oriented-seed tape growth was demonstrated for CdSe, and the principal differences in outcome between the HPB and HPVZM approaches have been documented, providing a comparative basis for selecting one over the other depending on whether plate geometry or diameter/aspect ratio is the priority.

### 3.4 Off-Stoichiometric (Solution) Melt Growth: ACRT-Combined High-Pressure Bridgman

A more recent strategy sidesteps the wurtzite↔zincblende phase transition entirely by melting from a Se-rich melt-solution at reduced temperature, rather than from the congruent stoichiometric melt.

- Because the 2H→3C phase transition occurs at about 1425 °C, roughly 100 °C below the true ZnSe melting point, stoichiometric melt growth passes through this transition and develops {111} twinning that disrupts single-crystallinity, preventing extraction of usable (100) wafers.
- To avoid the transition altogether, ZnSe has been grown from an off-stoichiometric, Se-rich melt-solution using the Accelerated Crucible Rotation Technique combined with high-pressure Bridgman (ACRT-HPB). A slight excess of Se in the growth charge lowers the effective melting/crystallization temperature to below 1400 °C, keeping growth entirely within the stable zincblende phase field and avoiding the disruptive phase transition.
- ACRT (periodic accelerated/decelerated crucible rotation) is used in this context primarily to homogenize the Se-rich boundary layer at the growth interface and suppress constitutional supercooling that a diffusion-limited, off-stoichiometric solution growth would otherwise be prone to.
- This is presented as a route toward diameters beyond the ~50 mm ceiling that limits vapor-phase methods, motivated by ZnSe's attractiveness for infrared-countermeasure applications, where it offers a wider bandgap and broader transparency than materials such as GaAs.

---

## 4. Comparative Summary

| Method | Typical growth rate | Typical scale | Main strength | Main limitation |
|---|---|---|---|---|
| Self-seeded / seeded PVT | ~1.9–3 mm/day (furnace translation) | Bulk boules, ≲ 50 mm diameter | High crystalline perfection (aside from twins); low impurity levels achievable | Slow; diameter-limited; Se-partial-pressure/stoichiometry drift during growth |
| CVT (I₂ transport) | Governed by transport-agent partial pressures | Small-to-moderate boules/substrates | Lower source temperature than PVT; thermodynamically well modeled | Halogen incorporation; still diameter-limited |
| Vertical Bridgman (Ar overpressure, stoichiometric melt) | 0.8–4 mm/h (twin-free window) | Up to ~25 mm diameter demonstrated | Faster than vapor growth; can be twin-free with correct seed angle/rate | Narrow process window vs. {111} orientation and rate; near-$T_m$ phase transition risk |
| Closed double-crucible Bridgman | ~3.6 mm/h | Larger, reproducible twin-free boules | Composition control decouples growth interface from bulk melt drift | Requires precise overheat (+76 K) and 30 K/cm gradient control |
| High-pressure Bridgman / HPVZM | Process-dependent | Tapes up to 120×120×12 mm | Large-area plate geometry; very high resistivity achievable | Inclusion (bubble) control tied tightly to stoichiometry |
| ACRT-HPB, Se-rich melt-solution | Process-dependent | Aimed at >50 mm diameter | Avoids the 2H↔3C transition entirely by lowering process temperature | Off-stoichiometric solution growth chemistry adds its own segregation/impurity considerations |

---

## 5. Key Process-Design Takeaways

- **Stoichiometry control is the unifying challenge** across every method: incongruent vaporization (vapor growth) and incongruent melting/segregation (melt growth) both push the growing crystal off the ideal 1:1 Zn:Se ratio unless actively managed (source pretreatment in PVT; double-crucible or off-stoichiometric solution design in melt growth).
- **The 2H↔3C phase transition ~100 °C below $T_m$** is the single largest obstacle to twin-free melt-grown ZnSe, and essentially all successful melt-growth strategies are, implicitly or explicitly, strategies for managing or avoiding this transition (orientation selection relative to {111} in standard Bridgman; lowering the process temperature below the transition in ACRT-HPB Se-rich growth).
- **Growth-axis/seed orientation relative to (111)** is as important a lever as thermal gradient or pull rate for suppressing low-angle grain boundaries and twins in Bridgman growth.
- **Vapor methods remain the reference for crystalline/optical quality and purity** (GDMS, PL, SWBXT, HRTXD data all point to very high perfection in contactless-grown regions), but are capped near 50 mm in useful diameter, which is why melt-growth variants continue to be developed for large-aperture optics and IR components.

---

*Compiled from published crystal-growth literature (NASA NTRS reports, ScienceDirect, ACS Crystal Growth & Design, SPIE proceedings, and DOE/OSTI reports) on ZnSe physical/chemical vapor transport and Bridgman melt growth.*
