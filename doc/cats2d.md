# Cats2D Multiphysics Simulation Software

**Subject:** Cats2D (cats2d.com), developed by Andrew Yeckel (with Ralph T. Goodwin)
**Report date:** July 2026
**Prepared as:** A comprehensive, current-state technical review

---

## 1. Executive Summary

Cats2D is a specialized, independently developed finite-element multiphysics simulation code for two-dimensional and 3D-axisymmetric (swirl) problems in coupled fluid dynamics, heat transfer, mass transfer, and moving-boundary/free-surface phenomena. It is the primary computational tool of Andrew Yeckel, a research scientist formerly affiliated with the University of Minnesota's crystal growth modeling group led by Jeffrey J. Derby, and it has underpinned several decades of peer-reviewed research on bulk melt and solution crystal growth. The code's distinguishing technical feature is a custom-written, extremely fast and memory-efficient direct (frontal/nested-dissection) linear solver authored by Ralph Goodwin, Yeckel's long-time collaborator.

Cats2D is **not a commercial product**. It is not sold, licensed, distributed for download, or supported as a packaged application in the way that ANSYS Fluent, COMSOL, or OpenFOAM are. There is no evidence on the website of a public source code repository, installer, or license terms — despite one page describing installation "out of the box" under OS X, Linux, and Unix. The site functions primarily as a personal research showcase, technical blog, and archive of Yeckel's scientific and artistic output, built around a single-developer (plus one close collaborator) codebase with a 30+ year history.

This report synthesizes information gathered directly from cats2d.com (Overview, Features, History, Publications, Developments/blog, Documentation, and Research Topics pages) as of the site's current published state.

---

## 2. What Cats2D Is

### 2.1 Technical positioning

Cats2D is described by its author as software that "specializes in analysis of transport phenomena in moving boundary problems with complex interfacial conditions, such as phase change, interfacial mass transport, and free surfaces with capillarity." It is a general-purpose Galerkin finite-element solver for stationary and time-dependent problems in:

- **Coupled momentum, heat, and mass transport** in arbitrary 2D or 3D-axisymmetric (swirl) geometries
- **Moving/free boundaries**, implemented via an **Arbitrary Lagrangian–Eulerian (ALE)** finite element formulation
- **Multiphase problems** with an arbitrary number of phases, including phase change with volume expansion/contraction, latent heat, solute segregation, and melt growth kinetics with **Gibbs–Thomson undercooling**
- **Free-surface flows with capillarity**, including surfactant transport and thermo- and electro-capillary effects, plus evaporative multiphase transport
- **Magnetohydrodynamics (MHD)**: induction heating, traveling and rotating magnetic fields
- **Chemical species transport** with homogeneous and heterogeneous reaction kinetics
- **Continuation and bifurcation analysis**: automated first-order and arclength parameter continuation, constrained multi-parameter tracking, parameter sensitivity analysis, frequency response, and linearized stability analysis
- **Inverse problems and model-based process control**

The finite element discretization uses a **nine-node biquadratic velocity / linear discontinuous pressure element (Q2/P–1)**, which satisfies the Ladyzhenskaya–Babuška–Brezzi (LBB) stability condition (eliminating spurious pressure modes) and, according to Yeckel, conserves mass exactly in an integral sense over each element — a property he argues is superior to the more commonly used biquadratic-bilinear (Q2/P1, continuous pressure) element for accurate pathline computation.

### 2.2 Integrated environment

Unlike typical academic CFD codes that rely on separate meshing, solving, and post-processing tools chained together in a workflow, Cats2D integrates **mesh generation, solution, and post-processing into a single interactive program** with a **text-based, menu-driven command-line interface**. Key workflow features include:

