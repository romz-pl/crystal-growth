# Growth of CdTe: II–VI Semiconductor Crystal Growth Process

## 1. Overview and Motivation

Cadmium telluride (CdTe) is a direct-bandgap II–VI compound semiconductor ($E_g \approx 1.5\ \text{eV}$ at room temperature) used as a substrate for HgCdTe (MCT) infrared detector epitaxy, as an absorber material in thin-film photovoltaics, and as the base material for room-temperature nuclear radiation detectors (CdTe and CdZnTe, CZT). Bulk single-crystal growth of CdTe is notoriously difficult compared with elemental or III-V semiconductors because of:

- A high equilibrium vapor pressure of Cd and Te$_2$ over the melt, requiring sealed/pressurized ampoules.
- A narrow homogeneity range and strong deviation from stoichiometry, producing native point defects (Cd vacancies, Te antisites, interstitials) that act as electrically active centers.
- Low critical resolved shear stress and low thermal conductivity, making the crystal prone to plastic deformation and dislocation generation under the thermal stresses inherent to melt growth.
- A tendency to twin on {111} planes during solidification.

Because of these difficulties, several distinct growth strategies have been developed, spanning melt growth, solution growth, and vapor growth.

---

## 2. Melt Growth Techniques

### 2.1 Bridgman and Vertical Gradient Freeze (VGF) Growth

The dominant industrial method for bulk CdTe (and CdZnTe) is the vertical Bridgman (VB) or vertical gradient freeze technique, generally performed inside a sealed, thick-walled quartz ampoule.

**Process sequence:**

1. **Charge synthesis.** High-purity (6N–7N) elemental Cd and Te are loaded into a quartz ampoule, evacuated to $\sim 10^{-6}$ Torr, and sealed. The ampoule is heated in a rocking or vertical furnace above the CdTe melting point ($T_m \approx 1092^\circ\text{C}$) to synthesize the compound directly from the elements, with careful temperature ramping to control the exothermic reaction and avoid ampoule rupture from the Cd overpressure.
2. **Ampoule design.** A conical or hemispherical tip is used to promote single-nucleus formation; some processes use a seed crystal placed at the tip to control crystallographic orientation.
3. **Translation/gradient-freeze.** In VB, the ampoule is slowly translated (typically 1–10 mm/day) through a fixed axial temperature gradient (typically 1–5 K/cm near the melting point) so the solid–liquid interface sweeps upward through the melt. In VGF, the ampoule remains stationary and the furnace temperature profile is ramped down electronically, achieving an equivalent effect without moving parts, reducing vibration-induced striations.
4. **Interface shape control.** The axial and radial temperature gradients are tuned (often modeled with codes such as CGSim or FEMAG-CZ) to keep the growth interface as flat or slightly convex (toward the melt) as possible, since a concave interface promotes constitutional supercooling and stray nucleation, while an excessively convex interface increases radial thermal stress and dislocation density.
5. **Overpressure control.** Because Cd vapor pressure over the melt can exceed several atmospheres near $T_m$, either (a) a fully sealed ampoule with a calculated Cd reservoir/cold-zone is used to fix the partial pressure and hence the stoichiometry, or (b) an inert gas overpressure (high-pressure Bridgman, HPB) counter-balances the internal vapor pressure, allowing thinner-walled ampoules and reduced risk of explosive failure.
6. **Post-growth stoichiometry annealing.** After solidification, the boule is annealed in a controlled Cd- or Te-rich vapor atmosphere at $600$–$800^\circ\text{C}$ for extended periods (days to weeks) to homogenize the native point-defect population and adjust electrical resistivity toward semi-insulating behavior, since as-grown boules are usually far from the ideal stoichiometric point.
7. **Cooldown.** Slow cooling (often <50 K/h) through the temperature range where CdTe is most susceptible to plastic deformation minimizes dislocation multiplication from thermal stress.

**Key process variables:**

| Parameter | Typical range | Effect |
|---|---|---|
| Growth (translation) rate | 1–10 mm/day | Higher rates increase constitutional supercooling risk and defect incorporation |
| Axial gradient at interface | 1–5 K/cm | Higher gradients suppress twinning but increase thermal stress |
| Cd overpressure | up to several atm | Sets melt stoichiometry; controls native defect density |
| Post-growth anneal | 600–800 °C, Cd or Te atmosphere | Adjusts stoichiometry, reduces deep-level defect density |

### 2.2 Traveling Heater Method (THM)

THM is a solution-growth variant particularly favored for detector-grade CdTe/CdZnTe because it operates well below the melting point, reducing thermal stress and impurity incorporation from container walls.

1. A polycrystalline CdTe source rod and a seed crystal are placed at opposite ends of a sealed ampoule, separated by a thin zone of Te-rich solvent (a **Te solvent zone**, since Te-rich CdTe has a strongly depressed liquidus temperature, often around $800$–$900^\circ\text{C}$ versus $1092^\circ\text{C}$ for the pure melt).
2. A narrow, localized heater (the "hot zone") is translated slowly (typically a few mm/day) along the ampoule. At the leading edge of the hot zone, source material dissolves into the Te-rich solvent; at the trailing edge (near the seed), CdTe recrystallizes epitaxially onto the growing crystal as the solvent zone becomes locally supersaturated on cooling.
3. Because the growth temperature is well below $T_m$, thermal gradients and associated stresses are dramatically reduced compared with Bridgman growth, yielding lower dislocation densities and reduced Te-precipitate formation.
4. Growth is extremely slow (the process can take weeks to months for a full boule) because it is diffusion-limited through the thin solvent zone, but this is compensated by superior crystalline quality and compositional homogeneity for detector applications.
5. Segregation of dopants and of the Zn fraction in CdZnTe is governed by the solvent-zone transport; the effective segregation coefficient can be tuned via the growth rate and solvent zone width.

