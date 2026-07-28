# Development Roadmap: High-Fidelity Physics-Based Model of InP Czochralski / LEC Crystal Growth

## 0. Purpose, Scope, and Design Philosophy

This roadmap defines the technical program required to build an industrial-grade, physics-based simulation tool for indium phosphide (InP) single-crystal growth by the Czochralski (CZ) and Liquid-Encapsulated Czochralski (LEC) methods, starting from first-principles continuum physics and culminating in a validated, extensible, production-quality software system.

InP is chosen as the target material because it combines several features that make it one of the hardest CZ/LEC systems to model correctly:

- High equilibrium dissociation pressure of phosphorus at the melting point (~1062°C), requiring either high inert overpressure or a B$_2$O$_3$ encapsulant layer (LEC), which introduces a third phase and a complex triple-phase-line physics problem.
- Low critical resolved shear stress and low thermal conductivity relative to Si and GaAs, making InP extremely susceptible to thermally-induced dislocation generation — dislocation density is often the primary industrial figure of merit, not just macroscopic shape or diameter control.
- Strong dependence of electrical and optical properties on point-defect and dopant distribution, requiring accurate segregation and constitutional supercooling modelling for semi-insulating (Fe-doped) and conducting (S, Sn, Zn-doped) InP.
- Semi-transparency of the melt and crystal to thermal radiation at growth temperatures, requiring radiative transfer treatment beyond simple surface-to-surface view-factor models in some regimes.
- Industrially relevant magnetic damping (MCZ) and accelerated crucible rotation technique (ACRT) variants that couple magnetohydrodynamics or time-dependent forcing into the melt flow.

The roadmap is organized as a layered program: physics foundations → single-physics numerical solvers → coupled multiphysics solver → free-boundary/interface tracking → defect and dopant transport → global furnace-scale coupling → validation program → software engineering and productization → extensibility to other materials/processes. Each layer specifies deliverables, numerical methods, key risks, and validation criteria. The document assumes a multi-year effort (typically estimated at 4–7 years to reach industrial-grade maturity for a team of 4–10 FTE including HPC engineers, applied mathematicians, and crystal growth physicists), phased into overlapping work packages (WPs).

Guiding principles:

1. **Physical completeness before speed.** Every simplifying assumption must be traceable, quantified, and reversible — the architecture should never make an approximation irreversible.
2. **Verification and validation (V&V) as first-class deliverables**, not an afterthought — method of manufactured solutions (MMS), code-to-code benchmarks, and experiment-to-code comparisons are budgeted from day one.
3. **Numerical robustness over elegance** — free-boundary, strongly coupled, high-Prandtl-number, low-diffusivity systems are numerically brutal; robustness (monotonicity, conservation, mesh quality preservation) takes priority over higher-order accuracy where the two conflict.
4. **Extensibility by construction** — material properties, process variants (CZ, LEC, MCZ, VCZ, ACRT), and geometry must be data-driven, not hard-coded, so the same core solver later supports GaAs, GaSb, CdTe, Ge, or Si without re-architecture.

---

## 1. Scientific Foundations: Governing Physics

### WP1.1 — Thermal-Fluid Governing Equations in the Melt

The InP melt is modeled as an incompressible (Boussinesq or low-Mach) Newtonian fluid in a rotating, deforming domain. The core governing system:

**Continuity:**
$$
\nabla \cdot \mathbf{u} = 0
$$

**Momentum (rotating frame, Boussinesq buoyancy):**
$$
\rho_0 \left( \frac{\partial \mathbf{u}}{\partial t} + (\mathbf{u}\cdot\nabla)\mathbf{u} + 2\boldsymbol{\Omega}\times\mathbf{u} + \boldsymbol{\Omega}\times(\boldsymbol{\Omega}\times\mathbf{r}) \right) = -\nabla p + \mu \nabla^2 \mathbf{u} + \rho_0 \mathbf{g}\,\beta_T (T - T_0) + \mathbf{F}_{\ast}
$$

where $\mathbf{F}_{\ast}$ is a placeholder for additional body forces (Lorentz force for MCZ, solutal buoyancy term $\beta_C(C-C_0)$ for dopant-driven convection).

**Energy (melt):**
$$
\rho_0 c_p \left( \frac{\partial T}{\partial t} + \mathbf{u}\cdot\nabla T \right) = \nabla\cdot(k_\ell \nabla T) - \nabla\cdot \mathbf{q}_{rad}
$$

**Energy (crystal, static frame or crystal-fixed rotating frame, with pulling):**
$$
\rho_s c_{p,s} \left( \frac{\partial T}{\partial t} + V_{pull}\frac{\partial T}{\partial z} \right) = \nabla\cdot(k_s(T) \nabla T) - \nabla\cdot \mathbf{q}_{rad}
$$

Deliverables:
- Formal derivation document (internal technical note) establishing every term, every non-dimensional group (Grashof $Gr$, Marangoni $Ma$, Prandtl $Pr$, Reynolds $Re_\Omega$ for crucible/crystal rotation, Ekman number $Ek$, Rayleigh $Ra$), and the regime map for InP-relevant operating conditions.
- Explicit statement of Boussinesq validity limits for InP (density variation across the melt temperature range) and decision on when a low-Mach / variable-density formulation is required instead.
- Reference property database (see WP1.5) feeding every coefficient above as $T$-dependent, not constant.

Key references:
- Derby, J.J. & Brown, R.A., "Thermal-capillary analysis of Czochralski and liquid encapsulated Czochralski crystal growth," *J. Cryst. Growth* 74 (1986) 605–624.
- Kobayashi, N., "Computer simulation of the melt flow during Czochralski growth," *J. Cryst. Growth* 43 (1978) 357–363.
- Langlois, W.E., "Buoyancy-driven flows in crystal-growth melts," *Annu. Rev. Fluid Mech.* 17 (1985) 191–215.

### WP1.2 — Free/Moving Boundaries and Interface Physics

Four coupled free boundaries define the CZ/LEC domain:

1. **Melt–crystal interface** $\Gamma_{sl}(t)$ — determined by the Stefan condition:
$$
k_s \nabla T_s \cdot \mathbf{n} - k_\ell \nabla T_\ell \cdot \mathbf{n} = \rho_s L \, (V_{int}\cdot\mathbf{n})
$$
with $T = T_m$ (or a curvature/kinetics-corrected melting point, see WP1.3) on $\Gamma_{sl}$.

