# Commercial GaSb Crystal Pullers

## 1. Context: why GaSb growth equipment is a specialized niche

GaSb (melting point ≈ 712 °C, Sb vapor pressure at $T_m$ modest but non-negligible) sits in an unusual position among III–V melt-growth targets. Unlike GaAs or InP, its dissociation pressure at the melting point is low enough that many groups grow it in an **open, unpressurized quartz-tube LEC or Cz configuration**, without the 60–150 bar pressure vessels required for GaAs/InP. This means GaSb pullers are frequently *adapted general-purpose Czochralski or LEC systems* rather than a distinct commercial product line dedicated solely to GaSb. There is no major supplier building "GaSb-only" pullers; instead, GaSb is grown on:

1. General-purpose LEC/Cz pullers from crystal-growth-equipment houses (used with B₂O₃ or alkali-halide encapsulants under inert gas, unpressurized or lightly pressurized),
2. Vertical Bridgman / Vertical Gradient Freeze (VGF) furnaces from the same vendors, and
3. In-house or university-built systems, often descended from decommissioned commercial GaAs high-pressure pullers.

The two dominant melt-growth routes for commercial GaSb boules are **LEC** (still the majority production method, typically 2–3 inch, increasingly 4–6 inch) and **VB/VGF** (lower dislocation density, less common commercially for GaSb specifically, though well established for GaAs/InP).

---

## 2. Commercial puller platforms actually used for GaSb

### 2.1 Cyberstar / ECM Technologies (ECM Greentech, France — brand "Cyberstar")
The most consistently cited commercial platform in the compound-semiconductor LEC/Cz literature.

- **Oxypuller series** (Oxypuller 05-03, 20-04, 30-06/08/10): general oxide/compound Cz pullers, crucible sizes from lab-scale (300 g) up to 100 kg-class charges, crucible diameters up to 400 mm, working temperatures to 2300 °C.
- **High-Pressure LEC puller**: explicitly <cite index="20-1">marketed as highly suitable for production of III-V compound semiconductor crystals, e.g. GaAs, InP and InSb, by means of the high-pressure liquid-encapsulated Czochralski (HPLEC) method</cite>, and is fully computerized for closed-loop process control. Because GaSb has a much lower dissociation pressure than GaAs/InP, the same hardware is run at low or ambient pressure for GaSb, which is a comparatively gentle regime for this equipment class.
- Modular components sold separately — <cite index="21-1">pulling/translation mechanisms, rotation units with weighing devices, crucible rotation/translation stages, furnace chambers, water-cooled seed shafts, automatic feeders, and ADC (automatic diameter control) software</cite> — which is how many university and national-lab GaSb rigs are actually assembled (buy the Cyberstar motion/control stack, build a custom hot zone).
- Cyberstar also offers dedicated Bridgman furnaces with <cite index="26-1">mono- or multi-heater configurations and a rotating-thermocouple system that permits crucible rotation without losing crucible temperature measurement</cite> — directly relevant to VB/VGF GaSb growth.
- Successor branding: ECM Technologies / ECM Lab Solutions now sells the same lineage of hardware; <cite index="23-1">the Czochralski furnace line reaches 400 mm crucible diameter and 2300 °C, with pulling heads offering 0.01–100 mm/h translation speed and intuitive growth-monitoring software</cite>.

### 2.2 Melbourn / MCP-Metal Specialities (formerly Metals Research, UK) — high-pressure LEC pullers
Historically the workhorse of III-V LEC growth in Europe and widely retrofitted or referenced for GaSb-adjacent alloy work.
- <cite index="10-1,27-1">A Melbourn high-pressure puller was used for 3 kg LEC melts of In-doped GaAs, and the same class of transparent-furnace LEC rig has been used to grow Ga₁₋ₓInₓSb alloy crystals in the ⟨111⟩ direction from GaSb seeds</cite>. This illustrates the typical pattern: a puller purpose-built for GaAs/InP is repurposed for GaSb and its dilute alloys because the GaSb thermal/pressure regime is a comfortable subset of what the machine is designed for.

### 2.3 Legacy US platforms — Hamco / Metals Research CG-series, Cambridge Instruments
- The **Hamco CG800** (1970s-era) is a well-documented Cz/LEC stand still in active use as a rebuilt research platform; <cite index="7-1">a Hamco CG800 was completely rebuilt into a melt-replenishment Czochralski research platform, retaining the original stand and chambers while replacing the control system, power supply, and hot-zone components</cite>. Many academic GaSb growth papers of the 1980s–2000s trace back to Hamco- or Metals Research–derived stands.
- **Cambridge Instruments CI 358**: <cite index="16-1">an adapted CI 358 puller was used at Arizona State University for autonomous, digitally controlled high-pressure LEC growth of 4 kg, 3-inch GaAs boules</cite> — again, the same puller family is the platform of choice when groups extend their GaAs LEC capability to GaSb.

