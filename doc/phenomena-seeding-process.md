# The Role of Seeding in Crystal Growth from the Melt

## 1. Introduction and Scope

Seeding is the operation by which a small, pre-characterized single crystal (the *seed*) is brought into contact with a melt in order to initiate controlled, oriented, single-crystalline growth. Although it occupies only the first few minutes to hours of a growth run that may last days, the seeding stage is disproportionately important: essentially every macroscopic defect class that plagues bulk melt growth — dislocations, low-angle grain boundaries, twins, polycrystallinity, and even gross morphological instabilities of the growth front — can trace its origin to events at or immediately after seed–melt contact. This document surveys the physical mechanisms operative during seeding, the engineering procedures developed to control them across the major melt-growth methods (Czochralski/CZ and variants, Kyropoulos, Bridgman/vertical Bridgman–Stockbarger, and float-zone), and the key literature underpinning current practice.

## 2. Functions of the Seed Crystal

The seed serves several simultaneous physical roles, and seeding protocols must satisfy all of them at once:

1. **Nucleation template.** The seed provides a pre-existing crystalline surface onto which the melt solidifies epitaxially, eliminating the need for homogeneous or heterogeneous nucleation from an undercooled melt — a process that would otherwise proceed with essentially uncontrolled, and generally polycrystalline, orientation.
2. **Crystallographic orientation selector.** The seed's orientation (e.g., $\langle 100 \rangle$, $\langle 111 \rangle$, $\langle 0001 \rangle$ depending on material and application) is inherited by the growing crystal, fixing the relationship between growth axis and lattice directions relevant to downstream device processing (cleavage, wafer cutting, anisotropic etching).
3. **Heat sink / thermal boundary condition.** In pulled-growth methods the seed and pull rod conduct the latent heat of solidification away from the growth interface, and the seed's own thermal history sets the initial curvature and stability of the interface. The seed crystal acts as a nucleation centre and as a heat sink through which the latent heat of solidification escapes.
4. **Mechanical support.** In pulled methods the entire crystal hangs from the seed and neck; in vertical Bridgman-type methods the seed anchors the initial solid front inside the ampoule/crucible.
5. **Point of maximum defect risk.** Because of thermal shock and interface-curvature effects at first contact (Section 3), the seed–crystal junction is generically the most dislocation- and grain-boundary-prone region of the entire boule.

## 3. Physical Mechanisms at Seed–Melt Contact

### 3.1 Thermal shock and dislocation generation

When a cold seed is dipped into a melt held near the equilibrium melting point, it experiences a large, transient temperature gradient. The resulting thermal stresses commonly exceed the critical resolved shear stress for dislocation glide, nucleating dislocations at or near the contact surface. As crystal growth begins, the seed crystal exists at a much lower temperature than the molten polysilicon, and as a result, when the seed crystal comes into contact with the surface of the melt, it experiences a thermal shock that causes dislocations to be formed in the seed crystal. These dislocations propagate preferentially along specific crystallographic planes: dislocations tend to propagate along the crystallographic plane of the seed crystal that is the most dense, and for a monocrystalline silicon seed with a ⟨100⟩ orientation, dislocations generally propagate along the ⟨111⟩ plane at roughly 55° to the growth axis. This geometric relationship is the physical basis for the necking strategy described in Section 4.1: a sufficiently long, thin neck lets glide-plane geometry carry dislocations out to the free surface, where they terminate, rather than continuing indefinitely into the bulk of the growing crystal.

### 3.2 Partial melt-back and meniscus formation

Immediately after dipping, the seed tip is deliberately partially remelted by fine control of heater power, removing seed-crystal surface layers that may already carry mechanically damaged or oxidized material and re-establishing a clean, thermally equilibrated solid–liquid interface. It is important to adjust the power of the heater(s) carefully so that a certain portion of the dipped seed is remelted and a melt meniscus is formed. The capillary meniscus that forms at this stage governs the subsequent diameter response to pulling and heater-power perturbations and is the quantity actively controlled in automatic diameter control (ADC) systems.

