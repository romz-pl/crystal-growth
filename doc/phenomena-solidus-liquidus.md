# The Role of Solidus and Liquidus in Crystal Growth from the Melt

## 1. Introduction

Nearly all industrially and scientifically important melt-growth processes — Czochralski (CZ), Bridgman/Vertical Gradient Freeze (VGF), Float Zone (FZ), Kyropoulos, Edge-defined Film-fed Growth (EFG), and directional solidification — involve crystallizing a material that is not a single pure element but an alloy, solid solution, or doped compound. Whenever the melt contains more than one chemical species (dopants, alloying elements, non-stoichiometric excess of one constituent, or intentional co-doping), the **liquidus** and **solidus** curves of the relevant phase diagram govern almost every aspect of the solidification behavior: the equilibrium partitioning of solute between phases, the freezing range, constitutional supercooling, interface morphology, and macro/microsegregation. Understanding and correctly modelling these curves is therefore central to melt-growth process design and crystal quality control.

This document provides a systematic overview of the thermodynamic basis of the liquidus/solidus, their coupling to segregation phenomena (equilibrium and effective distribution coefficients), their role in interface stability and constitutional supercooling, and their treatment in continuum growth models and simulation tools such as those in this reference library (CGSim, CrysMAS, FEMAG-CZ, CrysVUn).

---

## 2. Thermodynamic Definitions

### 2.1 The binary phase diagram

For a binary system A–B (solvent A, solute/dopant B), at a given pressure the equilibrium phase diagram plots temperature $T$ against composition $C$ (mole or mass fraction of B). Two key curves bound the two-phase (solid + liquid) coexistence region:

- **Liquidus line** $T_L(C)$: the locus of temperatures above which the alloy of composition $C$ is fully liquid. Below $T_L$, solid begins to nucleate/grow.
- **Solidus line** $T_S(C)$: the locus of temperatures below which the alloy is fully solid. Above $T_S$ (but below $T_L$), solid and liquid coexist in equilibrium.

At any temperature $T$ between $T_S$ and $T_L$ for a nominal (bulk) composition $C_0$, the compositions of the coexisting solid ($C_S$) and liquid ($C_L$) phases are given by the intersections of the horizontal tie-line at $T$ with the solidus and liquidus curves respectively (lever rule):

$$
f_S = \frac{C_L - C_0}{C_L - C_S}, \qquad f_L = \frac{C_0 - C_S}{C_L - C_S}
$$

where $f_S$, $f_L$ are the solid and liquid mass/mole fractions.

### 2.2 Equilibrium distribution (segregation) coefficient

The **equilibrium distribution coefficient** $k_0$ (also called the equilibrium segregation coefficient) is defined as the ratio of solute concentration in the solid to that in the liquid at the interface, under full local thermodynamic equilibrium:

$$
k_0 = \frac{C_S^\ast}{C_L^\ast}
$$

For dilute solutions, near the melting point of the pure solvent, the liquidus and solidus can be linearized:

$$
T_L(C) \approx T_m + m_L\, C, \qquad T_S(C) \approx T_m + m_S\, C
$$

with $m_L$, $m_S$ the liquidus and solidus slopes ($m_L, m_S < 0$ for most dopants that depress the melting point, $k_0 < 1$; $m_L, m_S > 0$ and $k_0 > 1$ is also possible, e.g. some dopants in silicon such as... — species-dependent). In this linear approximation:

$$
k_0 \approx \frac{m_L}{m_S}
$$

This is the single most consequential material parameter inherited from the phase diagram for melt-growth segregation modelling — nearly all continuum segregation models (Scheil, BPS, etc., see below) take $k_0$ as an input derived from the solidus/liquidus geometry.

### 2.3 Freezing range and its practical significance

The vertical separation $\Delta T = T_L(C_0) - T_S(C_0)$ at the nominal melt composition is the **freezing range** (or "mushy zone width" in temperature terms). It directly affects:

- **Interface morphology**: a wide freezing range favors a broadened two-phase (mushy) region and increases the tendency toward constitutional supercooling and interface breakdown (cellular/dendritic growth) — undesirable in most single-crystal growth.
- **Process control tolerance**: a narrow freezing range (as in nearly pure or dilute systems) permits a sharper, more stable solid–liquid interface, which is why heavily doped or highly alloyed melts are markedly harder to grow as single crystals than lightly doped ones.
- **Axial/radial segregation severity**: wider $\Delta T$ generally correlates with more pronounced macrosegregation because more solute must be rejected/redistributed over a larger thermal span.

---

## 3. Constitutional Supercooling and Interface Stability

### 3.1 The constitutional supercooling criterion

