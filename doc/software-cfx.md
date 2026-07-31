# ANSYS/CFX for High-Fidelity Czochralski Crystal Growth Simulation: A Critical Evaluation and Comparison with CrysMAS

**A technical report for researchers and engineers in semiconductor crystal growth, CFD, heat transfer, and multiphysics simulation**

---

## Executive Summary

ANSYS/CFX is a general-purpose, pressure-based, finite-volume (element-based finite-volume, EbFVM) Navier–Stokes solver with mature turbulence, multiphase, radiation, and (via coupling with ANSYS Maxwell/Emag or the Electromagnetics coupling) magnetohydrodynamic modeling capability. It is **not** a crystal-growth code: it has no native representation of a crystal-melt phase boundary as a moving, shape-determined solidification front governed by the Stefan condition, no built-in Czochralski pulling/rotation kinematics, no automatic radiative-enclosure view-factor solver tuned for multi-material, multi-cavity hot-zone assemblies with graphite/insulation/gas domains, and no integrated global (furnace-to-melt) heat-transfer framework of the kind purpose-built codes provide out of the box.

**CrysMAS** (Fraunhofer IISB, Erlangen), by contrast, is a dedicated, three-decades-refined crystal-growth process simulator whose entire architecture — deforming boundary-fitted meshing, quasi-steady interface tracking, radiative enclosure modeling, resistive/inductive heating, magnetic field coupling (including the KRISTMAG® traveling magnetic field approach), and inverse process-control modules — is organized around the physics of melt-growth furnaces (Czochralski, VGF, LEC, gradient-freeze, etc.).

**Bottom line:** ANSYS/CFX *can* be used for high-fidelity **local** (melt-domain) CZ simulation — 3D transient turbulent/oscillatory convection, Marangoni effects, MHD damping, oxygen/dopant transport — and is demonstrably used this way in the peer-reviewed literature. However, essentially every published high-quality CFX-based CZ study either (a) restricts itself to the melt sub-domain and imports thermal/electromagnetic boundary conditions computed by a dedicated global code (frequently CrysMAS itself), or (b) invests substantial in-house development (user Fortran/CEL routines, macros, external coupling scripts) to approximate global-furnace and interface-tracking capabilities CrysMAS provides natively. CFX is therefore best understood as a **high-fidelity local-physics engine** that is complementary to, not a replacement for, a dedicated global process simulator — unless an organization is prepared to make a multi-year investment in custom extension.

---

## 1. Introduction and Scope

### 1.1 The Czochralski process as a simulation problem

The Czochralski (CZ) method pulls a single crystal from a rotating crucible of molten material (silicon, germanium, GaAs, sapphire, oxide crystals, etc.) using a rotating, counter-rotating or co-rotating seed. Faithful simulation must resolve, simultaneously or in a coupled hierarchy:

1. **Global (furnace-scale) heat transfer**: conduction in crucible, susceptor, insulation, and heater; resistive or RF/inductive heat generation; surface-to-surface radiative exchange across a geometrically complex, multi-material enclosure with participating and non-participating surfaces; conjugate coupling to the gas atmosphere.
2. **Melt convection**: buoyancy-driven (natural) convection, Marangoni (thermocapillary) convection at the free melt surface, forced convection from crystal and crucible rotation, and — where applied — magnetohydrodynamic (MHD) damping or stirring from static, rotating, cusp, or traveling magnetic fields.
3. **Melt/crystal interface tracking**: a moving, a priori unknown solid–liquid interface governed by the Stefan (latent-heat) condition, coupled to the pulling rate and thermal field, whose *shape* (concave/convex/flat) is a primary process-quality metric.
4. **Free melt-surface (meniscus) shape**: determined by the Young–Laplace equation with growth-angle and wetting conditions at the triple line, coupling directly to crystal diameter control.
5. **Species/dopant transport**: segregation at the growth interface (effective segregation coefficient, boundary-layer-controlled), oxygen dissolution from the quartz crucible, oxygen/dopant evaporation at the free surface, and incorporation into the growing crystal.
6. **Stress and point-defect fields** in the solidified crystal (thermal stress, dislocation generation, vacancy/interstitial point-defect transport — Voronkov theory) — usually a downstream, decoupled calculation but dependent on the thermal field computed above.
7. **Transients associated with process control**: seeding, shouldering, body growth, tailing, and the slow drift of crucible melt level and immersed heater geometry as the melt is depleted.

No single physics package addresses all seven items natively "out of the box" with the same maturity; the question this report addresses is how far ANSYS/CFX can go, at what cost, relative to a code (CrysMAS) built specifically for this domain.

### 1.2 What "ANSYS/CFX" means in this report

