# UCLA Workshop: Single-Cell RNA-Seq Visualization Toolkit

This repository contains tools and scripts developed for a UCLA workshop focused on generating visualizations from single-cell RNA sequencing (scRNA-seq) data. The primary script, `figure_generation.py`, provides a flexible framework for creating a variety of plots (e.g., UMAP, heatmaps, violin plots, etc.) from AnnData objects using a JSON configuration file.

## Repository Contents

- **[`figure_generation.py`](./figure_generation.py)**: The main Python script for generating visualizations from scRNA-seq data stored in `.h5ad` format.
- **[`requirements.txt`](./requirements.txt)**: A list of Python dependencies required to run the script.
- **[`PLOT_API_DOCUMENTATION.md`](./PLOT_API_DOCUMENTATION.md)**: Detailed API-like documentation for the plotting functions in `figure_generation.py`.
- **[`datasets/`](./datasets/)**: Directory to store input `.h5ad` files (e.g., `HLCA_full_superadata_v3_norm_log_deg.h5ad`).
- **[`results/`](./results/)**: Directory where output plots and tabular data are saved.

## Features

- **Supported Plot Types**:
  - UMAP (with gene expression or categorical coloring)
  - Heatmaps (clustered or unclustered, using Seaborn or Matplotlib)
  - Violin plots (gene expression across conditions)
  - Dot plots (gene expression by cell type or covariate)
  - Volcano plots (differentially expressed genes)
  - Cell frequency boxplots (by donor with statistical testing)
  - Venn diagrams (marker gene or DEG overlap)
  - UpSet plots (complex gene set overlaps)
  - Radar plots (aggregated cell frequencies)
  - Network visualizations (using `igraph` or `networkx`)
- **Input**: AnnData objects (`.h5ad`) with precomputed statistics (e.g., `marker_stats`, `disease_stats`).
- **Output**: PDF and PNG files for plots, TSV files for tabular data, saved to a specified output directory.
- **Customization**: Configurable via JSON input for plot types, cell types, covariates, genes, and more.

## Installation

### 1. Clone the Repository
```bash
git clone https://github.com/pankajrajdeo/UCLA_Workshop.git
cd UCLA_Workshop
```

### 2. Set Up a Virtual Environment (optional but recommended)
```bash
python -m venv venv
source venv/bin/activate  # On Windows: venv\Scripts\activate
```

### 3. Install Dependencies
```bash
pip install -r requirements.txt
```

The required dependencies include:
- `numpy`, `pandas`, `scipy` (core data handling)
- `scanpy`, `statsmodels` (scRNA-seq and stats)
- `matplotlib`, `seaborn`, `matplotlib-venn`, `upsetplot` (visualization)
- `networkx`, `python-igraph` (network plotting)

See `requirements.txt` for the full list with version constraints.

## Usage

### 1. Prepare Your Data
- **Download the Dataset**: Obtain the `HLCA_full_superadata_v3_norm_log_deg.h5ad` file from this [Google Drive link](https://drive.google.com/file/d/1fD2uikNSbJhfQAhKESWIoHAXn9pZmI8b/view?usp=sharing).
- **Move the File**: Place the downloaded `HLCA_full_superadata_v3_norm_log_deg.h5ad` file into the `datasets/` directory:
  ```bash
  mv /path/to/downloaded/HLCA_full_superadata_v3_norm_log_deg.h5ad datasets/
  ```
- This `.h5ad` file contains the integrated Human Lung Cell Atlas (HLCA) data with supercell bins (50 cells per bin), reducing 2,282,447 cells to 50,520 metacells, and includes precomputed `marker_stats` and `disease_stats` in `adata.uns`.
- Create a JSON configuration file specifying the analysis parameters (see example below).

### 2. Run the Script
```bash
python figure_generation.py <json_input_file> <output_directory>
```
- `<json_input_file>`: Path to your JSON configuration file (e.g., `config.json`).
- `<output_directory>`: Directory to save output files (default: `results`).

#### Example
To generate a volcano plot for differentially expressed genes in "Alveolar macrophages" under "COVID-19" conditions:
```bash
python figure_generation.py datasets/HLCA_config_volcano.json results
```
For all plot types:
```bash
python figure_generation.py datasets/HLCA_config_all.json results
```

### JSON Configuration
Example configuration tailored to `HLCA_full_superadata_v3_norm_log_deg.h5ad` dataset for a volcano plot comparing "COVID-19" vs. "normal" in "Alveolar macrophages":
```json
{
    "adata_file": "datasets/HLCA_full_superadata_v3_norm_log_deg.h5ad",
    "plot_type": "volcano",
    "cell_type_index": "ann_finest_level",
    "covariate_index": "disease",
    "covariates": ["normal", "COVID-19"],
    "cell_type": "Alveolar macrophages",
    "disease": "COVID-19",
    "direction": "up",
    "n_genes": 100,
    "donor_index": "donor_id"
}
```

Alternatively, to generate all plot types with a broader scope:
```json
{
    "adata_file": "datasets/HLCA_full_superadata_v3_norm_log_deg.h5ad",
    "plot_type": "all",
    "cell_type_index": "ann_finest_level",
    "covariate_index": "disease",
    "covariates": ["normal", "COVID-19", "pulmonary fibrosis"],
    "gene": "ACE2",
    "gene_symbols": [],
    "cell_type": "Alveolar macrophages",
    "disease": "COVID-19",
    "direction": "up",
    "n_genes": 100,
    "donor_index": "donor_id"
}
```
Save these as `datasets/HLCA_config_volcano.json` or `datasets/HLCA_config_all.json`.

## Output
- Plots are saved as PDF and PNG files (e.g., `results/volcano_Alveolar_macrophages_COVID-19.pdf` or `results/UMAP_ACE2_normal_COVID-19.pdf`).
- Tabular data (e.g., DEGs, intersections) are saved as TSV files in the `results/` directory.

## Documentation
For detailed information on the plotting functions, including required and optional parameters, refer to **[`PLOT_API_DOCUMENTATION.md`](./PLOT_API_DOCUMENTATION.md)**. This file provides API-like documentation for each visualization type in **[`figure_generation.py`](./figure_generation.py)**.

## Requirements
- The script relies on **Python 3.8+** and the libraries listed in `requirements.txt`.
- Key dependencies include:
  - `scanpy` for scRNA-seq data handling
  - `matplotlib` and `seaborn` for plotting
  - `networkx` and `python-igraph` for network visualizations

_Last updated: March 19, 2025_
