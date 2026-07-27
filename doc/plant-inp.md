# Greenfield InP Single-Crystal (LEC/CZ) Production Facility — Techno-Economic Cost Breakdown

**Scope:** A dedicated facility for growing semiconductor-grade Indium Phosphide (InP) single-crystal boules from the melt via the Liquid-Encapsulated Czochralski (LEC) process — the industry-standard variant of CZ used for InP because of phosphorus's high dissociation pressure at the melting point (1062 °C, ~27.5 atm P₂ over-pressure). Output basis: undoped semi-insulating (Fe-doped) and n-type (S-doped) boules, 2"–4" diameter (with a path to 6"), suitable for downstream slicing/lapping/polishing into substrate wafers. Wafering/polishing is treated as a downstream, optionally integrated operation and is broken out separately (Section 6).

Note on methodology: public, audited capital-cost disclosures for InP-specific LEC lines are not published by any producer (AXT, Sumitomo Electric, IQE, InPACT, Freiberger — all treat this as proprietary). Figures below are therefore a bottom-up engineering estimate built from (a) known compound-semiconductor furnace/equipment pricing, (b) GaAs LEC/VGF plant analogues (a closely related process and cost structure), (c) raw-material market pricing, and (d) general specialty-fab construction benchmarks. Treat all numbers as **order-of-magnitude planning estimates (±30–40%)**, not vendor quotes.

---

## 1. Executive Summary

| Category | Low-end estimate | High-end estimate |
|---|---|---|
| Total CAPEX (crystal-growth-only facility, ~5,000–8,000 boules/yr capacity, 2"–4") | **US$18–25 million** | **US$45–65 million** |
| Total CAPEX if wafering/polishing line integrated | +US$8–15 million | +US$20–35 million |
| Annual OPEX (steady-state, growth-only) | **US$6–9 million/yr** | **US$14–20 million/yr** |
| Approx. cost per finished 3" boule (fully loaded) | US$1,200–2,000 | US$3,000–5,000 |
| Typical project timeline (greenfield, permits→first boule) | 24 months | 42 months |

Two scale scenarios are carried throughout this document:

