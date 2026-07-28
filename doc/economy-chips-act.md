# The EU Chips Act 2.0 and the Critical Raw Materials Act: Implications for the Compound Semiconductor Bulk Crystal Growth Industry

**A technical–policy assessment for producers of melt-grown single crystals and wafers (Si, Ge, GaAs, InP, GaP, InAs, GaSb, InSb, CdTe, CdZnTe)**

*Prepared July 2026*

---

## 1. Executive Summary

The European Union's semiconductor industrial policy has entered a second legislative cycle. The original **European Chips Act** (Regulation (EU) 2023/1781, in force since 21 September 2023) mobilised roughly €43 billion in public and private investment with the explicit target of doubling the EU's share of global semiconductor production to 20% by 2030. On **3 June 2026**, the European Commission adopted a **proposal for "Chips Act 2.0"** as part of a broader "European Technological Sovereignty Package," alongside a proposed **Cloud and AI Development Act (CADA)** and an EU Open Source Strategy. Chips Act 2.0 is explicitly framed as a correction to the "lab-to-fab" gap exposed by the first Act — the observation that European strength in semiconductor R&D (imec, CEA-Leti, Fraunhofer) has not translated into commensurate industrial-scale manufacturing capacity, and that the 20%-by-2030 target is very unlikely to be met on the current trajectory.

In parallel, the **Critical Raw Materials Act** (Regulation (EU) 2024/1252, "CRMA," in force since 23 May 2024) establishes a framework of 2030 benchmarks (≥10% domestic extraction, ≥40% domestic processing, ≥25% recycling, ≤65% import concentration from any single third country) for 34 "critical" and 17 "strategic" raw materials. **Gallium and germanium** — the two elements of most direct relevance to III-V and IV-IV compound semiconductor crystal growth — sit on both lists. This is not incidental: China's July 2023 export-licensing regime on gallium and germanium (tightened to an outright ban on exports to the US in December 2024) is the immediate geopolitical trigger that gave the CRMA's raw-material provisions real teeth for the compound semiconductor supply chain, and it is frequently cited in Commission and industry-association documents as the paradigm case of "critical raw material weaponisation."

For an industry built on Czochralski (CZ), Liquid-Encapsulated Czochralski (LEC), Vertical Gradient Freeze (VGF), horizontal and vertical Bridgman, and related melt-growth techniques — i.e., companies pulling or freezing boules of Si, Ge, GaAs, InP, GaP, InAs, GaSb, InSb, CdTe and CdZnTe — these two legislative instruments matter in different but complementary ways:

- **Chips Act 2.0** is primarily a *demand-and-capacity* instrument: it is trying to fix weak downstream pull (fabs, packaging, "First-of-a-Kind" and "Strategic Projects" across the value chain "from materials to advanced packaging") and to accelerate permitting for capital-intensive manufacturing facilities, of which crystal-growth and wafering plants are a foundational, capital-intensive tier.
- **CRMA** is primarily a *feedstock security* instrument: it targets the upstream elemental and compound precursor supply (Ga metal, Ge metal/GeO₂, As, Sb, In) on which GaAs, InP, GaSb, InSb, and CdTe/CZT growth depend, and creates a permitting, financing, and stockpiling architecture around "Strategic Projects."

This report analyses both instruments in detail, maps them onto the technical realities of melt-growth crystal production, profiles the European (and adjacent) companies actually engaged in CZ/LEC/VGF/Bridgman growth of these materials, and assesses where the policy architecture helps, where it is silent, and where structural gaps remain (notably: neither instrument contains material-specific, growth-technology-specific support comparable to, e.g., the US CHIPS Act's explicit substrate provisions, and the CRMA's Strategic Projects are overwhelmingly weighted toward battery/magnet/PGM materials rather than semiconductor-grade Ga/Ge/In/As/Sb refining).

---

## 2. From the Original Chips Act to Chips Act 2.0: Legislative Evolution

### 2.1 The 2023 European Chips Act — structure and record

Regulation (EU) 2023/1781 ("European Chips Act") rests on three pillars:

1. **Chips for Europe Initiative** — €3.3 billion of Union-level funding (Horizon Europe + Digital Europe Programme reallocations) for pilot lines, design platforms, competence centres, and a semiconductor skills academy, administered largely through the **Chips Joint Undertaking (Chips JU)**, the successor to the KDT/ECSEL Joint Undertakings.
2. **Framework for security of supply / "First-of-a-Kind" (FOAK) facilities** — a state-aid and permitting mechanism allowing Member States to fast-track approval and support for "Integrated Production Facilities" (IPFs) and "Open EU Foundries" (OEFs) that are novel to Europe, in exchange for supply-priority commitments during a crisis.
3. **Monitoring and crisis-response mechanism** — an early-warning system, a European Semiconductor Board (Member State coordination), and emergency toolbox for crisis conditions (comparable in spirit to the mechanism the CRMA later adopted for raw materials).