2. **Melt–ambient (or melt–encapsulant, in LEC) free surface** $\Gamma_{lv}$ — governed by the Young–Laplace normal-stress balance with Marangoni (thermocapillary) tangential stress:
$$
p_\ell - p_{amb} = \sigma\,\kappa, \qquad \mu \frac{\partial u_t}{\partial n}\Big|_{\Gamma_{lv}} = \frac{d\sigma}{dT}\nabla_t T
$$

3. **Crystal side surface** (with radiative and possibly convective boundary condition) and its coupling to the meniscus at the triple line.

4. **Encapsulant–gas interface and encapsulant–crystal interface** (LEC only), each with its own surface tension and triple-line physics, and the B$_2$O$_3$ layer's own internal convection (WP7).

Deliverables:
- Formal treatment of the triple-phase line (crystal–melt–encapsulant/ambient) including growth-angle boundary condition (fixed growth angle for InP, ~11–14° depending on facet/crystallographic orientation) as the physical closure for diameter control, per Bardsley/Boucher meniscus theory.
- Quasi-steady meniscus (thin-film / lubrication) approximation for fast-convergence diameter-control coupling, alongside a fully resolved free-surface option for research-grade runs.
- Explicit interface-tracking numerical strategy decision (see WP3): ALE deforming mesh vs. level-set vs. phase-field, with documented trade-offs specifically for the CZ topology (thin meniscus film, large aspect ratio changes over a growth run).

Key references:
- Bardsley, W., Green, G.W., Holliday, C.H., Hurle, D.T.J., "Automatic control of Czochralski crystal growth," *J. Cryst. Growth* 16 (1972) 277–279.
- Boucher, E.A., Evans, M.J.B., "Pendent drop profiles and related capillary phenomena," *Proc. R. Soc. Lond. A* 346 (1975) 349–374.
- Surek, T., Chalmers, B., "The growth of shaped crystals from the melt," *J. Cryst. Growth* 29 (1975) 1–11 (growth-angle concept).

### WP1.3 — Interface Kinetics, Undercooling, and Facetting

Pure Stefan-condition models assume local equilibrium at $\Gamma_{sl}$. For InP, two refinements are required for predictive accuracy:

- **Kinetic undercooling**: $T_m^{eff} = T_m - \Delta T_{kin}(V_{int})$, generally negligible for CZ growth rates but must be quantified, not assumed away, since InP has a lower melting entropy of fusion than Si and can show measurable interface kinetics at high pull rates.
- **Facet formation on {111} planes**: InP crystals commonly nucleate facets at the periphery of an otherwise rounded interface. Facet growth follows a different (defect-nucleation-limited, Voronkov-type or 2D-nucleation) kinetic law than the rounded interface, producing a locally flat interface segment with a distinct dopant segregation behavior ("facet striations"). This is a first-order effect for dopant homogeneity modelling in heavily doped InP and must be included as a switchable sub-model, not deferred to "future work," given its practical importance.

Deliverables:
- Literature-calibrated facet kinetic law and criterion for facet nucleation/edge position as a function of local interface undercooling and orientation.
- Sensitivity study quantifying the impact of neglecting facetting on predicted radial dopant segregation, to justify its priority ranking against other WPs.

Key references:
- Voronkov, V.V., "Standard model for defect formation in silicon growth," *J. Cryst. Growth* 335 (2011) — for the interface-kinetics/point-defect coupling method (methodologically transferable).
- Fujiwara, K. et al., "Facet formation on Czochralski-grown GaAs and InP," *J. Cryst. Growth* 208 (2000) 41–48.
- Hurle, D.T.J. (ed.), *Handbook of Crystal Growth, Vol. 2: Bulk Crystal Growth*, North-Holland (1994) — Ch. on interface kinetics.

### WP1.4 — Radiative Heat Transfer

InP melt and crystal are semi-transparent in parts of the relevant spectral range at growth temperature, unlike opaque-solid assumptions valid for many metals. Two-tier radiation strategy:

- **Tier 1 (furnace/global scale)**: surface-to-surface radiative exchange with view factors between crucible, heater, insulation, encapsulant surface, crystal surface, and chamber walls, including specular/diffuse reflectivity of graphite/quartz components and (for LEC) the B$_2$O$_3$ encapsulant's own radiative properties.
- **Tier 2 (crystal-scale semi-transparency)**: participating-medium radiative transfer within the crystal, coupled to the energy equation via a radiative divergence term. Options ranked by cost/accuracy: Rosseland diffusion approximation (cheap, valid only optically thick), $P_1$/spherical-harmonics approximation, discrete-ordinates method (DOM), or full Monte Carlo ray tracing for verification benchmarks.

Deliverables:
- Spectral absorption coefficient database for InP melt and solid as a function of $T$ and dopant/free-carrier concentration (free-carrier absorption is significant for heavily doped, e.g., Sn- or S-doped, conducting InP — this changes effective radiative conductivity and therefore interface shape, and must not be treated as a Si/GaAs-generic constant).
- Verification of the chosen participating-media method against Monte Carlo reference solutions on canonical geometries before production use.

Key references:
- Modest, M.F., *Radiative Heat Transfer*, 3rd ed., Academic Press (2013).
- Lu, C.W., Chen, J.C., "Effect of crystal rotation on the growth interface shape of Czochralski-grown crystals under radiative and semi-transparent conditions," *J. Cryst. Growth* 266 (2004).
- Kakimoto, K. et al., work on radiative transfer in Si/GaAs CZ growth (methodological basis, adapted for InP optical data) — see *Prog. Cryst. Growth Charact. Mater.* review articles.

### WP1.5 — Materials Property Database

A dedicated, versioned, uncertainty-quantified property database is a standalone deliverable, not a side task, because model accuracy is bounded above by property-data accuracy regardless of numerical fidelity:

