# Yuri N. Makarov — Scientific Biography

## Overview

Yuri N. Makarov (Юрий Николаевич Макаров, publishing as **Yu.N. Makarov**) is a Russian-American physicist and crystal-growth engineer whose career bridges Soviet-era computational fluid dynamics research on vapor-phase epitaxy reactors, the founding of one of the world's leading commercial crystal-growth modeling companies (Soft-Impact Ltd. / STR Group), and the pioneering commercialization of bulk aluminum nitride (AlN) crystal growth through Nitride Crystals, Inc. He is best known within the crystal-growth-modeling community as co-developer, together with Vladimir V. Kalaev and collaborators, of the RANS/LES turbulence and gas-flow modeling methodology that became the standard approach for simulating melt convection and global heat transport in industrial Czochralski (Cz) silicon crystal growth during the late 1990s and 2000s. He holds a Ph.D. and has an h-index in the range associated with roughly 5,000+ citations across nearly 300 publications spanning crystal growth modeling, wide-bandgap semiconductor materials (SiC, AlN, GaN), epitaxy, defect physics, and, more recently, graphene-based sensors and photoelectrochemical water splitting.

---

## 1. Early Career: Ioffe Institute and the Origins of Crystal Growth CFD (1980s)

Makarov's scientific career began at the **A.F. Ioffe Physical-Technical Institute** of the Russian Academy of Sciences in Leningrad/St. Petersburg, one of the principal centers of Soviet solid-state and semiconductor physics. Working alongside **Alexander I. Zhmakin**, Makarov undertook some of the earliest computational fluid dynamics studies applied to semiconductor vapor-phase reactor design — work that predates, and helped lay the groundwork for, the melt-convection modeling for which he later became best known.

Key early publications from this period include:

- **Zhmakin, A.I. and Makarov, Yu.N.**, "Numerical Simulation of Hyposonic Viscous Flows," *Soviet Physics – Doklady*, Vol. 30, pp. 120–123 (1985).
- **Makarov, Yu.N. and Zhmakin, A.I.**, "On Flow Regimes in VPE [Vapor-Phase Epitaxy] Reactors," *Journal of Crystal Growth*, Vol. 94, pp. 537–551 (1989).

These papers established a numerical framework — later built out with unstructured-grid finite-volume methods — for treating buoyancy-driven, low-Mach-number, high-temperature-gradient gas flows in the enclosed, heated geometries typical of both vapor-phase epitaxy reactors and, subsequently, bulk crystal-growth furnaces. This methodological foundation — treating coupled radiative heat transfer, conjugate heat transfer through solid furnace/crucible components, and complex buoyancy-driven flow in unstructured-grid CFD — became the throughline of Makarov's subsequent 40-year career.

---

## 2. Founding Soft-Impact Ltd. and STR (Semiconductor Technology Research), Inc. — the STR Group (early–mid 1990s)

In the post-Soviet transition of the early-to-mid 1990s, Makarov co-founded **Soft-Impact Ltd.** in St. Petersburg — a spin-off research and software company built around the Ioffe Institute crystal-growth-modeling group — together with colleagues including Alexander I. Zhmakin, Sergey Yu. Karpov, Mark S. Ramm, and others. Soft-Impact became the Russia-based modeling and software-development arm of what evolved into the international **STR Group** (also operating under the name **Semiconductor Technology Research, Inc.**, and later marketed simply as **STR**), with Makarov serving as company president and, in publications, frequently listed under the U.S.-registered entity "STR, Inc." alongside "Soft-Impact Ltd." as the Russian modeling affiliate.

STR Group grew into a specialized international developer of physics-based simulation software for:

- **Bulk crystal growth from the melt and solution** — Czochralski (Cz), Liquid-Encapsulated Czochralski (LEC), Directional Solidification System (DSS), Kyropoulos, and Bridgman methods, commercialized as the **CGSim** software package;
- **Bulk crystal growth from the vapor phase** — physical vapor transport (PVT/sublimation) growth of SiC, AlN, and GaN, commercialized as **Virtual Reactor (VR)**;
- **Epitaxy and deposition** — CVD of SiC, MOCVD/HVPE of III-nitrides, polysilicon deposition by the Siemens process (**PolySim**), and atomic layer deposition, commercialized variously as **CVDSim**, **STREEM**, and related tools;
- **Optoelectronic and electronic device simulation** — LED/LD structures (**SiLENSe**), current spreading and light extraction in LED chips (**SimuLED, SpeCLED, RATRO**), and HEMTs/FETs (**FETIS**).