- **Scenario A — Pilot/Specialty fab:** 4–6 LEC pullers, ~1,000–2,000 boules/yr, 2"–3" diameter, target markets = photonics, LiDAR, HBT/HEMT RF.
- **Scenario B — Volume fab:** 20–30 LEC pullers, ~8,000–12,000 boules/yr, 3"–4" diameter (6" R&D line), target = telecom laser diode substrates, PIC foundries, high-volume optical transceiver supply chain.

---

## 2. Process & Facility Overview (basis for cost model)

### 2.1 Core process steps
1. **Precursor synthesis** — high-purity In (7N) + red/black P (7N) reacted to form polycrystalline InP charge (in-situ synthesis furnace, or purchased pre-synthesized poly-InP).
2. **LEC crystal growth** — poly-InP + B₂O₃ encapsulant loaded into a pBN (pyrolytic boron nitride) crucible inside a high-pressure (~50–100 atm) puller; seeded pull under controlled rotation, typically 3–8 mm/h growth rate, multi-day pull cycles (36–96 h per boule depending on diameter/length).
3. **Post-growth conditioning** — anneal (dislocation/stress relief), boule inspection (XRD, resistivity, EPD/etch-pit density mapping), end-cropping.
4. **QA/QC & certification** — resistivity mapping, Hall measurement (for SI material), FTIR for carbon, GDMS for trace metals, EPD, twin/grain inspection.
5. *(Optional, Section 6)* Wafering: ID-saw or wire-saw slicing → lapping → edge profiling → DSP/CMP polishing → cleaning → packaging.

### 2.2 Facility zoning implications for cost
- **Cleanroom core (crystal growth + metrology):** ISO Class 7–8 (Class 10,000–100,000) is generally sufficient for LEC growth (unlike front-end wafer fabs); tighter ISO 5–6 needed only in wafering/polish finishing bay.
- **Hazardous materials handling:** phosphorus (pyrophoric red/white P forms, toxic PH₃ off-gas risk), arsenic-free but still requires SEMI S2/S8-class EHS engineering, scrubbers, and gas monitoring.
- **High-pressure vessel safety:** pullers operate as pressure vessels (ASME Section VIII code equipment) — driving both CAPEX (certified vessels, interlocks) and permitting timeline.
- **Utilities:** substantial 3-phase power for resistive/RF heating, high-purity argon/N₂ supply, process cooling water, compressed dry air, and phosphine/toxic-gas abatement.

---

## 3. CAPITAL EXPENDITURE (CAPEX)

### 3.1 Land, Site & Buildings

| Item | Scenario A (pilot) | Scenario B (volume) | Notes |
|---|---|---|---|
| Land acquisition (3–8 ha, industrial-zoned) | $0.5–1.5M | $1.5–3M | Highly region-dependent; figures assume Central/Eastern Europe or similar mid-cost industrial land |
| Building shell (steel-frame industrial, incl. slab, structural) | $2–3.5M | $6–10M | ~2,000–3,500 m² (A) vs. 8,000–15,000 m² (B) |
| Cleanroom build-out (ISO 7–8 core, HVAC, HEPA, pressure cascades) | $1.5–2.5M | $5–9M | $1,500–3,000/m² typical for this ISO class |
| EHS infrastructure (P/PH₃ scrubbers, gas cabinets, emergency systems, fire suppression) | $0.8–1.5M | $2.5–4.5M | Driven by phosphorus/phosphine hazard class |
| Site utilities tie-in (power substation, water, gas, waste) | $0.5–1M | $1.5–3M | |
| **Subtotal — Site & Buildings** | **$5.3–10M** | **$16.5–29.5M** | |

### 3.2 Process Equipment

| Item | Unit cost | Scenario A qty/cost | Scenario B qty/cost |
|---|---|---|---|
| LEC/HP-CZ crystal puller (high-pressure vessel, multi-zone heater, automated diameter control) | $0.7–1.8M each | 4–6 units → $3.5–8M | 20–30 units → $16–40M |
| Poly-InP synthesis furnace/reactor (if in-house synthesis) | $0.4–0.9M each | 1–2 → $0.5–1.2M | 3–5 → $1.5–3.5M |
| pBN crucible sets & consumable tooling (initial stock) | $15–40k/crucible; multi-use but limited-life | $0.2–0.4M | $0.8–1.5M |
| Post-growth anneal furnaces | $80–200k each | 2 → $0.2–0.4M | 6 → $0.6–1.2M |
| Metrology & QC suite (XRD, Hall/resistivity mapping, FTIR, EPD/etch station, GDMS access or outsourced) | Bundle | $1–2M | $2.5–4.5M |
| Material handling (glovebox lines, inert-atmosphere transfer, robotics for load/unload) | Bundle | $0.6–1.2M | $2–4M |
| Gas delivery & purification systems (Ar/N₂ purifiers, VOC/PH₃ abatement) | Bundle | $0.5–1M | $1.5–3M |
| Facility monitoring/SCADA & process control software | Bundle | $0.3–0.6M | $0.8–1.5M |
| **Subtotal — Process Equipment** | | **$6.8–14.8M** | **$26.7–59.2M** |

*Basis: mid-range production-grade CZ/LEC systems for compound semiconductors run roughly $300k–$1.5M per unit depending on automation and size; the pressurized, multi-heater LEC configuration required for InP/GaAs sits toward the upper half of that band given ASME-certified pressure vessel requirements and multi-zone thermal control.*

### 3.3 Utilities & Support Infrastructure

| Item | Scenario A | Scenario B |
|---|---|---|
| Electrical supply upgrade + backup generation (crystal growth is power-intensive, multi-day continuous pulls — UPS/genset critical to avoid pull loss) | $0.8–1.5M | $2.5–4.5M |
| Process cooling water / chillers | $0.3–0.6M | $1–2M |
| Compressed/inert gas farm (bulk Ar, N₂, specialty gas storage) | $0.4–0.8M | $1.2–2.5M |
| Effluent/waste treatment (P-bearing solid & liquid waste, B₂O₃ recovery/handling) | $0.3–0.7M | $1–2M |
| **Subtotal — Utilities** | **$1.8–3.6M** | **$5.7–11M** |

### 3.4 Soft Costs

| Item | Scenario A | Scenario B |
|---|---|---|
| Engineering, design, project management (10–15% of hard cost) | $1.4–2.9M | $4.9–9.9M |
| Permitting, EHS licensing, regulatory (hazardous materials handling license, pressure-vessel certification) | $0.3–0.6M | $0.8–1.5M |
| Commissioning, qualification runs, process yield ramp (material + engineering time to first qualified boule) | $0.8–1.8M | $2.5–5M |
| Contingency (15–20%) | $2.1–4.2M | $8–13M |
| **Subtotal — Soft Costs** | **$4.6–9.5M** | **$16.2–29.4M** |

### 3.5 CAPEX Total

| | Scenario A (pilot) | Scenario B (volume) |
|---|---|---|
| **Total CAPEX** | **~$18.5–37.9M** | **~$65.1–129M** |

*(Note: the Executive Summary range narrows Scenario B's upper bound; treat the range above as the full sensitivity band including aggressive contingency assumptions. A disciplined build with strong local incentives and re-used shell buildings lands nearer the low end.)*

---

## 4. OPERATING EXPENDITURE (OPEX)

### 4.1 Raw Materials

| Input | Approx. market price (2025–2026) | Consumption basis |
|---|---|---|
| Indium (7N, semiconductor grade) | $250–450/kg (indium metal prices are volatile; China supply-dominant) | ~0.48 kg In per kg InP (mass fraction) |
| Red/white phosphorus (7N-equivalent electronic grade) | $8–20/kg (bulk P), higher for ultra-high-purity | ~0.28 kg P per kg InP |
| Boron oxide (B₂O₃) encapsulant | $15–40/kg | Consumed per run, ~1–3 kg per growth run depending on crucible size |
| pBN crucibles | $15,000–40,000 each, limited reuse cycles (typically 3–10 runs before degradation) | Major recurring consumable cost |
| Dopants (Fe for SI, S/Sn/Zn for n/p-type) | Minor cost, high purity premium | ppm-level addition |
| High-purity Ar/N₂ gas | Bulk industrial gas contract pricing | Continuous purge during multi-day pulls |
| **Estimated raw material cost per kg of InP charge** | **~$180–320/kg** | Before yield losses |

Because single-crystal yield (usable boule mass vs. charge mass) in LEC InP growth is often **50–70%** (lower than more mature Si/GaAs processes, consistent with the ~25% yield penalty reported industry-wide for compound-semiconductor crystal growth versus mature materials), the **effective raw-material cost per kg of shippable single-crystal InP is roughly $280–550/kg** before further wafering losses.

### 4.2 Consumables & Maintenance

| Item | Scenario A (annual) | Scenario B (annual) |
|---|---|---|
| pBN crucible replacement | $0.3–0.6M | $1.5–3M |
| Heater elements, insulation packs, seed rods | $0.15–0.3M | $0.6–1.2M |
| Gas consumption (Ar/N₂/specialty) | $0.2–0.4M | $0.8–1.6M |
| Preventive maintenance & spare parts (puller mechanicals, pressure-vessel seals, vacuum pumps) | $0.3–0.6M | $1.2–2.2M |
| Metrology consumables (etchants, standards, calibration) | $0.1–0.2M | $0.3–0.6M |
| **Subtotal** | **$1.05–2.1M** | **$4.4–8.6M** |

### 4.3 Utilities (operating)

| Item | Scenario A (annual) | Scenario B (annual) |
|---|---|---|
| Electricity (multi-day, multi-zone resistive heating is the dominant utility cost — each puller draws roughly 15–40 kW average over a 2–4 day pull) | $0.6–1.2M | $2.5–5M |
| Process cooling water | $0.05–0.1M | $0.2–0.4M |
| Compressed air / facility HVAC | $0.1–0.2M | $0.4–0.8M |
| **Subtotal** | **$0.75–1.5M** | **$3.1–6.2M** |

### 4.4 Labor

| Role | Headcount (A) | Headcount (B) | Fully loaded cost/head (EU mid-cost region) |
|---|---|---|---|
| Crystal growth operators/technicians | 8–14 | 30–50 | $35–55k |
| Process/crystal growth engineers | 3–5 | 10–15 | $60–90k |
| QC/metrology staff | 3–4 | 8–12 | $45–65k |
| Maintenance/facilities technicians | 2–4 | 8–12 | $40–60k |
| EHS/regulatory compliance | 1–2 | 3–5 | $50–70k |
| Management/admin/quality systems | 3–5 | 8–12 | $55–80k |
| **Total annual labor cost** | **$1.1–1.9M** | **$4.5–7.5M** | |

*(Labor costs assume a Central European or similarly mid-cost manufacturing labor market; a US or Western European site would run 30–60% higher, a South/East Asian site 40–60% lower.)*

### 4.5 Overheads & Other

| Item | Scenario A (annual) | Scenario B (annual) |
|---|---|---|
| Facility overhead (insurance, property tax, general admin) | $0.3–0.6M | $0.9–1.8M |
| Waste handling/disposal (P-bearing waste, B₂O₃ reclaim/disposal) | $0.15–0.3M | $0.5–1M |
| Quality system & certification maintenance (ISO 9001, customer PPAP-style audits) | $0.1–0.2M | $0.3–0.6M |
| Depreciation (equipment, 8–12 yr useful life — non-cash but relevant to full cost) | $0.7–1.5M | $3–6M |
| **Subtotal** | **$1.25–2.6M** | **$4.7–9.4M** |

### 4.6 OPEX Total (steady-state, excluding depreciation for cash-OPEX view)

| | Scenario A | Scenario B |
|---|---|---|
| Raw materials (at target volume) | $1.5–2.8M | $9–16M |
| Consumables & maintenance | $1.05–2.1M | $4.4–8.6M |
| Utilities | $0.75–1.5M | $3.1–6.2M |
| Labor | $1.1–1.9M | $4.5–7.5M |
| Overheads (excl. depreciation) | $0.55–1.1M | $1.7–3.4M |
| **Total cash OPEX** | **~$5–9.4M/yr** | **~$22.7–41.7M/yr** |
| Plus depreciation (non-cash) | +$0.7–1.5M | +$3–6M |

---

## 5. Yield, Throughput & Unit Economics

### 5.1 Throughput assumptions

| Parameter | Scenario A | Scenario B |
|---|---|---|
| Pullers | 4–6 | 20–30 |
| Pull cycle time (incl. load/cool/unload) | 4–6 days | 4–6 days |
| Runs per puller per year (accounting for maintenance downtime) | ~50–65 | ~50–65 |
| First-pass single-crystal yield (crack-free, on-spec, low EPD/twin-free) | 50–70% | 55–70% (learning-curve improvement at scale) |
| Boules/year | ~1,000–2,000 | ~8,000–13,000 |

### 5.2 Indicative fully-loaded cost per boule

| | Scenario A | Scenario B |
|---|---|---|
| Cash OPEX ÷ boules/yr | ~$3,000–6,000/boule | ~$2,000–4,000/boule |
| CAPEX amortization contribution (10-yr straight-line ÷ boules/yr) | ~$900–1,900/boule | ~$500–1,000/boule |
| **Indicative fully-loaded unit cost** | **~$4,000–7,900/boule** | **~$2,500–5,000/boule** |

This is directionally consistent with market pricing context: the InP wafer market is valued in the low hundreds of millions of dollars globally with a low-double-digit CAGR, <cite index="2-1">and reflects a material that carries persistent upward price pressure due to indium scarcity and technically demanding, long-cycle-time growth</cite> — meaning boule-level unit economics here should be read as a floor cost, not a market price; commercial ASPs for finished wafers embed substantial further wafering/polishing value-add and margin.

---

## 6. Optional Downstream: Wafering & Polishing Line (if vertically integrated)

Many InP producers integrate slicing/lapping/polishing rather than sell boules; if in scope:

| Item | Additional CAPEX | Additional annual OPEX |
|---|---|---|
| Wire saws / ID slicing (multi-wire, slurry or diamond-wire) | $2–5M | Consumables (wire, slurry): $0.5–1.2M/yr |
| Lapping & edge-profiling stations | $1–2.5M | $0.2–0.5M/yr |
| DSP/CMP polishing (double-side polish, chemical-mechanical) | $3–6M | Pads, slurry, chemicals: $0.8–2M/yr |
| Cleanroom upgrade to ISO 5–6 for polish/final inspection | $2–4M | HVAC/utility delta: $0.3–0.6M/yr |
| Metrology upgrade (surface roughness, TTV, particle counting) | $1–2M | $0.15–0.3M/yr |
| Additional labor (slicing/polish operators, +15–30 heads at scale) | — | $0.7–1.8M/yr |
| **Subtotal (wafering integration)** | **$9–19.5M** | **$2.65–6.4M/yr** |

---

## 7. Key Cost Sensitivities & Risk Factors

1. **Indium price volatility** is the single largest raw-material risk — indium is a byproduct metal (mainly from zinc refining) with thin global supply and price swings of 2–3× over multi-year cycles; long-term supply contracts materially de-risk OPEX.
2. **Crystal yield is the dominant unit-economics lever.** Moving first-pass yield from 55% to 70% has a larger unit-cost impact than most CAPEX optimizations — process control (thermal field modeling, vibration isolation, automated diameter/pressure control) merits disproportionate engineering investment.
3. **pBN crucible costs and reuse cycles** are a recurring, underappreciated OPEX driver; crucible life is sensitive to thermal cycling protocol.
4. <cite index="1-1">Manufacturing yields for semiconductor-grade compound-semiconductor crystal growth often run roughly 25% lower than for more mature semiconductor materials</cite>, which should be built into ramp-curve planning rather than assumed away in year-1 projections.
5. **Scale economics are real but non-linear**: Scenario B's per-boule cost is lower than Scenario A's largely because of labor and overhead dilution, not raw material efficiency — raw material cost per kg is comparable across scale.
6. **Larger-diameter transition (4"→6") risk**: <cite index="8-1">4-inch InP substrates are considered the likely near-term mainstream product succeeding 2-inch, with 6-inch development still oriented toward mass-production readiness rather than being currently mainstream</cite> — a facility designed only for 2"–3" risks obsolescence against the industry's roadmap; puller vessels sized for future diameter upgrades cost more upfront but protect against a costly retrofit.
7. **Regulatory/EHS costs** (phosphorus handling, pressure vessel certification) are a fixed-ish cost that hits pilot-scale facilities disproportionately hard on a per-boule basis — a strong argument for right-sizing Scenario A only if a credible path to volume exists.

---

## 8. Key References

- Technavio, *Indium Phosphide (InP) Wafers Market Growth Analysis — Size and Forecast 2026-2030*, market and yield-challenge overview.
- WaferWorld, *Understanding the InP Wafer Market: Prices in 2025, Prospects, and More* (Nov. 2025).
- Shanghai Famous Trade Co. / ZMSH Semitech, *How Is Indium Phosphide (InP) Manufactured? A Scientific Overview from Crystal Growth to Photonic Devices* (2026).
- Firebird Optics, *Indium Phosphide (InP) Wafers* — process/wafering overview.
- DISCO Corporation, *Processing of Indium Phosphide (InP)* — LEC process description.
- PowerWay Wafer, *Monocrystalline InP Substrate Wafer* — diameter roadmap (2"→4"→6").
- PowerWay Wafer, *Gallium Arsenide Single Crystal Growth Process: LEC, VB, VGF* — analogous LEC process/equipment detail.
- Freiberger Compound Materials, *GaAs Wafer Technologie* — LEC puller/crucible/process engineering detail (closely analogous plant).
- OSHA, *Semiconductors — Ingot Growing* — LEC/Bridgman process safety and equipment description.
- IMARC Group, *Gallium Arsenide Production Plant Cost, Setup, DPR 2026* — analogous compound-semiconductor plant CAPEX/OPEX category structure.
- Taoxia Intelligent Equipment, *How Much Is the Crystal Growing Furnace Price in 2025? Cost Guide* — furnace/puller pricing benchmarks.
- Materials Research Furnaces (MRF), *Crystal Growth Furnaces* — CZ/Bridgman equipment specification reference.
- Friedrich, S., *Erlangen — An Important Center of Crystal Growth and Epitaxy*, Crystal Research and Technology, 2020 — historical LEC puller development for III-V materials.
- Springer, *MLEK crystal growth of (100) indium phosphide*, Journal of Electronic Materials — alternative/advanced InP growth technique reference.

---

*Disclaimer: This document is a planning-level techno-economic estimate assembled from public secondary sources and standard industrial engineering cost-estimation practice. It is not a substitute for vendor quotations, a bankable feasibility study, or site-specific engineering (EPC) estimates, which should be commissioned before any capital commitment.*

---

> [!NOTE]
> 
> Generated by Claude.ai
>
> Model: Sonet 5
>
> Prompt: Role: Act as a semiconductor manufacturing consultant specializing in III–V compound semiconductor production, crystal growth, industrial engineering, and techno-economic analysis. I plan to build a greenfield industrial production facility for manufacturing Indium Phosphide (InP) single crystals grown from the melt using the Czochralski (CZ) process. The facility should produce semiconductor-grade InP boules for wafer manufacturing. Provide an extensive, structured, and technically detailed cost breakdown covering both the capital expenditures (CAPEX) required to establish the facility and the operating expenditures (OPEX) required to maintain and operate it.
> Provide key references. Show the output in Markdown format.
