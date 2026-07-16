# The Role of Dissociation Vapor Pressure in Crystal Growth from the Melt

## 1. Introduction and Scope

Many technologically important melt-grown crystals — III-V semiconductors (GaAs, InP, GaP), II-VI compounds (CdTe, ZnSe, CdS), oxide crystals used in optics and electronics, and certain halides — are congruently or incongruently melting compounds whose constituent species have significantly different volatilities. At the melting point, one component (typically the group-V or group-VI element, or a volatile oxide-forming species) exhibits a substantial equilibrium vapor pressure arising from thermal dissociation of the melt. This document surveys how dissociation vapor pressure governs melt stoichiometry, growth-system design, and defect formation, and how it is treated in continuum models of melt growth.

## 2. Physical Origin of Dissociation Vapor Pressure

### 2.1 Congruent vs. Incongruent Vaporization

A binary compound $AB$ melting at temperature $T_m$ may vaporize according to several possible reactions. For compounds such as GaAs, InP, and CdTe, the dominant high-temperature vaporization pathway is dissociative:

$$AB(l) \rightleftharpoons A(l) + \tfrac{1}{2}B_2(g)$$

or, for group-VI-rich systems,

$$AB(l) \rightleftharpoons A(g) + \tfrac{1}{2}B_2(g)$$

The equilibrium is governed by the mass-action law relating the activities of the condensed and vapor species to an equilibrium constant $K(T)$:

$$K(T) = \frac{a_A \, p_{B_2}^{1/2}}{a_{AB}}$$

where $a_i$ denotes the activity of species $i$ in the melt and $p_{B_2}$ is the partial pressure of the diatomic vapor species. Because $K(T)$ depends exponentially on temperature through the van 't Hoff relation,

$$\ln K(T) = -\frac{\Delta H^\ast}{RT} + \frac{\Delta S^\ast}{R}$$

small variations in melt temperature near $T_m$ produce large variations in the equilibrium dissociation pressure — often spanning several atmospheres for a temperature change of only tens of kelvin in systems like GaAs (where $p_{\mathrm{As}_2}$ at the melting point, $\sim 1238\,^\circ\mathrm{C}$, is on the order of 1 atm) or CdTe (where cadmium and tellurium vapor pressures separately approach several atmospheres near $1092\,^\circ\mathrm{C}$).

### 2.2 Stoichiometry Coupling

The dissociation reaction directly couples the melt's stoichiometric deviation $\delta$ (departure from the ideal $A:B = 1:1$ ratio) to the ambient overpressure of the volatile component. If the imposed overpressure $p_{B_2}^{\mathrm{ambient}}$ differs from the equilibrium dissociation pressure $p_{B_2}^{\mathrm{eq}}(T_m)$, the melt will lose or gain the volatile species until a new local equilibrium (or a steady-state evaporative flux) is established. This is the central mechanism by which vapor pressure control translates into control of point-defect concentrations in the grown crystal, since native point defects (vacancies, antisites, interstitials) in compounds such as GaAs are strongly stoichiometry-dependent.

## 3. Consequences for Crystal Growth System Design

### 3.1 Sealed and Pressurized Systems

Because uncontrolled loss of the volatile component would drive the melt off-stoichiometry and, in the extreme, cause violent boiling or melt ejection, growth of dissociating compounds requires either:

- **Sealed ampoule growth** (Bridgman, vertical gradient freeze, gradient freeze) with a controlled cold-zone vapor reservoir that fixes $p_{B_2}$ via the reservoir's own temperature, exploiting the strongly temperature-dependent equilibrium vapor pressure curve of the pure volatile element;
- **Liquid encapsulation** (LEC — Liquid Encapsulated Czochralski), in which a molten boric oxide ($B_2O_3$) layer floats atop the melt and mechanically suppresses the escape of dissociation vapor, allowing open-chamber pulling without a sealed pressure vessel;
- **Hot-wall / pressurized-chamber Czochralski (HP-VCZ, VCZ)**, in which the entire growth chamber is backfilled with an inert or reactive overpressure of the volatile species (or an inert gas at matching total pressure) to suppress net dissociation flux from the free melt surface.

### 3.2 Reservoir-Controlled Vapor Pressure (Bridgman / Gradient Freeze Family)

In two-zone sealed-ampoule methods, a source reservoir of the pure volatile element (e.g., As or Cd) is maintained at a temperature $T_r$ distinct from the melt temperature $T_m$. The reservoir's own vapor pressure curve $p^{sat}(T_r)$ — an independently tabulated thermophysical property of the pure element — sets the ambient partial pressure seen by the melt. The grower selects $T_r$ so that