By the 2010s–2020s, STR Group had grown to more than 40 scientists and engineers across offices in the USA, Japan, and Europe (including a modeling office in Belgrade, Serbia), serving over 200 industrial and academic customers worldwide, with local representation in China, Korea, and Taiwan. Makarov has continued to be publicly associated with STR Group as a founding figure throughout its subsequent history, even as day-to-day technical leadership of specific modeling lines passed to colleagues such as Vladimir Kalaev, Alexander Zhmakin, Sergey Karpov, and Mark Ramm.

---

## 3. Core Scientific Contribution: Turbulence and Gas-Flow Modeling of Czochralski Melt Convection (late 1990s – 2000s)

Makarov's most cited and technically influential body of work concerns the **coupled modeling of turbulent melt convection, global furnace heat transport, and gas-flow effects in industrial Czochralski silicon crystal growth**. This research, conducted principally by the Soft-Impact/STR modeling group (Makarov, Vladimir V. Kalaev, Ilya Yu. Evstratov, Alexander I. Zhmakin, and others) in close industrial collaboration with **Wacker Siltronic AG** (Erich/Evgenii Dornberger, Janis Virbulis, Wilfried von Ammon) and with turbulence specialists at **St. Petersburg Polytechnic University** (Evgenii M. Smirnov, Nikolai G. Ivanov), addressed a central industrial problem: modern 200–400 mm-diameter industrial Cz-Si melt pools operate at very high effective Reynolds numbers (~10⁵), so accurate prediction of dopant/oxygen distribution, melt–crystal interface shape, and thermal history requires a turbulence closure rather than a laminar or simple time-averaged treatment.

### 3.1 Key methodological papers

- **Evstratov, I.Yu., Kalaev, V.V., Zhmakin, A.I., Makarov, Yu.N., Abramov, A.G., Ivanov, N.G., Smirnov, E.M., Dornberger, E., Virbulis, J., Tomzig, E., von Ammon, W.**, "Modeling Analysis of Unsteady Three-Dimensional Turbulent Melt Flow during Czochralski Growth of Si Crystals," *Journal of Crystal Growth*, Vol. 230, pp. 22–29 (2001).
- **Kalaev, V.V., Evstratov, I.Yu., Makarov, Yu.N.**, "Gas Flow Effect on Global Heat Transport and Melt Convection in Czochralski Silicon Growth," *Journal of Crystal Growth*, Vol. 249, No. 1–2, pp. 87–99 (2003). — This paper is one of Makarov's most-cited works and gives the paper's name-checked contribution in the request: a systematic account of how the inert-gas (typically argon) flow field over the melt surface and through the hot zone couples back into global radiative/convective heat transport and, through it, into the turbulent melt-convection pattern, the shape of the melt–crystal interface, and oxygen transport from the crucible wall.
- **Kalaev, V.V., Lukanin, D.P., Zabelin, V.A., Makarov, Yu.N., Virbulis, J., Dornberger, E., von Ammon, W.**, "Calculation of Bulk Defects in CZ Si Growth: Impact of Melt Turbulent Fluctuations," *Journal of Crystal Growth*, Vol. 250, pp. 203–208 (2003).
- **Lukanin, D.P., Kalaev, V.V., Makarov, Yu.N., Wetzel, T., Virbulis, J., von Ammon, W.**, "Advances in the Simulation of Heat Transfer and Prediction of the Melt–Crystal Interface Shape in Silicon CZ Growth," *Journal of Crystal Growth*, Vol. 266, pp. 20–27 (2004).
- **Ivanov, N.G., Korsakov, A.B., Smirnov, E.M., Khodosevitch, K.V., Kalaev, V.V., Makarov, Yu.N., Dornberger, E., Virbulis, J., von Ammon, W.**, "Analysis of Magnetic Field Effect on 3D Melt Flow in CZ Si Growth," *Journal of Crystal Growth*, Vol. 250 (2003) — extending the RANS/LES melt-turbulence framework to include axial magnetic-field damping (MCZ growth).

### 3.2 Technical approach

The modeling methodology co-developed by Makarov and Kalaev combined:

1. A **hybrid RANS/LES (Reynolds-Averaged Navier–Stokes / Large-Eddy Simulation) turbulence closure**, using a differential turbulence model, to resolve unsteady, three-dimensional turbulent melt convection at industrially relevant Grashof/Reynolds numbers without the prohibitive cost of fully resolved DNS.
2. **Global, conjugate heat-transfer modeling** of the entire hot-zone assembly (melt, crystal, crucible, susceptor, heaters, insulation, chamber), coupling radiative exchange between semitransparent and opaque surfaces with conductive and convective transport, rather than treating the melt pool in isolation with prescribed boundary conditions.
3. Explicit **two-way coupling between the inert carrier-gas flow field and the melt/heat-transport solution** — the "gas flow effect" that gives the 2003 *J. Crystal Growth* paper its title — recognizing that argon purge-gas flow patterns over the melt free surface materially affect the global thermal field and hence the turbulent convection pattern in the melt.
4. Validation against industrial-scale experimental data (crucible/crystal rotation studies, thermocouple measurements, oxygen-concentration profiles) provided principally through the long-running collaboration with Wacker Siltronic.

