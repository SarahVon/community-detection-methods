# Comparing Community Detection Methods in a Sparrow Association Network

[View the rendered analysis](https://01a0bbd5-5c89-a860-3c73-6fdd567d84b2.share.connect.posit.cloud/) · [View the R Markdown source](community-detection-methods.Rmd)

This project uses `R`, `asnipe`, and `igraph` to compare three community-detection algorithms on a weighted association network of golden-crowned sparrows. Fast Greedy, Edge Betweenness (Girvan–Newman), and Louvain are applied to the same graph so their partitions can be compared by community count, membership, community size, modularity, and network structure.

The analysis demonstrates an important feature of network modeling: a community is not an observed label already present in the data. It is a structure inferred by an algorithm, and different algorithms can produce different, but still plausible, summaries of the same network.

## Project goals

- Convert group-by-individual observations into a weighted association network.
- Use the Simple Ratio Index to quantify pairwise association strength.
- Compare agglomerative, divisive, and multilevel approaches to community detection.
- Evaluate the resulting partitions using modularity, community counts, sizes, and membership.
- Visualize both the network partitions and the hierarchical structure of applicable methods.
- Explain why algorithm choice matters when interpreting social-network structure.

## Data and network construction

The analysis uses the public [sample association dataset](https://dshizuka.github.io/networkanalysis/SampleData/Sample_association.csv) provided with network-analysis teaching materials by Shizuka and collaborators. The observations describe which individually identified golden-crowned sparrows were recorded in the same groups.

I imported the group-by-individual data and used `asnipe::get_network()` with the **Simple Ratio Index (SRI)** to calculate pairwise association strengths. SRI values summarize the proportion of observed opportunities in which two individuals occurred together. The resulting adjacency matrix was converted into an undirected, weighted `igraph` network containing **25 birds**.

![Weighted golden-crowned sparrow association network](golden-crowned-sparrow.png)

*Each node represents an individual sparrow. Edges represent observed association, with greater width indicating a higher SRI value.*

These weights describe co-occurrence in the supplied observations. They should not automatically be interpreted as friendship, preference, causation, or biological fitness.

## Tools and methods

The project was completed in **R** and documented in **R Markdown** using:

- `asnipe` for constructing the association matrix
- `igraph` for graph creation, community detection, modularity, membership, and plotting
- `rmarkdown` for combining code, results, interpretation, and figures in a reproducible report
- A fixed random seed (`246`) for consistent network layouts

The workflow was:

1. Import the association observations.
2. Transpose the group-by-individual structure into the orientation required for network construction.
3. Calculate pairwise SRI association values.
4. Create an undirected weighted graph.
5. Apply all three community-detection algorithms to the same graph.
6. Record modularity, number of communities, memberships, and community sizes.
7. Compare the partitions visually and numerically.

## Community detection methods

### Fast Greedy

Fast Greedy is a hierarchical, agglomerative method. It begins with each node in its own community and repeatedly merges communities when doing so produces the largest available increase in modularity. The sequence of mergers can be displayed as a dendrogram.

For this network, Fast Greedy identified **four communities** with sizes **9, 6, 5, and 5** and a modularity of **0.609**.
 
![Fast Greedy community-detection dendrogram](dendrogram-fast-greedy.png)

*The Fast Greedy dendrogram (above) shows the sequence of community mergers and the four-community cut used in the final partition.*


![Fast Greedy community detection result](fast-greedy.png)

*Fast Greedy partition of the sparrow network into four communities.*

### Edge Betweenness

Edge Betweenness, also known as the Girvan–Newman approach, is hierarchical and divisive. It begins with the full network and repeatedly removes edges that lie on many shortest paths. Those high-betweenness edges often act as bridges between otherwise cohesive parts of the graph.

For this network, Edge Betweenness identified **three communities** with sizes **13, 7, and 5** and a modularity of **0.566**.

![Edge Betweenness community detection result](edge-betweenness-girvan-newman.png)

*The Edge Betweenness dendrogram (above) shows the divisive hierarchy created as high-betweenness connections are removed.*

![Edge Betweenness community-detection dendrogram](dendrogram-edge-betweenness.png)

*Edge Betweenness partition of the sparrow network into three communities.*

### Louvain

Louvain is a multilevel modularity-optimization method. It first moves individual nodes among nearby communities to improve modularity, then collapses the resulting communities into higher-level nodes and repeats the process.

For this network, Louvain identified **four communities** with sizes **9, 6, 5, and 5** and a modularity of **0.609**. Although the numeric community labels differ from the Fast Greedy output, the individual memberships form the same four groups.

![Louvain community detection result](louvain-multilevel.png)

*Louvain partition of the sparrow network into four communities.*

## Results

| Method | Strategy | Communities | Community sizes | Modularity |
| --- | --- | ---: | --- | ---: |
| Fast Greedy | Agglomerative modularity optimization | 4 | 9, 6, 5, 5 | 0.609 |
| Edge Betweenness | Divisive bridge removal | 3 | 13, 7, 5 | 0.566 |
| Louvain | Multilevel modularity optimization | 4 | 9, 6, 5, 5 | 0.609 |

![Comparison of Fast Greedy, Edge Betweenness, and Louvain partitions](algorithm-comparison.png)

*The node positions are held consistent across the three plots so differences in community assignment can be compared directly.*

Fast Greedy and Louvain produced the same four-community partition and the same modularity score. Their agreement provides stronger support for this four-group representation than community count alone would provide. Edge Betweenness produced a broader three-community partition, combining or reassigning nodes that the modularity-optimization methods separated.

Within this analysis, the four-community partition is the best-supported summary because it was independently recovered by two methods and achieved the highest observed modularity. That conclusion remains specific to this graph, weight construction, and algorithm configuration; it does not prove that four fixed social groups exist in the underlying sparrow population.

## Interpretation and limitations

- Community detection is exploratory and algorithm-dependent. A partition is a model of structure, not direct evidence of a permanent biological group.
- The network depends on the original sampling design, observation effort, missing observations, and the decision to use SRI.
- SRI values represent association strengths. Some shortest-path algorithms interpret numeric edge weights as distances or costs, where larger values mean farther apart. Using association strengths directly in Edge Betweenness can therefore affect its partition; an inverse-distance transformation would be worth evaluating in a follow-up analysis.
- Modularity is useful for comparing partitions on the same graph, but it has known scale and resolution limitations. A higher value does not automatically make a partition biologically correct.
- The analysis compares one small sample network and should not be generalized to other populations, seasons, or species.
- Package updates can change default behavior, layouts, or numerical output. The project does not currently lock package versions.

## Reproducing the analysis

Install the required packages in R:

```r
install.packages(c("asnipe", "igraph", "rmarkdown"))
```

Then render the report from the repository root:

```r
rmarkdown::render("community-detection-methods.Rmd")
```

The R Markdown file downloads the public CSV at render time, so reproduction requires internet access and continued availability of the source URL. The checked-in HTML report and PNG figures preserve the published outputs if the remote file changes or becomes unavailable.

## Repository contents

| File | Description |
| --- | --- |
| [`community-detection-methods.Rmd`](community-detection-methods.Rmd) | R Markdown analysis source |
| [`community-detection-methods.html`](community-detection-methods.html) | Rendered analysis report |
| [`golden-crowned-sparrow.png`](golden-crowned-sparrow.png) | Original weighted association network |
| [`algorithm-comparison.png`](algorithm-comparison.png) | Side-by-side comparison of all three methods |
| [`dendrogram-fast-greedy.png`](dendrogram-fast-greedy.png) | Fast Greedy hierarchical structure |
| [`fast-greedy.png`](fast-greedy.png) | Fast Greedy community partition |
| [`dendrogram-edge-betweenness.png`](dendrogram-edge-betweenness.png) | Edge Betweenness hierarchical structure |
| [`edge-betweenness-girvan-newman.png`](edge-betweenness-girvan-newman.png) | Edge Betweenness community partition |
| [`louvain-multilevel.png`](louvain-multilevel.png) | Louvain community partition |
| `README.md` | Project documentation |
