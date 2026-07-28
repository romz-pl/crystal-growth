# Greenfield GaSb Czochralski Crystal Growth Facility — Techno-Economic Analysis

**Scope:** Industrial-scale production of semiconductor-grade Gallium Antimonide (GaSb) single-crystal boules via Liquid-Encapsulated Czochralski (LEC) growth, from polycrystalline synthesis through boule inspection, sized for downstream wafer manufacturing. Wafer slicing/lapping/polishing (SLP) is treated as an optional downstream module and costed separately.

**Baseline plant assumption:** 2″–3″ (50–76 mm) diameter GaSb boules, semi-insulating/undoped or lightly doped (n- and p-type), nominal nameplate capacity of **150–200 boules/year** (≈ 400–600 kg finished single-crystal material/year), expandable to 3-inch/4-inch product mix. This scale corresponds to a "first industrial module" — a single clean-room bay with 6–10 LEC pullers — rather than a merchant-scale GaAs-style fab. All figures are order-of-magnitude engineering estimates (±30–40%) suitable for a pre-FEL (Front-End Loading) / conceptual (Class 4–5 AACE) cost estimate; a bankable estimate requires vendor quotations.

---

## 1. Process & Technology Basis

GaSb melts congruently at 712 °C with a modest antimony vapor pressure at the melting point (far lower than GaAs or InP), so GaSb **does not strictly require LEC encapsulation for stoichiometry control** the way arsenides do — many groups grow GaSb by conventional CZ under inert gas with only light B₂O₃ encapsulation or none at all. However, industrial practice still commonly retains a B₂O₃ or alkali-halide (LiCl+KCl) liquid encapsulant to suppress oxidation, control the free melt surface, and improve diameter control, and this is the configuration costed here.<cite index="1-1,2-1">Commercial bulk single-crystal GaSb is usually grown by the liquid encapsulated Czochralski (LEC) growth method, and although this method is well established and produces good quality material, microfacets, impurity striations, and twinning have been reported frequently.</cite>

Key process steps costed in this facility:

1. **Elemental precursor purification/verification** — incoming Ga (6N–7N) and Sb (6N–7N) QC.
2. **In-situ or ex-situ polycrystalline GaSb synthesis** from stoichiometric Ga+Sb melt.
3. **Seed crystal preparation** (GaSb ⟨100⟩ or ⟨111⟩ oriented seeds).
4. **LEC/CZ pulling** — seeding, necking, shouldering, body growth, tailing, under B₂O₃ encapsulant, controlled inert (N₂/Ar) or low-pressure atmosphere, resistive multi-zone graphite heating.
5. **Post-growth annealing** (dislocation/stress relief).
6. **Boule inspection & grading** — resistivity (four-point probe / eddy current), etch-pit density (EPD) via defect etch, XRD rocking curve, IR transmission, visual/twin inspection.
7. **Boule-end cropping, ID surface grinding, orientation flats/notches.**
8. *(Optional module)* **Wafer slicing, lapping, polishing, epi-ready finishing.**

Process modeling and yield optimization increasingly rely on coupled global heat-transfer/melt-convection simulation: <cite index="3-1">CGSim, a simulation software integrating the finite element method with machine learning techniques, has been used to optimize the heat flux and crystallization front morphology at the solid–liquid interface during GaSb crystal growth, reducing the protrusion angle at the melt–crystal interface</cite> and improving dislocation density outcomes. This is consistent with your existing crystal-growth simulation reference library (CGSim, CrysMAS, FEMAG-CZ) and should be used during process qualification rather than treated as a one-off R&D expense.

---

## 2. CAPEX — Capital Expenditure Breakdown

### 2.1 Land, Site & Civil Works