### 3.3 Interface shape and its dependence on seeding thermal conditions

The curvature of the solid–liquid interface at and just after seeding is set by the competition between conductive/convective heat extraction through the melt and radiative/conductive heat extraction through the seed and growing crystal. Different growth methods deliberately exploit different regimes:

- Kyropoulos processes with stronger heat extraction from the seed produce crystals of higher curvature, where the solid/liquid interface converges to a spherical shape around the contact point between the seed and the melt — a consequence of radiative heat extraction from the crystal surface combined with the low curvature of isothermal surfaces in the melt due to convection. This principle enhances vertical growth relative to horizontal enlargement but also increases thermal gradients in the crystal.
- In Bridgman-family methods, the axial temperature profile near the seed–melt junction can be engineered to obtain a convex (into the melt) interface, which is generally favorable for single-crystal selection and defect rejection; systematic curvature criteria based on the axial temperature profile have been developed to guide furnace and seed design.

### 3.4 Grain selection and stray-grain nucleation at the seeding interface

Even with a correctly oriented, dislocation-free seed, new grains can nucleate at the periphery of the seed–melt contact region — particularly where the seed partially melts back unevenly or where constitutional undercooling exists at the interface edge (common in alloys and doped systems). Seeding of single-crystal superalloys is strongly affected by the role of seed melt-back on casting defects, since incomplete or excessive melt-back changes the effective nucleation geometry available to competing grains. Similarly, in vertical Bridgman growth of sapphire, low-angle grain boundaries generated at the periphery of the seeding interface can be eliminated by introducing a thin-neck formation immediately following the initial seeding step, so that the main crystal body remains free of low-angle grain boundaries.

## 4. Seeding Procedures by Growth Method

### 4.1 Czochralski (CZ) and Related Pulled Methods

The canonical CZ seeding sequence, broken into discrete unit operations, is: a melting process, a seed crystal preheating process, a seeding process, a temperature adjustment process, a necking process, a shouldering process, a constant-diameter growth process, an ending process, and a cooling/crystal-removing process. Graphically: seeding procedure (seed dipped into the melt), followed by Dash necking, shouldering, cylindrical growth, growth of the end cone, lift-off, cooling, and removal of the crystal.

**Necking (the "Dash process").** The single most important defect-control step immediately following seeding in CZ growth of covalently bonded semiconductors is the necking (or "Dash necking") procedure, introduced by W. C. Dash in 1959. The necking process forms a long, thin neck portion 3–5 mm in diameter, which prevents dislocations generated in the seed crystal by thermal shock during dipping from propagating into the grown crystal, though the probability of achieving a fully dislocation-free crystal via this route is not always 100%. Practical implementations vary in pull rate and target diameter: dislocations are conventionally removed by growing the neck at a pull rate of 4–6 mm/min while holding a constant diameter of about 4.5–10 mm for a length of 30–200 mm, though necks wider than about 10 mm are difficult to render dislocation-free by this fast, thin-neck approach. An alternative "slow, thick-neck" strategy has also been patented: a neck with an intermediate portion mostly wider than 10 mm can still be freed of dislocations if grown at a rate below about 4 mm/min (typically 1.0–3.0 mm/min), allowing dislocations to annihilate faster than they multiply, producing a mechanically much stronger neck able to support larger crystal masses. This trade-off matters industrially because the classic thin Dash neck is the weakest part of the crystal and can fracture under its own weight during growth, which is why conventional Dash-necked crystals are typically limited to about 100 kg or less, even as demand has grown for much larger boules.

