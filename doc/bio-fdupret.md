# François Dupret (UCLouvain): An Exhaustive Scientific Biography

## Overview

François Dupret was a Belgian applied mathematician and mechanical engineer who spent his entire academic career at the Université catholique de Louvain (UCLouvain), where he became one of the world's leading figures in the numerical modelling and simulation of bulk crystal growth processes. Over more than three decades he built a research programme spanning computational fluid dynamics, non-Newtonian and viscoelastic flow, polymer processing, and — most prominently — the global, time-dependent simulation of industrial crystal-growth furnaces (Czochralski, Bridgman, Floating Zone, and related techniques). His work bridged rigorous applied mathematics (finite element theory, distribution theory, asymptotic methods) with direct industrial application, most visibly through the FEMAG family of simulation codes and the company FEMAGSoft S.A., which he co-founded to bring his group's models to semiconductor and photovoltaic manufacturers worldwide. He died unexpectedly in February 2018, and was memorialised at the ninth International Workshop on Modelling in Crystal Growth (IWMCG-9) later that year as a founding figure of the field.

---

## 1. Education and Formation

- Dupret pursued his doctoral studies at the Université Catholique de Louvain under the supervision of **Marcel J. Crochet**, a leading figure in computational rheology and non-Newtonian fluid mechanics.
- He obtained his **Ph.D. in 1981** from UCLouvain. His dissertation, *"Méthode variationnelle pour le calcul par éléments finis d'écoulements à surface libre"* ("Variational method for the finite element calculation of free-surface flows"), falls under the Mathematics Subject Classification heading of Fluid Mechanics.
- This thesis work is reflected in his earliest publications on variational/finite-element methods for free-surface and surface-tension-driven flows (see Section 4.1), which established the mathematical toolkit — variational principles, Lagrange multipliers for free boundaries, finite elements with moving meshes — that he would later redeploy at industrial scale in crystal growth modelling.
- Crochet's group at UCLouvain was, during this period, a major international centre for the numerical simulation of viscoelastic and free-surface flows, and several of Dupret's co-authors from this early period (Crochet himself, Jean-Marie Marchal, Yves Ryckmans, Paul Wouters) remained recurring collaborators for the following decade.

## 2. Institutional Career at UCLouvain

- Dupret's entire academic career was based at UCLouvain, in **Louvain-la-Neuve, Belgium**, where he was affiliated with **Applied Mechanics**, within what later became the Institute of Mechanics, Materials and Civil Engineering (**iMMC**).
- He built and led a research group at UCLouvain dedicated to the numerical simulation of industrial materials-processing problems, with two major thematic poles that persisted throughout his career:
  1. **Bulk crystal growth process modelling** (semiconductor and optical crystals).
  2. **Polymer processing and complex/non-Newtonian fluid flows** (injection moulding, resin transfer moulding, fibre-suspension flows, liquid-crystalline polymers).
- His laboratory trained and collaborated with a long list of doctoral students, postdoctoral researchers, and engineers, many of whom co-authored the bulk of his publication record and several of whom went on to independent academic or industrial careers (see Section 5).
- Dupret was also active in the university's applied-mathematics and mechanical-engineering teaching, and his group's software developments (see Section 6) were closely tied to industrially sponsored and doctoral research at UCLouvain.
- **Death:** Dupret passed away unexpectedly in **February 2018**, while still active in research. His passing was marked with a dedicated memorial session at the ninth International Workshop on Modelling in Crystal Growth (IWMCG-9, Wailea, Hawaii, 2018), where he was remembered as "a driving force in crystal growth modeling from the early 1980s," noted for his "academic rigor and engaging personality," and credited with having hosted the IWMCG in Belgium on two occasions (Durbuy, 1996, and Spa, 2015).

## 3. Research Programme: Thematic Overview

Dupret's scientific output, comprising at least **69 tracked publications** spanning 1981–2012 (with associated citations continuing to accrue well after his death), organises naturally into several interlocking research threads.