As solute is rejected at a growing solid–liquid interface with $k_0 < 1$, it accumulates in a thin boundary layer ahead of the interface, locally depressing the actual liquidus temperature relative to the imposed thermal gradient. If the *actual* temperature gradient in the melt near the interface falls below the gradient of the liquidus temperature profile set up by this solute pile-up, the liquid ahead of the interface is supercooled *not* because of undercooling in the usual thermal sense, but because of the local composition — hence "constitutional supercooling."

The classical **Tiller–Rutter–Jackson–Chalmers (Mullins–Sekerka refined)** criterion for interface breakdown (planar → cellular/dendritic transition) is:

$$
\frac{G}{V} < \frac{m_L\, C_0 (1-k_0)}{k_0 D_L}
$$

where:
- $G$ = temperature gradient in the liquid at the interface,
- $V$ = growth (pulling/interface advance) velocity,
- $m_L$ = liquidus slope,
- $C_0$ = nominal (far-field) solute concentration,
- $k_0$ = equilibrium distribution coefficient,
- $D_L$ = solute diffusivity in the liquid.

This criterion is a direct, quantitative link between the **liquidus slope** $m_L$ (a phase-diagram quantity) and the process parameters ($G$, $V$) that a grower can control. It is foundational in Czochralski, Bridgman, and directional solidification practice for selecting pull rates and thermal gradients that avoid morphological instability (see Tiller et al. 1953; Mullins & Sekerka 1964).

### 3.2 Constitutional supercooling and the Mullins–Sekerka linear stability analysis

The Mullins–Sekerka (1964) linear stability analysis extends the simple criterion above into a full perturbation analysis of interface stability, incorporating capillarity (Gibbs–Thomson effect), the liquidus slope, and both thermal and solutal diffusion fields. The liquidus slope $m_L$ enters directly as the "coupling constant" between interface-shape perturbations and the local equilibrium melting-point depression, making it one of the primary sensitivity parameters in stability maps used in the growth literature.

---

## 4. Effective Distribution Coefficient and Segregation Models

### 4.1 Why equilibrium $k_0$ is not directly observed

In practice, growth interfaces are not infinitely slow, and diffusion in the melt does not fully homogenize the boundary layer, so the concentration actually incorporated into the growing solid corresponds to an **effective distribution coefficient** $k_{\text{eff}} \ge k_0$ (for $k_0 < 1$), which depends on growth velocity, boundary-layer thickness (set by convection), and $D_L$.

### 4.2 Burton–Prim–Slichter (BPS) relation

The most widely used bridge between the equilibrium phase-diagram value $k_0$ and observed segregation is the **BPS equation** (Burton, Prim & Slichter, 1953):

$$
k_{\text{eff}} = \frac{k_0}{k_0 + (1-k_0)\, e^{-V\delta/D_L}}
$$

where $\delta$ is the effective diffusion boundary-layer thickness (a function of melt convection, rotation rate, and geometry). As $V\delta/D_L \to 0$ (slow growth, thin boundary layer / vigorous mixing), $k_{\text{eff}} \to k_0$; as $V\delta/D_L \to \infty$, $k_{\text{eff}} \to 1$ (complete solute trapping, no segregation).

This relation is the standard closure used in essentially every continuum Czochralski/Bridgman transport-and-segregation code (CGSim, CrysMAS, FEMAG-CZ, CrysVUn all implement BPS-type or extended boundary-layer segregation models), and $k_0$ — extracted from the solidus/liquidus geometry — is its indispensable input.

### 4.3 Scheil (non-equilibrium lever rule) model

For solidification where diffusion in the *solid* is negligible (a good approximation for most melt-grown semiconductors and oxides) but the liquid is well mixed, the **Scheil equation** gives the solid composition as a function of solid fraction $f_S$:

$$
C_S(f_S) = k_0\, C_0\, (1 - f_S)^{k_0 - 1}
$$

This describes the progressive axial (or "normal") macrosegregation observed along a Bridgman ingot or the length of a Czochralski boule as growth proceeds and the melt becomes progressively enriched (or depleted) in solute. Again, $k_0$ — derived from the solidus/liquidus slopes — is the controlling parameter; the entire axial segregation profile scales with it.

### 4.4 Coupling to full continuum models