This methodology, and the CGSim software platform in which it was subsequently commercialized, became a widely cited and adopted reference point for the international crystal-growth-modeling community (see, e.g., citation trails through Fraunhofer IISB, University of Latvia, IKZ Berlin, and Tohoku University groups) and is routinely cited in review articles on industrial crystal-growth simulation, including Bogdanov, Ofengeim & Zhmakin's "Industrial Challenges for Numerical Simulation of Crystal Growth" (2004).

---

## 4. Bulk Vapor-Phase Growth: SiC and Pioneering Bulk AlN (late 1990s–2010s)

In parallel with the melt-growth modeling line, Makarov led and co-authored an extensive body of work on **physical vapor transport (PVT/sublimation) growth of wide-bandgap semiconductor bulk crystals**, first for silicon carbide (SiC) and subsequently — in what became one of his signature contributions to materials science — for **bulk aluminum nitride (AlN)**.

### 4.1 SiC modeling and Virtual Reactor

Working with the Soft-Impact/STR "Virtual Reactor" team (Mark S. Ramm, Sergey Yu. Karpov, Alexander I. Zhmakin, Michael Bogdanov, and others), Makarov co-authored numerous papers on coupled heat/mass transport, thermoelastic stress, and dislocation-density evolution during sublimation growth of SiC boules, e.g.:

- **Zhmakin, I.A., Kulik, A.V., Karpov, S.Yu., Demina, S.E., Ramm, M.S., Makarov, Yu.N.**, "Evolution of Thermoelastic Strain and Dislocation Density during Sublimation Growth of Silicon Carbide," *Diamond and Related Materials*, Vol. 9, pp. 446–451 (2000).
- **Bogdanov, M.V., Galyukov, A.O., Karpov, S.Yu., Kulik, A.V., Kochuguev, S.K., Ofengeim, D.Kh., Tsyrulnikov, A.V., Zhmakin, I.A., Ramm, M.S., Zhmakin, A.I., Makarov, Yu.N.**, "Virtual Reactor: A New Tool for SiC Bulk Crystal Growth Study and Optimization," *Materials Science Forum*, Vols. 353–356, pp. 57–60 (2001).
- **Makarov, Yu.N., Litvin, D.P., Vasiliev, A., Nagalyuk, S.S. et al.**, "Sublimation Growth of 4 and 6 Inch 4H-SiC Low Defect Bulk Crystals in Ta (TaC) Crucibles," *Materials Science Forum*, Vols. 858 (2016).

### 4.2 Founding Nitride Crystals, Inc. and pioneering bulk AlN crystal growth

Makarov subsequently co-founded **Nitride Crystals, Inc.** (also referenced in earlier publications as **Nitride-Crystals Ltd.**, St. Petersburg, and later headquartered in Richmond, Virginia, USA), of which he became **President and CEO**. Nitride Crystals specialized in the sublimation-sandwich-method (SSM) growth of bulk AlN single crystals on SiC seeds — extending the SiC PVT know-how of the STR/Soft-Impact group into a new and, at the time, largely unindustrialized wide-bandgap material prized for its very high thermal conductivity, deep-UV transparency, and utility as a native substrate for AlGaN-based deep-ultraviolet optoelectronics. Representative publications from this program, several conducted jointly with **The Fox Group, Inc.** (USA) and with long-time collaborator **Evgeny N. Mokhov** (a leading figure in Russian sublimation-growth science), include:

