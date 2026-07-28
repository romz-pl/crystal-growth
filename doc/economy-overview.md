# Feasibility Study & Business Report

## Establishing a Vertically Integrated Compound Semiconductor Manufacturer in Poland
### Bulk III–V Crystal Growth and Wafer Production: InP, GaP, GaSb

**Prepared:** July 2026
**Benchmark companies:** Sumitomo Electric Industries (Japan); Freiberger Compound Materials GmbH (Germany); AXT Inc. (USA); JX Nippon Mining & Metals (Japan)

---

## Executive Summary

This report assesses the feasibility of founding a Polish compound-semiconductor company ("NewCo" or "the Company") to grow bulk III–V single crystals and process them into polished wafers, with an initial product line of **Indium Phosphide (InP)**, **Gallium Phosphide (GaP)**, and **Gallium Antimonide (GaSb)**. The intended positioning is as a European, EU-based, vertically integrated substrate supplier serving photonics, optoelectronics, RF/power electronics, infrared (IR) systems, and research markets — occupying a niche analogous to Freiberger Compound Materials (Freiberg, Germany) but differentiated by product mix (GaSb is not currently a Freiberger product) and by full EU/Poland domicile.

**Headline findings:**

- **Market pull is real but narrow.** The global InP wafer market is estimated in the low-to-mid hundreds of millions of USD (roughly USD 200–220 million in 2025–2026), growing at a low-double-digit CAGR (~11–12%) on the back of 800G/1.6T datacom optics, 5G/6G backhaul, LiDAR, and quantum-photonics demand.The indium phosphide wafer market size is expected to grow from USD 198.17 million in 2025 to USD 221.42 million in 2026 and is forecast to reach USD 385.65 million by 2031 at 11.73% CAGR, driven by hyperscale data-center upgrades to 800G and 1.6T optics, the global rollout of 5G and preparation for 6G backhaul, and expanding quantum-photonics funding, with the market estimated at USD 211.3 million in 2025. GaSb and GaP are materially smaller, more specialized markets (IR optoelectronics/thermophotovoltaics for GaSb; LED and some RF/optoelectronic niches for GaP), each likely in the tens of millions of USD globally.
- **Supply concentration is an opportunity and a risk simultaneously.** Industry concentration is moderate: the top five suppliers — Sumitomo Electric, AXT, Freiberger, JX Nippon Mining and Metals, and Visual Photonics Epitaxy — collectively held around 70% of revenue in 2024. This is a moat for incumbents (crystal-growth know-how, multi-year customer qualification cycles) but also means a well-capitalized, technically credible new EU entrant addresses a genuine "second-source" and "de-risking" demand from Western customers.
- **Policy tailwinds are strong and currently building.** The EU's Critical Raw Materials Act, Chips Act 2.0 proposal (June 2026), and a nine-country "Semiconductor Coalition" that explicitly includes Poland create a funding and political environment more favorable to this venture than at any point in the last decade.Nine EU Member States — Austria, Belgium, Finland, France, Germany, Italy, Poland, Spain and the Netherlands — launched the Semiconductor Coalition, agreeing to reinforce cooperation to strengthen Europe's competitiveness and strategic autonomy in the semiconductor sector by supporting research, expanding production capacity, and fostering a skilled workforce. The Chips Act 2.0 proposal clarifies the scope of first-of-a-kind projects eligible for state aid to include the full value chain from raw materials to advanced packaging and assembly.
- **Feedstock risk is the central strategic vulnerability.** Gallium and indium — the two core Group III elements needed — are subject to Chinese export licensing since 2023–2025, with gallium production roughly 80–98% China-controlled and indium roughly 55–70% China-controlled.China controls the overwhelming majority of primary gallium supply and imposed export controls on gallium in 2023, creating immediate supply disruption for GaN power electronics, GaAs RF chips, and military radar systems. Roughly 70% of refined indium is still produced in China, and the EU's Critical Raw Materials Act and U.S. critical-minerals initiatives both list indium as a strategic material essential to technology and defense. This cuts both ways: it is a genuine cost and availability risk, but it is also the single strongest argument for EU public co-funding of a Polish crystal-growth facility.
- **Capital intensity and gestation period are the primary commercial risks.** Crystal growth (VGF/VB/LEC), wafering, lapping/polishing, and epi-ready surface preparation require multi-million-euro cleanroom and furnace capex per product line, multi-year customer qualification cycles (typically 18–36 months per design-in), and deep metallurgical/crystallographic expertise that does not exist at scale in Poland today and must be substantially imported or built via PhD-level R&D partnerships.
- **Overall verdict:** The venture is **feasible but high-risk and capital-intensive**, best pursued as a **phased, EU-co-funded, single-product-first strategy** (most plausibly GaSb or InP, not all three simultaneously), anchored to a Polish or regional research-institute partnership, with realistic timelines of 4–6 years to first qualified revenue and 8–10 years to potential profitability at meaningful scale.

---

## 1. Introduction and Scope

### 1.1 Purpose
This study evaluates whether it is technically, economically, and strategically sound to establish a Polish compound semiconductor company that:
1. Synthesizes high-purity III–V polycrystalline feedstock (InP, GaP, GaSb);
2. Grows bulk single crystals (boules) via established industrial methods (Vertical Gradient Freeze/Vertical Bridgman — VGF/VB — and/or Liquid Encapsulated Czochralski — LEC);
3. Processes boules into sliced, lapped, polished, and epi-ready wafers;
4. Sells wafers (and potentially epitaxy-ready substrates) to European and global customers in photonics, optoelectronics, RF/microwave, power electronics, IR sensing/thermophotovoltaics, and academic/research markets.

### 1.2 Why This Model (Sumitomo / Freiberger)
Both benchmark companies are **vertically integrated substrate specialists** — they do not fabricate devices; they sell certified, characterized wafers to device makers (fabs, foundries, epi houses, research labs). Freiberger has established a worldwide reputation as a supplier of top-grade GaAs, InP and GaN wafers, using efficient and highly automated production techniques from synthesis and crystal growth through wafer polishing and cleaning. This is a capital-intensive, IP-and-process-know-how-driven business model with long customer relationships, not a commodity manufacturing business — a crucial framing for the financial model in Section 7.

