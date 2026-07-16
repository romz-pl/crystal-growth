# Constitutional Supercooling in Crystal Growth from the Melt

## 1. Introduction and Historical Origin

Constitutional supercooling (CS) — sometimes called constitutional undercooling — is one of the foundational concepts in the theory of solidification of alloys and doped melts. It explains why a nominally planar solid–liquid interface, growing under conditions that would be thermally stable for a pure substance, can become morphologically unstable and break down into cells, dendrites, or other non-planar structures once a rejected (or absorbed) solute is present.

The term itself, along with a qualitative account of the phenomenon, was introduced by Rutter and Chalmers in their study of the cellular substructures formed during the solidification of tin. It was subsequently placed on a quantitative footing by Tiller, Jackson, Rutter, and Chalmers, whose 1953 paper is generally cited as the origin of the classical CS criterion. Winegard and Chalmers extended the concept to the promotion of heterogeneous nucleation and the formation of equiaxed grain structures ahead of a growing front.

CS remains central to crystal growth from the melt (Czochralski, Bridgman, float-zone, directional solidification, and related techniques) because it links macroscopic control parameters — growth rate, imposed thermal gradient, melt convection, and dopant/impurity concentration — to microscopic interface morphology, and hence to the ultimate crystalline quality, dopant homogeneity, and defect content of the grown crystal.

## 2. Physical Origin of the Effect

### 2.1 Solute Rejection at the Interface

During solidification of a binary (or multicomponent) melt with an equilibrium segregation coefficient $k_0 = C_s/C_l \neq 1$ (where $C_s$ and $C_l$ are the solid and liquid concentrations at the interface), solute is generally rejected into the liquid ($k_0 < 1$) or, less commonly, depleted from it ($k_0 > 1$) as the interface advances. Under diffusion-limited growth without convective mixing, this rejection builds up a boundary layer of enriched (or depleted) liquid immediately ahead of the interface, following the classical Burton–Prim–Slichter (BPS) or Scheil-type solute-boundary-layer profiles.

### 2.2 Depression of the Local Liquidus Temperature

Because the equilibrium liquidus temperature $T_L$ of the alloy is itself a function of local composition, $T_L = T_L(C_l)$, the solute-enriched layer ahead of the interface corresponds to a *lower* local liquidus temperature than the bulk melt. The actual temperature field near the interface, however, is set by the applied thermal gradient $G$ and is largely unaffected by the solutal boundary layer (since thermal diffusivity typically exceeds solutal diffusivity by two to four orders of magnitude — a large Lewis number). 

The result is that there can exist a region ahead of the interface where the *actual* local temperature $T(x)$ is lower than the *local equilibrium liquidus temperature* $T_L(C_l(x))$ dictated by the local solute concentration — even though the actual temperature increases monotonically away from the interface. This region is said to be constitutionally supercooled (or constitutionally undercooled): the liquid there is below its own freezing point given its local composition, even though it is not supercooled in the ordinary thermal sense.

### 2.3 Consequence for Interface Stability

If such a supercooled zone exists, any small protrusion of the solid interface into the melt finds itself growing into liquid that is *more* undercooled than the liquid at the original planar position, which promotes further, accelerated growth of the protrusion. This is a positive feedback mechanism: perturbations are amplified rather than damped, and the planar interface is morphologically unstable. Conversely, if no constitutionally supercooled region exists ahead of the interface, a protrusion grows into progressively warmer liquid (relative to the local liquidus), which suppresses the perturbation and the interface remains planar and stable.

## 3. The Classical Tiller–Rutter–Jackson–Chalmers Criterion

For steady-state directional solidification at velocity $V$, with an imposed temperature gradient $G$ in the liquid at the interface, and a diffusion-controlled solute boundary layer characterized by liquid diffusivity $D_l$, the classical criterion for the *onset* of constitutional supercooling compares the actual thermal gradient to the gradient of the liquidus temperature evaluated through the steady-state solute profile.

For the steady-state solute profile ahead of a planar interface (no convection, semi-infinite liquid), the concentration gradient at the interface is:

$$
\left.\frac{dC_l}{dx}\right|_{x=0} = -\frac{V}{D_l}\,C_l^{*}\,(1-k_0)
$$

where $C_l^{\ast}$ is the interfacial liquid concentration and $k_0$ is the equilibrium partition coefficient. Using the liquidus slope $m = dT_L/dC_l$ (negative for solute that depresses the melting point), the gradient of the local liquidus temperature at the interface is:

