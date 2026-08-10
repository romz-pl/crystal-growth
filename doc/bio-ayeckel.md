# Andrew Yeckel: A Scientific Biography

## Overview

Andrew Yeckel is a computational transport-phenomena researcher and software developer best known as the principal author, alongside Ralph T. Goodwin III, of **Cats2D** (Crystallization and Transport Simulator, 2D) and its 3D counterpart **Cats3D** — finite-element multiphysics codes for simulating coupled fluid dynamics, heat transfer, mass transfer, and moving-boundary phase change in materials processing systems. Over a research career spanning more than three decades, Yeckel built an unusually deep, singular body of work at the intersection of numerical algorithm development and applied crystal growth science, much of it carried out in close, long-running collaboration with Jeffrey J. Derby at the University of Minnesota. Since 2014 he has worked as an independent researcher, continuing to develop Cats2D and publish research on his own website.

## Education

- **B.S., Chemical Engineering** — University of California, San Diego, 1984.
- **Ph.D., Engineering Sciences (Chemical Engineering)** — University of California, San Diego, 1989. Dissertation: *"Modeling of Mass Transport in the Growth and Doping of Thin Films by Chemical Vapor Deposition,"* advised by Stanley Middleman.

Yeckel's doctoral work with Middleman established the pattern that would define his subsequent career: rigorous continuum transport modeling of materials-processing systems, combining mathematical analysis with practical engineering design questions (in this case, uniformity of film growth and doping in low-pressure chemical vapor deposition, LPCVD).

## Employment History

| Period | Position | Institution |
|---|---|---|
| 1989–1992 | Postdoctoral Research Associate | Dept. of Chemical Engineering and Materials Science, University of Minnesota |
| 1992–1993 | Consultant | Process Analysts, Inc., Lakewood, Colorado |
| 1994–1995 | Postdoctoral Research Associate | Dept. of Chemical Engineering and Materials Science, University of Minnesota |
| 1995–1999 | Research Associate | Dept. of Chemical Engineering and Materials Science, University of Minnesota |
| 9/2007–4/2008 | Visiting Scientist | Fraunhofer Institute of Integrated Systems and Device Technology (IISB), Erlangen, Germany |
| 1999–2014 | Senior Research Associate | Dept. of Chemical Engineering and Materials Science, University of Minnesota |
| 2014–present | Independent Researcher | Self-employed |

Yeckel's first postdoctoral appointment at Minnesota (1989–1992) placed him in the orbit of L.E. "Skip" Scriven's fluid-mechanics group, where he worked on free-boundary problems in coating flows — experience that would directly seed the free-surface and moving-boundary algorithms later built into Cats2D. His second and much longer stint at Minnesota (1994–2014, spanning postdoc, research associate, and senior research associate ranks) was conducted principally within Jeffrey J. Derby's research group in the Department of Chemical Engineering and Materials Science, where he became the group's central computational and software-development figure for two decades.

## Scientific and Technical Contributions

### Early work: CVD and thin-film processing (1986–1990)

Yeckel's earliest publications, co-authored with his doctoral advisor Stanley Middleman, addressed transport and uniformity problems in low-pressure chemical vapor deposition (LPCVD) — modeling diffusion–convection coupling in CVD reactors, growth-rate nonuniformity in doped polysilicon films, and boron diffusion from borosilicate glass sources. This work led to a practical invention: the **"cageboat,"** a novel silicon-wafer carrier designed to improve deposition uniformity, which was reported in the *Journal of the Electrochemical Society* (1990) and went on to see use in commercial DRAM fabrication.

A parallel strand of this early work addressed liquid-jet cleaning of films from solid surfaces (with Middleman and L. Strong/L.A. Klumb), extending his transport-modeling toolkit to impinging-jet stagnation flows.

### Free-boundary fluid dynamics and coating flows (1991–1994)

At Minnesota under Scriven, Yeckel worked on flow turning and recirculation in slot coating and related coating flows, and developed multiparameter continuation methods for tracking desired flow states in nonlinear fluid-dynamics problems — techniques for systematically mapping solution branches as physical parameters vary, later a hallmark capability of Cats2D. This period also connected him to CFAL, a free-boundary fluid dynamics code developed by Juan de Santos (a graduate student under Scriven), which directly informed the design philosophy Yeckel and Goodwin would bring to Cats2D.

