# The Solidus and Liquidus: An Atomic-Structure Perspective

## 1. What the two curves actually encode

In a binary (or multicomponent) phase diagram, the **liquidus** is the locus of $(T, x)$ points at which the *last* trace of solid disappears on heating (or the *first* solid nucleates on cooling), and the **solidus** is the locus at which the *last* trace of liquid disappears on cooling (or the first liquid appears on heating). Between them lies the two-phase field $L + S$, whose boundaries at a given temperature are fixed by a horizontal tie-line intersecting both curves — the compositions of the coexisting liquid and solid are generally *different* from each other and from the nominal alloy composition since the composition of the first solid formed does not match that of the parent liquid, and the compositions of the solid and liquid phases in equilibrium at a given temperature are read off the intersection of a tie-line with the solidus and liquidus curves.

The existence of a *finite-width* two-phase gap (rather than a single sharp melting point, as for a pure substance) is the central fact to explain. A pure metal has no such gap: heating pure copper, it starts to melt at a single temperature, and while melting, solid and liquid coexist as two phases at one fixed temperature. The moment a second species is introduced, this single point splits into two curves separated by a temperature (and composition) interval. Understanding *why* requires looking at what mixing a second atomic species does to the microscopic organization of the liquid and the solid, and how that translates into the competing free energies $G^L(T,x)$ and $G^S(T,x)$.

---

## 2. The atomic-structure starting point: liquids are *not* just "disordered solids"

### 2.1 Short-range order (SRO) versus long-range order (LRO)

The crystalline solid is defined by long-range positional order: a periodic lattice with well-defined coordination shells extending, in principle, to infinity. The liquid retains **short-range order** — a well-defined nearest-neighbor coordination number and interatomic spacing, visible as sharp peaks in the pair-distribution function $g(r)$ — but loses long-range order beyond a few atomic diameters. This SRO/LRO distinction is the structural language used across condensed-matter treatments of ordering transitions, whether in binary alloys, magnetic systems, or crystallizing mixtures where the atomic short-range-order (Warren–Cowley) parameter is taken into account explicitly in deriving the free energy and phase diagram.

Because the liquid retains substantial local coordination and bonding character (it is a dense, structured fluid, not a dilute gas), its energy is not wildly different from the solid's — the enthalpy of fusion $\Delta H_{fus}$ is typically only a few percent of the cohesive energy. What separates liquid from solid thermodynamically is overwhelmingly **configurational entropy**: the liquid can explore vastly more atomic arrangements (positional disorder, plus — in a mixture — chemical/compositional disorder on top of it).

### 2.2 Why a *pure* substance still gives one sharp temperature

For a one-component system, $G^L(T)$ and $G^S(T)$ are each single curves in $T$ (no compositional degree of freedom). They cross at exactly one temperature, $T_m$, where the phase with the lowest free energy at a given temperature is the most stable, and at the melting temperature the two curves cross, so solid and liquid are in equilibrium — a single point, hence a single melting temperature and zero-width two-phase field. This is the baseline the solidus/liquidus gap deviates from.

---

## 3. Adding a second species: configurational entropy of mixing and the splitting of $T_m$

### 3.1 Free energy of a solution

For a binary system, each phase's molar free energy is written as the sum of a mixing term and the pure-component ("fusion") reference:

$$
G^{\phi}(T,x) = x_A G_A^{\phi} + x_B G_B^{\phi} + \Delta G_{mix}^{\phi}(T,x), \qquad \phi = L, S
$$

with, for a regular solution,

$$
\Delta G_{mix} = \Delta H_{mix} - T\Delta S_{mix} = x_A x_B \, \Omega + RT\left(x_A \ln x_A + x_B \ln x_B\right)
$$

This is exactly the standard regular-solution form: the free energy of a regular solid solution is the sum of the free energy of mixing and the free energy of fusion, and the mixing free energy itself splits into an enthalpic interaction term and an ideal configurational-entropy term.

The atomic-structure content of this equation is important and is often skipped over:

