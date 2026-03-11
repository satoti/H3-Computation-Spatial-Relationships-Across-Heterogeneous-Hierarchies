# Algorithm 2: Spatial Relationship Computation

This documents the logic for identifying 17 qualitative spatial relationships (Topological, Proximity, and Hierarchical) across heterogeneous hierarchies.

---

## 1. Relationship Taxonomy
The framework categorizes interactions into three primary domains:
* **Topological**: Identical, Complete Containment, Touch, Intersect, Overlap, Disjoint.
* **Proximity**: Neighbour (d=1), Close (d=2), Near (d=3,4), Far (d≥5), Far Away (d=-1).
* **Hierarchical**: Direct Parent (Complete/Partial), Ancestor (Complete/Partial), Hierarchical Touch, Hierarchical Overlap.

---

## 2. Classification Logic (Pseudocode)
The overlap ratio ($\rho$) used in the following steps is defined as:
$$\rho = \frac{|A \cap B|}{\min(|A|, |B|)}$$
where $A$ and $B$ represent the H3 cell sets of the two spatial units, and $|A|$ denotes the number of cells in set $A$.

1. **Resolution Check**: Compare H3 resolutions ($r_i, r_j$) of the two feature representations.
2. **Same Resolution Path** ($r_i = r_j$):
    * Perform **Set Intersection** on H3 cell sets to find shared cells ($S$).
    * **Touch**: If overlap ratio $\rho \le 5\%$ and shared cells are on the boundary.
    * **Intersect**: If overlap ratio $\rho \le 10\%$.
    * **Overlap**: If overlap ratio $\rho > 10\%$.
    * If sets are disjoint, compute minimum **H3 grid distance** ($d$).
    * Assign Proximity label: **Neighbour** ($d=1$), **Close** ($d=2$), **Near** ($d=3,4$), or **Far** ($d \ge 5$).
3. **Different Resolution Path** ($r_i \neq r_j$):
    * Map the finer-resolution cells to the coarser resolution ($r_c$) using `h3SetToParent`.
    * Validate containment via **geometric union check** to distinguish between *Complete* and *Partial*.
    * Check alignment with the coarser feature's **border cells** to identify *Hierarchical Touch*.
---

## 3. Results
This set-theoretic approach, replacing traditional vector-based intersection tests used in the Dimensionally Extended Nine-Intersection Model (DE-9IM), achieved a **3.6x computational speedup** while identifying 11 relationship types not natively supported by traditional topology.

---

## 4. Illustrative Examples from the Welsh Case Study

### Topological Relationship: Identical
Demonstrates spatial equivalence across different hierarchies (administrative vs electoral) at H3 Resolution 5.
![Identical Relationship](../images/Wales_in_Adminstrative_in_electoral2.png)

---

### Proximity Relationship: Neighbour (d = 1)
Illustrates the "Neighbour" relationship where features share no common H3 cells but are directly adjacent in the grid (minimum grid distance $d=1$).
![Neighbour Relationship](../images/Whitchurch_Cf52_Nieghbouring2.png)

---

### Proximity Relationship: Near (d = 3–4)
Illustrates qualitative proximity based on H3 grid distance. In this example, the minimum H3 grid distance between feature sets is four cells.
![Near Relationship](../images/Cyncoed_f149_close_R_Map.png)

---

### Hierarchical Relationship: Direct Parent (Complete Containment)
Shows how finer-resolution H3 cells representing the CF23 postal sector (resolution 8) are fully contained within the coarser Cardiff administrative boundary (resolution 7).
![Direct Parent Containment](../images/Cardiff_Cf23_last_direct_containment_parent.png)

---
### Hierarchical Relationship: Complete Containment (Cross-Hierarchy Alignment)

This example demonstrates how the H3-based representation can reconcile
minor geometric inconsistencies between heterogeneous spatial datasets.

In the original vector geometries, the CF105 postal sector extends slightly
beyond the Butetown community boundary along the southern coastline.
However, after mapping both features to the H3 grid, all CF105 cells fall
within the H3 representation of Butetown.

As a result, the framework classifies the relationship as **Complete
Containment** in the discretised spatial model.

![Vector Geometry Context](../images/Butetown_cf105_extedndingbyond_bouundaries.png)

![H3 Cell Representation](../images/Cf105_Butetown_12Map.png)


### Hierarchical Relationship: Direct Parent (Partial Containment)
**Example: Lisvane and Thornhill ED / Thornhill Community**
As documented in the research appendix (Section F.10), a **Partial Containment** relationship is identified when the child H3 cell set is not fully contained within the parent's hexagonal representation. This example illustrates the limit of grid approximation where the geometric discrepancy is significant enough to be preserved in the qualitative output.
![Partial Containment](../images/Thornhill_Cells_H33_white2.png)