### Bulk crystal growth modeling (1992–2014)

From the early 1990s onward, in collaboration with Jeffrey J. Derby and a long series of Derby's graduate students and postdocs, Yeckel became one of the field's leading computational specialists in continuum transport modeling of bulk melt- and solution-crystal-growth systems. This body of work — the great majority of his roughly 70 refereed journal articles and book chapters — addressed:

- **Vertical Bridgman / accelerated crucible rotation (ACRT) growth** of cadmium zinc telluride (CdZnTe), including segregation control, three-dimensional imperfections, detached (dewetted) Bridgman growth stability, and both proportional-integral and model-based nonlinear feedback control schemes for stabilizing the process.
- **Float-zone refinement** of electronic-grade silicon sheets.
- **Solution crystal growth** of potassium titanyl phosphate (KTP) and potassium dihydrogen phosphate (KDP), including three-dimensional, time-dependent flow and mass-transport analyses.
- **Electrodynamic gradient freeze (EDG)** growth of CdZnTe, including furnace-gradient effects, interface-shape control via dynamic "bell-curve" furnace profiles, and coupling of global furnace models to local three-dimensional flow models.
- **Traveling heater method (THM)** growth, including fundamental growth-rate limits and effects of rotating magnetic fields under microgravity conditions.
- **Edge-defined film-fed growth (EFG)** of cesium iodide and sapphire scintillator crystals, and micro-pulling-down (μ-PD) growth of sapphire.
- **Horizontal ribbon growth of silicon**, including thermal-capillary and segregation analysis.
- **Microgravity crystal growth**, including g-jitter effects, magnetic-field stabilization, and multi-scale modeling for space-based processing.
- **Particle engulfment during solidification**, developing steady-state and dynamic models for how second-phase particles interact with a moving solid–liquid interface.

A recurring technical theme across this body of work is the use of **magnetohydrodynamic (MHD) effects** — steady, rotating, and traveling magnetic fields — to suppress or control buoyancy-driven convection during melt growth, a strategy Yeckel and Derby examined analytically and computationally across multiple growth configurations.

Beyond specific growth systems, Yeckel made methodological contributions of broader applicability to computational transport phenomena, including:

- Parallel finite-element algorithms for three-dimensional incompressible flow (tested on CM-5 and T3D supercomputers) and associated preconditioning strategies.
- Techniques for setting a pressure datum in incompressible-flow computations.
- The **approximate block Newton method**, developed with Derby and L. Lun, for coupling multiple nonlinear solvers across different physical scales and phenomena (e.g., coupling local crystal-growth models to global furnace thermal models) — published in the *Journal of Computational Physics* (2009) and applied to multi-scale crystal-growth computations (2010).
- A **Schur-complement formulation** (with Lun and Derby) for free-boundary Stefan problems of phase change.
- Analysis of the existence, stability, and nonlinear dynamics of detached Bridgman growth states under zero gravity.

Yeckel also contributed occasional work outside crystal growth per se, including a diffusion-reaction model for DNA microarray assays (with C.J. Gadgil, Derby, and W.-S. Hu, 2004) and permeability calculations in fiber networks relevant to biomechanics (with T. Stylianopoulos et al., 2008).

### The Fraunhofer IISB visiting scientist appointment (2007–2008)

Yeckel spent an academic year (September 2007–April 2008) as a Visiting Scientist at the Fraunhofer Institute of Integrated Systems and Device Technology (IISB) in Erlangen, Germany, supported by a **Fraunhofer Society Prof.x2 Fellowship**. This placed him within a European center of excellence for crystal growth simulation alongside researchers such as Jochen Friedrich and Georg Müller, with whom Derby's group had existing collaborative and co-authorship ties (see, e.g., item 23 in the publication list below).

## Cats2D and Cats3D: Software Development

### Origins (1991–1996)

