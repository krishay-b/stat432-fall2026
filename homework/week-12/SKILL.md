---
name: cluster-compare
description: Compare several clustering algorithms on a dataset, select one, and write a one-page report presenting only the selected method. Use only when the user explicitly asks to use cluster-compare on a named dataset; never apply it on your own.
---

# cluster-compare

**Intent:** Given a dataset and its feature columns, decide how the observations group, choose one clustering method on stated evidence, and report it on a single page. The caller supplies the data file, the feature columns, any identifier or label columns, and a seed. Never assume them.

## Protocol

1. **Screen the data.** Report sample size, feature count, missingness, and feature scale. State whether features share units. Standardize features only when their scales differ materially; say which choice was made and why.
2. **Reduce if p is large.** When features greatly outnumber observations, compute PCA and retain components covering a stated share of variance. Cluster in that space and say so. Dimension reduction is preprocessing, never a clustering result.
3. **Fit at least three algorithms.** Include K-means, hierarchical clustering (state the linkage), and one graph- or density-based method such as spectral clustering. Run each over the same candidate range of cluster counts.
4. **Choose the number of clusters.** Use an internal criterion computed the same way for every method — average silhouette width is the default — and report the curve over the candidate range rather than a single number.
5. **Select one method.** Rank methods by the internal criterion at each method's own best cluster count. Break near-ties toward the method whose assignment is most stable under resampling: refit on bootstrap or subsampled data and report mean agreement. Name the rule before applying it.
6. **Interpret with held-aside labels only.** If true labels exist, they must not influence preprocessing, tuning, or selection. Use them once, after selection, to describe the groups.

## Required report

**Hard limit: one printed page**, counting every word, figure, and table. If the content does not fit, cut comparison detail first, never the selected method's evidence.

Present clustering results for **the selected method only**. Other methods may appear in a single comparison line or small table giving their selection criterion value — never their assignments, cluster sizes, profiles, or plots.

Include, in order:

1. **Setup**, 2-3 sentences: data, dimensions, preprocessing, seed.
2. **Method selection**, 2-3 sentences: algorithms tried, the criterion, the value for each, and why the winner won.
3. **One figure** showing the selected clustering: observations in two interpretable coordinates, colored by cluster. Label axes with their meaning and variance share. Use a colorblind-safe palette.
4. **One table** profiling the selected clusters: size plus the few features or components that most separate them.
5. **Findings**, 3-5 sentences: what the groups are, and what they correspond to if labels exist.
6. **Limitations**, 2-3 sentences: at minimum, whether the criterion separated the methods, and the stability of the chosen solution.

## Rules

- Clustering is unsupervised. State plainly that groups are discovered structure, not validated classes.
- Report the internal criterion to three decimals, and never call a difference meaningful when it is smaller than the spread across resamples.
- K-means and spectral methods depend on initialization: run many random starts, keep the best objective, and report the number of starts.
- Never report a cluster count chosen by eye from a plot alone.
- If one solution is a near-duplicate of another, say so rather than presenting them as distinct findings.
- If the best criterion value is weak in absolute terms, say the data may not have strong cluster structure. Do not manufacture a finding.
- Verify one reported number by recomputing it a second way, and say which.
- Plain, specific prose. No restating the table in sentences, no filler.
