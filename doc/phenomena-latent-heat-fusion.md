# The Role of Latent Heat of Fusion in Crystal Growth from the Melt

## 1. Introduction

Latent heat of fusion, $L$ (per unit mass or per unit volume, $L_v = L\rho$), is the energy released at the solid–liquid interface as atoms attach to the crystal lattice during solidification, and absorbed during melting. In melt growth processes — Czochralski (CZ), Bridgman/vertical gradient freeze (VGF), float zone (FZ), Kyropoulos, EFG, directional solidification, and related techniques — $L$ is not a minor correction term but one of the central quantities coupling the thermal field to the moving interface. It enters the Stefan boundary condition, governs interface morphological stability jointly with capillarity and diffusion, sets the characteristic scale of interface roughness and faceting, and constrains the achievable growth rate for a given furnace heat-extraction capacity. This document surveys these roles systematically.

## 2. The Stefan Condition: Latent Heat as a Moving-Boundary Source Term

At the solid–liquid interface $\Gamma(t)$ moving with normal velocity $V_n$, global energy conservation requires

$$
k_s \left.\frac{\partial T_s}{\partial n}\right| - k_l \left.\frac{\partial T_l}{\partial n}\right| = L_v \, V_n
$$

where $k_s, k_l$ are the solid and liquid thermal conductivities and $n$ is the interface normal (pointing into the liquid). This is the classical **Stefan condition**: the discontinuity in conductive heat flux across the interface must exactly supply (on freezing) or absorb (on melting) the latent heat associated with the local growth rate.

Consequences that follow directly from this relation:

- **Growth rate is thermally rate-limited.** For a furnace configuration with fixed heat-extraction capacity (through the crystal, in CZ; through the ampoule wall, in Bridgman), the maximum sustainable pulling/translation rate is bounded by how fast $L_v V_n$ can be conducted away. This is why, e.g., large-diameter CZ silicon growth cannot be pulled arbitrarily fast — the crystal's own axial conduction must carry away both the sensible heat extracted upward and the latent heat generated at the interface.
- **Interface shape is a free boundary problem.** Because $V_n$ and the interface position are unknowns coupled to the two-phase heat equation through this flux jump, melt growth is inherently a Stefan-type free-boundary problem; this is the physical basis for the moving/free interface treatment used throughout continuum growth models (see `crystal-growth-reference` library, continuum model physics coverage) and in the global heat-transfer solvers CGSim, CrysMAS, FEMAG-CZ, and CrysVUn.
- **Coupling to melt convection.** Because $L$ is released exactly at the interface, and the interface shape (concave/convex/flat) is itself determined by whether more heat is conducted into the crystal or into the melt, latent heat feeds back on Marangoni and buoyancy-driven convection patterns, and hence on the single-cell vs. multi-cell melt flow transitions relevant to CZ interface shape control.

## 3. Morphological Stability: The Mullins–Sekerka Framework

The classical linear stability analysis of a planar solidification front — due to **Mullins and Sekerka (1963, 1964)** — identifies latent-heat release as one of the two competing physical effects that determine whether a planar interface remains stable or breaks down into cells/dendrites.

For a pure melt, a linear stability analysis for small perturbations shows that thermal effects are destabilizing if more of the latent heat flows into supercooled liquid than into the solid, while capillary effects of interfacial free energy are stabilizing, so that overall stability depends on the competition between heat flow and capillarity. Physically: a small protrusion of the interface into a supercooled melt sits in a region where the local temperature gradient is steeper, so the latent heat produced there diffuses away more easily, allowing the interface to grow faster there so that the protrusion is amplified rather than damped. Capillarity (interfacial free energy, via the Gibbs–Thomson effect) resists this by penalizing high-curvature protrusions, providing the short-wavelength cutoff.

For alloy solidification, the same latent-heat/heat-flow competition is joined by solute diffusion effects (destabilizing for a positive liquidus-slope system rejecting solute ahead of a growing solid), which is the dynamical (Mullins–Sekerka) generalization of the older, purely thermodynamic **constitutional supercooling** criterion of Tiller, Jackson, Rutter and Chalmers. As one review notes, the constitutional-supercooling criterion refers only to the liquid phase and ignores the latent heat of fusion and the heat flow throughout the growing crystal, whereas the full perturbation theory of interface stability is built on the dynamics of the entire melt–crystal system.

