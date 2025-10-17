# decision_tree_significance

Graduate project: it is not possible to measure the "information gain" from the bottom layer of a decision tree (C4.5 in this case). Determine how (or if) to tell how significant the final split of a decision tree is.

Solution: after a decision tree has been fully created and tested, take the "bottom layer" leaf nodes with a shared parent node (i.e. "sibling" nodes) of a decision tree and assign a score (Accuracy x Correct), or (correct classifications ^2 / total classifications). Then merge the "sibling" nodes and take assign a score to the merged "parent" node. The final comparison adds the two siblings' scores and subtracts the re-merged parent's scores, (Acc.A x Cor.A) + (Acc.B x Cor.B) - (Acc.M x Cor.M) = split significance score.

The measure is simple to compute, compatible with standard pruning workflows, and can act as a practical heuristic for late-split evaluation. Our experiments on multiple real-world datasets show that this approach can identify and prune non-beneficial splits, improving model interpretability without compromising accuracy. Datasets
with many samples and fewer attributes more often exhibit families with nonzero delta, sometimes ≥ 0.6, reflecting informative last splits. In contrast, settings with few samples but many attributes frequently produce few evaluable families and many with delta ~= 0.

While usually within [0-1], this score is not a ratio, and recursive application "up" the decision tree is likely to give misleading information without further research and refinement.
