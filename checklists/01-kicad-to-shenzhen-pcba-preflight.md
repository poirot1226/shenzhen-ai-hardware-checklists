# 01 · KiCad to Shenzhen PCBA Pre-Flight Checklist (5–3,000 Units)

Use this checklist before uploading Gerber, BOM, and Pick-and-Place (CPL) files to JLCPCB/LCSC, PCBWay, Seeed Fusion, or a Shenzhen Bao'an turnkey EMS factory.

> **Full Reference Tables & Tiered Cost Benchmarks (5 / 50 / 500 / 3,000 Units):**
> https://shenzhenaihardware.com/china-pcb-assembly

---

## A. Schematic & Component Selection (Before Routing)

- [ ] **Maximize LCSC Basic Parts (5–50 pc runs)**: Replace non-critical passives (resistors, caps, standard LEDs) with in-stock LCSC Basic part numbers to avoid ~$3 per-reel Extended component loading fees.
- [ ] **Audit AI-generated schematics manually**: Verify ESP32-S3 / nRF52 strapping pins (e.g., `GPIO0`, `GPIO45`) are not tied to active peripherals that block boot, and verify every MPN is active (not EOL) with matching pad-to-package footprints.
- [ ] **Confirm voltage & power ratings explicitly in BOM**: Never leave generic labels like `10uF 0603` without voltage rating (e.g., `16V X5R`) and dielectric spec.
- [ ] **Add Rev A bench-test points**: Include labeled pads for `3V3`, `5V`, `GND`, and `UART/SWD` programming headers so Rev A boards can be debugged without micro-soldering magnet wire.

## B. PCB Layout, Stackup & DFM Rules

- [ ] **Match factory DRC & impedance stackup**: Import the target fab's minimum trace/space (≥0.127 mm / 5 mil for 4-layer economic) and specify the exact controlled-impedance stackup code (e.g., `JLC04161H-7628`) for 50Ω Wi-Fi/BLE antennas and 90Ω USB-C differential pairs.
- [ ] **Keep SMD parts single-sided (Top layer only) on 5–50 pc prototypes**: Avoid double-sided SMT until enclosure geometry forces it; single-sided stays in Economic PCBA tiers and avoids dual-stencil/reflow setup fees.
- [ ] **Specify ENIG (Immersion Gold) for fine-pitch QFN/BGA/USB-C**: Avoid Lead-Free HASL on 0.4 mm pitch USB-C receptacles or MEMS microphones where uneven solder domes trigger bridges or cold joints.
- [ ] **Keep solid ground reference under RF & buck converters**: Do not split ground planes under Wi-Fi/BLE traces or switch-mode power loops.

## C. Gerber, Drill, BOM & CPL File Export

- [ ] **Export complete RS-274X Gerbers + Excellon Drills (`.zip`)**: Confirm `Edge.Cuts` outline is closed and PTH/NPTH drill files are clearly merged or labeled.
- [ ] **Use a rotation-normalized CPL/Centroid export**: Export via KiCad Fabrication Toolkit (or manually normalize `.pos` rotation offsets to Asian pick-and-place feeder conventions).
- [ ] **Inspect EVERY polarized part in the factory 3D Placement Viewer at 400% zoom**: Visually verify Pin-1 dots on every QFN IC, LDO, diode, LED, and USB-C connector before clicking Pay.
- [ ] **Attach Assembly Drawing PDF + explicit DNP list**: Mark unpopulated debug headers or optional sensors explicitly as `DNP` (Do Not Populate) so the factory does not stall or hand-solder unwanted parts.

## D. Shipping, Compliance & Commercial Scaling (50 → 500+ Units)

- [ ] **Ship Rev A prototypes dry (no Li-Po battery installed)**: Standard PCB air couriers reject loose or installed lithium cells without UN38.3 transport certification and DG-approved channels.
- [ ] **Separate compliance obligations from batch size**: Statutory FCC Part 15 / EU RED / UN38.3 compliance is triggered by RF capability, lithium batteries, and commercial market placement — *not* an arbitrary 300- or 500-unit legal cutoff. Confirm regulatory scope with an accredited lab before commercial sales.
- [ ] **Budget landed cost, not EXW factory price**: Factor in courier/DDP freight, HTS customs classification (e.g., US Section 301 tariffs where applicable), EU/UK EORI + VAT, and a functional pogo-pin test jig before quoting crowdfunding or retail margins.
- [ ] **Lock IP & factory verification before turnkey box-build**: Execute a bilingual PRC-law NNN agreement and verify the EMS entity before releasing full enclosure STEP files and firmware binaries.

---

*Related open checklists in this repository: [02 · China NNN & Factory Vetting](./02-china-nnn-and-factory-vetting.md) · [03 · Shenzhen Entry & Huaqiangbei](./03-shenzhen-entry-and-huaqiangbei-field-checklist.md)*