### 2.3 Physical Vapor Transport (PVT) / Sublimation Growth

For applications requiring lower-defect, lower-stress crystals without ever passing through the liquid phase (avoiding melt-related stoichiometric and container-interaction issues):

1. Polycrystalline CdTe source material sublimes at one end of a sealed ampoule held at a source temperature typically $850$–$950^\circ\text{C}$.
2. Vapor species (a mixture of Cd(g) and Te$_2$(g), with the equilibrium $\text{CdTe(s)} \rightleftharpoons \text{Cd(g)} + \tfrac{1}{2}\text{Te}_2\text{(g)}$) are transported down a modest axial gradient and recondense on a cooler seed or nucleation surface, typically 20–50 K below the source temperature.
3. Variants include the **Markov method** and **closed-space sublimation**, differing mainly in ampoule geometry and gradient control.
4. Growth rates are low (sub-mm/day) but the technique is attractive for a purely solid–vapor equilibrium that avoids melt/container contamination and residual thermal-stress dislocations associated with solidification shrinkage.

---

## 3. Thermodynamic and Defect Considerations

The single most distinctive aspect of CdTe growth relative to elemental or III-V crystals is the **partial-pressure–stoichiometry relationship**. The p-T-x phase diagram of the Cd–Te system has a narrow single-phase CdTe field, and the equilibrium Cd partial pressure over the melt or solid varies by orders of magnitude across this field. Consequently:

$$
p_{\text{Cd}} \cdot p_{\text{Te}_2}^{1/2} = K(T)
$$

where $K(T)$ is the temperature-dependent equilibrium constant for the vaporization reaction. Controlling $p_{\text{Cd}}$ (via a dedicated Cd reservoir at a controlled temperature, distinct from the growth zone) fixes the point on the solidus/liquidus at which the crystal is grown, and hence the native defect chemistry: Cd-rich growth favors Te vacancies and reduces Cd-vacancy-related acceptor states, while Te-rich growth favors Cd vacancies ($V_{\text{Cd}}$), which are the dominant deep acceptor responsible for compensating residual donors and enabling semi-insulating behavior needed for detector-grade material.

Post-growth annealing under controlled Cd or Te overpressure is therefore treated as an integral part of the growth process rather than an afterthought, since as-grown stoichiometry rarely matches the electrical specification required by the application (detector-grade high-resistivity material vs. photovoltaic absorber layers vs. low-defect-density substrates).

---

## 4. Defect and Quality Control Issues Specific to CdTe

- **Twinning:** CdTe has a low stacking-fault energy, and {111} twin formation is common, especially at high growth rates or with unfavorable interface curvature. Seed orientation (commonly $\langle 111 \rangle$ or $\langle 100 \rangle$) and careful interface shape control mitigate this.
- **Te inclusions/precipitates:** Non-stoichiometric, Te-rich growth conditions or rapid cooling can trap micrometer-scale Te-rich second-phase precipitates, which are detrimental to detector performance (charge trapping) and are characterized by IR transmission microscopy.
- **Low critical resolved shear stress:** CdTe deforms plastically at relatively low stress, so thermal gradients that would be tolerable in Si or GaAs readily generate dislocations in CdTe; this motivates the lower-gradient THM and PVT approaches for the highest-quality material.
- **Compositional grading in CdZnTe:** When Zn is added (CdZnTe/CZT) to increase bandgap and hardness, the segregation coefficient of ZnTe in CdTe ($k_{\text{ZnTe}} \neq 1$) produces axial compositional gradients along Bridgman-grown boules, requiring either post-growth characterization/rejection zones or specialized growth-rate profiling to flatten the Zn distribution.

---

## 5. Summary Comparison of Growth Methods

| Method | Growth Temp. | Growth Rate | Typical Use | Key Advantage | Key Drawback |
|---|---|---|---|---|---|
| Vertical Bridgman / VGF | ~1092 °C (melt) | mm/day | Bulk substrates, CZT detectors | High throughput, large boules | Higher thermal stress, dislocations, twinning |
| THM | 800–900 °C (solution) | very slow (mm/week) | Detector-grade CdTe/CZT | Low thermal stress, high purity | Very slow, complex solvent-zone control |
| PVT / Sublimation | 850–950 °C (vapor) | sub-mm/day | Research-grade, low-defect crystals | No melt/container interaction | Slow, small boules |

---

## 6. Representative Process Flow (Bridgman/VGF)

1. Elemental synthesis of CdTe charge in sealed ampoule
2. Ampoule design with seed pocket/conical tip
3. Melt homogenization above $T_m$
4. Controlled translation/gradient-freeze through the melting point under fixed axial gradient
5. In-situ Cd overpressure control via reservoir zone
6. Slow post-growth cooldown
7. Post-growth stoichiometry annealing (Cd- or Te-rich atmosphere, 600–800 °C)
8. Wafering, characterization (IR transmission, etch-pit density, resistivity mapping), and rejection of twinned/defective regions