ANSYS/CFX is evaluated as it is typically deployed in this application space:

- **CFX-Solver** (coupled, implicit, pressure-based, element-based finite-volume Navier–Stokes/energy solver) as the core.
- **CFX Expression Language (CEL)** and **User Fortran / User CEL Functions** for custom source terms, boundary conditions, and material properties.
- **ANSYS Meshing / ICEM CFD** for hybrid unstructured/structured mesh generation.
- Optional coupling to **ANSYS Maxwell** (or the legacy Emag solver) via **System Coupling** or one-way field mapping for electromagnetic (induction heating, Lorentz force) problems.
- **Radiation models** built into CFX (Discrete Transfer, Monte Carlo, P1, Rosseland) and the **Surface-to-Surface (S2S)/view-factor** radiation model shared across the ANSYS Workbench (Mechanical/Fluent radiation utilities are sometimes used in hybrid workflows).
- **Immersed/Deforming mesh technology**: ANSYS CFX's Arbitrary Lagrangian–Eulerian (ALE) moving-mesh capability, mesh motion models, and (in recent releases) overset/Chimera meshing.

Where relevant, this report distinguishes CFX from **ANSYS Fluent**, since a meaningful fraction of the published "ANSYS-based" CZ literature in fact uses Fluent rather than CFX; the two share the Workbench environment and many downstream capabilities (radiation, UDFs vs. CEL) but have materially different solver architectures (pressure-based coupled EbFVM in CFX vs. Fluent's cell-centered FVM with both pressure-based and density-based solvers). This distinction matters for anyone benchmarking published results against a CFX-specific implementation.

---

## 2. Physics Coverage: What CFX Provides Natively

### 2.1 Fluid flow and turbulence

CFX's core strength — a robust, well-validated, coupled pressure-velocity solver with a broad turbulence-model library (RANS: $k$–$\varepsilon$, $k$–$\omega$, SST, RSM; scale-resolving: SAS-SST, DES, LES) — is directly applicable to CZ melt convection, which is known experimentally and numerically to transition from steady laminar to oscillatory, and eventually to weakly turbulent regimes as the melt Grashof/Marangoni numbers increase with crucible size. The relevant dimensionless groups are:

$$
Gr = \frac{g\beta\Delta T L^3}{\nu^2}, \qquad
Ma = \frac{\left(\partial\sigma/\partial T\right)\Delta T\, L}{\mu\, \alpha}, \qquad
Ta = \left(\frac{2\Omega L^2}{\nu}\right)^{2}, \qquad
Ha = B L \sqrt{\frac{\sigma_{el}}{\mu}}
$$

where $\sigma$ in the Marangoni number is surface tension (not to be confused with electrical conductivity $\sigma_{el}$ in the Hartmann number). CFX can resolve buoyant, thermocapillary, rotationally forced, and (with EM coupling) magnetically damped regimes across this parameter space, and LES/SAS approaches in CFX have been used successfully in the literature to capture the oscillatory-to-turbulent transition relevant to large-diameter silicon CZ growth.

### 2.2 Conjugate heat transfer

CFX supports fully conjugate heat transfer (CHT) between fluid and solid domains natively, including temperature-dependent thermal conductivity, and this is adequate for coupling melt convection to crucible/crystal conduction in a **local** model. For the **global** furnace problem, however, CFX's CHT must be paired with a working radiation model across a multi-domain, high-temperature, non-participating (or weakly participating) cavity — see §2.4.

### 2.3 Free-surface and interface methods

CFX offers two relevant classes of tool:

- **Free-surface/multiphase methods** (VOF-type homogeneous or inhomogeneous multiphase, level-set-like free-surface treatment) for tracking the melt/ambient-gas interface. These can, with care, represent the deformable meniscus, but native CFX free-surface models are not formulated with the Young–Laplace growth-angle condition that determines the melt meniscus and crystal diameter in CZ growth; that condition must be imposed via custom boundary conditions.
- **Mesh motion / ALE deforming-mesh capability**, which is the mechanism typically used to track the **solid–liquid growth interface** as a moving, deforming internal boundary. CFX's mesh-deformation and remeshing tools were not designed for a boundary whose *position* is itself an unknown determined by a coupled Stefan condition; achieving this in CFX requires an external iterative loop (see §3.1) that repeatedly deforms the mesh, recomputes the thermal field, and adjusts the interface location until the isotherm at the melting point coincides with the mesh boundary — a capability CrysMAS provides as a built-in, purpose-designed algorithm.

### 2.4 Radiative heat transfer

CFX includes the Discrete Transfer Radiation Model (DTRM), Monte Carlo, P1/Rosseland (diffusion-approximation) methods, and — critically for hot-zone furnace geometries — a **Surface-to-Surface (view factor) model** for radiative exchange between opaque, diffuse-gray surfaces in an enclosure. This is functionally the same physical model CrysMAS uses (radiative enclosure method with view factors), so in principle CFX has the *right kind* of radiation model available. In practice:

- CFX's S2S/view-factor tooling is general-purpose and not tuned for the specific geometric idiosyncrasies of CZ hot zones (heat shields, multi-heater graphite assemblies, crucible/susceptor stacks, viewport occlusion by the crystal and pull rod).
- Non-gray, wavelength-dependent, or semi-transparent radiation (relevant for oxide crystals such as sapphire, where the crystal itself transmits substantial radiation) is not handled by the standard opaque-diffuse-gray S2S model and requires either a banded/semi-transparent radiation model (available in ANSYS Fluent's discrete-ordinates implementation with semi-transparent media, but not equivalently mature in CFX) or custom development.
- Meshing a full 3D hot-zone assembly (multiple graphite parts, insulation, crucible, melt, crystal, chamber walls) for accurate view-factor computation is a substantial pre-processing task each time geometry changes — precisely the workflow CrysMAS streamlines with dedicated CAD-to-furnace-model tools.

### 2.5 Electromagnetics / MHD

CFX has no native electromagnetic (induction heating, Lorentz-force) solver. Magnetic and electric field problems — resistive heater current distribution, RF induction heating of the susceptor, static/rotating/cusp/traveling magnetic field interaction with the conducting melt — require coupling to a separate EM solver (ANSYS Maxwell, Emag/Ansoft, or an external MHD code) and one-way or two-way field mapping of the Lorentz force density $\mathbf{J}\times\mathbf{B}$ and Joule heating $|\mathbf{J}|^2/\sigma_{el}$ into CFX as source terms via CEL/User Fortran. This is workable and has been done in the literature (see §5), but it is an assembled multi-code workflow, not a built-in CFX capability, and the coupling fidelity (induced-field feedback on the melt flow, i.e., two-way MHD) is nontrivial to implement correctly.

### 2.6 Species transport and segregation

CFX's scalar transport equations can represent dopant/oxygen concentration fields with prescribed diffusivities, and boundary conditions can approximate a segregation coefficient at the growth interface. However:

- The moving-interface segregation condition — flux balance at a boundary advancing at the pull rate, with an effective segregation coefficient $k_{eff}$ that itself depends on the interfacial melt flow via the Burton–Prim–Slichter relation
$$
k_{eff} = \frac{k_0}{k_0 + (1-k_0)\exp(-v\,\delta/D)}
$$
(where $v$ is the interface velocity, $\delta$ the diffusion boundary-layer thickness, and $D$ the solute diffusivity) — is not a native CFX feature and must be implemented via custom boundary profiles coupled to the (also custom) interface-tracking logic.
- Free-surface evaporation of oxygen/dopant species (relevant to CZ silicon oxygen control) requires a custom flux boundary condition, as demonstrated in the Fluent-based literature using specialized evaporation-flux formulations.

### 2.7 Solidification / latent heat

CFX has no dedicated solidification module analogous to Fluent's built-in "Solidification & Melting" model (enthalpy-porosity method). A latent-heat release/absorption term at the melting isotherm can be implemented via a custom energy source term (CEL/User Fortran) or via an enthalpy-porosity mushy-zone formulation ported into CFX, but this is again custom development rather than a shipped feature.

---

## 3. Gap Analysis: What Requires Custom Development in CFX

| Capability | Native in CFX? | Effort to add |
|---|---|---|
| Turbulent/laminar/oscillatory melt convection | **Yes** | — |
| Conjugate heat transfer, melt ↔ crucible/crystal | **Yes** | — |
| Buoyancy (Boussinesq/full density) | **Yes** | — |
| Marangoni (thermocapillary) BC | Partial — needs custom surface-tension-gradient wall shear BC | Low–Medium |
| Free-surface/meniscus shape with growth-angle condition | Partial — free-surface multiphase exists, growth-angle physics does not | Medium |
| Moving solid–liquid interface with Stefan condition | **No** | High — external iterative mesh-deformation loop |
| Latent heat release at growth front | **No** (no enthalpy-porosity module) | Medium |
| Crystal/crucible pulling and rotation kinematics | Partial — via mesh motion/rotating frames | Medium |
| Radiative enclosure (opaque, diffuse-gray) | **Yes** (S2S/DTRM/Monte Carlo) | Low (setup effort per geometry) |
| Semi-transparent/banded radiation (oxide crystals) | **No** (limited) | High |
| Induction/resistive heating (electromagnetics) | **No** — requires Maxwell/Emag coupling | High |
| Static/rotating/traveling magnetic field MHD (Lorentz force) | **No** — requires EM coupling + CEL source terms | High |
| Two-way MHD (induced field feedback) | **No** | Very High |
| Species transport (dopant, oxygen) | **Yes** (generic scalar transport) | Low |
| Segregation at moving interface ($k_{eff}$, BPS relation) | **No** | Medium–High |
| Free-surface species evaporation flux | **No** | Medium |
| Global furnace model (heater power ↔ set-point inverse solve) | **No** | High |
| Automated furnace CAD → hot-zone mesh workflow | **No** (generic meshing only) | Medium–High |
| Crystal thermal-stress / point-defect post-processing | Partial (via ANSYS Mechanical coupling for stress; no native point-defect module) | Medium–High |
| Transient melt-level/geometry drift over a full pull | **No** built-in process framework | High |

**Reading the table:** the leftmost, lowest-effort rows are exactly the general CFD/CHT/radiation capabilities CFX ships with. The highest-effort rows — moving-interface tracking with the Stefan condition, electromagnetics/MHD coupling, segregation at a moving boundary, and a global inverse-heater-power furnace framework — are the capabilities that define a *dedicated* crystal-growth code, and each is either absent or requires substantial in-house engineering in CFX.

### 3.1 The interface-tracking problem in detail

This deserves elaboration because it is the single largest practical obstacle to "industrial-grade" CZ simulation in CFX. A dedicated code solves the moving-boundary problem as an integral part of its algorithm: the melt/crystal interface position is an unknown solved simultaneously (or in a tightly coupled outer iteration) with the temperature field, subject to
$$
k_s \left.\frac{\partial T_s}{\partial n}\right|_{\Gamma} - k_l \left.\frac{\partial T_l}{\partial n}\right|_{\Gamma} = \rho_s\, L_f\, v_n
$$
where $\Gamma$ is the interface, $v_n$ its normal velocity (linked to the pulling rate in quasi-steady growth), $L_f$ the latent heat of fusion, and $k_s,k_l$ the solid/liquid thermal conductivities. CrysMAS implements this as a built-in deforming-grid or interface-tracking algorithm with a quasi-Newton solution strategy specifically tuned for this class of problem.

In CFX, achieving the same result requires building an **external control loop** around the solver: (1) guess an interface shape and generate/deform a boundary-fitted mesh to it; (2) solve the coupled thermal/flow field; (3) evaluate the Stefan-condition residual along the interface; (4) update the interface shape (e.g., via a Newton or relaxation scheme implemented in a scripting layer — Python/Perl driving CFX in batch mode — or via CFX's own mesh-motion/User Fortran hooks); (5) re-mesh or deform and repeat to convergence. This is a legitimate and published approach, but it is bespoke software engineering layered on top of CFX, not a feature CFX provides.

---

## 4. CrysMAS: Capability Summary

CrysMAS (Crystal growth Modeling and Analysis System) is developed and maintained by the Crystal Growth Laboratory of the Fraunhofer Institute for Integrated Systems and Device Technology (IISB), Erlangen, and represents the merger of two earlier IISB codes, STHAMAS and CrysVUn, into a unified package. It is a finite-volume code built specifically for high-temperature crystal-growth furnace simulation, with the following native characteristics documented in the peer-reviewed literature:

- **Finite-volume method on unstructured (triangular in 2D axisymmetric; extendable) grids**, with a quasi-Newton iterative solution method for the coupled global energy equation, well suited to strongly nonlinear, radiation-dominated high-temperature systems.
- **Native radiative enclosure modeling** using the view-factor/enclosure method across arbitrary multi-material furnace geometries — this is a first-class, purpose-built capability rather than a generic tool requiring extensive per-case setup.
- **Global (furnace-scale) heat transfer**, coupling heater elements (resistive and, via extensions, inductive), insulation, crucible, susceptor, melt, crystal, and gas/chamber domains in one model, with the capability to solve the **inverse problem**: given specified set-point temperatures, solve for the heater power(s) needed to achieve them — a capability directly useful for process design and control that has no native CFX counterpart.
- **Melt-flow, heat transfer, and phase-change computation within the crystal-growth domain**, including convection, conduction, and solidification/melting at a tracked interface, coupled to the global furnace solution to provide realistic thermal boundary conditions.
- **Electromagnetic/magnetic field coupling**, including the KRISTMAG® approach for traveling magnetic fields (TMFs) generated by heater-magnet modules (HMMs), used to compute Lorentz force densities that are then applied to melt-flow calculations — either within CrysMAS itself for global/quasi-2D analysis, or exported as boundary/source data to a local 3D solver (including, in published work, CFX) for detailed melt-flow computation.
- **Segregation and dopant/impurity transport modeling**, tuned to the moving-interface, slow-growth-rate regime characteristic of bulk crystal growth (VGF, EDG, CZ), including anomalous segregation effects reported in CZT growth studies.
- **Applicability across growth methods**, not just CZ: VGF, LEC, gradient-freeze, and related Bridgman-type methods share the underlying global-furnace/interface-tracking architecture.
- **Validation pedigree**: CrysMAS and its predecessor codes have been validated against decades of IISB's own experimental crystal-growth campaigns (documented extensively in the Müller/Friedrich IISB literature, including the review by Friedrich (2020) tracing four decades of IISB crystal-growth modeling and its industrial licensing history) and used by multiple external research groups and companies (e.g., University of Minnesota/Derby group for CZT/EDG modeling, University of Timisoara collaboration on VGF/LEC).

### 4.1 What CrysMAS does *not* natively provide at CFX's level of sophistication

To be fair to both codes: CrysMAS's turbulence modeling, transient scale-resolving flow physics (LES/SAS-type resolution of oscillatory/turbulent melt convection), and general-purpose multiphysics flexibility (arbitrary UDF-style extensibility, broad multiphase modeling, FSI coupling to structural mechanics) are narrower than CFX's. Where a research question is specifically about high-Reynolds-number transient melt turbulence, 3D non-axisymmetric flow structures, or coupling to structural/stress solvers beyond simple thermal-stress postprocessing, CFX's general CFD maturity is an advantage that a domain-specific but narrower code cannot fully match without commensurate development effort of its own.

---

## 5. Comparative Analysis

| Dimension | ANSYS/CFX | CrysMAS |
|---|---|---|
| **Primary design intent** | General-purpose industrial CFD/CHT | Dedicated crystal-growth furnace/process simulation |
| **Turbulence modeling** | Extensive (RANS through LES/DES/SAS) | Limited/basic relative to CFX |
| **Global furnace radiative heat transfer** | Available (S2S/DTRM/Monte Carlo) but generic, setup-intensive | Native, purpose-built, workflow-optimized |
| **Solid–liquid interface tracking (Stefan condition)** | Not native — requires custom external loop | Native, core architectural feature |
| **Inverse heater-power solve for set-point control** | Not available | Native |
| **Electromagnetics (induction heating, static/rotating/traveling B-fields)** | Requires external EM solver (Maxwell) + custom coupling | Native for key cases (KRISTMAG® TMF), integrated |
| **Segregation at moving interface (BPS-type)** | Not native — custom implementation | Native, tuned for slow-growth regimes |
| **Free-surface/meniscus with growth-angle physics** | Not native — custom BC development | Native to CZ-type modeling |
| **Semi-transparent/banded radiation (oxide crystals)** | Weak/absent | Present in relevant IISB-domain applications |
| **Multi-method applicability (CZ, VGF, LEC, gradient freeze)** | Depends entirely on custom setup per method | Native, shared architecture across methods |
| **Numerical method** | Coupled, implicit, element-based FVM (EbFVM), pressure-based | Finite volume on unstructured grids, quasi-Newton for strongly nonlinear coupled system |
| **Meshing workflow for hot-zone geometry** | Generic ANSYS Meshing/ICEM; substantial manual effort per geometry change | Streamlined, purpose-built for furnace/crucible/crystal assemblies |
| **Validation status (public literature)** | Validated per-study; no unified crystal-growth validation suite | Validated across decades of IISB experimental campaigns and multiple external institutions |
| **Industrial readiness for CZ (out of the box)** | Low–Medium (requires substantial extension) | High (designed for this) |
| **Scalability (parallel HPC)** | Strong — mature MPI-parallel solver, widely used at scale in industrial CFD | More limited; scale of published CrysMAS studies is typically single-workstation/small-cluster, consistent with quasi-steady/2D-3D hybrid workflows rather than large-scale transient turbulence |
| **Extensibility / general multiphysics** | High (CEL, User Fortran, System Coupling to structural/EM solvers, broad ANSYS ecosystem) | Narrower — extension typically means collaboration with IISB or coupling to external codes (e.g., Cats2D for ampoule-scale FEM) |
| **Usability for crystal-growth-specific workflows** | Requires domain expertise to configure correctly; steep learning curve for this application | Designed for crystal-growth engineers; lower barrier for furnace-scale process studies |
| **Licensing / ecosystem** | Broad commercial CFD license, large user/support base, frequent releases | Specialist license from Fraunhofer IISB, smaller user base, tied to IISB's development roadmap |
| **Cost structure** | Commercial CFD suite pricing (general-purpose, not crystal-growth-specific) | Specialist software licensing, typically with domain-expert support from IISB |

### 5.1 How the two are actually combined in published practice

The literature search underlying this report converges on a consistent pattern that is itself the strongest evidence for the comparative assessment above: **published high-fidelity CZ studies that use CFX for melt-flow physics routinely use CrysMAS (or a comparable dedicated code, e.g., CGSim) to generate the global thermal and electromagnetic boundary conditions that CFX then consumes.** A representative and directly on-topic example: 3D melt-flow calculations for square-shaped silicon CZ growth under a traveling magnetic field were performed in ANSYS-CFX, but the furnace-scale temperature field supplying thermal boundary conditions to the CFX local model — and the Lorentz-force densities from the KRISTMAG® traveling-field approach — were computed beforehand using axisymmetric CrysMAS calculations. This is not an isolated case; it reflects a broader, sensible division of labor described across the CZ modeling literature: dedicated codes (CrysMAS, CGSim, STHAMAS) handle 2D/axisymmetric global furnace and electromagnetic computations, while general CFD codes (CFX, Fluent) are reserved for 3D transient/turbulent local melt-flow physics that dedicated codes handle more coarsely.

This pattern has two important implications:

1. It validates the core finding of this report: CFX is not typically used as a *standalone* CZ simulation environment in serious published work; it is used as a *local high-fidelity flow solver downstream of* a global process code.
2. It suggests that the most cost-effective "extension strategy" for an organization wanting CFX-level melt-flow fidelity is not to reimplement CrysMAS's global/interface-tracking machinery inside CFX, but to build (or license) a coupling workflow that imports boundary conditions from a dedicated global code — precisely the workflow already demonstrated in the literature.

---

## 6. Effort Assessment: Building a CFX-Based CZ Environment Approaching CrysMAS

For an organization aiming to reach CrysMAS-equivalent CZ modeling capability using ANSYS/CFX as the foundation, the realistic development program includes:

1. **Global furnace radiation/CHT module** (Medium–High effort): configure and validate S2S/enclosure radiation across representative hot-zone geometries; build a reusable, parameterized meshing workflow (likely via ANSYS Workbench journaling/scripting or an external meshing tool) so that geometry changes do not require full manual remeshing each time.
2. **Electromagnetics coupling** (High effort): establish a robust one-way or two-way coupling to ANSYS Maxwell (or an external MHD/induction-heating code) for resistive/inductive heating and Lorentz-force computation; validate against known analytical or experimental cases (e.g., cusp/rotating/traveling field benchmarks) before trusting results.
3. **Moving-interface tracking framework** (High effort): implement an external control loop (scripted batch-mode CFX runs, or User Fortran-driven mesh deformation) that solves the Stefan condition at the melt/crystal boundary; this is likely the single largest and riskiest development item, since numerical robustness of interface-tracking algorithms is itself a research topic in the crystal-growth CFD literature.
4. **Latent heat / mushy-zone treatment** (Medium effort): implement enthalpy-porosity or equivalent source-term treatment via CEL/User Fortran.
5. **Free-surface meniscus and growth-angle physics** (Medium effort): custom boundary conditions coupling the free-surface shape to the growth angle and crystal-diameter control logic.
6. **Segregation/species transport at the moving interface** (Medium–High effort): custom flux boundary conditions implementing BPS-type effective segregation, plus free-surface evaporation flux models for oxygen/dopant control in CZ silicon.
7. **Inverse process-control capability** (High effort, often deprioritized): CrysMAS's ability to solve for heater power given target set-points is a distinct capability class (an outer optimization/inverse-problem loop around the forward solver) not typically prioritized in general CFD workflows; without it, CFX-based studies are limited to *forward* (specified heater power/temperature) analysis, which is materially less useful for process design.
8. **Validation program**: because none of the above are shipped, validated capabilities, each requires its own validation against experiment or against results from an established code (frequently CrysMAS itself, per the pattern in §5.1) before the combined framework can be trusted for industrial decision-making.

**Realistic estimate:** for a team with strong CFD, numerical-methods, and scientific-programming expertise (the profile typical of a HPC/CFD specialist with FEM/parallel-solver background), building a CFX-based CZ environment that covers items 1–6 above to a publication-quality standard is a **multi-year effort** (order of 2–4 person-years, depending on scope and how much can be adapted from the existing published literature's methods rather than developed from scratch), even before item 7 (inverse control) — which is arguably not worth reimplementing at all given CrysMAS's existing maturity in this specific area. This is consistent with the observed practice (§5.1) of pairing CFX with CrysMAS rather than replacing it.

---

## 7. Recommendations

### 7.1 For academic/research groups

- **Use CFX (or Fluent) for what it is genuinely good at**: 3D transient, turbulence-resolving melt-flow studies, MHD damping/stirring investigations (with EM fields imported from Maxwell or a dedicated MHD code), and detailed local free-surface/Marangoni studies — ideally as a downstream, high-fidelity companion to a global model rather than a replacement for one.
- **Do not attempt to reimplement CrysMAS's global-furnace and interface-tracking machinery from scratch** unless the research question is specifically about numerical methods for moving-boundary problems; the effort is disproportionate to the likely publishable novelty, and the dedicated codes already provide validated tools for this purpose.
- **Where available, obtain a CrysMAS license/collaboration with Fraunhofer IISB** (or an equivalent global-model code such as CGSim) to generate boundary conditions, following the demonstrated literature workflow.
- Where the crystal is optically semi-transparent (oxides such as sapphire, YAG, etc.), evaluate whether ANSYS Fluent's semi-transparent/banded radiation models better serve the need than CFX's more limited native radiation options, or budget for custom development regardless of which ANSYS product is chosen.

### 7.2 For industrial CZ process-engineering teams

- If the organization already has an ANSYS enterprise license and in-house CFD expertise, CFX is a reasonable platform for **targeted, local melt-flow studies** (e.g., evaluating a new magnet configuration's effect on interface shape, or investigating the onset of flow instabilities as crucible diameter scales up) — provided global thermal boundary conditions are sourced from a validated external model.
- For **process design, heater-power set-point determination, and rapid geometry/hot-zone iteration** — the bread-and-butter of industrial CZ furnace engineering — a dedicated code (CrysMAS, CGSim, or equivalent) is the more cost-effective and lower-risk choice; CFX's generality is a liability here, not an asset, because it requires re-deriving capabilities the dedicated tools ship with.
- A **hybrid workflow** (dedicated code for global/inverse/interface-tracking, CFX for selected high-fidelity local 3D transient studies) is the pattern best supported by the published literature and is recommended as the default architecture rather than an all-CFX or all-CrysMAS approach.
- Budget realistically: treat any CFX-based CZ capability beyond basic local melt-flow analysis as a multi-year software-engineering investment (§6), not a configuration exercise, and weight this against CrysMAS licensing costs plus Fraunhofer IISB collaboration/support.

### 7.3 General

- Maintain awareness that "ANSYS-based CZ simulation" in the literature is not monolithic: Fluent and CFX differ in solver architecture and in the maturity of specific features (e.g., Fluent's built-in solidification/melting model, semi-transparent radiation options), so conclusions from Fluent-based studies should not be assumed to transfer directly to CFX without verification.
- Any claim of CFX "industrial-grade CZ simulation capability" should be scrutinized for whether it in fact describes a **local melt-flow model receiving externally computed boundary conditions**, since this is the dominant pattern in credible published work, not a standalone global CZ simulation performed entirely within CFX.

---

## 8. Key References

1. Kirpo, M. (2013). *Global simulation of the Czochralski silicon crystal growth in ANSYS FLUENT.* Journal of Crystal Growth, 371, 60–69. https://doi.org/10.1016/j.jcrysgro.2013.02.001 — Demonstrates global 2D axisymmetric CZ furnace modeling in a general-purpose ANSYS CFD code, explicitly situating it against dedicated codes CGSim and CrysMAS/STHAMAS.
2. Vizman, D., et al. *Numerical simulation of Czochralski crystal growth under the influence of a traveling magnetic field generated by an internal heater-magnet module (HMM).* — 3D melt-flow calculations performed in ANSYS-CFX, with furnace-scale thermal field and KRISTMAG® Lorentz-force densities computed beforehand in CrysMAS — the key literature example of the CFX/CrysMAS division of labor described in §5.1.
3. Sabanskis, A., et al. *Modelling of a magnetohydrodynamics free surface problem arising in Czochralski crystal growth.* Magnetohydrodynamics / related journal. https://doi.org/10.1080/13873950802551542 — Mathematical formulation of the coupled free-surface, magnetic-field, rotation, and buoyancy problem in CZ growth; relevant to understanding what a fully coupled MHD free-surface model requires beyond CFX's native capability.
4. Derby, J.J., and co-authors (Yeckel, Salk, et al.). Multiple works on CrysMAS-based global modeling coupled to Cats2D ampoule-scale finite-element modeling for VGF/EDG growth of CZT and related materials, including *Control of thermal conditions during crystal growth by inverse modeling* and *Modeling the growth of CZT by the EDG process* — describe CrysMAS's finite-volume, quasi-Newton global solution method, its inverse heater-power capability, and its validated application across multiple research institutions.
5. Friedrich, J. (2020). *Erlangen — An Important Center of Crystal Growth and Epitaxy: Major Scientific Results and Technological Solutions of the Last Four Decades.* Crystal Research and Technology. https://doi.org/10.1002/crat.201900053 — Historical and technical review tracing the development of STHAMAS, CrysVUn, and their merger into CrysMAS at Fraunhofer IISB, including their industrial licensing history.
6. *Development and validation of a thermal simulation for the Czochralski crystal growth process using model experiments.* ScienceDirect, 2022. https://doi.org/10.1016/j.jcrysgro.2022.126676 — References the CrysMAS manual and situates CrysMAS-based thermal modeling against experimental validation campaigns; useful bibliography for global CZ thermal-field validation literature (Müller & Friedrich 2004; Krauze et al. 2010 on LES applicability for CZ Si with traveling magnetic fields).
7. Fraunhofer IISB, *CrysMAS Manual and Equipment Simulation resources.* https://download.iisb.fraunhofer.de/downloads/Manual/index.html and https://www.iisb.fraunhofer.de/en/research_areas/materials/equipment_simulation.html — Primary vendor documentation for CrysMAS capabilities.
8. *3D computation of oxygen transport in Czochralski crystal growth of silicon considering evaporation.* Journal of Crystal Growth. https://doi.org/10.1016/j.jcrysgro.2006.10.190 — Demonstrates the custom free-surface evaporation flux formulation needed for oxygen-transport modeling in a general CFD code, illustrating the "custom development" effort category discussed in §2.6 and §3.

---

## Appendix A: Governing Equations Reference (Melt-Domain Local Model)

**Continuity, momentum (Boussinesq buoyancy), and energy in the melt**, in a rotating reference frame at angular velocity $\boldsymbol{\Omega}$:

$$
\nabla \cdot \mathbf{u} = 0
$$

$$
\rho_0\left(\frac{\partial \mathbf{u}}{\partial t} + (\mathbf{u}\cdot\nabla)\mathbf{u} + 2\boldsymbol{\Omega}\times\mathbf{u} + \boldsymbol{\Omega}\times(\boldsymbol{\Omega}\times\mathbf{r})\right) = -\nabla p + \mu \nabla^2 \mathbf{u} + \rho_0 \beta (T - T_0)\, \mathbf{g} + \mathbf{J}\times\mathbf{B}
$$

$$
\rho_0 c_p \left(\frac{\partial T}{\partial t} + \mathbf{u}\cdot\nabla T\right) = k \nabla^2 T
$$

**Marangoni boundary condition** at the free melt surface ($n$ normal, $s$ tangential):

$$
\mu \left.\frac{\partial u_s}{\partial n}\right|_{surface} = \frac{\partial \sigma}{\partial T}\, \frac{\partial T}{\partial s}
$$

**Stefan (interface energy balance) condition** at the melt/crystal boundary $\Gamma$, with $v_n$ the normal growth velocity:

$$
k_s \left.\frac{\partial T_s}{\partial n}\right|_{\Gamma} - k_l \left.\frac{\partial T_l}{\partial n}\right|_{\Gamma} = \rho_s L_f v_n
$$

**Segregation at the moving interface** (Burton–Prim–Slichter effective segregation coefficient):

$$
k_{eff} = \frac{k_0}{k_0 + (1-k_0)\, \exp\!\left(-\dfrac{v\,\delta}{D}\right)}
$$

These equations define the physics an ANSYS/CFX-based CZ model must ultimately reproduce; §2–§3 of this report assess, term by term, which are native and which require custom implementation.

---

> [!NOTE]
> 
> Generated by Claude.ai
>
> Model: Sonet 5
>
> Prompt: Write a comprehensive, technically rigorous report evaluating the suitability of ANSYS/CFX for high-fidelity numerical simulation of the Czochralski (CZ) crystal growth process. The report should critically assess ANSYS/CFX's capabilities, limitations, required extensions, and practical implementation challenges. It should also provide a detailed comparison with CrysMAS, the dedicated crystal-growth simulation software developed by the Fraunhofer Institute for Integrated Systems and Device Technology (Fraunhofer IISB). The report should be written for researchers and engineers involved in semiconductor crystal growth, computational fluid dynamics (CFD), heat transfer, and multiphysics simulation.
> Objectives
> Determine whether ANSYS/CFX can serve as a viable platform for industrial-grade CZ crystal growth simulation.
> Identify which physical phenomena can be modeled using standard ANSYS/CFX capabilities and which require custom development.
> Compare ANSYS/CFX with CrysMAS regarding physics coverage, numerical methods, validation status, industrial readiness, scalability, extensibility, and usability.
> Assess the effort required to build a CZ simulation environment in ANSYS/CFX that approaches the capabilities of CrysMAS.
> Provide recommendations for research, academic, and industrial use cases.
> Provide key references. Show the output in Markdown format.
