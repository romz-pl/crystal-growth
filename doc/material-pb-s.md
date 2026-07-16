# Growth of PbS Single Crystals (IV–VI Semiconductor)

## 1. Material Background

Lead sulfide (PbS, galena) is the archetypal member of the lead-chalcogenide (IV–VI, or more precisely Pb-VI) semiconductor family, alongside PbSe and PbTe. It crystallizes in the rock-salt (NaCl, $Fm\bar{3}m$) structure with lattice parameter $a \approx 5.936\ \text{Å}$, and is a narrow-gap semiconductor ($E_g \approx 0.41\ \text{eV}$ at 300 K, direct gap at the $L$-point of the Brillouin zone). It melts congruently at approximately 1391 K (1118 °C).

Growth of PbS is dominated by two coupled difficulties that distinguish it from more "conventional" III-V or II-VI melt growth:

1. **Extreme sensitivity of electrical properties to stoichiometry.** PbS is a nonstoichiometric compound with a very narrow homogeneity range around the 1:1 composition. Native point defects — Pb vacancies/interstitials and S vacancies/interstitials — act as shallow acceptors or donors, so carrier type and concentration are set almost entirely by the Pb/S ratio in the growth environment rather than by extrinsic dopants alone.
2. **High sulfur vapor pressure over the melt.** Because S (and $\text{S}_2$ / $\text{S}_x$ vapor species) are volatile relative to the PbS compound, melt growth in an open or poorly sealed system loses sulfur preferentially, driving the crystal toward the Pb-rich side of the phase field and altering carrier concentration along the growth axis.

These two facts govern essentially every design decision described below.

---

## 2. The Pb–S Phase Diagram and Its Consequences

The Pb–S system has been described thermodynamically using associated-solution models for the liquid (treating "Pb", "S", and "PbS" as coexisting species) combined with a point-defect (sublattice) model for the solid PbS phase, in which doubly ionized vacancies on the Pb and S sublattices are the dominant native defects responsible for the deviation from exact 1:1 stoichiometry. More recent CALPHAD assessments extend this to five-sublattice models that explicitly track interstitials, electrons, and holes, since PbS (like PbTe) cannot be treated as a strictly stoichiometric line compound.

Key implications for crystal growers:

- The **congruent melting point does not coincide exactly with the stoichiometric composition** — the liquidus maximum is displaced slightly toward one side of the phase field, and the exact displacement/sign depends on temperature.
- The **homogeneity range (width of the single-phase PbS field) is extremely narrow**, so small uncontrolled composition shifts during growth (evaporative sulfur loss, reaction with the ampoule wall, incomplete equilibration) move the crystal noticeably along the defect-concentration axis.
- Because equilibrium vapor pressure of the volatile species ($\text{S}_2$, Pb) changes by orders of magnitude across the homogeneity range, **the partial pressure of sulfur maintained over the charge during growth is the primary practical handle** for controlling n- or p-type conduction and carrier concentration — this is the same physical principle used in nonstoichiometry-controlled MBE and vapor growth of other IV–VI compounds (PbTe, PbSe).

A consequence documented in the classic Bridgman-growth literature on PbS is that **carrier concentration varies systematically along the length of a Bridgman-grown boule**, tracking the local departure from the congruent/stoichiometric point as the melt composition evolves during directional solidification — this is a direct manifestation of the phase diagram's narrow homogeneity range combined with segregation of the excess species.

---

## 3. Growth Methods

### 3.1 Bridgman (Vertical / Horizontal) Growth from the Melt

Bridgman growth is the most widely used bulk technique for PbS and is well documented historically (Lawson, Strauss, Short and coworkers).

**Procedure outline:**
1. High-purity Pb and S (or pre-reacted, pre-synthesized polycrystalline PbS) are loaded into a sealed ampoule — historically **graphite** ampoules or graphite-coated fused-silica ampoules, chosen to minimize reaction with the melt.
2. The charge is sealed under vacuum or under a controlled inert/sulfur partial pressure to fix the stoichiometry set-point, since an open system would boil off sulfur preferentially.
3. The ampoule is passed through a furnace with a temperature gradient straddling the PbS melting point (~1391 K), either by translating the ampoule through a fixed two- (or three-) zone furnace or by translating the furnace over a fixed ampoule.
4. Directional solidification proceeds from one end (often seeded), with the solid/liquid interface advancing at a controlled rate.

