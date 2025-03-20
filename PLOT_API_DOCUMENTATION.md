# Plot API Documentation

This document provides API class-like documentation for each plot type defined in the provided Python code within the [figure_generation.py](https://github.com/pankajrajdeo/UCLA_Workshop/blob/main/figure_generation.py) script, detailing required and optional variables, their types, and descriptions based on standard practices.
---

## Table of Contents
1. [Stats Plot](#1-stats-plot-statsplotconfig)
2. [Heatmap Plot](#2-heatmap-plot-heatmapplotconfig)
3. [Radar Plot](#3-radar-plot-radarplotconfig)
4. [Cell Frequency Plot](#4-cell-frequency-plot-cellfrequencyplotconfig)
5. [Volcano Plot](#5-volcano-plot-volcanoplotconfig)
6. [Dot Plot](#6-dot-plot-dotplotconfig)
7. [Violin Plot](#7-violin-plot-violinplotconfig)
8. [Venn Plot](#8-venn-plot-vennplotconfig)
9. [UpSet Genes Plot](#9-upset-genes-plot-upsetgenesplotconfig)
10. [UMAP Plot](#10-umap-plot-umapplotconfig)
11. [Network Plot](#11-network-plot-networkplotconfig)

---

## 1. Stats Plot (`StatsPlotConfig`)
**Description**: Generates a TSV file of differentially expressed genes (DEGs) or marker genes based on the specified direction.

| Variable         | Required | Type                          | Description                                                                                     |
|------------------|----------|-------------------------------|-------------------------------------------------------------------------------------------------|
| `adata_file`     | Yes      | `str`                        | Path to the .h5ad AnnData file containing the dataset.                                          |
| `plot_type`      | Yes      | `Literal["stats", "all"]`    | Specifies the plot type. Must be "stats" or "all".                                             |
| `direction`      | Yes      | `Literal["regulated", "up", "down", "markers"]` | Gene regulation direction. Default is "regulated". Options determine DEGs or marker genes.     |
| `cell_type`      | Yes      | `str`                        | Specific cell type to focus on for DEG or marker gene analysis.                                |
| `disease`        | Yes      | `str`                        | Condition or disease to filter by for DEG analysis.                                            |
| `n_genes`        | No       | `Optional[int]`              | Number of top genes to include if `gene_symbols` is empty. Defaults to 100.                    |

---

## 2. Heatmap Plot (`HeatmapPlotConfig`)
**Description**: Visualizes gene expression across cells or aggregated groups in a heatmap.

| Variable              | Required | Type                          | Description                                                                                     |
|-----------------------|----------|-------------------------------|-------------------------------------------------------------------------------------------------|
| `adata_file`          | Yes      | `str`                        | Path to the .h5ad AnnData file to be analyzed.                                                  |
| `plot_type`           | Yes      | `Literal["heatmap", "all"]`  | Specifies the plot type. Defaults to "heatmap".                                                |
| `gene_symbols`        | Yes      | `List[Union[str, Dict]]`     | List of gene symbols or dictionaries with a 'Gene' key. Can be empty if inferred from metadata.|
| `cell_type_index`     | Yes      | `str`                        | Column name in `adata.obs` representing cell types.                                            |
| `covariate_index`     | Yes      | `str`                        | Column name in `adata.obs` representing the primary covariate (e.g., 'disease'). Defaults to "disease". |
| `covariates`          | Yes      | `List[str]`                  | List of covariate values for filtering. Includes "normal" by default for HLCA datasets.        |
| `display_variables`   | Yes      | `List[str]`                  | List of grouping fields for aggregation/visualization, derived from dataset metadata.          |
| `direction`           | Yes      | `Literal["regulated", "up", "down", "markers"]` | Gene regulation direction. Default is "regulated".                                     |
| `cell_type`           | No       | `Optional[str]`              | Specific cell type to subset data. Must match `cell_type_index`.                               |
| `cell_types_to_compare` | No     | `Optional[List[str]]`        | List of cell types to compare in the heatmap. Required if comparing multiple cell types.       |
| `disease`             | No       | `Optional[str]`              | Disease name to filter data. Inferred from `covariates` if not provided.                       |
| `covariate`           | No       | `Optional[str]`              | Single covariate value for filtering (deprecated; use `covariates`).                           |
| `show_individual_cells` | No     | `bool`                       | If True, displays individual cells. Defaults to True.                                          |
| `median_scale_expression` | No   | `bool`                       | If True, normalizes rows by subtracting median expression. Defaults to False.                  |
| `cluster_rows`        | No       | `bool`                       | Enables hierarchical clustering on rows (genes). Defaults to True.                             |
| `cluster_columns`     | No       | `bool`                       | Enables hierarchical clustering on columns (samples/groups). Defaults to True.                 |
| `heatmap_technology`  | No       | `Literal["seaborn", "imshow"]` | Heatmap rendering library. Defaults to "seaborn".                                            |
| `samples_to_visualize`| No       | `Literal["cell-type", "all"]` | Subset data by "cell-type" or use "all" cells. Defaults to "cell-type".                       |
| `restrict_studies`    | No       | `Optional[List[str]]`        | List of studies to restrict to (e.g., "Sun_2020" for HLCA). Defaults to None.                  |
| `study_index`         | No       | `Optional[str]`              | Column name for study metadata (e.g., "study" for HLCA). Defaults to None.                     |

---

## 3. Radar Plot (`RadarPlotConfig`)
**Description**: Renders a radar plot of average cell-type frequency by condition.

| Variable         | Required | Type                          | Description                                                                                     |
|------------------|----------|-------------------------------|-------------------------------------------------------------------------------------------------|
| `adata_file`     | Yes      | `str`                        | Path to the .h5ad AnnData file.                                                                |
| `plot_type`      | Yes      | `Literal["radar", "all"]`    | Specifies the plot type. Must be "radar" or "all".                                            |
| `covariate_index`| Yes      | `str`                        | Field in `adata.obs` representing the grouping variable (e.g., 'disease').                     |
| `donor_index`    | Yes      | `str`                        | Field in `adata.obs` representing the donor identifier.                                        |
| `cell_type_index`| Yes      | `str`                        | Field in `adata.obs` representing the cell type.                                               |
| `restrict_studies`| No      | `Optional[List[str]]`        | List of studies to restrict to (e.g., "Sun_2020" for HLCA). Defaults to None.                  |
| `study_index`    | No       | `Optional[str]`              | Column name for study metadata (e.g., "study" for HLCA). Defaults to None.                     |

---

## 4. Cell Frequency Plot (`CellFrequencyPlotConfig`)
**Description**: Generates a plot of cell frequencies across conditions, with the first covariate as the control group.

| Variable         | Required | Type                          | Description                                                                                     |
|------------------|----------|-------------------------------|-------------------------------------------------------------------------------------------------|
| `adata_file`     | Yes      | `str`                        | Path to the .h5ad AnnData file.                                                                |
| `plot_type`      | Yes      | `Literal["cell_frequency", "all"]` | Specifies the plot type. Must be "cell_frequency" or "all".                               |
| `covariates`     | Yes      | `List[str]`                  | List of conditions/diseases. First item is the control group.                                  |
| `cell_type_index`| Yes      | `str`                        | Field in `adata.obs` for cell-type annotation.                                                 |
| `covariate_index`| Yes      | `str`                        | Field in `adata.obs` representing disease/condition.                                           |
| `donor_index`    | Yes      | `str`                        | Field in `adata.obs` representing the donor identifier.                                        |
| `sex_index`      | Yes      | `str`                        | Field in `adata.obs` representing sex or gender annotations.                                   |
| `restrict_studies`| No      | `Optional[List[str]]`        | List of studies to restrict to (e.g., "Sun_2020" for HLCA). Defaults to None.                  |
| `study_index`    | No       | `Optional[str]`              | Column name for study metadata (e.g., "study" for HLCA). Defaults to None.                     |

---

## 5. Volcano Plot (`VolcanoPlotConfig`)
**Description**: Creates a volcano plot from precomputed differential expression results.

| Variable         | Required | Type                          | Description                                                                                     |
|------------------|----------|-------------------------------|-------------------------------------------------------------------------------------------------|
| `adata_file`     | Yes      | `str`                        | Path to the .h5ad AnnData file.                                                                |
| `plot_type`      | Yes      | `Literal["volcano", "all"]`  | Specifies the plot type. Must be "volcano" or "all".                                          |
| `cell_type`      | Yes      | `str`                        | Cell type used in the DE comparison for labeling.                                              |
| `disease`        | Yes      | `str`                        | Condition used in the DE comparison for labeling.                                              |
| `direction`      | Yes      | `Literal["regulated", "up", "down", "markers"]` | Gene regulation direction. Default is "regulated".                                     |
| `top_n`          | No       | `Optional[int]`              | Number of top genes to highlight. Defaults to 8.                                               |

---

## 6. Dot Plot (`DotPlotConfig`)
**Description**: Plots gene expression with dot size representing fraction and color representing expression level.

| Variable         | Required | Type                          | Description                                                                                     |
|------------------|----------|-------------------------------|-------------------------------------------------------------------------------------------------|
| `adata_file`     | Yes      | `str`                        | Path to the .h5ad AnnData file.                                                                |
| `plot_type`      | Yes      | `Literal["dotplot", "all"]`  | Specifies the plot type. Must be "dotplot" or "all".                                          |
| `disease`        | Yes      | `str`                        | Condition for DE comparison. Defaults to "normal" or "control" if not specified.               |
| `covariates`     | Yes      | `List[str]`                  | List of conditions to filter by. Must be non-empty; defaults to all diseases if unspecified.   |
| `covariate_index`| Yes      | `str`                        | Field in `adata.obs` representing disease/condition.                                           |
| `cell_type_index`| Yes      | `str`                        | Column name in `adata.obs` representing cell type.                                             |
| `direction`      | Yes      | `Literal["regulated", "up", "down", "markers"]` | Gene regulation direction. Default is "regulated".                                     |
| `gene_symbols`   | Yes      | `List[Union[str, Dict]]`     | List of genes or dictionaries with a 'Gene' key. Can be empty if inferred.                     |
| `cell_type`      | No       | `Optional[str]`              | Specific cell type to visualize (optional for multi-cell-type plots).                          |
| `restrict_studies`| No      | `Optional[List[str]]`        | List of studies to restrict to (e.g., "Sun_2020" for HLCA). Defaults to None.                  |
| `study_index`    | No       | `Optional[str]`              | Column name for study metadata (e.g., "study" for HLCA). Defaults to None.                     |

---

## 7. Violin Plot (`ViolinPlotConfig`)
**Description**: Displays the distribution of expression for a single gene across specified covariates.

| Variable         | Required | Type                          | Description                                                                                     |
|------------------|----------|-------------------------------|-------------------------------------------------------------------------------------------------|
| `adata_file`     | Yes      | `str`                        | Path to the .h5ad AnnData file.                                                                |
| `plot_type`      | Yes      | `Literal["violin", "all"]`   | Specifies the plot type. Must be "violin" or "all".                                           |
| `gene`           | Yes      | `str`                        | Single gene symbol to plot. Must exist in `adata.var_names`.                                   |
| `cell_type`      | Yes      | `str`                        | Specific cell type to focus on.                                                                |
| `covariates`     | Yes      | `List[str]`                  | List of conditions to filter by. Must be non-empty.                                            |
| `covariate_index`| Yes      | `str`                        | Primary grouping index in `adata.obs` (e.g., 'disease').                                       |
| `cell_type_index`| Yes      | `str`                        | Column name in `adata.obs` representing cell type.                                             |
| `display_variables`| Yes    | `List[str]`                  | List of grouping fields for aggregation/visualization, derived from metadata.                  |

---

## 8. Venn Plot (`VennPlotConfig`)
**Description**: Shows overlap of marker genes or DEGs for 2-3 cell types or covariates.

| Variable            | Required | Type                          | Description                                                                                     |
|---------------------|----------|-------------------------------|-------------------------------------------------------------------------------------------------|
| `adata_file`        | Yes      | `str`                        | Path to the .h5ad AnnData file.                                                                |
| `plot_type`         | Yes      | `Literal["venn", "all"]`     | Specifies the plot type. Must be "venn" or "all".                                             |
| `cell_types_to_compare` | No   | `Optional[List[str]]`        | List of 2 or 3 cell types for marker gene comparison. omit if comparing DEGs by covariates.    |
| `covariates`        | No       | `Optional[List[str]]`        | List of 2 or 3 covariates for DEG comparison. Provide only if comparing covariates.            |
| `cell_type`         | No       | `Optional[str]`              | Cell type to filter DEGs by, required only for covariate DEG comparison.                       |

---

## 9. UpSet Genes Plot (`UpSetGenesPlotConfig`)
**Description**: Handles complex overlaps of marker genes or DEGs across multiple cell types or covariates.

| Variable            | Required | Type                          | Description                                                                                     |
|---------------------|----------|-------------------------------|-------------------------------------------------------------------------------------------------|
| `adata_file`        | Yes      | `str`                        | Path to the .h5ad AnnData file.                                                                |
| `plot_type`         | Yes      | `Literal["upset_genes", "all"]` | Specifies the plot type. Must be "upset_genes" or "all".                                    |
| `cell_types_to_compare` | No   | `Optional[List[str]]`        | List of cell types for marker gene intersection. omit if comparing DEGs by covariates.          |
| `covariates`        | No       | `Optional[List[str]]`        | List of covariates for DEG intersection. Provide only if comparing covariates.                 |
| `cell_type`         | No       | `Optional[str]`              | Cell type to filter DEGs by, required only for covariate DEG comparison.                       |

---

## 10. UMAP Plot (`UmapPlotConfig`)
**Description**: Generates a UMAP visualization of single-cell data.

| Variable         | Required | Type                          | Description                                                                                     |
|------------------|----------|-------------------------------|-------------------------------------------------------------------------------------------------|
| `adata_file`     | Yes      | `str`                        | Path to the .h5ad AnnData file.                                                                |
| `plot_type`      | Yes      | `Literal["umap", "all"]`     | Specifies the plot type. Must be "umap" or "all".                                             |
| `covariates`     | Yes      | `List[str]`                  | Values within `covariate_index` to subset on. Defaults to "normal" or "control" if unspecified.|
| `covariate_index`| No       | `Optional[str]`              | Column in `adata.obs` to subset data (e.g., 'condition').                                      |
| `color_by`       | No       | `Optional[str]`              | Metadata column or gene to color the UMAP. Defaults to 'celltype' or another field if not provided. |
| `cell_type_index`| No       | `Optional[str]`              | Column in `adata.obs` used for clustering. Defaults to `color_by` if not provided.             |
| `gene`           | No       | `Optional[str]`              | Gene name to color by expression. Overrides `color_by` if present.                             |

---

## 11. Network Plot (`NetworkPlotConfig`)
**Description**: Constructs a gene interaction network with nodes colored by Log Fold Change.

| Variable         | Required | Type                          | Description                                                                                     |
|------------------|----------|-------------------------------|-------------------------------------------------------------------------------------------------|
| `adata_file`     | Yes      | `str`                        | Path to the .h5ad AnnData file.                                                                |
| `plot_type`      | Yes      | `Literal["network", "all"]`  | Specifies the plot type. Must be "network" or "all".                                          |
| `gene_symbols`   | Yes      | `List[dict]`                 | List of dictionaries with 'Gene' and 'Log Fold Change' keys for node coloring. Can be empty.   |
| `cell_type`      | Yes      | `str`                        | Specific cell type for filtering or labeling the network.                                      |
| `covariate_index`| Yes      | `str`                        | Primary grouping index in `adata.obs` (e.g., 'disease').                                       |
| `direction`      | Yes      | `Literal["regulated", "up", "down", "markers"]` | Gene regulation direction. Default is "regulated".                                     |
| `disease`        | No       | `Optional[str]`              | Condition used in the DE comparison for labeling.                                              |
| `n_genes`        | No       | `Optional[int]`              | Number of top genes to include if `gene_symbols` is empty. Defaults to 1000.                   |
| `network_technology` | No   | `Optional[Literal["igraph", "networkx"]]` | Library for network construction. Defaults to "igraph".                               |

---
