# Segregation at the Growth Interface

## 1. Scope and Framework

In continuum (macroscopic) models of melt or solution crystal growth — as implemented in global simulation codes such as CGSim, CrysMAS, FEMAG-CZ, CrysVUn, and Cats2D — the crystal–melt (or crystal–solution) interface is treated as a moving, sharp mathematical surface $\Gamma(t)$ separating two continua: the solid phase (crystal) and the liquid phase (melt or solution). Solute segregation refers to the redistribution of a dopant, impurity, or solute species between these two phases as the interface advances. This phenomenon is governed by an interfacial partition (distribution) law coupled with mass conservation, heat transport, fluid flow, and species diffusion/convection equations, all solved self-consistently on the continuum scale (as opposed to atomistic or phase-field descriptions of interface attachment kinetics).

The macroscopic segregation problem sits at the intersection of:

- **Thermodynamics** (equilibrium phase diagram, distribution coefficient)
- **Interface kinetics** (non-equilibrium partition under finite growth rate)
- **Transport phenomena** (diffusion and convection of solute in the melt boundary layer)
- **Global heat and momentum transport** (which set the growth rate, interface shape, and flow field that in turn control segregation)

---

## 2. The Equilibrium Distribution (Segregation) Coefficient

### 2.1 Definition

At thermodynamic equilibrium, the partitioning of a solute between solid and liquid at the interface is described by the **equilibrium segregation coefficient**:

$$
k_0 = \frac{C_s^{*}}{C_l^{*}}
$$

where $C_s^{*}$ is the solute concentration in the solid immediately at the interface and $C_l^{*}$ is the solute concentration in the liquid immediately at the interface. This quantity is a direct consequence of the binary (or multicomponent) phase diagram — specifically the ratio of the slopes of the solidus and liquidus lines near the melting point of the solvent:

$$
k_0 = \frac{m_l}{m_s} \quad \text{(in the dilute-solution limit, from local liquidus/solidus slopes)}
$$

- If $k_0 < 1$: solute is rejected into the melt during growth (most dopants in Si, Ge, GaAs, oxide crystals).
- If $k_0 > 1$: solute is preferentially incorporated into the solid.
- If $k_0 = 1$: no segregation occurs; the solute distributes uniformly.

### 2.2 Concentration Dependence

$k_0$ is strictly constant only in the dilute limit. For non-dilute systems, or where the phase diagram is non-linear, $k_0 = k_0(C_l^{*}, T^{*})$ becomes a function of local interface concentration and temperature, requiring a locally linearized liquidus slope $m_l(C)$ evaluated at each interface point in the simulation.

---

## 3. Non-Equilibrium (Effective) Segregation Coefficient

### 3.1 Motivation

In real growth processes, growth rates $V$ are finite, and solute rejected at the interface cannot instantaneously equilibrate with the bulk melt. A solute-enriched (or depleted) boundary layer of thickness $\delta_c$ develops ahead of the interface. The continuum model captures this via mass transport equations rather than atomistic attachment kinetics, but the **effective distribution coefficient** $k_{\mathrm{eff}}$ emerges as a diagnostic/derived quantity representing the ratio of solute actually incorporated into the crystal to the solute concentration in the bulk melt far from the interface:

$$
k_{\mathrm{eff}} = \frac{C_s^{*}}{C_{l,\infty}}
$$

where $C_{l,\infty}$ is the solute concentration in the well-mixed bulk liquid, outside the diffusion boundary layer.

### 3.2 The Burton–Prim–Slichter (BPS) Relation

The classical macroscopic closure linking $k_0$, growth rate, boundary-layer transport, and $k_{\mathrm{eff}}$ is the **BPS equation**:

$$
k_{\mathrm{eff}} = \frac{k_0}{k_0 + (1 - k_0)\, e^{-V \delta_c / D_l}}
$$

where:

- $V$ — crystal growth (pulling/interface advance) rate normal to the interface,
- $D_l$ — solute diffusion coefficient in the liquid,
- $\delta_c$ — effective mass-transfer (concentration) boundary-layer thickness, determined by the flow field (forced and/or natural convection, crystal/crucible rotation).