- A simple, human-readable **control file format** ("flowctrl") where commands/comments can appear in any order
- A **macro recorder** for automating and customizing figure generation
- A **command-line/flag parser** enabling batch processing (mesh refinement, post-processing, parameter sweeps), including queuing to batch systems
- **High-resolution, publication-ready image output**, with automatically generated **LaTeX tables and problem-statement text** for direct inclusion in manuscripts
- A custom **CIELAB (L\*a\*b\*)-based color scale** for scientific visualization, added specifically because Yeckel considers it more perceptually intuitive than HSV-based schemes (he references Kenneth Moreland's diverging warm–cool color map research)

### 2.3 The solver: the code's centerpiece

The single most emphasized technical asset of Cats2D is its **direct linear equation solver**, authored by Ralph Goodwin. It is a frontal-type solver reengineered around **nested dissection** for equation assembly/elimination, using multi-threaded **CBLAS** operations for simultaneous elimination of multiple equations ("four pivots"/multirank outer products) and static condensation. Documented performance claims (see §5) include:

- Roughly linear (not quadratic) scaling of factorization wall-clock time with problem size, up to several million unknowns
- A memory-usage reduction of ~89% relative to the prior ("old") solver generation
- Full, accurate Gaussian-elimination factorizations of ~4 million-unknown problems in under a minute on a 2013-era dual-core laptop

Yeckel frames this as a deliberate rejection of parallel-computing-as-panacea: his repeated technical argument (see §6) is that **algorithmic and serial-code improvements dwarf the gains available from brute-force parallelization**, and that Cats2D's philosophy is "use it and forget it" — no solver tuning required from the user.

---

## 3. History and Development Lineage

Cats2D has an unusually well-documented, personal 30+ year lineage, entirely narrated by Yeckel himself:

| Period | Development |
|---|---|
| **1991** | Ralph Goodwin, as a postdoc under Bill Schowalter at the University of Illinois, starts "The Code." |
| **1992** | Andrew Yeckel joins Goodwin's effort, bringing experience from CFAL (a free-boundary fluid dynamics code developed by Juan de Santos under Skip Scriven at the University of Minnesota). |
| **1992–1995** | Yeckel and Goodwin jointly build most of the core elements underlying the modern code. |
| **1994** | The code (then called "Charisma," ~80,000 lines) is already substantial; Goodwin publishes an early online user manual while a visiting professor at ESPCI Paris (1995). |
| **1996** | Goodwin leaves for industry. Yeckel continues solo development for the next 18 years, with extensive testing/validation support from Jeff Derby's crystal growth research group at the University of Minnesota. |
| **2000–2002** | A few students begin using the code; Yeckel starts a new user manual. |
| **2003** | The code is renamed **Cats2D** ("Crystallization And Transport Simulator," 2D), reflecting its heavy use in bulk crystal growth research; this is also the citation name used in subsequent publications. |
| **2014** | Yeckel leaves the Derby research group and undertakes a "massive rewriting" — modernizing for 64-bit computing, reorganizing the UI, removing broken/obsolete features, and adding capabilities typical of commercial CFD codes. Around the same time, Goodwin rejoins and rewrites the frontal solver multiple times, ultimately landing on the nested-dissection algorithm described above. |
| **2015–present** | Yeckel operates independently (self-described as having "left his job" in the mid-2010s), developing Cats2D without institutional affiliation, funding, or oversight, publishing results and commentary via cats2d.com. |

By Yeckel's own account (as of a 2019/2020-era blog entry), the codebase is approximately **170,000 lines of code across roughly 240 source files**, written primarily in **C** (with some use of CBLAS/BLAS libraries, and — per his stated philosophy — deliberately avoiding CUDA and minimizing dependence on non-permanent technology stacks; MPI is mentioned as tolerable, GPU frameworks are not).

---

## 4. Scientific Track Record and Publications

Cats2D (and its predecessor "Charisma") has a substantial, verifiable publication record spanning **1995 to 2018**, overwhelmingly concentrated in **bulk/melt crystal growth modeling**, much of it produced in collaboration with Jeff Derby's group at the University of Minnesota. The Publications page lists:

- **53 refereed journal articles and book chapters** (plus 8 more listed separately under "Articles with disputed author lists" — a candid, unusual disclosure by Yeckel that these papers involved authorship disagreements)
- **19 conference proceedings papers**
- **1 additional book-chapter contribution** (1995, in a volume edited by Stan Middleman)

Representative subject matter includes:
- Float-zone refinement of electronic-grade silicon
- Vertical Bridgman and gradient-freeze growth of **cadmium zinc telluride (CZT)**, a major application domain (radiation detector material), including accelerated crucible rotation technique (ACRT), submerged baffles/insulators, traveling and rotating magnetic fields, and segregation control
- Micro-pulling-down growth of sapphire
- Edge-defined film-fed growth (EFG) of cesium iodide and silicon ribbon
- Particle engulfment during silicon crystal solidification (including SiC/Si₃N₄ particle pushing, work tied to microgravity experiments)
- Traveling heater method (THM) growth limits
- Model-based feedback control of Bridgman crystal growth
- Numerical-methods contributions in their own right: an approximate block Newton method for coupled nonlinear solvers (*J. Comput. Phys.*, 2009), a Schur-complement formulation for Stefan (phase-change) problems (*J. Comput. Phys.*, 2010), and a benchmark study of pressure-datum setting in incompressible flow solvers (*Int. J. Numer. Meth. Fluids*, 1999)
- One outlier application: a diffusion-reaction model for DNA microarray assays (2004), showing the code's generality beyond crystal growth

Journals represented include *Journal of Crystal Growth* (the dominant venue, by far), *Journal of Computational Physics*, *International Journal for Numerical Methods in Fluids/Engineering*, *Chemical Engineering Science*, *Physics of Fluids*, *Journal of Fluid Mechanics*, and *Journal of Biotechnology*, among others.

**Notably, essentially all of this publication activity predates 2019.** No refereed publications from 2019 onward are listed. This is consistent with Yeckel's departure from institutional research (the Derby group) around 2014–2015 and his transition to independent, largely unpublished (in the peer-review sense) work documented instead through the website's blog.

A striking authorship note: Goodwin, despite being co-architect of the solver central to essentially every one of these papers, is **not a coauthor on any of them** — his contribution is instead acknowledged via code citation, a point Yeckel discusses at unusual length and with evident discomfort in the "developments" blog (see §6).

---

## 5. Independent Validation Claims

Yeckel places heavy emphasis on code verification and validation, articulated as a near-manifesto (see §6.3). Verification/validation activities documented on the site include:

- **Exact-solution benchmarks**: Couette–Poiseuille flow (with arbitrary domain rotation), solid-body rotation, Von Kármán swirling flow, Homann stagnation-point flow, Stokes flow past a sphere, and **Hill's spherical vortex** (an 1884 exact solution used to validate derived quantities such as vorticity, pressure, and principal stresses to within ~0.02% error on a ~71,000-equation discretization using a non-coordinate-aligned mesh)
- **Numerical benchmark problems**: the 2D lid-driven cavity (described as Yeckel's "favorite computational test bed ever," with an associated benchmark paper), Rayleigh–Bénard convection, and Taylor–Couette flow
- **Physical experiment comparisons**: reproduction of classic flow-visualization photographs from Milton Van Dyke's *An Album of Fluid Motion* (1982), including Kármán vortex street formation behind a cylinder (validated against Taneda's 1979 photograph of flow past a fence, and against Honji & Taneda 1969 and Countanceau & Bouard photographs of impulsively started cylinder flow at Re = 1700–5000), and thermal convection between concentric cylinders (Grigull & Hauf, 1966, at Grashof ≈ 385,000–405,000)
- **Solver performance benchmarking** (§2.3): quantitative wall-clock and memory scaling studies comparing the "old" and "new" (post-2014) Cats2D solvers on the lid-driven cavity problem up to ~4 million degrees of freedom, run on a 2014 MacBook Pro

Yeckel's stated epistemic position (published in the "Two sides of the same coin" blog entry) is that the correctness of the governing equations (Navier–Stokes, energy, species transport) is essentially settled physics, and that the real risk in CFD lies in implementation correctness — which he argues can only be established through exhaustive testing against known solutions, not through source code inspection or public code release. This is an explicit, argued rejection of the "open code for peer review" norm advocated by reproducibility/open-science initiatives (he cites, and disagrees with, the Science Code Manifesto and a *Nature*-linked "publish your code" blog post).

---

## 6. Yeckel's Public Commentary and the Nature of the Website

A defining and unusual characteristic of cats2d.com is that it doubles as a **long-form, first-person blog** ("Developments" page) mixing:

1. Technical updates to Cats2D (new features: Brownian-motion-augmented particle tracking, streaklines, CIELAB color scales, principal-stress/extension-axis visualization tools)
2. **Fine-art output** generated using Cats2D's flow simulations as a generative medium (named collections: "Triskelion," "Fandango," "Kaleidoscope," a "Mondrian" series reproducing De Stijl-style compositions via physics-based flow calculations), including physical prints on canvas and Chromaluxe aluminum
3. Extensive **opinion essays** on the state of CFD, academic scientific computing, software engineering practice, and (occasionally) unrelated personal/social commentary

### 6.1 Positions on the CFD/scientific-computing industry
Yeckel is highly critical of the trajectory of both commercial and academic CFD:
- He characterizes CFD industry growth (~13% annualized, 1990–2010, citing a source he does not name in detail) as "pitiful" relative to the collapse in computing costs over the same period, and asserts that growth has stayed "tepid" since
- He identifies ANSYS as the dominant commercial CFD vendor (~$1 billion annual revenue, "much of which comes from services") and criticizes persistently high licensing costs
- He argues academic CFD/scientific-computing research and education have declined, largely because faculty principal investigators do not personally engage in code development, leaving it to transient trainees, resulting in "intellectual scaffolding" that degrades over time even as computing capability grows
- He is sharply skeptical of machine learning as a scientific/intellectual category, characterizing it (in a 2019-era entry) as "model selection and data fitting" rather than "learning," and disputes the framing of neural networks as exhibiting anything resembling cognition

### 6.2 Positions on parallel computing vs. algorithms
A recurring, technically substantive argument (§2.3, and the "Vetrate di Chiesa" entry) is a ranked hierarchy of importance for CFD performance:

> **Numerical methods > Algorithms > Serial optimization > Parallelization**

He illustrates this with Goodwin's solver history: two purely serial/algorithmic improvement phases (1992 static condensation + multi-pivot elimination; 2014 nested dissection) delivered a cumulative ~20× serial speedup and improved asymptotic scaling from roughly O(N^1.5) to O(N^1.2), while multithreading contributed a comparatively modest ~3× on top of that. He uses this to argue that "parallelizing a poorly optimized algorithm is a waste of time" and that hardware-driven approaches (vector supercomputers → parallel supercomputers → GPU computing) cannot compensate for weak underlying algorithms, given the O(N³) cost floor of dense Gaussian elimination.

### 6.3 Positions on reproducibility and open source
Yeckel explicitly rejects mainstream open-science/reproducibility norms as applied to CFD codes, arguing:
- Reproducibility of computational results is "an illusion" given the constantly shifting technology landscape
- Source code inspection cannot verify a nontrivial CFD code's correctness; only extensive testing against known solutions can
- He is unpersuaded that proprietary codes (he cites Fluent specifically) should be excluded from publication-supporting use while unreviewed one-off academic codes are accepted uncritically
- He offers his own six-point "no-bullshit CFD manifesto" (numerical rigor, vigorous validation, convergence discipline without artificial stabilization, honest visualization, methodological documentation sufficient for expert replication, and ongoing personal skill maintenance), explicitly dismissing "reproducibility declarations, version control, GitHub, and all that" as "bullshit"

**This is a materially different philosophy from most modern scientific-software practice**, which increasingly emphasizes public repositories, continuous integration, and open licensing (e.g., OpenFOAM, FEniCS, deal.II). Cats2D is positioned by its author as the deliberate antithesis of that trend: closed-source, single/dual-developer, validated by exhaustive internal testing rather than external code review.

### 6.4 Personal and biographical content
The Developments page interleaves substantial personal material: a decades-long friendship/collaboration narrative with Goodwin (they met in 1985; Goodwin was a Navy nuclear-submarine veteran turned UCSD chemical engineering student); reflections on a 30-year marriage; food, sailing/"Carbon Fiber," and CSA farming references in the site footer; and numerous asides on unrelated topics (drug policy statistics, journalism's handling of unit conversions, a *Star Trek* reference, starfish behavior). This content is idiosyncratic and central to the site's character but is **not technical documentation** of the software itself.

---

## 7. Current State of the Software (as documented)

### 7.1 Availability and access
- The Overview page states Cats2D "installs out of the box under OS X, Linux, and Unix operating systems" and references an "Installation" page and a "text-based user interface" ("menu") page.
- However, **no public download link, source repository, package manager entry, license, or pricing/access information is presented on any page reviewed.** There is no evidence Cats2D is distributed to the general public, and Yeckel's own commentary (§6.3) suggests he does not believe in open publication of the source code. The most plausible reading is that "installs out of the box" describes the experience for Yeckel himself and any direct collaborators/former colleagues, not a publicly downloadable product.
- The site includes a Contact page and references a Curriculum Vitae, suggesting Yeckel is reachable for collaboration, consulting, or (per a "Cats2D onsite training" blog entry heading) training engagements, though no further detail on commercial terms is given.

### 7.2 Documentation maturity
- The primary **User Manual is explicitly described as outdated** ("badly lagged development of the code and much within it is no longer current"), with a promised rewrite ("Coming soon!") that, based on available material, had not appeared as of the site's most recent updates.
- A "weaknesses" page is linked, indicating the author maintains an explicit, self-critical list of the code's limitations — an unusual degree of candor for simulation software documentation.
- Supplementary technical notes exist as standalone PDFs covering: Stefan-problem interface boundary conditions, Gibbs–Thomson undercooling computation, particle-motion modeling near interfaces, finite element representation of static pressure, Newton-like block coupling algorithms, and pre-Cats2D parameter-study/continuation methods work — collectively indicating meaningful documented numerical methodology despite the absence of a current unified user manual.
- A dedicated benchmark paper on the 2D lid-driven cavity is referenced as an update to prior high-accuracy benchmarks in the literature.

### 7.3 Development activity and cadence
- The "Developments" blog format has no visible dates on individual entries in the extracted content, but internal references allow rough dating: entries reference events "eight years" after a 2011 white paper (~2019), a "past four years" of work relative to a Research Topics page dated 2015–2019, and copyright notices ranging **2016–2020** on unpublished blog content and **2015–2019** on the Research Topics page. The site's overall copyright line (homepage) reads **"Copyright © 2020."**
- One entry explicitly states "this is the first time I have posted anything here in over a year," indicating **irregular, bursty update cadence** rather than continuous active development logging.
- Feature additions documented in relatively recent entries include: semi-stochastic Brownian-motion particle path integration, streakline visualization, CIELAB-based color mapping, and new vector/contour plot types for principal stress/extension-axis visualization — indicating the code continued to receive active numerical and visualization feature development at least through the late 2010s.
- Given the absence of dated entries in the retrieved content beyond the visible copyright ranges, **this report cannot confirm specific development activity in 2021–2026** from the site content alone; readers requiring the latest status should consult cats2d.com directly, particularly the Developments page, for any more recent entries.

### 7.4 Scientific credibility signals
- Strong: multi-decade, peer-reviewed publication record in a respected specialty (crystal growth transport modeling); a Cats2D-generated image was used for the cover of a Springer/European Mathematical Society-affiliated journal focused on nonlinear analysis (per Yeckel's account); extensive, methodologically serious validation against exact solutions, canonical numerical benchmarks, and physical flow-visualization experiments.
- Caveats: the code is not independently audited or open to public/community review; all validation is self-reported and self-conducted by the author; there is no third-party or community user base described (in contrast to widely adopted open-source or commercial CFD tools); publication output appears to have ceased in the peer-reviewed sense around 2018, coincident with Yeckel's move to fully independent, non-institutional work.

---

## 8. Comparison Context

To situate Cats2D within the broader CFD/multiphysics software landscape as of this report:

| Attribute | Cats2D | Typical commercial CFD (e.g., ANSYS Fluent, COMSOL) | Typical open-source CFD (e.g., OpenFOAM, FEniCS) |
|---|---|---|---|
| Distribution | Not publicly distributed | Licensed, paid | Freely available, open source |
| Dimensionality | 2D and 3D-axisymmetric only | Full 3D | Full 3D |
| Development team | 1–2 people (Yeckel, Goodwin) | Large commercial teams | Distributed open-source communities |
| Core differentiator | Custom nested-dissection direct solver; free-boundary/ALE moving-mesh specialization; crystal-growth physics | Broad general-purpose feature set, GUI, vendor support | Broad general-purpose feature set, community modules |
| Validation model | Author-conducted, exhaustive, published on personal site | Vendor-conducted + large user base | Community-conducted, distributed |
| Typical use case | Yeckel's own research (historically crystal growth, now broader transport phenomena and flow visualization/art) | Industrial/commercial engineering analysis | Academic and industrial research, education |
| Openness philosophy | Explicitly closed-source, anti-"open code" stance | Closed source by design | Open source by design |

Cats2D occupies a niche that is increasingly rare in scientific computing: a **serious, methodologically rigorous, single-author research code** maintained entirely outside institutional, commercial, or open-source community structures. Its closest historical peers are other bespoke academic transport-phenomena codes from the free-boundary/crystal-growth modeling community (e.g., codes developed in Scriven's, Brown's, or Derby's research groups), several of which Cats2D is directly descended from or contemporaneous with (CFAL, at Minnesota).

---

## 9. Assessment

**Strengths**
- A genuinely fast, low-memory, well-engineered direct solver with credible, quantified performance benchmarks
- A long, verifiable, peer-reviewed scientific track record in a specialized but industrially relevant domain (bulk crystal growth for semiconductor and radiation-detector materials)
- Unusually rigorous and transparent validation methodology, documented in detail
- An integrated mesh/solve/post-process workflow that avoids common multi-tool CFD friction
- Sophisticated continuation, bifurcation, and stability-analysis capabilities not commonly found even in commercial packages

**Limitations and open questions**
- No public source code, license, installer, or pricing information is available; practical accessibility to a general user or organization is unclear to nonexistent
- User documentation (the core manual) is self-acknowledged as outdated, with a promised rewrite of uncertain status
- Development activity, judged by dated public content, appears bursty and driven by one individual's personal research and artistic interests rather than a roadmap or funded program
- No refereed publications are evident after 2018, and there's no visible external (non-Yeckel, non-Goodwin) user community
- The website blends serious technical content with substantial personal, artistic, and opinion material, which — while giving valuable insight into the author's engineering philosophy — makes it a poor substitute for conventional software documentation and complicates due diligence for anyone evaluating the tool for adoption
- The current (2026) state of the project cannot be fully confirmed from the retrieved content alone, since the most recent dated markers found are circa 2019–2020

**Bottom line:** Cats2D is best understood not as an off-the-shelf simulation product but as the enduring personal research instrument of a highly experienced computational transport-phenomena scientist, with real scientific pedigree and a technically impressive solver, but with essentially no public commercial or open-source footprint. Anyone seeking to use, license, or collaborate on Cats2D would need to contact Andrew Yeckel directly via the site's Contact page, as no self-service access path is documented.

---

## 10. Sources

All information in this report was drawn directly from cats2d.com, specifically:
- Home (`/`)
- Overview (`/overview.html`)
- Features (`/features.html`)
- History (`/history.html`)
- Publications (`/publications.html`)
- Solver Performance (`/performance.html`)
- Documentation (`/documentation.html`)
- Research Topics (`/topics.html`)
- Developments/blog (`/developments.html`)

No external sources were used to characterize Cats2D itself; industry context comparisons (§8) reflect general, widely known characteristics of the named commercial and open-source packages and are included for orientation only.

---

> [!NOTE]
> 
> Generated by Claude.ai
>
> Model: Sonet 5
>
> Prompt: Prepare a thorough and detailed technical report on the Cats2D (https://cats2d.com/) by Andrew Yeckel. The technical report must comprehensively address the current state of affairs. It must be exhaustive and wide-ranging. Show output in Markdown format.