| Item | Basis | Estimated Cost (USD) |
|---|---|---|
| Land acquisition/lease (industrial zone, ~3,000–5,000 m²) | Purchase or long lease, EU/PL industrial park rates | $0.5M – $1.5M |
| Site preparation & civil works | Grading, foundations, utilities routing | $0.8M – $1.5M |
| Building shell (steel-frame industrial building, ~2,000–3,000 m²) | Includes crane bay for furnace installation/servicing | $2.5M – $4.5M |
| Clean-room build-out (ISO Class 7–8 / Class 10,000, ~500–800 m²) | Growth bay + inspection lab; HEPA filtration, gowning | $1.5M – $3.0M |
| HVAC, process cooling water loop, compressed air, N₂/Ar gas distribution | Facility infrastructure | $1.0M – $2.0M |
| Electrical substation & power distribution | See §2.4 for load sizing | $1.5M – $3.0M |
| Fire suppression, EHS systems (toxic gas detection — Sb/As dust) | Code compliance | $0.4M – $0.8M |
| **Subtotal — Land, Site & Civil** | | **$8.2M – $16.3M** |

### 2.2 Crystal Growth Process Equipment

This is the core capital block. LEC/CZ pullers for III–V antimonides are specialized, low-volume equipment (a handful of global suppliers: AXT-adjacent tooling, PVA TePla/Crystal Growing Systems lineage, Cyberstar, GT Advanced-derived puller platforms, and Chinese suppliers e.g. supplying the domestic GaSb/InSb market).

| Item | Specification | Unit Cost (USD) | Qty | Total (USD) |
|---|---|---|---|---|
| LEC/CZ crystal puller, high-pressure (up to ~100 bar), 3-zone resistive graphite heating, automated diameter control, ⌀4–8″ crucible capability | <cite index="7-1">Mark IV-class pullers for AIIIBV compounds (GaP, InP, GaSb, GaAs, InAs), high-pressure LEC up to 100 bar, crystals up to 4″ diameter and ~30 cm length, multi-heater graphite system to 1800 °C, diameter control system, pBN or quartz crucibles 4″–8″</cite> | $0.9M – $1.6M | 6–10 | $5.4M – $16.0M |
| Precision weighing/diameter-control sensor packages (if not bundled) | Load-cell + optical diameter sensing, automated PID pull-rate/rotation control | $50k – $100k | 6–10 | $0.3M – $1.0M |
| pBN (pyrolytic boron nitride) and quartz crucibles (spares/consumable capital float) | Initial inventory of pBN crucibles, 4″–6″ | $3k – $8k/unit | 40–60 | $0.15M – $0.4M |
| In-situ synthesis reactor / pre-alloying furnace (if not synthesizing directly in the puller) | Sealed quartz-ampoule or two-zone horizontal furnace for stoichiometric Ga+Sb pre-reaction | $150k – $350k | 1–2 | $0.15M – $0.7M |
| Seed crystal preparation & orientation station (X-ray Laue orienter, wire saw for seed cropping) | | $150k – $300k | 1 | $0.15M – $0.3M |
| Post-growth annealing furnace(s) | Controlled-atmosphere box/tube furnace, up to ~600–700 °C | $80k – $180k | 2 | $0.16M – $0.36M |
| Inert gas supply system (N₂/Ar purification, high-pressure gas handling for LEC) | Purity ≥6N gas, pressure regulation to 100 bar | $0.3M – $0.6M | 1 | $0.3M – $0.6M |
| Furnace cooling water skids (closed-loop, DI water, chillers) | | $0.2M – $0.4M | 1 | $0.2M – $0.4M |
| **Subtotal — Growth Process Equipment** | | | | **$6.85M – $19.76M** |

### 2.3 Boule Finishing & Metrology Equipment

