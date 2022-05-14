# NABERT-Large+
![model_3](/imgs/model_3.png)



[**Getting Started**](#getting-started) | [**Results**](#results)

This repository provides:
* Reproduction guides and Training results of:
    * NAQANet
    * NABERT
    * NABERT+
* We also retrained NABERT+ with BERT-Large, which gained **8.2% EM** and **7.4% F1** improvement on dev datasets of [Discrete Reasoning Over the content of Paragraphs](https://allenai.org/data/drop) (DROP).
* A detailed report

The codes and training configs are based on [@raylin1000](https://github.com/raylin1000)(NABERT Model) and [AI2](https://github.com/allenai/allennlp-models/blob/main/allennlp_models/rc/models/naqanet.py).

<a href="https://pytorch.org/get-started/locally/"><img alt="PyTorch" src="https://img.shields.io/badge/PyTorch-ee4c2c?logo=pytorch&logoColor=white"></a>
<a href="https://github.com/allenai/allennlp"><img alt="Config: AllenNLP" src="https://img.shields.io/badge/Config-AllenNLP-89b8cd"></a>

## Getting Started

### Install dependencies

```bash
# clone project
git clone https://github.com/BC-Li/nabert-large
cd nabert-large

# [OPTIONAL] create conda environment
conda create -n myenv python=3.7
conda activate myenv

# install pytorch according to instructions
# https://pytorch.org/get-started/

# install requirements
pip install -r requirements.txt
```

### Running NAQANet Baseline

> This will require a GRAM for ~8GB and about 20 hours on RTX3090 to make the model reach convergence.

```bash
allennlp train /nabert-large/src/baseline/config/naqanet.jsonnet -s /nabert-large/src/baseline/storage --include-package baseline
```

### Running NABERT or NABERT+ Baseline.

```bash
allennlp train /nabert/src/nabert/config/nabert.json -s /nabert/src/nabert/storage --include-package nabert
```

### Train NABERT-Large+ 

Use config from [src/nabert-large/config](configs/experiment/). 

> Please ensure you have a GPU which have >22GB GRAM. I trained it on a single RTX3090 for about 20 hours with early stopping to avoid overfitting.

```bash
allennlp train /nabert/src/nabert/config/nabert-large.json -s /nabert-large/src/nabert-large/storage --include-package nabert-large
```

### TensorBoard Support

AllenNLP also supports TensorBoard. To open it, just change the `--logdir` parameter to run following command.

```bash
tensorboard --logdir="/nabert-large/src/nabert-large/storage"
```

## Results

| Model                                      | EM        | F1        |
| ------------------------------------------ | --------- | --------- |
| NAQANet                                    | 46.20     | 49.24     |
| NABERT                                     | 54.67     | 57.64     |
| NABERT+                                    | 62.67     | 66.29     |
| NumNet                                     | 64.92     | 68.31     |
| NABERT-Large+ (dropout=0.11)               | **67.82** | **71.25** |
| OPERA (Current Rank 1 on DROP Leaderboard) | 86.79     | 89.41     |
| Human                                      | 94.90     | 96.42     |

## Training Result

### NABERT-Large+
| Train Batch EM                                               | Train Batch F1                                               | Validation/Train EM                                                | Validation/Train F1                                                |
| ------------------------------------------------------------ | ------------------------------------------------------------ | ------------------------------------------------------------ | ------------------------------------------------------------ |
| ![epoch_metrics_em](/imgs/nabert-large/epoch_metrics_em.svg) | ![epoch_metrics_f1](/imgs/nabert-large/epoch_metrics_f1.svg) | ![em](/imgs/nabert-large/em.svg) | ![f1](/imgs/nabert-large/f1.svg) |


### NAQANet Baseline

| Train Batch EM                                      | Train Batch F1                              | Train EM                        | Train F1                        |
| --------------------------------------------------- | ------------------------------------------- | ------------------------------- | ------------------------------- |
| ![train_batch_em (1)](/imgs/naqanet/train_batch_em.svg) | ![train_batch_f1](/imgs/naqanet/train_batch_f1.svg) | ![train_em](/imgs/naqanet/train_em.svg) | ![train_f1](/imgs/naqanet/train_f1.svg) |

| Train Loss                          | Validation EM                             | Validation F1                             |
| ----------------------------------- | ----------------------------------------- | ----------------------------------------- |
| ![train_loss](/imgs/naqanet/train_loss.svg) | ![validation_em](/imgs/naqanet/validation_em.svg) | ![validation_f1](/imgs/naqanet/validation_f1.svg) |

### NABERT

| Train Batch EM                                         | Train Batch F1                                         | Validation/Train EM              | Validation/Train F1              |
| ------------------------------------------------------ | ------------------------------------------------------ | -------------------------- | -------------------------- |
| ![epoch_metrics_em](/imgs/nabert/epoch_metrics_em.svg) | ![epoch_metrics_f1](/imgs/nabert/epoch_metrics_f1.svg) | ![em](/imgs/nabert/em.svg) | ![f1](/imgs/nabert/f1.svg) |


### NABERT+

| Train Batch EM                                               | Train Batch F1                                               | Validation/Train EM                                                | Validation/Train F1                                                |
| ------------------------------------------------------------ | ------------------------------------------------------------ | ------------------------------------------------------------ | ------------------------------------------------------------ |
| ![epoch_metrics_em](/imgs/nabert+/epoch_metrics_em.svg) | ![epoch_metrics_f1](/imgs/nabert+/epoch_metrics_f1.svg) | ![em](/imgs/nabert+/em.svg) | ![f1](/imgs/nabert+/f1.svg) |