Key features of the resulting stability picture:

- A destabilizing role for latent heat rejection arises specifically when more heat is conducted into the (supercooled) liquid than into the solid — i.e., under **constitutional or thermal supercooling ahead of the front**. Under a stabilizing positive gradient in the liquid (heat flowing away from the interface predominantly through the solid), latent-heat release is instead compatible with stable planar growth.
- In the pure-melt limit, thermal effects are the destabilizing factor whenever more latent heat flows into the supercooled liquid than into the solid, while capillarity remains stabilizing; for alloys, solute rejection generally adds a destabilizing contribution that competes with thermal and capillary effects.
- The theory predicts a critical perturbation wavelength: instability first appears at long wavelengths and a band of wavelengths becomes unstable as conditions worsen, eventually giving rise to the cellular and dendritic interface morphologies seen experimentally in directionally solidified alloys and melt-grown crystals.
- **Directional asymmetry between melting and freezing.** A subtlety worth stressing for melt-growth practice: the destabilizing latent-heat mechanism operates during growth but not during melting when the heat needed to melt the crystal is supplied through the melt — which is why, for example, an ice cube retains a smooth, rounded shape while melting even though a growing ice front can develop cells and dendrites. This asymmetry is a direct, sign-dependent consequence of where the latent-heat term sits in the flux-jump condition.

A large modern literature (see review by Alexandrov & Galenko, 2024, and the phase-field and colloidal-freezing studies below) extends the original Mullins–Sekerka analysis to rapid solidification, nonlinear regimes, and non-equilibrium interface kinetics, but the qualitative latent-heat/capillarity/solute competition established in 1963–1964 remains the organizing framework used throughout the field, including in the continuum melt-growth models (radiative heat transfer, Marangoni convection, segregation at the growth interface) catalogued in the crystal-growth reference library.

## 4. Latent Heat and Interface Roughness: The Jackson $\alpha$-Factor

A separate but related role of $L$ concerns the **microscopic** structure of the interface — whether it is atomically rough (giving smooth, isotropic, "non-faceted" growth) or atomically smooth (giving faceted growth dominated by step/kink kinetics).

**Jackson's criterion** quantifies this via a dimensionless roughness parameter

$$
\alpha = \xi \frac{\Delta S_f}{R} = \xi \frac{L}{R T_m}
$$

where $\Delta S_f = L/T_m$ is the entropy of fusion per mole, $R$ is the gas constant, $T_m$ the melting point, and $\xi$ a crystallographic geometric factor ($\xi \le 1$) describing the fraction of nearest-neighbor bonds within the interfacial layer. The physical content is that entropy of fusion — and hence latent heat — controls how sharply the free energy of the interface depends on its degree of order:

- Materials with small latent heats of fusion, such as quartz, tend to have molecularly rough interfaces and grow with a non-faceted morphology, while materials with large latent heats, such as most silicates, tend to have smooth interfaces and grow with a faceted morphology.
- More quantitatively, phases with $\alpha < 2$ or with entropy of fusion greater than about 16.8 J mol⁻¹ K⁻¹ exhibit faceted morphology during crystallization from the melt; by this analysis most semiconductors and metalloids grow with faceted morphology, whereas common metals — which have low entropies of fusion — show non-faceted or dendritic growth.
- Experimental studies on ionic melts corroborate the trend directly: crystals with a smaller entropy-of-fusion parameter grew in a non-faceted round form at small supercoolings and as non-faceted dendrites at larger supercoolings, whereas crystals with larger entropy-of-fusion parameters showed markedly faceted growth up to considerably large supercoolings, with intermediate compounds showing a *mixed* faceted/non-faceted character depending on supercooling — i.e., the same latent-heat-derived parameter organizes a whole family of morphological transitions, not just a binary split.
- Because $\alpha$ depends on $L/T_m$, and $L$ itself can shift with alloy composition, the roughening/faceting transition can be composition- and pressure-dependent within a single chemical system; Co–Si alloy studies show measured latent heats of fusion feeding directly into predictions of faceted vs. non-faceted eutectic morphology via the Jackson framework, with latent heats determined from DSC traces of the melting process across a composition series and tabulated for use in exactly this kind of morphology prediction, and comparably measured enthalpies of fusion for Co–Si alloys found to differ from literature/estimated values, motivating direct experimental measurement rather than reliance on the Neumann–Kopp rule.
- Pressure/temperature-tuned systems show the same interface undergoing a **roughening transition** as thermodynamic conditions change: in high-pressure ice growth, the growth morphology changes from a circular disc to a hexagonal plate as temperature decreases and pressure increases along the melting curve, with growth kinetics simultaneously changing from linear to parabolic, interpreted as a roughening transition of specific crystallographic facets analyzed via the Jackson criterion.

