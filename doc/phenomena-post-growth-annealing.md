# Post-Growth Annealing in Crystal Growth from the Melt

## 1. Scope and Definition

*Post-growth annealing* refers to controlled thermal treatments applied to a melt-grown crystal (or wafers cut from it) **after** solidification is complete, as distinct from:

- **In-growth thermal control** — the axial/radial temperature gradients $G_0$ and pulling/growth rate $v$ imposed *during* solidification (e.g. the Voronkov criterion $v/G_0$ governing vacancy/interstitial dominance in Czochralski silicon);
- **Post-growth cooling** — the (often uncontrolled) descent from the solidification temperature $T_m$ to room temperature immediately following growth, which is itself frequently the dominant source of the defects that post-growth annealing is designed to remedy;
- **Device-process annealing** — thermal budgets applied much later during wafer fabrication (oxidation, diffusion, RTA), which are outside melt-growth technology proper but interact with grown-in defect populations.

Post-growth annealing sits at the interface of these regimes: it is a *deliberate, separately-controlled* thermal step (in-situ in the growth furnace, or ex-situ in a dedicated furnace) whose purpose is to modify the defect, stress, stoichiometry, or dopant/impurity state of an already-solidified crystal without re-melting it.

## 2. Physical Objectives of Post-Growth Annealing

### 2.1 Relief of Thermoelastic Stress and Control of Post-Growth Dislocations

During melt growth, especially in Czochralski (CZ), Bridgman/VGF, and related methods, radial and axial temperature gradients in the still-hot crystal generate thermoelastic stresses. Where these exceed the critical resolved shear stress at the local temperature, plastic relaxation occurs via dislocation glide and multiplication — described by Haasen–Alexander–Sumino (H-A-S) type viscoplastic constitutive laws coupling dislocation density evolution to stress and temperature, and by Jordan-type purely thermoelastic stress models used as a first estimatewhere dislocation generation is thermal stress driven, with the Haasen–Alexander model coupling dislocation multiplication and creep strain rates compared against the Jordan model based on thermoelastic stresses. Critically, dislocation generation is not confined to the growth front: post-growth dislocations are not connected with the growth front and instead form at a later stage of growth or during cooling after growth, arising mainly from stress-relaxing dislocation glide. In crystals grown in their plastic regime, the as-grown dislocation geometry may be substantially altered by post-growth glide of growth dislocations and by the generation of entirely new post-growth dislocations.

Controlled annealing (slow, programmed cooling, or an isothermal hold below $T_m$) is used to let the crystal relax stress by dislocation motion at a rate/temperature combination that limits multiplication, rather than allowing uncontrolled cooling gradients to drive uncontrolled glide and pattern formation (dislocation cells, low-angle boundaries, polygonization). At the continuum-thermodynamic level, plastic work during this relaxation is mainly dissipated as heat, with the remainder stored as elastic dislocation energy in a process far from equilibrium that promotes self-organized dissipative structures such as periodic and cellular dislocation patterns. Managing the post-growth thermal history is therefore a direct lever on which self-organized defect microstructure the crystal ends up with.

### 2.2 Reduction of Grown-in Point-Defect Aggregates (Voids/COPs, Interstitial Clusters)

In CZ silicon, grown-in vacancy agglomerates (crystal-originated particles, COPs) and their inner oxide linings are a principal target of post-growth annealing. High-temperature annealing in a reducing or inert ambient ($\text{H}_2$, Ar, or mixtures) dissolves the oxide layer lining the void walls and allows interstitial silicon to backfill the voids: high-temperature annealing in hydrogen, inert gas, or mixtures causes out-diffusion of oxygen near the surface, dissolves the oxide films lining the grown-in voids since oxygen becomes unsaturated, and the voids are eliminated by interstitial silicon supplied under near-equilibrium conditions. This is not perfect near the surface: substantial residues of these defects can remain even a micron below the wafer surface, degrading the near-surface region relevant to device yield, which is why anneal schedules (temperature, ambient, ramp rate, duration) are engineered rather than a single fixed recipe. Quantitatively, the depth-dependence of COP dissolution can be modelled from initial COP size and oxygen concentration together with concurrent oxygen precipitation kinetics, giving depth profiles of remaining defects that match measurements well — i.e. post-growth annealing outcomes are now reasonably predictable from coupled void-dissolution/precipitation models rather than purely empirical.

### 2.3 Control of Oxygen and Dopant Precipitation