$$p^{sat}(T_r) \approx p_{B_2}^{\mathrm{eq}}(T_m, \delta_{\mathrm{target}})$$

thereby fixing the melt at (or near) a desired stoichiometry $\delta_{\mathrm{target}}$, often chosen to lie on the congruent-melting composition or slightly off it to favor a particular native defect population. This reservoir-temperature strategy is the standard route for stoichiometry control in GaAs VGF/VB and CdTe/CdZnTe Bridgman growth.

### 3.3 Encapsulant Layers and Boric Oxide Chemistry (LEC)

In LEC growth, the $B_2O_3$ encapsulant must remain molten (viscosity and wetting behavior are temperature-sensitive) and must maintain a sufficient hydrostatic head to counteract the dissociation-driven gas pressure trying to bubble through it. The chamber is additionally pressurized with inert gas (commonly to 20–60 atm for GaAs LEC) as a second line of containment, since $B_2O_3$ alone is imperfectly impermeable to volatile species and can itself dissolve small amounts of the melt's volatile component, subtly perturbing the effective stoichiometry balance.

### 3.4 Interface and Free-Surface Effects

Where the melt is exposed to a free surface (as opposed to fully sealed and equilibrated), a local evaporative flux $J$ of the volatile species can be estimated from Hertz-Knudsen-type kinetics,

$$J = \alpha_c \left( p_{B_2}^{\mathrm{eq}}(T_s) - p_{B_2}^{\mathrm{ambient}} \right) \sqrt{\frac{M}{2\pi R T_s}}$$

where $T_s$ is the local free-surface temperature, $M$ the molar mass of the vapor species, and $\alpha_c$ a condensation/evaporation coefficient. Because free-surface temperature is spatially non-uniform (radial temperature gradients driven by crucible heating, rotation, and radiative losses), this flux is itself non-uniform, coupling the vapor pressure problem to the free-melt-surface thermal and Marangoni-flow physics that govern convective transport beneath the surface. Regions of the melt surface running hotter than the setpoint (e.g., due to local convective upwelling) will preferentially lose volatile species, seeding local stoichiometry gradients that later solidify into the crystal.

## 4. Coupling to Stoichiometry, Point Defects, and Crystal Quality

### 4.1 Melt-to-Crystal Stoichiometry Transfer

At the growth interface, the crystal solidifies with a stoichiometric deviation that reflects (but is not necessarily identical to) the melt's deviation, modulated by the segregation behavior of the relevant native defects and by the local growth rate (through solute-trapping-like kinetics at high growth velocity). Since native defect formation energies in compounds like GaAs are strongly composition-dependent, the vapor-pressure-set melt stoichiometry is one of the primary levers by which growers control:

- **Antisite defect concentration** (e.g., $\mathrm{As}_{Ga}$ antisites in GaAs, associated with the EL2 deep level, whose concentration is a strong, well-documented function of melt As fraction);
- **Vacancy and interstitial populations**, which in turn affect electrical compensation, carrier lifetime, and mechanical/dislocation behavior via point-defect–dislocation interactions;
- **Precipitate and inclusion formation**, when local supersaturation of the volatile component (from vapor-pressure excursions during growth) exceeds the solid solubility limit upon cooling, nucleating second-phase precipitates (e.g., As precipitates in semi-insulating GaAs).

### 4.2 Axial and Radial Segregation Coupling

Because the equilibrium dissociation pressure depends on melt temperature, and melt temperature varies axially as the ampoule or boule is progressively frozen (in Bridgman-family growth) or as the pulled crystal length changes the thermal environment (in Czochralski-family growth), the effective melt stoichiometry — and hence the vapor-pressure equilibrium point — drifts over the course of a growth run. This produces axial gradients in native defect concentration analogous to (and superimposed upon) classical dopant segregation described by the effective distribution coefficient. Vapor-pressure-driven stoichiometry drift is therefore treated, in rigorous process models, as an additional pseudo-species transport problem coupled to the usual dopant segregation equations.

## 5. Vapor Pressure in Continuum Process Models

### 5.1 Boundary Condition Formulation

In global heat/mass transfer simulations (e.g., in CGSim, FEMAG-CZ, or custom finite-element melt-growth codes), dissociation vapor pressure enters primarily as a **boundary condition at the free melt surface and/or at the ampoule vapor space**, rather than as a bulk-melt transport equation. Typical formulations include:

- **Fixed vapor pressure (Dirichlet-type) condition**, appropriate for well-equilibrated sealed systems with a large vapor reservoir buffering any local flux;
- **Flux (Neumann-type) condition** derived from Hertz-Knudsen or Langmuir evaporation kinetics, appropriate for open or quasi-open systems (LEC, VCZ) where local surface temperature variations can drive non-uniform evaporative loss;
- **Coupled reservoir-melt equilibrium**, in which the vapor space is itself modeled as a well-mixed compressible gas volume whose pressure evolves according to mass conservation with source terms from melt evaporation and reservoir sublimation — necessary when reservoir and melt are not assumed to instantaneously equilibrate.

### 5.2 Coupling to Melt Convection and Thermal Field

Because the vapor pressure boundary condition depends on local free-surface temperature, and the free-surface temperature field is itself set by the melt's convective state (buoyancy-driven, Marangoni, and forced convection from crystal/crucible rotation), vapor pressure modeling cannot generally be decoupled from the broader melt-flow simulation. This is one of several reasons dissociation-pressure-sensitive growth systems (GaAs, InP, CdTe) have historically motivated some of the more elaborate coupled thermal-fluid-species process models in the crystal growth simulation literature, relative to congruently-vaporizing, low-volatility systems (e.g., silicon Czochralski, where vapor pressure effects are comparatively minor except for dopant/oxide volatilization).

### 5.3 Numerical and Practical Challenges

- **Stiffness from exponential temperature dependence**: because $p^{eq}(T)$ varies exponentially with $T$ via the van 't Hoff relation, small errors in the computed free-surface or reservoir temperature field propagate into large errors in predicted vapor pressure, demanding high-accuracy thermal solutions in the relevant vapor-generating regions.
- **Multi-scale species transport**: gas-phase transport of the dissociation vapor within the growth chamber (particularly in open or partially open configurations) may itself be diffusion- or convection-limited, requiring a gas-phase transport submodel coupled to the melt-surface flux boundary condition.
- **Uncertain thermophysical input data**: equilibrium constants, activity coefficients in non-ideal melts, and evaporation/condensation coefficients are frequently only approximately known for less-studied compounds, introducing significant model uncertainty relative to the well-characterized elemental-silicon case.

## 6. Representative Material Systems

| System | Dissociation species | Approx. vapor pressure near $T_m$ | Dominant industrial method |
|---|---|---|---|
| GaAs | $\mathrm{As}_2$, $\mathrm{As}_4$ | $\sim 1$ atm at $1238\,^\circ\mathrm{C}$ | LEC, VGF/VB, HP-VCZ |
| InP | $\mathrm{P}_2$, $\mathrm{P}_4$ | Several atm at $1062\,^\circ\mathrm{C}$ | LEC, VGF |
| CdTe / CdZnTe | Cd, $\mathrm{Te}_2$ | Several atm at $1092\,^\circ\mathrm{C}$ | Bridgman, THM |
| GaP | $\mathrm{P}_2$, $\mathrm{P}_4$ | High (tens of atm regime) | LEC (high-pressure), VGF |
| ZnSe / ZnS | Zn, $\mathrm{Se}_2$ / $\mathrm{S}_2$ | Very high | Seeded PVT preferred over melt growth |

The last row illustrates a key practical consequence: when dissociation vapor pressure becomes too large for any melt-containment strategy to manage economically, growers abandon melt growth altogether in favor of vapor-phase methods (PVT, sublimation-recondensation), which sidestep the containment problem by working with the vapor phase directly rather than suppressing it.

## 7. Summary

Dissociation vapor pressure is not a peripheral thermophysical curiosity in melt growth of volatile compound semiconductors and related materials — it is a first-order design constraint that determines the choice of growth method (sealed vs. encapsulated vs. pressurized), the engineering of reservoir and chamber pressure control, and, through its coupling to melt stoichiometry, a primary determinant of native point-defect populations and hence electrical and optical crystal quality. Rigorous continuum process models must treat it as a temperature-sensitive boundary condition tightly coupled to the melt's convective thermal field, rather than as an independent, spatially uniform parameter.

## 8. Suggested Further Reading Directions

- Thermodynamic assessments of III-V and II-VI phase diagrams (CALPHAD-type treatments) for equilibrium constant and activity data.
- Process-modeling literature on LEC and VGF GaAs growth addressing coupled encapsulant/vapor-pressure/thermal-field simulation.
- Point-defect thermodynamics literature relating melt stoichiometry to native defect formation energies (e.g., EL2/antisite studies in GaAs).
- Bridgman/gradient-freeze reservoir design studies for CdTe and CdZnTe detector-grade crystal growth.


---

> [!NOTE]
> 
> Generated by Claude.ai
>
> Model: Sonet 5
>
> Prompt: Provide an extensive overview of the role of dissociation vapor pressure in crystal growth from the melt. Show the output in Markdown format.