This microscopic (kinetic, faceting) role of $L$ is complementary to, and operates on a different length/time scale than, the macroscopic Mullins–Sekerka morphological-stability role in Section 3 — the former governs the atomic-scale attachment kinetics and equilibrium shape of a facet, the latter governs the stability of a macroscopically flat front to long-wavelength perturbations. Both, however, trace back to the same underlying quantity, $L$, entering through the entropy of fusion in one case and through the Stefan flux-jump condition in the other.

## 5. Practical / Process-Engineering Consequences

### 5.1 Interface shape control in Czochralski-type growth
Because the latent heat generated at the interface must be conducted away either into the crystal or into the melt, the balance between crystal/crucible rotation-driven flow and buoyancy-driven convection in the melt directly affects interface curvature. As the melt level falls during a CZ pull, rotation-induced flow begins to dominate over buoyancy-driven flow, and this transition can destabilize the melt flow pattern, switching it from a single-cell pattern associated with a desirable convex solidification interface to a two-cell pattern associated with an undesirable concave interface — a shift that alters where the released latent heat is preferentially conducted and can amplify or damp interface perturbations per the Mullins–Sekerka mechanism above.

### 5.2 Growth-rate/thermal-gradient trade-off
In pulled-crystal methods generally, increasing the growth (pulling) rate raises the local rate of latent-heat release at the interface. If not matched by increased heat extraction, this destabilizes the process: as pulling rate increases with other conditions held fixed, growth can become unstable because the crystal temperature rises, causing melt and die/ampoule temperature increases and an uncontrolled increase in crystal diameter; this is generally addressed by increasing the temperature gradient near the interface to increase radiative heat loss from the growing crystal or by reducing heater power, though an excessively steep gradient raises the cooling rate enough to induce thermal strain and degrade crystal quality. This is a direct process-level manifestation of the Stefan-condition rate limit described in Section 2.

### 5.3 Latent heat in numerical melt-pool / solidification models
Latent heat release/absorption must be captured correctly in any quantitative thermal model of a moving solid–liquid front, well beyond crystal-pulling contexts. In laser-based additive manufacturing melt-pool modeling, for example, accounting for the latent heat of fusion in the heat-conduction model — alongside temperature-dependent thermophysical properties, with melting and crystallization phase transitions handled via a source-term method — leads to measurable melt-pool elongation (up to roughly 22% depending on process parameters) together with a modest reduction in pool width and penetration depth, and this latent-heat effect grows more pronounced at higher scanning speeds. This illustrates that the source-term ("apparent heat capacity" / enthalpy-method) treatment of $L$ used in melt-growth Stefan problems is the same numerical device used across the wider field of solidification modeling.

### 5.4 Directional solidification of alloys: thin-sample latent-heat data
Quantitative morphological-stability calculations require accurate latent-heat data as direct model input. In directional-solidification stability studies on the model alloy system CBr$_4$ (thin-sample analog experiments), the latent heat of fusion of the pure substance is tabulated alongside the melting temperature, liquidus slope, partition coefficient, solid–liquid surface tension, and solid/liquid densities and diffusion constant as the thermophysical parameter set entering the linear morphological stability analysis, with the capillary length parameter in the stability theory explicitly constructed as $\Gamma' = \sigma/L_0$ — i.e., latent heat per unit volume directly sets the scale of the capillarity term that competes with the destabilizing latent-heat-diffusion term identified in Section 3.

## 6. Summary of the Physical Roles of $L$