CZ silicon incorporates oxygen from the quartz crucible during growth; its distribution and precipitation behavior downstream are annealing-sensitive. Oxygen precipitates must reach a certain size and density to getter metallic impurities effectively, and nitrogen doping is used to homogenize oxygen precipitation during high-temperature annealing in wafers optimized against void formation. The *non-equilibrium point-defect concentration* frozen in during growth strongly affects subsequent behavior: the vacancy concentration present during precipitate growth affects the recombination activity of the resulting oxygen precipitates, and non-equilibrium point-defect concentrations measurably affect both precipitate and dislocation growth during anneal. Separately, COP density and size distribution in CZ silicon can be tuned via pulling rate and post-growth cooling conditions, and high-temperature annealing reduces defect size and partially dissolves COPs, whereas no COPs are observed at all in float-zone or epitaxial material — underscoring that post-growth annealing is compensating for a defect population that is intrinsic to the CZ process itself.

### 2.4 Stoichiometry Correction and Electrical Compensation in Compound Semiconductors

In II–VI and related compound crystals (CdTe, CdZnTe, etc.), post-growth annealing is often the *primary* route to usable electrical properties rather than a secondary cleanup step, because as-grown material is far from the stoichiometric, electrically compensated state needed for device use (e.g. semi-insulating radiation-detector-grade CdTe:Cl). Annealing under a controlled component (Cd or Te) partial pressure shifts native point-defect equilibria (vacancies, antisites, and their complexes with the dopant) to achieve charge compensation and high resistivity — treated in detail in the classical point-defect thermodynamics literature (Kröger) and in dedicated postgrowth-annealing studies of CdTe:Cl.

### 2.5 Recrystallization and Ordering in Thin/Epitaxial and Non-Bulk Melt-Adjacent Growth

Although the present overview centers on bulk melt growth, the same annealing logic (thermally driven atomic rearrangement toward a lower-defect, more ordered state) appears in adjacent growth technologies. In MOCVD-grown wafer-scale hexagonal boron nitride, high-temperature post-growth annealing markedly improves both structural and optical properties, with the crystallinity and homogeneity enhancement attributed to solid-state atomic rearrangement during annealing, accompanied by the appearance of excitonic photoluminescence and an enlarged optical band gap in the annealed films. In 2D transition-metal dichalcogenide-type films, post-growth annealing at high temperature drives three-dimensional structural reorganization, with a marked improvement in out-of-plane crystallinity, reduced defect density, and rearrangement of grain boundaries observed by GIXRD and STEM, and dislocation and grain-boundary migration in these 2D systems proceeds via in-plane displacement of a few atoms around the dislocation core, unlike bulk 3D systems. These cases illustrate the same generic mechanism — thermally activated defect migration/annihilation and grain-boundary rearrangement — operating in a different (2D, in-plane) geometry than bulk thermoelastic relaxation.

## 3. Governing Mechanisms

| Mechanism | Driving force | Characteristic model / description |
|---|---|---|
| Dislocation glide & multiplication | Resolved shear stress from thermal gradients | Haasen–Alexander–Sumino viscoplastic law; Jordan thermoelastic stress model |
| Dissipative dislocation patterning | Plastic work far from equilibrium | Self-organization into cells/networks during/after relaxation |
| Void (COP) dissolution | Oxygen desaturation at void walls; interstitial Si supply | Oxide-shell dissolution kinetics coupled to O diffusion |
| Oxygen precipitation | Supersaturation of interstitial oxygen | Nucleation/growth kinetics, sensitive to frozen-in vacancy concentration |
| Point-defect/stoichiometry adjustment | Deviation from equilibrium native-defect concentrations | Kröger-type defect chemistry under controlled vapor/component pressure |
| Grain-boundary/dislocation rearrangement in 2D films | Thermally activated in-plane atomic displacement | Local bond reorganization at dislocation cores/GBs |

The unifying thermodynamic picture is that melt growth freezes in a set of defect populations and internal stresses characteristic of a *non-equilibrium* growth-front and cooling history; post-growth annealing supplies additional thermal energy and (often) a longer, better-controlled time-temperature path to drive the system toward configurations closer to local thermodynamic/kinetic equilibrium — while never fully reaching ideal-crystal equilibrium, since the anneal itself is time- and temperature-limited and can introduce its own artifacts (incomplete near-surface defect removal, new dislocation generation from imposed anneal gradients, redistribution rather than elimination of impurities).

## 4. Practical / Process Considerations

- **Ambient**: reducing (H$_2$), inert (Ar, N$_2$), or component-overpressure atmospheres are chosen according to which defect chemistry is being targeted (void dissolution vs. stoichiometry/compensation).
- **Temperature and duration**: dislocation-density reduction can be substantial — annealing for 6 hours at 1366 °C has been shown to reduce dislocation density in silicon by roughly 95%, along with migration of the associated linear defect features — but standard fixed-temperature post-solidification anneals used industrially for solar-grade silicon are noted to be insufficient on their own: a fixed-temperature, post-solidification high-temperature anneal is generally used in silicon crystal growth for solar cells, yet dislocation densities remain high, plausibly because new dislocations continue to form from thermal gradients within the ingot during the anneal itself. This motivates anneal schedules that also manage the gradients imposed during the anneal, not just peak temperature.
- **Depth-dependence**: near-surface defect removal is generally less complete than bulk removal, which matters directly for wafer-based devices where the near-surface region is functionally critical.
- **Coupling to growth parameters**: post-growth annealing cannot be optimized independently of growth-stage choices (pulling rate, $v/G_0$, crucible/crystal rotation used to homogenize impurity distribution and thermal field) — crystal rotation homogenizes impurity distribution and suppresses temperature-field inhomogeneities, while counter-rotating the crucible stabilizes melt flow and controls oxygen incorporation — since the defect and stress state the anneal must correct is set by these upstream choices.