| Item | Purpose | Estimated Cost (USD) |
|---|---|---|
| ID (internal diameter) diamond grinding station | Boule cylindrical grinding to spec diameter | $0.25M – $0.5M |
| Wire/blade cropping saw (boule end removal, seed/tail crop) | | $0.15M – $0.3M |
| Orientation flat/notch grinder | | $0.1M – $0.2M |
| Four-point-probe resistivity mapper | Electrical characterization | $0.08M – $0.15M |
| Hall-effect measurement system (mobility, carrier concentration) | | $0.15M – $0.3M |
| X-ray diffractometer (double-crystal rocking curve, DCXRC) | <cite index="3-1">Crystal quality evaluated through X-ray double crystal rocking curves</cite> and orientation verification | $0.3M – $0.6M |
| Chemical defect-etch station + optical/EPD counting microscope | Etch-pit density (dislocation density) measurement, fume-hooded | $0.15M – $0.3M |
| FTIR/IR transmission spectrometer | Optical quality, free-carrier absorption | $0.1M – $0.2M |
| Glow-discharge mass spec (GDMS) or ICP-MS (outsourced or in-house) | Trace impurity certification | $0.3M – $0.8M (in-house) or opex if outsourced |
| Optical inspection microscopes, twin/grain boundary detection | | $0.05M – $0.15M |
| **Subtotal — Finishing & Metrology** | | **$1.63M – $3.50M** |

### 2.4 Utilities, Power & EHS Infrastructure

GaSb LEC growth is power-intensive: multi-zone resistive graphite heaters running near 1000–1050 °C melt temperature (GaSb melts at 712 °C, but graphite hot-zone components typically run hotter) for 24–72 hour pull cycles, per puller, at high pressure.

| Item | Basis | Estimated Cost (USD) |
|---|---|---|
| Dedicated MV/LV electrical substation, backup generation | ~1.5–3 MW connected load for 6–10 pullers + facility | $1.5M – $3.0M *(also listed in §2.1; avoid double count — reconcile at rollup)* |
| Uninterruptible power supply (UPS) for in-process boules | Loss of power mid-pull can scrap a boule | $0.2M – $0.5M |
| Toxic/pyrophoric gas monitoring (Sb dust, B₂O₃ handling, potential arsine cross-contamination controls if co-located with GaAs) | EHS compliance | $0.2M – $0.4M |
| Effluent/wastewater treatment (Sb-bearing process water) | Antimony is a regulated water pollutant | $0.3M – $0.6M |
| Solid waste handling (Sb/Ga scrap reclamation stream) | Feeds into recycling economics, §5 | $0.1M – $0.2M |
| **Subtotal — Utilities/EHS (incremental, excluding substation already counted)** | | **$0.8M – $1.7M** |

### 2.5 Optional Downstream Module — Wafer Slicing, Lapping & Polishing (SLP)

If the facility is to deliver finished wafers rather than boules only:

| Item | Estimated Cost (USD) |
|---|---|
| Multi-wire slicing saw (diamond wire, ⌀2–4″ capable) | $0.4M – $0.8M |
| Lapping machines (double-side) | $0.2M – $0.4M |
| Chemical-mechanical polishing (CMP) stations | $0.5M – $1.2M |
| Wafer cleaning line (spin-rinse-dry, wet benches) | $0.3M – $0.6M |
| Wafer metrology (thickness/TTV, particle counting, surface roughness AFM) | $0.3M – $0.6M |
| **Subtotal — SLP Module (optional)** | **$1.7M – $3.6M** |

### 2.6 Indirect & Soft Costs

| Item | Basis | Estimated Cost (USD) |
|---|---|---|
| Engineering, procurement & construction management (EPCM) | ~10–15% of direct capital | $1.5M – $4.0M |
| Process qualification & pilot runs (material scrap, engineering time, simulation licenses — CGSim/CrysMAS/FEMAG) | 6–12 months qualification campaign | $0.5M – $1.2M |
| Spare parts & commissioning stock | 5–8% of equipment capital | $0.5M – $1.5M |
| Permitting, environmental impact assessment, licensing (EU/PL industrial + hazardous materials handling) | | $0.2M – $0.5M |
| Contingency | 15–25% of total direct + indirect (standard for Class 4–5 estimate) | $2.5M – $7.0M |
| **Subtotal — Indirect/Soft Costs** | | **$5.2M – $14.2M** |

### 2.7 CAPEX Summary (Boules-Only Facility, Excl. SLP Module)

