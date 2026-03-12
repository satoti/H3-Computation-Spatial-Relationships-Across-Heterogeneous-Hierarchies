# H3-Based Computation of Qualitative Spatial Relationships

This repository contains the methodology, algorithms, and reference metrics for the research paper:  
**"H3-Based Computation of Qualitative Spatial Relationships Across Heterogeneous Geographic Hierarchies"** *Authors: Abdurauf Satoti and Alia I. Abdelmoty (Cardiff University)*

---

## 🗺️ Overview
[cite_start]Traditional Geographic Information Systems (GIS) often classify spatially separated features as simply `DISJOINT`[cite: 10]. This framework leverages Uber's **H3 Discrete Global Grid System (DGGS)** to bridge heterogeneous hierarchies (Administrative, Electoral, and Postal) by:

1.  [cite_start]**Adaptive Transformation**: Converting irregular spatial units into standardized hexagonal cell sets based on feature area using a dynamic resolution mapping function $T(A_i)$[cite: 11, 14, 16].
2.  [cite_start]**Qualitative Reasoning**: Identifying **17 distinct relationship types** across Topological, Proximity, and Hierarchical domains[cite: 7, 27].
3.  [cite_start]**Methodological Transparency**: Full technical specifications, mathematical proofs, and pseudocode are provided in the **[Technical Report (2026)](./H3_Relationships_computation_papers.pdf)**[cite: 6].

---

## 📂 Repository Contents
* [cite_start]**[Algorithm 1: H3 Cell Assignment](./algorithms/Algorithm_1_Cell_Assignment.md)**: Details the adaptive resolution mapping function $T(A_i)$ and the geometry buffering logic[cite: 12, 17].
* [cite_start]**[Algorithm 2: Relationship Classification](./algorithms/Algorithm_2_Relationship_Computation.md)**: Documents the decision-tree logic for computing 17 spatial relationships via H3 set-theoretic operations[cite: 26, 32].
* [cite_start]**[Reference Metrics: Mapping Thresholds](./algorithms/Appendix_A_Mapping.md)**: Provides the complete area thresholds ($m^2$) for H3 resolutions 0–15[cite: 21, 24].

---

## 📈 Key Research Findings
* [cite_start]**Performance**: Achieved a **3.6 speedup** over traditional vector-based DE-9IM operations (49 minutes vs. 177 minutes)[cite: 49].
* [cite_start]**Fidelity**: Maintained a mean area approximation error of **8.30%**, suitable for qualitative reasoning[cite: 50].
* [cite_start]**Functional Equivalence**: Successfully identified **433 Identical relationships** where traditional vector models found only 11, reconciling minor boundary discrepancies[cite: 51].

---

## 🎓 Citation
If you use this framework or the mapping thresholds in your research, please cite:

**Journal Paper (In Submission):**
> Satoti, A., & Abdelmoty, A. I. (2026). H3-Based Computation of Qualitative Spatial Relationships Across Heterogeneous Geographic Hierarchies. [cite_start]*Transactions in GIS / ISPRS International Journal of Geo-Information*[cite: 55, 56].

**Methodological Foundation (Technical Report):**
> Satoti, A. (2026). *Technical Report: H3-Based Spatial Representation and Relationship Modeling for Heterogeneous Hierarchies*. [cite_start]Cardiff University[cite: 1, 4].

---

## 🖼️ Visual Examples
Representative examples of the spatial relationships identified by the framework are provided in the [Algorithm 2 documentation](./algorithms/Algorithm_2_Relationship_Computation.md). [cite_start]These examples illustrate topological, proximity, and hierarchical classifications derived from the Welsh case study[cite: 47].

## ✉️ Contact
For questions regarding the methodology or data implementation, please contact **Abdurauf Satoti** at [SatotiAm@cardiff.ac.uk].
