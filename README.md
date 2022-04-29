![header](imgs/header.png)
# STARFALL
[**Getting Started**](#getting-started) | [**Results**](#results)



STARFALL is a natural language inference system on [Discrete Reasoning Over the content of Paragraphs](https://allenai.org/data/drop) (DROP) dataset.

It is also a project for MSRA-USTC Joint PhD Innovation Project 2022.

<a href="https://pytorch.org/get-started/locally/"><img alt="PyTorch" src="https://img.shields.io/badge/PyTorch-ee4c2c?logo=pytorch&logoColor=white"></a>
<a href="https://github.com/allenai/allennlp"><img alt="Config: AllenNLP" src="https://img.shields.io/badge/Config-AllenNLP-89b8cd"></a>



## Getting Started

Install dependencies

```bash
# clone project
git clone https://github.com/BC-Li/STARFALL
cd STARFALL

# [OPTIONAL] create conda environment
conda create -n myenv python=3.7
conda activate myenv

# install pytorch according to instructions
# https://pytorch.org/get-started/

# install requirements
pip install -r requirements.txt
```

Running NAQANet Baseline:

```bash
allennlp train /STARFALL/src/baseline/config/naqanet.jsonnet -s /STARFALL/src/baseline/storage --include-package baseline
```

Train starfall with config from [src/starfall/config](configs/experiment/)

```bash
allennlp train /STARFALL/src/starfall/config/starfall.jsonnet -s /STARFALL/src/starfall/storage --include-package STARFALL
```

## Results

### NAQANet Baseline:

| Train Batch EM | ![train_batch_em (1)](/imgs/train_batch_em (1).svg) |
| -------------- | --------------------------------------------------- |
| Train Batch F1 | ![train_batch_f1](/imgs/train_batch_f1.svg)         |
| Train EM       | ![train_em](/imgs/train_em.svg)                     |
| Train F1       | ![train_f1](/imgs/train_f1.svg)                     |
| Train Loss     | ![train_loss](/imgs/train_loss.svg)                 |
| Validation EM  | ![validation_em](/imgs/validation_em.svg)           |
| Validation F1  | ![validation_f1](/imgs/validation_f1.svg)           |



