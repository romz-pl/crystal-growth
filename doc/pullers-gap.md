# Commercial Gallium Phosphide (GaP) Crystal Pullers

## 1. Why GaP Requires a Specialized Puller

Gallium phosphide cannot be grown from an open melt the way silicon or germanium can. Two properties of the material dictate the entire design of a GaP puller:

- **High melting point**: GaP melts at approximately 1467–1470 °C, considerably higher than GaAs (~1238 °C) and far higher than Si (1414 °C is comparable, but the dissociation problem below is unique to GaP).
- **High phosphorus dissociation pressure at the melting point**: at $T_m$, the equilibrium vapor pressure of phosphorus over the melt is on the order of 30–35 atm. If the melt is left open to a low-pressure atmosphere, phosphorus boils off preferentially, the melt becomes gallium-rich, and stable single-crystal growth is impossible.

The commercial solution, developed in the late 1960s and standard ever since, is the **Liquid Encapsulated Czochralski (LEC)** method: the melt surface is covered with a layer of molten, transparent boric oxide ($\text{B}_2\text{O}_3$), and the entire growth chamber is pressurized with an inert gas (usually $\text{N}_2$ or Ar) to a pressure equal to or exceeding the phosphorus dissociation pressure. This suppresses evaporative loss of phosphorus while still allowing the seed and growing crystal to be pulled up through the encapsulant layer in the conventional Czochralski manner.

Consequently, "a commercial GaP crystal puller" is in practice synonymous with a **high-pressure LEC puller**, mechanically and thermally similar to (and in most vendor product lines, the same basic platform as) the pullers used for LEC GaAs and InP, differing mainly in maximum operating pressure/temperature ratings and in crucible/susceptor/heater materials suited to the higher process temperature.

---

## 2. Core Architecture of a Commercial LEC Puller for GaP

A typical commercial LEC/GaP puller comprises:

1. **Pressure vessel (autoclave/chamber)**
   Stainless-steel, water-cooled, rated typically for 20–150 bar (some historical designs to 100 atm), since the operating pressure must exceed the ~30–35 atm phosphorus dissociation pressure of GaP with margin for safety and process control. <cite index="12-1,14-1">A crystal puller is loaded with material in a crucible with an outer graphite susceptor, melted, and the crystal is pulled in a pressurized atmosphere, with the melt completely encapsulated by boric oxide to prevent dissociation as the vapor pressure is matched or exceeded by inert gas pressure applied in the chamber.</cite>

2. **Heating system**
   Resistive graphite (carbon) heaters surrounding a graphite susceptor that holds the crucible; some designs use multiple independently controlled heater zones ("multi-heater" pullers) for improved axial/radial gradient control. <cite index="9-1">A new generation of high-pressure pullers used for large-diameter LEC crystal growth are designed for charges up to 50 kg and crucibles up to 12 inches, and are equipped with fully computerized process and diameter control systems.</cite>

3. **Crucible**
   Historically fused silica (quartz) for GaP; pyrolytic boron nitride (pBN) crucibles became standard for high-purity, low-dislocation LEC growth of III-V compounds generally, since pBN is chemically inert to the melt and to $\text{B}_2\text{O}_3$ at these temperatures.

4. **Liquid encapsulant system**
   A charge of anhydrous $\text{B}_2\text{O}_3$ is loaded above the polycrystalline GaP charge; on heating it melts first (lower melting point) and floats due to lower density, forming a transparent sealing layer through which the seed is dipped and the crystal withdrawn. <cite index="37-1">Gallium phosphide crystals are normally grown by the liquid encapsulated Czochralski technique under high pressure of inert gas using liquid boric oxide to suppress dissociation of the compound by loss of phosphorus, though diameter control in this method is extremely difficult and crystal growers using it are typically forced to accept crystals of widely varying diameter</cite> unless active diameter-control measures (weighing cells, diameter sensing, floating-plate apertures) are incorporated.

5. **Pull/rotation mechanism**
   A vertically travelling pull shaft carrying the seed holder, with independent seed and crucible rotation, feeding through a rotary pressure seal into the high-pressure chamber.

6. **Gas handling and pressure control**
   Inert gas ($\text{N}_2$ or Ar) supply, pressure regulation, and venting/safety systems, since the chamber must be pressurized well before and throughout melting to prevent GaP dissociation. <cite index="8-1">Some advanced puller variants additionally incorporate applied magnetic fields (from superconducting or resistive magnets) to suppress melt temperature fluctuations and improve crystal quality</cite> — a refinement more common on GaAs LEC pullers but mechanically transferable to GaP platforms.

7. **Automated diameter/weight control**
   Modern commercial units include computerized diameter control (optical or weighing-based) and process automation, evolved from the manual, operator-controlled systems of the 1960s–1970s.

### Typical GaP-specific process parameters
| Parameter | Typical value |
|---|---|
| Melt temperature | ≈1467–1500 °C |
| Encapsulant | $\text{B}_2\text{O}_3$, layer thickness ~2–5 cm |
| Chamber pressure | tens of atm (inert $\text{N}_2$/Ar), sufficient to exceed P dissociation pressure |
| Crucible material | fused silica or pBN |
| Typical pull rate | ~10 mm/hr (historical low-defect recipes) |
| Typical rotation rate | ~10 rpm |
| Wafer sizes commercially available | 2″ and 3″ (50.8 mm, 75 mm), historically also smaller diameters |