**Known outcomes and limitations:**
- Large, crack-free PbS boules can be obtained by the Bridgman technique using graphite ampoules, and their general metallurgical quality is typical of Bridgman-grown crystals (moderate dislocation density, some subgrain structure from thermal stress).
- A significant drawback is that graphite ampoules incorporate a measurable **carbon content into the crystal**, which must be considered when interpreting electrical and optical data.
- As predicted from the phase diagram, the **carrier concentration varies along the length of the boule**, reflecting the progressive shift in melt stoichiometry as growth proceeds (constitutional segregation of the excess Pb or S species into the residual melt).
- As with Bridgman growth generally, precise control of the solid/liquid interface shape (flat to slightly convex toward the melt) is important for defect control, and the growth rate tends to drift nonlinearly near the ends of the boule due to the "end effect" associated with finite crucible/ampoule length — more pronounced for shorter crucibles and smaller-diameter seeds.

### 3.2 Physical Vapor Transport (PVT) / Sublimation–Recondensation Growth

Because PbS sublimes appreciably below its melting point and the vapor-phase route avoids melt/container reactions, **physical vapor transport is a major alternative to melt growth** for IV–VI compounds generally, and is often preferred when higher crystalline perfection or reduced crucible contamination is required.

**Procedure outline:**
1. Polycrystalline PbS source material (or elemental Pb + S) is placed at the hot end of a sealed, evacuated ampoule (fused silica, evacuated to $10^{-4}$–$10^{-5}$ Pa is typical in related lead-chalcogenide processes).
2. A temperature gradient is imposed along the ampoule; the source sublimes, and PbS vapor species (molecular PbS, or dissociated Pb + S$_2$) diffuse/convect to the cooler end.
3. Vapor re-condenses at the cold end onto a seed (or nucleates spontaneously) to build the single crystal.
4. Growth rates are inherently slower than melt growth, and crystal diameters obtained by simple free sublimation transport are often modest (historically limited to on the order of a centimeter or less for good-quality single crystals), with long growth campaigns required.

**Variant — chemical vapor transport (CVT):** as used for related sulfides (SnS, Bi$_2$S$_3$), a transport agent (e.g., a halogen or halide such as I$_2$/AgI) can be introduced to form a volatile intermediate species that enhances the transport rate compared to pure sublimation, at the cost of introducing a transport-agent-related impurity that must be accounted for.

**Vapor-phase epitaxy (thin-film variant):** For thin, oriented single-crystal PbS layers rather than bulk boules, heteroepitaxial chemical vapor deposition onto water-soluble alkali-halide substrates (NaCl, KCl) has been demonstrated, exploiting a good structural match — PbS (100) grows registered to NaCl/KCl (100) with the in-plane $\langle 010 \rangle$ directions aligned — enabling later substrate dissolution to free-standing or transferred single-crystal PbS films for photodetector applications. This is a route to device-oriented single-crystal films rather than bulk boules and reflects a rock-salt-on-rock-salt epitaxial relationship exploiting the shared NaCl-type structure.

### 3.3 Melt–Vapor Combined ("Sealed-Tube Bridgman/Pulling with Vapor Equilibration") Methods

A documented industrial-style process for lead chalcogenides (PbS, PbSe, PbTe) combines melt growth with vapor-phase stoichiometry control in a single sealed quartz ampoule:
1. High-purity Pb and chalcogen (S) powders are weighed to the target molar ratio and sealed into an evacuated quartz tube (vacuum on the order of $10^{-4}$–$10^{-5}$ Pa).
2. The charge is heated in a vertical furnace to fully react and melt, forming PbS in situ.
3. The melt is superheated roughly 20 °C above the melting point to homogenize, then cooled back down toward the melting point.
4. The sealed ampoule is then pulled through the furnace gradient (Bridgman-type translation) at a slow rate — on the order of 5–7 mm/day, sustained for 7–10 days — yielding a single-crystal boule (diameters on the order of 25–30 mm reported for this class of process).

