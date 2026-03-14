# Algorithm 1: Adaptive H3 Cell Assignment for Hierarchical Spatial Units

This document provides the complete specification for transforming irregular spatial geometries (administrative, electoral, and postal) into adaptive H3 hexagonal representations, as described in Section 3.1 of the associated research paper.

## 1. Mathematical Framework

### 1.1 Resolution Mapping Function T(A<sub>i</sub>)

A threshold-based function T: ℝ⁺ → {0, 1, …, 15} assigns an H3 resolution r<sub>i</sub> based on the area A<sub>i</sub> (in m²) of spatial unit i. The thresholds are calibrated so that the assigned resolution produces cells whose average area is substantially smaller than the spatial unit being represented, ensuring adequate geometric coverage without excessive cell counts.

The complete mapping is provided in [Appendix A: Resolution Mapping Thresholds](./Appendix_A_Mapping.md).

Representative thresholds used in the Welsh dataset:

| Resolution | Area Range (m²) | Example Scale |
|:---:|:---|:---|
| 5 | A<sub>i</sub> ≥ 10,000,000,000 | Wales (~21,218 km²) → 129 cells |
| 7 | 100,000,000 ≤ A<sub>i</sub> < 1,000,000,000 | Districts |
| 9 | 1,000,000 ≤ A<sub>i</sub> < 10,000,000 | Castle Ward (~1.73 km²) → 30 cells |
| 11 | 100,000 ≤ A<sub>i</sub> < 500,000 | Small postal sectors |

### 1.2 Geometry Buffering

To ensure complete coverage of irregular boundaries, a minimal buffer is applied in a metre-based CRS (EPSG:27700, British National Grid):

> d<sub>r</sub> = 0.5 × h3.edge_length(r, unit='m')

The factor 0.5 ensures that H3 cell centres near the geometry's boundary are included in the polyfill operation whilst minimising over-coverage. The buffered geometry is then reprojected to WGS84 (EPSG:4326) for H3 polyfill.

For example, buffering increased Ely Community Ward's cell count from 31 to 52 cells at resolution 9, ensuring full boundary coverage.

### 1.3 Fallback Mechanism

To address cases where the initial resolution yields no H3 cells (e.g., due to small or irregular geometries), the resolution is incrementally increased:

> r<sub>i</sub><sup>(k)</sup> = T(A<sub>i</sub>) + k,  for k = 0, 1, 2, 3

The process terminates when cells are generated or the maximum of three increments is reached. The buffer is recalculated at each fallback resolution.

## 2. Pseudocode

```
ALGORITHM: H3 Cell Assignment for Spatial Units
────────────────────────────────────────────────

INPUT:  unit_dict  — dictionary mapping Spatial_unit_ID to Unit objects
                      with attributes: hierarchy_id, unit_level, geometry, name
        T(A)       — threshold-based resolution mapping function

OUTPUT: records    — list of {Spatial_unit_ID, assigned_res, h3_cells}

  1  records ← EMPTY_LIST
  2  FOR hid IN UNIQUE(unit_dict.values.hierarchy_id) DO
  3      hierarchy_units ← FILTER(unit_dict.values, hierarchy_id = hid)
  4      FOR level IN UNIQUE(hierarchy_units.unit_level) DO
  5          level_units ← FILTER(hierarchy_units, unit_level = level)
  6          FOR unit IN level_units DO
  7              projected_geometry ← PROJECT(unit.geometry, EPSG:27700)
  8              area ← COMPUTE_AREA(projected_geometry)          // area in m²
  9              IF area ≤ 0 THEN
 10                  APPEND({Spatial_unit_ID: unit.ID, assigned_res: -1, h3_cells: ∅}, records)
 11                  CONTINUE
 12              END IF
 13              res ← T(area)                                     // assign resolution
 14              std_geometry ← STANDARDIZE(projected_geometry)    // fix self-intersections,
 15                                                                // dissolve multipart
 16              buffer_dist ← 0.5 · h3.edge_length(res, unit='m')
 17              buffered_geometry ← BUFFER(std_geometry, buffer_dist)
 18              h3_input_geometry ← PROJECT(buffered_geometry, EPSG:4326)
 19              h3_cells ← H3_POLYFILL(h3_input_geometry, res)
 20              max_attempts ← 3
 21              attempt ← 0
 22              WHILE h3_cells = ∅ AND attempt < max_attempts DO
 23                  res ← res + 1                                 // increment resolution
 24                  buffer_dist ← 0.5 · h3.edge_length(res, unit='m')
 25                  buffered_geometry ← BUFFER(std_geometry, buffer_dist)
 26                  h3_input_geometry ← PROJECT(buffered_geometry, EPSG:4326)
 27                  h3_cells ← H3_POLYFILL(h3_input_geometry, res)
 28                  attempt ← attempt + 1
 29              END WHILE
 30              h3_cells ← UNIQUE(h3_cells)                       // deduplicate
 31              APPEND({Spatial_unit_ID: unit.ID, assigned_res: res,
 32                      h3_cells: JOIN(h3_cells, ",")}, records)
 33          END FOR
 34      END FOR
 35  END FOR
 36  RETURN records
```

## 3. Key Design Decisions

- **CRS handling**: Areas are computed in EPSG:27700 (British National Grid) for metric accuracy. Buffering is performed in the same metre-based CRS before reprojection to WGS84 for H3 compatibility.
- **Buffer factor (0.5)**: Selected through iterative testing; smaller factors (< 0.4) resulted in incomplete boundary coverage, larger factors (> 0.6) caused unnecessary over-coverage. The value 0.5 achieved a mean area error of 8.30% (SD = 4.80%) across the Welsh dataset (n = 3,242).
- **Deduplication**: Generated H3 cells are deduplicated before storage to eliminate redundancies introduced by buffering.

## 4. Implementation Notes

The algorithm is implemented in Python using:
- `h3-py` for H3 polyfill, edge length computation, and cell operations.
- `geopandas` and `shapely` for geometry standardisation and buffering.
- `ArcPy` for geospatial data management and feature extraction.

## 5. Reference

For the complete mathematical derivation and area thresholds, refer to Section 3.1 of the research paper and [Appendix A](./Appendix_A_Mapping.md).
