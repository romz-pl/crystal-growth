# Growth of CdSe Single Crystals

## 1. Material Background

Cadmium selenide (CdSe) is a II–VI compound semiconductor with a direct band gap of approximately $1.74\ \text{eV}$ at room temperature, making it important for optoelectronics, photodetectors, solar cells, and — in nanocrystal form — quantum dot applications. Bulk CdSe crystallises in two polymorphs:

- **Wurtzite (hexagonal, $P6_3mc$)** — the thermodynamically stable phase at ambient pressure, the form obtained in essentially all melt- and vapor-grown bulk boules.
- **Zinc blende (cubic, $F\bar{4}3m$)** — metastable, typically only accessible in thin films or nanostructures grown under kinetic (low-temperature) control.

CdSe melts congruently at approximately $1350\ \text{K}$ ($\sim 1077\ ^\circ\text{C}$), but this melting point sits close to the point where Cd and Se partial vapor pressures become extremely large — this is the central complication that drives crystal growers toward vapor-phase and sealed-ampoule methods rather than open-melt techniques like Czochralski.

## 2. Why CdSe Is a Difficult Melt-Growth Candidate

Three material properties dominate process selection:

1. **High dissociation vapor pressure.** Near the melting point, CdSe partially dissociates into Cd and $\text{Se}_2$ vapor, with total pressures reaching several atmospheres. An open-crucible pull (as in conventional Czochralski) would lose stoichiometry through evaporation.
2. **Narrow region of existence.** The homogeneity range around the stoichiometric composition is narrow; small deviations in the Cd:Se ratio strongly affect native point-defect concentration (Cd or Se vacancies/interstitials), and hence electrical and optical properties.
3. **Low thermal conductivity and high thermal expansion anisotropy** (hexagonal structure) — this makes the crystal prone to thermal stress, twinning, and stacking faults if axial and radial gradients are not carefully controlled.

These constraints are the same reasons other II–VI compounds (CdTe, CdZnTe, ZnSe) are grown by sealed or vapor methods rather than by Czochralski.

## 3. Principal Growth Methods

### 3.1 Vertical Bridgman / Vertical Gradient Freeze (VB/VGF) — most common route

This is the dominant technique for producing bulk CdSe boules, following the same rationale used for CdTe and CZT.

**Process outline:**

1. **Charge synthesis.** Stoichiometric (or slightly Cd-rich) elemental Cd and Se are loaded into a fused-silica (quartz) ampoule, which is evacuated and sealed to prevent oxidation and to contain vapor pressure.
2. **Compound synthesis (reaction stage).** The sealed ampoule is heated slowly through the Cd–Se reaction exotherm (well below the melting point first, to avoid a runaway pressure spike from the highly exothermic Cd + Se reaction) and then raised above the CdSe melting point to homogenise the melt.
3. **Directional solidification.** The ampoule (or the furnace, in modern multi-zone systems) is translated through a temperature gradient that straddles the melting point, so the solid–liquid interface sweeps from one end of the ampoule to the other at a controlled rate (typically on the order of a few mm/hour to a few mm/day, depending on diameter and desired defect density).
4. **Overpressure control.** A separate, cooler zone of the ampoule may be held at a controlled temperature to fix the Cd (or $\text{Se}_2$) vapor pressure over the melt — directly analogous to the "cadmium overpressure" method used for CdTe — which stabilizes the melt stoichiometry and suppresses the formation of the second, excess-element phase upon cooling.
5. **Seeding (optional).** A single-crystal seed of known orientation may be placed at the cold end to promote single-grain growth and control crystallographic orientation of the boule.
6. **Post-growth anneal.** The grown boule is annealed under a controlled Cd or Se vapor pressure to homogenise native point defects and reduce precipitate formation.

**Key control parameters:**

$$
G = \left.\frac{dT}{dz}\right|_{\text{interface}}, \qquad v_{\text{growth}} = \frac{dz_{\text{interface}}}{dt}
$$

The ratio $G/v_{\text{growth}}$ governs interface morphological stability (constitutional supercooling criterion) and hence whether growth remains planar or breaks down into cellular/dendritic growth.

### 3.2 Physical Vapor Transport (PVT) / Sublimation Growth

Because CdSe sublimes congruently below its melting point (i.e., the solid can pass directly into a Cd + Se$_2$ vapor mixture that recondenses as CdSe), sublimation-based sealed-ampoule growth is a widely used and often preferred alternative to melt growth, avoiding the highest-pressure regime entirely.

**Process outline:**

