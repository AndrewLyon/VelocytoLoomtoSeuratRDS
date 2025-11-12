##Follow all of the steps in this script to work with velocyto files in arm64-MacOS operating systems

##Run in a rosetta (x86_64 based) conda environment!!
#x86_64 conda envrionment installed with:
#CONDA_SUBDIR=osx-64 conda create -n emu
##Then make it permanent with:
#conda activate emu 
#conda config --env --set subdir osx-64
##Add necessary conda package sites for installation 
#conda conda config --add channels bioconda
#conda config --add channels conda-forge
#flexible will allow conda to install packages from different conda channels you have available
#conda config --set channel_priority flexible #strict will use the top channel in your channel list for everything
#Your conda environement will need to have r-base r-seurat r-velocyto.r and r-devtools installed:
#conda install r-seurat r-velocyto.r r-devtools
##open R in your conda environment with:
#R (yes, just capital R)
#This script uses SeuratWrappers and Velocito.R to convert velocyto output loom into seurat rds
#devtools::install_github(https://github.com/satijalab/seurat-wrappers) to install seuratwrappers
##Call the packages in R for use:
library(Seurat)
library(SeuratWrappers)
ducks <- SeuratWrappers::ReadVelocity("location/of/sample.loom", engine = "hdf5r") #load the .loom file, output of velocyto using velocyto.r
seu <- as.Seurat(ducks, default.assay = "spliced", slot = "counts") #convert to a seurat object
saveRDS(seu, file="new/location/for/sample.rds") #save the seurat object as a rds file, import into analysis script
