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
    └── 009-LigandReceptor.Rmd
```


- `preprocessing/` contains scripts used for preprocessing the raw gene x cell matrix using Seurat
    * In `001-PreprocessingLogNormalize.Rmd` the data was filtered based on QC metrics and log normalized
    * In `002-PreprocessingSctransform.Rmd` the data was not filtered and normalized using the regularized negative binomial regression from `sctransform`
    * In `003-DimredClustering.Rmd` the data from `002-PreprocessingSctransform.Rmd` was clustered and visualized using UMAP, and we identified cluster-specific marker genes
    * In `004-CelltypeAnnotation.Rmd` the clusters were assigned a cell type according to the cluster-specific marker genes and marker genes from Brady 2007 (https://doi.org/10.1126/science.1146265). 
    * In `005-PlotFilteredCells.Rmd` the cells that were filtered in `001-PreprocessingLogNormalize.Rmd` were integrated in the annotated atlas to determine the bias during filtering
    * In `006-PloidyTimezone.Rmd` each cell was assigned a ploidy level and developmental zone annotation by correlating its transcriptome with reference profiles (see https://github.com/ohlerlab/COPILOT)

- `trajectory_inference/` contains scripts used for trajectory inference on the preprocessed data using Slingshot
    * In `007-EpidermalTrajectory.Rmd` we infer developmental trajectories on the subset of epidermal cell types, and perform trajectory differential expression using tradeSeq. 
    * In `008-TrajectoryGO.Rmd` genes are clustered according to their expression along pseudotime, and we perform GO enrichment analysis on these clusters. 
    * In `009-LigandReceptor.Rmd` we infer ligand-receptor interactions between the different lineages based on co-expression using PlantPhoneDB. 
    
- `data.tar.gz` contains all data used during the analysis and `sessionInfo.txt` contains information on the R package versions. 
