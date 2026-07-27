# AXT, Inc.: A Vertically Integrated Compound Semiconductor Materials Enterprise — A Technical Review

**A graduate-level industrial technical review of raw-material purification, bulk melt crystal growth, wafering, epitaxy, and downstream device applications**

---

## Preface and Epistemic Framework

This report distinguishes three categories of claim throughout, marked inline:

- **[PUBLIC]** — Directly documented in AXT SEC filings (10-K, 10-Q, 8-K), company investor presentations, press releases, or peer-reviewed literature authored by AXT scientists.
- **[INFERENCE]** — A reasonable engineering inference from public information, general compound-semiconductor process physics, and patent literature, but not explicitly confirmed by AXT.
- **[PROPRIETARY/UNKNOWN]** — Information that is either explicitly withheld by AXT as a trade secret, or for which no public documentation exists (exact thermal profiles, dopant concentrations, crucible geometries, seed orientation protocols, etc.).

AXT does not publish detailed process recipes; the specific engineering of its Vertical Gradient Freeze (VGF) furnaces, dopant schedules, and thermal-gradient control algorithms constitutes protected intellectual property and trade secrets. This report reconstructs the physically necessary unit operations from the public record and from the general metallurgy/crystal-growth literature on III–V and IV-group melt growth, while explicitly flagging where AXT's proprietary execution deviates from — or merely resembles — textbook VGF/LEC/Czochralski practice.

---

## 1. Corporate and Industrial Overview

### 1.1 Identity and Structure **[PUBLIC]**

AXT, Inc. (Nasdaq: AXTI), headquartered in Fremont, California, is a materials science company — not a device manufacturer — that designs, grows, and finishes bulk single-crystal compound and elemental semiconductor substrates. AXT explicitly states it does *not* design or manufacture integrated circuits or optoelectronic chips; its product is the substrate wafer upon which epitaxial device layers are subsequently grown by its customers (or by third-party epi houses).

AXT's core substrate materials are:

| Material | Symbol | Crystal class | AXT growth method |
|---|---|---|---|
| Gallium arsenide | GaAs | Zinc-blende III–V compound | Vertical Gradient Freeze (VGF) |
| Indium phosphide | InP | Zinc-blende III–V compound | VGF (originally also LEC via Crystacomm) |
| Germanium | Ge | Diamond-cubic Group IV element | VGF |

Historically AXT also introduced gallium nitride (GaN) substrate offerings, though GaN is a minor product line relative to GaAs/InP/Ge.

### 1.2 Manufacturing Footprint **[PUBLIC]**

AXT manufactures essentially all of its substrate and raw-material product in the People's Republic of China, citing favorable facility and labor costs relative to the US, Europe, or Japan. Its principal manufacturing operations include:

- **Beijing (Tongzhou district)** — legacy site; InP crystal growth and wafer processing.
- **Kazuo, Liaoning Province** — GaAs crystal growth; co-located raw-material joint ventures (BoYu, JinMei).
- **Dingxing, Hebei Province** — newer, large-scale, purpose-built high-volume manufacturing facility.
- **Tongmei manufacturing complex** (Beijing suburb) — described by AXT as roughly 300,000 sq ft across eight buildings, which the company describes as the world's largest III–V wafer production facility.

AXT's principal operating subsidiary, **Beijing Tongmei Xtal Technology Co., Ltd.**, has itself pursued a STAR Market (Shanghai) listing process, indicating a degree of operational and financial separation of the China manufacturing entity from the US-listed parent — a structurally important detail for understanding AXT's corporate architecture and, more recently, its exposure to Chinese export-control regimes.

### 1.3 The Vertical Integration Thesis **[PUBLIC]**

AXT's central strategic differentiator, repeated consistently across two decades of 10-K filings, is backward integration into raw-material supply through partially owned Chinese subsidiaries and joint ventures (ownership stakes historically ranging from ~10% to 100%, with board representation retained across the raw-material entities). These entities supply:

- Gallium metal at multiple purity grades: 4N (99.99%), 6N, and 7N (99.99999%)
- Arsenic (elemental, multiple purity grades)
- Germanium and germanium dioxide (GeO₂)
- Indium phosphide polycrystalline (poly) starting charge material
- Pyrolytic boron nitride (pBN) crucibles used as the crystal-growth container
- Boron oxide (B₂O₃), used as an encapsulant in some growth configurations
- Quartz (fused silica) ampoule/tubing components
- Scrap-material recycling services

Named joint-venture/subsidiary entities documented in AXT SEC filings include Beijing BoYu Semiconductor Vessel Craftwork Technology Co. (pBN crucibles and pBN-based OLED-related tooling), Nanjing JinMei Gallium Co., ChaoYang JinMei Gallium Co., ChaoYang KaiMei, Beijing Ji-Ya Semiconductor Material Co. ("JiYa"), Xiaoyi XingAn Gallium Co., ChaoYang ShuoMei High Purity Semiconductor Materials Co., and ChaoYang XinMei High Purity Semiconductor Materials Co. This is a genuinely unusual degree of upstream integration relative to peer substrate suppliers (e.g., Freiberger Compound Materials, Sumitomo Electric, Vital Materials), most of whom purchase refined gallium/arsenic/indium on the open market rather than co-owning refiners.

**[INFERENCE]** This structure functions economically as a captive-supplier network: AXT both consumes the joint ventures' output internally and sells surplus production to third parties, giving AXT visibility into upstream pricing and availability — materially significant given that gallium and germanium are both List-designated "critical minerals" subject to Chinese export licensing since 2023, and China dominates global refined gallium and germanium supply.

---

## 2. Raw Material Purification: From Ore to Electronic-Grade Feedstock