| Category | Low (USD) | High (USD) |
|---|---|---|
| Land, Site & Civil | 8.2M | 16.3M |
| Growth Process Equipment | 6.85M | 19.76M |
| Finishing & Metrology | 1.63M | 3.50M |
| Utilities/EHS (incremental) | 0.8M | 1.7M |
| Indirect & Soft Costs | 5.2M | 14.2M |
| **Total CAPEX (boules only)** | **≈ $22.7M** | **≈ $55.5M** |
| *Add: SLP downstream module* | *+1.7M* | *+3.6M* |
| **Total CAPEX (boules + finished wafers)** | **≈ $24.4M** | **≈ $59.1M** |

A minimal "pilot-industrial" configuration (2–3 pullers, no SLP, minimal building) could enter service near the low end of the boules-only range, or below it (~$12–18M) if an existing industrial shell is leased rather than built new. A full 10-puller merchant facility with in-house wafering trends toward or above the high end.

---

## 3. OPEX — Operating Expenditure Breakdown

Basis: steady-state annual operation, single facility scale as above (150–200 boules/yr, 6–10 pullers), assumed 3-shift or 2-shift continuous operation given multi-day pull cycles.

### 3.1 Raw Materials

GaSb stoichiometry is 1:1 molar Ga:Sb; by mass, GaSb is ~48.4 wt% Ga / 51.6 wt% Sb (atomic masses Ga 69.72, Sb 121.76).

| Material | Grade | Approx. Market Price (2026) | Annual Consumption (est.) | Annual Cost (USD) |
|---|---|---|---|---|
| Gallium metal | 6N–7N (semiconductor grade) | <cite index="18-1">Retail gallium price ≈ $2,269/kg as of July 2026, up sharply from ~$300/kg in 2020</cite>; bulk industrial 6N pricing typically carries a purity premium over the 4N benchmark <cite index="29-1">where primary low-purity (99.99%-pure) gallium prices in China have themselves risen to the $380–420/kg range</cite> — assume **$2,000–3,500/kg** for 6N–7N bulk industrial contract pricing | ~250–350 kg/yr | $0.5M – $1.2M |
| Antimony metal | 6N–7N | Base antimony metal trades far below gallium (tens of $/kg for metallurgical grade) but 6N-7N semiconductor-grade Sb carries a substantial refining premium; assume **$150–400/kg** for 6N+ | ~270–380 kg/yr | $0.04M – $0.15M |
| Boron oxide (B₂O₃) encapsulant | Anhydrous, semiconductor grade | $50–150/kg | ~500–1,000 kg/yr (partial reuse/recovery possible) | $0.03M – $0.15M |
| pBN/quartz crucible consumption (replacement, not initial capital fill) | Single-use or limited-reuse per campaign | $3k–8k/crucible | 80–150 crucibles/yr | $0.3M – $0.9M |
| Seed crystals, dopants (Te, Sn, Zn, etc., ppm-level) | High-purity dopant sources | Minor | — | $0.05M – $0.15M |
| High-purity inert gas (N₂/Ar) | Bulk or on-site generation | | | $0.1M – $0.3M |
| **Subtotal — Raw Materials** | | | | **$1.02M – $2.85M** |

Note: gallium market volatility is a first-order commercial risk for this business — <cite index="25-1">the gallium market changed in 2023 when China introduced export licensing for several gallium products, exports dropped sharply and even fell to zero for a period, tightening availability outside China and lifting prices, and most analysts expect continued upward pressure on prices through the second half of the 2020s absent scaled recycling and new recovery projects</cite>. A GaSb producer outside China is directly exposed to this feedstock risk and should budget for price hedging or long-term supply contracts, and should design the process for maximal Ga/Sb reclamation from scrap (§5).

### 3.2 Direct Labor

