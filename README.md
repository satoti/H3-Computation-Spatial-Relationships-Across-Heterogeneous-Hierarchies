# H3-Based Computation of Qualitative Spatial Relationships

This repository contains the methodology, algorithms, and reference metrics for the research paper:  
**"H3-Based Computation of Qualitative Spatial Relationships Across Heterogeneous Geographic Hierarchies"** *Authors: Abdurauf Satoti and Alia I. Abdelmoty (Cardiff University)*

---

## 🗺️ Overview
Traditional Geographic Information Systems (GIS) often classify spatially separated features as simply `DISJOINT`. This framework leverages Uber's **H3 Discrete Global Grid System (DGGS)** to bridge heterogeneous hierarchies (Administrative, Electoral, and Postal) by:

1.  **Adaptive Transformation**: Converting irregular spatial units into standardized hexagonal cell sets based on feature area.
2.  **Qualitative Reasoning**: Identifying 17 distinct relationship types including Topological, Proximity (Neighbour, Close, Near, Far), and Hierarchical (Direct Parent, Ancestor).
3.  **High-Performance Computing**: Achieving a **3.6x computational speedup** compared to standard vector-based DE-9IM operations.

---

## 📂 Repository Contents
* **[Algorithm 1: H3 Cell Assignment](./algorithms/Algorithm_1_Cell_Assignment.md)**: Details the adaptive resolution mapping function $T(A_i)$ and the geometry buffering logic.
* **[Algorithm 2: Relationship Classification](./algorithms/Algorithm_2_Relationship_Classification.md)**: Documents the decision-tree logic for computing 17 spatial relationships via H3 set-theoretic operations.
* **[Reference Metrics: Mapping Thresholds](./algorithms/Appendix_A_Mapping.md)**: Provides the complete area thresholds ($m^2$) and average cell areas for H3 resolutions 0–15.

---

## 📈 Key Research Findings
* **Enhanced Semantics**: Introduced 11 relationship types absent in traditional topology, enabling queries such as *"Which postal sectors are Near this electoral ward?"*
* **Scalability**: Demonstrated robust performance across **2.6 million feature pairs** within the Welsh administrative landscape.
* **Data Integration**: Successfully identified functional equivalence (Identical relationships) between features with minor geometric vertex discrepancies.

---

## 🎓 Citation
If you use this framework or the mapping thresholds in your research, please cite:
> Satoti, A., & Abdelmoty, A. I. (2026). H3-Based Computation of Qualitative Spatial Relationships Across Heterogeneous Geographic Hierarchies. *Transactions in GIS* (In Submission).
---

## 🖼️ Visual Examples
Representative examples of the spatial relationships identified by the framework are provided in the [Algorithm 2 documentation](./algorithms/Algorithm_2_Relationship_Classification.md#4-illustrative-examples-from-the-welsh-case-study). These examples illustrate topological, proximity, and hierarchical classifications derived from the Welsh case study.

## ✉️ Contact
For questions regarding the methodology or data implementation, please contact **Abdurauf Satoti** at [SatotiAm@cardiff.ac.uk].