By early 2026, the Commission's own accounting cited **over €80 billion** in public-plus-private investment triggered under the Act's framework since 2023 (a figure that includes flagship logic/memory fabs such as Intel's paused/rescoped Magdeburg project, TSMC's Dresden joint venture ESMC, Infineon's Dresden expansion, STMicroelectronics/GlobalFoundries in Crolles, and ZF/Bosch/Infineon SiC and GaN power-device investments) — but independent assessments (Bruegel, ESIA/SEMI Europe policy notes cited in the 2026 impact assessment) converged on the conclusion that the **20%-of-global-capacity-by-2030 target will not be reached**, with realistic estimates in the low-to-mid teens. The gap is disproportionately concentrated in **leading-edge logic** (sub-5nm) and in translating Europe's genuine strength in materials, equipment, and compound-semiconductor R&D into volume manufacturing.

### 2.2 The Chips Act 2.0 proposal (3 June 2026)

The Commission's proposal, published together with its Annexes and a three-part Impact Assessment, restructures the Chips for Europe Initiative into **"Chips for Europe Initiative 2.0"** and introduces several new instruments. According to the Commission's own summary and contemporaneous industry-association analysis (Aeneas, SEMI, eeNews Europe), the proposal is organised around four priorities:

1. **Improving investment conditions and competitiveness** — including new financing instruments and continuation of the IPF/OEF state-aid framework.
2. **Strengthening research, innovation and skills** across the semiconductor ecosystem — an extension of Chips JU pilot lines and competence centres.
3. **Accelerating permitting** — a hard target of **maximum 12 months** for permitting approvals, and a new **"Semiconductor Regions of Excellence"** label intended to help regional manufacturing clusters (many of which — Grenoble/Crolles, Dresden/Saxony's "Silicon Saxony," Traunreut, Villach, and various Nordic sites — already host crystal-growth or epitaxy capacity) attract co-investment.
4. **Boosting demand and international cooperation** — including new **"Demand Accelerators"**, public/innovation procurement rules, **"Grand Challenges"** for AI-relevant chips, and expanded **Strategic Partnerships on Semiconductors** with third countries.

Two provisions are of particular structural interest to bulk-crystal producers:

- **"First-of-a-Kind" and "Strategic Projects" spanning the *full value chain*, explicitly including "materials"** — a widening of scope relative to the original Act, which was drafted with fab-centric (front-end logic/memory) facilities primarily in mind. The proposal's own framing — "Supporting 'First-of-a-Kind' projects across the semiconductor value chain, from materials to advanced packaging" — is the clearest textual hook by which a compound-semiconductor substrate producer (rather than only a wafer fab) could in principle access IPF/FOAK-style state-aid clearance and streamlined permitting.
- **Synergy with the Cloud and AI Development Act (CADA)** for data-centre/AI-accelerator demand — relevant less to III-V melt growth directly and more to the Si and (increasingly) SiC/GaN power and RF ecosystem that surrounds AI infrastructure, but indirectly relevant insofar as GaAs and InP photonic/RF substrates feed optical interconnect and mmWave components inside AI data-centre fabric.

As of this writing (28 July 2026), the Chips Act 2.0 proposal — like the parallel CADA proposal — is a Commission text that must still complete the ordinary legislative procedure (European Parliament and Council co-decision), so its final scope, funding envelope, and binding force remain subject to negotiation. Companies should treat the specific instruments described above as *directionally reliable but not yet legally final*.

### 2.3 What Chips Act 2.0 does *not* do for bulk-crystal growers

It is important to be precise about the limits of the proposal from a substrate producer's point of view:

- There is, as of the June 2026 text, **no dedicated funding line, tax instrument, or state-aid category specific to compound-semiconductor substrate or bulk-crystal manufacturing** (unlike, for instance, targeted US CHIPS and Science Act guidance documents and NDAA provisions that explicitly discuss substrate/materials supply chains). Substrate makers must qualify under the general FOAK/IPF/Strategic Project criteria applicable to any "novel-to-Europe" facility.
- The 12-month permitting target and Regions of Excellence label are **generic instruments** that apply equally to a logic fab, a SiC power-device line, or (potentially) a GaAs/InP boule-growth and wafering plant — there is no guarantee that crystal-growth facilities, which are far smaller in footprint and capital intensity than a leading-edge logic fab, will be prioritised in the same way.
- The demand-side measures (Demand Accelerators, Grand Challenges, procurement rules) are oriented toward **chip products** (AI accelerators, mainstream logic) rather than upstream **substrate materials** — a GaAs/InP/GaSb wafer producer sells to III-V fabs and epitaxy houses (e.g., IQE, EpiGaN/Soitec, in-house epi lines at IIVI/Coherent, Sumitomo Electric, or defence/space primes), not directly into the "chip demand" the Act is designed to stimulate.

---

## 3. The Critical Raw Materials Act (CRMA): Structure and Relevance to Compound Semiconductor Feedstocks

### 3.1 Legal architecture

Regulation (EU) 2024/1252 was adopted 11 April 2024 and entered into force 23 May 2024. Its core architecture:

- **34 Critical Raw Materials (CRMs)** and, within that list, **17 Strategic Raw Materials (SRMs)** subject to enhanced obligations (Annex I/II definitions updated periodically; the most recent update, referenced in Commission communications around late 2025, refreshed both lists).
- **2030 domestic-capacity benchmarks**: ≥10% of annual EU consumption from domestic extraction, ≥40% from domestic processing, ≥25% from recycling, and **no more than 65% of annual consumption sourced from any single third country** for any SRM.
- **Strategic Projects mechanism**: projects (extraction, processing, recycling, or substitution) that meet technical, environmental, and strategic criteria may be designated "Strategic Projects," unlocking streamlined permitting (statutory deadlines: 27 months for extraction projects, 15 months for processing/recycling projects), enhanced access to EU financing instruments (InvestEU, the CRM Facility under the "Chips and Raw Materials" pillar of the "Scaling up" instruments, and Member State co-financing), and priority regulatory treatment.
- **National programmes for strategic stockpiling**, joint purchasing mechanisms, and a **Critical Raw Materials Board** (Member States + Commission) for coordination, monitoring, and crisis response — structurally parallel to the Chips Act's European Semiconductor Board.

Gallium and germanium are on **both** the Critical and Strategic lists. Arsenic and antimony are on the Critical list (not Strategic). Indium and tellurium — both essential to InP, InAs, InSb, CdTe, and CdZnTe growth — are **not** on either list as of the current designation, a gap discussed further in §5.

### 3.2 Why gallium and germanium specifically matter to melt-growth producers

- **Gallium** is the group-III constituent of GaAs, GaP, GaSb, and (via alloying) InGaAs/InGaP — i.e., it is a direct feedstock for LEC- and VGF/Bridgman-grown III-V boules, not merely an epitaxial dopant. High-purity (6N–7N) gallium metal is the precursor from which polycrystalline GaAs (via the horizontal Bridgman "boat" synthesis route or direct-synthesis-then-LEC approach) is synthesised before single-crystal pulling.
- **Germanium** is (a) a melt-grown elemental semiconductor in its own right (CZ-Ge substrates for III-V multi-junction solar cells and infrared optics), and (b) — critically for GaAs LEC growth — germanium and its compounds are used in some doping schemes, while high-purity Ge is separately essential to infrared optics (lenses, IR windows) often produced by the same specialty-materials companies that also grow II-VI and III-V crystals (e.g., II-VI/Coherent's germanium optics business alongside its CdZnTe/CdTe growth operations).
- China's dominance is stark and well documented: **~90–98% of global gallium production** and **~60–83% of global germanium production** (depending on year and whether "low-purity primary production" or "refined/high-purity" is measured) are Chinese, with China's exports historically accounting for roughly **71% of EU gallium imports** and a comparable majority of EU germanium imports pre-2023.

### 3.3 The China export-control shock (2023–2025) as the CRMA's proximate cause

On **3 July 2023**, China's Ministry of Commerce (MOFCOM) and General Administration of Customs announced a licensing regime — effective 1 August 2023 — requiring export licences (with disclosed end-user and end-use) for gallium and germanium metals and specified compounds (including gallium arsenide and germanium epitaxial-substrate-related items in some product codes). This was followed on **20 October 2023** by analogous controls on graphite, and on **15 September 2024** by controls on antimony. On **3 December 2024**, China announced an outright **export ban to the United States** on gallium, germanium, and antimony, in direct response to a further round of US semiconductor export controls.

Documented downstream effects relevant to this industry:

- **Price shocks**: European gallium spot prices rose roughly **68%** in the months following the July 2023 announcement (versus an ~18% rise in the US), and germanium metal prices more than doubled by 2024 relative to pre-control levels (reported figures around **US $3,000+/kg**, versus roughly $1,300–1,500/kg pre-2023).
- **Trade diversion / "backdoor" flows**: US Geological Survey and trade-flow analyses (Stimson Center, 2026) show germanium exports to the US falling to officially zero while Chinese germanium exports to **Belgium** rose by roughly 224% over the same period — strongly suggesting re-export through the EU, with Belgium's Umicore-anchored germanium refining and recycling capacity as the plausible transhipment/processing node.
- **Industry association response**: **SEMI Europe** issued a formal comment on the export-licence regime (reflecting the concerns of 300+ European member companies in the microelectronics supply chain), concluding that in the **short term** no acute supply disruption was expected for the EU compound-semiconductor industry, because (a) gallium and germanium are not geologically scarce and can be produced or recovered in Europe/the US, and (b) absolute EU consumption volumes for GaAs/Ge-substrate-grade material are small relative to aluminium-smelting-byproduct gallium capacity globally — but the association flagged the **medium-term structural dependency** on Chinese refining capacity and pricing dominance as the real risk, precisely the dependency the CRMA benchmarks are designed to address.
- **AXT / Tongmei exposure**: US-headquartered AXT Inc., a major global GaAs and germanium substrate supplier and a direct competitor to European producers such as Freiberger Compound Materials, manufactures substantially all of its substrate product in China through its subsidiary Tongmei, which also produces high-purity gallium raw material; Tongmei had to separately seek export permits for GaAs and Ge substrates under the licensing regime, illustrating that even nominally "non-Chinese" global suppliers can have Chinese-jurisdiction manufacturing and raw-material exposure.

### 3.4 CRMA Strategic Projects directly relevant to Ga/Ge

As of the **25 March 2025** designation round (47 Strategic Projects across 13 Member States; expanded in later rounds toward ~60 projects), the projects of most direct relevance to compound-semiconductor feedstock are:

| Project | Promoter | Country | Type | Material |
|---|---|---|---|---|
| **GePETO** | Umicore | Belgium | Processing | Germanium |
| **ReGAIN** | Umicore | Belgium | Substitution | Germanium (substitution/reduced-use) |

Notably, **gallium-specific refining/processing Strategic Projects in the EU are comparatively few** relative to battery-material projects (lithium, nickel, cobalt, graphite, manganese dominate the 47-project list). Germany's **Ingal Stade GmbH** announced plans (outside the formal CRMA Strategic Project list, but consistent with its objectives) to restart primary gallium production, historically a European capability that lapsed once Chinese low-cost gallium (recovered as a bauxite/alumina-refining byproduct) made Western primary production commercially unviable in the 1990s–2000s. The Commission's own consilium.europa.eu communications project that, *if* the designated projects are fully realised, EU gallium import dependency could fall from ~71% to ~17% and germanium could reach full EU self-sufficiency by 2030 — but these are policy aspirations tied to project completion, not present-day supply security.

### 3.5 What CRMA does *not* cover for this industry

- **Indium** (InP, InAs, InSb feedstock) and **tellurium** (CdTe, CdZnTe feedstock) are absent from both the Critical and Strategic lists in the current designation, despite indium's well-documented supply concentration (China dominant; also produced as a zinc-refining byproduct in Korea, Canada, Belgium) and tellurium's extreme scarcity and by-product status (recovered mainly from copper-refining anode slimes). This is a material gap for InP-based photonics/RF substrate producers (e.g., for telecom lasers, and for space-qualified multi-junction solar cell substrates) and for CdTe/CZT producers serving both photovoltaic (CdTe thin-film PV, where the *device* material is chemically vapour-deposited rather than melt-grown, but which competes for the same tellurium pool) and radiation-detector (CZT gamma/X-ray detector) markets.
- **Arsenic** and **antimony** are Critical (not Strategic) raw materials — meaning they benefit from monitoring and some streamlined provisions but do not receive the enhanced financing/stockpiling treatment SRM status confers, despite arsenic being the group-V feedstock for GaAs, InAs, and GaAs-based synthesis, and antimony being essential to InSb and GaSb.
- The CRMA's benchmarks and Strategic Project mechanism are **overwhelmingly weighted toward battery, magnet, and platinum-group-metal supply chains** (consistent with the EU's parallel decarbonisation and defence-electrification priorities) rather than semiconductor-grade high-purity (6N+) material. A refined-metal Strategic Project targeting battery-grade nickel says little about whether 7N-purity Ga metal (the grade actually required for LEC/VGF GaAs growth, as opposed to Ga metal for gallium-based alloys or LED epitaxy) will be available at competitive cost in the EU.

---

## 4. The European (and Adjacent) Melt-Growth Compound Semiconductor Landscape

This section maps the actual industrial base the two Acts are meant to serve.

### 4.1 Silicon (CZ, FZ)

While silicon is not "critical" in the CRMA sense (silicon metal is on the *Strategic* list as a feedstock for solar/battery-grade silicon and ferrosilicon, not semiconductor-grade polysilicon specifically), European CZ-Si capability is concentrated in:

- **Siltronic AG** (Munich/Burghausen, Germany; also fabs in Singapore and the US) — one of the world's top-five CZ-silicon wafer producers, spanning 200mm and 300mm, and a direct beneficiary of Chips Act-linked German state aid for its planned 300mm fab expansions.
- **Soitec** (Bernin, France) — SmartCut/SOI wafer technology, not itself a bulk CZ grower at large scale but deeply integrated with CEA-Leti and French Chips Act-adjacent funding.
- Silicon feedstock (polysilicon, metallurgical-grade silicon) is where the CRMA's "silicon metal" strategic designation actually bites — Wacker Chemie (Burghausen) is the principal EU polysilicon/hyperpure-silicon producer and is the material link between CRMA silicon-metal provisions and Siltronic's CZ pulling operations.

### 4.2 Germanium (CZ) and the II-VI/optics-adjacent producers

- **Umicore** (Belgium) is the dominant EU germanium refiner/recycler (GePETO and ReGAIN Strategic Projects) but is principally a chemicals/materials and recycling company rather than a CZ-Ge crystal grower in the boule-pulling sense; it supplies germanium dioxide, germanium tetrachloride (optical fibre precursor), and refined germanium metal feedstock to downstream crystal growers.
- **Umicore's germanium substrate business** (historically supplying CZ-grown Ge wafers for III-V multi-junction solar cells used in space and concentrator-PV applications) sits within the same corporate group as its refining/recycling operations — a rare example of a European company spanning both CRMA-relevant upstream refining and actual melt-growth substrate production.
- **AXT Inc.** (US-headquartered, China-manufacturing) and **Sumitomo Electric** (Japan) are the principal non-EU competitors in Ge and GaAs substrates, both structurally more exposed to (AXT) or structurally protected within (Sumitomo, as a Japan-based producer under Japan's own critical-minerals diversification policy) the China raw-material relationship described in §3.3.

### 4.3 Gallium Arsenide (LEC, VGF) and Gallium Phosphide

- **Freiberger Compound Materials GmbH** (Freiberg, Saxony, Germany) is the pre-eminent European GaAs substrate producer, growing semi-insulating (SI) and semiconducting (SC) GaAs by both **LEC** (the traditional route for SI GaAs used in RF/microwave ICs) and **VGF/VB** (increasingly preferred for lower dislocation density, larger diameter — up to 150mm — and better compositional uniformity, particularly for optoelectronic and high-power laser diode substrates). Freiberger is jointly owned by Sumitomo Electric and Siltronic-adjacent German industrial interests, giving it a direct institutional link into both the Japanese and German/EU semiconductor policy ecosystems, and situates it squarely within "Silicon Saxony," one of the clusters that could plausibly seek "Semiconductor Regions of Excellence" status under Chips Act 2.0.
- Freiberger's feedstock (high-purity Ga metal, As) exposure is the clearest direct link in the entire EU compound-semiconductor industry between CRMA gallium provisions and an actual melt-growth production line.
- **AXT** and **Sumitomo Electric** remain the principal global competitors as noted; **Vital Materials** and other Chinese GaAs producers are increasingly significant at the low/mid end.

### 4.4 Indium Phosphide (LEC, VGF)

- InP substrate production in Europe is comparatively thin. **Wafer Technology Ltd** (Milton Keynes/Swanage lineage, UK — now part of the **IQE plc** group) has historically been a European (post-Brexit: UK, so a "third country" relative to the EU regulatory perimeter, but deeply integrated into EU supply chains) producer of InP, GaAs, GaSb, and InSb substrates by VGF and LEC.
- **IQE plc** (Cardiff, Wales) itself is principally an epitaxial-wafer (epiwafer) house rather than a bulk-crystal grower, but its ownership of Wafer Technology gives it upstream bulk-substrate capability — relevant because IQE is a frequently cited example in UK/EU compound-semiconductor cluster policy (the "CS Connected" cluster in South Wales) of vertical integration from boule to epiwafer.
- Continental European InP capacity is limited; much EU demand for InP substrates (telecom lasers, photodetectors, space solar cells) is met by Japanese (Sumitomo Electric) and US (currently reduced — historically AXT-adjacent and IntelliEPI-adjacent) suppliers, making InP arguably the material with the **largest strategic gap** relative to the indium-omission from CRMA's SRM list noted in §3.5.

### 4.5 Antimonide and other narrow-gap III-V/IV-VI materials (GaSb, InSb, InAs)

- These are lower-volume, higher-value-per-wafer materials serving infrared detector, thermophotovoltaic, and quantum/spintronic research markets. **Wafer Technology Ltd** (UK) is again a relevant Bridgman/VGF-route producer of GaSb and InSb. **IQE** and specialty players in Germany (e.g., **Vitesco/former Vishay Semiconductor** infrared businesses) and France (**III-V Lab**, a Nokia Bell Labs/CEA/Thales joint venture focused on III-V epitaxy and devices rather than bulk growth per se) round out a thin but technically sophisticated EU/UK ecosystem.
- Because antimony (Sb) is CRMA-critical (though not strategic) and gallium is both critical and strategic, GaSb sits at an interesting policy intersection — but in practice the wafer volumes are so small that neither Act's benchmarks are likely to be materially driven by antimonide-crystal demand.

### 4.6 CdTe and CdZnTe (Bridgman, VGF, and Travelling Heater Method variants)

- **Coherent Corp.** (formerly II-VI Incorporated; US-headquartered but with significant European manufacturing footprint, including in Germany via former former II-VI/Optotec and Saxony-based sites) is the dominant global producer of CdZnTe (CZT) for gamma/X-ray radiation detectors (nuclear security, medical imaging) and of CdTe substrates for HgCdTe (MCT) infrared detector epitaxy, grown principally by **high-pressure Bridgman** and **THM (travelling heater method)** variants.
- **Kromek plc** (Sedgefield, UK) grows CZT by a modified Bridgman process for radiation-detection applications — a UK (third-country) example of a small, technically important CZT crystal grower.
- Pure-play **CdTe thin-film photovoltaic** (First Solar and similar) is a *device* technology using vapour-deposited (not melt-grown) CdTe and is therefore outside this report's scope, but it is a major consumer of the same upstream tellurium pool and therefore a relevant demand-side competitor for tellurium feedstock that CZT/CdTe crystal growers must consider — reinforcing the significance of tellurium's absence from the CRMA's critical/strategic lists (§3.5).

### 4.7 Summary table: material, growth technique, and principal EU/UK producers

| Material | Principal melt-growth technique(s) | Key EU/UK producer(s) | CRMA feedstock status |
|---|---|---|---|
| Si | CZ, Float Zone | Siltronic, (Wacker — polysilicon) | Silicon metal: Strategic (feedstock only) |
| Ge | CZ | Umicore (refining + substrates) | Germanium: Critical + Strategic |
| GaAs | LEC, VGF/VB | Freiberger Compound Materials | Gallium: Critical + Strategic; Arsenic: Critical |
| GaP | LEC, VGF | Freiberger (limited), niche Asian/US suppliers dominant | Gallium: Critical + Strategic |
| InP | LEC, VGF | Wafer Technology/IQE (UK) | Indium: not listed; Phosphorus: Critical |
| InAs | Bridgman/VGF | Wafer Technology (UK), niche | Indium: not listed; Arsenic: Critical |
| GaSb | Bridgman/VGF | Wafer Technology (UK) | Gallium: Critical + Strategic; Antimony: Critical |
| InSb | Bridgman/VGF/Czochralski variants | Wafer Technology (UK) | Indium: not listed; Antimony: Critical |
| CdTe | Bridgman, THM | Coherent Corp. (EU sites), Kromek (UK, CZT focus) | Tellurium: not listed |
| CdZnTe (CZT) | High-pressure Bridgman, THM | Coherent Corp., Kromek | Tellurium: not listed; Zinc: not listed |

---

## 5. Synthesis: Where the Policy Framework Helps, and Where the Gaps Are

### 5.1 Points of genuine alignment

1. **Feedstock security for GaAs is the single clearest win.** Freiberger's LEC/VGF GaAs production is directly downstream of gallium and (to a lesser policy-visible extent) arsenic supply, and gallium is both Critical and Strategic under CRMA, with active Strategic Projects (via Umicore, in Belgium, for germanium; gallium-specific EU primary-production restart efforts such as Ingal Stade). The Commission's own projected trajectory (71%→17% gallium import dependency by 2030) — if realised — would materially de-risk Freiberger's (and any future EU GaAs entrant's) feedstock position.
2. **Chips Act 2.0's explicit "materials to advanced packaging" value-chain language** is a meaningful widening of the FOAK/Strategic Project concept that, unlike the 2023 Act's fab-centric drafting, at least textually contemplates a crystal-growth or wafering facility qualifying for streamlined permitting and state-aid clearance — something no compound-semiconductor substrate maker could confidently claim under the original Act.
3. **The 12-month permitting target and Regions of Excellence label**, while generic, directly address one of the genuine operational pain points reported by European specialty-materials manufacturers: multi-year permitting timelines for furnace/growth-facility expansions (particularly relevant given the hazardous-materials handling — arsine/phosphine synthesis routes, cadmium and tellurium handling — inherent to compound-semiconductor crystal growth, which routes such facilities through more demanding environmental and worker-safety permitting than a typical Si CMOS fab).

### 5.2 Structural gaps specific to this industry

1. **No indium or tellurium coverage.** This is the most consequential gap for InP, InAs, InSb, CdTe, and CdZnTe producers. Given indium's supply concentration (predominantly a zinc-refining byproduct, with China, South Korea, and a small number of other producers dominating) and tellurium's extreme scarcity (a copper-refining byproduct with some of the most concentrated production of any element used in electronics), the absence of CRMA-level attention leaves the InP and CdTe/CZT segments of the melt-growth industry without the streamlined-permitting, financing, and stockpiling tools that GaAs and Ge producers can in principle access.
2. **CRMA Strategic Projects skew toward battery/magnet/PGM materials, not semiconductor-purity refining.** Of the 47 (later ~60) designated Strategic Projects, only two (GePETO, ReGAIN — both Umicore, both germanium) are unambiguously relevant to compound-semiconductor feedstock; gallium-specific EU processing capacity is comparatively underrepresented in the formal Strategic Project list relative to its dual (Critical+Strategic) designation, suggesting the *application pipeline* (which the Commission draws from) has not yet produced sufficient bankable gallium-refining projects — an opportunity for EU-based crystal growers or specialty-metals refiners to originate new Strategic Project applications in future designation rounds (the Commission has signalled further calls).
3. **Chips Act 2.0 remains, as of mid-2026, an unadopted proposal.** Its permitting acceleration, Regions of Excellence label, and materials-inclusive FOAK/Strategic Project language are subject to the ordinary legislative procedure and could be narrowed, delayed, or reweighted toward AI/logic priorities during Parliament and Council negotiation — a live legislative-risk factor for any compound-semiconductor producer planning capital investment on the assumption that current draft provisions will survive intact.
4. **Volume mismatch with the Act's political centre of gravity.** Both Chips Act 2.0 and CADA are substantively organised around AI-accelerator and data-centre demand (leading-edge logic, HBM memory, advanced packaging for AI chips). Compound-semiconductor substrates for RF/microwave, photonics, infrared detection, and space applications are comparatively low-volume, high-margin, defence/space-adjacent markets that do not map cleanly onto the "Demand Accelerators" and "Grand Challenges" framing, which is explicitly tied to AI Gigafactories and cloud infrastructure. Compound-semiconductor producers may need to engage proactively (via SEMI Europe, national trade associations, or direct Commission consultation) to ensure sector-specific provisions are not crowded out during co-decision negotiations.
5. **Purity-grade specificity is entirely absent from CRMA benchmarks.** The Act's 2030 targets are volumetric (tonnes of gallium, tonnes of germanium) with no distinction between LME-tradable commercial-grade metal and the 6N–7N (99.9999–99.99999%) purity required for LEC/VGF single-crystal growth. A Strategic Project that satisfies the CRMA's processing benchmark by producing commercial-grade gallium ingots does nothing to secure the ultra-high-purity feedstock pipeline Freiberger or any EU GaAs grower actually requires; purification to semiconductor grade is a separate, capital-intensive step not explicitly incentivised by the Regulation's text.

### 5.3 Practical recommendations for industry participants

For companies in this space — whether established European players (Freiberger, Umicore, Coherent's EU operations, Wafer Technology/IQE, Kromek, Siltronic) or prospective entrants — the policy landscape suggests:

- **Engage early in Chips Act 2.0 trilogue negotiations** (Parliament/Council co-decision) to ensure the "materials to advanced packaging" FOAK/Strategic Project language is preserved and, ideally, sharpened with explicit reference to compound-semiconductor substrate manufacturing as a qualifying activity category, not merely a theoretically-includable one.
- **Originate CRMA Strategic Project applications for high-purity gallium and (where applicable) indium/tellurium refining**, given the Commission's stated intent to issue further designation calls; the current under-representation of semiconductor-grade Ga/Ge projects relative to battery-material projects appears to reflect an application-pipeline gap rather than a policy exclusion.
- **Advocate through SEMI Europe and national industry bodies** for indium and tellurium to be considered in the next scheduled CRMA critical/strategic list review, given their direct relevance to InP-photonics/RF and CdTe/CZT radiation-detection and infrared-imaging value chains — both of which have clear EU strategic/defence relevance (space-qualified InP photonics, CZT for nuclear-security radiation detection) that aligns with the CRMA's stated defence/aerospace strategic criteria.
- **Monitor the China export-control trajectory** (gallium/germanium licensing, the December 2024 US-targeted ban, and any extension to EU-targeted measures) as the primary near-term operational risk, independent of how quickly EU legislative instruments mature; the SEMI Europe assessment that "no acute short-term disruption" existed as of 2024 should not be read as a durable medium-term assurance, particularly for germanium given the observed Belgium trade-diversion pattern that indicates the EU is itself already a transhipment/refining node in the current China-constrained system.

---

## 6. Key References

**Legislation and Official EU Sources**
- Regulation (EU) 2023/1781 of the European Parliament and of the Council of 13 September 2023 establishing a framework of measures for strengthening Europe's semiconductor ecosystem (European Chips Act), *Official Journal of the European Union*.
- Regulation (EU) 2024/1252 of the European Parliament and of the Council of 11 April 2024 establishing a framework for ensuring a secure and sustainable supply of critical raw materials (Critical Raw Materials Act), *Official Journal of the European Union*.
- European Commission, *Proposal for the Chips Act 2.0* (including Annexes and three-part Impact Assessment), adopted 3 June 2026. Digital Strategy portal: https://digital-strategy.ec.europa.eu/en/library/proposal-chips-act-20
- European Commission, *Chips Act 2.0* policy page: https://digital-strategy.ec.europa.eu/en/policies/chips-act-2
- European Commission, *European Chips Act* policy page: https://digital-strategy.ec.europa.eu/en/policies/european-chips-act
- European Commission, *Communication on European Tech Sovereignty*, 3 June 2026.
- Council of the European Union, *Critical Raw Materials Act* infographic and Strategic Projects overview: https://www.consilium.europa.eu/en/infographics/critical-raw-materials/
- European Commission, *Study on the Critical Raw Materials for the EU 2023* (Annex on criticality assessment methodology and material-by-material data).
- International Energy Agency, *Strategic Projects of the CRMA*: https://www.iea.org/policies/26758-strategic-projects-of-the-crma

**Industry Association and Legal Analysis**
- SEMI Europe, *Comments on the Export Controls on Gallium and Germanium*, submitted to relevant authorities, 2024.
- Aeneas, "Chips Act 2.0: EU Proposes New Measures to Strengthen Semiconductor Competitiveness and Resilience," June 2026: https://aeneas-office.org/2026/06/03/european-commission-unveils-proposed-chips-act-2-0/
- White & Case LLP, "Strategic Projects for the EU: list of 47 Strategic Projects announced," April 2025.
- Jones Day, "The EU Critical Raw Materials Act and Its Impact on the Mining Sector: Strategic Opportunities for Industry Stakeholders," May 2026.
- EIT RawMaterials, "The Strategic Projects backed by EIT RawMaterials."

**China Export Controls and Market Impact**
- Stimson Center, "China's Germanium and Gallium Export Restrictions: Consequences for the United States," 2026.
- ORF America, "China's Critical Mineral Export Controls: Background & Chokepoints," May 2025.
- U.S. International Trade Commission, "Germanium and Gallium: U.S. Trade and Chinese Export Controls," Executive Briefing.
- 3D InCites (IFTLE), "China Restricts Exports of Gallium and Germanium," October 2023.
- Yole Group, "China's Export Restrictions on Ga and Ge Shake Global Semiconductor Industry," 2023.
- CSIS Hidden Reach, "Mineral Monopoly: China's Control over Gallium Is a National Security Threat," July 2023.

**Technical / Industry Background on Melt-Growth Materials and Producers**
- Freiberger Compound Materials GmbH — corporate and technical materials on LEC and VGF GaAs and GaP substrate production.
- IQE plc / Wafer Technology Ltd — corporate materials on InP, GaAs, GaSb, and InSb substrate production by VGF/LEC.
- Coherent Corp. (formerly II-VI Incorporated) — corporate materials on CdTe/CdZnTe Bridgman and THM crystal growth for infrared and radiation-detection applications.
- Kromek plc — corporate materials on modified-Bridgman CZT growth for radiation detection.
- Umicore — corporate materials on germanium refining/recycling (GePETO, ReGAIN projects) and multi-junction solar-cell germanium substrates.

---

*This report reflects publicly available information as of 28 July 2026. The Chips Act 2.0 proposal was, at time of writing, still subject to the EU's ordinary legislative procedure (European Parliament and Council co-decision) and had not entered into force; readers should verify current legislative status before relying on specific provisions described here for investment or compliance decisions.*

---

> [!NOTE]
> 
> Generated by Claude.ai
>
> Model: Sonet 5
>
> Prompt: Prepare an extensive, technically rigorous report on the **European Union Chips Act 2.0** (including the evolution of the original EU Chips Act and any proposed or adopted "Chips Act 2.0" initiatives) and the **Critical Raw Materials Act (CRMA)** from the perspective of the **compound semiconductor bulk crystal growth industry**.
>
> The report should focus on companies producing semiconductor single crystals and wafers using melt-growth technologies, including **Czochralski (CZ)**, **Liquid Encapsulated Czochralski (LEC)**, **Vertical Gradient Freeze (VGF)**, **Bridgman**, and related techniques. Consider materials such as **Si**, **Ge**, **GaAs**, **InP**, **GaP**, **InAs**, **GaSb**, **InSb**, **CdTe**, **CdZnTe**, and other semiconductor crystals grown from the melt.
>
> Structure the report as follows:
>
> 1. **Executive Summary**
>
>    * Main objectives of the EU Chips Act and the Critical Raw Materials Act
>    * Strategic importance for the European semiconductor ecosystem
>    * Expected impact on crystal-growth companies
> 2. **Background**
>
>    * Overview of the European semiconductor supply chain
>    * Role of bulk crystal growth in semiconductor manufacturing
>    * Position of Europe in the global semiconductor materials market
> 3. **EU Chips Act**
>
>    * Legislative objectives
>    * Pillars of the Act
>    * Funding mechanisms
>    * Pilot lines and manufacturing initiatives
>    * Support for research and innovation
>    * Public-private partnerships
>    * State aid provisions
>    * Strategic manufacturing incentives
>    * Effects on substrate and wafer manufacturers
> 4. **EU Chips Act 2.0**
>
>    * Current status (proposed, under discussion, or adopted)
>    * Major differences compared with the original Chips Act
>    * New strategic priorities
>    * Expected funding opportunities
>    * Support for advanced semiconductor materials
>    * Relevance to III–V and II–VI compound semiconductors
> 5. **Critical Raw Materials Act**
>
>    * Objectives and legal framework
>    * Strategic and critical raw materials relevant to semiconductor manufacturing
>    * Supply-chain resilience
>    * Mining, refining, recycling, and stockpiling policies
>    * Permitting and strategic projects
>    * International partnerships
>    * Environmental and sustainability requirements
> 6. **Critical Raw Materials for Bulk Crystal Growth**
>    Analyze the supply chain, availability, and strategic importance of materials including:
>
>    * Gallium
>    * Indium
>    * Germanium
>    * Arsenic
>    * Phosphorus
>    * Antimony
>    * Tellurium
>    * Cadmium
>    * Zinc
>    * Boron
>    * Silicon
>    * Graphite
>    * High-purity quartz
>    * Other materials required for crucibles, encapsulants, dopants, and crystal-growth equipment.
> 7. **Impact on Semiconductor Crystal Growth Companies**
>    Analyze how the legislation affects:
>
>    * Crystal growers
>    * Wafer manufacturers
>    * Epitaxy suppliers
>    * Equipment manufacturers
>    * Chemical suppliers
>    * Research institutes
>    * Universities
>    * Semiconductor start-ups
> 8. **Business Opportunities**
>
>    * New manufacturing investments
>    * Funding programs
>    * Horizon Europe
>    * European Innovation Council
>    * Important Projects of Common European Interest (IPCEI)
>    * European Investment Bank financing
>    * National funding schemes
>    * Infrastructure development
> 9. **Case Study: Establishing a Compound Semiconductor Crystal Growth Company in Poland**
>    Evaluate how the EU Chips Act and the CRMA would influence a new company producing bulk III–V semiconductor crystals (e.g., InP, GaAs, GaP, InAs, GaSb) in Poland. Discuss:
>
>    * Potential funding opportunities
>    * Strategic advantages
>    * Regulatory obligations
>    * Supply-chain risks
>    * Access to European customers
>    * Collaboration opportunities with European research organizations
>    * Long-term competitiveness
> 10. **Comparison with Other Regions**
>     Compare the European framework with:
>
>     * U.S. CHIPS and Science Act
>     * China's semiconductor industrial policies
>     * Japan's semiconductor strategy
>     * South Korea's semiconductor initiatives
> 11. **Strategic Assessment**
>
>     * Opportunities
>     * Risks
>     * Weaknesses
>     * Long-term outlook
>     * Recommendations for investors
>     * Recommendations for crystal-growth companies
>     * Recommendations for policymakers
> 12. **References**
>
>     * Include 30–50 authoritative references.
>     * Prioritize official European Commission documents, regulations, communications, impact assessments, policy papers, reports, industry analyses, and peer-reviewed literature.
>     * Clearly distinguish legally binding regulations from policy proposals and consultation documents.
>
> **Requirements**
>
> * Write in a formal technical style.
> * Use Markdown.
> * Include tables summarizing legislation, funding instruments, critical raw materials, strategic projects, and business impacts.
> * Explain how the legislation affects each stage of the semiconductor value chain, from raw material extraction through refining, crystal growth, wafer fabrication, device manufacturing, and recycling.
> * Clearly identify which provisions are already in force and which remain proposed or under discussion.
> * Highlight implications specifically for the **bulk crystal growth industry**, with particular emphasis on **III–V compound semiconductors** and **high-purity semiconductor materials**.