For specific doping regimes the thermal-shock/dislocation problem can be sidestepped rather than corrected: dislocation-free silicon crystals have been grown from heavily boron-doped melts without any dislocation-elimination necking process at all — no dislocations were generated in a heavily boron-doped ⟨100⟩ seed during dipping, and no misfit dislocations occurred in the grown crystal, showing that shoulder and body growth can begin immediately after seeding under these conditions. Complementary industrial patents refine pull-rate windows for boron-doped, low-resistivity material: a pulling rate of 2 mm/min or less during necking, applied to boron-doped silicon with resistivity ≤1.5 mΩ·cm and a neck diameter of 2 mm to just under 5 mm, avoids scratch defects at the wafer surface after wafering.

Furnace-side thermal engineering during dislocation elimination is also actively controlled: retracting a cooling coil and thermal insulation member away from the melt surface during Dash-neck drawing, so that they sit within a defined "dislocation-elimination range" relative to the melt surface, is used to ensure dislocations are eliminated only under the specific thermal conditions to which the Dash method properly applies.

**Orientation-dependent difficulty.** Not all seed orientations neck equally well: for a ⟨110⟩-oriented seed, slip dislocations proved difficult to eliminate by Dash necking, requiring the neck's minimum diameter to be reduced to as little as 2 mm before dislocation-free necking finally succeeded, after several prior attempts had failed.

### 4.2 Kyropoulos Method

Kyropoulos seeding is deliberately engineered around strong axial heat extraction through the seed to produce a highly curved, near-hemispherical growth front, which promotes rapid diametral enlargement from a small seed footprint — a defining feature of the method's ability to grow large-diameter, low-dislocation-density boules of oxide crystals such as sapphire. Practical KY seeding of sapphire involves soaking the seed 3–5 mm below the melt surface, using a rotationally asymmetric heat-loss (radiation) structure so the seed preferentially grows a crystalline disk to one side, then lifting the seed at a low average rate on the order of 3–12 mm/h with intermittent transient rises, rotating between rises to redistribute preferential growth directionally, and repeating this until the seed section reaches 60–80 mm in length and the solid–liquid interface reaches an equivalent cross-sectional diameter of 40–60 mm, at which point seeding is considered complete. As noted in Section 3.3, this strong-curvature regime trades off enhanced early-stage vertical/radial growth against elevated thermal gradients that must subsequently be managed to avoid dislocation generation in the enlarging boule.

### 4.3 Bridgman / Vertical Bridgman–Stockbarger and Directional Solidification

In Bridgman-type growth the seed typically sits at the bottom of a sealed ampoule and is not pulled through a free surface but rather held stationary while a temperature gradient is translated past it (or the ampoule is translated through a fixed gradient). Seeding quality here is governed less by mechanical necking and more by (i) the shape of the seed itself and (ii) the axial temperature profile at the seed–melt junction:

- Seed crystal shape and seeding characteristics have a direct and well-documented effect on outcomes in vertical Bridgman growth of sapphire; introducing a thin-neck step right after seeding is one effective route to suppressing low-angle grain boundaries nucleated at the periphery of the seed–melt interface.
- Convex (into-the-melt) interface shapes at and after seeding are generally sought because they help reject stray grains and impurities toward the ampoule wall/crystal periphery; systematic axial-temperature-profile curvature criteria have been proposed specifically to engineer convex growth interfaces in Bridgman systems, and such criteria have been used in practice — e.g., to optimize growth conditions and reduce compositional segregation in (K,Na)NbO₃-based crystals grown by the vertical Bridgman–Stockbarger method, informed by prior thermal-property analysis of the precursor oxides and suitable crucible dimensioning.
- Seeded bicrystal and multi-crystal growth (e.g., for superalloy turbine blade research) depends critically on controlled, partial seed melt-back: the seeding-grain-selection technique for orientation control in high-throughput molds builds directly on earlier work establishing how the degree of seed melt-back governs casting-defect formation in seeded single-crystal superalloys.

### 4.4 Self-Seeding and Grain-Selection Variants

