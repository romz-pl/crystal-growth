# Beijing Tongmei Xtal Technology Co., Ltd.: A Technical Review of Vertically Integrated Compound Semiconductor Substrate Manufacturing

**A graduate-level industrial technical review**

---

## Preface and Epistemic Framing

This report distinguishes three tiers of information throughout:

- **[DOCUMENTED]** — drawn from public filings (SEC/SSE), press releases, patents assigned to AXT/Tongmei, or peer-reviewed literature on the specific processes AXT/Tongmei has publicly described.
- **[INFERRED]** — standard industrial/scientific practice for this materials class, reasonably attributable to Tongmei's process given documented inputs, outputs, and equipment, but not confirmed in a Tongmei-specific public source.
- **[PROPRIETARY/UNKNOWN]** — process parameters, recipes, or engineering details that are commercially confidential and not publicly disclosed; flagged explicitly rather than guessed at.

Tongmei does not publish detailed process specifications (this is normal — crystal growth recipes are the core trade secret of any III-V substrate supplier). This review therefore combines Tongmei/AXT-specific disclosures with the general science and engineering of melt-grown compound semiconductor crystals, as documented in the crystal growth literature, to construct a coherent, textbook-level picture of the likely manufacturing chain.

---

## 1. Corporate and Structural Overview

**[DOCUMENTED]** Beijing Tongmei Xtal Technology Co., Ltd. ("Tongmei") is a Beijing-headquartered material science company that develops and manufactures high-performance compound and single-element semiconductor substrate wafers: gallium arsenide (GaAs), indium phosphide (InP), and germanium (Ge). Tongmei is a subsidiary of **AXT, Inc.** (Nasdaq: AXTI), a Fremont, California-headquartered company that retains worldwide sales, administration, and customer-service functions while Tongmei (and its own subsidiaries) carries out essentially all manufacturing.

Tongmei is often referred to in the literature and press as simply "AXT's China operations," but it is worth being precise about its corporate architecture, which was substantially reorganized around 2020–2022 in preparation for an (ultimately unconsummated to date, subject to regulatory review) IPO on the Shanghai Stock Exchange STAR Market (Sci-Tech innovAtion boaRd):

- Tongmei's IPO application was **approved by the SSE** for forwarding to the China Securities Regulatory Commission (CSRC) in July 2022, a step AXT characterized as a "major milestone," though the filing remained subject to CSRC review.
- In December 2020, AXT contributed equity in several operating subsidiaries into Beijing Tongmei, including **Baoding Tongmei**, **Chaoyang Tongmei**, **Nanjing Jinmei**, **Chaoyang Jinmei**, and **Beijing Boyu**.
- AXT established a US sales entity, **AXT-Tongmei**, in December 2020 to serve as the overseas selling/procurement entity; Beijing Tongmei subsequently acquired AXT-Tongmei in May 2021.
- The result, per Tongmei's own STAR Market filings, is "a complete industry chain for the R&D, production and sale of semiconductor substrate materials, pBN crucibles, key raw materials and high-purity metals" — i.e., a deliberately constructed vertically integrated entity spanning raw-material refining through finished substrate sale.

**[DOCUMENTED] Manufacturing footprint.** Tongmei operates manufacturing facilities in **three separate locations in China**. The flagship site is described as a suburb-of-Beijing complex of **eight buildings totaling approximately 300,000 square feet**, which AXT describes as "the world's largest III-V wafer production facility." A second major site is in **Dingxing**, Hebei Province (Baoding prefecture, ~90 minutes south of Beijing), acquired to host relocated GaAs manufacturing; at acquisition it comprised roughly 140,000 sq ft of manufacturing space plus 50,000 sq ft of offices/dormitories, with a total site footprint of ~18.8 acres and room for expansion. A third site, associated with the Chaoyang-branded subsidiaries, supports raw-material and possibly germanium-related operations. **[INFERRED]** The staged relocation plan (2017–2018 onward) moved GaAs crystal growth and wafering to Dingxing while InP and Ge substrate manufacturing were slated to remain at the original Beijing facility, at least for an interim period; the current (2026) split across sites is not fully disclosed in the sources reviewed here.

**[DOCUMENTED] Scale indicators (2025–2026).** AXT reported consolidated quarterly revenue in the range of roughly $19–28 million across 2025–2026, with substrate sales dominated by GaAs and (increasingly) InP, and with the Asia-Pacific region accounting for the large majority (77–87%) of revenue — consistent with a China-manufactured product sold heavily into Asian device-fabrication and OSAT customers, alongside direct export. Customer concentration has risen sharply, with the top five customers moving from ~29% of revenue to over 45% between 2024 and Q3 2025, with two customers individually exceeding 10% of revenue — a pattern consistent with the optical-transceiver/data-center supply chain, where a small number of large laser/photonics integrators (e.g., Lumentum, Coherent) are dominant InP consumers.

---

## 2. The Vertical Integration Model: Raw Materials to Finished Substrate

### 2.1 Strategic rationale

**[DOCUMENTED]** AXT/Tongmei's central strategic thesis, stated consistently across 10-K filings from the mid-2000s through 2024, is that **partial ownership of upstream raw-material joint ventures** in China provides (a) pricing advantages, (b) supply reliability, (c) market-trend visibility, and (d) shorter procurement lead times for materials that are otherwise thinly traded, geopolitically sensitive, and difficult to source at semiconductor-grade purity. AXT holds **board representation in all of these entities** and consolidates for accounting purposes those in which it holds a majority/controlling interest, using equity accounting for minority stakes. Ownership percentages across the JV portfolio have historically ranged from roughly 25% to 83%.