### 3.1 Free-surface and viscoelastic flow (early period, 1981–1994)
Building directly on his doctoral work, Dupret's first decade of research addressed:
- Variational/finite-element methods for free-surface flows with surface tension.
- Fundamental mathematical properties of viscoelastic constitutive models (loss of evolution, type change, sign of extra-stress eigenvalues) for Maxwell and Johnson–Segalman fluids, largely in collaboration with Jean-Marie Marchal and Marcel Crochet.
- Discretisation-error analysis in viscoelastic flow computation, and $h$–$p$ finite element treatment of interface singularities in two-fluid flows.

### 3.2 Global modelling of crystal growth furnaces (from 1986 onward)
This became the dominant and defining thread of his career. Key conceptual contributions include:
- The **"global" heat-transfer modelling** approach: rather than modelling only the melt or only the solid crystal in isolation, Dupret's method solves for heat conduction, diffuse-grey radiative exchange, and (where relevant) convection **simultaneously across the entire furnace** — melt, crystal, crucible, susceptor, insulation, heating elements — as a single coupled system driven only by external control parameters (pulling rate, heater power). This was a significant methodological advance over furnace models that treated internal boundary conditions as prescribed rather than computed.
- Extension of the global approach to **fully time-dependent (dynamic) simulation**, capturing the transient evolution of the crystal radius, the solid–liquid interface shape, and the whole thermal field over an entire growth run — as opposed to steady or quasi-steady snapshots.
- Application across multiple growth techniques and materials: Czochralski (Si, Ge, GaAs), Liquid-Encapsulated Czochralski (LEC) growth of GaAs, and vertical Bridgman growth (including the Mellen electro-dynamic gradient furnace).
- Incorporation of **melt convection** (including turbulent/eddy-viscosity treatments for large silicon melts) and its influence on interface shape and global heat transfer.
- Development of **reduced-order ("lumped") dynamic models** — small systems of ordinary differential equations capturing the essential Czochralski transients — intended for real-time/on-line simulation and eventual incorporation into automatic growth-control loops, in collaboration with the automatic-control group of Vincent Wertz at UCLouvain.
- Simulation of **back-melting** phenomena during shouldering, where the growth process must automatically switch between solidification and remelting regimes.
- Development of **adaptive/unstructured meshing techniques**, including grade-adaptive 1D boundary mesh generation and shape-quality 2D unstructured mesh generation with incremental refinement, needed to support moving-boundary finite element simulation of the growth interface throughout an entire dynamic run.
- Later work introduced a novel and highly efficient numerical technique to simulate the effect of an applied **transverse magnetic field (TMF)** on 3D melt flow and global heat transfer in large-diameter Czochralski silicon growth, validated against industrial-scale furnace configurations and literature data (2012, with Yoan Collet, Olivier Magotte, Nathalie Van den Bogaert).

### 3.3 Point defects and microdefect engineering in Czochralski silicon
From the mid-1990s, in close collaboration with industrial partners (notably Wacker Siltronic, via E. Dornberger and W. von Ammon) and academic collaborators (Talid Sinno, Robert A. Brown, Jan Vanhellemont), Dupret's group extended the global thermal/flow models to predict **intrinsic point-defect** (vacancy and self-interstitial) distributions and their aggregation into extended defects:
- Simulation of **grown-in void** formation and non-uniform void distributions in vacancy-rich Czochralski silicon, linking thermal history and point-defect dynamics to void nucleation and growth.
- Investigation of the influence of **boron doping concentration** on the position of the oxidation-induced stacking-fault ring (R-OSF).
- Dynamic, fully time-dependent prediction of point-defect distributions, including efforts to reconcile experimentally measured self-interstitial and vacancy diffusion coefficients with the classical **V/G criterion** (pulling-rate-to-thermal-gradient ratio) governing defect-type selection.
- Co-authorship of a major review, *"Defect engineering of Czochralski single-crystal silicon"* (Sinno, Dornberger, von Ammon, Brown, Dupret; *Materials Science and Engineering: R: Reports*, 2000), which became a standard reference in the field for linking crystal-growth process modelling to microelectronic-grade wafer quality.
- Later work (with F. Loix, A. de Potter, R. Rolinsky, N. Van den Bogaert, V. Regnier) integrated the full chain of point- and micro-defect formation, transport, recombination, and nucleation mechanisms into a unified predictive framework for optimising Czochralski silicon ingot quality (2009).