Required properties (all as functions of $T$, and where relevant, dopant concentration and stoichiometry deviation), each with source, method, and stated uncertainty:
- Melt: density $\rho_\ell(T)$, dynamic viscosity $\mu(T)$, thermal conductivity $k_\ell(T)$, specific heat $c_{p,\ell}(T)$, thermal expansion $\beta_T$, solutal expansion $\beta_C$ (per dopant species), surface tension $\sigma(T)$ and $d\sigma/dT$, electrical conductivity (for MCZ Lorentz-force modelling).
- Solid: $k_s(T)$ down to room temperature (needed for post-growth cooldown/stress modelling), $c_{p,s}(T)$, $\rho_s(T)$, elastic constants $C_{ij}(T)$, thermal expansion coefficient $\alpha(T)$, critical resolved shear stress (CRSS) $\tau_c(T)$ and its strain-rate dependence.
- Interface: latent heat of fusion $L$, equilibrium segregation coefficients $k_0$ for each relevant dopant (S, Sn, Zn, Fe, Te) and for the native point defects (In/P vacancies, antisites), liquidus/solidus data near the In-rich and P-rich sides (In–P binary phase diagram) to capture congruent-melting-point sensitivity.
- Encapsulant (B$_2$O$_3$): viscosity (strongly $T$-dependent, several orders of magnitude over the relevant range), density, thermal conductivity, surface/interfacial tensions with InP melt and with the ambient gas, water-content dependence (industrially significant and often under-documented).
- P equilibrium vapor pressure over InP melt as a function of $T$ and melt stoichiometry — essential for LEC overpressure design and for any model of dissociation/mass-loss at exposed melt surfaces.

Deliverables:
- Property database as versioned, machine-readable (JSON/HDF5) files with full provenance metadata, decoupled from solver code (data-driven architecture principle from §0).
- Documented gaps and recommended targeted experimental/DFT measurement campaigns (WP9) for properties with high uncertainty or contradictory literature values (notably: high-temperature $k_\ell$ of InP melt, and $B_2O_3$ viscosity-water-content relation).

Key references:
- Ohring, M. / Landolt-Börnstein series, *Semiconductors: Physics of Group IV Elements and III-V Compounds*, Vol. III/17a (InP data compilation).
- Nishizawa, J., "Semi-insulating InP," and related property compilations in the *Handbook of Semiconductor Technology*.
- Bachmann, K.J. et al., "Preparation of InP," in *Semiconductors and Semimetals* Vol. 20 — thermophysical and phase-diagram data.
- Van den Bogaert, N., Dupret, F., "Dynamic global simulation of the Czochralski process," parts I & II, *J. Cryst. Growth* 171 (1997) 65–93 — methodology for property-uncertainty propagation.
## 2. Dopant, Stoichiometry, and Point-Defect Transport

### WP2.1 — Macroscopic Dopant Segregation

Convection-diffusion transport of each dopant species $C_i$ in the melt:
$$
\frac{\partial C_i}{\partial t} + \mathbf{u}\cdot\nabla C_i = D_i \nabla^2 C_i
$$
with the interfacial segregation boundary condition (effective segregation coefficient $k_{eff}$ from Burton–Prim–Slichter theory, itself a function of local growth rate and boundary-layer thickness, both outputs of the resolved melt flow):
$$
k_{eff} = \frac{k_0}{k_0 + (1-k_0)\exp(-V_{int}\delta/D_i)}
$$

Deliverables:
- Fully resolved (not BPS-parameterized) boundary-layer segregation as the production model, since the whole point of a high-fidelity tool is to predict $\delta$ from the flow field rather than assume it; BPS retained only as a fast reduced-order cross-check.
- Coupled solution of axial and radial macrosegregation, reproduced against classical striation experiments.
- Explicit treatment of multi-dopant systems (co-doping, compensation) for semi-insulating Fe-doped InP, where Fe segregation interacts with residual shallow donor/acceptor background.

### WP2.2 — Stoichiometry and Native Point Defects

InP congruent melting is stoichiometry-sensitive; melt In:P ratio drift (from P loss by dissociation) shifts the effective liquidus and native point-defect incorporation (In vacancies, P vacancies, antisites), which in turn affects electrical compensation in nominally undoped or Fe-doped semi-insulating material. This is InP-specific physics with no direct Si analogue and must not be ported wholesale from Si/GaAs point-defect codes.

Deliverables:
- Mass-balance sub-model for P loss/retention as a function of encapsulant coverage, overpressure, and exposed melt area (LEC vs. high-pressure CZ regimes).
- Coupling of stoichiometry state to the segregation coefficients of WP2.1 and to the point-defect incorporation model (Frenkel-pair or Schottky-defect equilibrium approach, calibrated against DLTS/Hall data from literature).
- Explicit uncertainty bounds — this sub-model should be flagged as lower-TRL (technology readiness level) than the thermal-fluid core, and scheduled with contingency.

Key references:
- Burton, J.A., Prim, R.C., Slichter, W.P., "The distribution of solute in crystals grown from the melt," *J. Chem. Phys.* 21 (1953) 1987–1991.
- Tomizawa, K., "Numerical simulation of dopant transport," in *Handbook of Crystal Growth*, Vol. 2b, North-Holland (1994).
- Hurle, D.T.J., "A comprehensive thermodynamic analysis of native point defect and dopant solubilities in gallium arsenide," *J. Appl. Phys.* 85 (1999) — methodology directly extensible to InP.
- Bliss, D.F. et al., "Native point defects and stoichiometry effects in LEC InP," *J. Cryst. Growth* 128 (1993).

## 3. Thermoelastic Stress and Dislocation Generation

Dislocation density is frequently the single most important industrial output of an InP CZ/LEC simulation, given InP's low CRSS (roughly a factor of ~2–3 lower than GaAs, several times lower than Si at comparable homologous temperature).

### WP3.1 — Thermoelastic Stress Field

Quasi-static thermoelasticity solved on the (evolving) crystal domain using the temperature field from WP1:
$$
\nabla \cdot \boldsymbol{\sigma} = 0, \qquad \boldsymbol{\sigma} = \mathbb{C}(T):(\boldsymbol{\varepsilon} - \boldsymbol{\varepsilon}_{th}), \qquad \boldsymbol{\varepsilon}_{th} = \alpha(T)(T - T_{ref})\mathbf{I}
$$
with anisotropic elastic tensor $\mathbb{C}$ (zinc-blende cubic symmetry — 3 independent constants $C_{11}, C_{12}, C_{44}$), evaluated on the actual crystallographic orientation of the seed/pulled crystal (typically ⟨100⟩ or ⟨111⟩ for InP).

### WP3.2 — Dislocation Generation and Multiplication

Von Mises or resolved-shear-stress criterion against $T$-dependent CRSS, coupled to Alexander–Haasen-type dislocation dynamics for multiplication:
$$
\frac{dN}{dt} = K N \left(\frac{\tau_{eff}}{\tau_0}\right)^m \exp\left(-\frac{Q}{k_B T}\right), \qquad \tau_{eff} = \tau_{RSS} - \tau_{back}(N)
$$
where $N$ is mobile dislocation density and $\tau_{back}$ is the hardening back-stress from existing dislocations — this is the standard Alexander–Haasen–Sumino (AHS) framework, well established for Si/GaAs, requiring InP-specific calibration of $K$, $m$, $Q$.

