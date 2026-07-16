# Growth of Aluminium Phosphide (AlP) Single Crystals

## 1. Material Background

Aluminium phosphide (AlP) is a III–V compound semiconductor with the zincblende crystal structure, space group $F\bar{4}3m$, lattice constant $a \approx 5.4635\ \text{\AA}$. It is an indirect-bandgap semiconductor with $E_g \approx 2.45\ \text{eV}$ at room temperature, making it of interest for optoelectronic alloys (e.g. AlGaInP quaternaries used in visible LEDs and laser diodes) rather than as a standalone device material.

AlP is notoriously difficult to grow as a bulk single crystal because of two intrinsic material properties:

1. **High melting point and dissociation pressure.** AlP melts at approximately $2550\ \text{K}$ (some reports place congruent melting near $2823\ \text{K}$ under high pressure — literature values vary because AlP tends to decompose before reaching a clean melting point at ambient pressure).
2. **Strong chemical reactivity.** Aluminium has an extremely high affinity for oxygen; molten Al-rich material reacts violently with silica (crucible material), water vapor, and even nitrogen at high temperature. AlP also hydrolyzes in moist air, releasing phosphine ($\text{PH}_3$) — a toxic, pyrophoric gas.

Because of this, **AlP is essentially never grown by the melt-based bulk methods** used for GaAs, InP, or GaP (Czochralski, LEC, Bridgman/VGF). Instead, growth proceeds by one of:

- **Physical/Chemical Vapor Transport (PVT / CVT)** — the dominant method for bulk AlP crystals and platelets.
- **High-pressure solution growth** (Al-solution or flux growth) for small crystals.
- **Vapor-phase epitaxy (VPE), MOVPE, or MBE** — for thin epitaxial layers, usually as part of AlGaInP/AlGaAs heterostructures rather than bulk AlP.

Below is a detailed description of the vapor transport route, since it is the method by which actual bulk (though small) AlP single crystals have been obtained, followed by shorter treatments of the alternative routes.

---

## 2. Chemical Vapor Transport (CVT) Growth of AlP

### 2.1 Principle

CVT growth exploits a reversible chemical reaction between the solid source material and a transport agent (halogen or halide) that is endothermic or exothermic depending on direction, so that transport occurs from a source zone at temperature $T_1$ to a growth zone at temperature $T_2$ along a temperature gradient in a sealed ampoule.

For AlP, the most widely reported transport agent is **iodine** ($\text{I}_2$), though $\text{AlI}_3$ vapor generated in situ is the actual active transport species. A representative overall transport reaction is:

$$
\text{AlP(s)} + \tfrac{3}{2}\text{I}_2\text{(g)} \;\rightleftharpoons\; \text{AlI}_3\text{(g)} + \tfrac{1}{4}\text{P}_4\text{(g)}
$$

The equilibrium constant $K_p$ for this reaction is a strong function of temperature; because the reaction is endothermic in the forward direction, the equilibrium shifts to favor the gas-phase species at higher temperature. In a closed ampoule with a temperature gradient, source material at the hot end ($T_1$) volatilizes as $\text{AlI}_3$ and $\text{P}_4$/$\text{P}_2$ vapor, these species diffuse (or are convectively transported) across the gradient, and AlP redeposits at the cooler end ($T_2$), releasing $\text{I}_2$ which diffuses back to the source — closing the transport cycle.

### 2.2 Ampoule and Charge Preparation

- **Ampoule material:** fused silica (quartz), thoroughly cleaned, outgassed under vacuum at high temperature to remove adsorbed water (critical, since $\text{H}_2\text{O}$ reacts with AlP and with $\text{AlI}_3$).
- **Source charge:** polycrystalline AlP powder or lump material, synthesized beforehand (see §2.5) and loaded under inert atmosphere (glovebox) because AlP powder reacts with atmospheric moisture.
- **Transport agent loading:** iodine is added at a controlled concentration, typically on the order of $2$–$5\ \text{mg/cm}^3$ of ampoule volume. Too little iodine gives negligible transport rate; too much can lead to excessive nucleation and polycrystalline deposits rather than a few large single crystals.
- **Sealing:** the ampoule is evacuated to $\sim 10^{-5}$–$10^{-6}\ \text{Torr}$, often after a bake-out cycle, then flame-sealed under vacuum.

### 2.3 Furnace Configuration and Thermal Profile

A two- (or multi-) zone horizontal or vertical tube furnace is used, with independent temperature control of the source and growth zones. Typical reported conditions for AlP CVT:

| Parameter | Typical Value |
|---|---|
| Source zone temperature $T_1$ | $\sim 1050$–$1150\ ^\circ\text{C}$ |
| Growth zone temperature $T_2$ | $\sim 950$–$1050\ ^\circ\text{C}$ |
| Temperature gradient $\Delta T = T_1 - T_2$ | $\sim 50$–$100\ \text{K}$ over the ampoule length |
| Growth duration | days to a few weeks |
| Iodine concentration | $2$–$5\ \text{mg/cm}^3$ |

The ampoule is first brought to a uniform high temperature to homogenize and pre-react the charge, then the gradient is imposed. Transport direction (source hot, growth cool — "reverse" or "normal" transport, depending on the sign of $\Delta H$ of the transport reaction) must be established from the thermodynamics; for the AlI$_3$-mediated reaction above, the equilibrium favors vapor-phase species at the hotter end, so material transports from hot source to cooler growth zone.

### 2.4 Transport Rate and Mass Flux

The steady-state mass transport rate in the diffusion-limited regime can be estimated using a Nernst–Berthoud-type diffusion model:

$$
\dot{m} \;=\; \frac{D_{\text{eff}} \, A}{RT\,\bar{\ell}} \sum_i \nu_i \, p_i \, \Delta \ln K_p
$$

