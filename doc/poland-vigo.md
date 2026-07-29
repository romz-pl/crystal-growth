# VIGO Photonics and the Development of a Polish Compound Semiconductor Crystal Growth and Wafer Ecosystem

*A technical and economic assessment*

---

## 1. Executive Summary

VIGO Photonics S.A. (WSE: VGO), headquartered in Ożarów Mazowiecki near Warsaw, is Poland's only vertically integrated compound-semiconductor manufacturer with an unbroken production chain running from crystal/epitaxial material growth through detector chip fabrication, hybridization, and module-level system integration. Founded in 1987 as Vigo System and rebranded in 2022, the company has built nearly four decades of continuous know-how in II-VI (HgCdTe, CdTe, CdZnTe) and III-V (InAs, InAsSb, GaAs, InP) compound semiconductor materials science, initially in service of mid-wave and long-wave infrared (MWIR/LWIR) photon detectors for defense, industrial process control, and scientific instrumentation markets.

The company's strategic pivot — the **HyperPIC** project, a photonic integrated circuit (PIC) foundry initiative backed by up to **EUR 102.9 million** in European Commission state aid under the IPCEI ME/CT framework, part of a wider ~**PLN 1 billion** investment programme (~PLN 430 million of which is EU-funded) — is intended to establish Poland's first dedicated semiconductor factory, with production targeted for 2029. This positions VIGO as the most credible existing anchor for a national compound semiconductor crystal growth and wafer ecosystem, though important caveats apply regarding scale, materials scope, and the gap between epitaxial-wafer competence and true bulk boule growth.

This report evaluates VIGO's technical assets, its economic trajectory, and its fit as an R&D and industrial partner for Poland's ambitions in compound semiconductor materials, and closes with recommendations for how a national ecosystem could be built around, or alongside, VIGO's existing capability.

---

## 2. Company Profile and History

| Attribute | Detail |
|---|---|
| Legal name | VIGO Photonics S.A. (formerly Vigo System S.A.) |
| Founded | 1987 (rebranded 2022, on its 35th anniversary) |
| Headquarters | Ożarów Mazowiecki, Poland |
| Listing | Warsaw Stock Exchange main market, since 2014 (ticker VGO) |
| Employees | 450–500 (2025) |
| Ownership | Adam Piotrowski (majority owner and CEO) |
| International footprint | U.S. subsidiary (VIGO Photonics Corp.); Taiwan office since 2020 |
| Core products | MWIR/LWIR photon detectors, detection modules, epitaxial wafers, semiconductor materials |
| 2024 revenue | PLN 78.3 million (+4% y/y); adjusted EBITDA PLN 6.8 million |

VIGO's origin lies in Polish military and academic infrared-detector research, and it retains deep institutional ties to the **Military University of Technology (WAT)** in Warsaw, with whom it operates a joint laboratory researching medium-wavelength infrared HgCdTe photodetectors. This defense-and-metrology heritage is commercially significant: from 2023 to 2025, VIGO's largest sales growth came from a 78% increase in military contracts and a 42% increase in semiconductor manufacturing sales, and its products supply the Polish Ministry of Defense with detectors for smart ammunition, armored-vehicle and fire detection, and thermal-distribution sensors, several of which have civilian dual-use analogues such as railway axle and brake monitoring.

---

## 3. Technical Capabilities Relevant to Crystal Growth and Wafer Manufacturing

### 3.1 Materials portfolio

VIGO's core semiconductor system is **mercury cadmium telluride (Hg₁₋ₓCdₓTe, "MCT")**, the workhorse infrared-detector material, supplemented by **III-V antimonide/arsenide compounds (InAs, InAsSb)** and III-V epitaxial platforms (**GaAs, InP**) for photonic device fabrication.

Historically, MCT detector fabrication in the industry proceeded through several material-growth generations:

$$
\text{Bulk melt growth (historical)} \;\rightarrow\; \text{LPE} \;\rightarrow\; \text{MOCVD} \;\rightarrow\; \text{MBE}
$$

