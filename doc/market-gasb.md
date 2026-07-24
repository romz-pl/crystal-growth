# The Global Commercial Gallium Antimonide (GaSb) Single-Crystal Market

*A value-chain, technology, and market-structure overview — July 2026*

---

## 1. Executive Summary

Gallium antimonide (GaSb) is a narrow-bandgap (0.72–0.78 eV at 300 K), III‑V compound semiconductor grown almost exclusively as bulk single crystal by Czochralski-family methods and sold as polished wafers/substrates to epitaxy houses and device makers. Unlike GaAs or InP, GaSb is **not a high-volume commodity semiconductor**: it is a low-volume, high-value specialty substrate whose principal role is as a lattice-matched growth platform for the "6.1 Å material family" (InAs/GaSb/AlSb) used in mid-wave and long-wave infrared (MWIR/LWIR) detectors, interband cascade lasers (ICLs), and thermophotovoltaic (TPV) cells. The supply base is small — a handful of specialized crystal growers worldwide, most of them also antimonide (InSb) producers — and downstream demand is concentrated in defense/aerospace infrared imaging, gas-sensing lasers, and niche photovoltaics.

Two structural facts dominate the market picture in 2026:

1. **Extreme fragmentation of public market data.** Third-party "market research" reports on GaSb carry wildly inconsistent sizing — figures in circulation range from roughly **US$150 million** to (implausibly) **tens of billions of dollars**<cite index="12-1,18-1,14-1">with one source valuing the market at USD 150 million in 2025 growing to USD 500 million by 2034, another giving the same USD 150 million 2025 figure but a USD 300 million 2034 endpoint, and a third claiming a 2023 value of roughly USD 33 billion rising to USD 139 billion by 2032</cite>. The three-orders-of-magnitude spread indicates these are template-generated syndicated reports rather than rigorously sourced analyses (the largest figure is almost certainly a mislabeled/templated GaAs or generic "wafer" number). Treat all specific dollar figures in this space with caution — see §7.
2. **Feedstock geopolitics now sits upstream of the substrate market.** GaSb consumes elemental gallium and antimony, both subject to Chinese export controls since 2023–2024, which affects cost and availability for non-Chinese crystal growers even though China is not itself a leading GaSb *crystal* supplier.

---

## 2. Material Properties and Why They Matter Commercially