- **Makarov, Yu.N., Avdeev, O.V., Barash, I.S., Bazarevskiy, D.S., Chemekova, T.Yu., Mokhov, E.N., Nagalyuk, S.S., Roenkov, A.D., Segal, A.S., Vodakov, Yu.A., Ramm, M.G., Davis, S., Huminic, G., Helava, H.**, "Experimental and Theoretical Analysis of Sublimation Growth of AlN Bulk Crystals," *Journal of Crystal Growth*, Vol. 310, pp. 881–886 (2008) — a joint Nitride-Crystals Ltd./The Fox Group Inc. paper widely cited as a foundational account of practical bulk-AlN sublimation growth technology.
- **Mokhov, E.N., Izmaylova, I., Kazarova, O. et al., Makarov, Yu.N.**, "Specific Features of Sublimation Growth of Bulk AlN Crystals on SiC Wafers," *physica status solidi (c)*, Vol. 10 (2013).
- **Mokhov, E.N., Wolfson, A.A., Helava, H., Makarov, Yu.N.**, "Sublimation Growth of AlN and GaN Bulk Crystals on SiC Seeds," *Materials Science Forum*, Vols. 740–742 (2013).
- **Helava, H.I., Mokhov, E.N., Avdeev, O.A., Ramm, M.G., Litvin, D.P., Vasiliev, A.V., Roenkov, A.D., Nagalyuk, S.S., Makarov, Yu.N.**, "Growth of Low-Defect SiC and AlN Crystals in Refractory Metal Crucibles," *Materials Science Forum*, Vols. 740–742, pp. 85–90 (2013).
- Book chapters: **Avdeev, O.V., Chemekova, T.Y., Helava, H., ... Segal, A.S., Zhmakin, A.I.**, "Growth of Bulk AlN Crystals" and "Manufacturing of Bulk AlN Substrates," in *Comprehensive Semiconductor Science and Technology* (2011) and *Crystal Growth Technology: Semiconductors and Dielectrics* (2010).

Nitride Crystals' 2-inch bulk AlN substrates and associated growth process modeling and characterization work (defect studies, EPR/ENDOR/ODMR spectroscopy of shallow donors and color centers in bulk AlN, conducted with the Ioffe Institute's Pavel Baranov group) place Makarov among the small number of research-industry figures credited with establishing commercially viable bulk AlN crystal growth in the 2000s–2010s, alongside groups such as Crystal IS (later Asahi Kasei) and HexaTech in the United States.

---

## 5. Diversification into GaN Epitaxy, Point-Defect Physics, and Device/Sensor Applications (2010s–2020s)

From roughly 2013 onward, Makarov's publication record — now overwhelmingly affiliated with **Nitride Crystals, Inc., Richmond, VA** — broadens substantially beyond crystal-growth process modeling into experimental materials characterization and device physics, generally in collaboration with university groups. Major threads include:

### 5.1 HVPE-grown GaN point-defect physics

An extensive, long-running collaboration with **Michael A. Reshchikov** (Virginia Commonwealth University) and colleagues used steady-state and time-resolved photoluminescence (PL), compared against SIMS, DLTS/ODLTS, and positron annihilation spectroscopy, to identify and quantify point defects in hydride vapor-phase epitaxy (HVPE)-grown GaN — material supplied by Nitride Crystals/Nitride-Crystals affiliated growers (notably Alexander S. Usikov and Heikki Helava). Representative papers:

- Reshchikov, M.A., McNamara, J.D., Zhang, F. et al., Makarov, Yu.N., "Zero-Phonon Line and Fine Structure of the Yellow Luminescence Band in GaN," *Physical Review B* (2016).
- Reshchikov, M.A., Demchenko, D.O., Usikov, A., Helava, H., Makarov, Yu.N., "Carbon Defects as Sources of the Green and Yellow Luminescence Bands in Undoped GaN," *Physical Review B* (2014).
- Reshchikov, M.A. et al., Makarov, Yu.N., "Optically Generated Giant Traps in High-Purity GaN," *Physical Review B* (2016).
- Reshchikov, M.A. et al., Makarov, Yu.N., "Unusual Properties of the RY3 Center in GaN," *Physical Review B* (2019).
- Reshchikov, M.A., Vorobiov, M., Andrieiev, O. et al., Makarov, Yu.N., "Determination of the Concentration of Impurities in GaN from Photoluminescence and Secondary-Ion Mass Spectrometry," *Scientific Reports* (2020).

### 5.2 UV LEDs and III-nitride device structures