The fabrication of HgCdTe detectors was initially based on the growth of bulk crystals from melts, whereas present devices rely on epitaxial growth of HgCdTe from the liquid phase (LPE) and gas phase (MOCVD, MBE), with epitaxial techniques allowing low-temperature growth of high-quality HgCdTe heterostructures on CdTe and on alternative low-cost substrates such as GaAs and silicon. This is the same trajectory VIGO's own process technology has followed. VIGO's technical literature confirms the use of molecular beam epitaxy (MBE) for manufacturing bulk InAs, InAsSb, and superlattice InAs/InAsSb detectors, whose strong covalent III-V bonding yields a higher operating-temperature range, better crystal uniformity, and improved optical/electrical parameters, alongside a Planetary Reactor MOCVD system used for GaAs- and InP-based III-V epitaxial structures serving photonic devices (VCSELs, QCLs, photodetectors) and microelectronic devices.

The company itself frames its production chain end to end: VIGO is equipped with a complete production line for photonic products and semiconductor materials, spanning crystal growth, epitaxy (both MBE and MOCVD), processing, and packaging, and separately describes a complete front-end and back-end production line for semiconductor high-capacity instruments — from epitaxy of II-VI and III-V compounds, through detector chips, lasers, and their assembly and integration with electronics.

### 3.2 What "crystal growth" means in VIGO's context

A technically important distinction for anyone assessing VIGO as a *bulk crystal growth* partner (in the sense familiar from Czochralski, Bridgman/VGF, or THM boule-growth practice) is that VIGO's core competence, as documented in the public record and patent/technical literature on the MCT industry generally, is predominantly **epitaxial** rather than **bulk melt** growth:

- CdTe and CdZnTe (CZT) **bulk substrates** — the classical lattice-matched growth templates for HgCdTe epitaxy — are, industry-wide, difficult and costly to produce at large area. HgCdTe has conventionally been grown on a bulk substrate such as CdTe and CdZnTe, but it is difficult to form a large-area bulk substrate of these materials, which has historically motivated growth on alternative substrates such as GaAs, Si, or a GaAs layer on Si, despite the larger lattice mismatch and resulting higher dislocation density such substrates introduce. CdTe and CdZnTe single crystals, while the most widely used substrates for epitaxial HgCdTe growth, are expensive, difficult to produce with large area, and fragile and difficult to handle, and CdZnTe single-crystal substrates in particular remain in limited supply and are expensive, with only a small fraction of a boule typically suitable for adequate lattice matching to the HgCdTe film.
- This substrate scarcity is precisely why the entire industry, VIGO included, migrated toward **LPE, MOCVD, and MBE epitaxial growth on alternative or foreign substrates** as the dominant production route rather than reliance on bulk single-crystal boules.
- The transition from HgCdTe bulk crystal to epitaxial technologies such as LPE, MOCVD, and MBE enabled large-area HgCdTe material formation, together with associated wet/dry etching, passivation (via CdTe or dielectric overlayers), and ohmic-contact technologies using indium and gold metallization for n-type and p-type material respectively.

**Implication:** VIGO possesses world-class, decades-deep expertise in **compound semiconductor epitaxial growth and heterostructure engineering** (MBE, MOCVD, LPE) and in the downstream device, packaging, and system-integration steps. It is not, on current public evidence, a bulk boule-growth house in the sense of large-diameter CdZnTe, GaAs, or InP ingot pulling comparable to specialist bulk-crystal producers (e.g., AXT, Freiberger, 5N Plus, or Yamanashi/Sumitomo-type operations for III-V boules). A national ecosystem strategy should treat VIGO's strength as the **epitaxy-to-device** segment of the value chain and consider it a *downstream* rather than *upstream* (boule/ingot) node — a distinction with direct consequences for how a "compound semiconductor crystal growth and wafer" cluster should be architected around it (see Section 6).