| Role | Headcount (est.) | Fully-Loaded Annual Cost/FTE (Warsaw/PL industrial, 2026) | Annual Cost (USD) |
|---|---|---|---|
| Crystal growth operators (3-shift coverage for 6–10 pullers) | 10–16 | $35k – $55k | $0.35M – $0.88M |
| Process/materials engineers (growth recipe development, defect analysis) | 3–5 | $55k – $85k | $0.17M – $0.43M |
| Metrology/QA technicians | 4–6 | $30k – $50k | $0.12M – $0.30M |
| Maintenance & facilities technicians | 3–5 | $35k – $55k | $0.11M – $0.28M |
| EHS/compliance officer | 1 | $50k – $75k | $0.05M – $0.08M |
| Plant/operations management | 2–3 | $70k – $110k | $0.14M – $0.33M |
| Supply chain/procurement | 1–2 | $45k – $70k | $0.05M – $0.14M |
| **Subtotal — Direct Labor** | ~24–38 FTE | | **$0.99M – $2.44M** |

*(Employer social-security overhead in Poland typically adds ~20% on top of gross salary; figures above are treated as fully loaded.)*

### 3.3 Utilities (Energy, Water, Gas)

| Item | Basis | Annual Cost (USD) |
|---|---|---|
| Electricity | 6–10 pullers × ~15–30 kW average draw during multi-day pulls + facility HVAC/clean-room load ≈ 1.5–3 MW connected, ~40–55% average utilization → ~5–12 GWh/yr at industrial PL rates (~€0.12–0.20/kWh) | $0.6M – $2.2M |
| Process cooling water & DI water | | $0.1M – $0.25M |
| Inert/process gases (bulk N₂, Ar beyond raw-material line above — facility purge, glovebox inerting) | | $0.1M – $0.2M |
| **Subtotal — Utilities** | | **$0.8M – $2.65M** |

### 3.4 Maintenance, Spares & Equipment Upkeep

| Item | Basis | Annual Cost (USD) |
|---|---|---|
| Preventive/corrective maintenance on pullers (heater elements, seals, pressure vessels) | ~6–10% of process equipment CAPEX/yr | $0.4M – $2.0M |
| Metrology equipment calibration/service contracts | | $0.1M – $0.25M |
| Facility maintenance (HVAC, clean-room filters, building) | | $0.15M – $0.35M |
| **Subtotal — Maintenance** | | **$0.65M – $2.6M** |

### 3.5 Quality, Compliance & Outsourced Analytical Services

| Item | Annual Cost (USD) |
|---|---|
| Outsourced GDMS/trace-impurity certification (if not run in-house) | $0.1M – $0.3M |
| ISO 9001 / customer qualification audits, quality system maintenance | $0.05M – $0.15M |
| Environmental compliance monitoring & reporting (Sb effluent, hazardous waste manifesting) | $0.05M – $0.15M |
| **Subtotal — QA/Compliance** | **$0.2M – $0.6M** |

### 3.6 SG&A, Insurance, IP & Overheads

| Item | Basis | Annual Cost (USD) |
|---|---|
| General & administrative overhead | | $0.3M – $0.7M |
| Property & equipment insurance | ~0.5–1% of CAPEX/yr | $0.15M – $0.5M |
| Sales, marketing, technical customer support (given niche/qualified-customer market) | | $0.2M – $0.5M |
| R&D / continuous process improvement (simulation licensing, growth-recipe optimization, yield engineering) | | $0.2M – $0.5M |
| **Subtotal — SG&A** | | **$0.85M – $2.2M** |

### 3.7 OPEX Summary (Annual, Steady-State, Boules-Only)

| Category | Low (USD/yr) | High (USD/yr) |
|---|---|---|
| Raw Materials | 1.02M | 2.85M |
| Direct Labor | 0.99M | 2.44M |
| Utilities | 0.80M | 2.65M |
| Maintenance & Spares | 0.65M | 2.60M |
| QA/Compliance | 0.20M | 0.60M |
| SG&A/Insurance/R&D | 0.85M | 2.20M |
| **Total Annual OPEX** | **≈ $4.5M** | **≈ $13.3M** |

If the SLP wafering module is included, add wafering labor (~4–8 additional technicians, $0.15–0.4M/yr), consumables (slurry, diamond wire, polishing pads: $0.2–0.6M/yr), and incremental utilities/maintenance (~$0.15–0.4M/yr) — roughly **+$0.5M to +$1.4M/yr**.

---

## 4. Yield, Throughput & Unit Economics (Illustrative)