### 2.1 Why Purity Matters

Compound semiconductor device performance is exquisitely sensitive to unintentional impurities and native point defects. Deep-level trap states from transition-metal contaminants (Fe, Cr, Cu) or Group IV/VI residuals can pin the Fermi level, generate non-radiative recombination centers, or produce parasitic conduction. Target purity specifications for electronic-grade compound-semiconductor feedstock are typically **6N–7N** (99.9999%–99.99999%) for the constituent elements, i.e., total impurity content below the low parts-per-billion level for the most electrically active species.

### 2.2 Gallium Purification **[INFERENCE — general process metallurgy; AXT confirms grades produced, not the internal purification cascade]**

Gallium is a byproduct of bauxite (aluminum) and, to a lesser extent, zinc ore processing; it does not occur as a primary ore. Crude gallium recovered from Bayer-process liquors is typically only 3N–4N pure and must undergo further refinement. Industrially, this proceeds via a combination of:

1. **Chemical purification** — solvent extraction/ion exchange from Bayer liquor, followed by electrolytic refining to deposit gallium metal at high purity from acidic or alkaline gallate solution.
2. **Zone refining** — the crude gallium ingot is passed through a series of molten zones (a traveling RF or resistive heater), exploiting the fact that most impurities have a segregation coefficient $k < 1$ (they preferentially partition into the liquid rather than the re-freezing solid). Repeated zone passes progressively sweep impurities to one end of the ingot, which is then discarded.
3. **Vacuum distillation** — for impurities with sufficiently different vapor pressure from gallium, particularly effective for removing volatile metals.

AXT's public filings confirm it (via its joint ventures) produces gallium at 4N, 6N, and 7N grades, but the specific purification cascade (electrolytic vs. zone-refining vs. distillation, number of zone passes, crucible materials used to avoid recontamination) is **[PROPRIETARY/UNKNOWN]**.

$$
C_s(x) = k \, C_0 \, (1-x)^{k-1}
$$

is the classical Pfann normal-freezing/zone-refining relation describing solute concentration $C_s$ in the solidifying fraction $x$ of an ingot for a solute with effective segregation coefficient $k$, foundational to understanding why repeated directional solidification passes progressively purify a melt-grown ingot — this same physics reappears, non-trivially, inside the VGF crystal-growth step itself (Section 3.4).

### 2.3 Arsenic Purification **[INFERENCE]**

Elemental arsenic for III–V compound synthesis is typically produced by:

1. Roasting/refining of arsenic-bearing ores or as a byproduct of copper/lead/gold smelting, yielding crude arsenic trioxide (As₂O₃).
2. Reduction of As₂O₃ to elemental arsenic.
3. Vacuum sublimation/distillation — arsenic sublimes readily (triple point near 3 atm, 817 °C) and is commonly purified by vacuum distillation/sublimation in sealed quartz ampoules, which simultaneously purifies and reduces surface oxide.

AXT's filings confirm production of high-purity arsenic (multiple purity grades) through its China-based subsidiaries but do not disclose the specific purification train.

### 2.4 Germanium Purification **[INFERENCE, well-established industrial process]**

Germanium is recovered principally as a byproduct of zinc ore processing and from fly ash of certain coals. The classical, well-documented industrial route (used broadly across the Ge industry, not AXT-specific) is:

1. Extraction of germanium into GeCl₄ by chlorination of germanium-bearing zinc-refinery residues — GeCl₄ is a low-boiling liquid (b.p. 86.5 °C) that can be fractionally distilled to very high purity, since it is volatile and readily separated from non-volatile metal chlorides.
2. Hydrolysis of purified GeCl₄ to GeO₂.
3. Reduction of GeO₂ with hydrogen at elevated temperature to yield polycrystalline germanium metal.
4. Zone refining of the polycrystalline Ge ingot — germanium was historically one of the original demonstration materials for Pfann's zone-refining technique, and Ge zone refining routinely reaches electronic grade (impurity levels below ~10¹³ cm⁻³).

AXT's filings explicitly list **germanium dioxide (GeO₂)** as a distinct product line of its raw-material joint ventures, consistent with this GeCl₄ ⟶ GeO₂ ⟶ Ge reduction pathway; AXT germanium substrates are also documented as feeding into solar-cell (III–V multijunction space photovoltaic buffer/handle substrate) markets, which independently corroborates high-purity single-crystal Ge production.

### 2.5 Indium Phosphide Polycrystalline Charge Synthesis **[PUBLIC + INFERENCE]**

AXT's 10-K filings and press releases document that the company developed its own proprietary process (beginning circa 2001, scaled through Nanjing JinMei Gallium and successor entities) to manufacture InP polycrystalline ("poly") material — the direct compound-synthesis precursor charge used to grow single-crystal InP boules — because periodic shortages of merchant InP poly historically constrained supply.