---

## 3. Commercial Manufacturers of GaP (LEC) Crystal Pullers

### 3.1 PVA TePla / PVA TePla Crystal Growing Systems (Germany) — current market leader
<cite index="19-1">PVA TePla's crystal growing systems for compound semiconductors are explicitly marketed for gallium arsenide (GaAs), indium phosphide (InP), and gallium phosphide (GaP), materials used in optoelectronics (LED and laser systems), semiconductor technology, high-frequency technology, solar technology, and telecommunications.</cite> PVA TePla is the direct successor of the German LEC/VGF puller business historically associated with Leybold/Metals Research-derived compound-semiconductor equipment lines, and is today the most prominent named commercial supplier of GaP-capable high-pressure LEC pullers, alongside VGF systems for the same material set. <cite index="20-1">The company (headquartered in Wettenberg, Hesse, Germany) operates a dedicated subsidiary, PVA TePla Crystal Growing Systems GmbH.</cite>

### 3.2 Historical Western manufacturers (Metals Research / Cambridge Instruments)
The founding commercial GaP puller design traces to <cite index="28-1">the 1968 work of S.J. Bass and P.E. Oliver, who built a Czochralski crystal puller specifically to grow gallium phosphide crystals by the liquid encapsulation technique, obtaining large crystals only lightly contaminated by the crucible and boric oxide encapsulant, with electrical properties comparable to epitaxial vapour-grown material.</cite> This work (at what was then the Services Electronics Research Laboratory in the UK) established the LEC method and directly informed the commercial "Melbourn"-type pullers subsequently produced by **Metals Research Ltd.** (later **Cambridge Instruments**, then **Metals Research/MSI**), which became the standard Western supplier of LEC pullers for GaAs, GaP, and InP through the 1970s–1990s. Much of this equipment lineage was later absorbed into what is now the PVA TePla / Leybold-descended product family.

### 3.3 Japanese manufacturers
Japanese compound-semiconductor producers (e.g., Sumitomo Electric, Hitachi Cable, Nippon Mining/JX Nippon, and others) historically operated in-house or custom-built high-pressure LEC pullers for GaP, often built to proprietary specifications by Japanese heavy-equipment or furnace manufacturers rather than sold as an off-the-shelf commercial product — reflected in the many Japanese-assignee patents on LEC GaP/GaAs pulling apparatus and process refinements (doping strategies, low-defect-density recipes, boron-oxide water-content control). <cite index="30-1">One representative patent from this lineage describes controlling the temperature gradient in the $\text{B}_2\text{O}_3$ encapsulant to roughly 200 °C/cm and doping with strongly reducing impurities (silicon or other species with reducing activity ≥ that of boron) to obtain low dislocation and etch-pit densities, using pull rates of about 10 mm/hr and rotation rates of about 10 rpm.</cite>

### 3.4 Wafer/crystal suppliers using LEC-grown GaP (indicating industry-standard growth method, not equipment vendors themselves)
These companies grow or resell LEC-GaP boules/wafers, confirming LEC as the universal commercial growth technique, though they are downstream material suppliers rather than puller manufacturers:
- <cite index="3-1">UniversityWafer, Inc. — GaP wafers grown using the LEC method with 6N high-purity materials.</cite>
- <cite index="4-1">Western Minmetals (SC) Corporation — single-crystal GaP grown by the LEC technique, offered in 2″/3″ diameters, doped n-type (S, Te) or p-type (Zn).</cite>
- <cite index="5-1">PAM-XIAMEN — GaP wafers grown by LEC, epi-ready or mechanical grade, n-type/p-type/semi-insulating, (111) or (100) orientation.</cite>
- <cite index="6-1">Stanford Advanced Materials — single-crystal GaP wafers up to 2″ diameter, grown by the LEC technique using 6N-purity materials.</cite>

### 3.5 Adjacent/generic crystal-growth-furnace suppliers
Some general compound-semiconductor furnace suppliers list GaP explicitly among the materials their monocrystalline growth furnaces are designed for: <cite index="22-1">monocrystalline growing furnaces are marketed for SiC, InP, GaP, GaAs, CdZnTe, and InSb, in addition to dedicated polycrystalline-GaAs and CdTe furnace lines.</cite> These tend to be broad-line Asian equipment manufacturers serving the compound-semiconductor furnace market generally, rather than GaP specialists.

---

## 4. Design Variants and Refinements Relevant to GaP LEC Pullers