**Limiting behavior:**

$$
\lim_{V\delta_c/D_l \to 0} k_{\mathrm{eff}} = k_0 \qquad \text{(perfect mixing / diffusion-dominated removal)}
$$

$$
\lim_{V\delta_c/D_l \to \infty} k_{\mathrm{eff}} = 1 \qquad \text{(complete solute trapping, no back-diffusion)}
$$

This relation is central to continuum growth models because $\delta_c$ is not a free empirical parameter but is computed from the resolved velocity and species field (or estimated via a boundary-layer correlation, see §5).

---

## 4. Governing Equations in the Bulk Liquid and Solid

### 4.1 Species Transport in the Melt/Solution

The solute concentration field $C_l(\mathbf{x}, t)$ in the liquid obeys the convection–diffusion equation:

$$
\frac{\partial C_l}{\partial t} + \mathbf{u} \cdot \nabla C_l = D_l \nabla^2 C_l
$$

where $\mathbf{u}(\mathbf{x}, t)$ is the melt velocity field obtained from the coupled Navier–Stokes (or Boussinesq-approximated buoyancy-driven) equations, including contributions from:

- Buoyancy-driven (natural) convection,
- Forced convection from crystal and/or crucible rotation,
- Marangoni (thermocapillary) convection at free melt surfaces,
- Possibly magnetically damped or driven flow (for MHD-controlled growth, e.g., CZ with applied magnetic fields).

### 4.2 Species Transport in the Solid

In the solid, transport is generally diffusion-only and typically neglected on growth timescales (solid-state diffusivities are orders of magnitude smaller than in the melt), so:

$$
\frac{\partial C_s}{\partial t} \approx 0 \quad \text{(frozen-in composition, except for post-growth annealing/homogenization studies)}
$$

This is the standard justification for treating the solid concentration field as simply "written" by the moving interface at each instant, i.e., $C_s(\mathbf{x}) = C_s^{*}(\mathbf{x}_{\Gamma}, t)$ at the moment the interface passed through point $\mathbf{x}$.

---

## 5. Interfacial Boundary Conditions: The Solute Balance at $\Gamma$

### 5.1 Local Mass (Solute) Conservation at the Moving Interface

The interface is a discontinuity surface. A local solute flux balance in the frame moving with the interface (normal velocity $V_n$) gives:

$$
V_n \left( C_l^{*} - C_s^{*} \right) = -D_l \frac{\partial C_l}{\partial n} \Big|_{\Gamma^{+}} + D_s \frac{\partial C_s}{\partial n} \Big|_{\Gamma^{-}}
$$

Neglecting solid-state diffusion ($D_s \to 0$):

$$
V_n \left( C_l^{*} - C_s^{*} \right) = -D_l \frac{\partial C_l}{\partial n} \Big|_{\Gamma^{+}}
$$

This equation states that the solute rejected (or absorbed) by the moving interface, $V_n(C_l^{*} - C_s^{*})$, must be carried away (or supplied) by diffusive flux in the liquid immediately adjacent to the interface. This is the fundamental **interfacial boundary condition** applied at every point of $\Gamma$ in the continuum model, coupled to the equilibrium (or kinetic) partition relation $C_s^{*} = k_0 C_l^{*}$.

### 5.2 Combined Interface Condition

Substituting the partition law into the flux balance:

$$
V_n \, C_l^{*} (1 - k_0) = -D_l \frac{\partial C_l}{\partial n} \Big|_{\Gamma^{+}}
$$

This nonlinear Robin-type (mixed) boundary condition couples the local growth rate $V_n$ (itself determined by the thermal field via the Stefan condition, see §7) to the local solute concentration gradient in the melt.

### 5.3 Diffusion Boundary Layer Thickness

The boundary-layer thickness $\delta_c$ entering the BPS relation is estimated from the local hydrodynamic regime, either resolved directly by CFD or via standard correlations:

**Rotating disk (idealized CZ) correlation (Cochran–Levich):**

$$
\delta_c = 1.61\, D_l^{1/3} \, \nu^{1/6} \, \omega^{-1/2}
$$

where $\nu$ is the kinematic viscosity of the melt and $\omega$ is the crystal rotation rate.

