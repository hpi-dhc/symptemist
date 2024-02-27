# SympTEMIST

## Preparation

1. Clone xMEN repository to obtain dataloaders and benchmark script:

    ```
    git clone https://github.com/hpi-dhc/xmen
    cd xmen
    poetry install
    ```

2. Get latest version of SympTEMIST gazetteer from Zenodo (https://zenodo.org/records/10635215) and put the TSV into `xmen/local_files`

3. Prepare KB and indicies for candidate generation:

   ```
   xmen dict benchmarks/benchmark/symptemist.yaml --code examples/dicts/bsc_gazetteer.py
   xmen dict benchmarks/benchmark/symptemist.yaml --all
   ```


## Notebooks

|Notebook|Description|
|---|---|
|[0_Dataset.ipynb](0_Dataset.ipynb)|Statistics for SympTEMIST shared task and comparable datasets|
|[1_LLM_Simplification.ipynb](1_LLM_Simplification.ipynb)|Applying LLM-based text simplification|
 
## Experiments

Executing `1_LLM_Simplification.ipynb` results in a dataset of candidates based on simplified mentions (`candidates_simplified_cutoff`) in the current folder. It can be used as a candidate set for running the full SympTEMIST entity linking pipeline with a trainable re-ranker.
The BERT checkpoint for initializing the cross-encoder can also be adapted.

`cd xmen/benchmarks`

### Without Simplification

`python run_benchmark.py benchmark=symptemist output=./training`

### With Simplification (Pre-Processed Candidates)

`python run_benchmark.py benchmark=symptemist output=./training +candidates_path=../../symptemist/candidates_simplified_cutoff`

### With Simplification and other BERT checkpoint

(e.g. for `PlanTL-GOB-ES/roberta-base-bne`)

`python run_benchmark.py benchmark=symptemist output=./training +candidates_path=../../symptemist/candidates_simplified_cutoff +linker.reranking.training.model_name=PlanTL-GOB-ES/roberta-base-bne`