### 2.4 Chinese commercial suppliers (MTI Corporation and similar)
Lower-cost turnkey Cz/LEC systems increasingly used for GaSb R&D and small-scale production:
- <cite index="45-1">MTI's SKJ-50CZ is a Cz growth system rated to 2100 °C for up to 2-inch crystals, with a high-precision weighing-based diameter-control mechanism, pulling speed down to 0.03 mm/h, 1 rpm rotation, and a stainless steel water-cooled chamber evacuable to 3.75×10⁻⁵ torr</cite>, marketed for oxides, metals, and semiconductors generally; it and similar SKJ-series pullers are the entry-level commercial option seen in smaller Asian III-V labs.
- MTI also sells small Bridgman furnaces (e.g., SKJ-BG-1200) used analogously for VB-route GaSb work at lab scale.
- More broadly, GaSb-substrate suppliers such as those cataloged on III-V wafer marketplaces indicate an active but comparatively small-volume commercial GaSb market, consistent with GaSb pullers being adapted rather than purpose-built.

### 2.5 Full-scale industrial GaAs/InP puller platforms adaptable to GaSb
For context on the "high end" of what a GaSb-capable LEC puller *could* be scaled to (rarely needed for GaSb given its lower dissociation pressure, but same hardware family):
- <cite index="28-1">A new-generation multi-heater LEC puller designed for charges up to 50 kg and crucibles up to 12 inches has been used for 6-inch (200 mm) SI-GaAs growth</cite>, demonstrating the scale ceiling of the same commercial puller class that a 4–6 inch GaSb program (as pursued industrially in the last few years) would draw on.
- <cite index="35-1,37-1">Freiberger Compound Materials (FCM, Germany) is the only supplier historically using both LEC and VGF technologies in a single production line, up to 200 mm wafers, with VGF favored for high-current-density devices and LEC for larger-area, lower-current-density devices</cite> — the LEC/VGF duality mirrors exactly the two routes used for commercial GaSb.
- <cite index="40-1">AXT (USA) grows its III-V substrates by a proprietary VGF process, citing scalability, low stress, and low defect rates as key differentiators as diameters increase</cite>, illustrating the VGF-route alternative to LEC pullers at industrial scale.

---

## 3. Typical GaSb puller configuration (composite of the above platforms)

| Subsystem | Typical spec range for GaSb LEC/Cz | Notes |
|---|---|---|
| Crucible | Quartz or PBN, 2–6 inch charge diameter | Quartz common for lab/production LEC; PBN more common for VGF/VB ampoules |
| Encapsulant | B₂O₃, or KCl/LiCl eutectic | <cite index="11-1">Comparative studies show B₂O₃ vs. equimolar LiCl+KCl sealants give different thermal-field control and dislocation outcomes in LEC GaSb</cite> |
| Atmosphere | Inert gas (Ar, H₂ purge), low/ambient pressure | Contrasts with the 60–150 atm needed for GaAs/InP LEC on the same puller class |
| Pull rate | ~0.01–100 mm/h (hardware range); typical GaSb growth ~a few mm/h | <cite index="23-1">Cyberstar pulling heads are rated 0.01–100 mm/h</cite> |
| Rotation | Crystal and crucible counter-rotation, 0–~40–100 rpm hardware range | ACRT-style variable/oscillatory rotation used in related Bridgman GaSb/InSb work |
| Diameter control | Automatic (weight-sensing, ADC software) | Standard on Cyberstar/ECM and MTI mid/high-end systems |
| Heating | Resistive or inductive, depending on platform | Resistive more common for GaSb-scale (lower T) systems |

---

## 4. Growth-method landscape for GaSb specifically

- **LEC** remains <cite index="56-1">the primary industrial method for GaSb single-crystal growth, with 2-inch and 3-inch substrates dominating the market and 4–6 inch substrates still facing crystal-quality, reliability, and stability challenges</cite>.
- **VGF**, well established for GaAs/InP, has been demonstrated for 2-inch GaSb:Te: <cite index="38-1">2-inch-diameter Te-doped GaSb ingots were grown by VGF in quartz crucibles with an encapsulant; twinning at the seed/cone was a recurring problem with narrow seeds, but full-diameter, carefully oriented seeds gave single-crystal growth with dislocation densities as low as ~4–65 cm⁻²</cite>, positioning VGF as a credible low-defect alternative to LEC for GaSb, though not yet the dominant commercial route.
- Recent (2025) simulation-guided LEC optimization work is directly relevant to modern commercial puller practice: <cite index="15-1">a CGSim finite-element + machine-learning approach optimized crucible rotation and crystal-position configurations for GaSb LEC growth, reducing the solid–liquid interface protrusion angle to 0.086°, validated by X-ray double-crystal rocking curves and optical microscopy</cite>. A companion large-diameter study reports <cite index="28-1">a bottom-heater addition and optimized thermal field reducing 3-inch (100) GaSb substrate etch-pit density from 2842 to 147 cm⁻² (a 94.8% reduction), using a pulling rate of 8 mm/h and 2 rpm crucible rotation to minimize interface deflection</cite> — this is close to the state of the art for what a commercial LEC puller can achieve on GaSb today.