This is a textbook example of **backward vertical integration** in a critical-materials industry: rather than purchasing gallium, arsenic, germanium, indium, and crucible materials on the open market (where China itself controls a large share of global primary gallium and germanium supply), AXT/Tongmei internalized a meaningful fraction of that supply chain inside China, mitigating exposure to both price volatility and (ironically, given subsequent events) export-control risk — though, as discussed in Section 7, this strategy could not fully insulate the company once China itself imposed export controls on the finished substrates and the raw elements.

### 2.2 The raw-material joint-venture network

**[DOCUMENTED]** As of the mid-2020s, AXT states it participates in **more than ten joint ventures in China** producing materials "critical to the entire substrate manufacturing industry." The two entities AXT **consolidates** (i.e., controls) and reports on individually in recent earnings disclosures are:

| Entity | Products (as disclosed) |
|---|---|
| **BoYu** (Beijing Boyu / Boyu Chaoyang / Boyu Tianjin) | High-temperature pyrolytic boron nitride (pBN) crucibles; pBN-based tooling for OLED evaporation sources |
| **JinMei** (Nanjing Jinmei / Chaoyang Jinmei) | High-purity gallium, high-purity germanium, InP polycrystalline starting material, and (as of 2026) high-purity indium refining |

Beyond these two, the broader JV network (per AXT filings across multiple years) produces:

- **Raw gallium (4N, 99.99%)** and **refined high-purity gallium (6N, 7N, and reportedly up to 8N)**
- **Arsenic** at multiple purity grades (4N, 6N, 7N)
- **Germanium metal and germanium dioxide (GeO₂)**
- **Pyrolytic boron nitride (pBN) crucibles**, the vessel material of choice for melt growth of GaAs and InP (chemically inert to As/P-bearing melts at growth temperature, low reactivity, high thermal-shock resistance)
- **Boron oxide (B₂O₃)**, used as a liquid encapsulant in both liquid-encapsulated Czochralski (LEC) and encapsulated VGF/vertical Bridgman (VB) growth
- **High-purity indium**, added to the internal supply chain as recently as early 2026, explicitly to secure a "guaranteed supply of another critical material for InP substrates" as InP demand surged

**[DOCUMENTED/quantitative claim from third-party analysis, treat with appropriate caution]** One investment-research source states that the JV network processes standard 4N gallium up through 5N, 6N, 7N, and reportedly 8N purity. This level of purity (8N = 99.999999%) is at the extreme high end of what is industrially claimed for gallium refining anywhere and should be treated as a **vendor/analyst claim rather than a confirmed engineering specification**; AXT's own SEC filings reference 4N, 6N, and 7N gallium explicitly, not 8N.

### 2.3 Why raw-material purity matters at this stage

**[INFERRED — standard semiconductor materials science]** The purity of the Group III and Group V elemental feedstocks propagates almost directly into the electrically active impurity concentration of the final single crystal, because:

1. Many transition-metal and other impurities (Fe, Cr, Cu, Ni, Co, S, Se, Te at trace levels) act as unintentional dopants or deep-level traps in GaAs and InP, directly setting carrier concentration, compensation ratio, and minority-carrier lifetime.
2. For **semi-insulating (SI) GaAs**, achieving resistivities of ~10⁷–10⁸ Ω·cm depends on a precise compensation balance between the native deep donor **EL2** and shallow residual acceptors (principally carbon), which is only reproducible if background impurity levels are controlled at the sub-ppb level — feasible only with 6N–7N-class elemental gallium and arsenic.
3. For **conductive (n-type) GaAs and InP substrates** used under epitaxial laser and LED structures, controlled doping (Si, S, or Sn for n-type; Zn for p-type) must sit on top of an extremely clean background, or the dopant profile becomes unreproducible from ingot to ingot.

This is the direct scientific justification for why a substrate manufacturer would choose to own gallium/arsenic/germanium/indium refining capacity rather than simply buy "semiconductor grade" material on the open market: **reproducibility of electrical properties (resistivity, mobility, EPD, compensation) is only achievable with tight control of the entire purity chain**, and this control is more reliable when the purification step is owned rather than outsourced.

---

## 3. Crystal Growth: Bulk Single Crystals from the Melt

This is the technical heart of Tongmei's business and the focus requested. All three of Tongmei's substrate materials — GaAs, InP, and Ge — are produced as **bulk single crystals grown from a stoichiometric (or near-stoichiometric) melt**, then sliced into wafers. This section covers the physics, the specific growth technologies AXT/Tongmei is documented to use, and the process controls involved.

### 3.1 Why melt growth, and why VGF specifically

**[DOCUMENTED]** AXT states that it **"was the first company to commercialize VGF [Vertical Gradient Freeze] technology in the industry"** and that it was the first to introduce 6-inch-diameter GaAs substrates grown by VGF. VGF (a Bridgman-family, vertical-freeze technique) is AXT's proprietary/flagship growth process, referenced repeatedly and specifically (not just generically) across AXT's investor materials, patents, and technical marketing.

**[INFERRED/general crystal-growth science, consistent with documented VGF advantages]** Two melt-growth families dominate industrial III-V bulk crystal growth:

1. **Liquid-Encapsulated Czochralski (LEC)** — a seed crystal is dipped into the melt from above and slowly withdrawn while rotating, pulling the growing crystal upward through a B₂O₃ encapsulant layer that suppresses volatile Group V (As, P) loss from the melt surface. LEC allows relatively fast growth and good diameter control via meniscus/weight-sensing feedback, but the crystal experiences significant axial and radial temperature gradients as it is pulled through the hot zone, generating high thermal stress and, consequently, **relatively high dislocation densities** (etch pit density, EPD, often 10⁴–10⁵ cm⁻² in conventional LEC GaAs).