### 3.4 Process control and reduced/on-line models
Dupret pursued, in parallel with high-fidelity global simulation, the development of **fast, reduced dynamic models** suitable for real-time use:
- A "lumped model" for Czochralski growth expressed as a small system of coupled ODEs, designed to capture the essential process transients for use as an observer/predictor within a growth-control loop (with P. Jacmin, N. Van den Bogaert, V. Wertz).
- A reduced model for on-line, real-time simulation of the global heat transfer and solidification-front shape, explicitly intended for incorporation into industrial process-control systems (with E. Olivari, P. Jacmin, N. Van den Bogaert, V. Wertz).
- Later software-oriented work extended this quasi-dynamic/dynamic modelling hierarchy toward explicit **process optimisation and control** for both Czochralski (CZ) and Floating Zone (FZ) bulk growth, using the time-dependent FEMAG.2 software (2009, with Roman Rolinsky, Liang Wu, Vincent Regnier, and others).

### 3.5 Continuum theory of crystal defects (dislocations and disclinations)
In the later part of his career, Dupret pursued a more fundamental, purely mathematical line of research with **Nicolas Van Goethem** (later of the University of Lisbon), developing a rigorous **continuum/mesoscopic-scale theory of dislocations and disclinations** in single crystals:
- Use of **distribution theory** to represent concentrated defect densities along dislocation and disclination lines, resolving the multi-valuedness of the elastic displacement and rotation fields via intrinsic, single-valued Frank and Burgers vector fields.
- Derivation of fundamental identities relating the incompatibility tensor to the defect density fields, extending and reinterpreting the classical continuum theory of defects associated with Ekkehart Kröner.
- A multi-part treatment (2007, 2010, 2012) progressing from general theory and Volterra dislocations to the geometry of 2D dislocations and disclinations at both the mesoscopic and continuum scale, including treatment of countable families of dislocations.
- This body of work situates Dupret's contributions not only within applied/industrial crystal growth engineering but within the mathematical theory of continuum mechanics and defect geometry.

### 3.6 Polymer processing and complex fluids
Running throughout his career as a second major applied thread, Dupret worked extensively on the modelling and simulation of **polymer processing operations**, particularly injection moulding and composite manufacturing:
- Non-isothermal simulation of **injection moulding**, including temperature-field calculation with hybrid spatial discretisation for thin-cavity ("Hele-Shaw") geometries.
- Numerical prediction of **fibre orientation** in injection-moulded and compression-moulded short-fibre composites, including closure-approximation theory for orientation tensors and the "natural closure approximation."
- Development of a **closure approximation for nematic liquid-crystalline polymers** based on canonical distribution subspace theory and Bingham distributions (with Massimiliano Grosso and Pier Luca Maffettone).
- Non-isothermal simulation of the **resin transfer moulding (RTM)** process, and prediction of thermo-mechanical properties of compression-moulded fibre-reinforced composite parts (with Grégory Lielens, Alain Couniot, R. Keunings, and others).
- Modelling of **isothermal and non-isothermal crystallisation kinetics** of polyethylene terephthalate (PET), combining differential scanning calorimetry measurements with macro-kinetic modelling of induction time, degree of crystallinity, and secondary crystallisation.
- Simplified viscosity-law treatments (Cross law) for numerical simulation of Hele-Shaw injection-moulding flows.
- Micro-macro modelling of **permeability and hydrodynamic/mechanical dispersion** in porous media, relevant to resin flow through fibre preforms.

### 3.7 Electromagnetic and induction-heating modelling
With François Bioul, Dupret developed **matched asymptotic expansion techniques** to model two-dimensional induction-heating systems relevant to crystal-growth furnace design and to Marangoni/electromagnetically driven free-surface shear flows:
- Calculation of the electromagnetic (radio-frequency, alternating) field distribution and its confinement to a thin magnetic skin near conducting surfaces (Part I).
- Calculation of the resulting equivalent surface stresses and heat flux at the conductor surface (Part II).
- Analysis of free-surface shear flows driven jointly by **Marangoni (thermocapillary) effects** and alternating electromagnetic forces, of direct relevance to convection control in Czochralski and Floating Zone crystal growth.