- **$\Delta S_{mix} = -R(x_A \ln x_A + x_B \ln x_B)$** is the configurational entropy of randomly placing A and B atoms on the available sites — lattice sites in the solid, or "quasi-lattice" cells in the liquid (the cell/hole model of liquids, going back to Eyring and to the quasi-chemical treatments of Guggenheim). This term has an *infinite slope* at $x_A \to 0,1$ — the curve for entropy of mixing has an infinite gradient at $x_A = 0$ and $x_A = 1$ — which is the deep reason liquidus/solidus lines always meet the pure-component axes with finite, non-zero slope (freezing-point depression is universal, however dilute the impurity: this is the atomic-scale root of colligative behavior).

- **$\Omega = z N_0 \left[\varepsilon_{AB} - \tfrac12(\varepsilon_{AA} + \varepsilon_{BB})\right]$** (schematically) is the interchange energy, built directly from the **nearest-neighbor bond energies** and the **coordination number $z$** — i.e., from the local atomic structure. Whether $\Omega$ is negative (A–B bonding favored → ordering/compound tendency, negative deviations) or positive (like-atom bonding favored → clustering tendency, positive deviations, potentially phase separation or a miscibility gap) is set by chemistry at the bond level. For $W<0$ mixing is exothermic and $\Delta G_{mix}$ is negative at all temperatures; for $W>0$, $\Delta H_{mix}$ is positive (endothermic mixing), which produces a maximum in the mixing free energy at low temperature and, only above a critical temperature, a single minimum corresponding to complete solid solubility.

### 3.2 Why the liquid and solid mixing terms differ — and why that difference *is* the gap

Crucially, $\Omega^L \neq \Omega^S$ and the entropy terms are not identical either, because:

1. **Coordination number differs.** Close-packed crystals have $z = 12$ (FCC/HCP) or $8$ (BCC), fixed and uniform. Liquids have a *reduced and fluctuating* average coordination (typically $\sim$10–11 for simple metallic liquids near freezing), with a distribution of local environments rather than one crystallographically fixed value. This changes the effective bond-counting in $\Omega$.

2. **Site availability / free volume.** The liquid has extra free volume and configurational freedom (atoms are not confined to fixed lattice points), which is precisely the extra entropy that stabilizes the liquid at high $T$ relative to the solid, and which also allows the liquid to accommodate a given solute atom (size, bonding mismatch) with a smaller energetic penalty than the rigid lattice can. This asymmetry between $G^L(x)$ and $G^S(x)$ — the liquid curve sitting lower in energy/flatter in composition than the solid curve away from pure endmembers — is what forces the common-tangent construction described next to give *two different* compositions rather than one.

3. **Size mismatch and elastic strain in the solid.** Continuous solid solubility over the full composition range is possible only if atomic sizes differ by no more than about 15%; there are many examples of restricted mutual solid solubility even between elements with similar crystal structures and atom sizes. This is a purely structural (Hume-Rothery) constraint: substituting a mismatched atom into a rigid lattice costs elastic strain energy that has no liquid-phase analogue (the liquid can relax locally around a misfit atom far more cheaply). This raises $G^S(x)$ relative to $G^L(x)$ away from the pure endmembers, widening the two-phase gap or even truncating solid solubility (peritectic/eutectic systems, terminal solid solutions) instead of allowing a continuous solid solution.

### 3.3 The common-tangent construction: geometry that follows directly from atomic energetics

At a fixed $T$ between the two pure melting points, plot $G^L(x)$ and $G^S(x)$ on the same axes. Because they are different functions of $x$ (different curvatures, different minima, for the structural reasons above), they generally cross. The equilibrium compositions of coexisting solid and liquid at that $T$ are **not** given by the crossing point but by the **common tangent line** touching both curves — this is the Gibbs equal-chemical-potential condition, $\mu_A^L = \mu_A^S$ and $\mu_B^L = \mu_B^S$ simultaneously. A tangent drawn to the liquid free-energy curve at the parent composition intersects the solid free-energy curve at two points, and the portion of the solid curve between those two points lying below the tangent indicates the composition range over which it is thermodynamically favorable to precipitate solid from that liquid.

