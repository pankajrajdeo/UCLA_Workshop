# Human Lung Cell Atlas (HLCA) Metadata Document

## Dataset Metadata
- **Dataset Name**: HLCA_full_superadata_v3_norm_log_deg.h5ad  
- **Description**: Supercell bins of 50 cells per bin on the entire h5ad computed at the donor and cell level, reducing 2,282,447 cells to 50,520 metacells. The integrated Human Lung Cell Atlas (HLCA) represents the first large-scale, integrated single-cell reference atlas of the human lung. It consists of over 2 million cells from the respiratory tract of 486 individuals and includes 49 different datasets. It is split into the HLCA core and the extended or full HLCA. The HLCA core includes data of healthy lung tissue from 107 individuals and features manual cell type annotations based on consensus across 6 independent experts, as well as demographic, biological, and technical metadata. The datasets in the HLCA core were integrated using scANVI and can be used as a reference to map new datasets onto using scArches. The full HLCA includes 35 additional datasets that cover donors with various lung diseases. These datasets were mapped onto the core with scArches and include disease annotations as well as cell type annotations transferred from the HLCA core onto the mapped datasets. Note that while the HLCA includes an integrated, batch-corrected low-dimensional embedding, the gene counts themselves were not batch-corrected. Detailed information about all metadata in the objects, as well as further HLCA-related information, can be found on the HLCA landing page: [https://github.com/LungCellAtlas/HLCA](https://github.com/LungCellAtlas/HLCA). Raw counts are available in the downloaded .h undergrad at `adata.raw.X`, in the downloaded .rds at `seurat_object@assays$RNA@counts`, and via CELLxGENE Census.  
- **Species**: Homo sapiens  
- **Research Team**: Human Lung Cell Atlas Initiative  
- **Publication**: [https://www.nature.com/articles/s41591-023-02327-2](https://www.nature.com/articles/s41591-023-02327-2)  
- **Source**: [https://cellxgene.cziscience.com/collections/6f6d381a-7701-4781-935c-db10d30de293](https://cellxgene.cziscience.com/collections/6f6d381a-7701-4781-935c-db10d30de293)  

---

## Indexes and Annotations

### Donor Index
- **Field**: `donor_id`

### Cell Type Index
- **Field**: `ann_finest_level`  
- **Values**:  
  - Monocyte-derived Mph  
  - Alveolar macrophages  
  - NK cells  
  - Alveolar Mph CCL3+  
  - AT2  
  - Lymphatic EC mature  
  - B cells  
  - CD8 T cells  
  - CD4 T cells  
  - DC2  
  - Mast cells  
  - Suprabasal  
  - Smooth muscle  
  - Classical monocytes  
  - EC general capillary  
  - pre-TB secretory  
  - Multiciliated (non-nasal)  
  - AT1  
  - EC venous pulmonary  
  - EC arterial  
  - Adventitial fibroblasts  
  - Alveolar fibroblasts  
  - Hematopoietic stem cells  
  - Unknown  
  - Pericytes  
  - EC aerocyte capillary  
  - Myofibroblasts  
  - Plasma cells  
  - Basal resting  
  - Interstitial Mph perivascular  
  - EC venous systemic  
  - Lymphatic EC differentiating  
  - Smooth muscle FAM83D+  
  - AT2 proliferating  
  - Non-classical monocytes  
  - SM activated stress response  
  - DC1  
  - SMG mucous  
  - Ionocyte  
  - SMG duct  
  - Neuroendocrine  
  - Club (non-nasal)  
  - Goblet (nasal)  
  - Hillock-like  
  - Tuft  
  - Club (nasal)  
  - Goblet (bronchial)  
  - Multiciliated (nasal)  
  - Alveolar Mph proliferating  
  - SMG serous (bronchial)  
  - Subpleural fibroblasts  
  - Lymphatic EC proliferating  
  - Mesothelium  
  - AT0  
  - T cells proliferating  
  - Deuterosomal  
  - Migratory DCs  
  - Plasmacytoid DCs  
  - Peribronchial fibroblasts  
  - Alveolar Mph MT-positive  
  - Goblet (subsegmental)  
  - SMG serous (nasal)  

### Covariate Index
- **Field**: `disease`  
- **Values**:  
  - normal  
  - interstitial lung disease  
  - pneumonia  
  - COVID-19  
  - pulmonary fibrosis  
  - hypersensitivity pneumonitis  
  - pulmonary sarcoidosis  
  - non-specific interstitial pneumonia  
  - cystic fibrosis  
  - chronic obstructive pulmonary disease  
  - squamous cell lung carcinoma  
  - lung adenocarcinoma  
  - lung large cell carcinoma  
  - pleomorphic carcinoma  
  - lymphangioleiomyomatosis  
  - chronic rhinitis  

### Age Index
- **Field**: `development_stage`  
- **Values**:  
  - 22-year-old human stage  
  - 63-year-old human stage  
  - 52-year-old human stage  
  - 45-year-old human stage  
  - 46-year-old human stage  
  - 79-year-old human stage  
  - 50-year-old human stage  
  - 51-year-old human stage  
  - 18-year-old human stage  
  - 26-year-old human stage  
  - 24-year-old human stage  
  - 33-year-old human stage  
  - 2-year-old human stage  
  - 7-year-old human stage  
  - 1-month-old human stage  
  - 14-year-old human stage  
  - 12-month-old human stage  
  - 5-year-old human stage  
  - 3-month-old human stage  
  - 4-year-old human stage  
  - 11-month-old human stage  
  - 16-year-old human stage  
  - 12-year-old human stage  
  - 6-month-old human stage  
  - 9-year-old human stage  
  - 73-year-old human stage  
  - 77-year-old human stage  
  - 60-year-old human stage  
  - 20-year-old human stage  

### Sex Index
- **Field**: `sex`  
- **Values**:  
  - male  
  - female  
  - unknown  

### Study Index
- **Field**: `study`  
- **Values**:  
  - Lafyatis_Rojas_2019  
  - Meyer_2021  
  - Schultze_unpubl  
  - Duong_lungMAP_unpubl  
  - Seibold_2020  
  - Lafyatis_2019  
  - Teichmann_Meyer_2019  
  - Sun_2020  
  - Lambrechts_2021  
  - Schiller_2021  
  - Budinger_2020  
  - Wunderink_2021  
  - Banovich_Kropski_2020  
  - Gomperts_2021  
  - Zhang_2021  
  - Regev_2021  
  - Misharin_Budinger_2018  
  - Janssen_2020  
  - Kaminski_2020  
  - Misharin_2021  
  - Jain_Misharin_2021  
  - Thienpont_2018  
  - Eils_2020  
  - Sims_2019  
  - Krasnow_2020  
  - Nawijn_2021  
  - Xu_2020  
  - Barbry_Leroy_2020  
  - Meyer_Nikolic_2022  
  - Meyer_2019  
  - Peer_Massague_2020  
  - Schiller_2020  
  - Sheppard_2020  
  - Shalek_2018  
  - Tata_unpubl  

### Suspension Index
- **Field**: `suspension_type`  
- **Values**:  
  - cell  
  - nucleus  

### Assay Index
- **Field**: `assay`  
- **Values**:  
  - 10x 3' v1  
  - 10x 3' v2  
  - Seq-Well  
  - 10x 3' v3  
  - 10x 5' v1  
  - 10x 5' transcription profiling  
  - 10x 5' v2  
  - 10x 3' transcription profiling  
  - Drop-seq  

### Tissue Index
- **Field**: `tissue`  
- **Values**:  
  - lung parenchyma  
  - lung  
  - respiratory airway  
  - nose  

### Ethnicity Index
- **Field**: `self_reported_ethnicity`  
- **Values**:  
  - European  
  - Asian  
  - unknown  
  - African  
  - American  
  - admixed ancestry  
  - Pacific Islander  

### Sampling Index
- **Field**: `tissue_sampling_method`  
- **Values**:  
  - donor_lung  
  - surgical_resection  
  - lung_explant  
  - donor_lung_cryopreserved  
  - balf  
  - autopsy  
  - balf_cryopreserved  
  - autopsy_cryopreserved  
  - biopsy_cryopreserved  
  - scraping  
  - biopsy  
  - brush  

---

## Dataset-Specific Fields
- **Disease Stats**: `disease`  
- **Restrict Index**:  
  - study  
  - assay  
  - suspension_type  
  - tissue  
- **Display Index**:  
  - disease  
  - study  
  - assay  
  - suspension_type  

---

## Lineage Levels
- **Level 1**: `ann_level_1`  
- **Level 2**: `ann_level_2`  
- **Level 3**: `ann_level_3`  
- **Level 4**: `ann_finest_level`  

---

## Differential Expression
The following differential expression data is organized by disease and study, with associated cell types:  

1. **Disease**: chronic obstructive pulmonary disease  
   - **Study**: Kaminski_2020  
   - **Cell Types**: Alveolar macrophages, AT1, AT2, B cells, CD4 T cells, CD8 T cells, Classical monocytes, DC2, EC general capillary, Lymphatic EC mature, Mast cells, Multiciliated (non-nasal), NK cells, Non-classical monocytes  

2. **Disease**: chronic rhinitis  
   - **Study**: Shalek_2018  
   - **Cell Types**: Goblet (nasal)  

3. **Disease**: COVID-19  
   - **Study**: Zhang_2021  
   - **Cell Types**: Alveolar macrophages  

4. **Disease**: cystic fibrosis  
   - **Study**: Gomperts_2021  
   - **Cell Types**: Basal resting, Multiciliated (non-nasal), Suprabasal  

5. **Disease**: hypersensitivity pneumonitis  
   - **Study**: Banovich_Kropski_2020  
   - **Cell Types**: Alveolar macrophages, AT2, Monocyte-derived Mph  
   - **Study**: Misharin_Budinger_2018  
   - **Cell Types**: Alveolar macrophages, AT2  

6. **Disease**: interstitial lung disease  
   - **Study**: Banovich_Kropski_2020  
   - **Cell Types**: AT2, Classical monocytes  
   - **Study**: Misharin_Budinger_2018  
   - **Cell Types**: Alveolar macrophages, AT2, Monocyte-derived Mph, Multiciliated (non-nasal)  
   - **Study**: Sheppard_2020  
   - **Cell Types**: Monocyte-derived Mph, Pericytes, Smooth muscle  

7. **Disease**: lung adenocarcinoma  
   - **Study**: Peer_Massague_2020  
   - **Cell Types**: Alveolar macrophages, CD4 T cells, CD8 T cells  

8. **Disease**: non-specific interstitial pneumonia  
   - **Study**: Banovich_Kropski_2020  
   - **Cell Types**: Alveolar macrophages, CD4 T cells  

9. **Disease**: pulmonary fibrosis  
   - **Study**: Banovich_Kropski_2020  
   - **Cell Types**: Adventitial fibroblasts, Alveolar macrophages, AT2, CD4 T cells, CD8 T cells, Classical monocytes, DC2, EC arterial, EC general capillary, Lymphatic EC mature, Monocyte-derived Mph, Multiciliated (non-nasal), Non-classical monocytes, pre-TB secretory  
   - **Study**: Kaminski_2020  
   - **Cell Types**: Adventitial fibroblasts, Alveolar macrophages, Alveolar Mph proliferating, AT1, AT2, B cells, CD4 T cells, CD8 T cells, Classical monocytes, DC2, Lymphatic EC mature, Mast cells, Monocyte-derived Mph, Multiciliated (non-nasal), NK cells, Non-classical monocytes  
   - **Study**: Misharin_Budinger_2018  
   - **Cell Types**: Alveolar macrophages, AT2, Monocyte-derived Mph  
   - **Study**: Schiller_2020  
   - **Cell Types**: AT2, CD8 T cells, Classical monocytes, Mast cells  
   - **Study**: Sheppard_2020  
   - **Cell Types**: Adventitial fibroblasts, Alveolar fibroblasts, Pericytes, Smooth muscle  

10. **Disease**: pulmonary sarcoidosis  
    - **Study**: Banovich_Kropski_2020  
    - **Cell Types**: Alveolar macrophages, AT2  

---

## AnnData Structure
- **Shape**: [50520, 56295] (rows: metacells, columns: genes)  
- **X_dtype**: float32  
- **Observation Fields (`obs`)**:  
  - orig.ident  
  - Metacell  
  - suspension_type  
  - donor_id  
  - assay_ontology_term_id  
  - cell_type_ontology_term_id  
  - development_stage_ontology_term_id  
  - disease_ontology_term_id  
  - self_reported_ethnicity_ontology_term_id  
  - tissue_ontology_term_id  
  - organism_ontology_term_id  
  - sex_ontology_term_id  
  - 3'_or_5'  
  - age_range  
  - ann_finest_level  
  - ann_level_1  
  - ann_level_2  
  - ann_level_3  
  - ann_level_4  
  - ann_level_5  
  - core_or_extension  
  - dataset  
  - fresh_or_frozen  
  - lung_condition  
  - original_ann_level_1  
  - original_ann_level_2  
  - original_ann_level_3  
  - original_ann_level_4  
  - original_ann_level_5  
  - original_ann_nonharmonized  
  - reannotation_type  
  - sample  
  - scanvi_label  
  - sequencing_platform  
  - study  
  - tissue_sampling_method  
  - cell_type  
  - assay  
  - disease  
  - organism  
  - sex  
  - tissue  
  - self_reported_ethnicity  
  - development_stage  
  - ann  
  - ann_sample  
  - size  
  - is_primary_data  
  - datasets  
  - transf_ann_level_1_label  
  - transf_ann_level_2_label  
  - transf_ann_level_3_label  
  - transf_ann_level_4_label  
  - transf_ann_level_5_label  
  - Metacell_ID  
- **Variable Fields (`var`)**: [] (empty)  
- **Observation Embeddings (`obsm`)**:  
  - X_umap  
- **Unstructured Metadata (`uns`)**:  
  - disease_comparison_summary  
  - disease_stats  
  - interaction_data  
  - log1p  
  - marker_stats  
  - rank_genes_groups  
- **Layers (`layers`)**: [] (empty)  