### 3.3 Photonic Integrated Circuits (PIC) and the HyperPIC project

VIGO's forward strategy centers on mid-infrared and short-wave infrared **Photonic Integrated Circuits**. VIGO aims to gain a leading position in the MWIR PIC market while acquiring significant share of the SWIR-based PIC market, an endeavor that includes establishing a complete mid-infrared PIC production line via its EU-backed HyperPIC project, which seeks to construct a dedicated foundry between 2023 and 2026 before bringing PIC into production.

The financing structure is substantial by Polish industrial-policy standards: the HyperPIC project forms part of the European Important Projects of Common European Interest in Microelectronics and Communication Technologies (IPCEI ME/CT), intended to strengthen the European microelectronics industry alongside other major European semiconductor companies, with total eligible project costs of EUR 253.4 million and EU state aid approved up to EUR 102.9 million (41% of eligible costs). The stated ecosystem ambition is explicit in VIGO's own communications: the project is expected to enable the "Polonisation" of the supply chain, spur development of a Polish photonic technology cluster, create jobs across the project's partner and customer ecosystem, and attract engineering talent to Poland.

Independent corroboration places the capital scale even higher when including domestic co-financing: in April 2025 VIGO received an investment of PLN 1 billion, 430 million of which came from EU funds to increase European semiconductor manufacturing capacity; this funding is intended to expand the company's detector production line from 100,000 to 1 million units per year and grow staff from roughly 200 to 450–500, with the resulting dedicated facility set to become the first semiconductor factory in Poland, with production expected to begin in 2029.

### 3.4 Vertical integration as an ecosystem asset

VIGO's principal structural advantage is vertical integration across a chain that most compound-semiconductor start-ups or national programmes must instead assemble from several separate companies: material growth, epitaxy, chip fabrication (etching, passivation, contacts), detector hybridization/packaging, and system-level electronics integration all occur in-house. This reduces the number of external dependencies a Polish ecosystem would otherwise need to import, and gives VIGO direct commercial feedback loops between materials R&D and end-market performance (a rarity for pure-play material suppliers).

---

## 4. Economic and Market Position

### 4.1 Recent financial trajectory

| Metric | 2024 | Q1 2025 |
|---|---|---|
| Consolidated revenue | PLN 78.3 million (+4% y/y) | PLN 22 million (+39% y/y) |
| Adjusted EBITDA | PLN 6.8 million (-54% y/y) | — |
| Adjusted net profit | PLN -3.7 million (vs. PLN 8.9 million profit prior year) | — |
| Detectors/modules sales | — | PLN 20.9 million (+47% y/y) |
| Semiconductor materials sales | segment +42% y/y to PLN 8.8 million (full-year 2024) | PLN 1.2 million (-26% y/y, Q1 2025) |
| Military segment | +78% y/y to PLN 23.2 million (2024) | PLN 6.6 million, up ~50% y/y |
| Industrial segment | -11% y/y (2024) | +55% y/y to PLN 10.5 million |

A few economic conclusions follow:

1. **Growth is real but margin-compressed.** Revenue growth in 2024–2025 is solid (mid-single to high-double digits depending on segment) but 2024 adjusted EBITDA fell by more than half year-on-year and the company posted an adjusted net loss — consistent with a company in a heavy investment/scale-up phase (HyperPIC construction, facility build-out, US acquisition) rather than harvesting mode.
2. **Defense and industrial demand, not semiconductor-materials sales, are currently the profit engine.** The semiconductor-materials line is still small in absolute terms (PLN ~9 million/year) relative to detector/module sales; it is a strategic, R&D-adjacent segment more than a current cash generator. This matters for partner risk assessment: HyperPIC's success is a bet on transforming a currently modest materials-and-PIC line into the company's primary growth vector.
3. **Geographic diversification is underway but Europe-centric.** 65% of VIGO's products are sold within the European Union, complemented by expansion moves such as the 2026 acquisition of InfraRed Associates in the U.S. (a USD 8.4 million transaction finalizing the acquisition of assets from InfraRed Associates, Inc., a leading American infrared-detector manufacturer, as part of VIGO's geographical expansion and market-strengthening strategy, with the acquired assets held by VIGO Photonics Corp., the company's U.S. subsidiary) and a Taiwan office opened in 2020 that accounted for 19% of company revenue in 2022.
4. **State-aid dependency is significant and typical of EU chip-sovereignty programmes.** With ~41% of eligible HyperPIC costs coming from EU state aid, VIGO's expansion is materially underwritten by the Chips for Europe Initiative / IPCEI ME/CT framework rather than by organic cash flow — a structure common across the sector (Intel, STMicroelectronics/GlobalFoundries, and others have received comparable IPCEI support) but one that ties VIGO's build-out timeline and risk profile to continued EU political and funding commitment.