Where a pre-oriented seed crystal is unavailable or impractical (certain scintillator halides, some superalloy geometries), directional solidification can instead rely on *self-seeding* / natural grain selection, in which a narrow constriction or grain-selector geometry at the base of the crucible allows only one (essentially randomly oriented) grain to survive into the main growth chamber. Randomly oriented self-seeded Bridgman growth has been used, for instance, for the ternary iodide scintillator KCaI₃:Eu, where multi-ampoule geometries were used to grow several crystals simultaneously without an externally supplied oriented seed. This approach trades orientation control for simplicity and higher throughput, and is acceptable when the application (e.g., scintillation detection) is largely orientation-insensitive.

## 5. Seed Preparation and Pre-Growth Considerations

Beyond the dynamics of the contact event itself, seed *preparation* materially affects seeding outcomes:

- **Seed quality.** The seed must itself be dislocation-free (or of known, low, characterized dislocation density) and free of surface damage, since seeding cannot improve on the crystalline quality already present in the seed — it can only propagate or (via necking) partially clean up defects generated at the interface.
- **Seed preheating.** A dedicated preheat step is standard practice to reduce the thermal gradient magnitude at first contact, directly mitigating the thermal-shock mechanism of Section 3.1. A seed crystal preheating process is explicitly included as a discrete unit operation preceding the seeding process itself in modern CZ process descriptions.
- **Orientation choice.** Beyond fixing the final ingot's crystallographic frame, orientation choice affects how readily thermally-nucleated dislocations can be swept out during necking (Section 4.1), since this depends on the angle between the growth axis and the relevant slip planes.
- **Seed cross-section / diameter.** A larger seed cross-section increases mechanical robustness and thermal mass (reducing thermal shock) but complicates full melt-back and clean re-nucleation; a smaller seed eases melt-back control but is mechanically fragile and, in pulled growth, more prone to fracture at the neck under load.

## 6. Consequences of Seeding Defects for Downstream Growth

Failures at the seeding stage do not remain local. Dislocations nucleated at the seed–melt junction multiply and propagate along active slip systems throughout the length of a CZ or Bridgman boule unless arrested; unrejected stray grains nucleated at the seeding interface periphery can grow in competition with the main crystal and eventually overtake it, especially where interface curvature or thermal gradients favor off-axis grains. Because these consequences compound over the entire subsequent growth run — which may last many hours to days — the return on careful seeding-stage engineering (correct necking rate/geometry, correctly engineered interface curvature, controlled melt-back) is large relative to the short duration of the seeding stage itself.

## 7. Summary

Seeding is the nucleation and orientation-fixing operation common to essentially all melt-growth techniques, but the physical demands placed on it differ by method: CZ and float-zone growth manage seed–melt thermal shock primarily through a necking step (thin/fast Dash necks or thick/slow alternative necks, with method choice constrained by target crystal mass and orientation); Kyropoulos growth exploits strong seed-side heat extraction to obtain a highly curved interface enabling rapid diametral growth from seed to full boule; Bridgman-type methods rely on seed shape, controlled partial melt-back, and engineered axial temperature-profile curvature to reject stray grains and low-angle grain boundaries nucleated at the seed–melt interface periphery; and self-seeded/grain-selection variants dispense with an externally supplied oriented seed where orientation control is not application-critical. Across all of these, the seed's dual role as nucleation template and initial thermal boundary condition makes the seeding stage the single most defect-critical few minutes of an otherwise much longer growth process.

---

## Key References

