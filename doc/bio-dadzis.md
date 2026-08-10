# Kaspars Dadzis — Scientific Biography

**Affiliation:** Leibniz-Institut für Kristallzüchtung (IKZ), Max-Born-Straße 2, 12489 Berlin, Germany
**Field:** Crystal growth physics, multiphysical modelling, and experimental model-scale crystal growth
**ORCID:** 0000-0002-0126-7343

---

## 1. Overview

Kaspars Dadzis is a Latvian-German physicist and crystal-growth researcher at the Leibniz-Institut für Kristallzüchtung (IKZ) in Berlin, where he leads the "Model Experiments" research group. His work sits at the intersection of applied continuum physics, multiphysics numerical simulation, and dedicated laboratory-scale ("model") experiments designed to validate the theoretical models used to describe industrial crystal growth processes such as Czochralski (Cz) pulling, directional solidification, and float-zone growth. He is best known for reviving and formalising physical model experimentation as a rigorous validation tool for crystal growth simulations, for open-source simulation tooling built around the Elmer finite-element solver, and for winning an ERC Starting Grant (NEMOCRYS) — the first ever awarded to an IKZ researcher.

## 2. Education

- **University of Latvia, Riga** — Bachelor's and Master's studies in physics. He entered applied physics research already in his second year as an undergraduate, joining the group of Professor Andris Muižnieks, where he began with programming tasks for the numerical modelling of silicon crystal growth by the float-zone method. Both his bachelor's and master's theses continued this line of work (approx. 2002–2007).
- **Technische Universität Bergakademie Freiberg (TU Freiberg), Germany** — PhD (Dr.-Ing./Dr. rer. nat., defended 30 November 2012, thesis submitted 3 July 2012) in the field of directional solidification of multicrystalline silicon. Doctoral thesis: *"Modeling of directional solidification of multicrystalline silicon in a traveling magnetic field"* (published via TU Freiberg's Qucosa repository, urn:nbn:de:bsz:105-qucosa-117492). The thesis investigated the potential of a traveling magnetic field (TMF) for active control of melt flow during silicon solidification, developing a system of 3D numerical models built on open-source software to compute Lorentz forces, melt flow, and related transport phenomena. The doctoral work was carried out in industrial cooperation with SolarWorld (Freiberg) and the Fraunhofer Institutes IISB and THM.

## 3. Career Trajectory

| Period | Position / Activity |
|---|---|
| ~2002–2007 | Research assistant, University of Latvia, Riga — numerical simulation of float-zone crystal growth under Prof. Andris Muižnieks |
| 2008–2012 | Industrial/doctoral researcher, SolarWorld, Freiberg, Germany — silicon crystal growth for photovoltaics; concurrent PhD candidate at TU Bergakademie Freiberg |
| 2012–2016 | Continued industrial research at SolarWorld, Freiberg, focusing on silicon crystal growth for solar cells (post-doctoral period, ~4 years after the PhD) |
| 2016– | Joined the Leibniz-Institut für Kristallzüchtung (IKZ), Berlin-Adlershof, in the Silicon & Germanium working group |
| 2017 | Received the LIMTECH Young Scientist Award |
| 2020– | Founded and leads the IKZ junior research group **"Model Experiments"**, following award of an ERC Starting Grant |
| 2020–2025 | Principal Investigator, ERC Starting Grant project **NEMOCRYS** (Feb 2020 – Jan 2025) |
| 2023– | Principal Investigator, ERC Proof of Concept Grant **HANDSOME** (Hands-on Materials Science for Education) |

He now holds the title Dr. Kaspars Dadzis and continues as head of the Model Experiments group at IKZ, working within the institute's semiconductor/volume-crystals research area.

## 4. Major Research Programmes

### 4.1 NEMOCRYS — Next Generation Multiphysical Models for Crystal Growth Processes (ERC Starting Grant, 2020–2025)

In 2019 Dadzis was awarded an ERC Starting Grant, becoming the first IKZ researcher to receive this prestigious European Research Council funding line, and one of only four scientists in Germany selected that year in the "Products and Processes Engineering" panel. The grant provided **€1.5 million over five years**.

**Scientific rationale:** Crystal growth processes (e.g., Czochralski pulling, directional solidification) are highly complex, coupled multiphysical phenomena — involving heat transfer (including radiation and phase change), electromagnetism, melt and gas flow, and thermal/mechanical stress. Numerical simulation is routinely used for process optimisation, but the practical impossibility of direct, in-situ measurement inside real (opaque, high-temperature, vacuum-sealed, >1400 °C) industrial growth furnaces severely limits the accuracy achievable by theoretical/numerical models. As a result, crystal growth process development still relies heavily on experimental trial-and-error.

**Approach:** NEMOCRYS addressed this gap by reviving and formalising the **physical model experiment** as a validation methodology — deliberately scaling crystal growth processes down to accessible, low-temperature model systems using materials with low melting points (notably tin, melting at ~232 °C, and gallium, melting at ~30 °C) that are physically analogous to industrially relevant melts such as silicon. Reduced operating temperatures and relaxed vacuum-sealing requirements enable direct, simultaneous in-situ measurement of thermal fields, fluid flow, and stress distributions using modern optical and other measurement techniques — data that cannot practically be obtained from real high-temperature growth furnaces.

**Key infrastructure — the "MultiValidator":** The project built a dedicated model-scale Czochralski-type growth apparatus (approx. 0.5 × 1 m footprint, operating 30–700 °C) instrumented for coupled multiphysical measurement, alongside continued access to full-scale silicon growth furnace infrastructure (3 × 5 m, >1500 °C) for comparison.

**Conceptual link to history of science:** As part of NEMOCRYS, Dadzis explicitly revived the original 1918 Czochralski crystal-pulling experiment (Jan Czochralski's method for measuring the crystallisation velocity of metals) using tin, treating it as a multi-physical model experiment in its own right — reconnecting a century-old foundational technique with modern coupled-physics validation methodology.

**Outputs:** The project produced a suite of open-source simulation tools and codebases (hosted under the `nemocrys` GitHub organisation), including:
- **opencgs** — an open-source-based Python framework wrapping Gmsh (finite-element mesh generation) and Elmer FEM (multiphysics solver, including inductive heating and heat transfer) into an accessible interface for coupled crystal-growth simulation.
- **elmer-verification** — verification test cases for the Elmer finite-element solver.
- **test-cz-induction** — 2D steady-state electromagnetic and heat-transfer simulation of the NEMOCRYS "Test-CZ" model furnace with induction heating.
- **multilog** — a data acquisition and visualisation tool for recording measurements from multimeters, pyrometers, and optical/infrared cameras during model experiments.
- **crystal-game** — a visual/interactive simulation ("game") of Czochralski crystal growth, built for outreach and education.

Doctoral researchers trained within the NEMOCRYS/Model Experiments group include Arved Wintzer, whose PhD thesis *"Validation of multiphysical models for Czochralski crystal growth"* (TU Berlin, 2024) was produced under this programme.

### 4.2 HANDSOME — Hands-on Materials Science for Education (ERC Proof of Concept Grant, 2023– )

Building directly on NEMOCRYS, Dadzis was awarded an ERC Proof of Concept Grant of **€150,000** for the project *"Hands-on Materials Science for Education"* (HANDSOME) — the first ERC Proof of Concept Grant awarded to a researcher within the Forschungsverbund Berlin e.V. network. The project develops accessible, low-cost educational materials and tabletop demonstration experiments (building on the simple table-top model experiments — such as the tin Czochralski pull — developed as precursors to the MultiValidator apparatus) to bring crystal growth and materials science to a broader public and to support integration of the topic across educational contexts, addressing the fact that crystal growth remains a relatively unknown subject outside specialist research and industry circles.

### 4.3 Silicon crystal growth for photovoltaics and electronics (2008–2016 and ongoing)

Dadzis's earlier and continuing work addresses industrially critical silicon crystal growth technologies:

- **Directional solidification of multicrystalline silicon** under a travelling magnetic field (TMF) for active melt-flow control — the subject of his PhD and subsequent journal publications, aimed at improving silicon ingot quality (temperature field control, crystallisation interface shape, impurity transport) for photovoltaic applications.
- **Granulate-crucible silicon growth** — characterisation of impurities and structural defects (including transition-metal contamination) in silicon crystals grown from granulate feedstock in a continuous process, in collaboration with Fraunhofer IISB and TU Freiberg's Institute of Applied Physics.
- **Float-zone (FZ) silicon** — numerical simulation of species segregation and dopant/impurity distribution in FZ-grown crystals, and study of thermally stimulated dislocation generation during FZ growth, in collaboration with colleagues including Nikolay Abrosimov, Jānis Virbulis, and Andrejs Sabanskis (continuing the connection to his original Latvian float-zone modelling background).
- **Crucible-free silicon fibre growth** — simulation work supporting the growth of monocrystalline silicon fibres intended for mirror suspensions in gravitational-wave detectors, a niche high-precision application of crystal growth science.

## 5. Selected Publications

*(Representative list; not exhaustive. DOIs given where available.)*

- K. Dadzis, "Modeling of directional solidification of multicrystalline silicon in a traveling magnetic field," PhD thesis, TU Bergakademie Freiberg, 2012. urn:nbn:de:bsz:105-qucosa-117492
- K. Dadzis, G. Lukin, D. Meier, P. Bönisch, L. Sylla, O. Pätzold, "Directional melting and solidification of gallium in a traveling magnetic field as a model experiment for silicon processes," *Journal of Crystal Growth*, 445 (2016) 90–100. DOI: 10.1016/j.jcrysgro.2016.03.037
- K. Dadzis, P. Bönisch, L. Sylla, T. Richter, "Validation, verification, and benchmarking of crystal growth simulations," *Journal of Crystal Growth*, 474 (2017) 171–177. DOI: 10.1016/j.jcrysgro.2016.12.091
- K. Dadzis, O. Pätzold, G. Gerbeth, "Model experiments for flow phenomena in crystal growth," *Crystal Research & Technology*, 55(2) (2020) 1900096. DOI: 10.1002/crat.201900096
- K. Dadzis et al., "Characterization of Silicon Crystals Grown from Melt in a Granulate Crucible," (with K. Irmscher, C. Kranert, C. Reimann, N. Abrosimov, et al.), *Journal of Electronic Materials* (2020).
- H.-J. Rost, I. Buchovska, K. Dadzis, U. Juda, M. Renner, R. Menzel, "Thermally stimulated dislocation generation in silicon crystals grown by the Float-Zone method," *Journal of Crystal Growth*, 552 (2020) 125842. DOI: 10.1016/j.jcrysgro.2020.125842
- A. Enders-Seidlitz, J. Pal, K. Dadzis, "Development and validation of a thermal simulation for the Czochralski crystal growth process using model experiments," *Journal of Crystal Growth*, 593 (2022) 126750. DOI: 10.1016/j.jcrysgro.2022.126750
- N. Lorenz-Meyer, R. Menzel, K. Dadzis, A. Nikiforova, H. Riemann, "Lumped parameter model for silicon crystal growth from granulate crucible" (*Journal of Crystal Growth*).
- K. Surovovs, M. Surovovs, A. Sabanskis, J. Virbulis, K. Dadzis, R. Menzel, N. Abrosimov, "Numerical simulation of species segregation and 2D distribution in the Floating Zone Silicon crystals," *Crystals*, 12 (2022) 1718. DOI: 10.3390/cryst12121718
- K. Dadzis, "Czochralski growth of tin crystals as a multi-physical model experiment," preprint, arXiv:2305.06875 (2023).
- L. Vieira, I. Buchovska, I. Tsiapkinis, A. Wintzer, K. Dadzis, R. Menzel, "Simulation of crucible-free growth of monocrystalline silicon fibres for mirror suspension in gravitational-wave detectors," *Journal of Crystal Growth*, 629 (2024) 127549. DOI: 10.1016/j.jcrysgro.2023.127549

## 6. Honours and Recognition

- **LIMTECH Young Scientist Award (2017)** — awarded by the LIMTECH Alliance (a Helmholtz Association research initiative on liquid metal technology), recognising his work on model experiments and numerical simulation in crystal growth.
- **ERC Starting Grant (2019/2020)** — for NEMOCRYS; the first ERC Starting Grant awarded to an IKZ researcher in the institute's history, and one of four such grants awarded in Germany that year in the "Products and Processes Engineering" panel of the EU Horizon 2020 programme.
- **ERC Proof of Concept Grant (2023)** — for HANDSOME; the first such grant awarded to a researcher within the Forschungsverbund Berlin e.V. network.

## 7. Scientific Contributions and Themes

Across his career, several consistent threads characterise Dadzis's scientific contribution:

1. **Multiphysics coupling in crystal growth.** Treating crystal growth not as a single-discipline problem but as a genuinely coupled system spanning heat transfer (conduction, convection, radiation, latent heat), electromagnetism (induction heating, Lorentz-force-driven flow control via travelling magnetic fields), fluid dynamics (melt and gas flow), and thermomechanical stress — and building numerical frameworks (largely open-source, built on Elmer FEM and Gmsh) capable of representing this coupling.
2. **Physical model experiments as a validation paradigm.** His signature methodological contribution is the systematic use of low-melting-point analogue materials (gallium, tin) in specially designed, diagnostically accessible apparatus to obtain in-situ experimental data (flow fields, thermal fields, stress) that are inaccessible in real high-temperature industrial furnaces, explicitly to validate and improve numerical models rather than relying on trial-and-error process development.
3. **Open-source tooling for the crystal growth community.** Development and maintenance of publicly available simulation codebases (opencgs, elmer-verification, test-cz-induction, multilog) intended for reuse by the wider crystal growth simulation community, reflecting a commitment to reproducibility and shared infrastructure.
4. **Bridging industrial and fundamental research.** His trajectory — from industrial silicon photovoltaics research at SolarWorld to fundamental ERC-funded physics of crystal growth at IKZ — reflects a sustained effort to root fundamental multiphysics modelling in problems of direct industrial relevance (solar-grade silicon, semiconductor float-zone crystals, and niche applications such as gravitational-wave-detector mirror suspensions).
5. **Science communication and education.** Through HANDSOME and associated tabletop demonstration experiments (e.g., the historical Czochralski tin-pulling experiment), he has extended his research programme into public engagement and educational outreach in materials science.

## 8. Institutional Context

The Leibniz-Institut für Kristallzüchtung (IKZ) in Berlin-Adlershof is a member institute of the Forschungsverbund Berlin e.V. and the Leibniz Association, specialising in the growth of crystalline materials (bulk/volume crystals, thin films, and nanostructures) combining in-house plant engineering, numerical simulation, and crystal growth expertise. Dadzis's Model Experiments group operates within IKZ's semiconductor/volume-crystals research area, working alongside IKZ colleagues including Robert Menzel, Hans-Joachim Rost, Iryna Buchovska, and others on silicon and related semiconductor crystal growth, and maintaining active collaborative links to TU Bergakademie Freiberg, TU Berlin, Helmholtz-Zentrum Dresden-Rossendorf (HZDR), and the University of Latvia.

---

*Compiled from publicly available sources: IKZ Berlin institutional pages, Forschungsverbund Berlin e.V. press materials, Leibniz-Gemeinschaft news releases, TU Bergakademie Freiberg's Qucosa thesis repository, ResearchGate, GitHub (nemocrys organisation), and peer-reviewed journal metadata (Journal of Crystal Growth, Crystal Research & Technology, Crystals, Journal of Electronic Materials). Compiled August 2026; given the pace of Dadzis's ongoing research output, more recent publications and grants may exist beyond what is captured here.*


---

> [!NOTE]
> 
> Generated by Claude.ai
>
> Model: Sonet 5
>
> Prompt: Create an exhaustive scientific biography for Dadzis Kaspars (Leibniz-Institut für Kristallzüchtung (IKZ) in Berlin, Germany). Show the output in Markdown format. Do not copy the output of the exported files into the chat.