- **Ex-situ vs. in-situ synthesis**: <cite index="10-1">Synthesis from high-purity elemental components can be performed either directly in the puller before crystal growth, or in a separate high-pressure synthesis vessel (~100 bar) prior to loading the puller for growth — the latter approach permits use of a puller with a smaller/cheaper pressure rating, at the cost of needing additional pBN crucibles and encapsulant charges.</cite> This same trade-off applies directly to GaP, whose phosphorus dissociation pressure is even higher than the arsenic dissociation pressure of GaAs, making in-situ synthesis considerably more demanding.
- **Diameter control aids**: because of the difficulty of visually/electronically tracking diameter through an opaque or reflective encapsulant, specialized inventions such as floating ceramic plates (silicon nitride, chosen for a density that floats at the GaP/$\text{B}_2\text{O}_3$ interface) have been patented to constrain and stabilize crystal diameter during LEC GaP growth. <cite index="37-1">By use of such a floating-plate method, crystals with diameters controlled to within ±1 mm of the desired diameter have been obtained, compared to the otherwise highly variable diameters typical of unmodified LEC GaP growth.</cite>
- **Magnetic-field-assisted LEC (MLEC)**: developed and demonstrated primarily on GaAs pullers, <cite index="8-1">using superconducting magnets capable of supplying transverse fields on the order of 0.3 Wb/m² at the crucible center, which reduced melt temperature fluctuations from 18 °C down to 0.1 °C and enabled successful growth of larger-diameter crystals</cite> — a design concept transferable to GaP pullers where melt convection and thermal fluctuation similarly limit crystal quality.
- **Multi-heater, computer-controlled, large-charge pullers**: <cite index="9-1">next-generation high-pressure pullers for large III-V boules are designed for crucibles up to 12″ and charges up to 50 kg, with fully computerized process and diameter-control systems</cite> — these platforms are typically shared across GaAs/GaP/InP product lines by the same vendor, with GaP requiring the highest pressure/temperature rating of the three.

---

## 5. Key References

1. **Bass, S.J.; Oliver, P.E.** "Pulling of gallium phosphide crystals by liquid encapsulation." *Journal of Crystal Growth*, Vols. 3–4 (1968), pp. 286–290. — The foundational paper establishing the LEC method specifically for GaP; describes the original Czochralski puller built for this purpose.
2. **U.S. Patent 4,303,464** — "Method of manufacturing gallium phosphide single crystals with low defect density" (assignee: Sumitomo Electric Industries lineage), describing LEC GaP growth with controlled $\text{B}_2\text{O}_3$ temperature gradient and reducing-impurity doping for low dislocation density.
3. **U.S. Patent 4,431,476** — "Method for manufacturing gallium phosphide single crystals," describing the rotary LEC pulling process from GaP melt and the underlying dissociation-pressure/encapsulation physics.
4. **U.S. Patent 4,264,385** — "Growing of crystals," describing a floating-plate diameter-control method specifically for LEC-grown GaP using a hot-pressed silicon-nitride floating plate.
5. **U.S. Patent 4,824,520 / 4,654,110** — "Liquid encapsulated crystal growth" / "Total immersion crystal growth," describing general LEC apparatus and encapsulant (boric oxide) requirements applicable to GaAs, GaP, InP and related III-V/II-VI systems.
6. **U.S. Patent 5,514,881** — "GaP light emitting device having a low carbon content in the substrate," containing a representative schematic and description of a commercial-style LEC GaP pulling apparatus (pressure vessel, susceptor, crucible, $\text{B}_2\text{O}_3$ cap, inert-gas pressurization).
7. Freiberger Compound Materials / industry papers on LEC puller scale-up for GaAs (directly analogous puller technology to GaP): e.g., *Journal of Crystal Growth* papers on 6″ SI-GaAs LEC growth in multi-heater, computer-controlled high-pressure pullers, and on LEC vs. VGF process comparison and cost trade-offs.
8. **PVA TePla Crystal Growing Systems** — current commercial technology overview for GaAs/InP/GaP LEC and VGF crystal-growing systems: https://www.pvatepla.com/en/technology-fields/crystal-growing/
9. OSHA "Semiconductors – Ingot Growing" technical background page — general description of LEC Czochralski apparatus, pressures, and encapsulation physics for III-V compound semiconductors: https://www.osha.gov/semiconductors/gallium-arsenide/ingot-growing

---

## 6. Summary

Commercial GaP crystal pullers are, almost without exception, **high-pressure Liquid Encapsulated Czochralski (LEC) systems**, engineered around the need to contain phosphorus dissociation pressures of ~30+ atm at the ~1470 °C melting point. The foundational design dates to Bass & Oliver's 1968 work, was commercialized by Western manufacturers such as Metals Research/Cambridge Instruments (now largely consolidated into **PVA TePla Crystal Growing Systems**, the leading present-day named commercial vendor explicitly marketing GaP-capable LEC/VGF systems) and paralleled by extensive in-house/proprietary Japanese equipment development reflected in the compound-semiconductor patent literature. Modern commercial units add computerized multi-zone heating, automated diameter control, and (on some platforms) magnetic-field damping of melt convection, but the core high-pressure LEC architecture established in the late 1960s remains unchanged in principle.


---

> [!NOTE]
> 
> Generated by Claude.ai
>
> Model: Sonet 5
>
> Prompt: Provide an extensive overview of commercial Gallium Phosphide (GaP) crystal pullers used for growing crystals from a melt. Provide key references. Show the output in Markdown format.