### 4.2 Strategic market position

VIGO is repeatedly and independently characterized as Poland's principal semiconductor-sector asset. The "Semiconductor Industry in Poland 2026" report, published by tek.info.pl with support from the Polish Investment and Trade Agency (PAIH) and SEMI, highlighted VIGO as a key pillar of the domestic deep-tech ecosystem and a global market leader in semiconductor photonics, a recognition driven primarily by its expansion and PIC technology development. VIGO's leadership has also positioned the company as an articulator of national strategy rather than merely a beneficiary of it: at ISS Europe 2026 in Sopot, CEO Adam Piotrowski presented on "The Polish Ecosystem of Semiconductors and its Strategic Key Project — HyperPIC," framing advanced photonics and infrared sensing as essential pillars of the future semiconductor landscape amid a fragmented global supply chain, and emphasizing VIGO's role in strengthening Europe's industrial competitiveness and supply-chain sovereignty.

VIGO also participates in the broader European Chips JU pilot-line architecture, though not as lead coordinator: the EU's flagship **PIXEurope** PIC pilot line, the fifth Chips JU pilot line selected under the Chips for Europe Initiative, is coordinated by **ICFO (Barcelona)**, with a consortium involving participating entities from Austria, Belgium, Finland, France, Ireland, Italy, Poland, Portugal, the Netherlands, and the United Kingdom, co-financed by the Spanish Ministry for Digital Transformation and the Civil Service and supported by the Generalitat of Catalonia. Poland's participation in PIXEurope is real but auxiliary; VIGO's *own* HyperPIC project is the nationally led, Poland-headquartered complement to this pan-European effort, and is the more consequential vehicle for a Polish-anchored ecosystem strategy.

---

## 5. Assessment as an R&D and Industrial Partner

### 5.1 Strengths

- **Only vertically integrated compound-semiconductor manufacturer of scale in Poland**, spanning epitaxy through system integration — a rare combination that would otherwise require assembling multiple separate firms.
- **Nearly 40 years of continuous operating history** in a technically demanding materials segment (MCT), with proprietary in-house process technology rather than licensed/imported production lines.
- **Established academic-industrial link with the Military University of Technology**, providing a functioning technology-transfer channel between fundamental materials research and production — a template that could extend to other Polish technical universities (Warsaw University of Technology, AGH Kraków, Wrocław University of Science and Technology) for a broader materials-science talent pipeline.
- **Substantial, already-secured EU capital commitment** (up to EUR 102.9 million state aid within a EUR 253.4 million project, and a PLN ~1 billion combined investment package), meaningfully de-risking the initial capital-formation stage of a national ecosystem project.
- **Credible international commercial reach** (US subsidiary, Taiwan office, ~65% EU sales share), suggesting HyperPIC output would face export markets, not merely subsidized domestic demand.
- **Government and industry-body endorsement** (PAIH, SEMI-supported reporting, national-pavilion representation at SEMICON Taiwan) that provides institutional legitimacy for VIGO as an ecosystem anchor rather than a purely private commercial actor.

### 5.2 Limitations and risks

