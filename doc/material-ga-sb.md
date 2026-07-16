# Growth of GaSb Single Crystals: A Detailed Process Description

## 1. Material Background

Gallium antimonide (GaSb) is a III–V semiconductor with the zinc-blende crystal structure, a lattice constant of $a_0 = 6.0959\ \text{Å}$, and a direct bandgap of $E_g \approx 0.72\ \text{eV}$ at room temperature. It is used for thermophotovoltaic cells, mid-infrared laser diodes and detectors, tandem solar cells (as a substrate lattice-matched to InGaAsSb and related alloys), and as a substrate for antimonide-based heterostructures (e.g., InAs/GaSb type-II superlattices).

Key physical properties relevant to growth:

- Congruent melting point: $T_m = 712\,^{\circ}\mathrm{C}$ ($985\ \text{K}$)
- Density (solid): $\rho_s \approx 5.61\ \text{g/cm}^3$; density (liquid) is higher, so GaSb — like Ge and InSb — **contracts** upon melting rather than expanding (density inversion behavior partially resembles Ga-rich systems)
- Congruent (non-dissociative) melting, unlike GaAs or GaP, which simplifies stoichiometry control since no separate group-V overpressure is strictly required
- Very low critical resolved shear stress and low mechanical hardness compared to GaAs, making GaSb boules prone to dislocation generation and slip under thermal stress
- High native point-defect concentration: undoped GaSb is invariably **p-type** due to a high concentration of Ga-antisite-related acceptor complexes ($V_{Ga}$–$Ga_{Sb}$), typically $p \sim 10^{17}\ \text{cm}^{-3}$ even in "undoped" material

## 2. Overview of Growth Methods

GaSb is grown almost exclusively from the melt, since (unlike GaAs) it melts congruently at a moderate temperature and has no significant dissociation pressure problem. The dominant techniques are:

| Method | Typical Use Case | Dislocation Density | Diameter Achievable |
|---|---|---|---|
| Vertical Gradient Freeze (VGF) / Vertical Bridgman (VB) | Commercial substrate production | $10^2$–$10^4\ \text{cm}^{-2}$ | up to 4–6 inch |
| Horizontal Bridgman (HB) | Research, smaller boules | $10^2$–$10^3\ \text{cm}^{-2}$ | 2–3 inch (D-shaped) |
| Czochralski (CZ) / Liquid-Encapsulated Czochralski (LEC) | Round boules, higher throughput | $10^3$–$10^5\ \text{cm}^{-2}$ | up to 4 inch |
| Zone melting / Traveling Heater Method (THM) | Purification, low-defect research crystals | can be very low | small diameter |

Because GaSb melts congruently and has a low vapor pressure of Sb at the melting point, **no encapsulant boric oxide layer is strictly needed** the way it is for GaAs LEC growth, although some LEC variants still use $B_2O_3$ for thermal symmetry and to suppress Sb evaporation losses over long runs.

The remainder of this document details the **Vertical Bridgman / Vertical Gradient Freeze (VB/VGF)** process, since it is the industry-standard route for GaSb substrate production, and then discusses the **Czochralski** alternative.

## 3. Vertical Bridgman / VGF Growth of GaSb

### 3.1 Charge Preparation

1. **Elemental synthesis**: 6N–7N purity gallium and antimony are weighed in stoichiometric ratio (1:1 atomic) and loaded into a pyrolytic boron nitride (pBN) or quartz ampoule.
2. **Synthesis/homogenization**: The ampoule is evacuated and sealed under vacuum ($<10^{-5}\ \text{torr}$) or backfilled with an inert gas, then heated above $T_m$ to synthesize polycrystalline GaSb via direct reaction. Because the reaction is only mildly exothermic (compared to GaAs) and the vapor pressure of Sb over the melt is low, sealed-ampoule synthesis is comparatively gentle and safe.
3. **Doping**: Intentional dopants (Te for n-type, Zn for p-type, Sn as an alternative n-type dopant) are added to the polycrystalline charge at this stage. Because undoped GaSb is intrinsically p-type from native defects, achieving n-type material requires overcompensating with a donor at concentrations exceeding the native acceptor background.

### 3.2 Seeding and Ampoule Configuration

1. A single-crystal seed, oriented typically along $\langle 111 \rangle$ or $\langle 100 \rangle$, is placed at the bottom (VB) or in a shaped seed-well (VGF) of the crucible.
2. The crucible (commonly pBN, sometimes carbon-coated quartz) has a tapered or conical bottom to promote necking-down to a single grain from the seed.
3. The charge and seed assembly are loaded into the furnace ampoule, typically with a small overpressure of inert gas or a controlled Sb vapor source to suppress antimony loss during growth, since Sb has a non-negligible equilibrium vapor pressure near $T_m$.

### 3.3 Thermal Profile and Growth

The VB/VGF method relies on translating a temperature gradient (fixed multi-zone furnace, VGF) or the ampoule itself (VB) so that the solid–liquid interface advances progressively from the seed through the melt.

