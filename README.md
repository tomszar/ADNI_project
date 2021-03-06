[![DOI](https://zenodo.org/badge/DOI/10.5281/zenodo.6049171.svg)](https://doi.org/10.5281/zenodo.6049171)

# ADNI sex differences analysis

This is the repository of the *[Sex Differences in the Metabolome of Alzheimer's Disease Progression](https://www.frontiersin.org/articles/10.3389/fradi.2022.782864/full)* article.

Authors: Tomás González Zarzar, Brian Lee, Rory Coughlin, Dokyoon Kim, Li Shen and Molly A. Hall.

The purpose is to detect sex differences in metabolite-phenotype associations.

## Clone repository

To clone the respository, on your terminal type:

```bash
git clone https://github.com/tomszar/ADNI_project.git
```

Then, enter the respository and follow the next instructions

```bash
cd ADNI_project
```

## Environment setup

The repository provides an `environment.yml` file to use with conda

First, install [anaconda](https://www.anaconda.com/products/individual) on your local computer or user server account following the appropriate directions, using the corresponding installer to your operative system.
Next, on the terminal, in the root of this repository, install the conda environment by running:

```bash
conda env create -f environment.yml
```

If, for any reason, the installation through the environment file fails, you can install the environment manually, by running the following:

```bash
conda config --add channels r
conda config --add channels bioconda
conda config --add channels conda-forge
conda create --name adni_project python=3.9 pandas numpy scipy jupyterlab statsmodels scikit-learn pingouin r-base r-wgcna r-dplyr
conda activate adni_project
pip install clarite
```

## Replicate the analysis

Depending on whether you are replicating the analysis on your local machine or sending the job to a cluster, you can run either `run_local.sh` or `run_cluster.sh`

### On cluster

On your server terminal, run the following command:

```bash
qsub run_cluster.sh
```

The parameters used in the script are the ones used in the Penn State Roar server.
Depending on the system you will need to modify, remove, or add parameters to the script.
The script also contains the copying of the needed ADNI data sets into the `data` folder; you can either modify the paths of the data sets in the `ADNI_data_files.txt` file to match yours, or manually copy the files, and comment the lines in the `run_cluster.sh` script.
In the next section there is a brief description on the ADNI data sets needed.

### On local machine

Before running the pipeline, you will need to create the `data` folder and drop the files needed from ADNI.
On the terminal, type

```bash
mkdir data/
```

Copy the following files from ADNI in the `data` folder

- p180 data files: `ADMCDUKEP180UPLC_01_15_16.csv`, `ADMCDUKEP180FIA_01_15_16.csv`, `ADMCDUKEP180UPLCADNI2GO.csv`, `ADMCDUKEP180FIAADNI2GO.csv`, `ADMCDUKEP180FIAADNI2GO_DICT.csv`, `ADMCDUKEP180UPLCADNI2GO_DICT.csv`, `4610 FIA p180 Data.xlsx`, `4610 UPLC p180 Data.xlsx`.
- nmr nightingale files: `ADNINIGHTINGALE2.csv`, `ADNINIGHTINGALE2_DICT.csv`.
- fasting information: `BIOMARK.csv`.
- LOD values: `P180FIALODvalues_ADNI1.csv`, `P180FIALODvalues_ADNI2GO.csv`, `P180UPLCLODvalues_ADNI1.csv`, `P180UPLCLODvalues_ADNI2GO.csv`.
- QT-pad: `ADNI_adnimerge_20170629_QT-freeze.csv`.
- Drug classes: `ADMCPATIENTDRUGCLASSES_20170512.csv`

Next, on the terminal, type:

```bash
conda activate adni_project
bash run_local.sh > run_local.log
```