or, in simplified one-dimensional form commonly used for CVT rate estimation:

$$
\dot{m} = \frac{D \, A}{\bar{\ell}} \cdot \frac{p_1(\text{AlI}_3) - p_2(\text{AlI}_3)}{RT}
$$

where $D$ is the interdiffusion coefficient of the transport species in the ambient (dominated by $\text{I}_2$/$\text{AlI}_3$ partial pressures), $A$ is the ampoule cross-sectional area, $\bar{\ell}$ is the diffusion path length (source-to-growth zone distance), $T$ is the mean temperature, and $p_1, p_2$ are the partial pressures of the transporting species at the source and growth zone respectively (set by the local equilibria at $T_1$ and $T_2$).

In practice, growth rates for AlP CVT crystals are slow — crystal habit is typically small platelets or prisms of order millimeters, grown over one to several weeks. Larger boules are not achievable by this method; CVT is fundamentally limited to producing small single crystals or seed material rather than boules suitable for wafering.

### 2.5 Pre-synthesis of Polycrystalline AlP Source Material

Because commercial AlP source charge is not generally available in the same way as GaAs or InP, the source material is typically synthesized in situ or in a preliminary step by direct reaction of the elements:

$$
\text{Al(l)} + \text{P(g, s)} \;\longrightarrow\; \text{AlP(s)}
$$

This direct-synthesis route is itself hazardous, since it involves reacting molten aluminum with phosphorus vapor (from red or white phosphorus) at high temperature; the reaction is highly exothermic and phosphorus vapor pressure must be carefully controlled (often via a two-zone furnace: Al at high temperature in one zone, phosphorus source at a lower temperature in a second zone, with the phosphorus vapor pressure controlled by the phosphorus-zone temperature to avoid a runaway exothermic reaction or ampoule overpressure/explosion). Excess phosphorus overpressure is normally maintained during synthesis and the initial part of cool-down to suppress phosphorus loss and dissociation of the compound.

---

## 3. Alternative Route: High-Temperature Solution (Flux) Growth

Because congruent melting of AlP is impractical at ambient pressure, solution growth from an aluminum-rich melt has been explored:

- A **metal solvent** (typically excess Al, sometimes Sn or Ga-based solvents in principle, though Al-self-flux is most reported) is used to lower the effective liquidus temperature relative to congruent AlP melting.
- Phosphorus is dissolved into the Al-rich melt at controlled temperature ($\sim 1000$–$1200\ ^\circ\text{C}$ range, well below AlP's nominal melting point), and slow cooling or a temperature gradient drives supersaturation and AlP crystallization at a seed or on the crucible wall.
- The process must be conducted in a sealed, inert-atmosphere or evacuated ampoule (again quartz or sometimes BN-lined) to exclude oxygen and moisture, since molten Al is aggressively reducing toward oxide crucible materials.
- Crystal quality and size obtained by this route are generally modest (small crystallites), and contamination from crucible reaction and difficulty in achieving controlled nucleation are significant obstacles.

This method is conceptually the AlP analog of solution/flux growth used more successfully for other refractory compounds, but has seen far less development than CVT for AlP specifically.

---

## 4. Epitaxial Growth (Thin-Film AlP, Not Bulk)

For device-relevant material, AlP is essentially always grown as an epitaxial layer, lattice-matched or nearly lattice-matched to GaAs ($\Delta a/a \approx 0.65\%$), using:

- **Metal-Organic Vapor Phase Epitaxy (MOVPE/MOCVD):** trimethylaluminum (TMAl) and phosphine ($\text{PH}_3$) as precursors, typically at substrate temperatures of $650$–$750\ ^\circ\text{C}$, on GaAs substrates. Because AlP is highly reactive with oxygen and moisture even as a thin film, in-situ capping layers (e.g., GaAs or AlGaAs) are usually grown immediately on top to protect the AlP layer from atmospheric degradation once removed from the reactor.
- **Molecular Beam Epitaxy (MBE):** solid Al source and a cracked/valved phosphorus source (e.g., a valved cracker producing $\text{P}_2$), grown on GaAs substrates under ultra-high vacuum, again typically as thin layers within AlGaInP or AlGaAs-based heterostructures rather than as standalone thick films.

These epitaxial routes do not address bulk crystal growth but are the practical route by which AlP is actually incorporated into real devices (e.g., as a wide-gap window/cladding layer in red/orange/yellow AlGaInP LEDs).

---

## 5. Summary Comparison of Growth Routes

| Method | Crystal form obtained | Typical scale | Key challenges |
|---|---|---|---|
| CVT (I$_2$-transport) | Small single-crystal platelets/prisms | mm-scale | Slow growth, toxic PH$_3$/AlI$_3$ handling, no boule capability |
| Al-solution (flux) growth | Small crystallites | sub-mm to mm | Crucible reactivity, uncontrolled nucleation, limited development |
| MOVPE | Thin epitaxial films | µm-scale, on GaAs | Rapid oxidation/hydrolysis of exposed AlP, requires capping layer |
| MBE | Thin epitaxial films | µm-scale, on GaAs | Phosphorus source control (cracker), same oxidation issue |
| Direct melt (CZ/Bridgman) | **Not practical** | — | Melting point/dissociation pressure too high; incongruent behavior |

**Bottom line:** unlike GaAs, InP, or GaP, AlP has no established melt-growth technology for bulk boules. The dominant bulk-crystal method is iodine-mediated chemical vapor transport, producing only small single crystals, while all device-relevant AlP is grown as a thin epitaxial layer (MOVPE or MBE) on GaAs, always in combination with a protective capping layer due to AlP's extreme sensitivity to oxidation and hydrolysis.