- **Epitaxy-centric, not bulk-boule-centric.** As detailed in §3.2, VIGO's demonstrated core competence is epitaxial growth (MBE/MOCVD/LPE) and device fabrication, not large-diameter bulk ingot/boule growth of CdZnTe, GaAs, InP, or SiC. A national strategy aiming for a full "crystal growth and wafer" ecosystem — i.e., one that includes upstream substrate/boule production — cannot rely on VIGO alone for that upstream segment and should treat this as a capability gap to be filled by a separate partner, a new venture, or targeted technology transfer/licensing (e.g., partnerships with established bulk-crystal producers).
- **Financial profile currently in an investment/negative-margin phase.** 2024's EBITDA decline and net loss, while explainable by expansion capex, mean VIGO's balance sheet currently has less independent financial slack than its revenue figures alone would suggest; ecosystem planning should not assume VIGO can self-fund adjacent ecosystem investments beyond HyperPIC without further public co-financing.
- **Small absolute scale by global semiconductor standards.** At PLN 78 million (~EUR 18 million) 2024 revenue and 450–500 employees, VIGO remains a specialist niche player rather than a large-scale fab operator; comparisons to full-scale compound-semiconductor foundries (Vitesse, Wolfspeed, IQE, or major CMOS foundries) should be calibrated accordingly. HyperPIC's stated goal of scaling detector output tenfold (100k → 1M units/year) is significant relative to VIGO's own history but modest relative to global wafer/chip production volumes.
- **State-aid and EU-political dependency.** Because a large share of expansion funding flows through the Chips for Europe Initiative / IPCEI ME/CT, the project's timeline (2029 production start) is exposed to EU budgetary and political cycles, not solely to VIGO's execution capability.
- **Defense-sector revenue concentration** raises export-control and dual-use considerations for any international R&D partnerships built around VIGO's detector lines — a factor relevant to how open (versus security-vetted) a resulting ecosystem's collaboration model can be.
- **Single-material-system depth versus breadth.** VIGO's deepest expertise is HgCdTe/II-VI infrared materials; its III-V and photonic-integration work, while real and growing (GaAs/InP MOCVD, PIC R&D), is comparatively newer. A broad compound-semiconductor ecosystem (e.g., one also targeting GaN power electronics or SiC for automotive/energy applications) would need additional partners beyond VIGO's current materials scope.

### 5.3 Fit assessment

| Ecosystem function | VIGO fit | Notes |
|---|---|---|
| II-VI (HgCdTe/CdTe) epitaxial growth R&D | **Strong** | Core, decades-proven competence |
| III-V (GaAs/InP/InAs) epitaxial growth (MOCVD/MBE) | **Strong** | Actively used for photonic and microelectronic devices |
| Bulk boule/ingot growth (CdZnTe, GaAs, InP, SiC) | **Weak / absent on current evidence** | Industry-wide substrate scarcity is the very driver of epitaxial substitution; no public evidence of VIGO large-diameter boule capability |
| Wafer-level device fabrication & packaging | **Strong** | Full front-end/back-end line in-house |
| PIC design, foundry, and pilot-line development | **Emerging, well-funded** | HyperPIC is the central vehicle; timeline to 2029 |
| Talent pipeline / academic linkage | **Moderate-to-strong** | WAT partnership; extendable to other institutions |
| Export/commercialization channel | **Moderate-to-strong** | EU (~65%), US subsidiary, Taiwan office |
| Financial self-sufficiency for further scale-up | **Limited near-term** | Currently EBITDA-compressed, state-aid dependent |

---

## 6. Recommendations for a Polish Compound Semiconductor Ecosystem Strategy