Deliverables:
- Coupled thermoelastic + AHS solver producing predicted dislocation density maps ($N(r,z)$) across the boule, benchmarked against etch-pit-density (EPD) measurements on real InP boules (requires industrial partner or literature dataset access — flag as external dependency).
- Sensitivity study ranking furnace design/process parameters (pull rate, rotation rates, heater profile, afterheater/insulation design) by their effect on peak thermal stress, to make the tool directly actionable for furnace design iteration — this is the primary value proposition of the whole program for industrial users.
- Twin and polycrystalline-transition risk indicator, since InP is also prone to twinning at high thermal gradients, distinct from dislocation glide.

Key references:
- Alexander, H., Haasen, P., "Dislocations and plastic flow in the diamond structure," *Solid State Phys.* 22 (1968) 27–158.
- Jordan, A.S., Caruso, R., Von Neida, A.R., "A thermoelastic analysis of dislocation generation in pulled GaAs crystals," *Bell Syst. Tech. J.* 59 (1980) 593–637 (the foundational III-V thermoelastic-stress paper, directly transferable methodology).
- Kurz, W., Fisher, D.J., *Fundamentals of Solidification*, Trans Tech Publications — general framework.
- Chung, H.J. et al., "Thermal stress and dislocation density in LEC InP growth," specific InP-CRSS-calibration literature (search current *J. Cryst. Growth* / *J. Electron. Mater.* for latest calibration values, as figures vary across sources — treat as a literature-review deliverable in WP3, not a fixed citation).

## 4. Liquid Encapsulant (B$_2$O$_3$) Physics — LEC-Specific

The B$_2$O$_3$ encapsulant layer is not a passive boundary condition; it is an actively convecting, radiatively participating third fluid phase with its own free surfaces, and its thickness, viscosity profile, and coverage directly control axial gradients at the growth interface (the entire physical rationale for LEC over unencapsulated high-pressure CZ).

### WP4.1 — Encapsulant Flow and Heat Transfer

Full or lubrication-approximation Navier–Stokes/energy solve in the encapsulant annulus, coupled at both the InP-melt/B$_2$O$_3$ interface and the B$_2$O$_3$/ambient-gas interface, each with its own Marangoni and normal-stress balance.

### WP4.2 — Encapsulant Layer Thickness and Coverage Dynamics

Time-evolving encapsulant thickness as crystal diameter and melt level change through the run; risk of encapsulant breakthrough (loss of P confinement) at the triple line as a hard process-safety and yield constraint to be flagged by the model, not just simulated silently.

Deliverables:
- Coupled 3-phase (InP melt / B$_2$O$_3$ / ambient gas) free-boundary solver, initially 2D-axisymmetric, extended to 3D for ACRT/asymmetric cases (WP6).
- Sensitivity study of axial temperature gradient at the growth interface as a function of encapsulant thickness and viscosity (i.e., water content), connecting directly back to WP3 dislocation predictions — this is the key causal chain (encapsulant → gradient → stress → dislocations) that gives the LEC-specific model its industrial value over a generic CZ code.

Key references:
- Mullin, J.B. et al., "Liquid encapsulation crystal pulling at high pressures using an active method for accurate control of melt stoichiometry," *J. Cryst. Growth* 3–4 (1968) 281–285 (original LEC method paper).
- Jordan, A.S. et al. — extended thermoelastic LEC analyses (see WP3 refs).
- Bardsley, W. et al. on encapsulant meniscus mechanics.

## 5. Magnetohydrodynamics (MCZ Variant)

For magnetically damped CZ (MCZ) or InP variants using axial/transverse/cusp magnetic fields to suppress buoyant/thermocapillary turbulence in the melt, the Lorentz force term must be added to WP1's momentum equation:
$$
\mathbf{F}_{Lorentz} = \mathbf{J}\times\mathbf{B}, \qquad \mathbf{J} = \sigma_{el}(-\nabla\phi + \mathbf{u}\times\mathbf{B})
$$
requiring an additional electric potential Poisson equation and, for low magnetic Reynolds number (valid for InP melt conductivities and typical lab/industrial field strengths — to be verified quantitatively, not assumed), a quasi-static (inductionless) MHD approximation.

Deliverables:
- Inductionless MHD module as an optional physics package, verified against known analytical/benchmark MHD duct/Hartmann-layer flows before coupling into the full CZ solver.
- Regime map (Hartmann number $Ha$, magnetic interaction parameter $N$) identifying when MHD damping meaningfully changes the InP flow regime versus when it is a second-order correction, to prioritize this WP realistically against its considerable added complexity.

Key references:
- Series, R.W., Hurle, D.T.J., "The use of magnetic fields in semiconductor crystal growth," *J. Cryst. Growth* 113 (1991) 305–328.
- Davidson, P.A., "Magnetohydrodynamics in materials processing," *Annu. Rev. Fluid Mech.* 31 (1999) 273–300.
## 6. Numerical Methods and Discretization Strategy

### WP6.1 — Spatial Discretization

Recommendation: **finite element method (FEM)** as the primary discretization, for the following InP/CZ-specific reasons:
- Natural handling of deforming, unstructured, curved-boundary domains (crystal/melt interface shape evolves substantially, especially near seed-on and tail-off).
- Mature stabilized formulations (SUPG/PSPG, streamline-diffusion) for the convection-dominated regimes relevant here (high Prandtl number melt, $Pr_{InP} \approx 4$–$5$, and high Péclet number dopant transport, $Sc \sim 10$–$50$).
- Straightforward higher-order (Taylor–Hood or equal-order-stabilized) velocity-pressure elements for accurate Marangoni-flow boundary layers.

Finite volume method (FVM) retained as a documented alternative/cross-verification path (many production tools — CGSim, FEMAG-CZ — are FVM-based; code-to-code benchmarking in WP10 requires the team to understand both).

### WP6.2 — Moving-Mesh / Free-Boundary Strategy

**Arbitrary Lagrangian–Eulerian (ALE)** deforming mesh as the primary strategy for the melt/crystal/encapsulant domains and their shared free boundaries, since it gives sharp, well-resolved interfaces essential for the Stefan condition and meniscus physics of WP1.2–1.3 — critical for accurate radius/diameter control and thin-film encapsulant resolution.

