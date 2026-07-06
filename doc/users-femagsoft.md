# Organizations Known to Have Applied or Used FEMAG / FEMAG-CZ (FEMAGSoft S.A., Belgium) for Crystal Growth Modeling

This list compiles organizations that are documented — via peer-reviewed articles, patents, conference proceedings, or FEMAGSoft's own publication record — as having applied, used, co-developed, or explicitly cited the FEMAG family of software (FEMAG/CZ, FEMAG/CZ/OX, FEMAG/FZ, FEMAG/DS, FEMAG/VB, FEMAG/HEM, FEMAG/PVT) for crystal-growth process modeling. Entries are sorted chronologically by the earliest documented instance of use/citation found for each organization. Only independently verifiable sources are included; the FEMAGSoft customer list itself is login-gated and not publicly accessible, so it was not used as a source.

---

## Chronological List

### 1. Université catholique de Louvain (UCL) / CESAME Research Center — Belgium (University lab)
**First documented use:** 1986 (origin of the code)
FEMAG originated as academic research code developed by François Dupret and colleagues at UCL's CESAME research center beginning in the mid-1980s, predating the 2003 spin-off of FEMAGSoft/FEMAG S.A. UCL remains a continuous co-developer and co-publisher of FEMAG-related research through the company's history.
- Dupret, Ryckmans, Wouters, Crochet, *"Numerical calculation of the global heat transfer in a Czochralski furnace,"* J. Crystal Growth, 79 (1986) 84–91.
- Van den Bogaert & Dupret, *"Dynamic Global Simulation of the Czochralski Process,"* J. Crystal Growth, 171 (1997).
- de Potter et al., *"Numerical Simulation of Bulk Crystal Growth for Industrial Applications,"* joint UCL/FEMAGSoft affiliation (undated proceedings paper).

### 2. Shin-Etsu Handotai Co., Ltd. — Japan (Commercial company)
**First documented use:** ~1999–2003 (patent filings)
Multiple US patents assigned to Shin-Etsu Handotai describe using "global heat transfer analysis software called FEMAG" (citing the 1990 Dupret et al. paper) to design silicon CZ furnace hot zones, calculate V/G ratios, and predict defect-free growth windows.
- US6893499 — *Silicon single crystal wafer and method for manufacturing the same*
- US6902618 / US20030172865 — *Silicon single crystal wafer having void denuded zone... diameter above 300 mm*
- US7214268 — *Method of producing P-doped silicon single crystal*
- US6632280 — *Apparatus for growing single crystal, method for producing single crystal*
- US6190452 — *Silicon single crystal wafer and method for producing it*
- US20150240380 — *Method for growing silicon single crystal*

### 3. Komatsu Electronic Metals Co., Ltd. (later Sumitomo Sitix / SUMCO) — Japan (Commercial company)
**First documented use:** ~2000
Journal article on scaling silicon crystal growth to 400 mm diameter describes FEMAG (developed by Dupret et al.) as the primary tool for global heat transfer analysis, coupled with the STREAM CFD code for melt/gas flow.
- *"Numerical simulation for silicon crystal growth of up to 400 mm diameter in Czochralski furnaces,"* Journal of Crystal Growth, 2000.

### 4. Leibniz-Institut für Kristallzüchtung (IKZ Berlin) — Germany (National/institute lab)
**First documented use:** ~2010–2011
IKZ Berlin researchers used FEMAG-FZ for axisymmetric thermal-field calculations in floating-zone germanium crystal growth, validating simulation results against lateral photo-voltage scanning measurements.
- Wünscher et al., *"Crucible-free Pulling of Germanium Crystals,"* (Journal of Crystal Growth companion paper, DOI:10.1016/j.jcrysgro.2010.10.200), arXiv:1103.0627.
- IKZ Berlin is also a long-standing contributor to crystal-growth simulation benchmarking (e.g., Dadzis et al., *"Validation, verification, and benchmarking of crystal growth simulations,"* J. Crystal Growth, 2017), situating it within the same comparative-code community that references FEMAG-CZ, FEMAG-FZ, CGSim, and CrysMAS.