Bulk LEC/CZ growth of III–V antimonides has materially lower single-crystal yield than silicon CZ, driven by dislocation generation from the encapsulant's low thermal conductivity and thermal-gradient-induced defects: <cite index="8-1">the low thermal conductivity of the liquid encapsulant causes large temperature gradients and large temperature non-linearities in the growing crystal, which is unfavorable with respect to crystal quality as a relatively large number of structural defects are generated</cite>. Reported process improvements illustrate the scale of the yield-optimization opportunity: <cite index="1-1">in one LEC growth study, increasing the crystal growth temperature gradient from 5 to 7 °C/cm reduced dislocation density by 55% (from ~3,928 to ~1,785 cm⁻²) and improved carrier mobility by nearly 30%</cite>, though <cite index="1-1">pushing the gradient further to 9 °C/cm caused the crystallinity to deteriorate sharply</cite> — underscoring that gradient/process-window control is a first-order yield lever requiring the simulation-driven optimization referenced in §1.

| Parameter | Assumption |
|---|---|
| Pull cycle time (2–3″ boule, seed-to-tail) | 24–48 hours process + ~24 hours cool-down/turnaround |
| Pullers × cycles/year (allowing for maintenance downtime, ~70% uptime) | 6–10 pullers × ~150–200 cycles/yr combined |
| Single-crystal (usable boule) yield | 50–75% of pulls (typical for antimonide LEC; lower than Si CZ, comparable to or better than GaAs LEC once process-optimized) |
| Average finished boule mass (2–3″, single-crystal usable length) | ~1.5–3.5 kg |
| **Estimated annual finished single-crystal output** | ~150–450 kg/yr at this scale |

At the current commercial reference point, 3-inch GaSb wafers retail at roughly **€700–1,700/wafer** depending on grade and finish, per publicly listed pricing<cite index="10-1">, where a single 3" wafer (625±25 μm, epi-ready or testing grade) is quoted around €813–1,699 per piece with volume discounts</cite> — useful as a sanity check for back-calculating boule-equivalent revenue potential, though large customers negotiate substantially below list price.

---

## 5. Cost-Reduction Levers & Risk Factors

- **Gallium price/supply risk dominates raw-material OPEX.** Given China's export-licensing regime and structurally rising prices, securing long-term Ga supply contracts (or qualifying non-Chinese refiners) and maximizing **scrap/tailings reclamation** (recovering Ga and Sb from crucible residues, boule ends, and off-spec material via re-melt) materially de-risks the cost base.
- **Yield engineering is the single highest-leverage OPEX/CAPEX lever.** Because crucibles, dopants, and furnace time are consumed regardless of whether a pull yields usable single crystal, moving usable-boule yield from ~50% toward ~75%+ has an outsized effect on effective $/kg cost — this is where continued investment in melt-convection/interface-shape simulation (CGSim, FEMAG-CZ, CrysMAS — already in your reference library) pays back fastest.
- **Alternative growth methods** (VGF/Bridgman) are reported to produce lower dislocation density GaSb than LEC in some studies<cite index="2-1">, though polycrystalline growth is more common with Bridgman and an encapsulant is still needed to prevent melt–crucible contact and suppress polycrystalline nucleation</cite> — worth evaluating as a second-generation process route or parallel product line for defect-sensitive customers (e.g., IR detector substrates).
- **Furnace utilization** is the primary fixed-cost absorber: a facility running at 40% of nameplate pulls has roughly double the effective $/kg fixed-cost burden of one at 80%. Ramp-up financing should assume 18–30 months to reach steady-state utilization given the need for process qualification per product grade/orientation/doping.
- **Co-location synergies:** if built adjacent to an existing III–V (GaAs/InP) fab, several utility, EHS, and metrology capital items can be shared, plausibly reducing the low-end CAPEX estimate by 15–25%.

---

## 6. Key References

