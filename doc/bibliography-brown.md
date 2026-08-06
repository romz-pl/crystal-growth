# Robert A. Brown — Crystal Growth Modeling and Simulation Bibliography

Robert A. Brown (PhD, University of Minnesota, 1979, advisor L. E. Scriven; faculty at MIT 1979–2005; President, Boston University, 2005–2023) is one of the founding figures of quantitative, computational modeling of melt crystal growth. His group pioneered finite-element methods for coupled fluid flow, heat transfer, and free/moving-boundary (interface) problems in Czochralski (CZ), Bridgman, float-zone, and related bulk-growth processes, and extended this into turbulence modeling, defect/point-defect dynamics, dopant segregation, and thermal-stress analysis.

This bibliography is restricted to works on the **modeling and numerical simulation** of crystal growth (continuum transport modeling, finite-element/finite-volume methods, interface tracking, defect and segregation modeling). It excludes his separate body of work on viscoelastic/non-Newtonian fluid mechanics and polymer processing except where directly tied to crystal-growth modeling methodology. Entries are sorted chronologically by publication year; within a year, alphabetically by first author surname where order is not independently known.

> **Coverage note:** This list was compiled from citation trails in review articles (notably Derby et al., *Annu. Rev. Chem. Biomol. Eng.* 2024, "Modeling the Growth of Bulk, Single Crystals") and secondary reference lists (AIChE J. 1988; SIAM J. Appl. Math papers citing Brown; Grokipedia/Wikipedia biographical summaries), rather than from a single authoritative, complete CV publication list — Brown's own posted CV (Boston University) does not include a publications section. It should be treated as a **strong partial bibliography** of his crystal-growth modeling output (concentrated in 1979–2000, when this was his primary research focus), not as guaranteed-exhaustive. Co-authors central to this body of work include L. E. Scriven, J. J. Derby, L. J. Atherton, P. A. Sackinger, P. D. Thomas, T. A. Kinney, Z. Jiang, T. Sinno, W. E. Langlois, D. E. Bornside, and others in the MIT Crystal Growth / Materials Processing Center groups.

---

## 1979

- Brown, R. A. *The Shape and Stability of Three-Dimensional Fluid Interfaces*. PhD Thesis, University of Minnesota (advisor: L. E. Scriven), 1979. — Doctoral thesis establishing the finite-element/interface-tracking methodology later applied to crystal-melt interfaces.

## 1981

- Brown, R. A. Foundational early paper(s) on finite-element analysis of free-boundary problems relevant to melt growth (cited as "R. A. Brown (1981)" in later crystal-growth reviews; exact title/journal not independently confirmed from available sources).

## 1983

- Derby, J. J.; Brown, R. A. Finite-element analysis applied to interface and thermal-capillary modeling in Czochralski-type systems (early Derby–Brown collaboration; cited in AIChE J. 1988 reference list as Derby et al. 1983).

## 1985

- Derby, J. J.; Brown, R. A.; Geyling, F. T.; Jordan, A. S.; Nikolakopoulou, G. A. "A Thermal-Capillary Model for Liquid-Encapsulated Czochralski Growth." *Journal of the Electrochemical Society*, 132, 470 (1985).

## 1986

- Derby, J. J.; Brown, R. A. "Thermal-capillary analysis of Czochralski and liquid encapsulated Czochralski crystal growth." *Journal of Crystal Growth*, 75, 227–240 (1986).

## 1987

- Derby, J. J.; Atherton, L. J.; Thomas, P. D.; Brown, R. A. "Finite-Element Methods for Analysis of the Dynamics and Control of Czochralski Crystal Growth." *Journal of Scientific Computing*, 2, 297–343 (1987).

## 1988

- Brown, R. A. "Theory of Transport Processes in Single Crystal Growth from the Melt." *AIChE Journal*, 34(6), 881–911 (1988). — Landmark review synthesizing continuum transport theory (convection, segregation, interface shape, defect formation) for CZ and vertical Bridgman–Stockbarger growth; the most widely cited entry point to Brown's crystal-growth modeling framework.
- Derby, J. J.; Brown, R. A. "On the Quasi-Steady-State Assumption in Modeling Czochralski Crystal Growth." *Journal of Crystal Growth*, 87(2), 251–260 (1988).

## 1989

