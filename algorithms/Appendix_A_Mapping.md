# Reference Metrics: H3 Resolution Mapping Thresholds

This table provides the complete area thresholds ($m^2$) used by the mapping function $T(A_i)$ to assign H3 resolutions.

| H3 Res ($r_i$) | Area Threshold ($A_i$ in $m^2$) | Avg. Cell Area ($m^2$) |
| :--- | :--- | :--- |
| 0 | $A_i \ge 609,788,441,794,100$ | 4,357,449,416,078 |
| 1 | $86,801,780,399,000 \le A_i < \dots$ | 609,788,441,794 |
| 2 | $12,393,434,655,100 \le A_i < \dots$ | 86,801,780,399 |
| 3 | $1,000,000,000,000 \le A_i < \dots$ | 12,393,434,655 |
| 4 | $100,000,000,000 \le A_i < \dots$ | 1,770,347,655 |
| 5 | $10,000,000,000 \le A_i < \dots$ | 252,903,858 |
| 6 | $1,000,000,000 \le A_i < \dots$ | 36,129,062 |
| 7 | $100,000,000 \le A_i < \dots$ | 5,161,293 |
| 8 | $10,000,000 \le A_i < \dots$ | 737,328 |
| 9 | $1,000,000 \le A_i < \dots$ | 105,333 |
| 10 | $500,000 \le A_i < \dots$ | 15,048 |
| 11 | $100,000 \le A_i < \dots$ | 2,150 |
| 12 | $10,000 \le A_i < \dots$ | 307 |
| 13 | $1,000 \le A_i < \dots$ | 44 |
| 14 | $100 \le A_i < \dots$ | 6 |
| 15 | $A_i < 100$ | 0.9 |

*Note: Thresholds are designed to ensure cells are substantially smaller than the spatial units they represent.*
*Source: Table 1, [Technical Report](../documentation/H3_Relationships_computation_papers.pdf)*.