Cats2D traces its origin to 1991, when Ralph T. Goodwin, then a postdoctoral researcher working for Bill Schowalter at the University of Illinois, began writing a finite-element code for coupled transport problems. Yeckel, drawing on his prior experience with free-boundary fluid dynamics via the CFAL code (developed by Juan de Santos under Scriven at Minnesota), provided early technical advice to Goodwin's effort. In 1992, Yeckel formally joined Goodwin on the project, and over the following three years the two developed the core algorithmic architecture that still underlies Cats2D: a Galerkin finite-element method combined with an **arbitrary Lagrangian–Eulerian (ALE)** formulation for rigorous, sharp-interface tracking of moving and free boundaries.

### Solo development and the Derby group era (1996–2014)

When Goodwin left academia for industry in 1996, Yeckel continued developing the code alone for the next eighteen years, with continuous testing, validation, and application driven by the research needs of Jeffrey Derby's group at Minnesota. This tight feedback loop between code development and an active, publishing research group shaped Cats2D's particular strength in simulating transport phenomena in bulk crystal growth. The name "Cats2D" — an acronym for **C**rystallization **a**nd **T**ransport **S**imulator, 2**D** — was formally adopted in 2003.

### Independent redevelopment (2014–present)

In 2014, Yeckel left the Derby research group and became an independent researcher, undertaking what he has described as a "massive rewriting" of Cats2D: modernizing it for 64-bit computing, reorganizing its user interface, removing obsolete or broken features, and adding capabilities more typical of commercial CFD packages. Around this time Goodwin rejoined the effort, rewriting the code's frontal linear solver multiple times before settling on a nested-dissection-based algorithm.

### Technical capabilities

Per Yeckel's own technical documentation, Cats2D and its 3D counterpart Cats3D are general-purpose finite-element codes for stationary and time-dependent problems (2D and 3D-axisymmetric for Cats2D; fully 3D with MPI-based parallel domain decomposition for Cats3D) featuring:

- Coupled momentum, heat, and mass transport in arbitrary geometries.
- An arbitrary number of phases, with phase change, volume expansion/contraction, latent heat, segregation effects, and melt-growth kinetics including Gibbs–Thomson undercooling.
- Free-surface flows with capillarity and surfactant transport, and evaporative multiphase transport.
- Magnetohydrodynamic effects and induction heating.
- Arbitrary numbers of chemical species with homogeneous and heterogeneous reaction kinetics.
- Automated first-order and arclength parameter continuation, including along constrained relationships among multiple parameters.
- Parameter sensitivity analysis, frequency response, and linearized stability analysis.
- Inverse problems under arbitrary constraints and model-based process control.
- An integrated environment combining mesh generation, solution, and post-processing in a single interactive program.

Cats2D has never been released publicly; as of Yeckel's own account, it is available only by special arrangement.

### Litigation over ownership (2018)

In September 2018, Yeckel filed a copyright-infringement lawsuit in the U.S. District Court of Minnesota against his former employer, the University of Minnesota, and against Jeffrey Derby, disputing ownership of the Cats2D software following his 2014 departure. Neither defendant filed a formal answer or motion for summary judgment before the parties reached a settlement. On December 19, 2018, Yeckel voluntarily dismissed the suit with prejudice; under the settlement, Yeckel was recognized as sole owner of Cats2D, and the University and Derby were required to relinquish any claim of ownership and destroy their copies and derivative works of the software.

## Post-2014 Independent Work

Since becoming independent, Yeckel has maintained a personal website (andrewyeckel.com / cats2d.com) presenting both continued technical research and a body of digital and generative artwork produced using Cats2D's simulation and visualization capabilities (e.g., particle-laden flow visualizations he terms "ink balls," a "Kaleidoscope" art collection). Documented post-2014 technical work available on the site includes:

- Development of a semi-stochastic Brownian-motion model for particle-path integration in Cats2D.
- A long-running technical investigation into computing highly accurate, long-time particle pathlines and streaklines in steady incompressible flow, motivated by the observation that naively integrated pathlines in closed steady flows spuriously spiral or terminate — a violation of mass conservation.
- Continued development of critical-point-finding and flow-topology analysis algorithms, tracing back to methods he originally developed for CFAL in 1992.
- A Cats2D simulation of a Kármán vortex street — inspired by Sadatoshi Taneda's classical experimental visualization of the phenomenon — that was featured on the cover of a mathematics journal published by the European Mathematical Society, in the journal's area of nonlinear analysis.

## Professional Service and Recognition

