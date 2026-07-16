# Growth of CdS Single Crystals

Cadmium sulfide (CdS) is a II–VI compound semiconductor with a direct bandgap of $E_g \approx 2.42\ \text{eV}$ at room temperature. It crystallizes preferentially in the hexagonal wurtzite structure (though a metastable cubic zinc-blende phase also exists), and is used in photoconductors, photodetectors, thin-film solar-cell window layers (CdS/CdTe, CdS/CIGS), scintillators, and nonlinear-optical/acousto-optic devices. Because CdS has a very high melting point (~1750 °C at elevated pressure) and dissociates/sublimes rather than melting congruently at atmospheric pressure, its bulk single-crystal growth is dominated by **vapor-phase methods**, with melt growth used only under specialized high-pressure conditions.

This document summarizes the principal growth routes, the physics governing each, and typical process parameters.

---

## 1. Why CdS Is Vapor-Grown

At atmospheric pressure, CdS sublimes/dissociates before reaching a stable liquid phase:

$$
\text{CdS(s)} \;\rightleftharpoons\; \text{Cd(g)} + \tfrac{1}{2}\text{S}_2\text{(g)}
$$

The equilibrium vapor pressure over solid CdS becomes appreciable (Torr range) only above roughly 900–1000 °C, and true congruent melting requires an imposed inert-gas or self-generated overpressure exceeding ~100 atm near 1750 °C. Consequently:

- **Physical Vapor Transport (PVT)**, a sublimation–recondensation process in a sealed or semi-sealed ampoule, is the dominant industrial and laboratory method.
- **High-pressure melt techniques** (Bridgman/Kyropoulos-type, under inert-gas overpressure) are used less commonly, mainly for research-scale boules, because of the high pressures and specialized containment required.
- **Solution growth** (hydrothermal, flux) and **epitaxial** methods (MOCVD, CVD, PLD) are used for thin films and are outside the scope of *bulk single crystal* growth but are mentioned briefly for completeness.

---

## 2. Physical Vapor Transport (PVT) Growth

### 2.1 Principle

PVT is a self-sublimation process: polycrystalline CdS source material is placed at the hot end of a sealed (or semi-closed) ampoule; the seed or nucleation region sits at the cooler end. A temperature gradient $\nabla T$ drives sublimation at the source, diffusive/advective vapor transport of Cd and S₂ species along the ampoule, and recondensation at the cooler seed, where the crystal grows atom-by-atom.

Schematically:

$$
\text{CdS(s, source, } T_{\text{source}}) \;\longrightarrow\; \text{Cd(g)} + \tfrac{1}{2}\text{S}_2\text{(g)} \;\xrightarrow{\text{transport}}\; \text{CdS(s, crystal, } T_{\text{seed}})
$$

with $T_{\text{source}} > T_{\text{seed}}$.

### 2.2 Ampoule Configuration

A typical vertical PVT setup for large CdS boules (following configurations reported for industrial-scale growth) consists of:

- A **sealed or semi-closed vertical quartz (fused silica) ampoule**, evacuated and back-filled with a small partial pressure of an inert gas (e.g., Ar) or left near-vacuum.
- A **two-zone (or multi-zone) resistance furnace** providing independently controlled source and growth-zone temperatures.
- **Source charge**: high-purity (typically 5N–6N) polycrystalline CdS powder or sintered pellets.
- **Growth/seed zone**: either a spontaneously nucleated cone (unseeded) or an oriented CdS seed crystal.
- In refined "semi-closed tube" designs, **multiple thin internal tubes** are used to enforce quasi-one-dimensional diffusion–advection transport rather than uncontrolled multi-directional convective transport, which suppresses parasitic nucleation and improves crystal quality (reported FWHM of X-ray rocking curves around 58.5 arcsec for optimized configurations).

### 2.3 Typical Process Parameters

| Parameter | Typical range |
|---|---|
| Source zone temperature | ~1050–1150 °C |
| Seed/growth zone temperature | ~950–1050 °C |
| Axial temperature gradient | ~1–10 °C/cm |
| Ambient/inert gas pressure | near-vacuum to a few hundred Torr |
| Growth duration | days to a few weeks, depending on boule size |
| Growth rate | typically tens of μm/h to ~mm/day, pressure- and gradient-dependent |

The **total ambient pressure** strongly affects the growth rate: at very low pressure, transport is limited primarily by diffusion (rate scales with the Cd and S₂ partial-pressure gradient divided by total pressure); at higher inert-gas backpressure, diffusive transport is retarded (Stefan-flow suppression), giving a maximum in growth rate at some intermediate/optimal pressure. Empirical growth-rate correlations of the form

$$
\dot{m} \;\propto\; \frac{D_{\text{eff}}(T,P)\,\Delta p}{P\, L}
$$

(with $D_{\text{eff}}$ the effective vapor diffusivity, $\Delta p$ the partial-pressure driving force between source and growth zone, $P$ the total ambient pressure, and $L$ the source–seed separation) have been shown to reasonably predict experimental growth rates and to allow estimation of maximum practical growth time before the source charge is depleted.

### 2.4 Transport Mechanisms

Three sub-mechanisms are generally distinguished in vapor growth of compounds like CdS:

1. **Sublimation transport** — the solid sublimes directly to its constituent (or associated) vapor species, which recondense at the sink to reform the same solid composition.
2. **Decomposition–sublimation transport** — the source decomposes into gaseous species of different stoichiometry than the solid, which then react/recombine at the growth front to deposit the original compound.
3. **Auto-transport** — vapor species generated at the source undergo gas-phase or surface reactions en route that regenerate the transport agent, self-sustaining the process without an externally added transport agent.