| Role | Mechanism | Governing framework |
|---|---|---|
| Sets interface energy balance / growth-rate limit | Flux jump $k_s\partial_nT_s - k_l\partial_nT_l = L_v V_n$ | Stefan moving-boundary problem |
| Destabilizes/stabilizes planar front | Differential latent-heat diffusion into solid vs. supercooled liquid, competing with capillarity (and solute, for alloys) | Mullins–Sekerka linear stability theory |
| Sets faceted vs. non-faceted growth habit | Entropy of fusion $L/T_m$ controls interfacial roughening (Jackson $\alpha$-factor) | Jackson roughness criterion |
| Governs melting/freezing asymmetry | Sign of where $L$ is supplied/removed relative to the interface | Mullins–Sekerka + Stefan condition |
| Constrains process parameters (pull rate, rotation, gradient) | Heat-extraction capacity vs. latent-heat generation rate | Furnace-scale global heat transfer (CGSim/CrysMAS/FEMAG-CZ/CrysVUn class models) |

## 7. Key References

1. Mullins, W. W. & Sekerka, R. F. "Morphological Stability of a Particle Growing by Diffusion or Heat Flow." *J. Appl. Phys.* **34**, 323 (1963).
2. Mullins, W. W. & Sekerka, R. F. "Stability of a Planar Interface During Solidification of a Dilute Binary Alloy." *J. Appl. Phys.* **35**, 444–451 (1964).
3. Alexandrov, D. V. & Galenko, P. K. "The Mullins–Sekerka theory: 60 years of morphological stability." *J. Appl. Phys.* **136**, 055103 (2024). https://doi.org/10.1063/5.0218324
4. Jackson, K. A. "Mechanism of Growth," in *Liquid Metals and Solidification* (ASM, 1958) — origin of the roughness/entropy-of-fusion ($\alpha$-factor) criterion for faceted vs. non-faceted growth.
5. Kirkpatrick, R. J. "Crystal Growth from the Melt: A Review." *American Mineralogist* **60**, 798–814 (1975). http://www.minsocam.org/ammin/am60/am60_798.pdf
6. Tiller, W. A., Jackson, K. A., Rutter, J. W. & Chalmers, B. "The redistribution of solute atoms during the solidification of metals." *Acta Metallurgica* **1**, 428–437 (1953) — foundational constitutional-supercooling paper.
7. Handbook of Crystal Growth (2nd ed.), Introductory chapter on constitutional supercooling and Mullins–Sekerka stability theory. http://lab.semi.ac.cn/library/upload/files/2017/4/14152727842.pdf
8. Derby, J. J. and co-workers (Minnesota group) — continuum modeling of Czochralski melt flow, interface shape, and latent-heat coupling to convection cell transitions; see e.g. U.S. Patent on "Apparatus and method for control of melt flow pattern in a crystal growth process." https://image-ppubs.uspto.gov/dirsearch-public/print/downloadPdf/5162072
9. Viñals, J. et al. "Morphological stability analysis of directional solidification in thin samples." *J. Crystal Growth* **89**, 405–414 (1988) — thermophysical parameter tabulation including latent heat for CBr$_4$ stability calculations.
10. Study on latent heats of fusion and crystallization behavior of Co–Si binary alloys, correlating measured $\Delta H_f$ with Jackson-criterion faceting predictions. https://www.sciencedirect.com/science/article/abs/pii/S0925838809014868
11. Study of morphology and kinetics in ionic crystals growing from their melts, relating entropy-of-fusion parameter to faceted/non-faceted growth transitions as a function of supercooling. https://www.sciencedirect.com/science/article/abs/pii/0022024884901830
12. Study of latent-heat effects on melt-pool shape/size in laser-based directional energy deposition, illustrating the enthalpy-method (source-term) treatment of $L$ in a non-crystal-growth solidification context. https://pmc.ncbi.nlm.nih.gov/articles/PMC9736679/
13. Bowden, F. P. & co-workers / general reviews on nonequilibrium pattern formation in interface dynamics, including the melting/freezing asymmetry argument for latent-heat-driven instability. https://arxiv.org/pdf/patt-sol/9801002

*(References 5, 7, 9–13 above are drawn from source material located during this search; page numbers/journal details for items without a DOI should be verified against the original publication before citation in a formal manuscript.)*


---

> [!NOTE]
> 
> Generated by Claude.ai
>
> Model: Sonet 5
>
> Prompt: Provide an extensive overview of the role of latent heat of fusion in crystal growth from the melt. Provide key references. Show the output in Markdown format.