- **Program Chair**, 19th American Conference on Crystal Growth and Epitaxy, Keystone, Colorado, 2013.
- **Executive Committee**, American Association for Crystal Growth, 2013–2017.
- **Guest editor**, *Journal of Crystal Growth* special proceedings volumes: 3rd International Workshop on Modeling in Crystal Growth (Stony Brook, NY, 2001; Vol. 230); 14th American Conference on Crystal Growth and Epitaxy (Seattle, WA, 2003; Vol. 250); 6th International Workshop on Modeling in Crystal Growth (Lake Geneva, WI, 2009; Vol. 312).
- **Organizing committee**, International Workshop on Modeling in Crystal Growth: 3rd (Stony Brook, 2000), 6th (Lake Geneva, WI, 2009), 7th (Taipei, Taiwan, 2012).
- **Journal reviewer** for, among others: *Journal of Crystal Growth*, *Crystal Growth & Design*, *AIChE Journal*, *Chemical Engineering Science*, *Physical Review Letters*, *International Journal for Numerical Methods in Fluids*, *Journal of Computational Physics*, *International Journal for Numerical Methods in Engineering*, *SIAM Journal on Applied Mathematics*, *International Journal of Thermal Sciences*, *Journal of Engineering Mathematics*, *Journal of Colloid and Interface Science*, *Computational Materials Science*, *Chemical Engineering Journal*, *Computer Methods in Applied Mechanics and Engineering*, *Computers & Chemical Engineering*, *Journal of Computing in Civil Engineering*, *Industrial & Engineering Chemistry Research*, and *International Journal of Heat and Mass Transfer*.
- **Consulting engagements**: Centre for Thermophysical Researches, Ltd. (2003–2004); Cellresin Technologies (1999); DIGIRAD, Inc. (1996–1997); Creare, Inc. (1996); Process Analysts, Inc. (1990–1991).
- **Trustee**, The Ray Thomas Edwards Foundation (1997–present per his CV; his current website lists him as a trustee of the successor Edwards-Yeckel Research Foundation and formerly of the now-defunct Ray Thomas Edwards Foundation).

### Awards

- Fraunhofer Society Prof.x2 Fellowship, 2007–2008.
- Research featured on the cover of *Crystal Growth & Design* (American Chemical Society), 2001–2003.
- Minnesota Supercomputer Institute Research Scholarships, 1990–1991 and 1991–1992.
- Recognition for invention of the "cageboat" silicon-wafer carrier, adopted in commercial DRAM fabrication (1989/1990).
- The Graduate Student Award, Southern California–Nevada Section of The Electrochemical Society, 1987.

## Selected Publications

*The following is drawn from Yeckel's own curriculum vitae (dated April 2020) and is illustrative rather than a complete republishing of the list; see his CV at cats2d.com for the full bibliography of over 100 refereed articles, book chapters, proceedings papers, and other publications.*

