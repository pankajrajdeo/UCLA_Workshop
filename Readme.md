# UCLA Workshop: Single-Cell RNA-Seq Visualization Toolkit

This repository contains tools and scripts developed for a UCLA workshop focused on generating visualizations from single-cell RNA sequencing (scRNA-seq) data. The primary script, `figure_generation.py`, provides a flexible framework for creating a variety of plots (e.g., UMAP, heatmaps, violin plots, etc.) from AnnData objects using a JSON configuration file.

## Repository Contents

- **[`figure_generation.py`](./figure_generation.py)**: The main Python script for generating visualizations from scRNA-seq data stored in `.h5ad` format.
- **[`requirements.txt`](./requirements.txt)**: A list of Python dependencies required to run the script.
- **[`PLOT_API_DOCUMENTATION.md`](./PLOT_API_DOCUMENTATION.md)**: Detailed API-like documentation for the plotting functions in `figure_generation.py`.

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
- Ensure you have an AnnData object (`.h5ad` file) with precomputed statistics (`marker_stats`, `disease_stats`, `interaction_data` in `adata.uns` if needed).
- Create a JSON configuration file specifying the analysis parameters (see example below).

### 2. Run the Script
```bash
python figure_generation.py <json_input_file> <output_directory>
```
- `<json_input_file>`: Path to your JSON configuration file (e.g., `config.json`).
- `<output_directory>`: Directory to save output files (default: `results`).

#### Example
```bash
python figure_generation.py HLCA_full_superadata_v3_norm_log_deg.json results
```

### JSON Configuration
```json
{
    "adata_file": "path/to/HLCA_full_superadata_v3_norm_log_deg.h5ad",
    "plot_type": "all",
    "cell_type_index": "cell_type",
    "covariate_index": "disease",
    "covariates": ["control", "disease1", "disease2"],
    "gene": "GENE1",
    "gene_symbols": [],
    "cell_type": "T cells",
    "disease": "disease1",
    "direction": "up",
    "n_genes": 100,
    "cell_types_to_compare": ["T cells", "B cells", "Macrophages"],
    "donor_index": "donor",
    "sex_index": "sex",
    "display_variables": ["disease", "assay"],
    "study_index": "study",
    "restrict_studies": ["study1", "study2"],
    "variable2_index": "technology",
    "restrict_variable2": ["10x", "Smart-seq2"],
    "variable3_index": null,
    "restrict_variable3": null,
    "variable4_index": null,
    "restrict_variable4": null,
    "heatmap_technology": "seaborn",
    "network_technology": "igraph",
    "show_individual_cells": true,
    "color_by": "cell_type"
}
```
- `plot_type`: Can be `all`, `umap`, `heatmap`, `violin`, etc.
- See `PLOT_API_DOCUMENTATION.md` for full parameter details.

### Output
- Plots are saved as PDF and PNG files (e.g., `results/UMAP_GENE1_control_disease1.pdf`).
- Tabular data (e.g., DEGs, intersections) are saved as TSV files.

## Documentation
For detailed information on the plotting functions, including required and optional parameters, refer to **[`PLOT_API_DOCUMENTATION.md`](./PLOT_API_DOCUMENTATION.md)**. This file provides API-like documentation for each visualization type in **[`figure_generation.py`](./figure_generation.py)**.

## Requirements
- The script relies on **Python 3.8+** and the libraries listed in `requirements.txt`.
- Key dependencies include:
  - `scanpy` for scRNA-seq data handling
  - `matplotlib` and `seaborn` for plotting
  - `networkx` and `python-igraph` for network visualizations

## Contributing
Contributions are welcome! Please:

1. Fork the repository.
2. Create a feature branch:  
   ```bash
   git checkout -b feature/your-feature
   ```
3. Commit your changes:  
   ```bash
   git commit -m "Add your feature"
   ```
4. Push to the branch:  
   ```bash
   git push origin feature/your-feature
   ```
5. Open a pull request.

## License
This project is licensed under the MIT License. See the `LICENSE` file for details (to be added).

## Contact
For questions or support, please contact **Pankaj Rajdeo** or open an issue in this repository.

_Last updated: March 19, 2025_