2. **Vertical Gradient Freeze / Vertical Bridgman (VGF/VB)** — the melt and crucible remain essentially stationary while a **traveling vertical temperature gradient** is imposed (by sequentially adjusting multi-zone furnace heater power, rather than by mechanically translating the crucible) so that the crystal solidifies progressively from a seed at the bottom of the crucible upward. Because the melt is not mechanically pulled and free convection is comparatively suppressed, VGF crystals experience substantially lower thermal stress and much smaller radial temperature gradients, translating into **markedly lower dislocation densities** — published VGF GaAs work reports EPD ≤ 500 cm⁻² for Si-doped material, versus the much higher values typical of LEC.

**[DOCUMENTED, general literature, consistent with VGF rationale used industry-wide including by AXT]** This dislocation-density advantage is the central reason VGF has become the preferred method for GaAs and InP substrates destined for epitaxial laser diode and high-power device fabrication: dislocations act as non-radiative recombination centers and can propagate into epitaxial layers, degrading diode-laser lifetime and LED efficiency. VGF's "lower thermal stress during solidification produces fewer dislocations than LEC pulling," which is precisely why AXT has built its substrate franchise around it.

### 3.2 The VGF process in detail

**[DOCUMENTED — drawn from patents assigned to AXT and the general VGF literature, which are consistent with each other]**

A representative VGF process (per AXT-assigned US patents on 6-inch and 8-inch GaAs VGF growth, and consistent with the general VGF literature) proceeds as follows:

**Apparatus.** A cylindrical **pyrolytic boron nitride (pBN) crucible** — chemically inert, low-oxide, high-purity — sits inside a sealed fused-silica (quartz) **ampoule**, itself positioned within a **multi-zone resistive furnace**. The furnace zones (commonly upper "hot" zone, a gradient zone, and lower "cold"/seed zone) are independently power-controlled, allowing the axial temperature profile inside the ampoule to be shaped and then translated in time without any mechanical motion of the crucible (in the purest form of VGF) or with only slow crucible/pedestal translation (in VB variants).

**Charge and seeding.** A single-crystal **seed** (oriented, typically ⟨100⟩ or ⟨111⟩-family depending on target product) is placed at the bottom of the crucible in a shaped seed pocket. The crucible is then loaded with polycrystalline GaAs (or InP) charge material above the seed. A layer of solid **B₂O₃** is placed to later form a liquid encapsulant.

**Sealing and melt.** The ampoule is evacuated and sealed under vacuum, then heated. As the furnace temperature rises past the B₂O₃ softening point and then the GaAs melting point (≈1238 °C for congruent GaAs; InP melts at ≈1062 °C), the polycrystalline charge liquefies while the B₂O₃ becomes a mobile liquid layer that floats atop the melt, sealing it from the ampoule's residual atmosphere and — critically — suppressing dissociative loss of volatile arsenic (or phosphorus, for InP) from the melt surface, since As and P have very high equilibrium vapor pressures over their respective melts at growth temperature (several atmospheres for As over molten GaAs, tens of atmospheres for P over InP). Only the seed at the very bottom is kept below its melting point (a small unmelted "seed tip") to preserve crystallographic registry for subsequent growth.

**Overpressure control.** **[DOCUMENTED, general practice for VGF/LEC of As- and P-bearing melts]** Because arsenic and, especially, phosphorus vapor pressures over their respective melts are large, the sealed ampoule/autoclave is typically pressurized with an inert gas (commonly nitrogen or argon) to a pressure close to the equilibrium dissociation pressure of the compound at growth temperature, preventing the melt itself from losing stoichiometry through evaporative loss of the Group V species during the (many-hour to multi-day) growth run. **[DOCUMENTED — specific to a Tongmei/AXT-style process per patent]** One AXT-assigned patent for GaAs VGF additionally describes using a **solid carbon source** placed outside the crucible within the sealed ampoule; on heating, this generates a carbon-bearing gas that interacts with the melt through the B₂O₃ layer — plausibly a route for **controlled carbon incorporation**, since residual carbon acts as the dominant shallow acceptor responsible for compensating the native EL2 donor in semi-insulating GaAs, making resistivity reproducible from run to run.

**Controlled solidification.** Once the charge is fully molten (except the seed), the furnace's axial temperature profile is translated downward-to-upward in a controlled manner (by sequentially reducing power in progressively higher heater zones, following a pre-computed power-vs-time schedule), causing the solid–liquid interface to advance from the seed upward through the melt. Key process parameters, per the patent and academic literature, include:

- **Temperature gradient at the melt/crystal interface:** on the order of **0.1–2 °C/cm** (deliberately kept low — this is the entire point of VGF versus LEC — to minimize thermal stress and dislocation generation)
- **Interface shape control:** the solid–liquid interface is actively kept nearly planar, with convexity/concavity controlled to within roughly **±2 mm**, since a strongly curved interface concentrates thermal stress at the crystal periphery and nucleates dislocations and twins
- **Growth (crystallization) velocity:** typically on the order of **2–16 mm/hour** — slow by Czochralski standards, consistent with minimizing constitutional supercooling and interface breakdown
- **Rotation:** unlike Czochralski, VGF crystals are not pulled, though some implementations apply slow crucible/ampoule rotation to improve radial thermal symmetry
- **Total run time:** given growth rates of a few mm/hour and boule lengths of tens of centimeters, a single VGF growth run for a production-diameter boule plausibly takes on the order of **days**, though AXT does not publish exact cycle times **[PROPRIETARY/UNKNOWN]**

