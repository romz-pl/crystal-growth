# Scientific Biography: Nikolay Georgievich Ivanov

## Overview

Nikolay Georgievich Ivanov (Николай Георгиевич Иванов) is a Russian computational fluid dynamicist affiliated with Peter the Great St. Petersburg Polytechnic University (SPbPU — formerly St. Petersburg State Polytechnic University / Leningrad Polytechnic Institute). He holds the academic rank of *dotsent* (associate professor) and the degree of Candidate of Physical and Mathematical Sciences (Russia's Ph.D.-equivalent degree). Over a career spanning more than two decades, Ivanov has built a body of work centered on high-fidelity numerical simulation of turbulent and buoyancy-driven flows, spanning two outwardly distinct but methodologically unified application domains: (1) melt convection and heat transfer in industrial Czochralski crystal growth of silicon, and (2) cabin ventilation, contaminant transport, and life-support airflow modeling for crewed spacecraft, most notably the International Space Station (ISS). In the 2020s his research has extended into indoor/room ventilation flows, self-oscillating turbulent jets, and — prompted by the COVID-19 pandemic — the fluid dynamics of violent expiratory events (coughs) and aerosol dispersion.

## Institutional Affiliation

- **Institution:** Peter the Great St. Petersburg Polytechnic University (SPbPU), St. Petersburg, Russia.
- **Contact address on record:** 195251, Saint Petersburg, Polytechnicheskaya str., 29, Academic Building No. 1.
- Ivanov's affiliation is consistently listed across his publication record simply as St. Petersburg (State) Polytechnic University / Peter the Great St. Petersburg Polytechnic University, reflecting the institution's renaming (it adopted the "Peter the Great" designation in 2015).
- He is closely and durably associated with the university's fluid dynamics / aerohydrodynamics research group historically led by **Professor Evgueni M. Smirnov**, alongside long-term collaborators **Marina A. Zasimova**, **Denis S. Telnov**, **Vladimir V. Ris**, and **Alexander Levchenya**.

## Academic Credentials

- **Ph.D. in Physical and Mathematical Sciences** (Candidate of Physical and Mathematical Sciences, the standard Russian research doctorate at this career stage).
- **Academic title:** dotsent (доцент), the Russian rank roughly equivalent to associate professor.

No public, structured curriculum vitae with exact dates of degree conferral was located; the university's own personnel page (english.spbstu.ru) lists only the degree and title without dates. This biography is therefore built primarily from Ivanov's documented publication record and institutional listing rather than a dated academic CV.

## Researcher Identifiers

| Identifier | Value |
|---|---|
| Scopus Author ID | 36918442900 |
| ORCID | 0000-0001-9897-5401 |
| eLibrary (RSCI) SPIN | 9977-5244 |
| eLibrary (RSCI) Author ID | 13898 |
| ResearcherID (Publons/Clarivate) | A-8479-2014 |
| Google Scholar ID | ug4-VXsAAAAJ |

Google Scholar records approximately 822 citations to Ivanov's work at the time of consultation, under the listed research interests of Computational Fluid Dynamics, Heat Transfer, Buoyancy-Induced Flows, and Environmental Control and Life Support Systems.

## Research Program

Ivanov's research divides into several interlocking thematic strands, all unified by a methodological commitment to high-resolution, 3D, time-dependent (unsteady) numerical simulation of turbulent flow using both Reynolds-Averaged Navier–Stokes (RANS) and Large Eddy Simulation (LES) approaches, cross-validated wherever possible against experimental or in-flight measurement data.

### 1. Czochralski Crystal Growth: Melt Convection and Magnetic Field Control

Ivanov's earliest and most heavily cited line of work (concentrated in the late 1990s through mid-2000s) addressed the numerical modeling of turbulent melt convection in industrial-scale Czochralski (CZ) growth of single-crystal silicon — work carried out in close collaboration with the STR Group/Ioffe Institute crystal-growth simulation community (V.V. Kalaev, A.I. Zhmakin, Yu.N. Makarov) and with Wacker Siltronic researchers (E. Dornberger, J. Virbulis, E. Tomzig, W. von Ammon).

Key contributions in this area:
- Development and application of a hybrid RANS/LES turbulence model, based on a differential turbulence closure, to simulate 3D unsteady turbulent melt convection in an industrial CZ silicon crystal-growth system.
- Systematic analysis of the effect of applied direct-current magnetic fields (axial/vertical, transverse/horizontal, and cusp configurations) of varying strength and geometry on 3D melt flow, temperature distribution, and melt–crystal interface behavior in 300–400 mm diameter silicon melts, with results validated directly against experimentally measured temperature fields.
- Contribution to multi-author, cross-institutional benchmark studies (with I.Yu. Evstratov, V.V. Kalaev, A.I. Zhmakin, Yu.N. Makarov, A.G. Abramov, A.B. Korsakov, E.M. Smirnov, and the Wacker Siltronic group) modeling unsteady 3D turbulent melt flow during CZ growth of silicon crystals, and its consequences for oxygen transport, dopant distribution, and thermal fluctuations at the growth interface — work published in the *Journal of Crystal Growth* and *Microelectronic Engineering*.
- This body of work is part of the broader "industrial challenges for numerical simulation of crystal growth" literature that matured the use of coupled global heat-transfer/melt-convection modeling as a predictive design tool for large-diameter semiconductor-grade silicon boules.

Representative publication: **N.G. Ivanov, A.B. Korsakov, E.M. Smirnov, K.V. Khodosevitch, V.V. Kalaev, Yu.N. Makarov, E. Dornberger, J. Virbulis, W. von Ammon**, "Analysis of magnetic field effect on 3D melt flow in CZ Si growth," *Journal of Crystal Growth*, 2003, Vol. 250, pp. 183–188.

### 2. Spacecraft Cabin Ventilation and Life-Support CFD (International Space Station)

From the mid-2000s onward, Ivanov became a central contributor — alongside E.M. Smirnov, D.S. Telnov, and Chang H. Son (The Boeing Company) — to a long-running program of CFD analysis supporting the design and operational assessment of ventilation and Environmental Control and Life Support Systems (ECLSS) aboard the International Space Station.

This work systematically applied RANS (primarily via ANSYS FLUENT, using the high-Reynolds-number k–ε model) and LES (Smagorinsky–Lilly subgrid model) to:
- Predict airflow velocity fields and spatial/temporal carbon dioxide concentration distributions within pressurized ISS modules, identifying potential stagnant zones that could pose a risk to crew health and comfort.
- Model integrated, multi-module ISS configurations, including the full Assembly-Complete twelve-module on-orbit configuration, and visiting-vehicle (Space Shuttle and other spacecraft) ventilation interactions.
- Assess specific habitability configurations, including the Crew Alternative Sleeping Area (CASA) in the Columbus module and Crew Quarters (CQ) installations in Node 2, evaluating whether new hardware or stowage protruding into ECLSS keep-out zones compromised airflow adequacy.
- Cross-validate RANS and LES predictions against each other and against on-orbit/test measurement data for the Columbus module, establishing a practical evaluation procedure for inferring time-averaged velocity-magnitude fields from RANS mean-velocity and turbulent-kinetic-energy data.
- Model water droplet transport for ISS crew hygiene-activity applications (e.g., a 2013 AIAA technical paper).

Representative publications:
- **E.M. Smirnov, N.G. Ivanov, D.S. Telnov, Ch.H. Son**, "CFD modeling of cabin air ventilation in the International Space Station: a comparison of RANS and LES data with test measurements for the Columbus Module," *International Journal of Ventilation*, 2006, Vol. 5, No. 2, pp. 219–228.
- **E.H. Turner, C.H. Son, E.M. Smirnov, N.G. Ivanov, D.S. Telnov**, "Air circulation and carbon dioxide concentration study of International Space Station Node 2 with attached modules," *SAE Transactions*, 2004, Vol. 113, pp. 1150–1154.
- **E.M. Smirnov, N.G. Ivanov, D.S. Telnov**, "Integrated Computational Fluid Dynamics Ventilation Model for the International Space Station," SAE Technical Paper 2005-01-2794, 2005.
- **C.H. Son, E.M. Smirnov, N.G. Ivanov, D.S. Telnov**, "CFD study of ventilation and carbon dioxide transport for ISS Node 2 and attached modules," *SAE International Journal of Aerospace*, 2009, Vol. 4, pp. 519–524.
- **C.H. Son, E.M. Smirnov, N.G. Ivanov, D.S. Telnov**, "CFD modeling of International Space Station and visiting spacecraft ventilation: evaluation of design solutions for complex on-orbit operations," 12th International Conference on Air Distribution in Rooms (Roomvent 2011), 2011.
- **C.H. Son, N.G. Ivanov, D.S. Telnov, E.M. Smirnov**, "CFD Modeling of Water Droplet Transport for ISS Hygiene Activity Application," AIAA Technical Paper 2013-3456, 2013.
- **C.H. Son, N.G. Ivanov, E.M. Smirnov**, "CFD Study of Ventilation on Board the International Space Station," presented at the 4th IAA Symposium "Space Flight Safety," St. Petersburg, 3–5 July 2017.

Notably, this ISS ventilation research constitutes one of the more extended and productive academic–industry collaborations in the field, sustained for well over a decade between the SPbPU group and Boeing's Houston-based human-spaceflight engineering staff, and represents rare open Western-facing publication of Russian-side ISS environmental-control CFD analysis.

### 3. Subsea and Industrial Heat Exchanger Flows

Ivanov has also contributed to CFD analysis of industrial heat-transfer equipment, including numerical simulation of the effect of complex 3D flow on heat transfer from a tube bank in a subsea cooler.

Representative publication: **N.G. Ivanov, V.V. Ris, E.M. Smirnov, N.A. Tschur**, "Numerical simulation of 3D flow effect on heat transfer from a tube bank of subsea cooler," Proceedings of the 15th International Heat Transfer Conference (IHTC-15), August 10–15, 2014, Kyoto, Japan, Paper IHTC15-9766, Begell House Inc.

### 4. Room and Indoor Ventilation Flows (Turbulent Jets, LES)

In the 2020s, in collaboration with **Marina A. Zasimova** and international partners (e.g., D. Markov, Technical University of Sofia), Ivanov produced a series of studies applying vortex-resolving, wall-modeled LES to canonical indoor-ventilation test-room configurations — extending the CZ-growth- and ISS-derived turbulence-modeling expertise to the built-environment/HVAC domain.

Representative publications:
- **M.A. Zasimova, N.G. Ivanov, D. Markov**, "Numerical modeling of air distribution in a test room with 2D sidewall jet. II. LES-computations for the room with finite width," (also published in Russian as "Численное моделирование циркуляции воздуха в помещении при подаче из плоской щели. II. LES-расчеты для помещения конечной ширины"), *St. Petersburg Polytechnic University Journal: Physics and Mathematics* / associated Russian-language venue, ca. 2020–2021. The study used a 48-million-cell ANSYS Fluent mesh to reproduce the classical Nielsen et al. (1978, 1990) sidewall-slot-jet test-room experiments, examining near-wall jet behavior under two supply-slit-width configurations.
- **M.A. Zasimova, A.D. Krasikova, N.G. Ivanov**, "Control of self-oscillations of a round turbulent jet propagating in a narrow rectangular cavity," *Thermophysics and Aeromechanics*, 2024, Vol. 31, No. 4, pp. 791–804.
- **M.A. Zasimova, N.G. Ivanov, E.D. Stepasheva**, parametric numerical study of turbulent jet propagation from a slot into a confined space at Reynolds number 4×10³, comparing 2D and 3D unsteady RANS calculations against the confined-jet self-oscillation experiments of Mataoui et al. (2001); the study characterizes the ranges of open-boundary area and cavity height for which self-oscillation (flapping) modes occur, and quantifies discrepancies (~10%) between 2D and 3D Strouhal-number predictions.

### 5. Violent Expiratory Events and Respiratory Aerosol Dispersion (COVID-19-era research)

Reflecting the redirection of much of the international fluid dynamics community toward respiratory-flow and airborne-disease-transmission questions during the COVID-19 pandemic, Ivanov (with M.A. Zasimova and V.V. Ris) joined an international, multi-institutional benchmarking collaboration assessing the ability of different CFD codes and turbulence models to reproduce the short-duration, high-inertia flow of a prototypical cough and the resulting short-range dispersion of an aerosol droplet cloud.

- **J. Pallarès, A. Fabregat, A. Lavrinenko, H.A.b. Norshamsudin, G. Janiga, D.F. Fletcher, K. Inthavong, M. Zasimova, V. Ris, N. Ivanov**, et al., "Numerical simulations of the flow and aerosol dispersion in a violent expiratory event: Outcomes of the '2022 International CFD Challenge on violent expiratory events'," *Physics of Fluids*, 2023, Vol. 35, No. 4, Article 045106. This large international consortium (organized by Universitat Rovira i Virgili, Spain, and the University of Udine, Italy) compared multiple independent CFD codes and turbulence-model choices against DNS reference data for a 0.4-second mild-cough-like expiratory event.
- **M.A. Zasimova, N.G. Ivanov, V.V. Ris**, "URANS and LES simulation of the initial stage of propagation of a droplet-containing air jet characteristic of acute respiratory phenomena," Proceedings of the 8th Russian National Conference on Heat Transfer (RNKT), Moscow: MEI Publishing, 2022, Vol. 1, pp. 435–438 — subsequently developed further and cited in follow-on work on numerical simulation of the formation and motion of turbulent vortex clouds ("puffs"), published in *Fluid Dynamics* (Springer/Pleiades), 2023.

This strand of work directly connects Ivanov's long-standing turbulent-jet and indoor-airflow expertise (developed originally for spacecraft cabin ventilation) to a matter of acute public-health relevance, and situates him within a genuinely international response effort spanning Spain, Italy, Germany, Australia, Slovenia, Brazil, and Russia.

## Selected Bibliography (Chronological, Non-Exhaustive)

1. I.Yu. Evstratov, V.V. Kalaev, A.I. Zhmakin, Yu.N. Makarov, A.G. Abramov, **N.G. Ivanov**, A.B. Korsakov, E.M. Smirnov, E. Dornberger, J. Virbulis, E. Tomzig, W. von Ammon. "Modeling analysis of unsteady three-dimensional turbulent melt flow during Czochralski growth of Si crystals." *Journal of Crystal Growth*, 2001, Vol. 230, pp. 22–29.
2. **N.G. Ivanov**, E.A. Rudinsky, E.M. Smirnov, S.A. Lowry, E. Dornberger, J. Virbulis, E. Tomzig, W. von Ammon. "Global model of Czochralski silicon growth to predict oxygen content and thermal fluctuations at the melt–crystal interface." *Microelectronic Engineering*, 2001, Vol. 56, pp. 139–142.
3. I.Yu. Evstratov, V.V. Kalaev, A.I. Zhmakin, Yu.N. Makarov, A.G. Abramov, **N.G. Ivanov**, A.G. Korsakov, E.M. Smirnov, E. Dornberger, J. Virbulis, E. Tomzig, W. von Ammon. *Journal of Crystal Growth*, 2002, Vol. 237–239, pp. 1757–1761.
4. **N.G. Ivanov**, A.B. Korsakov, E.M. Smirnov, K.V. Khodosevitch, V.V. Kalaev, Yu.N. Makarov, E. Dornberger, J. Virbulis, W. von Ammon. "Analysis of magnetic field effect on 3D melt flow in CZ Si growth." *Journal of Crystal Growth*, 2003, Vol. 250, pp. 183–188.
5. E.H. Turner, C.H. Son, E.M. Smirnov, **N.G. Ivanov**, D.S. Telnov. "Air circulation and carbon dioxide concentration study of International Space Station Node 2 with attached modules." *SAE Transactions*, 2004, Vol. 113, pp. 1150–1154.
6. E.M. Smirnov, **N.G. Ivanov**, D.S. Telnov. "Integrated Computational Fluid Dynamics Ventilation Model for the International Space Station." SAE Technical Paper 2005-01-2794, 2005.
7. E.M. Smirnov, **N.G. Ivanov**, D.S. Telnov, C.H. Son. "CFD modeling of cabin air ventilation in the International Space Station: a comparison of RANS and LES data with test measurements for the Columbus Module." *International Journal of Ventilation*, 2006, Vol. 5, No. 2, pp. 219–228.
8. C.H. Son, E.M. Smirnov, **N.G. Ivanov**, D.S. Telnov. "CFD study of ventilation and carbon dioxide transport for ISS Node 2 and attached modules." *SAE International Journal of Aerospace*, 2009, Vol. 4, pp. 519–524.
9. C.H. Son, E.M. Smirnov, **N.G. Ivanov**, D.S. Telnov. "CFD modeling of International Space Station and visiting spacecraft ventilation: evaluation of design solutions for complex on-orbit operations." 12th International Conference on Air Distribution in Rooms (Roomvent 2011), 2011.
10. C.H. Son, **N.G. Ivanov**, D.S. Telnov, E.M. Smirnov. "CFD Modeling of Water Droplet Transport for ISS Hygiene Activity Application." AIAA Technical Paper 2013-3456, 2013.
11. **N.G. Ivanov**, V.V. Ris, E.M. Smirnov, N.A. Tschur. "Numerical simulation of 3D flow effect on heat transfer from a tube bank of subsea cooler." Proc. 15th International Heat Transfer Conference (IHTC-15), Kyoto, Japan, 2014, Paper IHTC15-9766.
12. C.H. Son, **N.G. Ivanov**, E.M. Smirnov. "CFD Study of Ventilation on Board the International Space Station." 4th IAA Symposium "Space Flight Safety," St. Petersburg, 2017.
13. M.A. Zasimova, **N.G. Ivanov**, D. Markov. "Numerical modeling of air distribution in a test room with 2D sidewall jet. II. LES-computations for the room with finite width." ca. 2020–2021.
14. M.A. Zasimova, **N.G. Ivanov**, V.V. Ris. "URANS and LES simulation of the initial stage of propagation of a droplet-containing air jet characteristic of acute respiratory phenomena." Proc. 8th Russian National Conference on Heat Transfer (RNKT), Moscow: MEI Publishing, 2022, Vol. 1, pp. 435–438.
15. J. Pallarès, A. Fabregat, A. Lavrinenko, H.A.b. Norshamsudin, G. Janiga, D.F. Fletcher, K. Inthavong, M. Zasimova, V. Ris, **N. Ivanov**, R. Castilla, P.J. Gamez-Montero, G. Raush, H. Calmet, D. Mira, J. Wedel, M. Štrakl, J. Ravnik, D. Fontes, F.J. de Souza, C. Marchioli, S. Cito. "Numerical simulations of the flow and aerosol dispersion in a violent expiratory event: Outcomes of the '2022 International Computational Fluid Dynamics Challenge on violent expiratory events'." *Physics of Fluids*, 2023, Vol. 35, No. 4, Article 045106.
16. M.A. Zasimova, A.D. Krasikova, **N.G. Ivanov**. "Control of self-oscillations of a round turbulent jet propagating in a narrow rectangular cavity." *Thermophysics and Aeromechanics*, 2024, Vol. 31, No. 4, pp. 791–804.
17. M.A. Zasimova, **N.G. Ivanov**, E.D. Stepasheva. Parametric numerical study of turbulent jet self-oscillation modes in confined spaces (2D/3D URANS vs. Mataoui et al. 2001 experiment), Reynolds number 4×10³.

## Key Collaborators

- **Evgueni M. Smirnov** — Professor, Peter the Great St. Petersburg Polytechnic University; principal long-term co-author across nearly all of Ivanov's ISS-ventilation and CZ-growth publications.
- **Marina A. Zasimova** — SPbPU; principal co-author of Ivanov's 2020s indoor-airflow, jet self-oscillation, and respiratory-aerosol work.
- **Denis S. Telnov** — SPbPU / Institute of Applied Mathematics and Mechanics; co-author on the ISS ventilation series.
- **Vladimir V. Ris** — SPbPU; co-author on subsea-cooler heat transfer and respiratory-aerosol work.
- **Chang H. Son** — The Boeing Company, Houston, TX; the sustained U.S. industry counterpart on the ISS ventilation collaboration.
- **Alexander B. Korsakov, K.V. Khodosevitch** — co-authors on the CZ silicon melt-flow/magnetic-field studies.
- **V.V. Kalaev, A.I. Zhmakin, Yu.N. Makarov, I.Yu. Evstratov, A.G. Abramov** (STR Group / Ioffe Institute) and **E. Dornberger, J. Virbulis, E. Tomzig, W. von Ammon** (Wacker Siltronic) — collaborators on the crystal-growth simulation benchmark studies.
- International CFD Challenge collaborators (2022–): J. Pallarès and A. Fabregat (Universitat Rovira i Virgili, Spain), C. Marchioli and S. Cito (University of Udine, Italy), and a wider consortium including G. Janiga, D.F. Fletcher, K. Inthavong, and others.

## Professional Notes and Context

- Ivanov's career illustrates a distinctive and unusual research trajectory within CFD: beginning in industrial semiconductor materials processing (Czochralski melt convection under magnetic damping), pivoting toward aerospace human-factors/life-support engineering (ISS cabin ventilation), and — over the past several years — extending into building/indoor-environment ventilation and, most recently, respiratory pathogen-transmission fluid dynamics. The common technical thread throughout is turbulence-resolving 3D unsteady simulation (RANS, LES, and hybrid RANS/LES approaches) of buoyancy-influenced and confined-jet flows, generally cross-validated against experimental or field data — precisely the specialization listed on his institutional profile: Computational Fluid Dynamics; Buoyancy-Induced Flows and Heat Transfer; CFD Techniques for Environment Control Systems Evaluation; CFD Methods for Optimization of Industrial Flow Passages.
- His sustained multi-decade collaboration with Boeing on ISS ECLSS/ventilation CFD is a notable example of continuing technical engagement between Russian and U.S./international aerospace engineering communities in the human-spaceflight domain.
- His participation in the 2022–2023 International CFD Challenge on violent expiratory events situates him within a broader, pandemic-era international scientific response effort spanning multiple continents.

## Sourcing and Confidence Notes

This biography was compiled from:
- Peter the Great St. Petersburg Polytechnic University's official English-language personnel page for Ivanov Nikolay Georgievich (english.spbstu.ru), which provided his degree, title, researcher identifiers, and a short list of selected publications.
- Google Scholar profile metadata (citation count, listed research interests, institutional affiliation, co-author network).
- Publisher records and citation-trail cross-referencing (ScienceDirect/Journal of Crystal Growth, SAE Mobilus, AIAA, Springer/Fluid Dynamics, AIP Physics of Fluids, Thermophysics and Aeromechanics, ResearchGate-hosted PDFs and abstracts, and conference-proceedings citation lists).

No independent, dated academic CV (with year of Candidate degree conferral, thesis title, or full institutional employment history) could be located; the specific years of his academic appointments and the title of his Candidate dissertation therefore remain undetermined from available public sources and are not asserted here. Similarly, no evidence was found (or should be inferred) linking this Nikolay G. Ivanov to the unrelated Nikolay Ivanov (atomic physics, Ioffe Institute-trained, editor of St. Petersburg Polytechnic University Journal: Physics and Mathematics) or other same-surname researchers at the same university, whose fields (many-electron atomic theory) and career-timeline details are distinct and are excluded from this biography.

---

> [!NOTE]
> 
> Generated by Claude.ai
>
> Model: Sonet 5
>
> Prompt: Create an exhaustive scientific biography for Ivanov Nickolay G. (St. Petersburg Polytechnic University). Show the output in Markdown format. Do not copy the output of the exported files into the chat.