### 5. Bruker Advanced Supercon (Bruker ASC) — Germany (Commercial company)
**First documented use:** 2010
Co-authored publication with FEMAGSoft (A. de Potter of FEMAG S.A. and B. Fischer of Bruker ASC) on applying strong magnetic fields (implying Bruker's superconducting magnet systems, modeled via FEMAG) to improve silicon PV ingot growth.
- de Potter & Fischer, *"Improvements of Si-Crystal Growing Processes for PV Applying Strong Magnetic Fields,"* InterPV, May 2010, pp. 82–85.

### 6. Unnamed/aggregate Chinese CZ-Si manufacturers and research groups (Commercial/academic, China)
**First documented use:** 2011
A journal article (Chinese semiconductor research context) reports use of "finite element analysis software femag-CZ" to study the effect of CUSP magnetic field configurations on oxygen concentration distribution during CZ-Si growth — indicating adoption of FEMAG-CZ within Chinese silicon-growth process R&D groups.
- *"Numerical simulation of CUSP magnetic field on oxygen concentration distribution in CZ-Si crystal growth,"* 2011.

### 7. FEMAGSoft S.A. / FEMAG S.A. — Belgium (Commercial company, developer/vendor)
**Ongoing, 2003–present**
As the software's developer and vendor (spun off from UCL in 2003), FEMAGSoft/FEMAG S.A. itself is the continuous author of record on essentially all FEMAG methodology papers, technical notes, and conference proceedings (ICCG, ECCOMAS, IFAC, Riga-Pamir MHD conferences, Modeling in Crystal Growth workshops, etc.) from 2003 onward, in most cases jointly with UCL. Representative works include the 2009 Shanghai ISTC/CSTIC proceedings paper and the 2012 *Journal of Crystal Growth* paper on transverse magnetic field simulation.

---

## Organizations Referenced as Comparator/Peer Codes Alongside FEMAG-CZ (Not Confirmed FEMAG Users)

The following organizations were identified in the search process as developers or users of **competing** crystal-growth simulation codes (CGSim, CrysMAS/STHAMAS, Virtual Reactor) that are frequently benchmarked or discussed *alongside* FEMAG-CZ in the literature, but no direct evidence of them using FEMAG-CZ itself was found. They are excluded from the main list but noted here for completeness and to avoid false attribution:
- **STR Group Ltd.** (Russia) — developer of CGSim / Virtual Reactor.
- **Fraunhofer Institute for Integrated Systems and Device Technology (Fraunhofer IISB)** — developer of CrysMAS/STHAMAS.

---

## Methodology and Limitations

- Sources used: FEMAGSoft S.A.'s own publications page (femagsoft.com), peer-reviewed journal articles (Journal of Crystal Growth, ScienceDirect, ResearchGate), issued US patents (via USPTO/Google Patents full text explicitly naming "FEMAG" as the simulation tool used), and arXiv preprints.
- FEMAGSoft's "Customers" page is access-restricted (login required) and could not be used as a source; consequently, this list reflects only organizations independently documented in the public literature as having applied FEMAG/FEMAG-CZ, and should **not** be considered a complete roster of FEMAGSoft's commercial licensees. Many licensed industrial users (e.g., large-scale silicon or sapphire producers) may not publish their internal simulation tool usage and are therefore not captured here.
- No independent, publicly documented instance of a university lab (other than UCL, the code's originating institution) or a national laboratory using FEMAG/FEMAG-CZ specifically (as opposed to competing codes such as CGSim or CrysMAS) was found in the available search results.
- Given the paywalled/restricted nature of many crystal-growth engineering publications and patents, this list should be treated as a well-sourced but non-exhaustive starting point rather than a definitive census.

---

> [!NOTE]
> 
> Generated by Claude.ai
>
> Model: Sonet 4.6
>
> Prompt: Create an exhaustive list of comertial companies, university labs, national labs, and other commertial and non-comertial organizations that applied or used the FEMAG / FEMAG-CZ programs from FEMAGSoft S.A. (Belgium) for modeling and simulating crystal growth. Show the output in Markdown format and sort the articles chronologically. Do not copy the output of the exported files into the chat.
