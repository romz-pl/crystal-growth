# Growth of AlAs (Aluminium Arsenide): A Detailed Process Description

## 1. Material Overview

Aluminium arsenide (AlAs) is a III-V compound semiconductor with the zinc-blende crystal structure (space group $F\bar{4}3m$), lattice constant $a \approx 5.6611\ \text{\AA}$ at 300 K — nearly lattice-matched to GaAs ($a \approx 5.6533\ \text{\AA}$), which is the single most important fact governing how AlAs is grown and used. It is an indirect-bandgap semiconductor ($E_g \approx 2.16$ eV, indirect, at 300 K), and it is chemically far more reactive than GaAs: exposure to ambient moisture rapidly oxidizes AlAs surfaces, forming arsenic oxides and, eventually, a friable, whitish hydrolysis product. This reactivity has a first-order effect on growth strategy: bulk single-crystal AlAs boules are essentially never grown and used directly (unlike GaAs, InP, or GaSb), because as-grown material degrades before it can be processed. Essentially all technologically useful AlAs is grown as **thin epitaxial layers**, almost always as part of an AlAs/GaAs or AlGaAs/GaAs heterostructure, capped in situ before air exposure.

This description therefore covers:
1. Why bulk melt growth is impractical for AlAs, and what it would require in principle.
2. The dominant real-world route: epitaxial growth (MBE and MOVPE) of AlAs layers and AlAs/GaAs superlattices/DBRs.
3. Growth physics, kinetics, and defect/quality control issues specific to AlAs.

---

## 2. Why Bulk (Melt) Growth Is Impractical

For congruent or near-congruent III-V compounds such as GaAs, InP, or GaSb, standard melt techniques (Liquid-Encapsulated Czochralski, Vertical Gradient Freeze, Horizontal Bridgman) are viable because:

- The compound melts congruently (or close to it) at an accessible temperature.
- The equilibrium overpressure of the volatile group-V species can be contained (e.g., using a $\text{B}_2 \text{O}_3$ encapsulant in LEC, or a sealed ampoule in VGF/Bridgman).
- The solidified crystal is chemically stable enough to survive dicing, polishing, and device processing in air.

AlAs fails on essentially all three counts:

