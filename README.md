# Heating System Design for a Residential Building

Thermal load calculation and heating system design for an 8-unit residential building, developed for the *Sperimentazione e Progettazione di Tecnologie Energetiche* course at Politecnico di Torino (A.Y. 2025–2026), supervised by Prof. Carlo Cima.

**Authors:** Alessandro Capodacqua, Gabriele De Stalis

## Overview

Given a three-level building (36 m × 24 m footprint — basement, living floor, non-walkable attic) located in Turin, the project covers the full design workflow of a residential heating system:

1. Assigning the building a geographic location and reference outdoor climatic conditions
2. Defining an internal layout with at least 4 apartment units
3. Selecting a realistic wall/floor stratigraphy with appropriate material thicknesses and thermophysical properties
4. Calculating the design thermal load for each room
5. Laying out the distribution network (heat generator, ducts, radiators, circulation pump) and sizing the pump head
6. Selecting the radiators and the heat generator
7. Verifying the generator's operating conditions and sizing the flue gas exhaust duct

The building has 8 apartments (~90 m² each), symmetric both vertically and horizontally, grouped into 4 representative exposures (North, South, South-East/South-West, North-East/North-West) to simplify the calculations without loss of generality.

## Methodology

- **Design conditions:** external design temperature Te = −8 °C (UNI 10349, Turin climatic zone), internal design temperature Ti = 20 °C (UNI 5364)
- **Transmittance & heat loss:** wall/floor/roof transmittances calculated per UNI EN ISO 6946; heat flux per element via UNI EN 12831 (Φ = U·A·(Ti − Te))
- **Ventilation losses:** air change rates per room use (0.5 vol/h standard rooms, 1 vol/h kitchens, 2 vol/h bathrooms)
- **Thermal bridges:** estimated with a simplified method at 15% of the sum of opaque + glazed + ventilation losses
- **Distribution network:** pipe sizing from mass flow and target velocity (1 m/s); head losses via the Fanning equation (distributed) and the β-coefficient method (localized, bends and radiators)
- **Pump selection:** sized on the most unfavorable circuit loop (worst-case pressure drop)
- **Generator sizing:** verified against Φ_gen > 1.15 · Φ_d per standard practice
- **Chimney sizing:** flue gas mass/volume flow rates from stoichiometric combustion of methane, natural draft verified against total head losses

## Key results

| Parameter | Value |
|---|---|
| Total building design thermal load Φ_d | 27.69 kW |
| Selected heat generator | Viessmann Vitodens 200-W, 32 kW condensing wall-hung boiler |
| Selected circulation pump | Grundfos CR 3-5 A-A-A-V-HQQV |
| Most unfavorable pressure drop | 128.4 kPa (bathroom, North-West apartment) |
| Chimney height | 7.5 m |
| Net chimney draft | +27.7 Pa (natural draft, no forced draft device needed) |
| Radiator model | Tema 4/681, 112.1 W/element |

## Repository structure

```
report/                       Original technical report (Italian, as submitted)
calculations/
  building-envelope/          Wall & floor stratigraphy, opaque/glazed surfaces,
                               attic, basement, ventilation & thermal bridges dispersion
  total-loads/                Per-room and whole-building thermal load summary
  distribution-network/       Radiator reference data, pipe sizing
  pump-head/                  Distributed & localized head losses, pump selection
  heat-generator/             Generator selection and performance
  chimney-sizing/             Flue gas flow rates, geometry, draft verification
  sources.md                  Standards, manufacturer data sheets used
drawings/                     AutoCAD MEP exports (floor plans, network layout)
images/                       Figures referenced in the report
```

All tables are provided as plain CSV files with translated (English) headers, split by calculation topic, so individual results can be checked or reused without opening the full report.

## Tools used

- **Excel / openpyxl** — thermal load calculations and automation
- **AutoCAD MEP** — floor plan drafting and heating network layout
- Manual calculations following UNI EN 12831-1, UNI EN ISO 6946, UNI 10349, UNI 5364, UNI 7357

## Notes on data fidelity

The CSV tables are a direct, unmodified transcription of the values reported in the original technical report. A few subtotal figures in the original document are labeled "kW" where the order of magnitude suggests "W" was intended (a units slip in the original spreadsheet export); these are flagged with a note in the relevant CSV rather than silently corrected, so the data stays faithful to what was actually submitted and graded.

## License

Academic project — shared for portfolio purposes. Please do not submit this work, or derivatives of it, as your own for academic credit.