Level-set or phase-field methods evaluated as a secondary/contingency path specifically for topologically difficult events (crystal neck formation at seeding, shoulder growth, tail-off pinch-off) where ALE remeshing becomes fragile; the roadmap should not commit irreversibly to pure-ALE without this contingency, since seed and tail transients are exactly where industrial furnace operators need the most predictive help (necking is the single highest-risk step for dislocation-free growth).

Deliverables:
- ALE mesh-motion solver (elastic pseudo-solid or Winslow-type mesh smoothing) verified for mesh-quality preservation under the large aspect-ratio and shape changes typical of a full InP boule run (seed, shoulder, body, tail).
- Automatic remeshing/mesh-quality-triggered re-projection pipeline with documented conservation properties (mass, energy, species must be conserved across remeshing events to machine precision or within a quantified, bounded tolerance).
- Contingency-path prototype (level-set or phase-field) specifically validated on the neck/tail topology-change problem.

### WP6.3 — Time Integration and Multi-Timescale Coupling

CZ/LEC growth spans timescales from milliseconds (turbulent/oscillatory melt convection) to hours (full boule pull). Recommended strategy:

- **Quasi-steady-state (QSS) mode**: pseudo-transient continuation for design-of-experiment sweeps and furnace design iteration, where only the slowly evolving crystal length/diameter matters and melt turbulence is time-averaged or RANS-modelled — this is the primary workhorse mode for the industrial use case (fast turnaround for design iteration).
- **Fully transient mode**: implicit (e.g., BDF2 or generalized-$\alpha$) time integration resolving actual melt flow transients, oscillatory convection, and ACRT-driven periodic forcing, used for research-grade runs and for validating that the QSS mode's time-averaging assumptions are actually justified for InP's operating regime (this justification step is often skipped in practice and should not be here).
- Explicit operator-splitting between the "fast" melt-flow/thermal subsystem and the "slow" global furnace thermal subsystem (WP7), with a documented, verified coupling/sub-cycling scheme rather than ad hoc time-step matching.

### WP6.4 — Turbulence/Transition Treatment in the Melt

InP melt flow at industrial crucible sizes and rotation rates is frequently transitional or weakly turbulent (moderate Grashof/Reynolds numbers relative to Si, but not negligible). Tiered approach:

- Direct solution (laminar/DNS-resolved) for small-diameter or low-Gr regimes and for method verification.
- Large-eddy simulation (LES) as the primary production closure for industrial-diameter, higher-$Gr$ cases, given RANS models' known poor performance for buoyancy-driven transitional convection in this geometry class.
- Explicit regime classification (documented $Gr$, $Re_\Omega$, $Ta$ thresholds specific to InP melt properties) to decide, per-run, which closure is appropriate — this must be a data-driven decision embedded in the tool, not a fixed global choice, since the same code will be used across small research crucibles and full industrial-diameter pulls.

Key references:
- Zienkiewicz, O.C., Taylor, R.L., Nithiarasu, P., *The Finite Element Method for Fluid Dynamics*, 7th ed., Butterworth-Heinemann (2014).
- Donea, J., Huerta, A., Ponthot, J.-Ph., Rodríguez-Ferran, A., "Arbitrary Lagrangian–Eulerian Methods," in *Encyclopedia of Computational Mechanics*, Wiley (2004).
- Sethian, J.A., *Level Set Methods and Fast Marching Methods*, Cambridge University Press (1999).
- Enger, S., Gräbner, O., Müller, G., Breuer, M., Durst, F., "Comparison of measured and calculated flow structures in a model of the industrial Czochralski crystal growth," *J. Cryst. Growth* 219 (2000) 144–150 — LES-relevant benchmark case.
- Kakimoto, K., Eguchi, M., Watanabe, H., Hibiya, T., "Flow instability of molten silicon during Czochralski crystal growth," *J. Cryst. Growth* 88 (1988) 365–370 — transition/oscillation reference methodology.

## 7. Global Furnace-Scale Coupling

### WP7.1 — Global Heat Transfer Model

Full furnace assembly (heater elements or RF coil, crucible, susceptor, insulation stack, chamber walls, gas ambient) modelled as a global thermal system coupled to the local melt/crystal/encapsulant solver of WP1–4. Two-way coupling is essential: local melt convection determines the crucible-wall heat flux distribution that the global model needs, while the global model sets the boundary conditions (radiative environment, heater power) that drive local melt convection.

### WP7.2 — Global-to-Local Coupling Architecture

Recommended architecture: a **hierarchical/nested coupling** scheme —
- Global quasi-steady thermal model (coarse mesh, full furnace geometry, radiation-dominated) computes furnace-scale temperature/heat-flux boundary conditions.
- Local high-fidelity model (WP1–6, fine mesh, melt/crystal/interface detail) solves within those boundary conditions.
- Iterative or (for QSS mode) one-way/lagged coupling per pseudo-time step, with convergence criteria explicitly defined and monitored (not just "run N iterations").

This mirrors the architecture used by the most credible existing production tools (see WP11 competitive analysis) and is chosen specifically because a fully monolithic global-to-local single mesh is computationally intractable at industrial scale for a multi-year iterative design tool.

Deliverables:
- Global furnace thermal solver, geometry-parametrized (data-driven per §0 principle) so furnace hardware changes (heater design, insulation redesign) are input-file changes, not code changes.
- Verified global/local coupling scheme with documented convergence behavior and failure-mode diagnostics (a critical robustness deliverable — coupled free-boundary + global-radiation systems are prone to non-convergence, and the tool must fail informatively, not silently).
- Ambient gas-flow sub-model (forced convection/purge gas flow pattern in the chamber), since gas-phase convective heat transport and P-vapor transport (WP2.2) both depend on chamber gas flow, particularly relevant for high-pressure CZ variants with significant inert gas flow.

Key references:
- Dupret, F., Van Den Bogaert, N., "Modelling Bridgman and Czochralski growth," in *Handbook of Crystal Growth*, Vol. 1b, North-Holland — global model methodology.
- Derby, J.J., Yeckel, A., "Heat transfer analysis and design for Czochralski crystal growth," in *Handbook of Crystal Growth*, Vol. 2a — canonical global/local coupling reference.
- Virbulis, J. et al., global CZ Si furnace modelling papers (methodologically transferable framework; note Si-specific numeric parameters do not transfer to InP).