- **Melting point and dissociation pressure**: AlAs melts at approximately 1740–1770°C (reported values vary; it is considerably higher than GaAs's 1238°C), and at these temperatures the As partial pressure at the congruent melting composition is extremely high, driving strong dissociative As loss unless very high overpressures or heavy encapsulation are used.
- **Encapsulant chemistry**: The $\text{B}_2 \text{O}_3$ encapsulant used successfully in GaAs LEC growth is far more reactive with molten Al than with Ga; Al reduces $\text{B}_2 \text{O}_3$, contaminating the melt with boron and destabilizing the encapsulant layer. This removes the standard LEC route.
- **Post-growth stability**: Even if a boule were grown, AlAs's rapid hydrolysis in humid air makes wafering, lapping, and polishing with conventional aqueous slurries essentially self-destructive to the material.

For these reasons, no commercial bulk AlAs crystal growth industry exists analogous to bulk GaAs or InP. The dimensionless-group framework and continuum melt models (Grashof, Marangoni, Prandtl numbers; rotational Ekman/Taylor numbers; radiative Boltzmann number) that govern CZ/Bridgman growth of other III-Vs are, in principle, transferable to a hypothetical AlAs melt system, but they are not exercised in practice because no viable containment/encapsulation scheme has been demonstrated at scale.

A small research literature exists on **high-pressure Bridgman-type or solution growth of AlAs and Al-rich AlGaAs bulk crystals** under inert, sealed, high-pressure ampoule conditions (to suppress dissociation), but these remain laboratory curiosities rather than a production technology.

---

## 3. The Dominant Route: Epitaxial Growth

AlAs is grown essentially exclusively as an epitaxial layer on GaAs (or occasionally Ge) substrates, using either **Molecular Beam Epitaxy (MBE)** or **Metal-Organic Vapor Phase Epitaxy (MOVPE, also called MOCVD)**. The near-perfect lattice match to GaAs (mismatch $< 0.15\%$) means AlAs and $\text{Al} _x \text{Ga} _{1-x} \text{As}$ alloys of any composition $x$ can be grown pseudomorphically on GaAs with negligible strain, to essentially unlimited thickness — this is the material-science foundation of the entire AlGaAs/GaAs heterostructure device family (HBTs, HEMTs, DBR mirrors in VCSELs, DHBTs, quantum well lasers).

### 3.1 Molecular Beam Epitaxy (MBE)

**Principle**: Ultra-high vacuum (UHV, $\sim 10^{-10} - 10^{-11}$ torr base pressure) physical deposition. Elemental Al and As (and Ga, for AlGaAs/GaAs heterostructures) are evaporated from separate effusion (Knudsen) cells and impinge as molecular/atomic beams onto a heated GaAs substrate.

**Key process steps**:

1. **Substrate preparation**: Epi-ready GaAs wafer, native-oxide desorption in vacuum at $\sim 580$–$630°C$ under As overpressure (monitored by RHEED — Reflection High-Energy Electron Diffraction — pattern transition from diffuse to streaky/spotty, indicating oxide removal and surface reconstruction).
2. **Buffer layer**: A homoepitaxial GaAs buffer ($\sim 100 - 500$ nm) is grown first to bury substrate defects and re-establish a smooth, well-reconstructed surface before switching to AlAs.
3. **AlAs growth proper**: Substrate held at $580 - 630°C$ (similar to GaAs, sometimes slightly higher to compensate for Al's lower surface mobility). Al flux and $\text{As}_4$ (or cracked $\text{As}_2$) flux are set so that growth proceeds in the **As-stable, group-III-limited regime**: growth rate is set by the arrival rate of Al atoms (typically calibrated to $\sim 0.5 - 1.0$ monolayer/s, i.e., roughly 0.3–1 $\mu$ m/hr), with As supplied in modest excess (As:Al beam-equivalent-pressure ratio typically 1.5–3×) to saturate the surface with As and suppress Al droplet formation, while avoiding a large enough excess to degrade surface morphology or incorporate excess As as point defects.
4. **Shuttering for heterostructures**: Because AlAs is almost always grown as part of an AlAs/GaAs multilayer (superlattice, DBR, quantum well barrier), the Al and Ga shutters are opened/closed with sub-second precision to define abrupt heterointerfaces; growth interrupts (brief pauses with shutters closed, under As flux) are sometimes used at each interface to allow surface adatoms to reach equilibrium sites and improve interface abruptness/smoothness, monitored via RHEED intensity oscillations (each oscillation period = one monolayer).
5. **In situ monitoring**: RHEED intensity oscillations give absolute growth-rate calibration (monolayers/s) and surface reconstruction (e.g., $(2\times4)$ As-rich reconstruction) confirms the growth regime is correctly As-stabilized.
6. **Doping**: Si (n-type) or Be/C (p-type) effusion cells provide dopants as needed for device layers; for DBR mirrors, AlAs layers are typically left undoped or lightly doped to minimize free-carrier absorption.
7. **Capping**: Because of AlAs's air-sensitivity, any AlAs surface layer that must survive ex situ processing is capped with a thin GaAs layer before the wafer leaves vacuum. Bare AlAs is essentially never exposed to atmosphere in a finished device structure.

**Special case — AlAs sacrificial/release layers**: A widely used application-specific growth mode is the deliberate growth of a thin ($\sim 10 - 100$ nm) AlAs layer as a **selectively-etchable sacrificial layer** beneath a GaAs (or AlGaAs) device layer, exploiting the fact that dilute HF solutions etch AlAs orders of magnitude faster than GaAs or low-Al-content AlGaAs. This is the basis of **epitaxial lift-off (ELO)** processes used to transfer thin-film devices (solar cells, LEDs, membranes) onto foreign substrates. Growth conditions for this layer are essentially the standard AlAs conditions above, with attention paid to layer uniformity and interface quality since the etch selectivity and mechanical release depend on it.

### 3.2 Metal-Organic Vapor Phase Epitaxy (MOVPE / MOCVD)

**Principle**: Chemical vapor deposition at near-atmospheric or reduced pressure ($\sim 20 - 760$ torr), in a horizontal or vertical reactor with a rotating, heated (typically $650$–$750°C$) susceptor. Trimethylaluminium (TMAl) and arsine (AsH$_3$), or safer arsine alternatives (e.g., tertiarybutylarsine, TBAs), are transported in a H$_2$ (or N$_2$) carrier gas and pyrolyze at the hot substrate surface.

**Key process steps**:

1. **Reactor and susceptor preparation**: Substrate loaded, purged, and heated to growth temperature under an AsH$_3$/H$_2$ (or TBAs/H$_2$) ambient to prevent As loss from the GaAs surface during ramp-up.
2. **Growth chemistry**: TMAl pyrolyzes at relatively low temperature and is highly reactive with oxygen and moisture — background O$_2$/H$_2$O contamination is the dominant source of oxygen incorporation into AlAs and AlGaAs layers, causing deep-level traps (the classic "DX center" and oxygen-related non-radiative recombination problems historically associated with MOVPE-grown AlGaAs). This makes **reactor and gas-line purity control** (point-of-use purifiers on carrier gas, ultra-dry TMAl source, load-lock/glovebox wafer handling) the single most critical practical issue in MOVPE AlAs growth, more so than for GaAs.
3. **V/III ratio**: Typically high (tens to $\sim 100$), since AsH$_3$ pyrolysis efficiency is lower than the metal-organic decomposition efficiency, and excess As overpressure suppresses Al-droplet/metallic defects and As antisite-related issues.
4. **Growth rate and temperature window**: Growth is normally run in the mass-transport-limited regime (rate set by group-III precursor delivery, largely temperature-insensitive over a wide window), typically $650$–$750°C$, at rates of order 1–5 $\mu$m/hr, matched to the paired GaAs growth conditions for heterostructure consistency.
5. **Interruption/switching for heterostructures**: As in MBE, digital switching of TMAl vs. trimethylgallium (TMGa) flows, with the AsH$_3$/TBAs flow held continuous, defines the AlAs/GaAs interfaces; MOVPE interfaces are generally somewhat less abrupt than MBE due to gas-switching transients and precursor memory effects in the reactor.
6. **Doping**: Analogous n-type (Si, from silane or disilane) and p-type (C, often from CCl$_4$ or intentionally from the TMAl/TMGa carbon background; Zn from DEZn) sources are used as required.

### 3.3 Comparison of the Two Routes

| Aspect | MBE | MOVPE |
|---|---|---|
| Environment | UHV, physical deposition | Near-atmospheric, chemical (pyrolytic) deposition |
| Growth temperature | $580$–$630°C$ | $650$–$750°C$ |
| Growth rate | $0.3 - 1\ \mu$m/hr | $1 - 5\ \mu$m/hr |
| Interface abruptness | Excellent (sub-monolayer, shutter-limited) | Good, but limited by gas-switching transients |
| Oxygen/carbon contamination risk | Low (UHV) but Al is highly reactive to any residual $\text{O}_2$ / $\text{H}_2 O$ | Higher — TMAl is very oxygen/moisture-sensitive; historically the dominant AlGaAs quality issue |
| In situ diagnostics | RHEED (real-time monolayer control) | Reflectance/ellipsometry-based, less direct |
| Typical application | DBRs, HEMTs, research heterostructures, precision quantum wells | High-volume LED/laser production, thicker device structures |

---

## 4. Growth Kinetics and Surface Physics Specific to AlAs

- **Lower Al adatom surface mobility**: Al adatoms diffuse more sluggishly on the growing surface than Ga adatoms at a given temperature, which tends to produce slightly rougher AlAs (and high-Al-content AlGaAs) surfaces/interfaces than pure GaAs under otherwise matched conditions. This is compensated in practice by growing AlAs at somewhat higher substrate temperature than the GaAs layers in the same heterostructure, or by inserting growth interrupts at heterointerfaces to allow adatom migration to equilibrium terrace sites.
- **As-stabilized growth regime**: As with GaAs, AlAs is grown under group-V-rich conditions (As:Al ratio kept in excess) to stay in the As-stable RHEED reconstruction regime and avoid metallic Al droplet formation, which would otherwise nucleate under Al-rich conditions and create haze/defects.
- **Strain**: Essentially zero, given the $<0.15\%$ lattice mismatch to GaAs — this is what permits arbitrarily thick AlAs layers and AlAs/GaAs superlattices (e.g., 20–40+ period DBR stacks for VCSEL mirrors) without misfit dislocation generation, in sharp contrast to strained systems like InGaAs/GaAs.
- **Oxidation kinetics as a *process step***: A distinctive feature of AlAs (not shared with GaAs) is that its rapid, selective oxidizability is deliberately *exploited* rather than merely tolerated. Wet thermal oxidation of AlAs (typically at $350$–$450°C$ in a N$_2$/H$_2$O steam ambient) converts AlAs into a low-refractive-index, insulating amorphous aluminium oxide, at a rate strongly dependent on Al mole fraction — this **selective lateral wet oxidation of a buried AlAs (or Al$_x$Ga$_{1-x}$As, $x$ near 1) layer** is the standard method for forming the current-confining oxide aperture in commercial VCSELs. So while bare AlAs's instability is a liability for bulk crystal growth, it is turned into the key functional mechanism of one of AlAs's most important applications.

---

## 5. Defect and Quality Considerations

- **Oxygen incorporation**: The most significant extrinsic defect issue, especially in MOVPE and in any AlAs surface briefly exposed to residual O$_2$/H$_2$O in the growth chamber; oxygen-related deep levels degrade minority-carrier lifetime and are historically linked to the DX-center behavior seen in Si-doped AlGaAs of high Al content.
- **Carbon incorporation**: From metal-organic precursor ligands in MOVPE; usually low but must be controlled, particularly for intentionally undoped high-purity layers.
- **Interface abruptness/roughness**: Governed by adatom mobility and growth-interrupt strategy, as above; critical for DBR reflectivity spectra and quantum-well confinement energies.
- **Post-growth handling**: Any process step exposing AlAs to ambient humidity (dicing, wet etching not intended to target the AlAs, storage) must be minimized or eliminated by design — devices are engineered so that AlAs layers are always buried beneath a stable cap (GaAs or high-Ga-content AlGaAs) except where oxidation or selective etching is the intended functional step.

---

## 6. Summary

AlAs is a textbook case of a III-V compound whose growth technology is dictated less by classical melt thermodynamics and more by chemical reactivity: incongruent, high-pressure, boron-incompatible melt behavior rules out bulk Czochralski/Bridgman-type production, so essentially all AlAs is grown as a thin epitaxial layer — by MBE for maximum interface precision (DBRs, quantum structures, research heterostructures) or MOVPE for higher-throughput production — always pseudomorphically on GaAs, always as part of a heterostructure, and always either buried beneath a protective cap or deliberately exposed only where its selective wet-oxidation or selective wet-etch behavior is the intended device mechanism (VCSEL oxide apertures, epitaxial lift-off release layers).