1. **Use VIGO as the anchor for the epitaxy-to-device (mid/downstream) segment**, not as a sole-source solution for upstream bulk crystal growth. HyperPIC should be treated as the flagship demonstrator of what a Polish PIC/photonics ecosystem node can achieve, while a parallel initiative targets bulk substrate capability.
2. **Commission or attract a dedicated bulk-crystal-growth partner** (domestic academic groups with Bridgman/VGF/Czochralski expertise, or an international substrate producer via joint venture) to close the upstream gap identified in §3.2 and §5.2 — particularly for CdZnTe and GaAs/InP boule production, where global supply concentration (and associated geopolitical exposure) is a recognized strategic vulnerability for any sovereign semiconductor ambition.
3. **Formalize and broaden the academic-industry linkage model** already proven with the Military University of Technology, extending it to Warsaw University of Technology, AGH University of Kraków, and Wrocław University of Science and Technology, to build a domestic pipeline of crystal-growth and epitaxy specialists (a talent category in chronic short supply even in mature semiconductor economies).
4. **Align ecosystem timelines to HyperPIC's 2029 production target**, using the intervening years for capacity-building in adjacent capabilities (metrology, characterization, defect engineering, process simulation) that can plug directly into VIGO's pilot line once operational.
5. **Monitor and hedge the state-aid dependency**, since continued Chips for Europe Initiative funding and EU political commitment to microelectronics sovereignty are not guaranteed on a multi-year horizon; a national contingency plan (co-funding mechanisms, alternative capital sources) would reduce single-point-of-failure risk.
6. **Leverage VIGO's existing international commercial channels** (EU market share, US subsidiary, Taiwan presence) as the export/commercialization arm for a wider ecosystem's output, rather than building parallel go-to-market infrastructure from scratch.
7. **Consider dual-use governance carefully.** Given VIGO's substantial and growing defense-sector revenue, any international R&D partnerships embedded in the ecosystem strategy should anticipate export-control review and possibly restrict some collaboration channels to security-vetted partners, particularly for infrared-detector-adjacent work.

---

## 7. Conclusion

VIGO Photonics is, on the current public record, the most substantial and most credible existing platform in Poland on which to build an advanced compound semiconductor materials and wafer ecosystem — but it is best understood as a **compound-semiconductor epitaxy, device, and photonic-integration** champion rather than a **bulk crystal-growth (boule/ingot)** specialist. Its HyperPIC project, underwritten by up to EUR 102.9 million in EU state aid within a EUR 253.4 million programme, and its role as a symbol of the "Polonisation" of the semiconductor supply chain and Polish photonics clustering, make it the natural nucleus for a national strategy — provided that strategy explicitly plans for, and separately resources, the upstream bulk-crystal-growth capability that VIGO's own technology roadmap does not currently supply. Used this way — as anchor tenant rather than sole occupant — VIGO offers Poland a genuine, already-substantially-funded head start rare among EU member states pursuing semiconductor-sector sovereignty.

---

## 8. Key References

