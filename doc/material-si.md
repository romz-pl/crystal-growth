# Growth of Silicon (Si) Single Crystals

## 1. Overview and Context

Silicon is the dominant elemental semiconductor for microelectronics and photovoltaics, and its single-crystal growth is arguably the most mature and highest-volume crystal growth process in industry. Two methods account for nearly all commercial and research-grade Si single crystals:

- **Czochralski (CZ) growth** — the workhorse for microelectronics-grade and most solar-grade material, producing >90% of the world's single-crystal Si.
- **Float Zone (FZ) growth** — a crucible-free technique used where extreme purity and high resistivity are required (power devices, detectors, some solar cells).

Both start from metallurgical-grade silicon that has been purified via the Siemens process (trichlorosilane reduction) to **electronic-grade polysilicon** (EG-Si), with total impurity content below ~1 ppb for critical dopants.

---

## 2. Feedstock Preparation

1. **Metallurgical-grade Si (MG-Si)**: produced by carbothermic reduction of quartz (SiO₂) in an arc furnace, purity ~98–99%.
2. **Conversion to trichlorosilane (SiHCl₃)**: MG-Si reacts with HCl at ~300 °C in a fluidized bed reactor.
3. **Distillation**: repeated fractional distillation removes boron, phosphorus, and metallic impurity chlorides.
4. **Siemens deposition**: SiHCl₃ vapor is decomposed on resistively heated Si "slim rods" at ~1100 °C via chemical vapor deposition (CVD), building up polysilicon rods to high purity (9N–11N, i.e., 99.9999999%+).
5. Alternative: **Fluidized Bed Reactor (FBR)** process using silane (SiH₄) decomposition onto Si seed particles — lower cost, granular product, increasingly used for solar-grade feedstock.

This polysilicon is the raw charge material for both CZ and FZ growth.

---

## 3. Czochralski (CZ) Growth of Silicon

### 3.1 Process Description

1. **Charge melting**: polysilicon chunks are loaded into a high-purity fused-quartz crucible, itself supported in a graphite susceptor, inside a puller furnace under inert atmosphere (typically Ar, sometimes with controlled partial pressure) and often reduced pressure.
2. **Melting**: RF or resistive heating brings the charge above the Si melting point, $T_m = 1414\,^\circ\text{C}$.
3. **Dopant addition**: dopants (B for p-type, P/As/Sb for n-type) are added to the melt to achieve target resistivity.
4. **Seeding**: a small, precisely oriented seed crystal (commonly $\langle 100 \rangle$ or $\langle 111 \rangle$) is dipped into the melt surface.
5. **Necking (Dash technique)**: the seed is withdrawn rapidly to form a thin neck (2–4 mm diameter), which eliminates dislocations generated at the seed–melt thermal shock interface — dislocations cannot propagate along $\langle 111 \rangle$ slip planes into a sufficiently thin neck.
6. **Crown/shoulder growth**: pull rate is reduced and the crystal diameter is expanded to the target diameter by controlling the balance of pull rate and melt temperature.
7. **Body growth**: constant-diameter growth is sustained via a closed-loop control system, typically using an optical diameter sensor tracking the meniscus bright ring, adjusting pull rate $v_p$ and/or heater power.
8. **Tail-off (end cone)**: pull rate and power are ramped to taper the diameter to zero before separating from the melt, avoiding thermal-shock-induced dislocations at the end of growth.

### 3.2 Governing Physics

**Interface thermal balance (Stefan-type condition).** At the solid–liquid interface, latent heat release must balance the net conductive heat flux difference:

$$
\rho_s L \, v_p = k_s \left.\frac{\partial T}{\partial z}\right|_{s} - k_l \left.\frac{\partial T}{\partial z}\right|_{l}
$$

where $\rho_s$ is solid density, $L$ the latent heat of fusion, $k_s$, $k_l$ the solid/liquid thermal conductivities, and $v_p$ the growth (pull) velocity.

**Maximum pull rate** is set by the requirement that the crystal can conduct away latent heat plus incoming radiative/convective heat load; empirically the CZ maximum growth rate scales with the axial temperature gradient in the solid near the interface,

$$
v_{p,\max} \approx \frac{k_s}{\rho_s L}\left.\frac{\partial T}{\partial z}\right|_{s}
$$

**Melt convection.** The CZ melt pool is driven by:
- **Buoyancy (natural) convection**, characterized by the thermal Rayleigh number

$$
Ra = \frac{g\,\beta\,\Delta T\,R^3}{\nu\,\alpha}
$$

- **Marangoni (thermocapillary) convection** at the free melt surface, characterized by

$$
Ma = \frac{\left|\dfrac{\partial \sigma}{\partial T}\right|\Delta T\, R}{\mu\,\alpha}
$$

- **Forced convection** from crystal and crucible rotation (often counter-rotated), characterized by rotational Reynolds numbers $Re_{cr} = \Omega_{cr} R_{cr}^2/\nu$ and $Re_{xtl} = \Omega_{xtl} R_{xtl}^2/\nu$.

For large-diameter modern CZ pullers (200–450 mm crystals), $Ra$ is very high ($10^7$–$10^9$), placing the melt flow in an oscillatory or turbulent regime, which is the principal source of microscopic growth-rate fluctuations and striations.

### 3.3 Dopant Segregation

Dopant incorporation is governed by the effective segregation coefficient:

$$
k_{\rm eff} = \frac{k_0}{k_0 + (1-k_0)\exp(-v_p \delta / D_l)}
$$