---

## 5. Key references

**Equipment / vendor sources**
- ECM Technologies / Cyberstar — Czochralski, LEC, Bridgman, Kyropoulos furnace lines: `ecm-usa.com/applications/crystal-growth`, `ecmlabsolutions.com/products/czochralski-crystal-growth/`, `cyberstar.fr`
- MTI Corporation — SKJ-series Cz and Bridgman systems: `mtixtl.com/products/skj-50cz`, `mtixtl.com/products/skj1200bg`
- DA Scientific Equipment Ltd. — Hamco CG800 rebuild case study: `dascientific.com/puller`
- Freiberger Compound Materials GmbH — LEC/VGF dual-technology production: `freiberger.com/en/technology/`
- AXT Inc. — VGF process for III-V substrates: semiconductor-today.com coverage of AXT 8-inch GaAs announcement

**GaSb-specific growth literature**
1. Kondo, S.; Miyazawa, S. "Low Dislocation Density GaSb Single Crystals Grown by LEC Technique." *J. Cryst. Growth* **1982**, *56*, 39–44.
2. Ohmori, Y.; Sugii, S.; Akai, K.; Matsumoto, K. "LEC Growth of Te-Doped GaSb Single Crystals with Uniform Carrier Concentration Distribution." *J. Cryst. Growth* **1982**, *60*, 79–85.
3. Cockayne, B.; Steward, V.; Brown, G.; MacEwan, W.; Young, M.; Courtney, S. "The Czochralski growth of gallium antimonide single crystals under reducing conditions." *J. Cryst. Growth* **1982**, *58*, 267–272.
4. Sunder, W. A.; Barns, R. L.; Kometani, T. Y.; Parsey, J. M.; Laudise, R. A. "Czochralski Growth and Characterization of GaSb." *J. Cryst. Growth* **1986**, *78*, 9–18.
5. Doerschel, J.; Geissler, U. "Characterization of Extended Defects in Highly Te-Doped ⟨111⟩ GaSb Single Crystals Grown by the Czochralski Technique." **1992**.
6. Costa, E.; De David, B.; Müller, A. "Investigations of structural defects by etching of GaSb grown by the liquid-encapsulated Czochralski technique." *Mater. Sci. Eng. B* **1997**, *44*, 208–212.
7. Reijnen, L.; Brunton, R.; Grant, I. "GaSb single-crystal growth by vertical gradient freeze." *J. Cryst. Growth* **2005**, *275*, e595–e600. (Also indexed as ScienceDirect record S002202480401485X.)
8. Study on liquid encapsulated Czochralski GaSb crystal growth technology (B₂O₃ vs. LiCl/KCl encapsulant comparison), *Journal of Piezoelectrics and Acoustooptics*, 2016.
9. Recent LEC optimization via simulation/ML for GaSb, *ACS Omega*, **2025**, DOI: 10.1021/acsomega.5c08508.
10. 200 mm-scale GaSb/GaAs LEC thermal-field optimization study (bottom heater, EPD reduction) — companion 2001/updated study, ResearchGate record 223099696.

**General LEC/VGF puller and defect-physics background (applies to GaSb via shared equipment/physics)**
- Modelling dislocation generation in high-pressure Czochralski growth of InP single crystals — Parts I & II (visco-plastic model), *J. Cryst. Growth*, ~2005.
- Autonomous LEC growth of GaAs by "intelligent" digital control, Arizona State University, *J. Cryst. Growth*, 1988.
- Liquid encapsulated Czochralski growth of 35 mm diameter GaP crystals (elastic anisotropy/stress modeling applicable across III-V LEC), *J. Cryst. Growth*, ~1988.
- OSHA process description of LEC Cz for compound semiconductors: `osha.gov/semiconductors/gallium-arsenide/ingot-growing`

**On the study of dislocation density in MBE GaSb-based structures** (defect-etchant and bulk-growth references compiled therein) — *Crystals* (MDPI), **2020**, 10, 1074.

---

## 6. Practical takeaway

There is no dedicated "GaSb crystal puller" product category as such — commercial GaSb boules are grown on the same LEC/Cz and VB/VGF platforms built for GaAs and InP (chiefly **Cyberstar/ECM**, legacy **Melbourn/Metals Research** and **Hamco/Cambridge Instruments** stands, and lower-cost **MTI**-class systems), simply run at the milder pressure/temperature regime GaSb's low dissociation pressure allows. The main current R&D frontier — reflected in the most recent literature — is scaling LEC GaSb from the well-established 2–3 inch range to 4–6 inch diameters while controlling interface shape and dislocation density, an effort increasingly guided by CGSim-style finite-element/ML process simulation rather than by any new puller hardware category.


---

> [!NOTE]
> 
> Generated by Claude.ai
>
> Model: Sonet 5
>
> Prompt: Provide an extensive overview of commercial Gallium antimonide (GaSb) crystal pullers used for growing crystals from a melt. Provide key references. Show the output in Markdown format.
