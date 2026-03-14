# Appendix A: Complete H3 Resolution Mapping Thresholds

This table provides the complete area thresholds (in m²) used by the adaptive resolution mapping function T(A<sub>i</sub>) to assign H3 resolutions to spatial units. These thresholds are calibrated so that the assigned resolution produces cells whose average area is substantially smaller than the spatial unit being represented, ensuring adequate geometric coverage without excessive cell counts.

## Resolution Mapping Function T(A<sub>i</sub>)

| Resolution (r<sub>i</sub>) | Area Threshold (A<sub>i</sub> in m²) | Avg. Cell Area (m²) |
|:---:|:---|---:|
| 0 | A<sub>i</sub> ≥ 609,788,441,794,100 | 4,357,449,416,078 |
| 1 | 86,801,780,399,000 ≤ A<sub>i</sub> < 609,788,441,794,100 | 609,788,441,794 |
| 2 | 12,393,434,655,100 ≤ A<sub>i</sub> < 86,801,780,399,000 | 86,801,780,399 |
| 3 | 1,000,000,000,000 ≤ A<sub>i</sub> < 12,393,434,655,100 | 12,393,434,655 |
| 4 | 100,000,000,000 ≤ A<sub>i</sub> < 1,000,000,000,000 | 1,770,347,655 |
| 5 | 10,000,000,000 ≤ A<sub>i</sub> < 100,000,000,000 | 252,903,858 |
| 6 | 1,000,000,000 ≤ A<sub>i</sub> < 10,000,000,000 | 36,129,062 |
| 7 | 100,000,000 ≤ A<sub>i</sub> < 1,000,000,000 | 5,161,293 |
| 8 | 10,000,000 ≤ A<sub>i</sub> < 100,000,000 | 737,328 |
| 9 | 1,000,000 ≤ A<sub>i</sub> < 10,000,000 | 105,333 |
| 10 | 500,000 ≤ A<sub>i</sub> < 1,000,000 | 15,048 |
| 11 | 100,000 ≤ A<sub>i</sub> < 500,000 | 2,150 |
| 12 | 10,000 ≤ A<sub>i</sub> < 100,000 | 307 |
| 13 | 1,000 ≤ A<sub>i</sub> < 10,000 | 44 |
| 14 | 100 ≤ A<sub>i</sub> < 1,000 | 6 |
| 15 | A<sub>i</sub> < 100 | 0.9 |

## Notes

- Individual H3 cells vary slightly in area depending on their position on the icosahedral grid; the values reported here represent global averages from the [H3 specification](https://h3geo.org/docs/core-library/restable/).
- In the Welsh dataset evaluated in the associated research paper, assigned resolutions ranged from 5 (Wales, approximately 21,218 km²) to 11 (small postal sectors, approximately 0.1–0.5 km²), with 86.3% of features receiving resolutions 8 or 9.
- Resolutions 0–4 and 12–15 were not exercised in this study but are included for completeness, as the framework is designed to operate across any geographic context and spatial scale.

## Source

Table A1, Appendix A of the research paper; threshold values verified against the [H3 Cell Statistics documentation](https://h3geo.org/docs/core-library/restable/).