1. Dash, W. C. (1959). Original description of the thin-neck dislocation-elimination procedure in Czochralski silicon growth (the "Dash neck" method), as cited in subsequent patent literature, e.g. US 2001/0020438 A1.
2. Czochralski, J. (1917). *Ein neues Verfahren zur Messung der Kristallisationsgeschwindigkeit der Metalle.* Zeitschrift für Physikalische Chemie — origin of the pulling technique.
3. von Ammon, W., Friedrich, J., & Müller, G. (2015). "Czochralski growth of silicon crystals." *Handbook of Crystal Growth* (or equivalent review), as referenced via ScienceDirect topic overview of the CZ method.
4. "Czochralski Process" and "Czochralski Method" topic overviews. *ScienceDirect Topics* (Materials Science / Physics and Astronomy collections). https://www.sciencedirect.com/topics/chemistry/czochralski-process ; https://www.sciencedirect.com/topics/physics-and-astronomy/czochralski-method
5. "Crystal Growth From Melt" topic overview, including seeded crystal growth from melt and solution and the liquid-encapsulated Czochralski (LEC) method. *ScienceDirect Topics*. https://www.sciencedirect.com/topics/materials-science/crystal-growth-from-melt
6. Characterization of shape and heat flow in melt-grown crystals by an effective seed radius — comparison of Kyropoulos vs. other interface-curvature regimes. *Journal of Crystal Growth*. https://www.sciencedirect.com/science/article/abs/pii/0022024868901462
7. CN105019023B — "A seeding method of Kyropoulos growing sapphire crystal." Google Patents (detailed KY seeding protocol: soak depth, asymmetric thermal structure, pull rate schedule, target neck geometry). https://www.google.com/patents/CN105019023B
8. Vertical Bridgman growth of sapphire — seed crystal shapes and seeding characteristics; thin-neck-after-seeding technique for eliminating low-angle grain boundaries. *Journal of Crystal Growth* (2014). https://www.researchgate.net/publication/261292567
9. An axial temperature profile curvature criterion for the engineering of convex crystal growth interfaces in Bridgman systems. *Journal of Crystal Growth*. https://www.sciencedirect.com/science/article/abs/pii/S0022024816305668
10. Orientation control of multiple single-crystal blades using a seeding-grain-selection technique; includes review of seed melt-back effects on casting defects in seeded single-crystal superalloys (citing Stanford, Djakovic, Shollock, McLean & D'Souza, *Scripta Materialia*, 50(1), 2004, 159–163; and Pollock & Murphy, *Metallurgical and Materials Transactions A*, 27, 1996, 1081–1094). https://www.sciencedirect.com/science/article/pii/S2238785424005222
11. Dislocation-Free Czochralski Silicon Crystal Growth without the Dislocation-Elimination-Necking Process. *Japanese Journal of Applied Physics* (heavily boron-doped seed/melt system). https://www.researchgate.net/publication/243737397
12. Process for eliminating dislocations in the neck of a silicon single crystal. US Patent 5,628,823 (slow, thick-neck dislocation elimination method).
13. Non-dash neck method for single crystal silicon growth. US Patent 5,885,344.
14. Process for eliminating neck dislocations during Czochralski crystal growth. WO 2003/021011 A1; US 2003/0047130 A1 (reduced axial-length dislocation elimination via interfacial heat-transfer control).
15. Apparatus for pulling single crystal by CZ method. US Patents 6,733,585; 6,977,010; 7,727,334; 8,002,893 (cooler/insulation retraction relative to the melt surface during Dash-neck drawing).
16. Method for pulling silicon single crystal. US Patent 8,652,254 (necking pull-rate and diameter windows for boron-doped, low-resistivity silicon).
17. Method for reducing thermal shock in a seed crystal during growth of a crystalline ingot. US Patent 6,090,198 (seed orientation vs. dislocation glide-plane geometry).
18. Method of manufacturing silicon single crystal, silicon single crystal and silicon wafer. US Patent 7,179,330 (⟨110⟩ seed necking difficulty case study).
19. Methods and devices for growing scintillation crystals / crystals with high uniformity without annealing. US Patents 12,116,517; 11,655,557; 12,286,725 (unit-operation decomposition of the CZ process including the discrete seeding process step).

*Note: patent references above are drawn from published patent literature retrieved via web search and are provided as primary technical sources for the specific process parameters cited; original journal-article DOIs are given where identified in the retrieved material.*

---

> [!NOTE]
> 
> Generated by Claude.ai
>
> Model: Sonet 5
>
> Prompt: Provide an extensive overview of the role of seeding process in crystal growth from the melt. Provide key references. Show the output in Markdown format.