**Forced-convection boundary layer (general):**

$$
\delta_c \sim \frac{D_l}{\mathrm{Sh}} L
$$

with $\mathrm{Sh}$ the Sherwood number (mass-transfer analog of Nusselt number) correlated as a function of Reynolds and Schmidt numbers:

$$
\mathrm{Sh} = f(\mathrm{Re}, \mathrm{Sc}), \qquad \mathrm{Sc} = \frac{\nu}{D_l}
$$

In fully resolved continuum simulations (CGSim, FEMAG-CZ, etc.), $\delta_c$ is not prescribed a priori but emerges implicitly from directly solving the coupled Navier–Stokes/species equations; the BPS formula is then used mainly as a diagnostic or reduced-order cross-check.

---

## 6. Constitutional/Thermodynamic Coupling

### 6.1 Liquidus Temperature Depression

The local liquidus temperature at the interface depends on the local melt composition:

$$
T_{\mathrm{liq}}^{*} = T_m + m_l \, C_l^{*}
$$

where $T_m$ is the melting point of the pure solvent and $m_l$ is the liquidus slope (negative for most dopant systems that lower the melting point). This couples segregation directly to the thermal field and to the shape/position of the growth interface, since the interface must satisfy $T^{*} = T_{\mathrm{liq}}^{*}(C_l^{*})$ — a **constitutional coupling** that can produce constitutional supercooling (§8).

### 6.2 Multicomponent / Multi-Dopant Systems

For simultaneous multiple solutes $C_l^{(i)}$, each species has its own $k_0^{(i)}$, $D_l^{(i)}$, and $m_l^{(i)}$, and the liquidus depression becomes (to first order):

$$
T_{\mathrm{liq}}^{*} = T_m + \sum_i m_l^{(i)} \, C_l^{(i)*}
$$

with cross-diffusion (Soret/Dufour-type) effects generally neglected in standard macroscopic growth codes unless explicitly modeled.

---

## 7. Coupling to Interface Shape and Growth Rate (Stefan Problem)

The normal interface velocity $V_n$ is not an independent input in most global models; it emerges from the **thermal Stefan condition**:

$$
\rho_s L_f \, V_n = k_s \frac{\partial T}{\partial n} \Big|_{\Gamma^{-}} - k_l \frac{\partial T}{\partial n} \Big|_{\Gamma^{+}}
$$

where $\rho_s$ is solid density, $L_f$ is latent heat of fusion, and $k_s, k_l$ are solid/liquid thermal conductivities. Because $V_n$ appears in both the thermal Stefan condition and the solute flux balance (§5.1–5.2), **segregation and interface morphology/growth-rate are two-way coupled**:

- Changes in local growth rate change local segregation ($k_{\mathrm{eff}}$ via BPS),
- Changes in local solute concentration change the local liquidus temperature (§6.1), which shifts the interface position/shape to maintain $T^{*} = T_{\mathrm{liq}}^{*}$, which in turn feeds back into $V_n$.

This bidirectional coupling is why segregation cannot, in general, be solved as a decoupled post-processing step in rigorous continuum simulations, though simplified/decoupled ("one-way coupled") approaches are common when solute concentrations are dilute enough that thermal feedback is negligible.

---

## 8. Constitutional Supercooling and Interface (In)stability

### 8.1 Criterion

When solute is rejected ahead of an advancing interface ($k_0 < 1$), a solute boundary layer forms in which the actual melt temperature $T(x)$ may fall below the local liquidus temperature $T_{\mathrm{liq}}(C_l(x))$ dictated by the solute profile — a condition called **constitutional supercooling**, which destabilizes a planar interface toward cellular/dendritic morphology. The classical criterion (linear stability, no convection) is:

$$
\frac{G}{V} < \frac{m_l\, C_{l,\infty} (1 - k_0)}{k_0 \, D_l}
$$

where $G$ is the temperature gradient in the liquid at the interface and $V$ the growth rate. Violation of this inequality (i.e., $G/V$ too small — high growth rate and/or low gradient) predicts interface breakdown.

### 8.2 Mullins–Sekerka Morphological Stability