$$
\left.\frac{dT_L}{dx}\right|_{x=0} = m\left.\frac{dC_l}{dx}\right|_{x=0} = -\frac{m V C_l^{\ast}(1-k_0)}{D_l}
$$

The classical CS criterion states that the interface is **constitutionally stable** (no CS-driven breakdown) if the imposed thermal gradient in the liquid, $G_l$, exceeds the local liquidus gradient in magnitude:

$$
G_l \;\geq\; \left|\frac{dT_L}{dx}\right|_{x=0} = \frac{-m\,V\,C_l^{\ast}(1-k_0)}{D_l}
$$

or, in the commonly quoted equivalent form using the far-field (bulk) composition $C_0$ and equilibrium partition coefficient,

$$
\frac{G_l}{V} \;\geq\; \frac{-m\,C_0\,(1-k_0)}{k_0\,D_l}
$$

This is the celebrated $G/V$ criterion. It shows that CS — and hence interface breakdown into cells or dendrites — is promoted by:

- **Low imposed thermal gradient** $G$ (small $G/V$),
- **High growth rate** $V$ (small $G/V$),
- **Large solute partitioning** (small $k_0$, large $|1-k_0|$),
- **Steep liquidus slope** $|m|$,
- **High bulk solute concentration** $C_0$,
- **Low solutal diffusivity** $D_l$ in the melt.

Conversely, a planar interface can be stabilized by growing slowly, imposing a steep thermal gradient, using a system with $k_0$ close to unity, or working with dilute solutions.

### 3.1 Extension to Convective (Stirred) Melts

The original TRJC analysis assumed a purely diffusive boundary layer. Tiller and Rutter (and later Tiller alone) extended the theory to melts with imposed convection or forced stirring, relevant directly to Czochralski growth where crystal/crucible rotation drives forced convection. In a stirred melt, the diffusive boundary layer of thickness $\delta \sim D_l/V$ is replaced (for sufficiently vigorous stirring) by an effective boundary layer of thickness $\delta_{\text{eff}}$ set by the hydrodynamic boundary layer, generally expressed through the dimensionless Peclet number $Pe = V\delta_{\text{eff}}/D_l$ via the Burton–Prim–Slichter effective distribution coefficient:

$$
k_{\text{eff}} = \frac{k_0}{k_0 + (1-k_0)\exp(-Pe)}
$$

The CS criterion is then reformulated in terms of $k_{\text{eff}}$ and $\delta_{\text{eff}}$ rather than the purely diffusive length scale $D_l/V$, generally predicting that faster stirring reduces the effective boundary-layer thickness, suppresses the concentration gradient at the interface, and thus stabilizes the interface against CS-driven breakdown — though stirring can introduce its own oscillatory instabilities in the interface response.

## 4. Relationship to Mullins–Sekerka Morphological Stability Theory

The TRJC constitutional-supercooling criterion is a **necessary but not sufficient** condition for interface instability: it identifies the thermodynamic driving force (a locally supercooled liquid region) without accounting for the stabilizing role of interfacial energy (capillarity) or the coupling between solutal and thermal diffusion fields around a perturbed, curved interface.

Mullins and Sekerka developed the full linear morphological stability theory that supersedes the simple CS picture. Their analysis, is the basis for the evolution of phase interfaces and the formation of solid-phase microstructures, and proceeds by imposing an infinitesimal sinusoidal perturbation of wavenumber $\omega$ on the planar interface and solving the linearized heat and solute diffusion equations in both phases, subject to the Gibbs–Thomson (curvature-undercooling) boundary condition at the perturbed interface. The result is a dispersion relation giving the growth rate of the perturbation as a function of $\omega$, $V$, $G$, and material parameters, including the solid–liquid interfacial energy $\gamma$.

The key results of Mullins–Sekerka theory relevant here are:

1. **Long-wavelength perturbations** ($\omega \to 0$) are governed essentially by the classical CS criterion: if $G/V$ is below the CS threshold, long-wavelength perturbations grow.
2. **Short-wavelength perturbations** are stabilized by interfacial (capillary) energy through the Gibbs–Thomson effect, which raises the local equilibrium temperature at a convex solid protrusion, suppressing growth of very fine-scale perturbations regardless of the CS criterion.
3. There consequently exists a **band of unstable wavelengths** between a lower cutoff (set by capillarity) and an upper cutoff (set by the diffusion field), with a wavelength of maximum growth rate that sets the characteristic cell or dendrite spacing observed experimentally.
4. In the limit of vanishing interfacial energy and slow growth velocity, the Mullins–Sekerka marginal-stability condition reduces exactly to the classical constitutional-supercooling criterion, which is why CS is often described as the zeroth-order (capillarity-free) limit of the full morphological stability theory.

