# Algorithm 1: H3 Cell Assignment for Hierarchical Spatial Units

This algorithm provides the procedure for transforming irregular spatial geometries (administrative, electoral, and postal) into adaptive H3 hexagonal representations.

## 1. Mathematical Framework
* **Resolution Mapping Function $T(A_i)$**: Assigns an H3 resolution $r_i \in \{0, \dots, 15\}$ based on the feature's area $A_i$ in square meters.
* **Geometry Buffering ($d_r$)**: To ensure complete coverage of irregular boundaries, a buffer is applied: $d_r = 0.5 \times \text{h3.edge\_length}(r, \text{unit='m'})$.
* **Fallback Mechanism**: If the initial resolution yields no cells, the system increments resolution ($r_i + k$) for up to three attempts ($k=1,2,3$).

## 2. Pseudocode Logic
1. **Project** geometry to a meter-based CRS (e.g., EPSG:27700).
2. **Compute Area** ($A_i$) and determine initial resolution $r$ via $T(A_i)$.
3. **Buffer** the geometry by distance $d_r$ to ensure boundary capture.
4. **Reproject** to WGS84 (EPSG:4326) for H3 compatibility.
5. **Generate Cells** using `H3_POLYFILL`.
6. **Fallback**: If empty, increment resolution and retry.
7. **Deduplicate** and store against the `Spatial_unit_ID`.