A more general linear stability analysis (Mullins–Sekerka) extends this to perturbations of arbitrary wavelength, yielding a growth-rate-dependent critical wavelength band for instability, incorporating surface energy (Gibbs–Thomson) stabilization:

$$
T^{*} = T_{\mathrm{liq}}(C_l^{*}) - \Gamma_{\mathrm{GT}} \, \kappa
$$

where $\Gamma_{\mathrm{GT}}$ is the Gibbs–Thomson coefficient (surface energy divided by entropy of fusion per unit volume) and $\kappa$ is the local interface curvature. This term stabilizes short-wavelength perturbations, capping the destabilization predicted by constitutional supercooling alone.

While full morphological (cellular/dendritic) stability analysis is generally outside the scope of purely macroscopic/continuum global heat-transfer models (which assume a smooth, sharp interface), constitutional supercooling checks are frequently used as **a posteriori indicators** of when the macroscopic solution is physically inconsistent (i.e., predicts an unstable growth regime) and where microscale/mesoscale models (phase-field, cellular automaton) would be needed for a fully resolved treatment.

---

## 9. Global (Radial and Axial) Segregation Phenomena

### 9.1 Axial Segregation

Even under a spatially uniform $k_{\mathrm{eff}}$, progressive solute rejection into a finite melt volume causes bulk melt concentration $C_{l,\infty}(t)$ to evolve over the growth run, described (in the perfect-mixing limit, no boundary layer) by the **normal freezing / Scheil equation**:

$$
C_s^{*}(f_s) = k_0 \, C_0 \, (1 - f_s)^{k_0 - 1}
$$

where $C_0$ is the initial melt concentration and $f_s$ is the solidified fraction of the melt. Under **effective** (BPS) partitioning instead of full equilibrium mixing, the Scheil-type equation is modified to use $k_{\mathrm{eff}}$ in place of $k_0$:

$$
C_s^{*}(f_s) = k_{\mathrm{eff}} \, C_0 \, (1 - f_s)^{k_{\mathrm{eff}} - 1}
$$

This produces the characteristic **axial (longitudinal) segregation profile** observed along the growth axis of Czochralski, Bridgman, and related boules — solute-depleted near the seed end (for $k_0<1$) and progressively enriched toward the tail end.

### 9.2 Radial Segregation

Non-uniformity of the growth interface shape (convex/concave/flat), combined with radially non-uniform flow (buoyant convection cells, Coriolis effects from rotation, thermocapillary flow), produces radially varying local growth rate $V_n(r)$ and local boundary-layer thickness $\delta_c(r)$. Since $k_{\mathrm{eff}}$ depends on $V_n \delta_c / D_l$ (BPS relation, §3.2), this generates **radial segregation** — non-uniform dopant concentration across the crystal cross-section, often correlated with interface curvature.

### 9.3 Striations

Time-dependent, often periodic fluctuations in $V_n$ and in the flow field (e.g., from unsteady/turbulent thermal convection, rotational striae from asymmetric thermal fields combined with crystal rotation, or growth-rate fluctuations from temperature oscillations in the heater/furnace) produce microscopic banding in dopant concentration known as **growth striations**. In continuum models, these require time-dependent (transient) solution of the coupled flow/thermal/species fields, as steady-state global simulations cannot capture striation formation by construction.

---

## 10. Interfacial Kinetic (Non-Equilibrium) Segregation Beyond BPS

### 10.1 Kinetic Segregation Coefficient

At very high growth rates (rapid solidification regimes), attachment kinetics at the atomic scale become rate-limiting, and the interface cannot maintain local equilibrium even locally ($C_s^{*} \ne k_0 C_l^{*}$). A phenomenological **kinetic partition function**, commonly the Aziz continuous growth model, is used:

$$
k(V) = \frac{k_0 + \left(V / V_D\right)}{1 + \left(V / V_D\right)}
$$

where $V_D$ is a characteristic diffusive speed at the interface (of order interatomic distance divided by atomic vibrational/diffusive relaxation time). As $V \to \infty$, $k(V) \to 1$ (complete solute trapping, i.e. partitionless solidification).