where $k_0$ is the equilibrium segregation coefficient (e.g., $k_0 \approx 0.8$ for B, $\approx 0.35$ for P in Si), $\delta$ is the boundary-layer thickness set by melt convection, and $D_l$ the dopant diffusivity in the melt. Because $k_0 \neq 1$ for all dopants in Si, axial resistivity gradients ("normal freezing" per the Scheil equation) and radial striations (from $v_p$ fluctuations coupled to $k_{\rm eff}$) are intrinsic features requiring control.

### 3.4 Point Defects and Microdefects

CZ Si crystal quality is dominated by the balance of intrinsic point defects — vacancies (V) and self-interstitials (I) — whose incorporation is governed by the **Voronkov criterion**:

$$
\frac{v_p}{G} \; \gtrsim \; \xi_{\rm crit}
$$

where $G$ is the axial temperature gradient at the interface and $\xi_{\rm crit} \approx 1.3 \times 10^{-3}\ \text{cm}^2\,\text{min}^{-1}\,\text{K}^{-1}$ (V/I boundary). Growth at $v_p/G$ above this threshold yields vacancy-rich material (prone to voids/COPs — Crystal Originated Particles), while below it yields interstitial-rich material (prone to dislocation loops); the industry aims for a narrow "perfect" or near-perfect denuded zone around this crossover.

### 3.5 Variants

- **MCZ (Magnetic CZ)**: an axial, transverse, or cusp-shaped magnetic field damps melt convection (via magnetohydrodynamic braking), reducing oxygen incorporation and striations. The effective viscosity increase scales with the Hartmann number $Ha = B R \sqrt{\sigma/(\rho \nu)}$.
- **Continuous CZ (CCZ)**: melt is continuously replenished from a secondary chamber, decoupling axial dopant/oxygen drift from melt depletion.

---

## 4. Float Zone (FZ) Growth of Silicon

### 4.1 Process Description

FZ growth is **crucible-free**, eliminating the dominant oxygen/carbon contamination pathway of CZ (crucible dissolution).

1. A vertical polycrystalline Si rod (from the Siemens process) is mounted with a seed crystal at the bottom.
2. An RF induction coil creates a narrow **molten zone** that is passed along the rod.
3. Surface tension alone supports the melt against gravity across the (small) unsupported zone — the **Pfann/Heffner floating-zone stability limit** restricts the maximum stable molten-zone diameter, given approximately by

$$
d_{\max} \approx 2\left(\frac{2\sigma}{\rho\, g}\right)^{1/2}
$$

for Si ($\sigma \approx 0.72\ \text{N/m}$, $\rho \approx 2530\ \text{kg/m}^3$ liquid), limiting practical FZ ingot diameters to roughly 100–150 mm without additional support fields, versus 450 mm achievable in CZ.
4. Multiple zone passes can be used for **zone refining**, exploiting $k_0 \neq 1$ to sweep impurities to one end.
5. Dopants may be introduced by **gas-phase (PF₅/B₂H₆) doping** during zone passage, or by neutron transmutation doping (NTD) of high-purity FZ rods post-growth (used for high-voltage power devices).

### 4.2 Governing Physics

- **No crucible contact** removes the oxygen source present in CZ; FZ Si typically has oxygen concentrations orders of magnitude below CZ Si (down to background/detection limits vs. $10^{17}$–$10^{18}\ \text{cm}^{-3}$ in CZ).
- **Needle-eye / RF coil design** concentrates induction heating in a thin band, maintaining a narrow, well-defined molten zone.
- **Melt-zone shape and stability** depend on the balance of surface tension, gravity, and electromagnetic (Lorentz) pressure from the RF coil, which can be used deliberately to help support larger zones.
- **Thermal gradients** at both interfaces (lower solidifying, upper melting) are steeper than in CZ, permitting different microdefect and dislocation dynamics; dislocation-free growth again relies on a thin-neck technique analogous to CZ.

### 4.3 Applications

FZ Si is preferred for:
- High-voltage power semiconductor devices (thyristors, IGBTs) requiring float-zone-grade resistivity uniformity and near-total absence of oxygen-related defects.
- Radiation detectors and high-resistivity substrates.
- Certain high-efficiency solar cells.

---

## 5. Comparative Summary

| Aspect | Czochralski (CZ) | Float Zone (FZ) |
|---|---|---|
| Crucible contact | Yes (fused quartz) | None |
| Max practical diameter | Up to 450 mm | ~100–150 mm |
| Oxygen content | High ($10^{17}$–$10^{18}\ \text{cm}^{-3}$) | Very low |
| Dopant uniformity | Segregation-limited; MCZ/CCZ improve control | Excellent via multi-pass zone refining, or NTD |
| Typical use | Microelectronics, most PV | Power devices, detectors, premium PV |
| Throughput / cost | High throughput, lower cost | Lower throughput, higher cost |

---

## 6. Post-Growth Characterization and Processing

Following growth, ingots undergo:
- **Diameter grinding** to precise cylindrical tolerance.
- **Wafer slicing** (wire saws), lapping, etching, and polishing (CMP).
- **Resistivity mapping** (four-point probe) and **defect characterization** (FTIR for oxygen/carbon, X-ray topography or defect etching for dislocations/COPs, minority-carrier lifetime mapping).
- For device-grade wafers, **epitaxial layers** may be deposited to place the active device region in a controlled, defect-engineered near-surface layer distinct from the bulk crystal.

---

## 7. Key References for Further Reading

- Voronkov, V.V., "The mechanism of swirl defects formation in silicon," *J. Cryst. Growth* 59 (1982).
- Dash, W.C., "Silicon crystals free of dislocations," *J. Appl. Phys.* 30 (1959).
- Müller, G. & Friedrich, J., chapters on melt growth in *Handbook of Crystal Growth*, 2nd ed. (Elsevier).
- Zulehner, W., "Czochralski growth of silicon," *J. Cryst. Growth* 65 (1983).