## 5. Key References

1. **Rudolph, P.** "Dislocation cell structures in melt-grown semiconductor compound crystals." — foundational treatment of post-growth dislocation glide and dissipative dislocation patterning. *Crystal Research and Technology* (review lineage; see also ScienceDirect topical overview, "Generation and propagation of dislocations during crystal growth").
2. **Rudolph, P.** "Thermal stress and dislocations in bulk crystal growth," in *Handbook of Crystal Growth* (2nd ed.), Elsevier, 2015 — comprehensive review of thermal-stress-driven defect generation, equilibrium/non-equilibrium thermodynamics of defect formation, and dislocation patterning during and after growth.
3. **Prasad, V., Pendurti, S.** "Models for Stress and Dislocation Generation in Melt Based Compound Crystal Growth," in Dhanaraj, G., Byrappa, K., Prasad, V., Dudley, M. (eds), *Springer Handbook of Crystal Growth*, Springer, 2010 — Haasen–Alexander and Jordan model comparison; LEC InP case study.
4. **[Mechanics of shaped crystal growth from the melt]**, *Journal of Materials Research*, 1996 — numerical formulation of thermal-stress-driven steady-state dislocation generation in shaped CZ growth of III–V compounds; comparison of Haasen–Alexander vs. Jordan models.
5. **Neuroth et al.** "The Generation of Growth Dislocations by Inclusions and Growth-Face Damages: An Experimental Study," *Crystal Research and Technology*, 2020 — distinguishes growth dislocations from post-growth (secondary-inclusion-driven, glide) dislocations via X-ray topography on salol grown from supercooled melt.
6. **Vanhellemont, J. et al.** "Defect Engineering During Czochralski Crystal Growth and Silicon Wafer Manufacturing" — COP formation, depth-dependent dissolution kinetics under high-temperature annealing, and coupling to oxygen precipitation.
7. US Patent 8,389,999 — "Method to reduce dislocation density in silicon using stress" — quantitative post-solidification annealing results (dislocation density reduction ~95% at 1366 °C / 6 h) and discussion of the limits of fixed-temperature anneals.
8. US Patent 6,743,289 — "Thermal annealing process for producing low defect density single crystal silicon" — process integration of controlled $v/G_0$ growth with post-growth annealing for point-defect-agglomerate control.
9. US Patent 6,129,787 — "Semiconductor silicon wafer, semiconductor silicon wafer fabrication method and annealing equipment" — mechanism of COP/void oxide-shell dissolution under H$_2$/inert high-temperature annealing and its near-surface limitations.
10. **Matveev, O.A., Terent'ev, A.I.** et al., compiled in "Basic principles of postgrowth annealing of CdTe:Cl ingot to obtain semi-insulating crystals" (arXiv:0704.2325) — postgrowth annealing for stoichiometry/compensation control in II–VI compound crystals; extensive primary-literature bibliography on point-defect thermodynamics in CdTe.
11. **Kröger, F.A.** *The Chemistry of Imperfect Crystals*, North-Holland, 1964 — the standard reference for point-defect thermodynamics underlying stoichiometry-correction annealing in compound semiconductors.
12. **[Improvements in structural and optical properties of wafer-scale h-BN film by post-growth annealing]**, *Scientific Reports* (PMC6646322) — solid-state atomic rearrangement and crystallinity/optical improvement via high-temperature post-growth annealing, illustrating the mechanism outside bulk melt growth.
13. **[Growth of Highly Conductive PtSe$_2$ Films...]**, arXiv:2503.20659 — post-growth annealing-induced 3D structural reorganization and grain-boundary/dislocation rearrangement in 2D crystalline films, with GIXRD/STEM evidence.

---
*Note: several entries above are drawn from search-result summaries where full author/journal metadata was not fully resolved; recommend confirming exact citation details (full author lists, volume/page numbers) against the original sources before use in a formal bibliography.*

---

> [!NOTE]
> 
> Generated by Claude.ai
>
> Model: Sonet 5
>
> Prompt: Provide an extensive overview of the role of post-growth annealing in crystal growth from the melt. Provide key references. Show the output in Markdown format.