In finite-element/finite-volume global growth simulators (CGSim, CrysMAS, FEMAG-CZ, CrysVUn — see this library's software-tools section), the solidus/liquidus/$k_0$ data are typically supplied as:

1. A **linearized phase diagram** ($T_m$, $m_L$, $k_0$) for dilute-limit problems (most common for doped Si, GaAs, oxide crystals with ppm–percent-level dopants).
2. A **full nonlinear phase-diagram table** ($T_L(C)$, $T_S(C)$) for concentrated alloy systems (e.g., SiGe, CdZnTe, GaInSb, and other pseudo-binary or ternary systems) where linearization fails over the relevant composition range.

The species transport equation solved in the melt,

$$
\frac{\partial C}{\partial t} + \mathbf{u}\cdot\nabla C = \nabla\cdot(D_L \nabla C)
$$

is coupled to the moving solid–liquid interface via a Stefan-type boundary condition that uses $k_0$ (or the full $C_S$–$C_L$ tie-line) to set the flux of rejected solute:

$$
D_L \left.\frac{\partial C}{\partial n}\right|_{\text{interface}} = V_n\, C_L^\ast (1-k_0)
$$

where $V_n$ is the local normal interface velocity. The interface temperature itself is pinned to the liquidus (or, more precisely, the liquidus corrected for curvature via the Gibbs–Thomson relation) rather than to the pure-substance melting point — a distinction that matters increasingly as dopant/alloy concentration rises.

---

## 5. Gibbs–Thomson (Curvature) Correction to the Liquidus

For a curved solid–liquid interface (as during dendritic, cellular, or even macroscopically curved CZ/Bridgman interfaces), the local equilibrium melting temperature is depressed relative to the flat-interface liquidus by the **Gibbs–Thomson effect**:

$$
T_{\text{interface}} = T_L(C_L^\ast) - \Gamma\, \kappa
$$

where $\Gamma$ is the Gibbs–Thomson coefficient (surface energy/entropy of fusion per unit volume) and $\kappa$ is the local interface curvature. This term is generally small for macroscopic melt-growth interfaces but becomes essential in:

- Dendrite-tip selection theory (microstructure prediction),
- Interface stability analyses (Mullins–Sekerka, §3.2),
- Phase-field models of solidification microstructure, which use the liquidus/solidus data (and their curvature-corrected form) as the equilibrium reference state around which the diffuse interface evolves.

---

## 6. Practical Consequences for Melt-Growth Processes

| Phenomenon | Governing phase-diagram quantity | Consequence for growth |
|---|---|---|
| Axial (normal) segregation | $k_0$ (via Scheil/BPS) | Dopant concentration drifts along crystal length; limits usable ingot fraction |
| Radial segregation | $k_0$, $k_{\text{eff}}$, interface shape | Non-uniform resistivity/composition across wafer diameter |
| Constitutional supercooling / interface breakdown | $m_L$, $k_0$, $\Delta T$ | Sets maximum stable growth rate for a given $G$; cellular/dendritic transition |
| Facet formation & impurity striations | Local liquidus curvature, kinetic undercooling | Non-uniform incorporation at facets vs. non-faceted regions |
| Mushy-zone width in Bridgman/VGF | $\Delta T = T_L - T_S$ | Determines interface sharpness, extent of two-phase region, permeability for interdendritic flow |
| Alloy/solid-solution crystal growth (e.g., SiGe, CdZnTe, HgCdTe) | Full nonlinear $T_L(C)$, $T_S(C)$ | Requires non-dilute treatment; linear $k_0$ approximation breaks down |

### 6.1 Czochralski and Kyropoulos growth

In CZ and Kyropoulos growth, the liquidus temperature at the melt's instantaneous bulk composition sets the required melt superheat and crucible-wall temperature profile. As the melt volume shrinks and solute rejected at the growing crystal accumulates (assuming $k_0<1$), the bulk liquid composition $C_L$ increases with solidified fraction according to Scheil-type behavior (well mixed, negligible solid diffusion), so the pull temperature must be continuously adjusted to track the rising $T_L(C_L)$ — a control problem directly derived from the liquidus curve's shape.

### 6.2 Bridgman/VGF/directional solidification

Here the solidus/liquidus separation directly defines the **mushy zone** thickness when growth is not idealized as sharp-interface. Continuum mushy-zone models (e.g., Darcy-flow interdendritic convection models) use the lever rule or Scheil relation, parameterized by the local $T_L$, $T_S$, to distribute the solid fraction $f_S(T)$ within the two-phase region, which in turn controls interdendritic melt flow resistance (via Kozeny–Carman-type permeability laws) and hence macrosegregation patterns (channels, freckles).

### 6.3 Float Zone and container-free methods

FZ growth of high-purity or intrinsic semiconductors benefits from typically very small $k_0$ (efficient purification per pass — zone refining is the discrete-pass analog of the segregation described by BPS/Scheil), and the liquidus/solidus data set the theoretical purification limit per pass via the same distribution-coefficient framework.

---

## 7. Determination of Solidus/Liquidus Data

Practical continuum modelling requires phase-diagram data as model input; sources include:

- **Experimental determination**: DTA/DSC (differential thermal/scanning calorimetry), quenching-and-metallography, and in-situ X-ray/neutron diffraction during controlled cooling.
- **CALPHAD (CALculation of PHAse Diagrams) assessments**: thermodynamic (Gibbs energy) modelling of each phase, fitted to experimental data, providing self-consistent $T_L(C)$, $T_S(C)$ over the full composition and temperature range, including metastable extensions useful for rapid-solidification/undercooling regimes.
- **First-principles (DFT) and CALPHAD-DFT hybrid approaches**: increasingly used for less-studied or exotic compound-semiconductor and oxide systems where experimental phase diagrams are incomplete.

For dilute dopants in common melt-growth systems (Si, Ge, GaAs, oxide crystals), tabulated $k_0$ values (often "segregation coefficient tables") are widely available in the crystal-growth literature and are commonly treated as approximately constant over the small composition range typical of doping, justifying the linearized liquidus/solidus treatment of §2.2 in most CZ/FZ device-grade crystal modelling.

---

## 8. Key References

1. Burton, J. A., Prim, R. C., & Slichter, W. P. (1953). *The Distribution of Solute in Crystals Grown from the Melt. Part I. Theoretical.* Journal of Chemical Physics, 21(11), 1987–1991.
2. Tiller, W. A., Jackson, K. A., Rutter, J. W., & Chalmers, B. (1953). *The redistribution of solute atoms during the solidification of metals.* Acta Metallurgica, 1(4), 428–437.
3. Mullins, W. W., & Sekerka, R. F. (1964). *Stability of a Planar Interface During Solidification of a Dilute Binary Alloy.* Journal of Applied Physics, 35(2), 444–451.
4. Scheil, E. (1942). *Bemerkungen zur Schichtkristallbildung.* Zeitschrift für Metallkunde, 34, 70–72.
5. Flemings, M. C. (1974). *Solidification Processing.* McGraw-Hill.
6. Kurz, W., & Fisher, D. J. (1998). *Fundamentals of Solidification* (4th ed.). Trans Tech Publications.
7. Hurle, D. T. J. (Ed.). (1993–1994). *Handbook of Crystal Growth*, Vols. 1–3. North-Holland/Elsevier. (See especially the chapters on segregation and constitutional supercooling in Vol. 2, "Bulk Crystal Growth.")
8. Brice, J. C. (1986). *Crystal Growth Processes.* Blackie & Son.
9. Müller, G., & Friedrich, J. (2004). *Handbook of Crystal Growth: Bulk Crystal Growth — Convection and Segregation.* (Also see Müller & Friedrich review chapters in *Crystal Growth Technology*, Scheel & Fukuda, Eds., Wiley, 2003.)
10. Saunders, N., & Miodownik, A. P. (1998). *CALPHAD (Calculation of Phase Diagrams): A Comprehensive Guide.* Pergamon Materials Series, Elsevier.
11. Derby, J. J., and co-workers — various papers on finite-element modelling of Czochralski growth incorporating segregation and interface tracking (University of Minnesota group; see the Derby bibliography section of this reference library for full citation list).
12. Dupret, F., & Van den Bogaert, N. (1994). *Modelling Bridgman and Czochralski Growth.* In *Handbook of Crystal Growth*, Vol. 2b, Ch. 15, North-Holland.

---

## 9. Summary

The liquidus and solidus curves are not a peripheral thermodynamic detail in melt crystal growth — they are the material-property backbone from which the equilibrium distribution coefficient $k_0$, the freezing range $\Delta T$, and the constitutional-supercooling criterion are all derived. Every major continuum segregation model in use today (BPS, Scheil, and their generalizations embedded in CGSim, CrysMAS, FEMAG-CZ, and CrysVUn) takes solidus/liquidus data as direct input, and interface stability limits that constrain achievable growth rates in CZ, Bridgman, and FZ processes are fundamentally set by the liquidus slope acting through the Tiller/Mullins–Sekerka criteria. Accurate phase-diagram data — whether from experiment, CALPHAD assessment, or first-principles calculation — is therefore a prerequisite for predictive, quantitative modelling of dopant/alloy segregation and interface morphology in melt growth.

---

> [!NOTE]
> 
> Generated by Claude.ai
>
> Model: Sonet 5
>
> Prompt: Provide an extensive overview of the role of solidus and liquidus in crystal growth from the melt. Provide key references. Show the output in Markdown format.