CdS PVT growth is generally treated as decomposition–sublimation transport, since the vapor is dominated by monatomic Cd and diatomic S₂ rather than molecular CdS vapor.

### 2.5 Defect and Stoichiometry Control

- **Cd/S stoichiometry deviations** during growth are the dominant source of native point defects: **sulfur vacancies** ($V_S$) act as shallow donors and are associated with characteristic photoluminescence emission near 2.0–2.1 eV in Cd-rich ("dark-type") crystals; more nearly stoichiometric or S-rich growth produces "clear-type" crystals with reduced native-defect luminescence.
- Post-growth **annealing under a controlled Cd, S, or Se overpressure** is commonly used to homogenize stoichiometry, passivate vacancy-related defects, and tune the resistivity (as-grown PVT CdS typically shows medium resistivity in the $10^6$–$10^8\ \Omega\cdot\text{cm}$ range).
- **Parasitic/multiple nucleation** at the growth front is the main quality-limiting issue in large-diameter ampoules; it is controlled by (i) restricting the ampoule to a small, well-defined nucleation zone or a single oriented seed, (ii) using guide tubes or baffles to enforce 1D vapor flow, and (iii) carefully shaping the axial temperature profile (sometimes with a locally *inverted* gradient near the nucleation region, analogous to strategies used in PVT growth of other wide-gap sublimating compounds such as AlN and SiC) to suppress spontaneous nucleation everywhere except at the intended growth front.

---

## 3. High-Pressure Melt Growth (Bridgman / Kyropoulos-type)

For applications requiring larger, more nearly stoichiometric single crystals with lower dislocation density than typical PVT boules, melt growth under high inert-gas overpressure is used, analogous to techniques developed for other II–VI compounds (CdTe, CdZnTe):

- CdS is loaded into a crucible (commonly pyrolytic BN or coated silica, chosen to minimize melt–crucible wall adhesion and wall nucleation) inside a high-pressure vessel.
- An **inert gas overpressure** (order of tens to ~100 atm) is applied to suppress dissociative sublimation and stabilize the liquid phase at the melting point.
- The charge is melted and then directionally solidified using a **vertical Bridgman-type** temperature profile (crucible or furnace translated through a fixed axial gradient), or, less commonly for CdS, Kyropoulos-type crystal pulling from an overpressured melt.
- A **large axial temperature gradient** promotes favorable (concave or near-planar) solid–liquid interface shape and larger grain size; forced or accelerated crucible rotation (ACRT) can be used to enhance melt mixing and reduce compositional segregation, at the cost of potentially deflecting the growth interface via Taylor–Görtler-type instabilities at the crucible sidewall.

Because of the severe pressure and containment requirements and the tendency toward twinning/grain formation in earth-based melt growth of chalcogenide II–VI compounds, high-pressure melt growth of CdS remains a specialized, lower-throughput route compared with PVT, and is used primarily for research ingots rather than production-scale material.

---

## 4. Other Growth Routes (Brief Overview)

| Method | Regime | Typical use for CdS |
|---|---|---|
| **Hydrothermal / solvothermal growth** | Solution, moderate T & P | Bulk single crystals with low defect density, slower growth |
| **Chemical vapor transport (CVT)** | Vapor, with added transport agent (e.g., I₂) | Enhances transport rate/control vs. pure sublimation PVT |
| **Melt growth under inert overpressure (Bridgman/Kyropoulos)** | Melt | Large-grain research boules |
| **Thin-film epitaxy** (CVD, MOCVD, sputtering, PLD, CBD) | Vapor/solution, thin film | Photovoltaic window layers, not bulk crystals |

---

## 5. Summary of Process Selection

- **PVT (sublimation–recondensation in a sealed/semi-closed ampoule)** is the standard method for bulk CdS single crystals, offering a mature, moderate-temperature (~1000–1150 °C), moderate-pressure process well suited to producing boules for detector, photoconductor, and optical applications.
- **High-pressure melt growth** offers potentially larger, more homogeneous crystals but at substantially higher process complexity and cost, and is used mainly in specialized research contexts.
- Across both routes, the central engineering challenges are (i) controlling the Cd:S stoichiometry of the growing crystal, (ii) suppressing parasitic nucleation to obtain single-domain boules, and (iii) managing the vapor/melt transport physics (diffusion, convection, or induced flows) to achieve a stable, well-shaped growth interface.

---

## References

1. Cheng, H. J.; Xu, Y. K.; Yang, W.; Yu, X. L.; Yan, R. Y.; Lai, Z. P. *Growth of CdS crystals by the physical vapor transport method.* J. Semicond. **2009**, 30(10), 103002.
2. *Growth rate of CdS by vapor transport in a closed ampoule.* J. Cryst. Growth (ScienceDirect).
3. *Self-selecting vapor growth of transition metal halide single crystals* (background on PVT/CVT/auto-transport mechanisms). arXiv:2211.07806.
4. *The Physical Vapor Transport Method for Bulk AlN Crystal Growth* (background on PVT nucleation control strategies applicable across sublimating wide-gap compounds). PMC6515034.
5. *CdTe synthesis and crystal growth using the high-pressure Bridgman technique* — background on high-pressure Bridgman methodology for II–VI compounds. ScienceDirect / OSTI 1596252.
6. *CdTe and CdZnTe Crystal Growth and Production of Gamma Radiation Detectors.* arXiv:1612.09571.