This regime is generally outside standard bulk melt/solution growth conditions (CZ, Bridgman, VGF, LEC, Kyropoulos operate at growth rates far below $V_D$), so most macroscopic growth codes use the equilibrium $k_0$ with BPS correction (§3.2) rather than full kinetic models, but it is included here for completeness of the physically relevant phenomena at the interface.

---

## 11. Numerical/Computational Implementation Notes in Continuum Codes

1. **Interface tracking**: The interface $\Gamma$ is usually tracked as a deforming boundary (body-fitted moving mesh / Arbitrary Lagrangian-Eulerian, ALE) rather than captured implicitly (level-set/phase-field), consistent with the "sharp interface" continuum approach.
2. **Segregation as a boundary condition, not a bulk equation**: The partition law and flux balance (§5) are applied as boundary conditions on the species transport PDE (§4.1), not as separate bulk conservation laws.
3. **Iterative/coupled solution**: Because $V_n$, $T^{*}$, $C_l^{*}$, and interface shape are mutually dependent, most codes solve the coupled thermal–flow–species–interface system iteratively (e.g., Newton-type or fixed-point iteration) at each (pseudo-)time step, especially in quasi-steady global CZ/Bridgman simulations.
4. **Dilute-solution approximation**: Nearly all global growth codes assume dilute solute concentrations, allowing linearized liquidus slopes $m_l$, constant $k_0$, and negligible solutal buoyancy feedback on the flow field — though solutal buoyancy (density variation with $C_l$) can be included via an extended Boussinesq term when segregation levels are significant (e.g., heavily doped Si, SiGe, or oxide solid solutions).
5. **Decoupling for post-processing**: A common simplified workflow computes the thermal/flow field first (assuming the solute field does not feed back on the melt properties or interface shape), then solves the species transport equation as a post-processing step using the frozen velocity and interface-shape fields — valid only when solutal effects on density, viscosity, and liquidus temperature are small.

---

## 12. Summary Table of Governing Relations

| Phenomenon | Governing Relation |
|---|---|
| Equilibrium partitioning | $k_0 = C_s^{*}/C_l^{*}$ |
| Non-equilibrium (BPS) partitioning | $k_{\mathrm{eff}} = k_0 / [k_0 + (1-k_0)e^{-V\delta_c/D_l}]$ |
| Bulk species transport (melt) | $\partial_t C_l + \mathbf{u}\cdot\nabla C_l = D_l \nabla^2 C_l$ |
| Interfacial solute flux balance | $V_n(C_l^{*}-C_s^{*}) = -D_l \, \partial C_l/\partial n\Big|_{\Gamma}$ |
| Liquidus depression | $T_{\mathrm{liq}}^{*} = T_m + m_l C_l^{*}$ |
| Thermal Stefan condition | $\rho_s L_f V_n = k_s \partial_n T\Big|_{\Gamma^{-}} - k_l \partial_n T\Big|_{\Gamma^{+}}$ |
| Constitutional supercooling criterion | $G/V < m_l C_{l,\infty}(1-k_0)/(k_0 D_l)$ |
| Gibbs–Thomson curvature correction | $T^{*} = T_{\mathrm{liq}}(C_l^{*}) - \Gamma_{\mathrm{GT}}\kappa$ |
| Axial macrosegregation (BPS-modified Scheil) | $C_s^{*}(f_s) = k_{\mathrm{eff}} C_0 (1-f_s)^{k_{\mathrm{eff}}-1}$ |
| Kinetic partition (Aziz model) | $k(V) = [k_0 + V/V_D]/[1 + V/V_D]$ |

---

*Document prepared as a technical reference on continuum-scale segregation modeling in melt/solution crystal growth (Czochralski, Bridgman/VGF, Kyropoulos, LEC, and related methods).*


---

> [!NOTE]
> 
> Generated by Claude.ai
>
> Model: Sonet 5
>
> Prompt: Provide an exhaustive description of the Segregation at the Growth Interface in the Continuum (Macroscopic) Model of Melt/Solution Growth. Provide description of all physical relevant phenomena. For equation formulation use latex symbols and $$ delimiter. Show the output in Markdown format. Do not copy the output of the exported files into the chat.
