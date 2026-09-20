# Community Detection Methods

An R/igraph analysis comparing Fast Greedy, Edge Betweenness (Girvan–Newman), and Louvain community-detection methods on a Golden-crowned Sparrow association network.

## Analysis sequence

1. Download the sample association matrix published by Shizuka et al. (2014).
2. Derive a weighted adjacency matrix with the Simple Ratio Index using `asnipe`.
3. Construct an undirected weighted `igraph` graph.
4. Run `cluster_fast_greedy()`, `cluster_edge_betweenness()`, and `cluster_louvain()`.
5. Compare modularity, community count, memberships, community sizes, network plots, and dendrograms in the rendered report.

## Outputs

- `community-detection-methods.Rmd` — reproducible source.
- `community-detection-methods.html` — self-contained rendered report with the generated plots, dendrograms, method comparisons, and reported results.

[Read the self-contained rendered report](community-detection-methods.html).

## Findings and limitations

The source report found four communities for Fast Greedy and Louvain (modularity **0.609**) and three for Edge Betweenness (modularity **0.566**). These results are specific to this network, association measure, software versions, and random-state choices. Community detection is exploratory: modularity can favor particular structures, algorithms can produce different partitions, and the association index affects edge weights. The analysis does not establish biological causation or generalize beyond the supplied sample network. Re-run the source with pinned package versions and a verified data URL before treating the values as a reproducible benchmark.

## Attribution

Network data: Shizuka et al. (2014), sample association data hosted at `dshizuka.github.io/networkanalysis/SampleData/Sample_association.csv`. Packages: `asnipe` and `igraph`. Check the original publication, data terms, package versions, and URL availability before reuse.

Author: Sarah Anderson.