## 8. Software Architecture and Engineering

### WP8.1 — Core Architecture Principles

- **Modular multiphysics kernel**: each physics module (melt flow, crystal thermoelasticity, radiation, MHD, dopant transport, encapsulant, global furnace) implemented as an independently testable, independently verifiable component behind well-defined interfaces (field data exchange, not tight code coupling), enabling later extensibility (§0) to other materials/processes without re-architecture.
- **Data-driven material/process configuration**: all material properties (WP1.5), process parameters, and furnace geometry defined in versioned input files, never hard-coded — this is what makes the "InP CZ/LEC" tool naturally extensible to GaAs, GaSb, Ge, Si, and to Bridgman/VGF variants with primarily a data/geometry change rather than a rewrite.
- **Separation of solver core (C++/Fortran performance layer) from orchestration/scripting layer** (Python), enabling rapid parameter-sweep scripting, ML-surrogate integration (WP12), and GUI/reporting layers without touching the validated numerical core — directly aligned with typical HPC/scientific-computing best practice for a codebase intended to survive years of extension.
- **Strict verification-first development**: no physics module merged into the coupled solver without a standalone MMS (method of manufactured solutions) verification test and, where an analytical or established benchmark solution exists, a benchmark comparison, both automated in CI.

### WP8.2 — Parallelization and HPC Strategy

- Domain-decomposition-based MPI parallelism for the FEM solver core (PETSc- or Trilinos-based linear algebra backend recommended over a custom solver, to avoid multi-year reinvention of preconditioners/Krylov solvers).
- GPU acceleration evaluated for the linear-algebra bottleneck (large sparse coupled Navier–Stokes/energy/species systems) once the CPU-parallel baseline is verified and profiled — sequenced deliberately after correctness is established, since premature GPU-porting of an unverified free-boundary solver is a common and costly failure mode.
- Explicit strong/weak scaling study and performance budget tied to the target production use case (design-of-experiment sweeps needing O(10–100) full-boule-run simulations per furnace-design iteration cycle) — this performance target should be set jointly with industrial stakeholders early, since it directly drives the QSS-vs-transient and RANS-vs-LES architectural choices in WP6.

### WP8.3 — Preconditioning and Linear/Nonlinear Solver Robustness

The coupled Navier–Stokes/energy/species/free-boundary/thermoelastic system is a strongly nonlinear, ill-conditioned system (high property contrast between melt, crystal, encapsulant, and gas; near-singular behavior near the triple line). Deliverables:

- Physics-based block/Schur-complement preconditioners for the coupled saddle-point (velocity-pressure) system, rather than generic black-box preconditioning, to achieve acceptable iteration counts at industrial mesh sizes.
- Robust Newton/Picard hybrid nonlinear solver strategy with documented globalization (line search / trust region) and fallback to continuation-in-parameter (e.g., ramping rotation rate, Marangoni number, or Grashof number) for hard-to-converge start-up states — a known, well-documented failure mode in CZ solvers that must be engineered around explicitly, not discovered late.
- Automated regression suite tracking solver robustness (iteration counts, convergence failures) across the parameter space as the codebase evolves, to catch robustness regressions introduced by seemingly unrelated changes.

Key references:
- Balay, S. et al., *PETSc/TAO Users Manual*, Argonne National Laboratory (current release) — solver backend reference.
- Elman, H., Silvester, D., Wathen, A., *Finite Elements and Fast Iterative Solvers*, 2nd ed., Oxford University Press (2014) — Navier–Stokes preconditioning.
- Kelley, C.T., *Solving Nonlinear Equations with Newton's Method*, SIAM (2003).
- Yeckel, A., Doty, C., Derby, J.J., "Robust Newton methods with fully coupled free-surface iteration for large-scale simulation of Czochralski crystal growth," *J. Cryst. Growth* 360 (2012) 1–10 — directly on-target reference for the exact robustness problem this WP addresses.
## 9. Verification and Validation (V&V) Program

V&V is architected as a standing program running in parallel with every WP above, not a terminal phase.

### WP9.1 — Verification (code is solving the equations correctly)

- Method of Manufactured Solutions (MMS) for every governing PDE module in isolation (momentum, energy, species, thermoelasticity, radiation) with quantified order-of-accuracy confirmation.
- Analytical benchmark comparisons where closed-form or semi-analytical solutions exist: Hartmann-layer MHD flow, Rayleigh–Bénard onset thresholds, pure-conduction Stefan-problem solutions, rotating-disk (von Kármán) boundary-layer flow as a rotation-driven-flow benchmark relevant to crystal/crucible rotation.
- Code-to-code benchmarking against at least one independent, published CZ benchmark problem set (e.g., the long-running international CZ silicon benchmark comparisons run by the crystal-growth-modelling community) as a cross-check of the coupled multiphysics solver, even though the target material differs — the benchmark tests numerical method fidelity, not InP-specific property accuracy.

### WP9.2 — Validation (equations/properties are the right physics for real InP growth)

Tiered against increasing experimental complexity:
- **Tier A — canonical model experiments**: transparent-analog or well-instrumented small-scale melt-flow experiments (e.g., laboratory Czochralski-configuration flow visualization with a low-melting-point analog fluid, or InP-specific if furnace access allows) for melt flow pattern and free-surface shape validation, decoupled from full crystal growth complexity.
- **Tier B — instrumented pilot InP growth runs**: thermocouple arrays, in-situ interface shape observation (X-ray or optical), post-growth EPD (etch pit density) mapping and Hall/photoluminescence-based dopant/point-defect characterization on real pulled boules — requires an industrial or academic InP growth partner; flag explicitly as an external dependency and secure early in the program, since experimental access lead time is often the true critical-path constraint on the whole roadmap.
- **Tier C — industrial-scale production-run comparison**: full-diameter, full-length boule comparison against production furnace logs and final wafer-level metrology (resistivity maps, dislocation density maps, radial dopant uniformity) — the ultimate acceptance test for "industrial-grade" claims.

Deliverables:
- A living validation matrix (which sub-model is validated against which experimental tier, with quantified error bounds) maintained as a first-class project artifact, reviewed at every major milestone.
- Explicit statement of the tool's validated operating envelope at each program stage — the model must never be presented as more broadly predictive than its actual validation coverage supports, and this envelope should gate any claims made to industrial users about applicability outside validated conditions.