This approach is essentially melt-growth Bridgman under a self-generated equilibrium vapor pressure of the volatile species inside the sealed ampoule, which is what allows reasonable control of the Pb:S ratio without an externally imposed vapor source.

---

## 4. Stoichiometry and Defect Control Strategies

Because electrical properties are set primarily by native defects rather than extrinsic dopants, practical PbS growth protocols emphasize:

- **Sealed-system growth** (evacuated, sealed ampoules) to prevent uncontrolled loss of sulfur vapor, which would otherwise drive the crystal Pb-rich and shift the majority carrier type/concentration.
- **Post-growth annealing under a controlled chalcogen (S$_2$) partial pressure**, analogous to established practice for PbTe/PbSe, to homogenize the Pb:S ratio throughout the boule and adjust carrier concentration toward a target value by equilibrating the crystal against an external vapor reservoir at a chosen temperature.
- **Minimizing container reactions**: quartz ampoules can react with Pb-rich melts/vapors at high temperature; graphite ampoules avoid some of these reactions but introduce carbon incorporation. The choice of container material is therefore a trade-off between chemical inertness and impurity incorporation.
- **Doping** (e.g., with group-I, group-III, or halogen impurities used historically in lead-chalcogenide work) can supplement native-defect control once the intrinsic Pb:S ratio is stabilized, but is generally secondary to stoichiometry control given the narrow homogeneity range.

---

## 5. Comparative Summary of Growth Routes

| Method | Typical Scale | Key Advantage | Key Limitation |
|---|---|---|---|
| Bridgman (graphite ampoule) | Large boules, cm-scale | Large, crack-free crystals achievable | Carbon incorporation; axial carrier-concentration gradient from stoichiometry drift |
| Sealed-tube melt/Bridgman with vapor equilibration | ~25–30 mm diameter boules | Reasonable stoichiometry self-control via sealed vapor | Slow growth rates (mm/day scale), multi-day process |
| Physical vapor transport (sublimation) | Small crystals, often < 1 cm | Avoids melt/container reactions; can give high perfection | Slow, small crystal size, long run times |
| Chemical vapor transport (with transport agent) | Small–moderate crystals | Faster transport than pure sublimation | Transport-agent impurity incorporation |
| Vapor-phase epitaxy on NaCl/KCl | Thin films | Oriented, device-ready single-crystal films; substrate is water-dissolvable | Not a bulk-boule method; substrate-limited film area |

---

## 6. Summary

PbS crystal growth is governed less by classical melt-growth fluid dynamics (though interface shape and growth-rate control remain relevant, as in any Bridgman process) and more by the **thermodynamics of a narrow-homogeneity-range nonstoichiometric compound with a volatile chalcogen component**. Practical single-crystal growth — whether by sealed-ampoule Bridgman, vapor transport, or vapor-phase epitaxy — is fundamentally an exercise in controlling the Pb:S ratio (via sealed-system vapor pressure, post-growth annealing, or transport-agent chemistry) in order to fix the native point-defect population that ultimately determines carrier type and concentration in the finished crystal.

---

### Selected Literature Basis

- N.R. Short, W.D. Lawson, A.J. Strauss et al. — foundational Bridgman-growth studies of PbS, carrier concentration vs. position along boules.
- Thermodynamic/CALPHAD assessments of the Pb–S(–Te) system using associated-solution liquid models and point-defect sublattice models for solid PbS.
- Patent literature (e.g., CN100344802C) describing sealed quartz-tube melt/Bridgman pulling of PbS/PbSe/PbTe with controlled pull rates.
- Vapor-phase epitaxial CVD growth of PbS single-crystal films on NaCl/KCl substrates for optoelectronic applications (*Nano Research*, 2022).
- General reviews of nonstoichiometry-driven carrier-concentration control in IV–VI compound growth (MBE and bulk).
