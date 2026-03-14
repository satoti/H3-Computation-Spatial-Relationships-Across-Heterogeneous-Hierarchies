# H3-Based Computation of Qualitative Spatial Relationships Across Heterogeneous Geographic Hierarchies

This repository provides the algorithms, reference metrics, and validation examples supporting the research paper:

> **Satoti, A. and Abdelmoty, A. I.** (submitted). H3-Based Computation of Qualitative Spatial Relationships Across Heterogeneous Geographic Hierarchies. *Transactions in GIS*.

**Authors:** Abdurauf Satoti and Alia I. Abdelmoty, School of Computer Science and Informatics, Cardiff University.

---

## Overview

Traditional Geographic Information Systems (GIS) classify spatially separated features as simply `DISJOINT`, providing no mechanism to capture graded proximity or hierarchical interactions across different administrative divisions. This framework uses Uber's **H3 Discrete Global Grid System (DGGS)** as a computational bridge between heterogeneous hierarchies (administrative, electoral, and postal) by:

1. **Adaptive Representation**: Converting irregular spatial units into standardised hexagonal cell sets using a dynamic resolution mapping function T(A<sub>i</sub>) that automatically assigns H3 resolutions based on feature area.
2. **Qualitative Relationship Computation**: Identifying **17 distinct relationship types** across topological, proximity, and hierarchical categories using set-theoretic operations over H3 cell sets.

---

## Repository Contents

| File | Description |
|:---|:---|
| [Algorithm 1: H3 Cell Assignment](./algorithms/Algorithm_1_Cell_Assignment.md) | Complete specification for adaptive resolution assignment, geometry buffering, and H3 tessellation, including full pseudocode. |
| [Algorithm 2: Relationship Classification](./algorithms/Algorithm_2_Relationship_Computation.md) | Classification logic for 17 spatial relationships with full pseudocode, 6 auxiliary functions, and validation examples. |
| [Appendix A: Mapping Thresholds](./algorithms/Appendix_A_Mapping.md) | Complete area thresholds for all 16 H3 resolution levels (0–15) with corresponding average cell areas. |
| [Technical Report](./documentation/H3_Relationships_computation_papers.pdf) | Full methodological documentation with mathematical framework, pseudocode, and evaluation results. |

---

## Key Research Findings

The framework was evaluated on **3,242 spatial units** across Welsh administrative, electoral, and postal hierarchies, comprising **2,627,499 cross-hierarchy feature pairs**.

| Metric | Result |
|:---|:---|
| **Computational speedup** | 3.6× faster than DE-9IM (49 min vs 177 min) |
| **Geometric fidelity** | Mean area error of 8.30% (SD = 4.80%) |
| **Functional equivalence** | 433 Identical relationships vs 11 EQUALS in DE-9IM |
| **Proximity semantics** | 1,025,984 disjoint pairs subdivided into Neighbour, Close, Near, Far categories |
| **Hierarchical awareness** | 6,537 hierarchical relationships invisible to conventional GIS |

---

## The 17 Relationship Types

**Topological** (same resolution): Identical, Complete Containment, Touch, Intersect, Overlap, Disjoint.

**Proximity** (same resolution, no shared cells): Neighbour (d=1), Close (d=2), Near (d=3–4), Far (d>4), Far Away (d=−1).

**Hierarchical** (different resolutions): Direct Parent Complete/Partial, Ancestor Complete/Partial, Hierarchical Touch, Hierarchical Overlap.

---

## Citation

If you use this framework or the mapping thresholds in your research, please cite:


```bibtex
@article{satoti2026h3,
  author  = {Satoti, Abdurauf and Abdelmoty, Alia I.},
  title   = {H3-Based Computation of Qualitative Spatial Relationships
             Across Heterogeneous Geographic Hierarchies},
  journal = {Transactions in GIS},
  year    = {2026},
  note    = {Manuscript submitted for publication}
}
```

**Methodological foundation:**

> Satoti, A. and Abdelmoty, A. I. (2025). A GIS-Native Framework for Qualitative Place Models: Implementation and Evaluation. *ISPRS International Journal of Geo-Information*, 14(12), 474. https://doi.org/10.3390/ijgi14120474

---

## Contact

For questions regarding the methodology or data, please contact **Abdurauf Satoti** at [SatotiAm@cardiff.ac.uk](mailto:SatotiAm@cardiff.ac.uk).

---

## Licence

This repository is licensed under the [MIT Licence](./LICENSE).