1. VIGO Photonics — *VIGO Financial Results Summary for 2024*. https://vigophotonics.com/vigo-revenue-estimates-for-q1-2025-2/
2. VIGO Photonics — *VIGO Revenue Estimates for Q1 2025*. https://vigophotonics.com/vigo-revenue-estimates-for-q1-2025/
3. VIGO Photonics — *Polish High-Tech Conquers the USA: VIGO Photonics Announces Acquisition of InfraRed Associates Assets*. https://vigophotonics.com/polish-high-tech-conquers-the-usa-vigo-photonics-announces-acquisition-of-infrared-associates-assets/
4. VIGO Photonics — Company LinkedIn page. https://www.linkedin.com/company/vigo-photonics
5. VIGO Photonics — *About Us*. https://vigophotonics.com/about-us/
6. Wikipedia — *Vigo Photonics*. https://en.wikipedia.org/wiki/Vigo_Photonics
7. Semiconductor Review — *VIGO Photonics: Top Semiconductor Manufacturing Solutions Company (2022)*. https://www.semiconductorreview.com/vigo-photonics
8. Prospeo — *VIGO Photonics Email Format / Company Profile*. https://prospeo.io/c/vigo-photonics-email-format
9. DIGITIMES — *VIGO Photonics, Poland's IR Detector Leader, Sees Future in Photonic IC* (2023). https://www.digitimes.com/news/a20230921VL204/ic-manufacturing-photonics-poland.html
10. ICFO — *The European Commission and Chips JU Select the PIXEurope Consortium to Lead the European Pilot Line on Advanced Photonic Integrated Circuits* (2024). https://www.icfo.eu/news/2436/
11. VIGO Photonics — *Adam Piotrowski Outlines Poland's Semiconductor Future at ISS Europe 2026*. https://vigophotonics.com/adam-piotrowski-outlines-polands-semiconductor-future-at-iss-europe-2026/
12. Notes From Poland — *Polish Electronics Firm Vigo Photonics Acquires US Rival InfraRed Associates for $8.4m* (2026). https://notesfrompoland.com/2026/03/27/polish-electronics-firm-vigo-photonics-acquires-us-rival-infrared-associates-for-8-4m/
13. optics.org — *The European Commission Has Approved State Aid up to EUR 102.9 Million for the VIGO Photonics Project*. https://optics.org/press-releases/the-european-commission-has-approved-the-amount-of-state-aid-up-to-eur-102.9-million-for-the-vigo-photonics-project
14. Laser Components — *VIGO Photonics Supplier Profile*. https://www.lasercomponents.com/en/supplier/vigo-photonics/
15. ResearchGate — *Growth and Properties of MOCVD HgCdTe Epilayers on GaAs Substrates* (joint VIGO/Military University of Technology study). https://www.researchgate.net/publication/238743235
16. ResearchGate — *Molecular Beam Epitaxy Growth of HgCdTe on Large-Area Si and CdZnTe Substrates*. https://www.researchgate.net/publication/227138891
17. arXiv — *Midinfrared Semiconductor Photonics: A Roadmap*. https://arxiv.org/pdf/2511.03868
18. USPTO — *Semiconductor Devices and Manufacturing Method Using II-VI Compounds with Wide Area*. https://image-ppubs.uspto.gov/dirsearch-public/print/downloadPdf/5952703
19. arXiv — *Adsorption, Desorption, and Interdiffusion in Atomic Layer Epitaxy of CdTe and CdZnTe*. https://arxiv.org/pdf/1910.02944
20. USPTO — *Method for Epitaxial Growth of Twin-Free, (111)-Oriented II-VI Alloy Films on Silicon Substrates*. https://image-ppubs.uspto.gov/dirsearch-public/print/downloadPdf/6045614
21. ResearchGate — *Bulk Growth of CdZnTe/CdTe Crystals*. https://www.researchgate.net/publication/291838622
22. USPTO — *Method and Apparatus for Formation of HgCdTe Infrared Detection Layers Employing Isothermal Crystal Growth*. https://image-ppubs.uspto.gov/dirsearch-public/print/downloadPdf/5846319
23. USPTO — *Methods of Splitting CdZnTe Layers from CdZnTe Substrates for the Growth of HgCdTe*. https://image-ppubs.uspto.gov/dirsearch-public/print/downloadPdf/7972938

---

*Note on sourcing: this report draws on VIGO Photonics' own public communications and financial disclosures, independent business press, EU/Chips JU programme documentation, and peer-reviewed/patent literature on HgCdTe and CdZnTe crystal growth technology. Financial figures are as publicly reported as of Q1 2025; readers seeking current-quarter figures or HyperPIC construction milestones should consult VIGO's latest investor-relations releases, as the project timeline (2023–2029) is still in progress as of this report's writing (July 2026).*

---

> [!NOTE]
> 
> Generated by Claude.ai
>
> Model: Sonet 5
>
> Prompt: Write a comprehensive, technically rigorous, and economically informed report on the role of the VIGO Photonics, in the development of semiconductor bulk crystal growth and wafer technologies. The report should evaluate VIGO Photonics as a potential research, development, and industrial partner for establishing an advanced compound semiconductor crystal growth and wafer manufacturing ecosystem in Poland. Provide key references. Show the output in Markdown format.