**[INFERENCE]** Compound synthesis of InP from elemental indium and red phosphorus is thermodynamically and practically hazardous: phosphorus has a high vapor pressure at the InP melting point (1062 °C) — roughly 27.5 atm — so direct combination of the elements is normally carried out inside a sealed, pressure-rated quartz ampoule (or inside a high-pressure synthesis autoclave), often using a two-temperature-zone horizontal Bridgman-type synthesis furnace in which solid phosphorus is held at a lower temperature (controlling its vapor pressure) while molten indium at the hot end reacts with the phosphorus vapor to form InP, which is allowed to accumulate as a polycrystalline boule or granulate. This basic two-zone vapor-transport synthesis principle is standard across the InP industry (see Gault, Monberg & Clemans, *J. Crystal Growth* 74 (1986) 491, a foundational reference on this synthesis approach, cited in AXT's own published crystal-growth papers). AXT's specific synthesis reactor design, temperature schedule, and phosphorus-vapor-pressure control strategy are **[PROPRIETARY/UNKNOWN]**.

### 2.6 Ancillary Materials

- **Pyrolytic boron nitride (pBN)** — Produced by chemical vapor deposition of BN from precursor gases (typically BCl₃ + NH�3) onto a graphite mandrel at high temperature, yielding a dense, chemically inert, high-purity ceramic. AXT's Beijing BoYu joint venture manufactures pBN crucibles — the essential crystal-growth container material because pBN is chemically compatible with molten III–V and IV melts (low wetting, minimal contamination) and can withstand the required growth temperatures (up to ~1500 °C, well above GaAs melting point of 1238 °C and InP melting point of 1062 °C).
- **Boron oxide (B₂O₃)** — used industry-wide as a liquid encapsulant in Liquid Encapsulated Czochralski (LEC) growth (to suppress dissociation/volatilization of the volatile Group V species from the melt surface); AXT's continued production of B₂O₃ is notable given its VGF (not LEC) primary process, and likely reflects both its legacy LEC capability (via the 2015 Crystacomm InP acquisition, which used LEC) and sales to third-party LEC growers.
- **Quartz tubing** — used for ampoule fabrication in VGF/VB-style sealed-ampoule growth and for InP poly synthesis vessels.

---

## 3. Bulk Single-Crystal Growth from the Melt

This is the technical core of AXT's business and the primary subject of this review's emphasis, per the request.

### 3.1 The General Problem of III–V and Ge Melt Growth

All three of AXT's substrate materials are grown by directional solidification of a melt inside a sealed or semi-sealed container, rather than by pulling a crystal from an open, free melt surface as in conventional Czochralski silicon growth. This family of methods — Bridgman, Vertical Bridgman (VB), Vertical Gradient Freeze (VGF), and Horizontal Bridgman (HB) — shares the essential physics of moving a solidification isotherm through a stationary melt contained in a crucible, in contrast to Czochralski-type pulling, where the crystal is withdrawn from the melt through a free surface.

The choice of melt-growth method for a given material is governed principally by:

1. **Congruent vs. incongruent melting and volatility of a constituent** — GaAs and InP both have highly volatile Group V constituents (As, P) at their melting points, requiring either a sealed ampoule with a controlled overpressure, an encapsulant layer, or a separate arsenic/phosphorus overpressure source.
2. **Thermal stress and dislocation generation** — dislocation density in melt-grown crystals scales strongly with the radial and axial temperature gradients present during and after solidification, via the Alexander–Haasen / Jordan–Caruso–Von Neida (JCVN) thermoelastic stress framework. Minimizing gradients reduces resolved shear stress on the relevant slip systems and hence dislocation multiplication.
3. **Crucible/container interaction** — free versus contained growth affects both stress state and the potential for parasitic nucleation at container walls.

### 3.2 Why AXT Uses VGF Rather Than LEC

**[PUBLIC — this is one of AXT's most extensively documented technical claims, including in a peer-reviewed paper by AXT scientists]**

Historically, the dominant industrial method for growing semi-insulating GaAs was **Liquid Encapsulated Czochralski (LEC)**: a seed crystal is dipped into a free GaAs melt through a floating layer of molten B₂O₃ (which suppresses arsenic loss by vapor sealing the melt surface) and pulled upward while rotating, in a manner directly analogous to Czochralski silicon growth. LEC is capable of large-diameter growth and reasonably fast throughput, but suffers from a fundamental limitation: the crystal is essentially unsupported except at the seed, and it grows through a large, uncontrolled axial and radial temperature gradient (often hundreds of °C/cm near the melt surface, driven by the need for strong convective/radiative heat loss from the exposed growing crystal). This large thermal gradient generates high thermoelastic stress in the still-hot, mechanically weak just-solidified crystal, which is relieved by dislocation generation and multiplication, typically yielding **dislocation densities (etch pit density, EPD) in the range of 10⁴–10⁵ cm⁻²** for LEC semi-insulating GaAs, with pronounced "W"-shaped radial dislocation distributions.

**Vertical Gradient Freeze (VGF)**, by contrast — the technique AXT states it was the first company to commercialize at industrial scale, and upon which its entire substrate business is built — grows the crystal inside a sealed crucible (commonly pBN) that itself remains essentially stationary, while a furnace with a carefully shaped axial temperature profile is either translated relative to the crucible, or (more typically in modern VGF practice) the furnace's multi-zone heater power profile is *ramped down as a programmed function of time* so that the melting isotherm sweeps axially through the stationary melt, without any relative mechanical motion of crucible and furnace at all in the purest "gradient freeze" implementations. Because:

- the crystal remains fully enclosed by the crucible throughout growth (mechanical support reduces stress-induced bending/twisting),
- the growth interface can be maintained nearly planar and the *radial* temperature gradient — the component most responsible for radial thermal stress and bow — can be made very small by careful multi-zone furnace design, and
- the overall thermal gradients at the growth front (both axial and radial) are typically an order of magnitude lower than in LEC,

VGF-grown GaAs and InP characteristically achieve **substantially lower EPD** than LEC material — AXT and the broader literature report VGF EPD commonly in the low 10³ cm⁻² range or below for semi-insulating GaAs, versus 10⁴–10⁵ cm⁻² for LEC — along with lower residual strain (measurable by birefringence/photoelastic imaging) and higher mechanical strength (fewer stress concentrators from which cracks propagate), which AXT states translates directly into lower wafer breakage and higher customer device yield. This EPD/stress advantage is the technical basis of AXT's entire competitive positioning and is corroborated in the peer-reviewed literature (a key AXT-authored reference is the paper on "AXT — VGF excellence of III–V semiconductors," describing low-EPD semi-insulating and Si-doped conductive GaAs single crystals grown by a proprietary low-thermal-gradient VGF technique at industrial scale).

**[INFERENCE]** The general relationship between thermal gradient and dislocation density in melt-grown III–V crystals can be understood qualitatively through a Haasen-type dislocation-multiplication model, in which the dislocation generation rate is driven by the resolved shear stress $\tau$ in excess of a critical stress $\tau_0$:

$$
\frac{dN}{dt} = K N \left(\frac{\tau - \tau_0}{\tau_0}\right)^{m}
$$

where $N$ is the mobile dislocation density, $K$ and $m$ are material constants, and $\tau$ is set by the thermoelastic stress field, which itself scales with the temperature gradient $\nabla T$ and the crystal radius $r$ approximately as $\tau \propto \alpha E \, r \, \nabla T$ for a simple radially symmetric thermal-stress estimate ($\alpha$ = thermal expansion coefficient, $E$ = Young's modulus). Because $\tau$ scales with *both* gradient and radius, this framework also explains why scaling to larger wafer diameters (AXT's push toward 8-inch GaAs, discussed in Section 4) is intrinsically harder in low-gradient VGF than in LEC: the low-gradient furnace design that gives VGF its dislocation advantage must be engineered ever more carefully as the crucible diameter grows, because the same $\nabla T$ produces proportionally more stress at larger $r$.

### 3.3 VGF Process Architecture — Reconstructed Unit Operations

Based on the general VGF/Vertical Bridgman literature (the method traces to Gault, Monberg & Clemans 1986, and subsequent development by AXT and others such as Sumitomo Electric, Freiberger, and Japan Energy) and AXT's public statements, the VGF process for GaAs can be reconstructed as follows. Steps marked with a dagger (†) involve parameter choices that are AXT trade secrets; the sequence and physical necessity of the steps themselves is standard crystal-growth engineering.

1. **Charge preparation.** Polycrystalline GaAs (itself synthesized from high-purity Ga and As, typically by a horizontal Bridgman or gradient-freeze synthesis reaction analogous to the InP synthesis described in §2.5) is loaded into a pBN crucible, generally along with a small overpressure control mechanism — either a sealed quartz ampoule containing an arsenic vapor source at a controlled temperature, or a pressurized inert-gas-backed puller (a "high-pressure VGF," HP-VGF) that mechanically counterbalances the equilibrium As vapor pressure over the melt (~1 atm at the GaAs melting point of 1238 °C) to prevent boiling/dissociation of the melt surface.
2. **Seed placement.** A single-crystal seed of the desired crystallographic orientation (for GaAs substrates, typically (100), often with a small deliberate offcut of a few degrees toward ⟨110⟩ to promote favorable step-flow morphology in subsequent epitaxy) is placed at the bottom (or occasionally the cone-shaped bottom taper) of the crucible.
3. **Melt-down.**† The furnace, generally a multi-zone resistive-heating furnace with independently controlled axial zones, is ramped to fully melt the polycrystalline charge while leaving only the tip of the seed unmelted ("seed-back-melting control" is a standard, delicate step in all Bridgman-family growth — melting too much of the seed loses orientation control; too little risks incomplete wetting and spurious nucleation).
4. **Dopant incorporation.**† Dopants are added to the melt prior to or during melt-down: silicon (Si) for n-type conductive GaAs, chromium (Cr) historically or, more commonly in modern semi-insulating material, intrinsic/undoped semi-insulating behavior is achieved via compensation from the native EL2 deep donor defect combined with controlled melt stoichiometry (slightly As-rich melts favor formation of the As-antisite-related EL2 center that pins the Fermi level near midgap, giving high resistivity without extrinsic doping). For InP, Fe doping is used to achieve semi-insulating material (Fe forms a deep acceptor that compensates residual shallow donors), while S, Sn, or Si doping yields n-type conductive InP.
5. **Directional solidification.**† The axial temperature profile of the multi-zone furnace is programmed (via either mechanical translation of crucible/furnace, or, in "true" gradient-freeze mode, purely by time-programmed power reduction in sequential heater zones) so that the melting-point isotherm sweeps slowly upward from the seed through the melt at a controlled growth rate, typically on the order of a few mm/hr to ~1 cm/hr for III–V VGF growth — slow compared to Czochralski pulling rates, which is a direct consequence of the low-gradient philosophy (slower growth is required to keep the interface stable and nearly planar at low $\nabla T$, per constitutional supercooling stability criteria, see §3.4).
6. **Post-growth anneal/cool-down.**† A controlled, slow cool-down from the melting point to room temperature is used to further relax residual thermal stress and, in the case of GaAs, to homogenize the EL2 deep-donor concentration axially along the boule via an annealing step that allows arsenic interstitial/antisite defect populations to equilibrate.
7. **Boule recovery.** The crucible is opened (destructively, in the case of sealed encapsulated designs) and the grown boule extracted, typically presenting a cylindrical body with a conical or hemispherical tail corresponding to the crucible geometry at the seed end.

### 3.4 Underlying Continuum Physics of the Growth Interface

Directional solidification of a binary or higher-order compound melt is governed by coupled heat transport, solute transport, and interface-stability physics that are common to the entire Bridgman/VGF/Czochralski family, differing primarily in geometry and boundary conditions.

**Solute segregation.** For a compound with a dopant or unintentional impurity of equilibrium segregation coefficient $k_0 = C_s/C_l$ (solid concentration over liquid concentration at equilibrium), the effective segregation coefficient under diffusion-limited transport with a boundary layer of thickness $\delta$ at growth velocity $v$ is given by the Burton–Prim–Slichter relation:

$$
k_{eff} = \frac{k_0}{k_0 + (1-k_0)\exp(-v\delta/D)}
$$

where $D$ is the solute diffusivity in the melt. In VGF's low-convection, low-growth-rate regime, transport is closer to diffusion-limited than in a strongly stirred Czochralski melt, meaning $k_{eff}$ tends toward $k_0$ and axial dopant uniformity is comparatively harder to achieve over the boule length than in a well-mixed system — a known trade-off the industry accepts in exchange for VGF's dislocation-density advantage. Axial dopant distribution along a normal-freeze boule (no remixing) follows the Scheil equation:

$$
C_s(f_s) = k_0\, C_0\, (1-f_s)^{k_0-1}
$$

where $f_s$ is the solidified fraction — directly analogous to the zone-refining relation in §2.2, and the reason melt-grown boules of any type show systematic axial resistivity/doping gradients that substrate manufacturers must characterize and grade against.

**Interface morphological stability.** A planar solidification front is stable against breakdown into cellular/dendritic morphology only if the constitutional supercooling criterion is satisfied:

$$
\frac{G}{v} \geq \frac{m\, C_0\, (1-k_0)}{k_0\, D}
$$

where $G$ is the temperature gradient in the melt ahead of the interface, $v$ is growth velocity, and $m$ is the liquidus slope. This inequality is precisely why VGF's low-gradient philosophy (small $G$) must be compensated by correspondingly slow growth rate $v$ to retain a stable, planar, low-defect growth front — connecting the macroscopic process choice (slow growth) directly to microscopic interface stability physics.

**Thermal-stress-driven dislocation generation** is treated in §3.2 above via the Haasen-type framework; the essential point restated here is that VGF's principal engineering lever — minimizing $\nabla T$ in all directions, especially radially — simultaneously (a) reduces thermoelastic stress and dislocation multiplication (the desired outcome) and (b) forces slower growth rates and complicates axial doping uniformity (the accepted trade-off), which is the fundamental physical reason VGF is a lower-throughput, higher-quality process relative to LEC.

### 3.5 Germanium Growth Specifics **[INFERENCE]**

Germanium, as a single-element Group IV semiconductor with no volatile constituent to manage, is intrinsically simpler to grow by VGF/VB than the III–V compounds — no sealed-ampoule overpressure management is required, and the melt is congruent by definition. AXT states it remains "the only company to manufacture germanium substrates using VGF technology," a claim that is plausible precisely because most commercial Ge substrate/solar-cell-buffer producers use conventional (open, Czochralski-type) pulling, since Ge lacks the volatility problem that historically motivated sealed-ampoule/VGF development for III–Vs in the first place; AXT's application of its proprietary low-gradient VGF furnace platform to Ge is therefore best understood as a process-platform reuse decision (leveraging the same low-stress, high-mechanical-strength furnace architecture developed for GaAs/InP) rather than a technical necessity of Ge growth chemistry.

### 3.6 Crystal Orientation and Boule Geometry **[INFERENCE — standard industry practice, not AXT-specific disclosure]**

Substrate wafers for device epitaxy are virtually universally specified by crystallographic orientation, since epitaxial nucleation, dopant incorporation, and surface reconstruction are all strongly orientation-dependent:

- GaAs and InP substrates: predominantly (100) orientation, frequently with a controlled offcut (2°–6°) toward a ⟨110⟩ or ⟨111⟩ direction to suppress anti-phase-domain formation in polar-on-polar epitaxy and to promote step-flow growth morphology.
- Semi-insulating GaAs is used as the base for high-frequency devices (HBTs, HEMTs, MMICs) where substrate conductivity must be minimized to reduce parasitic capacitance/loss; conductive (Si-doped, n-type) GaAs is used for LED/laser and some VCSEL applications where vertical current conduction through the substrate is required.

---

## 4. From Boule to Wafer: Mechanical and Chemical Substrate Finishing

Once a single-crystal boule is grown and its crystallographic quality confirmed (X-ray diffraction orientation check, resistivity mapping, EPD sampling), it undergoes a standard sequence of mechanical and chemical operations common across the compound-semiconductor substrate industry. AXT does not publicly disclose process-specific parameters (slurry chemistry, polish pad recipes, etch bath compositions) for these steps, so this section is presented as **[INFERENCE]** based on universal industry practice, unless otherwise cited.

1. **Boule characterization and orientation (X-ray diffraction, XRD).** The as-grown boule is X-ray oriented to precisely locate the crystallographic axes before any cutting, since the desired wafer offcut angle must be referenced to the true crystal lattice, not the physical boule geometry.
2. **End-grinding / cylindrical grinding.** The boule is ground to a controlled, precise cylindrical diameter (this is the step that ultimately sets the final wafer diameter — e.g., 4-inch, 6-inch, 8-inch — and is the reason "scaling to a new diameter" is a substantial engineering program: it requires not only a larger-diameter crystal but tooling and downstream equipment redesigned for the new size).
3. **Orientation flat/notch grinding.** A flat or notch is ground into the boule (or later into wafers) at a fixed crystallographic reference to allow subsequent lithographic/epitaxial tools to align devices to a known crystal direction.
4. **Wafering (ID or wire sawing).** The cylindrical boule is sliced into individual wafers using either an inner-diameter (ID) annular diamond saw (older technology) or, more commonly in modern high-volume production, a multi-wire saw using a slurry or fixed-abrasive wire — wire sawing achieves higher material yield (thinner kerf loss) and better surface/subsurface damage control than ID sawing, both important for expensive III–V material.
5. **Lapping.** Both wafer faces are lapped (typically with a free-abrasive slurry, e.g., alumina or silicon carbide particles in a carrier fluid, between rotating lapping plates) to remove saw damage and achieve global flatness/parallelism.
6. **Edge profiling (edge rounding/beveling).** Wafer edges are mechanically rounded to reduce edge chipping and stress concentration during subsequent handling and epitaxial/device processing — directly connected to AXT's marketed "lower breakage" claim, since VGF's inherent low residual stress is only fully realized in downstream yield if edge damage from mechanical finishing does not introduce new stress concentrators.
7. **Chemical-mechanical polishing (CMP).** A combination of mechanical abrasion and chemical etching (typically a colloidal silica or similar abrasive slurry combined with an oxidizing/etching chemistry appropriate to the specific compound, e.g., sodium hypochlorite-based slurries historically used for GaAs) achieves an epi-ready, damage-free, atomically smooth polished surface. Front-side (device-side) polish specifications are extremely stringent (sub-angstrom RMS roughness, near-zero subsurface damage) since epitaxial layer quality is directly inherited from substrate surface quality; back-side finish requirements are typically more relaxed (etched or lapped-only, sometimes polished for specific thermal or optical applications).
8. **Cleaning.** Multi-step wet chemical cleaning (organic solvent degrease, particle removal, native-oxide management) to remove polishing residue and particulates prior to packaging.
9. **Metrology and inspection.** Final wafers are characterized for thickness and total thickness variation (TTV), bow/warp, resistivity (four-point probe or contactless eddy-current methods), etch pit density (via a defect-revealing chemical etch, e.g., molten KOH etch for GaAs, followed by optical/automated EPD counting), particle count (via laser scattering surface scanners), and crystallographic perfection (X-ray topography for high-end material).
10. **Packaging.** Wafers are packaged in cleanroom-compatible, particle-controlled cassettes/shippers for delivery to epitaxy customers.

### 4.1 The 8-Inch GaAs Scaling Program **[PUBLIC]**

AXT publicly announced in April 2021 that it had shipped its first 8-inch (200 mm) diameter GaAs substrates — silicon-doped, n-type — to a major customer, describing this as enabled by its new Dingxing and Kazuo facilities, purpose-built for high-volume, higher-diameter production with improved automation. AXT explicitly frames each diameter increase as a major increase in technical difficulty, consistent with the thermal-stress-scaling argument developed in §3.2 (dislocation-generating stress scales with crystal radius at fixed gradient, so the low-gradient VGF advantage becomes progressively harder to preserve at larger diameter). AXT's stated demand driver for 8-inch GaAs is VCSELs for 3D sensing and LiDAR, and microLEDs for displays — applications where larger substrate diameter directly reduces device manufacturing cost per die by increasing the number of devices per epitaxial wafer run.

---

## 5. Epitaxy: The Interface Between Substrate and Device

AXT explicitly does not perform epitaxy as a commercial product line; it states it sells the majority of its substrates to companies that specialize in applying the epitaxial layer. This is nonetheless the essential next step in the materials-to-device chain and merits treatment because substrate specification (orientation, offcut, EPD, doping type/level, surface finish) is *defined by*, and only meaningful in the context of, the epitaxial and device processes downstream. **[INFERENCE / general epitaxy literature — not AXT-specific]**

- **Molecular Beam Epitaxy (MBE)** — ultra-high-vacuum physical deposition using effusion cells (or valved cracker cells for As/P) to deposit III–V layers atom-by-atom with monolayer-scale control; favored for the most demanding heterostructures (HEMTs, some VCSELs, quantum-well lasers) due to superior interface abruptness. AXT's raw-material filings note that its joint ventures supply "parts for MBE," indicating downstream customer relationships in this space.
- **Metalorganic Chemical Vapor Deposition (MOCVD / MOVPE)** — the dominant industrial epitaxy technology for high-volume compound-semiconductor device production (LEDs, VCSELs, HBTs, solar cells), using metalorganic precursors (e.g., trimethylgallium, trimethylindium, arsine or its safer substitutes, phosphine) thermally decomposed at a heated substrate surface; substantially higher throughput than MBE, making it the primary consumer of AXT's high-volume GaAs and InP substrate production.
- Epitaxial layer quality is directly inherited from substrate crystallographic perfection: threading dislocations in the substrate propagate into epitaxial layers, degrading minority-carrier lifetime (critical for lasers/LEDs/solar cells) and increasing leakage current (critical for HBTs/HEMTs) — this is the fundamental technical justification for AXT's entire value proposition around low-EPD VGF material.

---

## 6. Device Fabrication and Packaging (Downstream, Non-AXT)

AXT does not fabricate devices; this section is included for completeness of the "materials-to-devices" chain requested, and is drawn from general compound-semiconductor device literature, not AXT disclosures. **[INFERENCE / general knowledge]**

Representative device classes built on AXT's substrate materials, and their basic fabrication logic:

| Substrate | Representative device | Basic device physics |
|---|---|---|
| Semi-insulating GaAs | HBT (heterojunction bipolar transistor), pHEMT (pseudomorphic HEMT), MMIC | High-resistivity substrate minimizes parasitic capacitance/RF loss; devices built in epitaxial layers above |
| n-type conductive GaAs | VCSEL (vertical-cavity surface-emitting laser), LED | Vertical current injection through substrate; distributed Bragg reflector mirrors epitaxially grown above/below active region |
| InP (semi-insulating, Fe-doped) | Photonic integrated circuits, high-speed InP-based lasers/modulators, some HBTs | Lattice-matched to InGaAsP/InGaAs alloys spanning telecom wavelengths (1.3–1.55 µm) |
| InP (n-type conductive) | Laser diodes, avalanche photodiodes, high-speed optical transceivers | Vertical device architectures analogous to GaAs VCSELs |
| Germanium | III–V multijunction space solar cells (Ge as bottom sub-cell and/or mechanical handle substrate); some photodetectors | Ge's ~0.66 eV bandgap and reasonable lattice match to GaAs make it an efficient bottom cell and low-cost, mechanically robust growth template |

Device fabrication proceeds through standard planar-processing sequences (photolithography, dry/wet etching, metallization for ohmic and Schottky contacts, dielectric passivation, and for optoelectronic devices, mirror/facet formation) that are materially distinct from, and entirely downstream of, AXT's substrate manufacturing scope. Final packaging (die singulation, die attach, wire bonding or flip-chip bonding, hermetic or non-hermetic encapsulation, optical fiber coupling for photonic devices) is performed by AXT's customers or their contract assemblers, not by AXT.

---

## 7. AXT's Commercial Product Portfolio and End Markets **[PUBLIC]**

### 7.1 Substrate Product Lines

- **GaAs substrates**: historically offered from 1-inch through 6-inch diameter as the primary product line; 8-inch (200 mm) now in qualification/early production.
- **InP substrates**: 2-, 3-, and 4-inch diameters historically; AXT has more recently disclosed development work on larger InP diameters (6-inch) to serve AI-driven optical-networking demand.
- **Germanium substrates**: 2- and 4-inch diameters, used in solar and select electronic/photodetector applications.
- **Raw materials**: sold both to internal (AXT substrate) consumption and to third-party customers via the joint-venture entities — gallium (4N/6N/7N), arsenic, germanium/GeO₂, InP poly, pBN crucibles, B₂O₃, quartz tubing.

### 7.2 End Markets

AXT's own market description spans: 5G wireless infrastructure (RF power amplifiers built on semi-insulating GaAs), data-center optical connectivity/silicon photonics (InP-based lasers and photodetectors — an area of rapidly growing emphasis given AI-datacenter optical-interconnect demand), passive optical networks (telecom access-network lasers/detectors on InP), LED lighting, laser diodes, 3D-sensing and LiDAR VCSELs (GaAs), microLED displays (GaAs), and satellite/space solar cells (germanium).

### 7.3 Recent Strategic Developments **[PUBLIC]**

- **2015**: AXT acquired Crystacomm, Inc. (Mountain View, CA), an InP substrate producer using the Liquid Encapsulated Czochralski (LEC) technique, broadening AXT's InP capability and intellectual property base beyond pure VGF.
- **2021**: First shipment of 8-inch GaAs substrates to a major customer, driven by VCSEL/LiDAR/microLED demand.
- **2022 onward**: Beijing Tongmei Xtal Technology (AXT's principal Chinese operating subsidiary) pursued a STAR Market IPO process in China, involving formal disclosure of patent licensing arrangements between AXT (US parent) and Tongmei (China subsidiary) — notably, AXT's patents licensed to Tongmei were characterized in the IPO disclosure as relating mainly to GaAs and germanium substrate technology, predominantly filed before 2010, and explicitly *not* covering InP substrate technology, pBN materials, or other high-purity raw materials, and were said to account for a relatively small proportion (~6%) of Tongmei's relevant product revenue — a rare, unusually granular public data point on the economic value AXT attributes to its own core patented process IP versus accumulated unpatented trade-secret know-how.
- **2023–2025**: US–China trade tensions materially affected AXT, including Chinese export-permit requirements on gallium, germanium, and (from late 2024) InP-related exports, which AXT's own 10-K disclosures describe as having reduced North American revenue and pressured joint-venture equity income.
- **2025**: AXT reported declining full-year revenue (down ~11% year-over-year), attributed to reduced germanium wafer sales and export-permit friction, while noting the receipt of initial Chinese export permits enabling some InP shipments to Europe and Japan, and continued capacity investment in 8-inch GaAs and 6-inch InP.
- **Mid-2026**: Beijing Tongmei Xtal Technology entered a long-term (2027-delivery) InP wafer supply agreement with Nanjing Casela Technologies, explicitly framed by market commentary around AI-driven demand for InP substrates feeding high-speed optical interconnect/photonics markets.

---

## 8. Synthesis: Why the VGF/Vertical-Integration Model Matters

Drawing the threads of this report together, AXT's competitive position rests on three linked technical/strategic pillars, all traceable to public disclosure:

1. **A genuinely differentiated bulk-growth process (VGF)** whose low-thermal-gradient philosophy is physically well-justified as a route to lower dislocation density and residual stress than the historically dominant LEC method, at the cost of slower growth rates and more challenging axial dopant uniformity — a textbook illustration of the growth-rate/gradient/defect-density trade-off inherent to all melt-growth technology (§3.2–3.4).
2. **Backward integration into critical-mineral refining** (gallium, germanium, arsenic, InP poly, pBN) through Chinese joint ventures, which is economically unusual in this industry and has become strategically salient given the 2023–2026 tightening of Chinese export controls on gallium and germanium — materials for which China holds a dominant share of global refining capacity.
3. **A geographically concentrated, China-based manufacturing footprint**, which historically delivered AXT's cost advantage but has, in the current export-control environment, become a source of revenue volatility and geopolitical exposure that is now central to how public markets and AXT itself describe near-term company risk.

---

## References

**Primary AXT / SEC Sources [PUBLIC]**
1. AXT, Inc. Form 10-K, Fiscal Year 2024, SEC filing, https://www.sec.gov/Archives/edgar/data/1051627/000155837025003004/axti-20241231x10k.htm
2. AXT, Inc. Form 10-K, Fiscal Year 2020, SEC filing, https://www.sec.gov/Archives/edgar/data/1051627/000155837021003377/axti-20201231x10k.htm
3. AXT, Inc. Form 10-K, Fiscal Year 2019, SEC filing, https://www.sec.gov/Archives/edgar/data/1051627/000155837020002561/axti-20191231x10k.htm
4. AXT, Inc. Form 10-K, Fiscal Year 2013 and 2012 and 2011, SEC filings (EDGAR, CIK 0001051627).
5. AXT, Inc. Corporate Presentation, March 2025, https://s202.q4cdn.com/832677016/files/doc_presentations/2025/Mar/24/AXTI-Corporate-Deck-2025.pdf
6. AXT, Inc. Q2 2025 10-Q, SEC filing, https://s202.q4cdn.com/832677016/files/doc_financials/2025/q2/9d819079-5f70-466c-8a1c-fe515aab819c.pdf
7. "AXT, Inc. Supplies First 8-Inch Gallium Arsenide Wafers to Major Customer," GlobeNewswire / AXT press release, April 28, 2021.
8. "American Xtal Technology Announces a 3x Expansion of Its GaAs Substrate Capacity By Q301," PR Newswire / AXT press release, May 2000.
9. "AXT announces further expansion of operations in China and financial results," compoundsemiconductor.net, February 2002.
10. "AXT acquires InP substrate maker Crystacomm," semiconductor-today.com, July 2015.
11. "AXT supplies first 8-inch GaAs wafers," semiconductor-today.com, April 2021.
12. "AXT's Q3 revenue far exceeds guidance, after China export licenses granted for InP," semiconductor-today.com, November 2025.
13. AXT, Inc.: Reply to the Second Round Audit Inquiry Letter, Beijing Tongmei Xtal Technology STAR Market IPO application, MarketScreener/8-K disclosure, June 2022.
14. AXT 2025 10-K financial summary, TradingView News, March 2026.
15. "AXT (AXTI) Is Down 7.6% After AI-Focused Indium Phosphide Deal," Yahoo Finance, ~July 2026.

**Peer-Reviewed / Technical Literature**
16. AXT scientific authors, "AXT — VGF excellence of III–V semiconductors," *Materials Science and Engineering: B*, ScienceDirect (describes low-EPD semi-insulating and Si-doped conductive GaAs single crystals grown by proprietary low-thermal-gradient VGF at industrial scale).
17. W. A. Gault, E. M. Monberg, J. E. Clemans, "A novel application of the vertical gradient freeze method to the growth of high quality III–V crystals," *Journal of Crystal Growth*, 74 (1986), p. 491. (Foundational VGF/InP synthesis reference cited in AXT literature.)
18. I. C. Bassignana, D. A. Macquistan et al., in *Common Themes and Mechanisms of Epitaxial Growth Symposium*, Materials Research Society, San Francisco (1993), p. 185.
19. H. Yamamoto, O. Oda, M. Seiwa, M. Taniguchi, H. Nakata, M. Ejima, *Journal of the Electrochemical Society*, 136 (1989), p. 3098.
20. W. G. Pfann, *Zone Melting*, 2nd ed., Wiley, New York, 1966. (Foundational reference for zone-refining segregation physics, §2.2/§3.4.)
21. J. A. Burton, R. C. Prim, W. P. Slichter, "The Distribution of Solute in Crystals Grown from the Melt," *Journal of Chemical Physics*, 21 (1953), p. 1987. (Effective segregation coefficient, §3.4.)
22. S. K. Jordan, T. J. Caruso, A. R. Von Neida, "A thermoelastic analysis of dislocation generation in pulled GaAs crystals," *Bell System Technical Journal*, 59 (1980), p. 593. (Foundational thermal-stress/dislocation-generation framework, §3.2/§3.4.)

**General Reference Texts**
23. D. T. J. Hurle (ed.), *Handbook of Crystal Growth*, Vol. 2: Bulk Crystal Growth, Elsevier/North-Holland (standard reference for VGF/Bridgman/LEC comparative process physics).
24. R. Hull, *Properties of Crystalline Silicon* and analogous III–V property handbooks (EMIS Datareviews Series, INSPEC/IEE) for GaAs, InP, and Ge material property compilations.

---

*Note on sourcing confidence: Sections 1, 2.6 (partial), 4.1, and 7 are supported by direct, citable public statements from AXT SEC filings, press releases, and peer-reviewed AXT-authored literature. Sections 2.1–2.5, 3.3, 3.5, 3.6, 4 (steps 1–10), 5, and 6 combine confirmed AXT product/material facts with standard, well-established compound-semiconductor process engineering that is not AXT-specific disclosure — these are flagged inline as [INFERENCE]. AXT's exact furnace designs, thermal programs, dopant schedules, crucible geometries, and purification-cascade engineering remain undisclosed trade secrets and are marked [PROPRIETARY/UNKNOWN] throughout.*

---

> [!NOTE]
> 
> Generated by Claude.ai
>
> Model: Sonet 5
>
> Prompt: Provide an extensive, highly technical overview of AXT, Inc. (USA) and its vertically integrated compound semiconductor business, with particular emphasis on the production of bulk single crystals grown from the melt and their role in the compound semiconductor value chain. The report should focus on the complete materials-to-devices manufacturing chain, beginning with raw material purification, crystal growth, wafer production, epitaxy, device fabrication, packaging, and commercial products. The report should be written at the level of a graduate textbook or industrial technical review and should distinguish clearly between publicly documented information, reasonable engineering inferences, and unknown/proprietary processes. Provide key references. Show the output in Markdown format.
