L61: "hint on" -> "suggest"

L138: "The more" -> "More"

L147: "comparative studies" -> "comparative study"

L149: "Signac" -> "Signac,"

L153-L157: Not clear how this conclusion is reached based on the benchmarks presented. In Figure 1c, it looks like APEC performs similarly to Cusanovich 2018, while SnapATAC has higher Entropy and ARI.

Fig. 1: Difficult to see that TooManyPeaks has very low ARI. May want to add an arrow or other callout to indicate that TooManyPeaks was benchmarked, but had a value of (or close to) zero.

L218-219: Given the many methods tested, I'm not sure pointing out Cicero's failure in the main text is appropriate (especially since the latest update in the linked issue is uncontested as of July 2019 - have the authors attempted to use the latest suggestion provided by Dr. Pliner?).

Figure 2a: There appear to be many terminal branches in this tree containing combinations of Neutrophils and T cells - highly distinct cell types that should not mix in successful clustering analysis. The authors should discuss whether they believe the cell type labels are incorrect, or the clustering is not working.

L220-L221, Figure 2b: The restriction of T3 B cells to one branch seems to be due to having only a single terminal node for all B cells. This doesn't seem to match the assertion that TooManyPeaks identifies specific, rare subsets of cells. B cells are a rather broad category of immune cells. If TooManyPeaks is able to identify rare cell types, shouldn't the T3 B cells be in their own node, separate from other B cell types? Otherwise, the comparison drawn to other methods seems to suggest that TooManyPeaks is better because its cluster assignment resolution is lower than other methods. There is also still the distinct possibility that the labeling method used is not accurate, and the T3 B cells label is wrong, leading to the dispersed label annotations seen in competing methods.

L263: "To gaining" -> "To gain"

L269: GATA3? Are these Th2 cells? May be good to hypothesize - these are rather hard to distinguish using transcriptomics, and a feather in TooManyPeaks' cap if so.

RUNX1 has been reported to suppress GATA3 expression: https://www.ncbi.nlm.nih.gov/pmc/articles/PMC2196077/#:~:text=Runx1%20Negatively%20Regulates%20Th2%20Differentiation,the%20Th2%20lineage%20(11).

Could be interesting biology there.