Later refinements by Sekerka, Coriell, Trivedi, Kurz and others (e.g., Trivedi–Kurz extensions to rapid solidification, and modifications accounting for interface attachment kinetics, finite liquidus slope curvature, and non-equilibrium partitioning) have generalized the stability criterion for high-speed (rapid) solidification regimes where local interfacial equilibrium breaks down and where the simple CS criterion no longer correctly predicts the stability boundary.

## 5. Constitutional Supercooling in Specific Growth Techniques

### 5.1 Czochralski (CZ) Growth

In CZ growth, forced convection from crystal and crucible rotation, together with buoyancy-driven convection, strongly modifies the solutal boundary layer relative to the purely diffusive case. The CS criterion in stirred-melt form governs the maximum pull rate achievable before the interface breaks down into facets, cells, or the formation of "constitutional supercooling defects" observed as bubble/void trapping or polycrystallization at high growth rate — behavior well documented for doped Ge and GeSi CZ crystals, where the critical growth velocity for the onset of polycrystallization via CS can be estimated directly from the local liquidus slope and dopant segregation behavior.

### 5.2 Bridgman / Vertical and Horizontal Gradient Freeze

In Bridgman-family growth (vertical Bridgman, VGF, horizontal Bridgman/HB), CS governs both interface breakdown into cellular substructure and the coupled question of axial/radial dopant homogeneity. Numerical modeling comparing diffusion-limited growth to convective regimes shows that purely diffusive Bridgman growth cannot be improved in chemical homogeneity by adjusting growth parameters alone, whereas convective transport (particularly in horizontal Bridgman configurations where the melt flow extends through the full melt volume rather than being confined to a boundary layer near the interface) significantly improves radial homogeneity, in better agreement with the classical Scheil and Tiller/Smith segregation formulae than purely diffusive numerical predictions.

### 5.3 Float-Zone and Related Techniques

In float-zone growth of semiconductors, the absence of a crucible removes one major impurity source but leaves CS-controlled cellular breakdown as a primary limit on achievable growth rate for heavily doped crystals, particularly for dopants with $k_0 \ll 1$.

### 5.4 Directional Solidification of Alloys (Casting/Ingots)

Beyond single-crystal growth, CS is the central mechanism controlling the columnar-to-equiaxed transition (CET) in cast alloys. As articulated by Winegard and Chalmers and extensively developed since, the constitutionally supercooled zone ahead of a columnar dendritic front provides both the thermodynamic driving force for heterogeneous nucleation of new equiaxed grains and, once such grains form, a "nucleation-free" protective zone around each new grain that shields it from remelting during subsequent thermal fluctuations. The extent of the constitutionally supercooled zone, often parameterized through the growth-restriction factor $Q$ (related to $m$, $C_0$, and $k_0-1$), is now a standard tool for predicting and controlling grain refinement in commercial alloys.

## 6. Practical Consequences for Crystal Quality

1. **Cellular/dendritic breakdown** of an intended planar interface leads to trapped solute at cell/dendrite boundaries, producing striations, inclusions, and locally variable dopant concentration — a major yield-limiting defect in doped semiconductor and oxide crystal growth.
2. **Maximum achievable growth rate** for a given dopant concentration and thermal gradient is set, to leading order, by the CS criterion; exceeding it produces the morphological transition from planar to cellular interface.
3. **Grain refinement in castings** is fundamentally a CS-mediated phenomenon, connecting alloy chemistry (via $m\,C_0(k_0-1)$, i.e., the growth-restriction factor) to the resulting as-cast grain size.
4. **Trade-off with productivity**: since higher $G/V$ suppresses CS, and $G$ is often limited by furnace/hot-zone design while $V$ determines throughput, CS sets a fundamental process-engineering constraint balancing crystal quality against growth rate in essentially all melt-growth techniques.

## 7. Key References

1. J. W. Rutter and B. Chalmers, "A prismatic substructure formed during solidification of metals," *Canadian Journal of Physics*, **31** (1953) 15–39. — Original qualitative introduction of the constitutional supercooling concept, explaining cellular substructure in solidified tin.