| Property | Value | Commercial relevance |
|---|---|---|
| Crystal structure | Zinc blende | Compatible with standard III-V epitaxy tooling |
| Bandgap (300 K) | ~0.72–0.78 eV | Direct gap in the near/mid-IR — enables IR photonics |
| Lattice constant | ~6.096 Å | Anchors the "6.1 Å family" (GaSb/InAs/AlSb) — near-lattice-matched to InAs and AlSb, enabling low-defect heterostructure growth |
| Typical EPD (etch pit density) | <1,000 cm⁻² (LEC, commercial grade) | Determines usability for high-performance detector/laser epitaxy |
| Standard wafer sizes | 1", 2", 3", 4" (up to 6"+ at select suppliers) | 2" remains the workhorse size; larger diameters are a stated but slow-moving trend |

<cite index="1-1">The 2-inch substrate size has traditionally been the most widely used, as it provides a balance between cost-effectiveness and device performance, though demand for 3-inch and 4-inch diameters is increasing as manufacturers seek improved production efficiency and economies of scale</cite>, and <cite index="1-1">larger substrates offer advantages including more devices per wafer, reduced per-device manufacturing costs, and improved material quality and uniformity</cite>. In practice, GaSb has not followed GaAs/Si toward large-diameter (150 mm+) commodity scaling — device volumes are too low to justify the capital investment, and 2–4 inch remains standard even for advanced defense programs.

---

## 3. Value Chain

The GaSb value chain has four broadly distinct stages, typically performed by the same vertically integrated supplier:

```
Raw materials (6N-7N Ga, Sb)
        │
Polycrystalline synthesis (Ga + Sb → poly-GaSb charge)
        │
Bulk single-crystal growth (LEC / VGF / VBG / Cz-variant)
        │
Ingot processing: grinding, orientation (X-ray), wire-sawing into slices
        │
Wafer finishing: lapping, etching, polishing (SSP/DSP), epi-ready surface prep
        │
   ┌────┴─────┐
Substrate    Epiwafer (MBE/MOCVD overgrowth of
sale to      device layers, sold to detector/laser
epi houses   fabs or used in-house)
```

### 3.1 Crystal growth technologies

- **Liquid Encapsulated Czochralski (LEC)** — the dominant commercial method. <cite index="8-1">GaSb crystal is a compound formed by 6N pure Ga and Sb element and is grown by Liquid Encapsulated Czochralski method with EPD < 1000 cm⁻³, giving high uniformity of electrical parameters and low defect density suitable for MBE or MOCVD epitaxial growth</cite>. Boron oxide encapsulation suppresses antimony volatilization during pulling.
- **Vertical Gradient Freeze (VGF) / Vertical Bridgman (VBG/VB)** — offered by some suppliers as an alternative growth route, generally associated with lower dislocation density than LEC but historically less mature for GaSb than for GaAs. <cite index="41-1">Growth methods offered by suppliers include LEC, VGF and VBG</cite>.
- **Modified/standard Czochralski (Cz, Mo-Cz)** — used particularly for Te-doped n-type material for thermophotovoltaic and detector applications.

A recurring technical challenge specific to GaSb (relative to GaAs) is antimony's volatility and melt convection behavior in the growth furnace: <cite index="8-1">the space in the single crystal furnace is relatively open, heat convection is relatively complicated, and the defects of gallium antimonide are greatly affected by the drawing process, with the Sb element in polycrystalline material more volatile than in GaAs</cite>. This is a key reason GaSb boules remain smaller in diameter and lower in throughput than GaAs boules, keeping unit costs high.

### 3.2 Doping and wafer grades
Commercial GaSb is offered n-type (Te-doped), p-type (Zn-doped), and semi-insulating/undoped, with orientations of (100) and (111)A/B, off-cut variants for epitaxy, and both "epi-ready" (polished, MBE/MOCVD-qualified) and mechanical/research grades.

---

## 4. Market Structure

The market is a **specialty, low-volume, high-mix substrate business**, structurally closer to InSb, InAs, or GaN-substrate markets than to mainstream GaAs or InP. Characteristics:

- <cite index="1-1">The market is characterized by the presence of a limited number of specialized manufacturers</cite> rather than the dozens of vendors seen in mainstream compound-semiconductor substrates.
- Vertical integration is the norm: the same organization typically handles synthesis, crystal growth, and wafer finishing, often alongside sibling antimonide products (InSb) sharing furnace and finishing infrastructure.
- End demand is disproportionately weighted toward **defense, aerospace, and government-funded R&D** rather than high-volume consumer electronics, which limits scale economics compared with GaAs (driven by smartphone RF) or SiC/GaN power electronics (driven by EVs).
- Many "suppliers" visible online are **resellers/distributors** of wafers sourced from a smaller set of actual crystal growers, adding to the appearance of a crowded market without reflecting real production capacity.

---

## 5. Major Manufacturers and Suppliers

### 5.1 Primary crystal growers (own boule-growth capability)

| Company | HQ / Facilities | Notes |
|---|---|---|
| **IQE plc / Galaxy Compound Semiconductors, Inc.** | Spokane, WA, USA (Galaxy) + UK (Wafer Technology) | <cite index="5-1">Galaxy, a member of the IQE plc Group, specializes in manufacturing Indium Antimonide (InSb) and Gallium Antimonide (GaSb) single crystal substrates and is described as the world's leading supplier of GaSb and InSb materials, growing antimonide crystals by the Czochralski boule pulling method under ISO 9001:2008 certified processes</cite>. <cite index="6-1">IQE's broader substrate business manufactures substrates in both the UK and USA from fully vertically integrated operations spanning polycrystal synthesis, Czochralski bulk crystal growth, ingot grinding, wafer slicing, polishing, laser scribing and in-line metrology, offering 2 to 8-inch substrates across GaAs, InP, GaSb, InSb and InAs platforms</cite>. IQE is broadly considered the Western world's leading integrated GaSb/InSb producer.
| **Wafer Technology Ltd.** (UK, part of IQE) | St Asaph, Wales | Long-established UK antimonide/III-V substrate specialist, now operating under the IQE umbrella alongside Galaxy.
| **Xiamen Powerway Advanced Material Co. (PAM-XIAMEN)** | Xiamen, China | <cite index="8-1">Described as a leading manufacturer of compound semiconductor material in China, offering round, saw-cut, lap and polish GaSb wafers with epi-ready surface quality, grown by LEC</cite>. One of the more prominent Chinese GaSb suppliers with a broad compound-semiconductor product line.
| **China Crystal Technologies Co., Ltd.** | China | Named among the limited set of specialized GaSb manufacturers in market-structure analyses.
| **Western Minmetals (SC) Corporation** | Chengdu, China | <cite index="7-1">A major supplier of FZ/CZ single-crystal silicon and semiconductor compounds including VGF GaAs, InP, GaP, InSb and InAs substrates, headquartered in Chengdu and serving research, microelectronic and optoelectronic customers across the EU, North America, Japan and South Korea since 1997</cite>; also lists GaSb wafers/substrates.
| **AXT, Inc.** | Fremont, CA, USA (crystal growth largely in China) | Listed among key players in several GaSb market-structure summaries; AXT's core strength is GaAs/InP/Ge, with antimonide materials a smaller adjacent line.

### 5.2 Downstream fabricators, distributors, and specialty finishers
A larger tier of companies sells GaSb wafers (often as one line among many III-V/II-VI substrates), typically finishing or reselling boules from the primary growers above:

- **American Elements** — <cite index="2-1">manufactures high purity single crystal GaSb wafers for optoelectronics applications, with standard diameters from 25.4 mm (1 inch) to 300 mm (11.8 inches), in various thicknesses and orientations, polished or unpolished, with dopants available</cite>.
- **Azelis** — <cite index="3-1">specializes in manufacturing high-purity and ultra-high-purity substrates, supplying GaSb single-crystal wafers and polycrystalline GaSb for optoelectronic devices such as lasers, LEDs, and photoreceivers</cite>.
- **Stanford Advanced Materials (SAM)** — <cite index="4-1">provides single crystal GaSb wafer to the electronic and optoelectronic industry in diameters up to 4 inches, grown by LEC with EPD < 1000 cm⁻³, epi-ready for MBE/MOCVD, targeted at 2–4 µm band optical devices, microwave devices, and laminated solar cells</cite>.
- **OST Photonics** — <cite index="41-1">offers 2" and 3" GaSb wafers grown by LEC, VGF, and VBG, in undoped, N-type (Te) and P-type (Zn) variants</cite>.
- **UniversityWafer, Inc.** — small-quantity/R&D wafer distributor, including specialty bonded and gold-metallized GaSb wafer products.
- Other regional distributors/finishers: Bayville Chemical Supply, Bonda Technology, ALB Materials, SabiNano, Advanced Engineering Materials, FUNCMATER, and various China-based trading houses.

### 5.3 A note on GaAs producers (Freiberger, others) and GaSb
Major GaAs/InP houses such as **Freiberger Compound Materials** (Germany) are sometimes listed alongside GaSb in generic "antimonide/III-V" market reports, but Freiberger's public technology portfolio centers on GaAs, InP, and GaN via LEC/VGF; it is **not** established in public sources as a commercial GaSb boule grower. This illustrates a broader data-quality issue in this space: many market reports list large III-V players as "GaSb market participants" based on adjacent product lines rather than confirmed GaSb production.

---

## 6. Production Capacity

There is **no reliable, independently audited public figure** for global GaSb single-crystal production capacity (in kg/year or wafer-starts/year). This reflects the market's structure:

- Volumes are small enough that few of the primary growers publicly disclose capacity, and none of the market-research vendors surveyed cite verifiable production-volume data (only revenue estimates of questionable provenance — see §7).
- Boule diameters remain modest (2–4 inch dominant), and demand is largely pull-based from defense/aerospace programs and specialty photonics OEMs rather than driven by high-volume consumer roadmaps, so there is little commercial incentive for growers to publish capacity figures competitors could act on.
- The clearest qualitative signal is that **IQE/Galaxy Compound Semiconductors positions itself as the world's leading GaSb (and InSb) supplier**, implying it holds the largest share of Western capacity, with Chinese suppliers (Xiamen Powerway, Western Minmetals, and others) forming a parallel domestic-Chinese and export-oriented supply base.

---

## 7. Pricing

Public, verifiable list pricing for GaSb wafers is scarce; most vendors quote on request ("contact for quotation") rather than publishing price lists, consistent with a low-volume, spec-driven specialty market. What can be established:

- Wafers are sold across a matrix of **diameter (1"–4", occasionally larger), doping type/level, orientation, and surface finish (as-cut / SSP / DSP / epi-ready)**, each combination priced differently.
- As a specialty III-V substrate (versus commodity Si), GaSb wafers command a significant premium per unit area over silicon and are generally priced above standard GaAs wafers of comparable size, reflecting lower production volumes, higher raw-material cost (antimony), and more difficult crystal growth.
- Antimony feedstock cost is a direct and currently volatile input: <cite index="43-1">from August 2024 to December 2024, antimony shipments from China to the United States dropped 97% while prices rose approximately 200%</cite> — a shock that flows directly into non-Chinese GaSb producers' raw-material costs (see §8.3).

Given the absence of credible public pricing data, this report does not provide per-wafer price figures; buyers should treat any specific price quoted in third-party market reports as unverified.

---

## 8. Applications and Demand Drivers

### 8.1 Infrared photodetectors (largest strategic application)
GaSb is the historical native substrate for **InAs/GaSb type-II superlattice (T2SL)** detectors, a leading alternative to HgCdTe (MCT) for MWIR/LWIR focal plane arrays:

- <cite index="35-1">The nearly lattice-matched semiconductors InAs, GaSb, and AlSb are referred to as the "6.1 Å material system," and InAs/GaSb superlattices are typically grown on GaSb substrates, with InSb-like interfaces often used to provide strain relief</cite>.
- A recurring theme in the literature is that **substrate supply limitations have historically constrained the T2SL detector industry**: <cite index="35-1">GaSb substrates commercially available at the time often suffered from high defect density, poor surface morphology, limited size, and high cost, which led some groups to evaluate GaAs substrates — better in quality and available in larger commercial sizes — for superlattice detector growth instead</cite>, and <cite index="30-1">researchers have specifically developed InAs/GaSb type-II superlattice infrared photodetectors grown on GaAs substrates with a graded metamorphic buffer as a workaround for these substrate constraints</cite>.
- This dynamic is a defining feature of the current GaSb substrate market: **native GaSb substrates remain the performance benchmark, but GaAs-substrate T2SL is a live, commercially motivated alternative** driven partly by GaSb supply/cost/size constraints — a genuine headwind to GaSb substrate demand growth even as T2SL detector demand itself grows.
- Recent device work continues to use native GaSb substrates for best performance, e.g., <cite index="34-1">high-performance extended shortwave infrared T2SL detectors based on InAs/GaSb/AlSb grown directly on GaSb substrate</cite>.

### 8.2 Mid-infrared lasers
- **Interband cascade lasers (ICLs)** are built from GaSb-based heterostructures: <cite index="55-1">ICLs produce coherent radiation over a large part of the mid-infrared spectrum and are fabricated from epitaxially grown semiconductor heterostructures composed of layers of InAs, GaSb, AlSb, and related alloys</cite>. <cite index="61-1">ICLs use optical transitions between an electron state in the conduction band and a hole state in the valence band in a cascade of Sb-based type-II quantum-well structures, with interband-cascade technology considered ideal for high-performance lasing across the entire 3–6 µm range due to relatively wavelength-independent threshold powers, combining high performance with low power consumption</cite>. Commercial ICL suppliers include nanoplus (Germany), Thorlabs (US), and Alpes Lasers (Switzerland) — all downstream consumers of GaSb substrates/epiwafers for gas sensing, environmental monitoring, and industrial process control.
- **Type-I GaInAsSb/AlGaAsSb quantum-well diode lasers** on GaSb substrates address the shorter mid-IR band (up to ~3.7 µm) for applications like hydrocarbon gas sensing.

### 8.3 Thermophotovoltaics (TPV)
Low-bandgap GaSb cells are used to convert infrared radiation (e.g., from radioisotope or combustion heat sources) directly to electricity — a niche but strategically important application in space power and industrial waste-heat recovery, and <cite index="8-1">GaAs/GaSb laminated solar cells have demonstrated conversion efficiencies exceeding 30%</cite>.

### 8.4 Other applications
- Hall-effect and magnetoresistive sensors (leveraging GaSb's high carrier mobility).
- Microwave/high-frequency devices — GaSb's carrier mobility characteristics give it a role as a substrate/epitaxial platform in specialty RF work, though this is a minor share relative to GaAs/GaN.
- Substrates for epitaxial buffer layers enabling other antimonide-based devices (AlSb, InGaSb, GaAlAsSb systems).

---

## 9. Market Trends

### 9.1 Substrate-size evolution is slow and application-led
<cite index="1-1">While 2-inch has traditionally dominated for cost/performance balance, demand for 3-inch and 4-inch diameters is gradually increasing as manufacturers pursue production efficiency and economies of scale in high-volume environments</cite> — but "high volume" in GaSb terms is still modest compared with mainstream III-Vs; large-diameter scaling is constrained by both technical difficulty (Sb volatility, melt convection) and limited economic pull.

### 9.2 Defense and government-funded infrared programs are the primary demand engine
Growth narratives across the market-report literature consistently point to defense/aerospace infrared sensing (missile warning, thermal imaging, surveillance) and government R&D funding — rather than consumer electronics — as the structural demand driver, distinguishing GaSb from GaAs (where 5G/RF and consumer devices dominate) or SiC/GaN (where EV/power electronics dominate).

### 9.3 Competition from alternative substrates and material systems
- **GaAs-substrate T2SL** (metamorphic buffer approach) directly substitutes for GaSb substrates in some detector programs, motivated by GaSb's historical size/defect/cost limitations (§8.1) — a genuine long-term substitution risk for the GaSb substrate market even as the T2SL detector *device* market grows.
- **HgCdTe (MCT)** remains the incumbent, highest-performance IR detector material in many programs; T2SL/GaSb is generally positioned as a RoHS-compliant, more manufacturable alternative rather than a wholesale replacement.

### 9.4 Critical-minerals geopolitics is now a first-order risk factor
GaSb's two constituent elements are both on recent Chinese export-control lists, creating supply-chain and cost exposure for non-Chinese crystal growers that did not exist a few years ago:

- <cite index="43-1">In July 2023, China announced export restrictions on certain gallium and germanium products citing national security concerns, and prices for gallium and germanium surged, with gallium prices increasing by nearly 20% in the United States and Europe</cite>.
- <cite index="43-1">In August 2024, China announced restrictions on antimony; from August to December 2024, antimony shipments from China to the United States dropped 97% while prices rose 200%, and in December 2024 China banned exports of gallium, germanium, and antimony to the United States entirely, with the restrictions also covering the technology to process and refine these materials</cite>.
- <cite index="52-1">China is the largest producer of antimony, accounting for roughly 48% of the metal's globally mined output</cite>, and <cite index="48-1">the United States has no domestic antimony production and severely limited stockpiles</cite> — a direct structural vulnerability for any US-based GaSb crystal grower sourcing antimony feedstock.
- These controls have been partially and provisionally eased: <cite index="47-1">on November 7, 2025, China's Ministry of Commerce announced it would suspend implementation of several of its October 2025 export-control measures (and related prior measures) until November 10, 2026, pending further bilateral negotiation, meaning restrictions on gallium, germanium, antimony and superhard materials dual-use items were not, for the time being, being implemented against the United States</cite>. The situation remains fluid and should be checked for updates.
- Net effect for the GaSb substrate market: **feedstock cost volatility and supply-security concerns are pushing Western governments and primes to fund domestic/allied gallium and antimony supply chains**, indirectly supporting continued investment in Western GaSb crystal-growth capability (e.g., IQE/Galaxy in the US) as a strategic, not just commercial, priority.

### 9.5 Market-data quality is poor across the syndicated research industry
As flagged in §1 and §7, publicly available "market size" figures for GaSb from commercial market-research vendors disagree by orders of magnitude and show signs of templated, low-rigor production (identical company lists reused across unrelated material reports, inconsistent CAGR/base-year math). This is a structural feature of niche compound-semiconductor markets, which receive far less rigorous, primary-data-driven coverage than mainstream semiconductor segments. Analysts and buyers should treat any single-sourced GaSb market-size claim as indicative at best and seek corroboration from technical/trade literature, company disclosures, or direct supplier RFQs rather than syndicated market reports.

---

## 10. Key References

1. DataHorizzon Research — *Gallium Antimonide Single Crystal Substrate Market Size, Growth & Analysis Report, 2033* — https://datahorizzonresearch.com/gallium-antimonide-single-crystal-substrate-market-34364
2. American Elements — *Gallium Antimonide Wafer* — https://www.americanelements.com/gallium-antimonide-wafer-12064-03-8
3. Azelis — *Gallium Antimonide* — https://www.azelis.com/en/markets/electronics/products/high-purity-substrates/gallium-antimonide
4. Stanford Advanced Materials — *Gallium Antimony Wafer (GaSb) Supplier* — https://www.samaterials.com/gallium/2268-gallium-antimony-wafer.html
5. Galaxy Compound Semiconductors, Inc. (IQE plc) — company/product pages — https://abachy.com/catalog/materials/wafers-and-substrates/wafers/gasb-gallium-antimonide-wafers/galaxy-compound-semiconductors-inc ; http://www.galaxywafer.com/galaxy/products/gallium-antimonide-gasb/
6. IQE plc / Wafer Technology Ltd — *Gallium Antimonide (GaSb)* — http://www.wafertech.co.uk/products/gallium-antimonide-gasb/
7. Western Minmetals (SC) Corporation — GaSb product listing — https://wmcchemical.en.made-in-china.com/product/zsKEvoucZYWP/China-Gallium-Antimonide-GaSb-Wafer-Substrate-at-Western-Minmetals.html
8. PAM-XIAMEN (Xiamen Powerway Advanced Material) — *LEC Gallium Antimonide (GaSb) Wafer* — https://www.powerwaywafer.com/gasb-gallium-antimonide-wafer.html ; https://www.powerwaywafer.com/compound-semiconductor/gasb-wafer.html
9. Verified Market Research — *GaSb Wafer Market* — https://www.verifiedmarketresearch.com/product/gasb-wafer-market/
10. Verified Market Reports — *Global Gallium Antimonide (GASB) Market* and *Global Gallium Antimonide Wafer Market* — https://www.verifiedmarketreports.com/product/gallium-antimonide-gasb-market/ ; https://www.verifiedmarketreports.com/product/gallium-antimonide-wafer-market/
11. OpenPR / WiseGuy Reports — *Gasb Wafer Market Poised to Grow at 17.34% CAGR by 2032* — https://www.openpr.com/news/3665721/gasb-wafer-market-poised-to-grow-at-17-34-cagr-by-2032
12. ScienceDirect — *High operating temperature InAs/GaSb type-II superlattice detectors on GaAs substrate for the long wavelength infrared* — https://www.sciencedirect.com/science/article/pii/S1350449518305000
13. Chapter 1, *Type-II Superlattice Infrared Detectors* (David Z.-Y. Ting et al.) — https://bdt.semi.ac.cn/download/0.7938302486526054.pdf
14. PMC — *Extended Shortwave Infrared T2SL Detector Based on AlAsSb/GaSb Barrier Optimization* — https://www.ncbi.nlm.nih.gov/pmc/articles/PMC12114116/
15. Wikipedia — *Interband cascade laser* — https://en.wikipedia.org/wiki/Interband_cascade_laser
16. nanoplus — *Interband Cascade Laser (ICL)* — https://nanoplus.com/products/interband-cascade-laser
17. Compound Semiconductor — *Interband cascade lasers target the mid-infrared* — https://compoundsemiconductor.net/article/107445/Interband_cascade_lasers_target_the_mid-infrared/feature
18. Exiger — *China Announces Export Controls on Five Critical Minerals* — https://www.exiger.com/perspectives/critical-minerals-export-controls/
19. CSIS — *China Imposes Its Most Stringent Critical Minerals Export Restrictions Yet Amidst Escalating U.S.-China Tech War* — https://www.csis.org/analysis/china-imposes-its-most-stringent-critical-minerals-export-restrictions-yet-amidst
20. Pillsbury Law — *China Suspends Export Controls on Certain Critical Minerals and Related Items* — https://www.pillsburylaw.com/en/news-and-insights/china-suspends-export-controls-certain-critical-minerals-related-items.html
21. VOA News — *China announces new export controls for critical mineral [antimony]* — https://www.globalsecurity.org/wmd/library/news/china/2024/08/china-240816-voa01.htm
22. The Oregon Group — *China lifts export ban gallium, germanium, antimony* — https://theoregongroup.com/commodities/gallium-germanium/china-lifts-export-ban-gallium-germanium-antimony/

---

## 11. Notes on Methodology and Limitations

- This report synthesizes technical/trade literature, supplier public disclosures, and commercial market-research summaries available as of July 2026.
- **No production-capacity or price figures in this report should be treated as audited data** — none were found from primary, verifiable sources; all are qualitative or explicitly flagged as indicative.
- The GaSb single-crystal market is small enough, and dominated by enough privately held/vertically-integrated players, that authoritative third-party market sizing (of the kind available for GaAs, Si, or SiC) does not currently exist in the public domain. Any analysis requiring precise figures (revenue, tonnage, wafer starts) would require direct primary research — supplier RFQs, trade-data (HS code) analysis for gallium/antimony feedstock flows, and/or paid access to specialist compound-semiconductor industry trackers (e.g., Yole Group, TECHCET) not consulted in this report.

---

> [!NOTE]
> 
> Generated by Claude.ai
>
> Model: Sonet 5
>
> Prompt: Provide a comprehensive and up-to-date overview of the global commercial Gallium antimonide (GaSb) single-crystal market. The report should cover the entire value chain, from crystal growth to finished wafers, and include market structure, major manufacturers, production capacity, technologies, applications, pricing, and market trends. Provide key references. Show the output in Markdown format.