As $T$ is swept from the low-melting endmember's $T_m$ up to the high-melting endmember's $T_m$, the two tangent points trace out two curves in $(T,x)$ space: the liquid-side tangent points trace the **liquidus**, the solid-side tangent points trace the **solidus**. They are two different curves — rather than one — *precisely because* $G^L(x)$ and $G^S(x)$ are different functions, rooted in the differing atomic-scale environments (coordination, free volume, elastic accommodation) described in §3.2. This same double-tangent construction, and the resulting pair of curves explicitly labeled liquidus/solidus, appears even far from ordinary metallurgy — e.g., in dense Coulomb "liquids" of ionic mixtures in white-dwarf interiors, where a double tangent between the solid free-energy spline and the liquid free energy is used to map out the phase diagram of crystallization from the liquid into a short-range-ordered solid, with liquidus and solidus obtained from that construction — underscoring that the mechanism is generic to any two condensed phases with different atomic-scale free energy functions, not specific to metallic bonding.

---

## 4. Physical origin of common diagram shapes, traced to atomic structure

| Diagram feature | Atomic-structure origin |
|---|---|
| **Lens-shaped loop (complete solid solubility)** | Both A and B atoms are similar enough in size (<~15%, Hume-Rothery), electronegativity, and valence to substitute freely on a common lattice type; $\Omega^S \approx 0$ or mildly positive but not enough to open a miscibility gap below the solidus. |
| **Eutectic (V-shaped liquidus meeting at a minimum)** | Size/structure mismatch is large enough that solid solubility is restricted at both ends; two separate solid solution fields (each with its own liquidus/solidus branch) are more stable than one continuous solid solution, and their liquidus branches meet at the eutectic, where the liquid phase is in equilibrium with two solid phases at the lowest melting temperature of the mixture, precisely because — at the eutectic point the compositions of the two coexisting solids and the liquid coincide such that no further separation is thermodynamically favorable. |
| **Peritectic** | One solid phase is stable only over a narrow composition range because the atomic arrangement (e.g. an ordered sublattice or a specific coordination polyhedron) required is disrupted rapidly away from stoichiometry. |
| **Congruent melting compound (vertical line, cusp in liquidus with zero slope)** | A specific, strongly bonded local atomic arrangement (an intermetallic or "molecular" complex, e.g. AB or AB₂ short-range clusters) persists into the liquid itself; the solid compound melts congruently to a liquid of the same composition, and the liquidus slope is nonzero at the composition of a pure component but is zero at the composition of a solid compound that is completely dissociated in the liquid — reflecting the fact that near-stoichiometric short-range clustering in the melt mimics the solid's local order and suppresses the usual configurational-entropy-driven slope. |
| **Narrow solidus–liquidus gap for dilute solid solutions** | Very small solubility limits (steep, near-vertical solidus near $x=0$) occur when the mismatch penalty in the rigid lattice is severe but the liquid can dissolve the solute with only modest energy cost — a direct statement about differential structural tolerance of the two phases. |

---

## 5. Kinetic/atomic-transport underpinning of the two-phase region's physical reality

The two-phase field is not just a bookkeeping device; it corresponds to a genuinely observable microstructural state (solid grains/dendrites bathed in interdendritic liquid), and its persistence is tied to atomic mobility differences between the phases: the effectiveness of liquid-phase processes (e.g. sintering) arises because atomic diffusion rates through a liquid are much higher than through a solid, and because liquid surface tension draws solid particles together. During solidification in the two-phase field, continuous atomic partitioning occurs — rejected or preferentially incorporated solute atoms diffuse across the solid–liquid interface — which is why, at any temperature strictly between solidus and liquidus, the compositions of the coexisting solid and liquid phases diverge from the nominal average composition, i.e. elemental partitioning occurs between the two phases, converging back to the nominal composition only in the limiting cases where the system is (almost) fully solid (composition pinned at the solidus) or (almost) fully liquid (composition pinned at the liquidus) — at the liquidus the equilibrium state is predominantly liquid with only an infinitesimal solid fraction whose liquid-phase composition equals the overall average, and at the solidus the equilibrium state is predominantly solid with only a negligible liquid fraction whose solid-phase composition equals the overall average. Modern computational approaches even automate this: melting/solidification points can be located via molecular-dynamics-based free-energy calculations that track exactly this partitioning behavior atomistically rather than relying solely on empirical thermodynamic models using the compositional-partitioning signatures at the solidus and liquidus as the operational criteria for locating those points in simulation.