- **Gradient freeze principle**: A furnace with independently controlled hot and cold zones is used; the temperature profile is shifted axially (electronically, without mechanical translation, in VGF) or the ampoule is lowered (in VB) through a fixed axial gradient.
- **Axial thermal gradient**: Typically kept low, on the order of $2$–$10\ \text{K/cm}$ near the interface, to minimize thermal stress and dislocation generation, given GaSb's low critical resolved shear stress.
- **Growth rate**: Typically $1$–$10\ \text{mm/h}$, chosen slow enough to maintain a stable, nearly planar solid–liquid interface and avoid constitutional supercooling, particularly important because of the significant segregation of common dopants in GaSb.
- **Interface shape control**: A slightly convex (into the melt) interface is generally preferred to sweep dislocations toward the crystal periphery, but excessive convexity increases radial thermal stress. This is a central trade-off addressed by numerical modelling of the furnace's heat transfer (radiative and conductive) and, where convection is present, coupled melt flow.

Governing heat-transport balance at the moving interface (Stefan condition):

$$
k_s \left.\frac{\partial T}{\partial z}\right|_{s} - k_l \left.\frac{\partial T}{\partial z}\right|_{l} = \rho_s L\, v_g
$$

where $k_s, k_l$ are solid/liquid thermal conductivities, $L$ is the latent heat of fusion, and $v_g$ is the local growth velocity.

### 3.4 Dopant Segregation

Dopant incorporation along the boule length follows the normal-freezing (Scheil) relation when back-diffusion in the solid is negligible:

$$
C_s(f_s) = k_0\, C_0\, (1-f_s)^{k_0 - 1}
$$

where $C_0$ is the initial melt dopant concentration, $f_s$ is the fraction solidified, and $k_0$ is the equilibrium segregation coefficient. For GaSb, reported effective segregation coefficients include $k_0(\text{Te}) \approx 0.3$–$0.5$ and $k_0(\text{Zn}) \approx 0.02$–$0.1$, both substantially less than unity, producing pronounced axial resistivity gradients along the boule that must be characterized and sometimes compensated by melt replenishment or controlled convective mixing.

### 3.5 Post-Growth Cooling

After complete solidification, the boule is cooled slowly through the range near $T_m$ down to room temperature at a controlled rate (often a few tens of K/h near the melting point, faster thereafter) to minimize thermally induced dislocation multiplication and cracking, since GaSb's thermal expansion mismatch with the crucible material and its low fracture toughness make it prone to cracking on rapid cooling.

## 4. Czochralski / LEC Growth of GaSb (Alternative Route)

1. Polycrystalline GaSb charge is melted in a crucible (often pBN or graphite-lined) under inert atmosphere; a thin $B_2O_3$ encapsulant layer may be used to suppress Sb evaporation and reduce radial temperature asymmetry, although it is less critical than in GaAs LEC due to GaSb's lower Sb equilibrium vapor pressure at $T_m$.
2. A seed crystal is dipped into the melt surface, necked down to a small diameter to eliminate grown-in dislocations from the seed (Dash-necking technique), then shouldered out to full diameter.
3. The crystal is pulled upward at rates of order $1$–$3\ \text{mm/min}$ while both crystal and crucible are counter-rotated to average out azimuthal thermal asymmetries and control the melt convection pattern.
4. Because GaSb has a low critical resolved shear stress, dislocation densities in CZ/LEC GaSb tend to be higher than in Bridgman/VGF material unless very carefully optimized low-gradient "fully encapsulated" LEC conditions are used.
5. Diameter control is achieved by adjusting pull rate and heater power in response to real-time meniscus/weight-sensing feedback, following the standard Czochralski diameter-control control-loop approach used across melt-grown semiconductors.

## 5. Characterization and Quality Metrics

After growth, boules are typically evaluated by:

- **Etch pit density (EPD)** via molten KOH or other selective etchants to reveal dislocations
- **Hall effect measurements** along the boule length to map carrier concentration and mobility versus $f_s$, cross-checked against the Scheil segregation prediction
- **X-ray diffraction (rocking curve)** to assess crystallographic quality and misorientation
- **Infrared transmission/absorption** to check free-carrier absorption consistent with doping level
- **Wafering and lapping/polishing** to produce substrates, followed by chemo-mechanical polishing (CMP) to achieve epi-ready surface finish for subsequent MBE/MOCVD growth of antimonide device structures

## 6. Summary of Key Trade-offs

| Parameter | Effect if too high | Effect if too low |
|---|---|---|
| Axial thermal gradient | More dislocations, thermal stress | Interface instability, constitutional supercooling |
| Growth rate | Constitutional supercooling, poly-crystallization | Impractically long run times, excessive dopant back-segregation effects |
| Convex interface curvature | Radial stress, dislocation multiplication | Poor dislocation sweep-out, higher core defect density |
| Cooldown rate | Cracking, dislocation multiplication | Long cycle time, reduced throughput |

GaSb crystal growth is therefore fundamentally a compromise between maintaining a stable, near-planar or gently convex solidification interface, controlling dopant segregation, and limiting thermal stress in a mechanically soft, easily dislocated lattice — considerations shared conceptually with Ge and InSb growth but distinct from the dissociative, high-vapor-pressure challenges of GaAs and InP.
