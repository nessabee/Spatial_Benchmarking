# Spatial_Benchmarking
## Benchmarking Report by Vanessa Brien for SpaTalk (ZJUFanLab): 
GitHub link: https://github.com/ZJUFanLab/SpaTalk?tab=readme-ov-file
### 1. How to install it:
```r
# Run these lines
install.packages(pkgs = 'devtools')
devtools::install_github('linxihui/NNLM')
devtools::install_github('ZJUFanLab/SpaTalk')

### 2. Creating the SpaTalk object:
You need:
st_data: A data.frame or matrix or dgCMatrix containing counts of spatial transcriptomics, each column representing a spot or a cell, each row representing a gene.
st_meta: A data.frame containing coordinate of spatial transcriptomics with three columns, namely 'spot', 'x', 'y' for spot-based spatial transcriptomics data or 'cell', 'x', 'y' for single-cell spatial transcriptomics data.
species: A character meaning species of the spatial transcriptomics data.'Human' or 'Mouse'.
if_st_is_sc: For spot-based, set to FALSE. For single-cell, set to TRUE.
spot_max_cell: A integer meaning max cell number for each plot to predict. If if_st_sc is FALSE, please determine the spot_max_cell. For 10X (55um), we recommend 30. For Slide-seq, we recommend 1.
celltype: A character containing the cell type of ST data. To skip the deconvolution step and directly infer cell-cell communication, please define the cell type. Default is NULL.  
