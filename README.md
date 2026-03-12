# H3-Based Computation of Qualitative Spatial Relationships

This repository contains the methodology, algorithms, and reference metrics for the research paper:  
**"H3-Based Computation of Qualitative Spatial Relationships Across Heterogeneous Geographic Hierarchies"** *Authors: Abdurauf Satoti and Alia I. Abdelmoty (Cardiff University)*

---
## 🗺️ Overview

## 🗺️ Overview
Traditional Geographic Information Systems (GIS) often classify spatially separated features as simply `DISJOINT`. This framework leverages Uber's **H3 Discrete Global Grid System (DGGS)** to bridge heterogeneous hierarchies (Administrative, Electoral, and Postal) by:

1. **Adaptive Transformation**: Converting irregular spatial units into standardized hexagonal cell sets based on feature area using a dynamic resolution mapping function T(Ai).
2. **Qualitative Reasoning**: Identifying **17 distinct relationship types** across Topological, Proximity, and Hierarchical domains.
3. **Methodological Transparency**: Full technical specifications, mathematical proofs, and pseudocode are provided in the **[Technical Report (2026)](./documentations/H3_Relationships_computation_papers.pdf)**.

---

## 📂 Repository Contents
* **[Algorithm 1: H3 Cell Assignment](./algorithms/Algorithm_1_Cell_Assignment.md)**: Details the adaptive resolution mapping function T(Ai) and the geometry buffering logic (dr = 0.5 * edge length).
* **[Algorithm 2: Relationship Classification](./algorithms/Algorithm_2_Relationship_Computation.md)**: Documents the classification logic for computing 17 spatial relationships via H3 set-theoretic operations.
* **[Reference Metrics: Mapping Thresholds](./algorithms/Appendix_A_Mapping.md)**: Provides the complete area thresholds used for H3 resolution mapping (resolutions 0–15).

---

## 📈 Key Research Findings
* **Performance**: Achieved a **3.6 speedup** over traditional vector-based DE-9IM operations (49 min vs 177 min).
* **Fidelity**: Maintained a mean area approximation error of **8.30%**, confirming geometric fidelity suitable for qualitative reasoning.
* **Functional Equivalence**: Successfully identified **433 Identical relationships** where traditional vector models found only 11, reconciling minor boundary discrepancies.

---

## 🎓 Citation
If you use this framework or the mapping thresholds in your research, please cite:

**Journal Paper (In Submission):**
> Satoti, A., & Abdelmoty, A. I. (2026). H3-Based Computation of Qualitative Spatial Relationships Across Heterogeneous Geographic Hierarchies. *Transactions in GIS / ISPRS International Journal of Geo-Information*.

**Methodological Foundation (Technical Report):**
> Satoti, A. (2026). *Technical Report: H3-Based Spatial Representation and Relationship Modeling for Heterogeneous Hierarchies*. Cardiff University.

---

## ✉️ Contact
For questions regarding the methodology or data implementation, please contact **Abdurauf Satoti** at [SatotiAm@cardiff.ac.uk].