1. Study on liquid encapsulated Czochralski GaSb crystal growth technology — *Journal of Piezoelectric and Acoustooptic*, 2016. https://www.researchgate.net/publication/309579291
2. GaSb single-crystal growth by vertical gradient freeze — *ScienceDirect / Journal of Crystal Growth*. https://www.sciencedirect.com/science/article/abs/pii/S002202480401485X
3. Investigating the Growth of GaSb Single Crystals through Optimized LEC Method Utilizing Finite Element Simulation and Machine Learning Techniques — *ACS Omega*, 2025. https://pubs.acs.org/doi/10.1021/acsomega.5c08508
4. Liquid Encapsulation and Related Technologies for the Czochralski Growth of Semiconductor Compounds. https://www.researchgate.net/publication/282597001
5. LEC (Liquid Encapsulated Czochralski) Crystal Growing Equipment — vendor technical overview. https://abachy.com/catalog/semiconductor-equipment/wafer-manufacturing-equipment/crystal-growing-equipment/lec-liquid-encapsulated-czochralski-crystal-growing-equipment
6. Czochralski Process — overview, *ScienceDirect Topics*. https://www.sciencedirect.com/topics/chemistry/czochralski-process
7. Liquid-Encapsulated Czochralski (LEC) Growth System — Mark IV puller specifications, Ensemble3. https://ensemble3.eu/liquid-encapsulated-czochralski-(lec)-growth-system
8. Apparatus for manufacturing a compound-semiconductor single crystal by the LEC process — US Patent 4,668,481. https://patents.justia.com/patent/4668481
9. Gallium Antimonide (GaSb) Wafers — commercial pricing reference, Nanografi. https://shop.nanografi.com/silicon-wafers-semiconductor-wafers/gallium-antimonide-gasb-wafers/
10. LEC Gallium Antimonide (GaSb) Wafer specifications — PAM-XIAMEN. https://www.powerwaywafer.com/gasb-gallium-antimonide-wafer.html
11. Gallium Price Today & Historical — 2026 market data, Strategic Metals Invest. https://strategicmetalsinvest.com/gallium-prices/
12. USGS Mineral Commodity Summaries 2025 — Gallium. https://pubs.usgs.gov/periodicals/mcs2025/mcs2025-gallium.pdf
13. Gallium Refining: Processes, Purity Grades, and Supply Chain Geography (2026) — GalliumPrice.com. https://galliumprice.com/supply-chain/refining/
14. Gallium market commentary and 2023–2026 export-control impact — EarthRarest. https://earthrarest.com/gallium/price/
15. Antimony Prices — Shanghai Metals Market (SMM). https://www.metal.com/antimony

---

## 7. Summary Table

| | Low Estimate | High Estimate |
|---|---|---|
| **Total CAPEX (boules only)** | $22.7M | $55.5M |
| **Total CAPEX (boules + wafers/SLP)** | $24.4M | $59.1M |
| **Annual OPEX (boules only)** | $4.5M | $13.3M |
| **Annual OPEX (+ SLP)** | $5.0M | $14.7M |
| **Estimated annual output** | ~150 kg | ~450 kg finished single-crystal material |

*All figures are conceptual-level (AACE Class 4–5) estimates for planning purposes. A bankable feasibility study requires: (a) formal vendor RFQs for pullers and metrology equipment, (b) a detailed process qualification plan with target device specifications, (c) site-specific utility tariffs and construction quotations, and (d) a locked feedstock supply agreement given current Ga/Sb market volatility.*

---

> [!NOTE]
> 
> Generated by Claude.ai
>
> Model: Sonet 5
>
> Prompt: Role: Act as a semiconductor manufacturing consultant specializing in III–V compound semiconductor production, crystal growth, industrial engineering, and techno-economic analysis. I plan to build a greenfield industrial production facility for manufacturing Gallium Antimonide (GaSb) single crystals grown from the melt using the Czochralski (CZ) process. The facility should produce semiconductor-grade GaSb boules for wafer manufacturing. Provide an extensive, structured, and technically detailed cost breakdown covering both the capital expenditures (CAPEX) required to establish the facility and the operating expenditures (OPEX) required to maintain and operate it. Provide key references. Show the output in Markdown format.