1. Polycrystalline CdSe source powder or a pressed/sintered charge is placed at the hot end of a sealed, evacuated ampoule (or a growth cell inside a larger furnace, similar in concept to SiC PVT reactors).
2. The source zone is held at a high temperature $T_{\text{source}}$ (typically $1000\text{–}1150\ ^\circ\text{C}$), causing sublimation into Cd(g) and Se$_2$(g).
3. Vapor diffuses/convects down a temperature gradient to a cooler growth zone held at $T_{\text{growth}} < T_{\text{source}}$, where supersaturation drives recondensation onto a seed crystal or the ampoule wall.
4. The temperature difference $\Delta T = T_{\text{source}} - T_{\text{growth}}$ and the ampoule geometry set the transport flux and hence the growth rate; growth rates are generally slower than melt growth (fractions of a mm/hour) but yield lower thermal stress and dislocation density because the process operates well below the melting point.
5. A residual inert gas (or none, for pure sublimation) may be present to moderate the transport rate.

This is essentially the CdSe analogue of the physical vapor transport process used for SiC and other wide-gap or high-vapor-pressure compounds — differing from *chemical* vapor transport in that no separate transport agent (e.g., halogen) is required, since CdSe's own dissociation products serve as the vapor species.

### 3.3 Chemical Vapor Transport (CVT)

For smaller research-scale single crystals (rather than large boules), CVT with a halogen transport agent (commonly iodine, $\text{I}_2$) is used:

$$
\text{CdSe(s)} + \text{I}_2\text{(g)} \rightleftharpoons \text{CdI}_2\text{(g)} + \tfrac{1}{2}\text{Se}_2\text{(g)}
$$

The reaction is run in a two-zone sealed quartz ampoule with source and growth zones at different temperatures (typically source $\sim 750\text{–}850\ ^\circ\text{C}$, growth zone tens to ~100 °C cooler, though exact windows are optimised experimentally). The equilibrium is reversible: it proceeds forward at the hot source, and the increase in $\Delta G$ toward the cooler zone drives the reverse reaction, depositing CdSe there. CVT crystals are typically smaller (mm-scale platelets or needles) but useful for detailed physical property studies where boule-scale material is not required.

### 3.4 Solution and Flux Growth (Secondary Route)

Less commonly, CdSe can be grown from a metal-rich flux (e.g., excess Cd, or a low-melting-point solvent) at temperatures well below the compound's own melting point. This reduces vapor pressure problems and thermal stress further, at the cost of slower growth and generally smaller crystal size; it is more common for CdSe nanostructure and thin-crystal synthesis than for bulk boules.

## 4. Comparison of Methods

| Method | Typical growth rate | Max practical size | Main advantage | Main drawback |
|---|---|---|---|---|
| Vertical Bridgman / VGF | mm/hr–day | Boules, cm-scale | Large single crystals, scalable | High vapor pressure near $T_m$, thermal stress, twinning risk |
| Physical Vapor Transport (sublimation) | slow (sub-mm/hr) | cm-scale, thick platelets/boules | Growth below $T_m$ → lower stress/dislocations | Slower; needs long-duration furnace stability |
| Chemical Vapor Transport | very slow | mm-scale | Excellent crystalline quality for small samples | Not scalable to large boules; agent incorporation risk |
| Flux/solution growth | slow | mm–cm | Low-temperature, low-stress process | Solvent inclusion; slower kinetics |

## 5. Post-Growth Characterisation and Treatment

Regardless of route, CdSe boules/crystals are typically:

- **Annealed** under controlled Cd or Se$_2$ vapor pressure to adjust the native defect population (Cd vacancies act as acceptors; Se vacancies/Cd interstitials act as donors), which directly sets resistivity and photoconductive behaviour.
- **Characterised** by X-ray diffraction (confirming wurtzite phase and orientation), optical absorption/photoluminescence (band-edge and defect-level emission), Hall effect (carrier type/concentration/mobility), and etch-pit density or synchrotron topography (dislocation density).
- **Oriented and sliced** (if boule-grown) for wafer production, typically along the $c$-axis or specific low-index planes depending on device application.

## 6. Summary

CdSe growth is governed overwhelmingly by its dissociative vapor pressure near the melting point. This pushes practice toward **sealed-ampoule methods** — vertical Bridgman/VGF for large boules with vapor-pressure (overpressure) control, physical vapor transport for lower-stress bulk growth below the melting point, and chemical vapor transport or flux growth for smaller, very high-quality research crystals. The choice among these mirrors the same trade-offs seen across the II–VI family (CdTe, CdZnTe, ZnSe): melt methods give the largest crystals fastest but at the cost of higher thermal stress and stoichiometry control challenges, while vapor/solution methods trade growth rate for crystalline perfection and stoichiometric precision.
