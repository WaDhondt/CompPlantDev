# Github repository for "A Stroll Through the Developmental Landscape of Plants"

## Folder structure

```bash
.
├── LICENSE
├── README.md
├── data
│   ├── Brady2007
│   ├── Denyer2019
│   │   ├── GSE123818_Root_single_cell_wt_datamatrix.csv.gz
│   │   └── supplementary_tab_1.xlsx
│   ├── PlantPhone
│   │   └── LR_pair_ath.RDa
│   └── Shahan2022
│       ├── Root_bulk_arabidopsis_curated.RD
│       └── endo_exp.RD
├── intermediate_files
│   ├── denyer_wt_lognormalized.h5seurat
│   ├── denyer_wt_sctransform.h5seurat
│   ├── denyer_wt_sctransform_annotated.h5seurat
│   ├── denyer_wt_sctransform_clustered.h5seurat
│   ├── epidermal_tradeseq.rds
│   └── wt_cluster_DEgenes.rds
├── preprocessing
│   ├── 001-PreprocessingLogNormalize.Rmd
│   ├── 002-PreprocessingSctransform.Rmd
│   ├── 003-DimredClustering.Rmd
│   ├── 004-CelltypeAnnotation.Rmd
│   ├── 005-PlotFilteredCells.Rmd
│   └── 006-PloidyTimezone.Rmd
├── project.md
└── trajectory_inference
    ├── 007-EpidermalTrajectory.Rmd
    ├── 008-TrajectoryGO.Rmd
    └── 009-CellCellCommunication.Rmd
```


- `preprocessing/` contains scripts used for preprocessing the raw gene x cell matrix using Seurat
    * In `001-PreprocessingLogNormalize.Rmd` the data was filtered based on QC metrics and log normalized
    * In `002-PreprocessingSctransform.Rmd` the data was not filtered and normalized using the regularized negative binomial regression from `sctransform`
    * In `003-DimredClustering.Rmd` the data from `002-PreprocessingSctransform.Rmd` was clustered and visualized using UMAP, and we identified cluster-specific marker genes
    * In `004-CelltypeAnnotation.Rmd` the clusters were assigned a cell type according to the cluster-specific marker genes and marker genes from Brady 2007 (https://doi.org/10.1126/science.1146265). 
    * In `005-PlotFilteredCells.Rmd` the cells that were filtered in `001-PreprocessingLogNormalize.Rmd` were integrated in the annotated atlas to determine the bias during filtering
    * In `006-PloidyTimezone.Rmd` each cell was assigned a ploidy level and developmental zone annotation by correlating its transcriptome with reference profiles (see https://github.com/ohlerlab/COPILOT)


TODO:

- Reformat code for trajectory inference notebooks
- Add data and intermediate objects as gz
- Finish readme