- Middleman, S. and Yeckel, A. (1986). "A model of the effects of diffusion and convection on the rate and uniformity of deposition in a CVD reactor." *J. Electrochem. Soc.*, 133, 1951–1956.
- Yeckel, A. and Middleman, S. (1990). "Strategies for the control of deposition uniformity in low-pressure CVD: The design of a novel wafer carrier." *J. Electrochem. Soc.*, 137, 207–212. *(Origin of the "cageboat" wafer carrier.)*
- Yeckel, A., Salinger, A.G., and Derby, J.J. (1995). "Theoretical analysis and design considerations for float-zone refinement of electronic grade silicon sheets." *J. Crystal Growth*, 152, 51–64.
- Yeckel, A. and Derby, J.J. (1997). "Numerical experiments in preconditioning with application to incompressible flows in materials processing." *Parallel Computing*, 23, 1379–1400.
- Yeckel, A. (1998). "Tools for parameter studies in fluid dynamics." *Int. J. Numer. Meth. Fluids*, 28, 1199–1216.
- Yeckel, A., Doty, F.P., and Derby, J.J. (1999). "Effect of steady crucible rotation on segregation in high-pressure vertical Bridgman growth of cadmium zinc telluride." *J. Crystal Growth*, 203, 87–102.
- Yeckel, A. and Derby, J.J. (2004). "Dynamics of three-dimensional convection in microgravity crystal growth: g-jitter with steady magnetic fields." *J. Crystal Growth*, 263, 40–52 (erratum, 267, 751–753).
- Yeckel, A., Lun, L., and Derby, J.J. (2009). "An approximate block Newton method for coupled iterations of nonlinear solvers: Theory and conjugate heat transfer applications." *J. Comput. Phys.*, 228, 8566–8588.
- Lun, L., Yeckel, A., and Derby, J.J. (2010). "A Schur complement formulation for solving free-boundary, Stefan problems of phase change." *J. Comput. Phys.*, 229, 7942–7955.
- Yeckel, A. and Derby, J.J. (2011). "Existence, stability, and nonlinear dynamics of detached Bridgman growth states under zero gravity." *J. Crystal Growth*, 314, 310–323.
- Yeckel, A., Daoutidis, P., and Derby, J.J. (2012). "Stabilizing detached Bridgman melt crystal growth: Model-based nonlinear feedback control." *J. Crystal Growth*, 361, 16–24.
- Tao, Y., Yeckel, A., and Derby, J.J. (2016). "Steady-state and dynamic models for particle engulfment during solidification." *J. Comput. Phys.*, 315, 238–263.
- Yeckel, A. (2016). "Modeling high speed growth of large rods of cesium iodide crystals by edge-defined film-fed growth (EFG)." *J. Crystal Growth*, 449, 75–85.
- Yeckel, A. and Goodwin III, R.T. (2015). *Cats2D (Crystallization and Transport Simulator), User Manual.* Unpublished (andrewyeckel.com/documentation.html).
- Derby, J.J. and Yeckel, A. (2004). "Modeling of crystal growth processes." In: *Crystal Growth — From Fundamentals to Technology*, eds. G. Müller, J.-J. Métois, and P. Rudolph, Elsevier, pp. 143–167.
- Yeckel, A. and Derby, J.J. (2005). "Computer modelling of bulk crystal growth." In: *Bulk Crystal Growth of Electronic, Optical and Optoelectronic Materials*, ed. P. Capper, John Wiley & Sons, pp. 73–119.
- Derby, J.J. and Yeckel, A. (2015). "Heat transfer analysis and design for bulk crystal growth: Perspectives on the Bridgman method." In: *Handbook of Crystal Growth*, 2nd ed., Vol. 2, ed. P. Rudolph, Elsevier, pp. 793–843.

## Summary Assessment

Andrew Yeckel's scientific career is distinguished by an unusually long and productive partnership between algorithm development and applied science: rather than functioning purely as either an academic PI or a software engineer, he occupied a hybrid role for over two decades as the primary architect of a research group's core simulation tool while also being one of its most prolific scientific authors. His technical contributions cluster around rigorous, physically grounded finite-element treatment of moving and free boundaries — a mathematically demanding class of problem central to melt crystal growth — and around numerical infrastructure (parameter continuation, block Newton coupling, Schur-complement free-boundary solvers, parallel preconditioning) that generalizes well beyond crystal growth to other coupled multiphysics problems. His departure from the University of Minnesota in 2014, the subsequent 2018 litigation over software ownership, and his transition to fully independent researcher and code owner represent an unusual career trajectory for someone with his publication record, and his post-2014 output — spanning both continued rigorous numerical research (pathline integration, flow topology) and generative digital art built on the same simulation engine — reflects a distinctive continuation of that work outside conventional institutional structures.

---

*Compiled from Andrew Yeckel's curriculum vitae (cats2d.com/cv.pdf, dated April 2020), the Cats2D project history page (cats2d.com/history.html), Cats2D documentation and research-topics pages (cats2d.com), and reporting on the 2018 Cats2D copyright litigation (BYU Copyright Blog, "The Cats2D Suit is Dismissed"). Given that Yeckel is a living, non-widely-biographied individual whose primary public record is self-published, this account should be treated as thorough but drawn substantially from self-reported sources rather than independently verified third-party biography.*

---

> [!NOTE]
> 
> Generated by Claude.ai
>
> Model: Sonet 5
>
> Prompt: Create an exhaustive scientific biography for Andrew Yeckel (author of Cats2D). Show the output in Markdown format. Do not copy the output of the exported files into the chat.