**Post-growth annealing.** After solidification is complete, the boule (still inside the sealed ampoule) undergoes a controlled cool-down, and separately a **post-growth anneal** is applied to the finished ingot/wafer: heating from 900–1050 °C over 10–48 hours, then cooling to room temperature over 6–24 hours, followed by removal of a surface layer. This anneal step is documented (in the AXT patent literature) as reducing **light point defects (LPDs)** — a wafer-level defect metric relevant to epi-ready substrate quality — to fewer than 50 total defects on a 6-inch wafer at very low areal density. **[INFERRED — general crystal science]** Post-growth annealing in this temperature range also serves to homogenize residual point-defect and impurity distributions and to relax macroscopic thermal stress locked in during solidification, further reducing dislocation multiplication in subsequent epitaxial processing.

### 3.3 Material-specific considerations

**Gallium Arsenide (GaAs).**
- **[DOCUMENTED]** AXT/Tongmei offers GaAs substrates in **1-, 2-, 3-, 4-, 5-, and 6-inch diameters**, produced via VGF, and states it was first to commercialize 6-inch VGF GaAs.
- **[INFERRED — standard III-V materials engineering]** Two principal GaAs product classes are grown: **semi-insulating (SI) undoped GaAs** (resistivity ~10⁷–10⁸ Ω·cm, achieved via EL2/carbon compensation, no intentional dopant) for RF/microwave device substrates (HBT, pHEMT, MMIC power amplifiers), and **conductive, Si-doped n-type GaAs** (low EPD, ≤500 cm⁻² per the literature figure cited above) for optoelectronic devices (LEDs, VCSELs, diode lasers) where a conductive substrate enables simpler vertical device architectures and lower series resistance.
- **[DOCUMENTED]** Off-orientation (miscut) wafers — e.g., cut a few degrees off the (100) or (111)A/(111)B planes — are offered as made-to-order products, standard practice because miscut substrates promote step-flow epitaxial growth and suppress anti-phase domain formation when growing polar-on-nonpolar or otherwise mismatched epilayers.

**Indium Phosphide (InP).**
- **[DOCUMENTED]** InP substrates are offered in **2-, 3-, and 4-inch diameters**; AXT VP statements (2025–2026) describe InP as now the company's primary growth driver, serving **optical transceivers (pluggable and co-packaged optics, CPO), silicon-photonics light sources, VCSELs, and passive optical networks (PON)**, with data-center/AI-interconnect demand described as the dominant and fastest-growing application as of 2025–2026, outpacing PON.
- **[INFERRED, standard III-V melt-growth engineering, but with independent third-party quantitative corroboration]** InP is substantially harder to grow at high yield than GaAs, for two linked reasons: (1) phosphorus has a much higher equilibrium vapor pressure over molten InP than arsenic does over molten GaAs at the respective melting points, making stoichiometric/pressure control more demanding and dissociation losses more severe; and (2) InP is intrinsically more prone to twinning and dislocation generation during solidification. A third-party industry analysis states that **industry-wide single-crystal InP yields average only 20–25%**, with leading producers including AXT achieving roughly **15–20%**, and less-experienced Chinese producers **below 10%** — implying that of ~100 kg of high-purity indium feedstock, only ~10 kg becomes saleable finished product. This figure should be read as **third-party analyst estimate, not an AXT-confirmed number**, but it is directionally consistent with the well-documented difficulty of high-quality InP boule growth in the crystal-growth literature (twinning suppression via seed EPD control and crucible cone-angle optimization is an active research topic, as referenced in VGF InP growth literature).
- **[DOCUMENTED]** Historically, industrial InP has been grown by both LEC and VGF/VB; the literature explicitly documents **VGF-grown 2-inch and 4-inch low-EPD InP** with dislocation/twin control achieved via seed EPD selection and crucible cone-angle design — directly applicable to AXT/Tongmei's product range. **[INFERRED]** Given AXT's stated VGF specialization and product diameters (2–4 inch, i.e., the diameters at which VGF InP has been demonstrated in the literature) it is reasonable to infer Tongmei's InP is predominantly VGF-grown, though AXT does not explicitly confirm this is exclusively the case for InP the way it does for GaAs. **[PROPRIETARY/UNKNOWN]** whether any fraction of InP production still uses LEC.

**Germanium (Ge).**
- **[DOCUMENTED]** Ge substrates are offered in **2- and 4-inch diameters**; VP commentary (2025–2026) states Ge is a relatively small (<10%) part of AXT's business, used predominantly as the substrate for **triple-junction III-V/Ge space (satellite) solar cells**, with the company deliberately limiting exposure because gross margin is highly sensitive to volatile raw-germanium prices and because germanium export permits outside China have been difficult to obtain.
- **[INFERRED — standard practice]** Unlike GaAs and InP, germanium is an elemental (Group IV) semiconductor and does not face a stoichiometry-control problem during growth; it is essentially universally grown industrially by **Czochralski pulling** from the melt (Ge melting point 938.3 °C), a much more forgiving process than compound-semiconductor VGF/LEC given the absence of a volatile constituent. **[PROPRIETARY/UNKNOWN]** whether Tongmei uses Czochralski or a VGF/VB variant for Ge; this is not stated explicitly in the sources reviewed, though Czochralski is the overwhelmingly dominant industrial method for Ge substrate/solar-cell-grade material generally.
- **[INFERRED]** Ge substrates for triple-junction solar cells require very high crystalline perfection and controlled doping (typically Ga-doped p-type) because the Ge bottom cell is an active photovoltaic junction in the finished device, not merely a passive mechanical carrier as it sometimes is in electronic applications.

### 3.4 Comparison summary: melt-growth parameters

