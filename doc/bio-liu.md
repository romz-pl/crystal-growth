# Scientific Biography: Xuan Liu (Xin Liu, 劉欣)

**Field:** Numerical / global modeling of melt and solution crystal growth
**ORCID:** [0000-0003-0832-327X](https://orcid.org/0000-0003-0832-327X)

> **Note on sourcing.** This biography is compiled entirely from openly indexed publication records, journal author-affiliation metadata, and special-issue editorial listings. It is **not** based on a personal CV, institutional faculty page, or direct confirmation from the subject. Two things follow from that:
> 1. Publications in this field are consistently authored as **"Xin Liu"**; I found no indexed output under "Xuan Liu." The two are almost certainly the same person under different romanizations of 劉欣/劉軒-type given names, but I could not independently verify which is authoritative — flagged wherever it matters.
> 2. I was able to independently verify the **Kyushu University (RIAM, Kakimoto group)** and **Nagoya University (IMaSS, Ujihara group)** affiliations from multiple publication and editorial records. I could **not** independently verify the **Institute for Materials Research (IMR), Tohoku University** affiliation from public search — it appears nowhere in the records I retrieved. It is included below only because you stated it, and is marked accordingly. If you have a source for it (a paper, CV, or lab page), send it and I'll fold it in with proper dating.

---

## 1. Overview

Xin Liu is a researcher working in computational/numerical materials science, specializing in **global (furnace-scale) modeling of crystal growth from the melt and from solution**. His work sits at the interface of computational fluid dynamics, heat and mass transfer, and materials processing, applied principally to two industrially important crystal systems: **silicon (Si)**, grown by Czochralski (CZ), directional solidification, and floating-zone (FZ) methods, and **silicon carbide (SiC)**, grown by top-seeded solution growth (TSSG). His research is consistently characterized by coupling continuum-scale global furnace models (heat transfer, melt/solution convection, magnetic-field effects, dopant/impurity transport) with defect- and interface-level phenomena (dislocation generation, step bunching, solvent inclusion, solute evaporation), and, in his more recent work, by the integration of machine learning and data-driven methods into crystal growth process design.

## 2. Institutional Trajectory

Based on the traceable literature, Liu's career has moved through (at least) three institutional settings:

### 2.1 Research Institute for Applied Mechanics (RIAM), Kyushu University — with Koichi Kakimoto
This is the earliest and most extensively documented phase of his published work, spanning roughly **2009–2020**. He was part of the RIAM Crystal Growth Dynamics group under **Prof. Koichi Kakimoto**, a leading figure in global modeling of bulk crystal growth (recipient of the 2025 IOCG Frank Prize for contributions to numerical modeling in crystal growth). During this period, Liu contributed to:
- Global heat-transfer simulators for Czochralski and directional-solidification growth of silicon for photovoltaic (solar cell) applications.
- Studies of thermal-stress-induced dislocation distributions in directionally solidified silicon.
- Numerical investigation of carbon contamination during the CZ silicon melting process.
- A transient global model for magnetic-field-applied CZ silicon growth (published in *Journal of Crystal Growth*, 2020), coupling solid conduction, melt convection, and applied magnetic fields.
- Coupled 2D/3D global modeling of cusp-shaped magnetic field effects on heat, mass, and oxygen transfer in CZ growth.
- Dopant concentration modeling in floating-zone silicon growth, including natural convection, thermocapillary convection, electromagnetic force, and melt rotation effects.

Frequent co-authors in this period include Lijun Liu, Bing Gao, Satoshi Nakano, Zaoyang Li, Hiroaki Miyazawa, Hirofumi Harada, and X.F. Han — consistent with sustained membership in the Kakimoto RIAM group.

### 2.2 Institute for Materials Research (IMR), Tohoku University *(as stated by user — unverified in independently retrieved sources)*
You've indicated an intermediate or associated affiliation at IMR, Tohoku University. Tohoku IMR does host a crystal-growth-focused research division (結晶材料化学研究部門, Division of Crystal Chemistry) working on melt-based single-crystal growth and interfacial dynamics under applied electric, magnetic, and stress fields — a natural thematic fit with Liu's modeling expertise. However, no publication, editorial listing, or directory record surfaced in my searches ties Liu directly to IMR. This may reflect a short-term visiting position, a gap in open indexing, or a difference in how his name was recorded during that period. **This entry should be treated as unconfirmed pending a primary source.**

### 2.3 Institute of Materials and Systems for Sustainability (IMaSS), Nagoya University — with Toru Ujihara's group
The most recent and currently active phase (**circa 2021–present**), based in the Department of Materials Process Engineering (Graduate School of Engineering) and IMaSS at Nagoya University, under **Prof. Toru Ujihara**. This phase marks a shift in application system — from melt growth of silicon toward **solution growth of silicon carbide (4H-SiC)** via the top-seeded solution growth (TSSG) method — while retaining the same core methodological identity as a global/numerical modeler. Representative contributions include:
- Numerical investigation of solute (aluminum) evaporation during SiC TSSG growth, with a redesigned furnace structure to suppress evaporative solute loss (*Journal of Crystal Growth*, 2021).
- Data-driven optimization and experimental validation of lab-scale mono-like silicon ingot growth by directional solidification (*ACS Omega*, 2022) — explicitly combining numerical modeling with data-driven/machine-learning optimization.
- A transfer-learning-based method for predicting unsteady crystal growth behavior (*Advanced Theory and Simulations*, 2022).
- Modeling-based design of control patterns for uniform macrostep morphology in SiC solution growth (*Crystal Growth & Design*, 2023).
- A review of solution growth techniques for 4H-SiC single crystals, with emphasis on quasi-steady global modeling as a near-standard tool in the field (*Crystal Growth & Design*, 2023).
- Continued first- and co-authored contributions on solvent design, step-bunching suppression, and solution-flow control in SiC TSSG growth through 2023–2025.

He is listed with an ORCID-linked affiliation at IMaSS, Nagoya University, and appears as **Dr. Xin Liu**, guest co-editor (alongside Xuefeng Han and Andrejs Sabanskis) of the *Crystals* (MDPI) special issue **"Heat and Mass Transfer Modeling in Crystal Growth"** (submissions closed August 2023), where his listed research interests are: *multi-scale modeling on crystal growth, solidification process, materials informatics, silicon, machine learning, process optimization.*

## 3. Research Themes

Across all three institutional phases, several consistent methodological and topical threads run through Liu's body of work:

1. **Global (furnace-scale) modeling** — coupled treatment of conductive, convective, and radiative heat transfer across the entire growth furnace, rather than isolated melt/solution sub-domains, following the RIAM/Kakimoto tradition of "global modeling in crystal growth."
2. **Melt-crystal and solution-crystal interface dynamics** — dynamic phase-interface modeling, step bunching, macrostep morphology, and cellular structure formation in solution growth.
3. **Defect and impurity control** — dislocation generation from thermal stress, carbon contamination, oxygen transport, dopant/resistivity distribution, and solvent inclusion/evaporation.
4. **Magnetic-field-assisted growth** — cusp and horizontal magnetic field effects on melt convection and dopant transport in CZ silicon.
5. **Emerging data-driven methods** — transfer learning and data-driven optimization applied to crystal growth process design, marking a methodological expansion in the more recent (Nagoya) phase of his work.

## 4. Selected Publications (Representative, Not Exhaustive)

*Chronological, drawn from indexed literature under "Xin Liu" in this research area.*

- Liu, L.; Miyazawa, H.; Nakano, S.; **Liu, X.**; Li, Z.; Kakimoto, K. "Modeling and simulation of Si crystal growth from melt." *Physica Status Solidi (C)*, 6(3), 645–652 (2009).
- Liu, L.; **Liu, X.**; Li, Z.; Kakimoto, K. "Computer modeling of crystal growth of silicon for solar cells." *Frontiers in Energy*, 5(3), 305–312 (2011).
- **Liu, X.**; Gao, B.; Nakano, S.; Kakimoto, K. "Thermal stress induced dislocation distribution in directional solidification of Si for PV application." *Journal of Crystal Growth* (2014).
- **Liu, X.**; Gao, B.; et al. "Numerical investigation of carbon contamination during the melting process of Czochralski silicon crystal growth." *Journal of Crystal Growth* (2014).
- Han, X.F.; **Liu, X.**; et al.; Kakimoto, K. "Dopant concentration calculation in 200 mm floating-zone silicon." *Journal of Crystal Growth*, 545 (2020).
- **Liu, X.**; Harada, H.; et al.; Kakimoto, K. "A transient global model for magnetic-field-applied Czochralski silicon growth." *Journal of Crystal Growth*, 532 (2020).
- Kakimoto, K.; **Liu, X.**; Nakano, S. "Analysis of the effect of cusp-shaped magnetic fields on heat, mass, and oxygen transfer using a coupled 2D/3D global model." *Crystal Research and Technology*, 57(1) (2022).
- Dang, Y.; Zhu, C.; **Liu, X.**; Yu, W.; Liu, Xinbo; Suzuki, K.; Furusho, T.; Harada, S.; Tagawa, M.; Ujihara, T. "Numerical investigation of solute evaporation in crystal growth from solution: a case study of SiC growth by TSSG method." *Journal of Crystal Growth* (2021).
- **Liu, X.**; Dang, Y.; Tanaka, H.; Fukuda, Y.; Kutsukake, K.; Kojima, T.; Ujihara, T.; Usami, N. "Data-Driven Optimization and Experimental Validation for the Lab-Scale Mono-Like Silicon Ingot Growth by Directional Solidification." *ACS Omega*, 7(8), 6665–6673 (2022).
- Dang, Y.; Kutsukake, K.; **Liu, X.**; Inoue, Y.; Liu, Xinbo; Seki, S.; Zhu, C.; Harada, S.; Tagawa, M.; Ujihara, T. "A Transfer Learning-Based Method for Facilitating the Prediction of Unsteady Crystal Growth." *Advanced Theory and Simulations*, 5(9) (2022).
- Dang, Y.; Liu, Xinbo; Zhu, C.; Fukami, Y.; Ma, S.; Zhou, H.; **Liu, X.**; Kutsukake, K.; Harada, S.; Ujihara, T. "Modeling-Based Design of the Control Pattern for Uniform Macrostep Morphology in Solution Growth of SiC." *Crystal Growth & Design*, 23(2), 1023–1032 (2023).
- **Liu, X.**; Guan, Z.; Furusho, T.; Ujihara, T. "Review of solution growth techniques for 4H-SiC single crystal." (Review article; *Crystal Growth & Design* / related venue, 2023).

*(Author-order and precise venue for the review article should be verified against the publisher's page before citation; retrieved via secondary aggregator record.)*

## 5. Editorial and Community Roles

- **Guest Editor**, *Crystals* (MDPI) Special Issue: **"Heat and Mass Transfer Modeling in Crystal Growth"** (with Dr. Xuefeng Han, Zhejiang University, and Dr. Andrejs Sabanskis, University of Latvia), submission deadline 30 August 2023 — thematically a direct continuation of the "Global Modeling in Crystal Growth" special issue tradition established by Koichi Kakimoto in the same journal (2016).

## 6. Collaborator Network (Summary)

| Institution / Period | Key Collaborators |
|---|---|
| RIAM, Kyushu University | Koichi Kakimoto, Lijun Liu, Bing Gao, Satoshi Nakano, Zaoyang Li, Hiroaki Miyazawa, Hirofumi Harada, X.F. Han |
| IMaSS, Nagoya University | Toru Ujihara, Shunta Harada, Miho Tagawa, Kentaro Kutsukake, Yifan Dang, Xinbo Liu, Can Zhu, Wancheng Yu, Tomoaki Furusho, Noritaka Usami |

## 7. Open Questions for Verification

To make this record complete and fully citable, the following should be confirmed against primary sources:
- Exact **dates** of any Tohoku University IMR affiliation, and its position in the timeline relative to Kyushu and Nagoya.
- Whether "Xuan Liu" and "Xin Liu" are confirmed by the subject to be the same romanization of one name, or represent two related-but-distinct name forms (e.g., a name change, or a given-name/pen-name distinction).
- PhD-granting institution and year (the Kyushu/RIAM publication record from 2009 onward is consistent with, but does not itself confirm, a Kyushu University doctorate under Kakimoto).
- Current job title and start date at Nagoya University.

---
*Compiled from openly accessible publication metadata, journal author-affiliation listings, and MDPI/ACS editorial pages as of August 2026. Not a substitute for a CV-verified biography.*

---

> [!NOTE]
> 
> Generated by Claude.ai
>
> Model: Sonet 5
>
> Prompt: Create an exhaustive scientific biography for Liu Xuan (Tohoku University). Show the output in Markdown format. Do not copy the output of the exported files into the chat.