### 3.8 Numerical methods
Beyond specific applications, Dupret contributed methodological work in finite element analysis:
- The **conformal Petrov–Galerkin (CPG) method** for convection-dominated (advection-diffusion) problems on triangular meshes, constructing exact nodal test functions within a conformal finite-dimensional weak-form framework (with B. Delsaute).
- Reparametrisation techniques for **piecewise rational Bézier curves** with $G^1$-continuity, relevant to shape blending and geometric boundary representation in mesh generation (with Roman Rolinsky).

## 4. Selected Chronological Bibliography

The following list reflects a representative, chronologically organised subset of Dupret's tracked publications, drawn from his institutional and bibliographic record. It is illustrative of the breadth described above rather than a claim of total completeness (conference proceedings and internal technical reports are less consistently indexed than journal articles).

**1981–1986 — Doctoral and early free-surface/viscoelastic work**
- Dupret, F. (1981). *Étude numérique d'écoulements irrotationnels incompressibles avec tension superficielle par une méthode variationnelle*. Journal de Mécanique.
- Dupret, F. (1981). Numerical study of incompressible fluids with free surface and surface tension by a variational principle.
- Dupret, F. (1982). A method for the computation of viscous flow by finite elements with free boundaries and surface tension.
- Dupret, F.; Marchal, J.-M.; Crochet, M.J. (1985). On the consequence of discretization errors in the numerical calculation of viscoelastic flow. *Journal of Non-Newtonian Fluid Mechanics*.
- Dupret, F.; Marchal, J.-M. (1986). Loss of evolution in the flow of viscoelastic fluid. *Journal of Non-Newtonian Fluid Mechanics*.
- Dupret, F.; Marchal, J.-M. (1986). Extra-stress eigenvalues sign for a Maxwell fluid flow / Sur le signe des valeurs propres du tenseur des extra-contraintes... *Journal de Mécanique Théorique et Appliquée*.
- Dupret, F.; Ryckmans, Y.; Wouters, P.; Crochet, M.J. (1986). Global finite element calculation of the Czochralski growth.
- Dupret, F.; Nicodème, P.; Ryckmans, Y.; Wouters, P.; Crochet, M.J. (1986). Numerical calculation of the global heat transfer in a Czochralski furnace. *Journal of Crystal Growth*.

**1988–1994 — Global furnace modelling, GaAs/LEC, injection moulding**
- Dupret, F.; Vanderschuren, L. (1988). Calculation of the temperature field in injection molding. *AIChE Journal*.
- Nicodème, P.; Dupret, F.; Crochet, M.J.; Nagel, G. et al. (1988). Numerical simulation of heat transfer in LEC growth of gallium arsenide.
- Nicodème, P.; Dupret, F.; Crochet, M.J. (1988). Effect of geometrical parameters upon the LEC growth of GaAs crystals.
- Ryckmans, Y.; Nicodème, P.; Dupret, F. (1989/1990). Numerical simulation of crystal growth: influence of melt convection on global heat transfer and interface shape. *Journal of Crystal Growth*.
- Dupret, F.; Nicodème, P.; Ryckmans, Y. (1989). Numerical method for reducing stress level in GaAs crystals. *Journal of Crystal Growth*.
- Crochet, M.J.; Dupret, F.; Ryckmans, Y.; Monberg, E. et al. (1989). Numerical simulation of crystal growth in a vertical Bridgman furnace. *Journal of Crystal Growth*.
- Dupret, F.; Nicodème, P.; Ryckmans, Y.; Wouters, P.; Crochet, M.J. (1990). Global modeling of heat transfer in crystal growth furnaces. *International Journal of Heat and Mass Transfer*.
- Kakimoto, K.; Nicodème, P.; Lecomte, M.; Crochet, M.J.; Dupret, F. et al. (1991). Numerical simulation of molten silicon flow; comparison with experiment. *Journal of Crystal Growth*.
- De Frahan, H.H.; Verleye, V.; Dupret, F.; Crochet, M.J. (1992). Numerical prediction of fiber orientation in injection molding. *Polymer Engineering & Science*.
- Delvaux, V.; Van Kemenade, V.; Dupret, F.; Crochet, M.J. (1993). Finite elements for viscoelastic flows with change of type. *Theoretical and Computational Fluid Dynamics*.
- Berghezan, D.; Dupret, F. (1994). Numerical simulation of stratified coating flow by a variational method. *Journal of Computational Physics*.
- Levieux, F.; Berghezan, D.; Dupret, F. (1994). Analysis of the interface singularity of a two-fluid flow by h and h-p finite elements. *Computer Methods in Applied Mechanics and Engineering*.
- **Dupret, F.; Van den Bogaert, N. (1994). "Modelling Bridgman and Czochralski growth." In: *Handbook of Crystal Growth*, Vol. 2B, Chapter 15, ed. D.T.J. Hurle, North-Holland, pp. 875–1010.** — Dupret's most cited single work, a comprehensive reference chapter on the mathematical and numerical modelling of the two dominant industrial bulk melt-growth techniques.

