# Community Detection Methods

**Published results:** [Read the rendered report](https://01a0bbd5-5c89-a860-3c73-6fdd567d84b2.share.connect.posit.cloud/)  
**Public source:** [`community-detection-methods.Rmd`](community-detection-methods.Rmd)

I use a weighted association network of golden-crowned sparrows to compare Fast Greedy, Edge Betweenness (Girvan–Newman), and Louvain community detection in R/`igraph`.

## Purpose

This analysis examines how three algorithms partition the same observed association network and how their modularity, community counts, and structural interpretations compare. The partitions describe this sample graph; they do not establish biological causation or fixed social groups.

## Setup and data

Install `asnipe`, `igraph`, and `rmarkdown`. The Rmd reads the public sample association file maintained by Shizuka and collaborators:

<https://dshizuka.github.io/networkanalysis/SampleData/Sample_association.csv>

The raw CSV is not redistributed. Rendering therefore requires internet access and continued availability of that URL.

## Workflow

1. Import and transpose the group-by-individual observations.
2. Calculate pairwise association strengths with the Simple Ratio Index (SRI).
3. Build an undirected weighted `igraph` graph.
4. Run each community algorithm and record modularity, membership, and community sizes.
5. Compare the partitions with network plots and, for the hierarchical methods, dendrograms.

SRI weights represent observed association opportunities in this sample, not friendship, causation, or fitness.

## Methods and results

![Golden-crowned Sparrow association network](golden-crowned-sparrow.png)

*Weighted association network; thicker edges indicate stronger SRI association.*

- **Fast Greedy:** four communities, modularity **0.609**.
- **Edge Betweenness:** three communities, modularity **0.566**.
- **Louvain:** four communities, modularity **0.609**.

![Fast Greedy, Edge Betweenness, and Louvain comparison](algorithm-comparison.png)

Fast Greedy and Louvain support the same four-community summary for this graph, while Edge Betweenness produces a broader three-community partition by removing high-betweenness bridges. Community count remains dependent on the algorithm and modeling choices.

The individual figures are [`dendrogram-fast-greedy.png`](dendrogram-fast-greedy.png), [`fast-greedy.png`](fast-greedy.png), [`dendrogram-edge-betweenness.png`](dendrogram-edge-betweenness.png), [`edge-betweenness-girvan-newman.png`](edge-betweenness-girvan-newman.png), and [`louvain-multilevel.png`](louvain-multilevel.png).

## Limitations

Results reflect the supplied observation process, SRI choice, graph construction, algorithm settings, and layout/package versions. Modularity is scale-dependent, and the sample should not be generalized beyond this network.

## Reproducibility

With R and the packages above installed, render:

```r
rmarkdown::render("community-detection-methods.Rmd")
```

The render step downloads the public CSV at runtime; checked-in PNGs document the published outputs.

## Repository contents

- `community-detection-methods.Rmd` — analysis source
- `community-detection-methods.html` — rendered report
- PNG files — network, dendrogram, and comparison figures
- `README.md` — methods, results, attribution, and reproduction notes