### 1.3 Why Poland
- Existing Polish strengths in adjacent fields: Institute of Electron Technology (ITE), Institute of High Pressure Physics PAS ("Unipress," globally known for GaN/ammonothermal crystal growth), Wrocław and Warsaw technical universities, and a growing cluster of optoelectronics/photonics R&D.
- Political momentum: Poland is a signatory of the EU Semiconductor Coalition and hosts existing semiconductor investment (Intel's Wrocław/Kraków-adjacent assembly and test facility), demonstrating state willingness to co-invest.Intel is investing $4.6 billion in an assembly and test facility in Poland, with the Polish government expected to cover about one-third of this investment.
- Labor cost and STEM talent pool are favorable relative to Western Europe, though specialized crystal-growth expertise must largely be imported or trained from scratch (see Section 4.5).
- Geographic and logistical proximity to German, Dutch, and Nordic photonics/RF customers and to Freiberger itself (potential competitor or, less likely, partner/acquirer).

### 1.4 Limitations of This Study
This is a desk-based feasibility study drawing on public market data, industry literature, and the authors' technical understanding of III–V crystal growth. It does not substitute for: a site-specific engineering feasibility study, a bankable independent market study commissioned from a specialist (Yole, TECHCET, IHS Markit/S&P), or due diligence on specific equipment vendors, feedstock suppliers, and IP freedom-to-operate. These should be commissioned before capital commitment.

---

## 2. Market Analysis

### 2.1 Global Market Sizing by Product

| Material | Primary applications | Approx. global market size (2025–26) | Growth outlook | Key incumbents |
|---|---|---|---|---|
| **InP** | Photonic ICs, DFB/EML lasers, APDs, 800G/1.6T optical transceivers, THz devices, some HBT RF | ~USD 200–220M (2026), growing to ~USD 385–630M by 2031–2035 | High (~11–12% CAGR) | Sumitomo Electric, AXT, Freiberger, JX Nippon, Visual Photonics Epitaxy |
| **GaP** | LEDs (legacy), some visible-wavelength optoelectronics, solar cell substrates, selected RF | Small, mature, largely commoditized; tens of millions USD globally | Low/flat, LED-driven demand mostly migrated to GaN/sapphire | Chinese and Japanese suppliers dominate; limited Western capacity |
| **GaSb** | Mid-/far-infrared LEDs and lasers, thermophotovoltaics (TPV), IR detectors, some high-speed transistors (antimonide-based compound semiconductors, ABCS) | Niche, high-value, likely low tens of millions USD globally | Growing steadily — TPV for waste-heat/energy harvesting and defense IR are emerging growth vectors | Very few dedicated suppliers (e.g., Wafer Technology/IQE, AXT, some Russian/Chinese sources) — arguably the **least contested** of the three |

Sources: Mordor Intelligence and Future Market Insights market reports (InP);the indium phosphide wafer market was valued at USD 211.3 million in 2025, projected to reach USD 627.7 million by 2035 at 11.5% CAGR, while a separate estimate places the 2026 market at USD 221.42 million growing to USD 385.65 million by 2031 at 11.73% CAGR. GaP and GaSb figures are triangulated from adjacent compound-semiconductor market reports and are directionally indicative rather than precise, reflecting thinner public coverage of these smaller markets — an independent commissioned study is recommended before final investment decision.

### 2.2 Demand Drivers
- **Datacom/telecom optics:** Hyperscaler build-out of 800G and 1.6T optical modules is the single largest InP demand driver at present.Hyperscale data-center upgrades drive momentum to 800G and 1.6T optics, the global rollout of 5G and preparation for 6G backhaul, as well as expanding quantum-photonics funding, while larger-diameter substrates lower unit costs and hybrid InP-on-Si platforms promise further scalability.
- **European photonics ecosystem:** A genuine regional customer base already exists.Europe leverages deep photonics expertise across Germany and the Netherlands — the Ferdinand-Braun-Institut collaborates with Fraunhofer IZM to co-design InP HBTs for terahertz radar, while SMART Photonics pushes foundry services for InP-based photonic integrated circuits, and Freiberger Compound Materials supplies VGF wafers with sub-1e4 cm⁻² dislocation density that have secured design wins in quantum-communication pilots. These same customers (Fraunhofer institutes, SMART Photonics, university photonics groups) are natural early qualification targets for a Polish entrant, particularly under a "second European source" narrative.
- **Defense/IR:** GaSb-based mid-IR sources and detectors serve missile warning, thermal imaging, gas sensing, and free-space optical communication — segments with structurally strong European defense-spending tailwinds (2025–2030 EU and NATO rearmament budgets).
- **Research/university demand:** Small-volume, high-margin, high-mix demand for research-grade wafers (universities, national labs, quantum computing groups) — a plausible first revenue segment given lower qualification barriers than hyperscale/defense supply chains.

### 2.3 Competitive Landscape
Competitive intensity stays moderate because crystal-growth know-how, long customer qualifications, and high capex deter new entrants. The practical implication: incumbents are not vulnerable to price competition from a new entrant in the near term, but **are** vulnerable to a geopolitically-motivated "second source" argument that Western/EU customers are increasingly willing to pay a premium for.

Freiberger itself, the closest direct comparable, is a mid-sized specialist: Freiberger Compound Materials was founded in 1995, is headquartered in Freiberg, Germany, and has approximately 372 total employees. This scale (a few hundred employees, decades to build) is a realistic long-run size target for NewCo — not a five-year ambition.

### 2.4 Substitution and Technology Risk
- **InP-on-Si and heterogeneous integration** could reduce long-run bulk InP wafer demand per unit of photonic output, though most industry roadmaps still require native InP substrates for gain-medium and laser layers for the foreseeable future.
- **GaN** has structurally displaced GaP and much of GaAs in lighting and increasingly in RF/power — a long-term threat to GaP demand specifically, reinforcing that GaP should be treated as a legacy/niche line rather than a growth pillar.
- **Larger-diameter wafers** (moving from 2" toward 3"/4" InP, for example) reduce customers' per-die cost and are a moving target NewCo's process technology roadmap must track from day one.

---

## 3. Product & Technology Assessment

### 3.1 Crystal Growth Methods

| Method | Best suited to | Notes |
|---|---|---|
| **Vertical Gradient Freeze (VGF) / Vertical Bridgman (VB)** | InP, GaSb, GaAs | Lower thermal stress, lower dislocation density, favored by Freiberger for high-frequency/optoelectronic-grade InP. Freiberger's VGF process makes material well-suited for devices with high current density such as HBTs, LEDs, and lasers. |
| **Liquid Encapsulated Czochralski (LEC)** | Historically GaAs, some InP | Higher throughput, historically favored for semi-insulating substrates, but generally higher dislocation density than VGF |
| **Horizontal Bridgman (HB)** | GaSb, GaP (lower purity/lower cost lines) | Simpler furnace design, lower capex, but historically lower wafer diameters and more limited scalability |

InP synthesis is carried out in a quartz glass reactor at high pressure at InP melting temperatures; phosphorus is sublimated at around 500°C and transported as a gas to a crucible with liquid indium, where the two elements react to form InP, after which the melt is directionally solidified so that non-stoichiometric components and impurities can be separated in the solid state, and single crystals are then grown from the resulting polycrystalline material after etching. This synthesis-then-growth sequence — and the associated high-pressure, high-purity quartz/graphite tooling — is the technological core NewCo must master or license, and is the single largest source of process-development risk and cost in the plan.

GaAs, InP and GaN wafers are based on single crystals grown from the melt using the LEC or VGF process, or from the gas phase using HVPE technology, with required electrical properties obtained by adding dopants to produce n-type or p-type high-resistance (greater than 10⁷ Ω·cm) or low-resistance (less than 10⁻² Ω·cm) semiconductors, and wafer surfaces finished to an epi-ready, extremely low-contamination standard.

### 3.2 Process Flow (Freiberger-analogous model)
Freiberger's production process divides into four major areas: Synthesis, Crystal Growth (front end), Mechanical Wafering, and Final Wafering (back end), with each process step carefully monitored and process control data automatically collected. NewCo's process architecture should mirror this structure:

1. **Synthesis** — high-purity elemental precursors (In, Ga, P, Sb) combined under controlled atmosphere/pressure into polycrystalline feedstock.
2. **Crystal growth (front end)** — VGF/VB furnaces producing single-crystal boules with controlled dopant profiles and low dislocation density.
3. **Mechanical wafering** — wire-saw slicing, edge-rounding, lapping.
4. **Final wafering (back end)** — chemical-mechanical polishing (CMP), cleaning, epi-ready surface finishing, metrology/characterization, and certification.

### 3.3 Product-Specific Technical Considerations
- **InP:** Highest commercial priority given market size and growth. Requires the most stringent purity, dislocation density (<10⁴ cm⁻²  is the benchmark Freiberger publicly targets for its premium product), and diameter uniformity control given photonics customers' stringent qualification standards.
- **GaP:** Lowest technical barrier of the three but weakest long-term demand outlook (GaN substitution in LEDs). Consider as a "learning product" / cash-flow bridge rather than a strategic pillar, or deprioritize entirely in favor of concentrating capital on InP and GaSb.
- **GaSb:** Technically demanding (narrow bandgap, higher native defect densities, more limited literature/process base than InP or GaAs) but the least crowded competitive field and rising strategic (defense/IR) relevance — arguably the best "differentiated first mover" opportunity for a new entrant precisely because Freiberger and Sumitomo do not aggressively compete here.

### 3.4 Quality, Characterization, and Certification
Customers will require, at minimum: X-ray diffraction (crystallographic quality), etch pit density (dislocation density) mapping, resistivity/Hall mapping, FTIR (impurity/carrier concentration), surface particle and roughness metrology (AFM, optical profilometry), and — for photonics-grade material — photoluminescence mapping. This metrology suite itself represents several million euros of capex and is not optional; it is what allows a wafer to be sold as "epi-ready" rather than merely "polished."

---

## 4. Operational & Site Feasibility

### 4.1 Site Selection Criteria
- Proximity to a technical university/research institute (talent pipeline, potential shared cleanroom/metrology infrastructure, IP collaboration) — e.g., Warsaw, Wrocław, or a location near the Institute of High Pressure Physics PAS.
- Access to Special Economic Zone (SEZ) tax incentives and Polish Investment Zone (PSI) instruments.
- Reliable, cost-competitive industrial power supply (crystal growth furnaces are energy-intensive and run continuously for days-to-weeks per boule).
- Access to bonded logistics/customs infrastructure for importing controlled/precursor materials (In, Ga, P, Sb) and exporting finished wafers under appropriate export-control classifications.
- Availability of ultrapure water, process gases (arsine/phosphine-adjacent safety infrastructure, though InP/GaP/GaSb synthesis involves red/white phosphorus and antimony rather than arsine specifically — still requiring stringent industrial hygiene and environmental permitting).

### 4.2 Facility & Equipment (Indicative, Order-of-Magnitude)
| Category | Indicative capex (EUR) | Notes |
|---|---|---|
| Cleanroom shell (Class 1000–10000, ~1,500–3,000 m²) | 15–30M | Scales with number of parallel process lines |
| Crystal growth furnaces (VGF/VB, multiple units per material) | 10–25M | Custom-built or specialist-vendor (e.g., from Japanese/German furnace makers); long lead times (12–24 months) |
| Synthesis reactors (high-pressure quartz/graphite systems) | 5–10M | Highest safety/engineering risk category |
| Wafering line (saws, lappers, CMP polishers) | 8–15M | Can be phased; shared across products where feasible |
| Metrology & characterization suite | 5–10M | XRD, Hall, FTIR, AFM, PL mapping, cleanroom inspection tools |
| Utilities, gas handling, effluent treatment, safety systems | 8–15M | Environmental permitting-driven; phosphorus/antimony byproduct handling is non-trivial |
| **Indicative total capex (Phase 1, single product line, e.g., InP or GaSb only)** | **~50–90M** | Consistent with disclosed capex ranges for comparable compound-semiconductor fabs in EU Chips Act filings |
| **Full three-product buildout (Phase 2+)** | **~120–200M+** | Only pursued after Phase 1 de-risking and qualification success |

These figures are indicative, order-of-magnitude estimates for feasibility-study purposes and must be validated via vendor quotations and a detailed engineering study before any investment decision.

### 4.3 Feedstock Supply Chain
This is the single most strategically important — and most exposed — element of the plan.

China controls the overwhelming majority of primary gallium production, and imposed export controls in 2023 that created immediate supply disruption for GaN power electronics, GaAs RF chips, and military radar systems that depend on it. As of July 2026, the SMM industrial gallium benchmark stood at roughly USD 289/kg, while the China FOB export price remained around USD 400/kg — a gap confirming that export licensing, not production economics, is the binding constraint on Western supply.

Indium prices rose 26.97% in 2023, 23.18% in 2024, and were already up 17.82% year-to-date by October 2025, with China introducing export licensing requirements for indium in February 2025 alongside gallium and germanium — with roughly 70% of refined indium still produced in China. As of June 2026, indium was priced around USD 613/kg domestically in China versus roughly USD 707/kg in the USA, with China holding a 55–60% share of global supply — strategically sensitive but, unlike gallium, not currently considered irreplaceable in the near term given some Western smelting capacity.

**Implications for NewCo:**
- Feedstock cost volatility must be built into pricing/contracts (e.g., indexed or pass-through clauses with customers), not absorbed.
- A genuine strategic rationale exists for NewCo to seek EU/Polish state support specifically framed around *reducing Chinese feedstock leverage over European semiconductor supply chains* — this is the strongest single argument in any grant/state-aid application.
- Secondary/recycled indium and gallium sourcing (e.g., from ITO recycling, or Western byproduct-of-zinc/aluminum-refining streams) should be evaluated as a hedging strategy, though volumes are limited.
- Antimony (for GaSb) and phosphorus (for InP/GaP) carry their own, distinct geopolitical concentration risk (antimony is also a Chinese-export-controlled material as of 2024), compounding the exposure across all three product lines rather than diversifying it.

### 4.4 Environmental, Health & Safety (EHS) and Permitting
- Phosphorus (white/red) handling: pyrophoric/toxic hazard requiring specialized industrial safety systems, comparable in stringency to arsine handling in GaAs fabs.
- Antimony compounds: toxicity and environmental discharge controls under REACH.
- Furnace off-gas and effluent treatment: significant permitting lead time in Poland (typically 12–24 months for a facility of this hazard class) — should be initiated in parallel with, not after, facility design.
- Poland's environmental permitting framework is EU-harmonized (IED — Industrial Emissions Directive) but local/regional implementation speed varies; site selection should explicitly weight permitting-authority track record.

### 4.5 Talent and Human Capital
This is likely the **least appreciated but most binding constraint** on the whole venture.
- Bulk III–V crystal growth is a small global expert community (arguably a few hundred to low thousands of specialists worldwide with genuine hands-on VGF/LEC production experience), concentrated in Japan, Germany, the US, and China.
- Poland has strong condensed-matter physics, materials science, and semiconductor *processing* (thin-film, CMOS-adjacent) talent, but essentially no existing industrial base of bulk III–V *crystal growers* — this expertise must be imported (retained expatriate experts, hires from Freiberger/AXT/Sumitomo alumni networks, or licensed technology transfer) or built via a multi-year internal R&D program in partnership with a Polish research institute.
- Recommend: found the technical core team around 3–6 senior crystal-growth hires with direct industrial (not only academic) experience, supplemented by a partnership with the Institute of High Pressure Physics PAS or a similar body for shared metrology/cleanroom infrastructure in the earliest phase.

---

## 5. Regulatory, Policy, and Funding Environment

### 5.1 EU Chips Act and Chips Act 2.0
Semiconductors are the third most traded commodity globally after oil and vehicles, reaching revenues of USD 700.9 billion in 2025, and the industry's role as a critical supplier to modern industry has elevated it to an important strategic resource that can be a source of geopolitical leverage for regions lacking domestic capability. The European Chips Act, in force since September 2023, has served as a catalyst for renewed momentum and investment in the European semiconductor industry as part of a broader wave of European industrial policy.

However, independent analysis is candid about its limitations to date: the European Chips Act (Regulation (EU) 2023/1781) was intended to facilitate expansion of the EU's semiconductor industry, but in terms of scale of funding mobilized and strategic coordination of deployment, it has underdelivered — prompting the Commission to plan a Chips Act 2.

The proposed Chips Act 2.0 (June 2026) is materially more favorable to a project like NewCo's than the original act: the revision clarifies the scope of first-of-a-kind projects eligible for state aid funding to include the full value chain from raw materials to advanced packaging and assembly, alongside faster permitting procedures, a new Semiconductor Regions of Excellence label, and a new "grand challenges" instrument to support R&D in critical semiconductor technologies inspired by DARPA's mission-oriented approach. It also enables State aid funding for "First-of-a-Kind" projects not yet present in the Union across the whole semiconductor value chain from raw materials to packaging, designates Strategic projects to unlock EU co-investment, and establishes a Business-to-Business Semiconductor Supply Chain Platform to improve industry resilience to supply disruptions.

Budget caution is warranted, though: Chips Act 2.0 coincides with ongoing negotiations over the EU's 2028–34 budget, and the Commission has given no indication of the funding envelope that will be dedicated to semiconductors, with officials stating that money will be scarcer and investments must be more targeted.

### 5.2 Critical Raw Materials Act
The European Critical Raw Materials Act aims to ensure a secure and sustainable supply of critical raw materials for European industry and significantly lower the EU's dependency on imports from single-country suppliers, and is the basis for building up EU capacities and strengthening resilience along all stages of the critical raw materials value chain. Gallium is explicitly named among the strategic materials this Act targets, strengthening the policy case for co-locating feedstock-adjacent processing (even partial in-house synthesis/purification) with crystal growth in the EU.

### 5.3 Poland's Position
Poland is one of nine EU Member States — alongside Austria, Belgium, Finland, France, Germany, Italy, Spain, and the Netherlands — that launched the Semiconductor Coalition, agreeing to reinforce cooperation to strengthen Europe's competitiveness and strategic autonomy in the semiconductor sector through research support, capacity expansion, and workforce development. This gives NewCo a credible national-champion narrative for both EU-level (IPCEI, Chips Act 2.0) and Polish national co-funding instruments (Polish Development Fund, National Recovery Plan/KPO funds, PARP grants).

### 5.4 State Aid Precedent
The European Commission approved €659 million in German State aid for four new semiconductor facilities in July 2026, and separately approved €76 million in German State aid for a first-of-a-kind semiconductor testing equipment facility in June 2026 — demonstrating that eight-figure-to-nine-figure state aid for specialized, first-of-a-kind semiconductor facilities is an active, currently-approved funding mechanism, not a hypothetical one. NewCo's business plan and grant strategy should be built explicitly around qualifying as a "First-of-a-Kind" project (no existing EU bulk GaSb capacity, very limited EU bulk InP capacity outside Freiberger) under this framework.

### 5.5 Export Controls (Outbound)
As a producer of dual-use materials (InP and GaSb substrates have RF/defense/photonics-adjacent applications), NewCo will itself become subject to EU dual-use export control classification and potentially to Wassenaar Arrangement-derived controls on sales outside the EU/allied bloc — a compliance function that must be built in from incorporation, not retrofitted.

---

## 6. Strategic Analysis (SWOT)

### Strengths
- First (or near-first) EU-domiciled bulk GaSb capability — genuine differentiation from Freiberger's GaAs/InP/GaN focus.
- Strong EU/Polish policy tailwinds and state-aid precedent specifically for first-of-a-kind semiconductor materials projects.
- Access to Polish/EU STEM talent pool and EU research infrastructure (Horizon Europe, IPCEI, national institutes).
- "Second European source" narrative resonates strongly with customers currently dependent on Japanese/US suppliers amid supply-chain de-risking pressure.

### Weaknesses
- Zero existing industrial track record in bulk III–V crystal growth in Poland — must build capability essentially from scratch.
- High capital intensity (tens to ~200M EUR) against an unproven Polish balance sheet/credit history in this specific vertical.
- Long customer qualification cycles (18–36 months per design-in) mean revenue lags capex by several years even after successful technical ramp.
- GaP product line has structurally weak long-term demand (GaN substitution) and should not be relied upon for financial viability.

### Opportunities
- EU Chips Act 2.0 and Critical Raw Materials Act funding windows are open now and explicitly favor exactly this kind of first-of-a-kind, raw-materials-to-substrate project.
- Growing defense/IR and quantum-photonics demand in GaSb and InP respectively, both structurally under-supplied in Europe.
- Potential for strategic partnership, technology licensing, or even minority investment from an established player (Freiberger, AXT, a Japanese trading house, or a European defense prime) seeking EU-based capacity for supply-chain resilience reasons.
- Research/university market segment offers a lower-barrier, faster path to initial revenue and real-world process validation before pursuing hyperscale/defense-grade qualification.

### Threats
- **Feedstock geopolitical risk**, with gallium, indium, and antimony all subject to Chinese export licensing and price volatility largely outside NewCo's control.Since China's export controls came into force, exports of gallium and germanium have come to a near standstill, and prices for gallium, germanium, and indium have all risen sharply, in some cases by more than 40%.
- Established incumbents (Sumitomo, Freiberger, AXT, JX Nippon) have multi-decade process know-how, existing customer qualifications, and could respond to a new entrant with pricing pressure or accelerated technology roadmaps (larger diameters, InP-on-Si) that erode the addressable niche.
- EU funding uncertainty: the Commission has not yet indicated the budget envelope for semiconductors within the 2028–34 EU budget negotiations, and has signaled that funding will be more scarce and targeted than under the original Chips Act.
- Technology substitution risk (InP-on-Si, GaN displacing GaP) could compress addressable market for two of the three initial products over a 10-year horizon.
- Talent scarcity: global pool of experienced bulk III–V crystal growers is small, and competing employers (Sumitomo, Freiberger, AXT, and Asian foundries) can outbid a new entrant for the same limited talent pool.

---

## 7. Financial Feasibility (Indicative Model)

*The following is an illustrative, order-of-magnitude financial framework for feasibility purposes. It is not a bankable financial model and should be replaced with a detailed, vendor-quote-based model before any investment committee decision.*

### 7.1 Phasing Logic
Given capital intensity and technology risk, a **single-product-first, phased approach** is strongly recommended over simultaneous three-product launch:

- **Phase 0 (Years 0–1): Feasibility, team-building, site/permits, pilot lab.** Est. spend: EUR 5–10M. Output: process validation on small-diameter boules in a partner/pilot facility (potentially hosted at a Polish research institute), core technical team hired.
- **Phase 1 (Years 1–4): First industrial line — recommend GaSb or InP.** Est. capex: EUR 50–90M. Output: qualified pilot-scale production, first design-wins with research/photonics customers, EU/national grant co-funding secured (targeting 30–50% grant coverage consistent with disclosed EU state-aid precedents for first-of-a-kind facilities).
- **Phase 2 (Years 4–7): Scale-up of Phase 1 product + addition of second product line.** Est. capex: EUR 40–80M incremental. Output: meaningful commercial revenue, expansion into RF/defense/power-electronics customer qualification.
- **Phase 3 (Years 7–10+): Third product line (if still commercially justified) and capacity expansion.** GaP addition should be reassessed at this stage based on realized demand, given the weaker long-term outlook identified in Section 2.4 — it may be dropped from the portfolio entirely in favor of doubling down on InP and GaSb.

### 7.2 Revenue Assumptions (Illustrative)
- Wafer average selling prices (ASPs) vary enormously by diameter, doping, and grade; industry-general benchmarks for research-grade small-diameter III–V wafers run from roughly EUR 200–2,000+ per wafer depending on material, diameter, and specification, with production-grade high-volume wafers commanding lower unit prices at higher volume.
- At Phase 1 maturity (Year 4–5), illustrative annual revenue of EUR 15–30M is a plausible target for a single successfully-qualified product line at modest but real commercial volume — consistent with Freiberger's scale (~250–370 employees, presumably double-digit-to-low-triple-digit-million-EUR revenue) being reached only after ~20–30 years of operation.
- Break-even at the operating level is unlikely before Year 6–8, given qualification lag, capex depreciation, and feedstock cost exposure.

### 7.3 Cost Structure Considerations
- Feedstock (Ga, In, Sb, P) exposure should be treated as a pass-through/indexed cost wherever contractually possible, given the volatility documented in Section 4.3.
- Energy costs (continuous furnace operation) are a material and somewhat controllable cost lever — site selection and energy contracting strategy should be prioritized early.
- Yield ramp (the gap between theoretical and actual usable-wafer output per boule) is typically the single largest driver of unit economics in the first 2–3 years of any new crystal-growth line, and should be modeled conservatively (initial yields well below mature-industry benchmarks are normal and expected).

### 7.4 Funding Structure (Illustrative)
| Source | Plausible role | Rationale |
|---|---|---|
| EU Chips Act 2.0 / IPCEI / First-of-a-Kind state aid | 30–50% of Phase 1 capex | Directly targeted by policy design; precedent exists for comparable German facilities |
| Polish national instruments (KPO, PARP, Polish Development Fund) | 10–20% of Phase 1 capex | National-champion / strategic-autonomy narrative |
| Private equity / strategic investor / corporate venture | 20–40% of Phase 1 capex | Likely requires a credible technical team and initial pilot-scale proof points before commitment |
| Founder/management equity | Remainder | Standard for a deep-tech capital structure |

---

## 8. Risk Register

| Risk | Category | Likelihood | Impact | Mitigation |
|---|---|---|---|---|
| Feedstock (Ga/In/Sb) price spike or export licensing delay | Supply chain / geopolitical | High | High | Indexed customer contracts; strategic stockpiling; diversified (non-Chinese) sourcing where available; EU-level advocacy via Critical Raw Materials Act mechanisms |
| Failure to reach target crystal quality (dislocation density, purity) within planned timeline | Technical | Medium-High | High | Phased pilot-scale validation before full capex commitment; partnership with experienced crystal-growth hires/licensors; realistic (conservative) Phase 1 timeline |
| Customer qualification cycle longer than planned | Commercial | High | Medium-High | Target research/university segment first (shorter qualification cycles) as revenue bridge while pursuing hyperscale/defense qualification in parallel |
| EU/Polish grant funding delayed or reduced vs. plan | Financial / policy | Medium | High | Diversify funding sources; do not size Phase 1 capex assuming maximum grant coverage; monitor Chips Act 2.0 budget negotiations closely |
| Talent acquisition shortfall | Operational | Medium-High | High | Early, aggressive recruitment of a small number of senior crystal-growth experts; competitive compensation; partnership with Polish research institutes for junior talent pipeline |
| Technology substitution (InP-on-Si, GaN displacing GaP) erodes addressable market | Strategic | Medium (GaP), Low-Medium (InP) | Medium | De-prioritize GaP; maintain technology-roadmap monitoring; focus core differentiation on GaSb where substitution risk is lowest |
| Environmental/safety incident (phosphorus, antimony handling) | EHS / regulatory | Low-Medium | Very High | Rigorous EHS design from day one; independent safety audit before operation; conservative permitting timeline |
| Incumbent competitive response (pricing, accelerated roadmap) | Competitive | Medium | Medium | Differentiate on GaSb/EU-sourcing narrative rather than competing head-on with Freiberger/Sumitomo on price or InP volume alone |

---

## 9. Recommendations

1. **Do not launch all three products simultaneously.** Commission an independent, specialist market study (Yole Group, TECHCET, or equivalent) to confirm GaSb and InP demand sizing specifically, and select a single lead product — GaSb is the more differentiated strategic choice; InP is the larger and faster-growing market. GaP should be deprioritized or dropped given weak long-term demand.
2. **Pursue EU/Polish co-funding aggressively and early**, explicitly framing the project as a Chips Act 2.0 "First-of-a-Kind" and Critical Raw Materials Act-aligned strategic autonomy project — the policy window (2026 Chips Act 2.0 negotiation) is open now but budget-constrained, so early engagement matters.
3. **Build the technical core team before committing to full-scale capex.** A 12–18 month Phase 0 pilot period, ideally hosted in partnership with an existing Polish research institute, should validate crystal-growth process viability at small scale before the EUR 50–90M Phase 1 commitment.
4. **Target research/academic and photonics-foundry customers first**, given shorter qualification cycles than hyperscale or defense-grade supply chains, to generate early revenue and real-world process feedback.
5. **Treat feedstock supply chain strategy as a first-order strategic workstream, not a procurement afterthought.** Engage directly with EU Critical Raw Materials Act implementation bodies and explore long-term offtake or strategic-reserve arrangements for gallium, indium, and antimony.
6. **Commission a bankable, vendor-quote-based financial model and independent engineering feasibility study** before any final investment decision — the figures in this report are order-of-magnitude and directional only.
7. **Build export-control and dual-use compliance capability from incorporation**, given the RF/defense/photonics-adjacent nature of the products.

---

## 10. Key References

1. Mordor Intelligence, *Indium Phosphide (InP) Wafer Market – Size, Share & Industry Analysis*, 2026. https://www.mordorintelligence.com/industry-reports/indium-phosphide-wafer-market
2. Future Market Insights, *InP Wafer Market — Global Market Analysis Report 2025–2035*, 2025. https://www.futuremarketinsights.com/reports/inp-wafer-market
3. PitchBook, *Freiberger Compound Materials Company Profile*, 2026. https://pitchbook.com/profiles/company/292367-08
4. ReportPrime, *GaAs Substrate Wafer Market Size, Growth, Forecast Till 2032*. https://www.reportprime.com/gaas-substrate-wafer-r3847
5. PatSnap Discovery, *Freiberger Compound Materials GmbH: Company Profile & Technical Research*. https://discovery.patsnap.com/company/freiberger-compound-materials/
6. Freiberger Compound Materials, *GaAs Wafer Technology*. https://freiberger.com/en/technology/
7. Freiberger Compound Materials, *Company overview*. https://freiberger.com/en/
8. Freiberger Compound Materials, *Wafers — Product overview*. https://freiberger.com/en/products/
9. Freiberger Compound Materials, *InP substrate wafer specification*. https://freiberger.com/en/products/inp-wafer/
10. Center for Strategic and International Studies (CSIS), *A World of Chips Acts: The Future of U.S.–EU Semiconductor Collaboration*, 2026. https://www.csis.org/analysis/world-chips-acts-future-us-eu-semiconductor-collaboration
11. European Commission, *Chips Act 2.0 — Shaping Europe's Digital Future*, 2026. https://digital-strategy.ec.europa.eu/en/policies/chips-act-2
12. SEMI Europe, *EU Policy Brief*, April 2026. https://www.semi.org/sites/semi.org/files/2026-05/European_Policy_Brief_April_2026.pdf
13. European Commission, *European Critical Raw Materials Act*. https://commission.europa.eu/topics/competitiveness/green-deal-industrial-plan/european-critical-raw-materials-act_en
14. EUR-Lex, *Table of Contents — Chips Act 2.0 related document*, 2026. https://eur-lex.europa.eu/legal-content/EN/TXT/HTML/?uri=CELEX%3A52026SC0504
15. Poitiers, N. and Schenk, T., *Revamping Europe's Chips Strategy: Indispensability, Not Self-Sufficiency*, Bruegel Analysis 12/2026. https://www.bruegel.org/analysis/revamping-europes-chips-strategy-indispensability-not-self-sufficiency
16. European Chips Act Tracker, *Chips Act — Updates, Compliance, Training*. https://www.european-chips-act.com/
17. European Commission, *European Chips Act — Policy News*. https://digital-strategy.ec.europa.eu/en/policies/european-chips-act
18. Science|Business, *Chips Act 2.0 Hits the Right Notes, But What About the Budget?*, 2026. https://sciencebusiness.net/industry/chips-act-20-hits-right-notes-what-about-budget
19. Rare Earth Mining, *Indium Price Today: China Spot, USA & Europe Benchmarks*, 2026. https://rare-earth-mining.com/indium-price/
20. TRADIUM, *China's Export Restrictions: Prices for Technology Metals Rise Significantly*. https://tradium.com/market-insight/china-export-control-prices/
21. Rare Earth Mining, *Gallium Price Today: Industrial Spot, FOB & Outlook*, 2026. https://rare-earth-mining.com/gallium-price/
22. Fastmarkets, *China Grants Gallium, Germanium Export Licences; Indium Fundamentals Weak: LME Week*, 2026. https://www.fastmarkets.com/insights/china-gallium-germanium-indium-prices-lme-week/
23. Critical Minerals HQ, *Gallium Market 2026 — Prices, China Export Controls, GaN Demand*. https://criticalmineralshq.com/mineral/gallium
24. Strategic Metals Invest, *Indium Price Outlook 2026 — Steady Gains as Export Controls Tighten Supply*, 2025. https://strategicmetalsinvest.com/indium-outlook-2026/
25. Strategic Metals Invest, *Indium Price — Historical Prices, 2026 Forecast*. https://strategicmetalsinvest.com/indium-prices/

---

*Disclaimer: This report is a desk-based feasibility study prepared from public sources for planning and discussion purposes. It does not constitute investment, legal, engineering, or financial advice. Market size figures, cost estimates, and financial projections are order-of-magnitude and illustrative; independent, commissioned due diligence (market study, engineering feasibility study, bankable financial model, legal/regulatory review, and freedom-to-operate/IP analysis) is required before any capital commitment.*

---

> [!NOTE]
> 
> Generated by Claude.ai
>
> Model: Sonet 5
>
> Prompt: Prepare an extensive, professional-grade feasibility study and business report for establishing a vertically integrated compound semiconductor company in Poland, modeled after companies such as Sumitomo Electric Industries (Japan) and Freiberger Compound Materials (Germany).
> 
> ## Objective
> 
> Evaluate the technical, economic, strategic, financial, and commercial feasibility of creating a Polish manufacturer specializing in the production of bulk III–V semiconductor crystals and semiconductor wafers.
> 
> The initial product portfolio should include:
> 
> - Indium Phosphide (InP)
> - Gallium Phosphide (GaP)
> - Gallium Antimonide (GaSb)
> 
> Assume that the company intends to become a European supplier of high-purity substrates for photonics, optoelectronics, RF electronics, power electronics, infrared technologies, and research laboratories.
> 
> The report should critically evaluate both the opportunities and the risks of this business venture.
> 
> ---
> 
> # Report Requirements
> 
> Prepare a detailed report of approximately 15,000–25,000 words.
> 
> Use clear Markdown formatting with hierarchical headings, tables, bullet lists, and diagrams (using Mermaid where appropriate).
> 
> ---
> 
> # Executive Summary
> 
> Provide:
> 
> - Overall assessment
> - Major opportunities
> - Major risks
> - Estimated capital requirements
> - Expected timeline to profitability
> - Key recommendations
> 
> ---
> 
> # 1. Global Compound Semiconductor Industry
> 
> Describe:
> 
> - Current market size
> - Growth trends
> - Major market drivers
> - Regional production
> - European market
> - Asian market
> - US market
> - Long-term outlook (10–20 years)
> 
> ---
> 
> # 2. Benchmark Companies
> 
> Provide detailed case studies of companies including:
> 
> - Sumitomo Electric Industries
> - Freiberger Compound Materials
> - AXT
> - Tongmei Xtal Technology
> - Vital Materials
> - Wafer Technology Ltd.
> - PAM-XIAMEN
> - DOWA Electronics Materials
> - other major integrated crystal manufacturers
> 
> For each company discuss:
> 
> - History
> - Products
> - Crystal technologies
> - Manufacturing scale
> - Competitive advantages
> - Vertical integration
> - Markets served
> - Financial performance (if publicly available)
> 
> ---
> 
> # 3. Why Poland?
> 
> Analyze:
> 
> - Geographic advantages
> - EU membership
> - Access to European customers
> - Labor costs
> - Engineering workforce
> - Universities
> - Research institutes
> - Energy costs
> - Political stability
> - Logistics
> - Export opportunities
> - Environmental regulations
> - Availability of industrial land
> 
> Compare Poland with:
> 
> - Germany
> - France
> - Czech Republic
> - Slovakia
> - Taiwan
> - Japan
> - China
> 
> ---
> 
> # 4. Product Portfolio
> 
> For each material (InP, GaP, GaSb), discuss:
> 
> - Crystal growth technologies
> - Typical crystal diameters
> - Wafer diameters
> - Market demand
> - Major applications
> - Growth rate
> - Selling prices
> - Major customers
> - Manufacturing challenges
> 
> ---
> 
> # 5. Manufacturing Strategy
> 
> Discuss:
> 
> - Vertical integration
> - Raw material purification
> - Crystal growth
> - Wafer processing
> - Polishing
> - Epitaxy compatibility
> - Quality control
> - Packaging
> - Shipping
> 
> Compare:
> 
> - Internal production
> - Outsourcing
> - Hybrid strategy
> 
> ---
> 
> # 6. Technology Requirements
> 
> Describe required technologies including:
> 
> - Czochralski growth
> - Liquid Encapsulated Czochralski (LEC)
> - Vertical Gradient Freeze (VGF)
> - Vertical Bridgman
> - Zone refining
> - High-purity synthesis
> - Wafer slicing
> - Lapping
> - CMP polishing
> - XRD
> - X-ray topography
> - Hall measurements
> - FTIR
> - ICP-MS
> - Cleanroom technologies
> 
> ---
> 
> # 7. Facility Requirements
> 
> Estimate requirements for:
> 
> - Land
> - Buildings
> - Cleanrooms
> - Crystal growth laboratories
> - Production halls
> - Chemical laboratories
> - Utilities
> - Power consumption
> - Water
> - Gas systems
> - Waste treatment
> 
> ---
> 
> # 8. Equipment
> 
> Provide a comprehensive equipment list including estimated costs for:
> 
> - Crystal pullers
> - VGF furnaces
> - Bridgman furnaces
> - CMP equipment
> - Wire saws
> - Polishing systems
> - Characterization tools
> - Cleanroom equipment
> - Vacuum systems
> - Automation
> 
> ---
> 
> # 9. Supply Chain
> 
> Discuss:
> 
> - Gallium supply
> - Indium supply
> - Antimony supply
> - Phosphorus supply
> - Crucibles
> - BN components
> - Quartz components
> - Graphite
> - High-purity gases
> 
> Evaluate geopolitical risks.
> 
> ---
> 
> # 10. Customers
> 
> Identify potential customers including:
> 
> - Wafer manufacturers
> - Epitaxy companies
> - Defense
> - Telecommunications
> - Photonics
> - Universities
> - Space industry
> - Medical devices
> 
> Estimate European market opportunities.
> 
> ---
> 
> # 11. Competition Analysis
> 
> Perform a SWOT analysis.
> 
> Evaluate:
> 
> - Competitive advantages
> - Weaknesses
> - Barriers to entry
> - Pricing pressure
> - Technology barriers
> 
> ---
> 
> # 12. Financial Analysis
> 
> Estimate:
> 
> - Capital expenditure (CAPEX)
> - Operating expenditure (OPEX)
> - Annual operating costs
> - Labor costs
> - Utility costs
> - Revenue projections
> - EBITDA
> - Cash flow
> - Break-even analysis
> - ROI
> - NPV
> - Internal Rate of Return (IRR)
> 
> Develop optimistic, realistic, and pessimistic scenarios.
> 
> ---
> 
> # 13. Funding Opportunities
> 
> Analyze potential funding from:
> 
> - European Union programs
> - Polish government grants
> - Horizon Europe
> - European Investment Bank
> - Private equity
> - Venture capital
> - Strategic industrial investors
> 
> ---
> 
> # 14. Risk Assessment
> 
> Discuss:
> 
> - Technical risks
> - Market risks
> - Financial risks
> - Geopolitical risks
> - Export controls
> - Environmental regulations
> - Intellectual property
> - Supply-chain disruptions
> 
> Rank risks by probability and impact.
> 
> ---
> 
> # 15. Development Roadmap
> 
> Create a phased implementation plan covering:
> 
> - Company formation
> - Facility construction
> - Equipment procurement
> - Process development
> - Pilot production
> - Customer qualification
> - Volume production
> - International expansion
> 
> Provide estimated timelines and milestones.
> 
> ---
> 
> # 16. Strategic Recommendations
> 
> Recommend:
> 
> - Whether the company should be established
> - Most attractive product mix
> - Recommended growth technologies
> - Recommended level of vertical integration
> - Key strategic partnerships
> - Potential acquisition targets
> - Long-term expansion opportunities
> 
> ---
> 
> # References
> 
> Provide at least 100 real, verifiable references, including:
> 
> - Peer-reviewed journal articles
> - Books
> - Industry reports
> - Market analyses
> - Government publications
> - EU policy documents
> - Company annual reports
> - Technical standards
> 
> Requirements:
> 
> - Do not invent references.
> - Verify that all references exist.
> - Include DOI for journal papers whenever available.
> - Include publication year.
> - Clearly distinguish academic sources from industry sources.
> 
> ---
> 
> # Output Requirements
> 
> - Produce the report entirely in Markdown.
> - Use professional technical writing suitable for investors, government agencies, and industrial stakeholders.
> - Include numerous tables summarizing costs, markets, competitors, technologies, and risks.
> - Include Mermaid flowcharts, organizational diagrams, and strategic roadmaps where appropriate.
> - Clearly distinguish evidence-based conclusions from assumptions and explicitly state any uncertainties.