| Material | Melting point | Growth method | Key volatile species / control challenge | Typical AXT/Tongmei diameters |
|---|---|---|---|---|
| GaAs | 1238 °C | VGF (proprietary AXT process) | As (high vapor pressure) → B₂O₃ encapsulation + overpressure | 1"–6" |
| InP | 1062 °C | VGF (and historically LEC) | P (very high vapor pressure) → tighter pressure/stoichiometry control, twinning-prone | 2"–4" |
| Ge | 938 °C | Czochralski (inferred) | None (elemental, no dissociation) | 2"–4" |

---

## 4. From Boule to Substrate: Wafering and Finishing

**[INFERRED — this stage is universal, well-documented generic III-V wafer fab practice, and consistent with AXT's stated "wafer-processing know-how"]** After growth, the single-crystal boule proceeds through a standard sequence of mechanical and chemical operations to become a polished, epi-ready substrate wafer. AXT does not publish a detailed process flow, but the sequence below is the industry-standard chain for GaAs/InP/Ge boule-to-wafer conversion, consistent with the defect and dimensional specifications (EPD, LPD, thickness, orientation) that AXT does disclose:

1. **Boule evaluation and orientation** — X-ray diffraction (Laue back-reflection) to precisely determine crystallographic orientation before cutting, ensuring wafers are sliced to the specified on-axis or off-axis (miscut) orientation (e.g., (100), (111)A/B ± a few degrees, as AXT explicitly offers).
2. **Grinding to diameter** — the as-grown boule (whose outer surface follows the crucible/ampoule wall, not a perfectly cylindrical crystallographic form) is centerless- or OD-ground to a precise cylindrical diameter matching the target wafer spec (e.g., 100 mm, 150 mm), with a crystallographic **flat or notch** ground to indicate orientation and dopant/conductivity type per SEMI-standard convention.
3. **Wafer slicing** — the ingot is sliced into individual wafers using an **inner-diameter (ID) annular saw** or, in more modern lines, a **multi-wire saw** with abrasive slurry or fixed-abrasive wire, producing wafers at a target thickness (with saw kerf loss — typically several hundred microns per cut — being a direct yield/cost driver, especially significant for InP given its high raw-material cost).
4. **Lapping** — two-sided mechanical lapping removes saw damage and brings wafers to a controlled, uniform thickness and flatness using a hard abrasive slurry (e.g., alumina) on a rotating lapping plate.
5. **Edge profiling** — wafer edges are contoured/rounded to reduce edge chipping and particulate generation during subsequent device-fab handling.
6. **Etching** — a chemical etch (e.g., bromine-methanol or similar oxidizing acid-based etch systems for GaAs/InP) removes subsurface mechanical damage left by lapping and reveals the true crystal surface; this etch step is also frequently used analytically, since **etch-pit density (EPD)** — the standard dislocation-density metric quoted throughout this report — is measured by a defect-revealing etch followed by optical/automated pit counting.
7. **Chemical-mechanical polishing (CMP)** — one or both faces are polished to an epi-ready, sub-nanometer-roughness, damage-free finish using a colloidal-silica-type slurry, analogous in principle to silicon CMP but tuned to III-V chemistry.
8. **Cleaning and inspection** — final wet cleaning, particle/defect inspection (including the **light-point-defect (LPD)** scanning referenced in AXT's own anneal-related patent claims), thickness and bow/warp metrology, resistivity (four-point-probe or contactless eddy-current) mapping, and packaging in wafer carriers under controlled atmosphere.

**[DOCUMENTED]** AXT specifically markets a key VGF-derived advantage at this stage: because VGF produces boules with excellent diameter control, radial symmetry, and low thermal-dynamic stress, the resulting wafers can be processed to **ultra-thin final thickness (≥100 microns) without backside lapping after epitaxy** — i.e., the substrate does not need to be thinned post-epi (a step commonly required for LEDs/VCSELs to reduce series resistance or facilitate cleaving/dicing), because VGF material's low internal stress tolerates a thin starting wafer through the epitaxy thermal cycle without excessive bow or breakage. This is presented as a direct cost/yield advantage passed to downstream device customers.

**[PROPRIETARY/UNKNOWN]** Exact slurry chemistries, polish pad recipes, specific etchant formulations, and metrology tool models used by Tongmei are not publicly disclosed, as is standard for all substrate suppliers in this industry (these represent significant trade-secret IP even though the general unit-operation sequence above is public knowledge).

---

## 5. Downstream: Epitaxy, Device Fabrication, and Packaging

It is important to be precise about **where Tongmei's own manufacturing chain ends**, because this bears directly on how to describe the "materials-to-devices" chain accurately.

**[DOCUMENTED]** Tongmei/AXT is a **substrate (wafer) supplier**, not (based on all sources reviewed) an integrated device manufacturer, epitaxy house, or OSAT (outsourced assembly and test) company. AXT explicitly states: *"Our customers manufacture LEDs, electronic devices for switches, power amplifiers and laser diodes"* — i.e., Tongmei sells finished, polished, epi-ready substrate wafers to external customers who then perform epitaxial growth and device fabrication. This has been true across AXT's history; a 2006 filing lists customers including **Avago Technologies, IQE, MBE Technology, Osram Opto Semiconductors, Picogiga International, Sumika Epi Solution, Visual Photonics Epitaxy Co., and Xiamen Shanan Semiconductor** — a roster dominated by **epitaxy foundries and optoelectronic-device makers**, confirming the substrate-supplier positioning. More recent commentary (2025–2026) describes end-customers as "multiple US hyperscalers" (via their optical-module suppliers) and does not indicate any move by AXT/Tongmei into epitaxy or device fabrication itself.

Accordingly, the remainder of the materials-to-devices chain described below is **industry-general context for how Tongmei's substrates are subsequently used**, not a description of Tongmei's own operations, and is marked as such.

### 5.1 Epitaxy (external to Tongmei) — **[INFERRED / general industry context]**

Once a Tongmei GaAs, InP, or Ge wafer reaches an epitaxy house or an integrated device manufacturer, thin functional layers are grown on top by:

- **Metalorganic Chemical Vapor Deposition (MOCVD)** — the dominant technique for high-volume compound-semiconductor epitaxy (LEDs, VCSELs, HBTs, laser diodes), using metalorganic precursors (e.g., trimethylgallium, trimethylindium) and hydride gases (arsine, phosphine) in a heated reactor. Public patent literature co-authored/assigned in this space (including doping-control patents referencing InP substrates) documents precisely this kind of MOCVD process for InP-based laser epitaxy — trimethylindium plus phosphine plus a silane dopant source, laminar-flow reactor.
- **Molecular Beam Epitaxy (MBE)** — used for the most demanding heterostructure and quantum-well devices (high-performance HEMTs, VCSELs, some laser structures) where atomic-layer thickness/composition control is paramount.

The choice of substrate polarity, orientation, and off-cut angle (which, as noted, Tongmei offers as a made-to-order option) is dictated by the epitaxial device architecture the customer intends to grow — e.g., specific miscut angles are used to control ordering phenomena and surface morphology in InGaAsP/InP laser heterostructures, or to avoid anti-phase domains in polar-on-nonpolar systems.

### 5.2 Device fabrication and packaging — **[INFERRED / general industry context]**

After epitaxy, standard compound-semiconductor front-end processing (photolithography, dry/wet etching, metallization/ohmic contact formation, passivation) defines individual devices such as:

- **GaAs-substrate devices**: RF power amplifier MMICs/HBTs/pHEMTs for mobile handsets and wireless infrastructure; VCSELs for 3D sensing and short-reach datacom; LEDs for lighting/display/infrared illumination; edge-emitting laser diodes (e.g., for printer heads, industrial lasers).
- **InP-substrate devices**: long-wavelength edge-emitting lasers (DFB, EML — electro-absorption modulated lasers) and photodiodes for telecom/datacom optical transceivers; InP HEMTs for >100 GHz applications in defense/satellite communications; increasingly, laser dies that are flip-chip or hybrid/heterogeneously bonded onto **silicon-photonic integrated circuits**, since silicon itself cannot efficiently generate laser light (indirect bandgap) and must borrow direct-bandgap III-V gain material — a structural reason cited by industry analysts for why silicon-photonics adoption *increases* rather than eliminates InP demand.
- **Ge-substrate devices**: the germanium wafer serves as both mechanical substrate and the bottom sub-cell of a **lattice-matched triple-junction (e.g., InGaP/InGaAs/Ge or similar) solar cell**, subsequently packaged into radiation-hardened solar panels for satellites.

Devices are then diced, die-attached, wire-bonded or flip-chip bonded, and packaged (TO-can, butterfly, QSFP/pluggable transceiver modules for optics; overmolded packages for RF PAs; cover-glass-and-interconnect assembly for space solar cells) by OSAT and module-assembly companies — again, entities **external to and downstream of Tongmei**.

### 5.3 Commercial end-products incorporating Tongmei-derived material — **[DOCUMENTED, as stated end-market categories; specific device identity is inferred]**

AXT explicitly lists the following end markets as consuming substrates derived from this chain:

- 5G wireless infrastructure (GaAs RF PAs)
- Data-center optical connectivity / silicon photonics (InP lasers and photodetectors)
- Passive optical networks, PON (InP)
- LED lighting and display (GaAs, GaAs-based ternaries)
- Industrial and sensing lasers, LiDAR (GaAs, InP)
- 3D-sensing VCSELs (GaAs)
- Cell-phone power amplifiers (GaAs)
- Satellite/space solar cells (Ge)
- Co-packaged optics (CPO) and pluggable optical transceivers for AI data-center interconnect (InP) — the fastest-growing category as of 2025–2026

---

## 6. Quality Metrics and Specifications: What "High Performance" Means Here

**[DOCUMENTED / general III-V metrology, consistent with AXT's specific marketing claims]** The substrate industry (and AXT specifically, per its own technical marketing) qualifies wafers against several key metrics, each traceable to a specific growth or processing control:

| Metric | What it measures | Why it matters | Process lever |
|---|---|---|---|
| **Etch Pit Density (EPD)** | Dislocation density (dislocations/cm²), revealed by defect-selective chemical etch and optically counted | Dislocations degrade minority-carrier lifetime, laser-diode reliability/lifetime, and can propagate into epi layers | Growth method (VGF vs. LEC), axial/radial thermal gradient control, interface shape control |
| **Light Point Defects (LPD)** | Sub-surface/near-surface point-like scattering defects detected by laser surface scanning | Nucleation sites for epitaxial defects; affects device yield | Post-growth anneal profile, polishing quality |
| **Resistivity (SI GaAs)** | Bulk electrical resistivity, target ~10⁷–10⁸ Ω·cm | Required for RF device isolation | EL2/carbon compensation control, raw-material purity |
| **Diameter/flatness/bow/warp** | Dimensional and geometric wafer metrology | Compatibility with automated epi and fab tool handling (SEMI standards) | Growth diameter control (a stated VGF strength), lapping/polishing uniformity |
| **Surface roughness** | Sub-nm RMS roughness after CMP | Epitaxial nucleation quality, especially critical for MBE | CMP process/slurry |
| **Twin/grain-boundary freedom** | Absence of secondary crystal orientations (especially relevant for InP) | A twinned or polycrystalline boule cannot yield usable single-crystal wafers, directly setting yield | Seed EPD, crucible cone-angle design, interface control |

**[INFERRED]** The **InP yield problem** described in Section 3.3 (15–20% single-crystal yield even for leading producers) is best understood as primarily a **twinning and dislocation-nucleation yield loss** at the crystal-growth stage — i.e., much of the ~80% loss occurs before wafering even begins, when the growth run itself produces boule sections that are twinned, polycrystalline, or too heavily dislocated to qualify, rather than being wafering/polishing scrap. This is consistent with the well-documented sensitivity of InP (relative to GaAs) to twin formation during solidification.

---

## 7. Geopolitical and Supply-Chain Context (Directly Material to the Manufacturing Chain)

**[DOCUMENTED]** Because Tongmei's entire crystal-growth and raw-material operation is China-based, and because gallium, germanium, and (as of 2025) indium/tellurium/tungsten/bismuth/molybdenum have become subject to **Chinese export licensing controls**, Tongmei's position in the value chain has become a live regulatory chokepoint rather than a purely technical/economic one:

- **August 1, 2023**: China implemented export controls on gallium and germanium (announced July 3, 2023); Tongmei received initial export permits to resume GaAs and Ge substrate shipments to certain customers in September 2023.
- **February 4, 2025**: China's Ministry of Commerce and General Administration of Customs imposed export controls covering items related to **tungsten, tellurium, bismuth, molybdenum, and indium** — directly affecting InP substrate exports (since InP substrates are, definitionally, indium-bearing).
- **June 2025**: Tongmei received initial export permits to resume InP substrate shipments to certain customers.
- Germanium substrate export permits **outside China** have remained comparatively difficult to obtain through 2025, and AXT management has noted the germanium substrate market has "very poor gross margin potential" today given raw germanium price volatility and the administrative burden of licensing, leading the company to deliberately limit its exposure to that product line.
- Each individual export shipment/customer reportedly requires **specific permitting**, with InP permits taking approximately **60 business days (~3 months)** to process, per AXT management commentary — meaning the "vertically integrated" advantage AXT built to avoid supply risk in the 2000s–2010s did **not** protect the company from a categorically different risk (state export-licensing delay) that emerged in the 2020s.

**[INFERRED]** This context is directly relevant to a technical review because it means Tongmei's *effective* production capacity and *shippable* output can diverge significantly quarter to quarter — the crystal-growth and wafering technology described in Sections 3–4 may be running at stable rates while commercial shipment volumes swing sharply based on permit issuance timing, a dynamic explicitly visible in AXT's 2025–2026 quarterly revenue figures (e.g., $18M → $28M → $23M across consecutive quarters).

---

## 8. Synthesis: The Complete Value Chain as Documented

```
┌─────────────────────────────────────────────────────────────────────┐
│  UPSTREAM: RAW MATERIAL PURIFICATION  (Tongmei-affiliated JVs)      │
│  Ga ore/byproduct → 4N→6N/7N Ga  |  As →4N-7N  |  Ge, GeO2           │
│  In refining (from 2026)  |  pBN crucible synthesis  |  B2O3         │
└───────────────────────────────┬───────────────────────────────────────┘
                                 │  [Tongmei owns/co-owns this tier]
┌───────────────────────────────▼───────────────────────────────────────┐
│  CRYSTAL GROWTH  (Tongmei core operation — VGF, LEC-legacy, Cz-Ge)   │
│  Poly charge + seed → sealed pBN crucible → multi-zone furnace       │
│  → controlled axial gradient translation → single-crystal boule      │
└───────────────────────────────┬───────────────────────────────────────┘
                                 │  [Tongmei operation]
┌───────────────────────────────▼───────────────────────────────────────┐
│  WAFERING & FINISHING  (Tongmei core operation)                      │
│  Orient → OD grind → slice → lap → edge-profile → etch → CMP →      │
│  clean → metrology → ship as polished substrate wafer                │
└───────────────────────────────┬───────────────────────────────────────┘
                                 │  [Product boundary: Tongmei SELLS here]
┌───────────────────────────────▼───────────────────────────────────────┐
│  EPITAXY  (external customers: IQE-type foundries, integrated IDMs)  │
│  MOCVD / MBE growth of device heterostructures on Tongmei substrate  │
└───────────────────────────────┬───────────────────────────────────────┘
                                 │  [External to Tongmei]
┌───────────────────────────────▼───────────────────────────────────────┐
│  DEVICE FABRICATION  (external: fabless/IDM device makers)           │
│  Lithography, etch, metallization → RF PAs, VCSELs, lasers, LEDs,    │
│  photodiodes, triple-junction solar cells                            │
└───────────────────────────────┬───────────────────────────────────────┘
                                 │  [External to Tongmei]
┌───────────────────────────────▼───────────────────────────────────────┐
│  PACKAGING / MODULE ASSEMBLY  (external: OSATs, module integrators)  │
│  Optical transceiver modules, RF PA modules, solar panel assemblies  │
└───────────────────────────────┬───────────────────────────────────────┘
                                 │
┌───────────────────────────────▼───────────────────────────────────────┐
│  END SYSTEMS: AI data-center optics, 5G handsets/basestations,       │
│  LiDAR/3D sensing, satellite power systems, lighting/display          │
└─────────────────────────────────────────────────────────────────────┘
```

**Tongmei's documented vertical integration spans the top three boxes** (raw material through finished substrate) — this is the genuinely distinctive part of its business model relative to substrate-only competitors that buy elemental feedstock on the open market. It does **not**, per the public record, extend into epitaxy or device fabrication.

---

## 9. Key Uncertainties and Explicitly Unknown Items

For completeness, the following are **not resolvable from public sources** and should not be treated as established:

- Exact furnace design (zone count, heater technology, control-loop architecture) used in current Tongmei production, beyond what is disclosed in AXT-assigned patents (which describe representative, not necessarily current, tooling).
- Whether InP growth today is 100% VGF or retains any LEC capacity.
- Growth method used for Ge (Czochralski is the industry default and the best-supported inference, but not explicitly confirmed for Tongmei).
- Precise yield figures for GaAs and Ge growth (only InP yield estimates were found, and those are third-party analyst figures, not AXT-published data).
- Detailed dopant schedules, exact pBN crucible geometry/cone-angle specifications, exact anneal recipes, and CMP slurry chemistry — all standard trade secrets industry-wide.
- Current (2026) allocation of GaAs/InP/Ge production across the three manufacturing sites following the Dingxing relocation.
- Whether the 8N-purity gallium claim found in third-party analyst material reflects an actual current Tongmei/JinMei capability or is an overstatement; AXT's own filings top out at explicitly stated 7N.

---

## 10. Key References

1. AXT, Inc. Form 10-K, fiscal year 2024, U.S. Securities and Exchange Commission (raw-material joint-venture structure, product lines, facilities). https://www.sec.gov/Archives/edgar/data/1051627/000155837025003004/axti-20241231x10k.htm
2. AXT, Inc. Form 8-K, June 11, 2025 (InP export permit restoration). https://www.sec.gov/Archives/edgar/data/1051627/000143774925020087/axti20250611_8k.htm
3. AXT, Inc. Preliminary Information Document / Reply to Second Round Audit Inquiry Letter, Beijing Tongmei Xtal Technology STAR Market IPO filings, SEC Form 8-K exhibits, 2022. https://www.sec.gov/Archives/edgar/data/1051627/000155837022010098/axti-20220617xex99d1.htm
4. AXT, Inc. Form 424B5, 2006 (early joint-venture structure, customer list). https://www.sec.gov/Archives/edgar/data/0001051627/000104746906014641/a2174037z424b5.htm
5. AXT, Inc., "Tongmei Receives Initial Export Permits from China's Central Ministry of Commerce for Gallium Arsenide and Germanium Substrates," GlobeNewswire, September 20, 2023.
6. AXT, Inc., "AXT Announces Purchase of New Manufacturing Facility in Dingxing, China," press release.
7. AXT, Inc. corporate/product description, semiconductor materials distributor listing (VGF process description, facility size, product diameters). https://abachy.com/catalog/materials/crystal-growing-materials/process-chamber-components/pyrolitic-boron-nitride-pbn/axt-inc
8. Birkmann, B. et al., "Growth of 3″ and 4″ gallium arsenide crystals by the vertical gradient freeze (VGF) method," *Journal of Crystal Growth*, 211 (2000) 157–163.
9. Jurisch, M. et al. (as cited in VGF process-control literature), on VGF/Bridgman-type growth of GaAs and InP.
10. U.S. Patent, "Low etch pit density (EPD) semi-insulating III-V wafers" (AXT-assigned), method for 6-inch VGF GaAs growth with carbon-gas interaction and post-growth anneal specification. https://image-ppubs.uspto.gov/dirsearch-public/print/downloadPdf/8361225
11. U.S. Patent, "Method and system for vertical gradient freeze 8 inch gallium arsenide substrates" (AXT-assigned). https://image-ppubs.uspto.gov/dirsearch-public/print/downloadPdf/12398486
12. U.S. Patent, "Doping control in selective area growth (SAG) of InP epitaxy in the fabrication of solid state semiconductor lasers" (MOCVD doping-control process for InP-based lasers). https://image-ppubs.uspto.gov/dirsearch-public/print/downloadPdf/6245144
13. Growth and characterization of 2″ and 4″ low-EPD InP substrate crystals by the Vertical Gradient Freeze (VGF) method (twin-free 4″ semi-insulating InP; seed EPD and crucible cone-angle effects), as referenced in ResearchGate/ScienceDirect VGF crystal-growth literature summaries.
14. Semiconductor Today, "AXT's Q3 revenue far exceeds guidance, after China export licenses granted for InP," November 10, 2025. https://www.semiconductor-today.com/news_items/2025/nov/axt-101125.shtml
15. Semiconductor Today, "AXT's revenue grows 17% in Q1 after greater-than-expected export permits," May 5, 2026. https://www.semiconductor-today.com/news_items/2026/may/axt-050526.shtml
16. Yahoo Finance / Needham Conference coverage, "AXT Touts Surging Indium Phosphide Demand for AI Data Centers... Amid Export Curbs," January 15, 2026 (VP Tim Bettles technical/market commentary on GaAs and InP applications).
17. Global Semi Research (Substack), "AXT: The Indium Phosphide Play for AI's Optical Interconnect Transition," April 18, 2026 (third-party analyst estimate of InP single-crystal yield rates — cited here as analyst opinion, not AXT-confirmed data).
18. SemiconductorX, "GaAs & InP Wafers" technical/market overview (VGF vs. LEC dislocation-density rationale, MOCVD precursor supply-chain linkage). https://semiconductorx.com/wafer-production-gaas-inp.html
19. CB Insights, "Tongmei Crystal Technology — Products, Competitors, Financials, Employees, Headquarters Locations" company profile.
20. PatSnap, "AXT, Inc.: Company Profile & Technical Research" (patent portfolio and JV entity listing, including Boyu Chaoyang/Tianjin and Chaoyang Jinmei entities). https://discovery.patsnap.com/company/axt/

---

*This report was compiled from publicly available corporate filings, patents, press releases, and secondary industry/analyst commentary current as of July 2026. Where information was unavailable or explicitly proprietary, this has been flagged rather than inferred beyond the bounds of standard materials-science and crystal-growth engineering practice.*

---

> [!NOTE]
> 
> Generated by Claude.ai
>
> Model: Sonet 5
>
> Prompt: 