Work on chloride-hydride vapor-phase epitaxy (CHVPE)-grown GaN/AlGaN ultraviolet LED heterostructures, in collaboration with Sergey Kurin, Sergey A. Tarasov, and colleagues, addressing efficiency, degradation mechanisms, and defect-related quantum-efficiency loss (Natalia M. Shmidt's Ioffe Institute group).

### 5.3 Graphene-on-SiC sensors and photoelectrochemical water splitting

A further diversification into **graphene-based biosensors and gas sensors** grown on SiC substrate by thermal decomposition (with A.A. Lebedev, S.P. Lebedev, V.Yu. Davydov at the Ioffe Institute), used for blood-type sensing, NO₂ gas sensing, and influenza-virus biosensing, and into **GaN-based photoelectrochemical water splitting / hydrogen generation** using HVPE-grown GaN and GaN/AlGaN p–n structures as photoelectrodes (with Alexander Usikov, Serge Luryi (Stony Brook University), and colleagues).

---

## 6. Institutional and Professional Positions (Summary)

| Period (approx.) | Affiliation | Role |
|---|---|---|
| 1980s | A.F. Ioffe Physical-Technical Institute, Russian Academy of Sciences, Leningrad/St. Petersburg | Researcher — vapor-phase-epitaxy reactor flow modeling |
| Early–mid 1990s – present | Soft-Impact Ltd. (St. Petersburg) / STR, Inc. / Semiconductor Technology Research, Inc. / **STR Group** | Co-founder; President |
| 2000s–2010s | Nitride-Crystals Ltd. (St. Petersburg, Russia) | Co-founder |
| ~2010s–present | **Nitride Crystals, Inc.** (Richmond, VA, USA) | President and CEO |

*(Institutional titles above are reconstructed from consistent publication affiliations and professional-network listings over multiple decades rather than from a single formal CV; STR Group and Nitride Crystals, Inc. continue to operate as separate but historically linked companies, both publicly identifying Makarov as a founding figure.)*

---

## 7. Bibliometric Summary

- Google Scholar profile ("Nitride Crystals Inc.") credits Makarov with roughly **1,950+ citations** under that specific listing (a partial count, as his output spans multiple institutional name variants across decades).
- His ResearchGate profile lists **298 publications**, approximately **5,300+ citations**, and roughly 58,000 "reads," with current listed research interests in heat transfer, microelectronics, semiconductor devices/electronics, GaN, crystal growth, electrical engineering, materials engineering, and solar cells.
- His publication record spans peer-reviewed venues including *Journal of Crystal Growth*, *Physical Review B*, *Scientific Reports*, *Journal of Applied Physics*, *Applied Physics Letters*, *Diamond and Related Materials*, *Materials Science Forum*, *physica status solidi*, *Semiconductors*, *Technical Physics Letters*, and *Russian Microelectronics*, as well as conference proceedings of the International Conference on Silicon Carbide and Related Materials (ICSCRM), the American Conference on Crystal Growth and Epitaxy (ACCGE), and others.

---

## 8. Significance and Legacy

Makarov's career illustrates a distinctive trajectory within post-Soviet applied physics: a foundational contribution to computational fluid dynamics for semiconductor process engineering made within a Soviet academic institute (Ioffe Institute, 1980s), followed by the transformation of that expertise into one of the first successful Russian scientific-software spin-off companies of the post-1991 era (Soft-Impact/STR Group), and culminating in direct industrial pioneering of a new bulk-crystal material (AlN) through Nitride Crystals, Inc. His core technical legacy — the RANS/LES melt-turbulence and gas-flow-coupled global heat-transport modeling methodology developed with Vladimir Kalaev, Alexander Zhmakin, and Wacker Siltronic collaborators in the late 1990s and 2000s — remains a standard reference point in the Czochralski crystal-growth-simulation literature and underlies the CGSim software still marketed and continuously developed by STR Group today. His later-career pivot into bulk AlN growth, GaN defect physics, and graphene/optoelectronic device applications reflects a broader-than-typical range for a crystal-growth modeler, combining computational, materials-growth, and device-characterization expertise across a four-decade career.

---

## Note on Sourcing

This biography was compiled from web search of publicly available bibliographic and institutional sources: STR Group's corporate website (str-soft.com), Makarov's ResearchGate and Google Scholar profiles, citation records in *Journal of Crystal Growth* and related journals, review articles on industrial crystal-growth simulation (notably Bogdanov, Ofengeim & Zhmakin, "Industrial Challenges for Numerical Simulation of Crystal Growth," *Central European Journal of Physics*, 2004), and professional-network listings (LinkedIn, RocketReach) for Nitride Crystals, Inc. No single authoritative institutional CV or "About" page specific to Makarov as an individual was located; consequently, some biographical details — particularly exact founding dates of Soft-Impact Ltd./STR and precise year-by-year institutional transitions — are reconstructed from the consistent pattern of institutional affiliations across his publication record rather than confirmed by a dated primary-source biography. This should be treated as a strong, well-evidenced reconstruction rather than a confirmed-exhaustive official biography.

---

> [!NOTE]
> 
> Generated by Claude.ai
>
> Model: Sonet 5
>
> Prompt: Create an exhaustive scientific biography for Makarov Yuri N. (co-developer of modeling methodologies for melt turbulence and gas-flow effects on Czochralski heat transport; co-founder of STR Group/Nitride Crystals). Show the output in Markdown format. Do not copy the output of the exported files into the chat.