Key references:
- Roache, P.J., *Verification and Validation in Computational Science and Engineering*, Hermosa Publishers (1998).
- Oberkampf, W.L., Roy, C.J., *Verification and Validation in Scientific Computing*, Cambridge University Press (2010).
- International Workshop on Modeling in Crystal Growth (IWMCG) proceedings — ongoing community benchmark source; check current/latest proceedings for the most recent CZ benchmark case definitions.

## 10. Extensibility and Reduced-Order / Surrogate Modelling

### WP10.1 — Process-Variant Extensibility

Architected (per WP8.1) so the same core is reused for:
- Vapor-pressure-controlled CZ (VCZ) — unencapsulated, high-inert-overpressure alternative to LEC, differing primarily in boundary conditions (no encapsulant phase, different chamber gas-flow/pressure regime) — a natural, low-risk first extensibility test of the architecture.
- ACRT (accelerated crucible rotation technique) — time-periodic rotation-rate forcing, exercising the fully transient time-integration path of WP6.3 and a good stress-test of the architecture's handling of genuinely time-dependent (non-QSS) production cases.
- Magnetic CZ variants (WP5) as an optional physics module toggle.

### WP10.2 — Reduced-Order Models and ML Surrogates

For the industrial design-of-experiment use case, full high-fidelity runs (hours to days of wall-clock time even at HPC scale) are too slow for interactive furnace-design exploration. Deliverables:

- Reduced-order model (ROM) layer — proper orthogonal decomposition (POD) or similar projection-based ROM trained on ensembles of high-fidelity runs, providing fast (seconds-scale) approximate predictions for interactive design exploration, with explicit, quantified fidelity loss relative to the full model.
- ML surrogate models (e.g., Gaussian process or neural-network regressors mapping process parameters → key industrial outputs like peak dislocation density, radial resistivity uniformity) trained on the validated high-fidelity dataset, always paired with uncertainty quantification and explicit out-of-training-distribution detection, so the surrogate cannot silently extrapolate into unvalidated regimes.
- Clear governance rule: ROM/ML surrogates are a productivity layer on top of the validated physics core, never a replacement for it in final furnace-design sign-off decisions — the roadmap should treat this as a policy deliverable, not just a technical one, given the real risk of over-reliance on fast-but-unverified surrogates in an industrial setting.

Key references:
- Benner, P., Gugercin, S., Willcox, K., "A survey of projection-based model reduction methods for parametric dynamical systems," *SIAM Rev.* 57 (2015) 483–531.
- Kennedy, M.C., O'Hagan, A., "Bayesian calibration of computer models," *J. R. Stat. Soc. B* 63 (2001) 425–464 — foundational for combining simulation + experiment under uncertainty, directly applicable to the Tier B/C validation-plus-surrogate workflow above.

## 11. Competitive/Prior-Art Landscape (Context for Scientific Completeness)