2. W. A. Tiller, K. A. Jackson, J. W. Rutter, and B. Chalmers, "The redistribution of solute atoms during the solidification of metals," *Acta Metallurgica*, **1** (1953) 428–437. — The foundational quantitative paper establishing the classical $G/V$ constitutional supercooling criterion.

3. W. A. Tiller and J. W. Rutter, "The effect of growth conditions upon the solidification of a binary alloy," *Canadian Journal of Physics*, **34** (1956) 96–121. — Extension of the CS analysis to a range of growth conditions.

4. V. G. Smith, W. A. Tiller, and J. W. Rutter, "A mathematical analysis of solute redistribution during solidification," *Canadian Journal of Physics*, **33** (1955) 723–745. — Classical solute-redistribution (segregation) formulae used alongside the CS criterion.

5. W. W. Mullins and R. F. Sekerka, "Morphological stability of a particle growing by diffusion or heat flow," *Journal of Applied Physics*, **34** (1963) 323–329.

6. W. W. Mullins and R. F. Sekerka, "Stability of a planar interface during solidification of a dilute binary alloy," *Journal of Applied Physics*, **35** (1964) 444–451. — Together with reference 5, these establish the full linear morphological stability theory that generalizes and supersedes the simple CS criterion.

7. W. A. Tiller, "Constitutional supercooling during crystal growth from stirred melts — I: Theoretical," *Solid State Electronics*, **1** (1961). — Extension of CS theory to stirred/convecting melts, directly relevant to Czochralski growth.

8. W. G. Pfann, "Zone Melting," 2nd ed., Wiley, New York, 1966. — Classic reference on solute redistribution during zone refining/float-zone growth, closely tied to CS-limited growth rates.

9. W. Kurz and D. J. Fisher, *Fundamentals of Solidification*, 4th ed., Trans Tech Publications, Aedermannsdorf, 1998. — Standard textbook treatment connecting CS theory to microstructure selection in castings and directional solidification.

10. M. E. Glicksman, *Principles of Solidification*, Springer, New York, 2011, Chapter 9 "Constitutional Supercooling." — Modern pedagogical synthesis of the classical theory and its limitations at high growth rate.

11. R. Trivedi and W. Kurz, "Morphological stability of a planar interface under rapid solidification conditions," *Acta Metallurgica*, **34** (1986) 1663–1670. — Extension of Mullins–Sekerka/CS theory to rapid solidification where local interfacial equilibrium breaks down.

12. S. R. Coriell and G. B. McFadden, "Morphological Stability," in *Handbook of Crystal Growth*, Vol. 1B, 2nd ed., Elsevier, Amsterdam, 2015, pp. 595–630. — Comprehensive modern review connecting CS to the full morphological stability framework, including convective and kinetic effects.

13. D. V. Alexandrov and P. K. Galenko, "The Mullins–Sekerka theory: 60 years of morphological stability," *Journal of Applied Physics*, **136** (2024) 055103. — Recent review revisiting and extending the Mullins–Sekerka framework, with direct discussion of its historical connection to constitutional supercooling.

14. W. A. Winegard and B. Chalmers, "Supercooling and dendritic freezing in alloys," *Transactions of the American Society for Metals*, **46** (1954) 1214–1224. — Extension of CS concepts to nucleation and equiaxed grain formation in castings.

15. D. StJohn, M. Qian, M. Easton, and P. Cao, "The Contribution of Constitutional Supercooling to Nucleation and Grain Formation," *Metallurgical and Materials Transactions A*, **46** (2015) 4868–4885. — Modern comprehensive review of CS's role in grain refinement, the growth-restriction factor, and nucleation-free zone formation.

16. Y. Yang, D. R. Poirier, et al. and related authors, "Numerical analysis of constitutional supercooling during directional solidification of alloys," relevant volume — Numerical comparison of CS-based classical segregation formulae against fully convective Bridgman-growth simulations.

17. E. Scheil, "Bemerkungen zur Schichtkristallbildung," *Zeitschrift für Metallkunde*, **34** (1942) 70–72. — Origin of the Scheil equation, the diffusionless-liquid segregation model frequently compared against CS-limited growth predictions.

---

*Prepared as part of the crystal-growth continuum-model reference library (interface physics / segregation / instabilities section).*

---

> [!NOTE]
> 
> Generated by Claude.ai
>
> Model: Sonet 5
>
> Prompt: Provide an extensive overview of the role of constitutional supercooling in crystal growth from the melt. Provide key references. Show the output in Markdown format.
