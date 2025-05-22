# Spatial_Benchmarking
## Benchmarking Report by Vanessa Brien for SpaTalk (ZJUFanLab): 
GitHub link: https://github.com/ZJUFanLab/SpaTalk?tab=readme-ov-file

### Special note:
These intructions are skipping the deconvolution step from single-cell reference data (and assuming you have cell type labels already) and directly infering cell-cell communication.

### 1. How to install it:
```r
install.packages(pkgs = 'devtools')
devtools::install_github('linxihui/NNLM')
devtools::install_github('ZJUFanLab/SpaTalk')
```

### 2. Creating the SpaTalk object:
#### You need:
* **st_data**: A data.frame or matrix or dgCMatrix containing counts of spatial transcriptomics, each column representing a spot or a cell, each row representing a gene.
* **st_meta**: A data.frame containing coordinate of spatial transcriptomics with three columns, namely 'spot', 'x', 'y' for spot-based spatial transcriptomics data or 'cell', 'x', 'y' for single-cell spatial transcriptomics data.
* **species**: A character meaning species of the spatial transcriptomics data, in this case 'Human' or 'Mouse'.
* **if_st_is_sc**: For spot-based, set to FALSE. For single-cell, set to TRUE.
* **spot_max_cell**: An integer meaning max cell number for each plot to predict. If if_st_sc is FALSE, determine the spot_max_cell. From the R documentation, they recommend 30 for 10X (55um), and 1 for Slide-seq.
* **celltype**: A character containing the cell type of ST data. To skip the deconvolution step and directly infer cell-cell communication, please define the cell type. Default is NULL.

Here is an example on how to run it with spot-based ST data:
```r
obj <- createSpaTalk(
  st_data = st_data,
  st_meta = st_meta,
  species = "Human",
  if_st_is_sc = FALSE,
  spot_max_cell = 1,
  celltype = st_celltype)
```
### 3. Finding the ligand-receptor pairs and pathways
#### You need:
* **object**: Generated in step 2
* **lrpairs**: A data.frame of the system data containing ligand-receptor pairs of 'Human' and 'Mouse' from CellTalkDB. There is no need to load in anything, it is already included in the function!
* **pathways**: A data.frame of the system data containing gene-gene interactions and pathways from KEGG and Reactome as well as the information of transcriptional factors. There is no need to load in anything, it is already included in the function!
* **max_hop**: Max hop from the receptor to the downstream target transcriptional factor to find for receiving cells. Default is 3 for human and 4 for mouse.
* **if_doParallel**: For parallel computation to speed up analysis, default is TRUE.
* **use_n_cores**: Number of CPU cores to use. Default is all cores - 2.

Here is an example on how to run it:
```r
obj <- find_lr_path(object = obj, lrpairs = lrpairs, pathways = pathways)
```
### 4. Infering 