A brief, honest positioning against existing production and research CZ/LEC simulation tools is a necessary scoping input, not a distraction — it defines what already exists (so effort isn't wasted re-deriving solved sub-problems) and what is genuinely novel for InP:

- **CGSim** (STR Group) — commercial, broad CZ/VGF/Bridgman coverage across many materials; strong global furnace-scale thermal/stress modules; InP-specific property sets and encapsulant/LEC physics depth should be independently assessed rather than assumed present.
- **FEMAG / FEMAG-CZ** (Fraunhofer IISB) — strong academic pedigree (Müller, Friedrich groups) for melt convection and global heat transfer, historically Si-focused.
- **CrysMAS / CrysVUn** — global heat transfer and stress-focused tools from the same academic community; useful methodological and benchmark references (WP9.1) even where III-V/LEC coverage is limited.
- **Cats2D** (Derby, Yeckel, U. Minnesota) — research-grade, exceptionally strong on free-boundary/Newton-robustness methodology (WP8.3) and thermal-capillary modelling; a primary methodological reference throughout this roadmap, particularly WP1.2 and WP8.3.

Deliverables:
- A capability-gap matrix explicitly identifying where this program's InP/LEC-specific physics (encapsulant 3-phase dynamics, InP stoichiometry/point-defect coupling, InP-calibrated AHS dislocation parameters) goes beyond what is documented as available in existing tools, to justify the investment case for a from-scratch build versus extending/licensing an existing platform — this comparison should be revisited at each major program milestone as a go/no-go input.

## 12. Phased Project Plan (Indicative)

| Phase | Duration (indicative) | Primary WPs | Milestone / Exit Criterion |
|---|---|---|---|
| **Phase 0 — Foundations** | 6–9 months | WP1.1–1.5, WP9.1 (verification infra), WP8.1 (architecture) | Verified single-physics solvers (melt flow, conduction) pass MMS; property database v1 released |
| **Phase 1 — Coupled Free-Boundary Core** | 12–18 months | WP1.2–1.4, WP6.1–6.3, WP8.2–8.3 | Robust coupled melt/crystal/interface solver reproduces canonical CZ benchmark (WP9.1) to specified tolerance |
| **Phase 2 — InP-Specific Physics** | 12–18 months | WP2 (dopant/stoichiometry), WP3 (stress/dislocation), WP4 (LEC encapsulant) | Predicted dislocation density and dopant profile match Tier A/B validation data within quantified bounds |
| **Phase 3 — Global Coupling & Process Variants** | 9–12 months | WP7 (global furnace), WP5 (MHD), WP10.1 (VCZ/ACRT extensibility) | Full global-to-local coupled furnace simulation runs end-to-end for a representative production geometry |
| **Phase 4 — Industrial Validation & Productization** | 12–18 months, overlapping Phase 3 | WP9.2 Tier B/C, WP10.2 (ROM/ML), WP11 gap analysis, software hardening/UI/docs | Tier C industrial validation passed for at least one production furnace/recipe; ROM layer deployed for design-of-experiment use |
| **Ongoing** | continuous from Phase 1 | WP8.2 scaling, regression/CI, property-database maintenance | — |

Note on sequencing risk: WP2.2 (stoichiometry/point-defect coupling) and Tier B/C experimental validation (WP9.2) are explicitly flagged as the two highest-uncertainty, longest-lead-time items in the plan (respectively: genuinely open modelling questions, and external experimental-access dependency) and should be started as early as organizationally possible even though their WP numbering places them "later" — do not schedule them naively in strict WP-numeric order.

## 13. Risk Register (Summary)

| Risk | Likelihood | Impact | Mitigation |
|---|---|---|---|
| Property database gaps (esp. high-$T$ melt $k_\ell$, B$_2$O$_3$ viscosity-water relation) block quantitative accuracy | High | High | Early dedicated measurement/DFT campaign (WP1.5); sensitivity analysis to bound impact of uncertain properties before full investment |
| Free-boundary solver non-convergence at industrial parameter ranges | Medium-High | High | WP8.3 continuation/globalization strategy budgeted from Phase 1, not retrofitted |
| Neck/tail topology transitions break ALE mesh | Medium | Medium-High | Level-set/phase-field contingency prototype (WP6.2) developed in parallel, not sequentially after ALE failure is discovered |
| Experimental validation access (Tier B/C) delayed | Medium-High | High (blocks industrial-grade claim) | Secure academic/industrial growth partner in Phase 0, run in parallel with Phase 1–2 development |
| Stoichiometry/point-defect sub-model remains low-TRL / poorly calibrated | High | Medium | Explicit uncertainty flagging (§WP2.2); tool usable and valuable for thermal/stress/flow predictions even if this sub-model lags |
| Scope creep from "extensibility" ambitions delaying InP-specific delivery | Medium | Medium | Architecture (WP8.1) enables future extensibility without requiring other-material validation now; InP remains the sole validation target through Phase 4 |

## 14. Summary Reference List (Consolidated)

The reference list is distributed inline by work package above for direct traceability; the following are the highest-priority foundational texts spanning multiple WPs and worth acquiring first:

1. Hurle, D.T.J. (ed.), *Handbook of Crystal Growth*, 2nd ed., Vols. 1–2, North-Holland/Elsevier — the single most important reference set for this entire program.
2. Derby, J.J., Yeckel, A. and coworkers (University of Minnesota group) — collected papers on Czochralski free-boundary modelling and Newton-robust solvers (WP1.2, WP8.3).
3. Jordan, A.S., Caruso, R., Von Neida, A.R., *Bell Syst. Tech. J.* 59 (1980) — foundational III-V thermoelastic stress/dislocation paper (WP3).
4. Mullin, J.B. et al., *J. Cryst. Growth* 3–4 (1968) — original LEC method (WP4).
5. Modest, M.F., *Radiative Heat Transfer*, 3rd ed. — radiation methodology (WP1.4).
6. Roache, P.J. / Oberkampf & Roy — V&V methodology texts (WP9).
7. Bachmann, K.J. et al. / Landolt-Börnstein III/17a — InP materials property compilations (WP1.5).
8. Balay et al., *PETSc Users Manual* — recommended numerical linear algebra backend (WP8.2–8.3).

---

*End of roadmap. This document is intended as a living technical program plan — the validation matrix (§9.2), risk register (§13), and phased plan (§12) should be revisited at each major program milestone rather than treated as fixed at time of writing.*

---

> [!NOTE]
> 
> Generated by Claude.ai
>
> Model: Sonet 5
>
> Prompt: 
> **I want to develop a high-fidelity, physics-based numerical model of indium phosphide (InP) single-crystal growth using the Czochralski (CZ) or Liquid Encapsulated Czochralski (LEC) process.**
>
> **Please prepare an extensive, structured development roadmap that identifies every major scientific, engineering, computational, and validation task required to build such a model from first principles through industrial-scale simulation.**
>
> The roadmap should cover the complete modeling workflow, including:
>
> 1. **Crystal Growth Fundamentals**
>
>    * Physics of InP crystal growth
>    * Thermodynamics and phase equilibria
>    * Material properties
>    * High-pressure phosphorus atmosphere
>    * Encapsulant (B₂O₃) effects
>    * Defect formation mechanisms
> 2. **Mathematical Models**
>
>    * Heat transfer (conduction, convection, radiation)
>    * Melt flow (Navier–Stokes)
>    * Natural, forced, and Marangoni convection
>    * Species transport
>    * Interface evolution
>    * Crystal pulling and rotation
>    * Free-surface dynamics
>    * Stress and deformation
>    * Point-defect transport
>    * Segregation
>    * Dopant transport
>    * Gas-phase transport
>    * Electromagnetic fields (if applicable)
> 3. **Physical Properties Required**
>    Provide a complete inventory of all material properties required by the model, including:
>
>    * temperature dependence,
>    * pressure dependence,
>    * composition dependence,
>    * anisotropy,
>    * experimentally measured values,
>    * first-principles (DFT) calculations,
>    * CALPHAD databases,
>    * molecular dynamics,
>    * empirical correlations.
> 4. **Numerical Methods**
>
>    * Spatial discretization
>    * Time integration
>    * Nonlinear solvers
>    * Linear solvers
>    * Mesh generation
>    * Adaptive mesh refinement
>    * Moving boundary methods
>    * Interface tracking
>    * Parallel algorithms
>    * GPU acceleration
> 5. **Software Architecture**
>
>    * Modular design
>    * Coupling between physics modules
>    * Data structures
>    * Input/output formats
>    * Restart capability
>    * Visualization
>    * Testing framework
>    * Performance optimization
> 6. **Model Verification**
>
>    * Code verification
>    * Manufactured solutions
>    * Grid convergence studies
>    * Time-step convergence
>    * Conservation checks
>    * Sensitivity analysis
>    * Uncertainty quantification
> 7. **Model Validation**
>    Compare simulation results with experimental measurements, including:
>
>    * crystal shape,
>    * interface shape,
>    * temperature field,
>    * melt flow,
>    * segregation,
>    * dislocation density,
>    * thermal stress,
>    * crystal diameter,
>    * defect distribution,
>    * dopant concentration,
>    * growth rate.
> 8. **Computational Requirements**
>
>    * Expected computational cost
>    * HPC requirements
>    * CPU/GPU scaling
>    * Memory requirements
>    * Parallelization strategy
> 9. **Development Roadmap**
>    Divide the project into logical implementation phases, identifying:
>
>    * prerequisites,
>    * dependencies,
>    * milestones,
>    * expected outputs,
>    * recommended implementation order,
>    * approximate development effort,
>    * validation targets for each phase.
> 10. **Recommended Literature**
>     For every major topic, recommend authoritative textbooks, review articles, landmark papers, and recent publications (preferably from the last 10 years). Include DOIs whenever available.
>
> **The roadmap should be sufficiently detailed to serve as the basis for a multi-year research and software development project aimed at producing an industrial-grade simulation tool for InP crystal growth. Emphasize scientific completeness, numerical robustness, extensibility, and predictive accuracy.**