- Brown, R. A.; et al. (with K. Koai and coworkers) — melt-flow/thermal-capillary modeling extensions cited alongside Derby, Atherton, and Sackinger work of this period (cited as "R.A. Brown et al. (1989)" and "K. Koai et al. (1989)" in *Transport Phenomena in Czochralski Crystal Growth Processes*, Adv. Heat Transfer).
- Sackinger, P. A.; Brown, R. A.; Derby, J. J. "A Finite Element Method for Analysis of Fluid Flow, Heat Transfer and Free Interfaces in Czochralski Crystal Growth." *International Journal for Numerical Methods in Fluids*, 9(4), 453–492 (1989). — Introduces the mixed Lagrangian finite-element / Newton-solver methodology for coupled CZ melt flow, heat transfer, and free-surface/interface shape, benchmarked for silicon and GGG.

## 1990

- Bornside, D. E.; Brown, R. A.; et al. "Finite Element/Newton Method for the Analysis of Czochralski Crystal Growth with Diffuse-Grey Radiative Heat Transfer." *International Journal for Numerical Methods in Engineering*, 30(1), 1990.

## 1993

- Kinney, T. A.; Brown, R. A. "Application of Turbulence Modeling to the Integrated Hydrodynamic Thermal-Capillary Model of Czochralski Crystal Growth of Silicon." *Journal of Crystal Growth*, 132(3–4), 551–574 (1993). — Extends the Integrated Hydrodynamic Thermal-Capillary Model (IHTCM) with a k–ε turbulence closure for large-diameter Si melt flow driven by buoyancy, crystal/crucible rotation, and Marangoni stresses.

## 1994

- Jiang, Z.; Brown, R. A. Point-defect and dopant/oxygen transport modeling in CZ silicon growth. *Chemical Engineering Science*, 49, 2991 (1994). — Continuum point-defect (vacancy/self-interstitial) transport model linked to CZ thermal history, foundational to later defect-engineering work.

## 2000

- Sinno, T.; Dornberger, E.; von Ammon, W.; Brown, R. A.; Dupret, F. "Defect Engineering of Czochralski Single-Crystal Silicon." *Materials Science and Engineering: R: Reports*, 28(5), 149–198 (2000). — Comprehensive review connecting continuum melt/heat-transfer modeling to point-defect (vacancy/interstitial) aggregation and microdefect (COP, OSF ring) formation in CZ silicon; synthesizes the MIT (Brown/Sinno) and Wacker Siltronic (von Ammon/Dornberger) modeling traditions with Dupret's Louvain approach.

---

## Related / Secondary Sources Used to Compile This Bibliography

- Derby, J. J.; et al. "Modeling the Growth of Bulk, Single Crystals: Seeing What Is Hidden." *Annual Review of Chemical and Biomolecular Engineering*, 2024/2025 — cites and contextualizes multiple Brown papers above.
- "Theory of Transport Processes in Single Crystal Growth from the Melt," *AIChE J.* 34, 881 (1988) — its own reference list independently corroborates several entries above (Derby et al. 1985, 1987, 1988).
- *Transport Phenomena in Czochralski Crystal Growth Processes*, in *Advances in Heat Transfer* — reference list corroborates Brown 1981 and Brown et al. 1989 citations.
- Grokipedia and Wikipedia biographical entries on Robert A. Brown (used for career/context verification only, not as primary citation sources).
- MIT DSpace thesis record (dspace.mit.edu/handle/1721.1/9113) — a Brown-supervised MIT PhD thesis on microdefect formation linkage in CZ silicon and vertical Bridgman BGO growth (student thesis, listed for context; not itself authored by Brown).

**Caveat repeated for clarity:** Robert A. Brown authored or co-authored substantially more crystal-growth modeling papers than listed here — particularly numerous MIT PhD theses he supervised (by Derby, Atherton, Sackinger, Kinney, Jiang, Sinno, Bornside, W. Winegard, and others) that are the primary repository of the detailed numerical methodology. A fully exhaustive listing would require direct access to a Web of Science/Scopus author-disambiguated query for "Brown RA" affiliated with MIT Chemical Engineering, 1979–2005, which was not accessible from this environment.

---

> [!NOTE]
> 
> Generated by Claude.ai
>
> Model: Sonet 5
>
> Prompt: Create an exhaustive bibliography describing the modeling of crystal growth. Focus on bibliographies related to the Robert A. Brown (MIT/Boston University). Include only bibliographies for modeling and simulation work. Show the output in Markdown format. Sort the bibliography chronologically. Do not copy the output of the exported files into the chat.
