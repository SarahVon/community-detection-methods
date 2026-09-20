# Community Detection Methods

This R/`igraph` portfolio analysis compares three community-detection algorithms on the Golden-crowned Sparrow association network from Shizuka et al. (2014): Fast Greedy, Edge Betweenness (Girvan–Newman), and Louvain.

## Workflow and methods

1. Download the sample association matrix from the public URL in the R Markdown source.
2. Transpose the matrix as required by the `asnipe` workflow.
3. Convert associations to a weighted adjacency matrix with the Simple Ratio Index (`asnipe::get_network`).
4. Build an undirected weighted `igraph` graph.
5. Run `cluster_fast_greedy()`, `cluster_edge_betweenness()`, and `cluster_louvain()`.
6. Compare dendrograms, network partitions, modularity, community counts, memberships, and community sizes.

Fast Greedy is hierarchical/agglomerative; Edge Betweenness is divisive and computationally intensive; Louvain is a multilevel modularity method. A fixed seed is used for plotted layouts where applicable. The rendered report is self-contained and contains plots, not an uploaded copy of the source CSV.

## Reproduction

Install R and the `asnipe` and `igraph` packages, then render `community-detection-methods.Rmd` with `rmarkdown::render()`. The source uses the public project-relative URL `https://dshizuka.github.io/networkanalysis/SampleData/Sample_association.csv`; no local absolute paths are required. Network access and the continued availability of that URL are prerequisites. Raw CSV/data files are intentionally omitted from this repository.

## Results and limitations

The source report found four communities for Fast Greedy and Louvain (modularity 0.609) and three for Edge Betweenness (modularity 0.566). These values are specific to this network, association index, package versions, and algorithm settings. Modularity can favor particular structures, algorithms can produce different partitions, and the association index affects edge weights. The analysis is exploratory and does not establish biological causation or generalize beyond the supplied sample network.

## Attribution

Network data: Shizuka et al. (2014), sample association data hosted at `dshizuka.github.io/networkanalysis/SampleData/Sample_association.csv`. Please consult the original publication and data terms before reuse. Software: R, `asnipe`, and `igraph`.

## Repository contents

- `community-detection-methods.Rmd` — source code and narrative.
- `community-detection-methods.html` — rendered report reviewed for local-path and private-data safety.
- `README.md` — workflow, methods, reproduction, attribution, and limitations.
- `.gitignore` — excludes local data and generated/intermediate files.

Author: Sarah Anderson.
