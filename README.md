# H3-Based Computation of Qualitative Spatial Relationships

This repository contains the methodology, algorithms, and reference metrics for the research paper:  
**"H3-Based Computation of Qualitative Spatial Relationships Across Heterogeneous Geographic Hierarchies"** *Authors: Abdurauf Satoti and Alia I. Abdelmoty (Cardiff University)*

---

## 🗺️ Overview
Traditional Geographic Information Systems (GIS) often classify spatially separated features as simply `DISJOINT`. This framework leverages Uber's **H3 Discrete Global Grid System (DGGS)** to bridge heterogeneous hierarchies (Administrative, Electoral, and Postal) by:

1.  **Adaptive Transformation**: Converting irregular spatial units into standardized hexagonal cell sets based on feature area using a dynamic resolution mapping function $T(A_i)$.
2.  **Qualitative Reasoning**: Identifying **17 distinct relationship types** across Topological, Proximity, and Hierarchical domains.
3.  **Methodological Transparency**: Full technical specifications, mathematical proofs, and pseudocode are provided in the **[Technical Report (2026)](./H3_Relationships_computation_papers.pdf)**.

---

## 📂 Repository Contents
* **[Algorithm 1: H3 Cell Assignment](./algorithms/Algorithm_1_Cell_Assignment.md)**: Details the adaptive resolution mapping $T(A_i)$ and the geometry buffering logic ($d_r = 0.5 \times \text{edge_length}$).
* **[Algorithm 2: Relationship Classification](./algorithms/Algorithm_2_Relationship_Computation.md)**: Documents the logic for 17 spatial relationships via H3 set-theoretic operations (Overlap Ratio $\rho$ and Grid Distance $d$).
* **[Reference Metrics: Mapping Thresholds](./algorithms/Appendix_A_Mapping.md)**: Provides the complete area thresholds ($m^2$) for H3 resolutions 0–15.

---

## 📈 Key Research Findings
* **Performance**: Achieved a **3.6x computational speedup** compared to standard vector-based DE-9IM operations.
* **Fidelity**: Maintained a mean area approximation error of **8.30%**, suitable for qualitative reasoning.
* **Functional Equivalence**: Successfully identified **433 Identical relationships** where traditional vector models found only 11, reconciling minor boundary discrepancies.

---

## 🎓 Citation
If you use this framework or the mapping thresholds in your research, please cite:

**Journal Paper (In Submission):**
> Satoti, A., & Abdelmoty, A. I. (2026). H3-Based Computation of Qualitative Spatial Relationships Across Geographic Hierarchies. *Transactions in GIS / ISPRS International Journal of Geo-Information*.

**Doctoral Thesis (Methodology Foundation):**
> Satoti, A. (2026). *H3 Spatial Framework: Technical Specifications and Applicability*. [Doctoral dissertation, submitted for examination]. Cardiff University.

---

## ✉️ Contact
For questions regarding the methodology or data implementation, please contact **Abdurauf Satoti** at [SatotiAm@cardiff.ac.uk].
