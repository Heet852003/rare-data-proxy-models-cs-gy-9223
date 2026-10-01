# RareData

Data Engineering (CS-GY 9223), Fall 2026  
Project 6: Proxy Models for Needle-in-a-Haystack Semantic Filters

We are studying how to find rare matching records without calling an LLM on every row. The idea is to label a small sample, train a lightweight classifier on those labels, and use it to filter the remaining data.

Our focus is sampling. When very few rows match a query, a random sample may miss most of the useful examples. We want to see whether adaptive sampling can find more positives with the same labeling budget.

## What we plan to compare

- Random sampling as the baseline.
- Uncertainty sampling, with an initial random sample.
- A cluster-based sampler that adjusts where it samples as it finds positives.

We will start with a logistic regression proxy trained on text embeddings. Each method will use the same label budget and evaluation split. We will compare positive examples found, precision, recall, F1, and time spent on sampling and training. LLM calls and costs will be recorded separately.

The project brief requires at least three datasets with human gold labels. We still need to finalize the selection: one benchmark used by Chung et al., one with naturally rare positives, and one with a more nuanced predicate. Jigsaw Toxic Comments and query-based relevance datasets are candidates.

## Repository layout

| Folder | Contents |
| --- | --- |
| `src/` | Dataset loading, sampling, proxy models, and evaluation code |
| `configs/` | Experiment settings |
| `scripts/` | Commands for running experiments |
| `notebooks/` | Data exploration and plots |
| `experiments/` | Experiment plan and run notes |
| `data/` | Local datasets and cached embeddings |
| `results/` | Metrics and figures |

## Setup

Use Python 3.11 or newer.

```bash
git clone https://github.com/Heet852003/rare-data-proxy-models-cs-gy-9223.git
cd rare-data-proxy-models-cs-gy-9223
python -m venv .venv
source .venv/bin/activate
python -m pip install -r requirements.txt
```

On Windows, activate the environment with `.venv\Scripts\activate`.

The repo currently contains the project structure and initial experiment settings. The experiment runner and LLM integration have not been implemented yet.

## Working together

Create a branch for your changes and open a pull request when they are ready. Keep datasets, API keys, and large model files out of Git. Record the config and random seed with each experiment so we can reproduce the results.
