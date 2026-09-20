# Community Detection Methods

An R/igraph analysis comparing Fast Greedy, Edge Betweenness (Girvan–Newman), and Louvain community-detection methods on a Golden-crowned Sparrow association network.

## Methods

The workflow downloads the sample association matrix published by Shizuka et al. (2014), derives a weighted adjacency matrix using the Simple Ratio Index with `asnipe`, and constructs an undirected weighted `igraph` graph. It then runs `cluster_fast_greedy()`, `cluster_edge_betweenness()`, and `cluster_louvain()`, reporting modularity, community count, memberships, and community sizes. Network plots and dendrograms are generated from the R Markdown source.

- `community-detection-methods.Rmd` — reproducible source.
- `community-detection-methods.html` — self-contained rendered report and visual reference.

## Rendered report

Read the [self-contained rendered report](community-detection-methods.html) for the generated network plots, dendrograms, method comparisons, and reported results.

## Interpretation and limitations

The source report found four communities for Fast Greedy and Louvain (modularity 0.609) and three for Edge Betweenness (modularity 0.566), but these results are specific to this network, association measure, software versions, and random-state choices. Community detection is exploratory: modularity can favor particular structures, algorithms can produce different partitions, and the choice of association index affects edge weights. The analysis does not establish biological causation or generalize beyond the supplied sample network. Re-run the source with pinned package versions and a verified data URL before treating the reported values as a reproducible benchmark.

## Attribution

Network data: Shizuka et al. (2014), sample association data hosted at `dshizuka.github.io/networkanalysis/SampleData/Sample_association.csv`. Packages: `asnipe` and `igraph`. **Attribution placeholder:** confirm the original publication citation, data license, package versions, and URL availability before publication.

Author: Sarah Anderson. Revised from coursework for portfolio presentation.