**1996–2000 — Dynamic global simulation, silicon defects, polymer/composite processing**
- Dornberger, E.; von Ammon, W.; Van den Bogaert, N.; Dupret, F. (1996). Transient computer simulation of a CZ crystal growth process. *Journal of Crystal Growth*.
- Van den Bogaert, N.; Dupret, F. (1996). Simulation of back-melting in Czochralski growth. *Journal of Crystal Growth*.
- Jacmin, P.; Van den Bogaert, N.; Dupret, F.; Wertz, V. (1996). A lumped model for the growth of CZ processed crystals. *IFAC Proceedings Volumes*.
- Olivari, E.; Van den Bogaert, N.; Wertz, V.; Dupret, F. (1996). A reduced model for fast simulation of crystal growth. *IFAC Proceedings Volumes*.
- Van den Bogaert, N.; Dupret, F. (1997). Dynamic Global Simulation of the Czochralski Process I: Principles of the Method. *Journal of Crystal Growth*.
- Van den Bogaert, N.; Dupret, F. (1997). Dynamic Global Simulation of the Czochralski Process II: Analysis of the Growth of a Germanium Crystal. *Journal of Crystal Growth*.
- Assaker, R.; Van den Bogaert, N.; Dupret, F. (1997). Time-dependent simulation of the growth of large silicon crystals by the Czochralski technique using a turbulent model for melt convection. *Journal of Crystal Growth*.
- Olivari, E.; Jacmin, P.; Van den Bogaert, N.; Dupret, F. (1997). The use of a reduced model for on-line simulations of the Czochralski growth of single crystals. *Journal of Crystal Growth*.
- Dornberger, E.; Gräf, D.; Suhren, M.; von Ammon, W. et al. (1997). Influence of boron concentration on the oxidation-induced stacking fault ring in Czochralski silicon crystals. *Journal of Crystal Growth*.
- Dornberger, E.; Esfandyari, J.; Vanhellemont, J.; Dupret, F.; et al. (1997/1998). Simulation of grown-in voids in Czochralski silicon crystals.
- Dupret, F. (1997). Second International Workshop on Modelling in Crystal Growth, Durbuy, Belgium, October 13–16, 1997: Preface. *Journal of Crystal Growth*.
- Dupret, F. (1997). Modelling in crystal growth — Proceedings of the Second International Workshop on Modelling in Crystal Growth, Durbuy, Belgium: Preface. *Journal of Crystal Growth*.
- Dupret, F.; Verleye, V.; Languillier, B. (1997). Numerical prediction of the molding of composite parts.
- Van Rutten, N.; Dupret, F. (1997). Calculation and optimisation of the feeding system in thermoplastics injection.
- Mal, O.; Couniot, A.; Dupret, F. (1998). Non-isothermal simulation of the resin transfer moulding press. *Composites Part A*.
- Lielens, G.; Pirotte, P.; Couniot, A.; Dupret, F.; Keunings, R. (1998). Prediction of thermo-mechanical properties for compression moulded composites. *Composites Part A*.
- Verhoyen, O.; Dupret, F.; Legras, R. (1998). Isothermal and non-isothermal crystallization kinetics of polyethylene terephthalate: mathematical modeling and experimental measurement. *Polymer Engineering & Science*.
- Verhoyen, O.; Dupret, F. (1998). A simplified method for introducing the Cross viscosity law in the numerical simulation of Hele-Shaw flow. *Journal of Non-Newtonian Fluid Mechanics*.
- Dupret, F.; Couniot, A.; Mal, O.; Verhoyen, O. (1999). Modelling and simulation of injection molding. *Rheology Series*.
- Dupret, F.; Verleye, V. (1999). Modelling the flow of fiber suspensions in narrow gaps. *Rheology Series*.
- Grosso, M.; Maffettone, P.L.; Dupret, F. (2000). A closure approximation for nematic liquid crystals based on the canonical distribution subspace theory. *Rheologica Acta*.
- Sinno, T.; Dornberger, E.; von Ammon, W.; Brown, R.A.; Dupret, F. (2000). Defect engineering of Czochralski single-crystal silicon. *Materials Science and Engineering: R: Reports*.

