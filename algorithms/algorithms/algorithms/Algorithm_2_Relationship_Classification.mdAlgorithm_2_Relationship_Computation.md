# Algorithm 2: Spatial Relationship Classification

This documents the logic for identifying 17 qualitative spatial relationships (Topological, Proximity, and Hierarchical) across heterogeneous hierarchies.

---

## 1. Relationship Taxonomy
The framework categorizes interactions into three primary domains:
* **Topological**: Identical, Complete Containment, Touch, Intersect, Overlap, Disjoint.
* **Proximity**: Neighbour (d=1), Close (d=2), Near (d=3,4), Far (d>4), Far Away (d=-1).
* **Hierarchical**: Direct Parent (Complete/Partial), Ancestor (Complete/Partial), Hierarchical Touch, Hierarchical Overlap.

---

## 2. Classification Logic (Pseudocode)
1. **Resolution Check**: Compare H3 resolutions ($r_i, r_j$) of the two feature representations.
2. **Same Resolution Path**:
    * Perform **Set Intersection** on H3 cell sets.
    * If overlap ratio $\rho > 10\%$, classify as *Overlap*.
    * If sets are disjoint, compute minimum `gridDistance` using the H3 traversal API.
    * Assign Proximity label based on distance $d$.
3. **Different Resolution Path**:
    * Map the finer-resolution cells to the coarser resolution using `h3SetToParent`.
    * Validate containment via geometric check to distinguish between *Complete* and *Partial*.
    * Check alignment with the coarser feature's boundary cells to identify *Hierarchical Touch*.

---

## 3. Results
This set-theoretic approach, replacing traditional vector-based intersection tests, achieved a **3.6x computational speedup** while identifying 11 relationship types not natively supported by DE-9IM.
