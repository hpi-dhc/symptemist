# SympTEMIST

## Preparation

1. Clone xMEN repository to obtain dataloaders and benchmark script:

    `git clone https://github.com/hpi-dhc/xmen`

    `cd xmen`

    `poetry install`

2. Get latest version of SympTEMIST gazetteer from Zenodo (https://zenodo.org/records/10635215) and put into `xmen/local_files`

3. Prepare KB and indicies for candidate generation:

    `xmen dict benchmarks/benchmark/symptemist.yaml --code examples/dicts/bsc_gazetteer.py`

    `xmen dict benchmarks/benchmark/symptemist.yaml --all`


## Notebooks:

|Notebook|Description|
|---|---|
|[0_Dataset.ipynb](0_Dataset.ipynb)|Statistics for SympTEMIST shared task and comparable datasets|
|[1_LLM_Simplification.ipynb](1_LLM_Simplification.ipynb)|Applying LLM-based text simplification|
 
## Experiments

`cd xmen/benchmarks`

`python run_benchmark.py benchmark=symptemist output=~/scratch/xmen`