**2001–2012 — Meshing, magnetic fields, dislocation theory, defect optimisation**
- Kemmann, O.; Weber, L.; Jeggy, C.; Dupret, F.; et al. (2001). Simulation of the micro injection molding process.
- Wu, L.; Rolinsky, R.; Van den Bogaert, N.; Dupret, F.; et al. (2003). Development of new meshing techniques for the dynamic simulation of bulk crystal growth processes. *Rare Metals*.
- Bioul, F.; Dupret, F. (2005). Application of asymptotic expansions to model two-dimensional induction heating systems. Part I: calculation of electromagnetic field distribution. *IEEE Transactions on Magnetics*.
- Bioul, F.; Dupret, F. (2005). Application of asymptotic expansions to model two-dimensional induction heating systems. Part II: calculation of equivalent surface stresses and heat flux. *IEEE Transactions on Magnetics*.
- Bioul, F.; Dupret, F. (2005). Free surface shear flows induced by Marangoni and alternating electromagnetic forces. *Journal of Non-Equilibrium Thermodynamics*.
- Clain, S.; Dupret, F. (2006). Capillarity–dissolution system for a two-dimensional geometry. *Journal of Colloid and Interface Science*.
- Delsaute, B.; Dupret, F. (2005/2008). A (conformal) Petrov–Galerkin method for convection-dominated problems. *International Journal for Numerical Methods in Fluids*.
- Loix, F.; Thibaut, V.; Dupret, F. (2007). Modélisation micro-macro de la perméabilité et de la dispersion hydrodynamique dans un milieu poreux.
- Loix, F.; Thibaut, V.; Dupret, F. (2007). Modelling of permeability and mechanical dispersion in a porous medium and comparison with experimental measurements.
- Rolinsky, R.; Dupret, F. (2007). Practical C¹ reparametrization of piecewise rational Bézier curves.
- Van Goethem, N.; Dupret, F. (2007). A distributional approach to the geometry of dislocations at the mesoscale.
- Dornberger, E.; Esfandyari, J.; Gräf, D.; von Ammon, W.; et al. (2008). [work on grown-in void distributions continuing the 1997/1998 line].
- Loix, F.; Dupret, F.; de Potter, A.; Rolinsky, R.; Van den Bogaert, N.; Regnier, V. (2009). Optimization of silicon ingot quality by the numerical prediction of bulk crystal defects. *Solid State Phenomena*.
- Van Goethem, N.; de Potter, A.; Van den Bogaert, N.; Dupret, F. (2008). Dynamic prediction of point defects in Czochralski silicon growth: an attempt to reconcile experimental defect diffusion coefficients with the V/G criterion. *Journal of Physics and Chemistry of Solids*.
- Dupret, F.; Rolinsky, R.; Wu, L.; Regnier, V.; et al. (2009). Global simulation of CZ and FZ bulk crystal growth: from quasi-dynamic and dynamic modelling to process control and crystal quality optimization. *ECS Transactions*.
- Van Goethem, N.; Dupret, F. (2010). A distributional approach to the geometry of 2D dislocations at the mesoscale, Part A: General theory and Volterra dislocations; Part B: The case of a countable family of dislocations.
- Van Goethem, N.; Dupret, F. (2012). A distributional approach to 2D Volterra dislocations at the continuum scale. *European Journal of Applied Mathematics*.
- Van Goethem, N.; Dupret, F. (2012). A distributional approach to the geometry of 2D dislocations at the continuum scale. *Annali dell'Università di Ferrara, Sezione VII: Scienze Matematiche*.
- **Collet, Y.; Magotte, O.; Van den Bogaert, N.; Dupret, F.; et al. (2012). Effective simulation of the effect of a transverse magnetic field (TMF) in Czochralski silicon growth. *Journal of Crystal Growth*.** — one of Dupret's last major publications, extending global CZ furnace simulation to include magnetic-field effects on 3D melt flow at industrial scale.