---

## 6. Summary of the causal chain

1. A pure substance's $G^L(T)$ and $G^S(T)$ cross at one point → one melting temperature, no gap.
2. Alloying introduces a composition axis; configurational entropy of mixing (infinite-slope at the pure endmembers) and interchange/bond energy (built from nearest-neighbor coordination and bond strengths) enter $G^{L}(T,x)$ and $G^{S}(T,x)$ differently in each phase, because the liquid's local coordination, free volume, and structural relaxation ability around foreign atoms differ fundamentally from the rigid, fixed-coordination crystal lattice (elastic strain energy, size-mismatch limits, Hume-Rothery-type rules).
3. The common-tangent (equal chemical potential) construction on these two *different* free-energy curves generically yields **two distinct compositions** in equilibrium at each temperature — one on the liquid curve, one on the solid curve.
4. Sweeping temperature traces these tangent points into two curves: liquidus (bounding the all-liquid field) and solidus (bounding the all-solid field), with a genuine two-phase, partitioned microstructure filling the gap between them.
5. The particular shape of the gap (lens, eutectic, peritectic, congruent point) is fully determined by how strongly the atomic-scale mismatch (size, bonding, coordination) discriminates against solid solubility relative to liquid solubility.

---

## Key References

1. **Shercliff, H. R. & Ashby, M. F.**, *"Teach Yourself Phase Diagrams,"* Cambridge University Engineering Department teaching module — clear derivation-by-construction of liquidus/solidus from tangent constructions, with worked binary systems (Cu–Ni, Pb–Sn). Available via University of Maryland course archive.
2. **DoITPoMS (University of Cambridge), *"Phase Diagrams and Solidification"*** — TLP module deriving $\Delta G_{mix}$, regular solution theory, and the free-energy/common-tangent origin of two-phase fields from first principles.
3. **DeVoe, H.**, *Thermodynamics and Chemistry*, 2nd ed. — rigorous phase-rule treatment of binary liquidus/solidus/eutectic/peritectic topology (hosted on LibreTexts, Ch. 13).
4. **ScienceDirect Topics: "Solidus Line"** and **"Binary Phase Diagram"** — overviews of the free-energy tangent construction and Hume-Rothery size-mismatch solubility rules.
5. **Chen, C.-H. et al.**, *"A Generic and Automated Methodology to Simulate Melting Point"* (arXiv:2408.17270) — modern atomistic/MD approach connecting solute partitioning behavior directly to solidus/liquidus determination.
6. **Blouin-Hudon, E.-C. et al. / white-dwarf C/O crystallization study** (arXiv:2504.11545) — demonstrates that the same double-tangent, short-range-order-based construction of liquidus/solidus generalizes far beyond metallurgy, to Coulomb-liquid crystallization.
7. **Cowley, J. M.**, *"Short- and Long-Range Order Parameters in Disordered Solid Solutions,"* Phys. Rev. 120, 1648 (1960) — foundational treatment connecting short-range order parameters to configurational free energy in alloys.
8. **Cahn, J. W.**, *"Free Energy of a Nonuniform System,"* and *"Spinodal Decomposition,"* Acta Metall. 9 (1961) — for the free-energy-landscape treatment underlying phase-field/spinodal aspects of the same solution thermodynamics referenced in the DoITPoMS phase-field module.