*Aggregate bibliometric note: as tracked on ResearchGate, Dupret's record comprises 69 publications with roughly 2,000 citations, reflecting sustained influence particularly through the 1994 Handbook of Crystal Growth chapter and the 2000 defect-engineering review, both of which remain standard references cited in subsequent review literature on bulk crystal growth modelling (e.g., in *Annual Review of Chemical and Biomolecular Engineering* treatments of bulk single-crystal growth modelling).*

## 5. Collaborators and Research Network

Dupret's work was consistently collaborative, both within UCLouvain and with international academic and industrial partners. Principal collaborators identified across his publication record include:

- **Marcel J. Crochet** — UCLouvain, Dupret's doctoral advisor and closest early-career collaborator on viscoelastic flow and the founding Czochralski/Bridgman global-modelling papers.
- **Nathalie Van den Bogaert** — UCLouvain, co-author of the two foundational "Dynamic Global Simulation of the Czochralski Process" papers (1997) and the Handbook of Crystal Growth chapter (1994); a long-standing core collaborator across the crystal-growth modelling programme through 2012.
- **Nicolas Van Goethem** — later of the University of Lisbon (Centro de Matemática e Aplicações Fundamentais), Dupret's principal collaborator on the continuum theory of dislocations and disclinations (2007–2012), and on point-defect dynamics modelling.
- **Alain Couniot** — UCLouvain (later Sopra Steria Benelux), a recurring collaborator on polymer processing and composite moulding simulation.
- **Roman Rolinsky** — collaborator on meshing techniques, Bézier curve reparametrisation, and global CZ/FZ process control/optimisation software.
- **Talid Sinno** (University of Pennsylvania), **E. Dornberger** and **W. von Ammon** (Wacker Siltronic), **Robert A. Brown** (MIT/Boston University) — industrial-academic collaborators on point-defect and microdefect engineering in Czochralski silicon.
- **Jan Vanhellemont** (Ghent University) — collaborator on grown-in void and defect simulation.
- **Koichi Kakimoto** — Kyushu University, collaborator on early molten-silicon flow simulation validated against experiment (1991); later an international peer whose Japanese modelling group was frequently compared with Dupret's Belgian group as parallel poles of crystal-growth simulation research.
- **Yves Ryckmans, Paul Wouters, Pierre Nicodème** — UCLouvain, core members of the original 1986–1990 global-furnace-modelling team.
- **E. Monberg** (later OFS Fitel Denmark) — collaborator on vertical Bridgman furnace simulation (Mellen electro-dynamic gradient furnace).
- **Massimiliano Grosso** (University of Cagliari) and **Pier Luca Maffettone** — collaborators on liquid-crystalline polymer closure-approximation theory.
- **François Bioul** — collaborator on induction-heating and electromagnetically driven free-surface flow modelling.
- **Vincent Wertz** — UCLouvain (Department of Mathematical Engineering), collaborator on control-oriented reduced models for crystal growth.
- **Vincent Regnier, F. Loix, A. de Potter, Yoan Collet, Olivier Magotte, B. Delsaute, Liang Wu** — later-career UCLouvain co-authors on defect optimisation, magnetic-field simulation, and numerical methods.

According to the Mathematics Genealogy Project, Dupret formally supervised at least one doctoral student recorded in that database, with one further academic descendant, though his de facto mentorship extended to a considerably larger group of UCLouvain doctoral researchers and engineers reflected in his co-authorship record above.

## 6. Software and Industrial Impact: FEMAG and FEMAGSoft

A defining feature of Dupret's career was the translation of his group's mathematical models directly into industrially deployed simulation software:

- The **FEMAG** family of codes (and its time-dependent successor **FEMAG.2**) implemented the global, coupled heat-transfer/melt-flow/interface-tracking models developed by Dupret's group, and were applied to process-oriented simulation of essentially the full range of industrial bulk crystal growth techniques: **Czochralski, Kyropoulos, Floating Zone, Physical Vapour Transport, Directional Solidification, Vertical Bridgman, Vertical Gradient Freeze, and the Heat Exchange Method.**
- Dupret was associated with **FEMAGSoft S.A.**, a spin-off company based in Louvain-la-Neuve, Belgium (Avenue Jean Monnet), which commercialised this simulation software for use by semiconductor and photovoltaic-silicon manufacturers, positioning UCLouvain's academic modelling work directly within industrial crystal-growth process design and optimisation.
- His 1994 Handbook of Crystal Growth chapter (with N. Van den Bogaert) served for years as a primary reference work underpinning both academic and industrial modelling of Bridgman and Czochralski growth, and continues to be cited in surveys of the field.

## 7. Role in the International Crystal Growth Modelling Community

- Dupret was a founding and driving figure of the **International Workshop on Modelling in Crystal Growth (IWMCG)** series, a recurring specialist conference bringing together the small international community of researchers developing quantitative, physics-based models of bulk and solution crystal growth (with later venues including Hauppauge NY 2000, Fukuoka 2003, Bamberg 2006, Lake Geneva WI 2009, Taipei 2012, and Spa, Belgium 2015).
- He personally **hosted the IWMCG in Belgium on two occasions**: at Durbuy in 1996 (documented via his own editorial prefaces to the associated *Journal of Crystal Growth* proceedings volumes) and again at Spa in 2015.
- Contemporary historical accounts of the field (e.g., the 2020 retrospective on the Erlangen Crystal Growth Laboratory) place Dupret's UCLouvain group alongside Koichi Kakimoto's group in Japan and the Erlangen CGL/CrysVUn groups in Germany as one of the small number of internationally recognised centres competing and collaborating on quantitative Czochralski growth simulation methodology during the 1990s–2000s.
- Following his death, the IWMCG-9 organisers (2018, Wailea, Hawaii) devoted a **special memorial session** to Dupret, formally recognising his foundational role in the field "from the early 1980s" onward.

## 8. Assessment of Scientific Contribution and Legacy

Dupret's scientific legacy rests on several distinct but related pillars:

1. **Methodological**: he was among the pioneers of *global*, fully coupled, and eventually fully time-dependent finite-element simulation of entire crystal-growth furnace systems — an approach that moved the field from simplified or steady-state sub-models toward physically complete, industrially predictive tools.
2. **Applied/industrial**: through FEMAG and FEMAGSoft, his academic models were translated directly into commercial software used across essentially the full spectrum of industrial bulk crystal growth techniques, giving his work an unusually direct route from university research to semiconductor-industry practice.
3. **Defect physics**: his group's integration of thermal/flow modelling with intrinsic point-defect dynamics (vacancies, self-interstitials, grown-in voids, OSF rings) helped connect furnace-scale process engineering to microelectronic-grade crystal quality — a link of considerable practical importance to the silicon wafer industry.
4. **Mathematical foundations**: in the later part of his career, his collaboration with Nicolas Van Goethem on the distributional, continuum-scale theory of dislocations and disclinations extended his work into fundamental continuum mechanics, going beyond process engineering toward the mathematical theory of crystal defects themselves.
5. **Community building**: as a long-standing host and organiser of the IWMCG series, Dupret played a sustained institutional role in maintaining crystal-growth modelling as a coherent international research community, a role explicitly recognised in the memorial tribute following his death in 2018.

---

*This biography was compiled from publicly available bibliographic, institutional, and bibliometric sources, including UCLouvain/iMMC institutional records, ResearchGate's publication listing for Francois Dupret (Catholic University of Louvain), the Mathematics Genealogy Project, FEMAGSoft S.A.'s publications page, and published retrospectives on the international crystal-growth modelling community (including the IWMCG-9 memorial notice and the 2020 Erlangen Crystal Growth Laboratory historical review in* Crystal Research and Technology*). It should be treated as a research aid rather than an authoritative curriculum vitae; readers seeking primary-source verification of specific dates, titles, or affiliations are encouraged to consult UCLouvain's institutional repository and the original journal publications directly.*

---

> [!NOTE]
> 
> Generated by Claude.ai
>
> Model: Sonet 5
>
> Prompt: Create an exhaustive scientific biography for Francois Dupret, (Université catholique de Louvain). Show the output in Markdown format. Do not copy the output of the exported files into the chat.
