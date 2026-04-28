# Evaluating Knowledge Graph Complexity via Semantic, Spectral, and Structural Metrics for Link Prediction

This repository accompanies the paper **“Evaluating Knowledge Graph Complexity via Semantic, Spectral, and Structural Metrics for Link Prediction”**, published in **2025 IEEE International Conference on Big Data (BigData)**.

## Overview

Understanding dataset complexity is fundamental to evaluating and comparing link prediction models on knowledge graphs (KGs). This work studies whether the **Cumulative Spectral Gradient (CSG)** is a reliable complexity metric for multi-relational KG link prediction. We show that CSG is highly sensitive to parameter choices and does not consistently correlate with standard performance metrics such as **MRR** and **Hits@1**. In contrast, semantic metrics such as **Relation Entropy**, **Maximum Relation Diversity**, and **Relation Type Cardinality**, together with structural metrics such as **Average Degree**, **Degree Entropy**, **PageRank**, and **Eigenvector Centrality**, provide more informative signals of dataset difficulty.

## Main Findings

- **CSG is fragile in KG link prediction.** Its value changes noticeably with parameter choices and does not behave as a stable, model-agnostic complexity metric.
- **CSG does not reliably predict downstream performance.** Its correlation with MRR and Hits@1 is weak or inconsistent across datasets and models.
- **Semantic ambiguity is a stronger indicator of difficulty.** Higher Relation Entropy, Maximum Relation Diversity, and Relation Type Cardinality are associated with lower MRR and Hits@1.
- **Structural connectivity helps explain recall-oriented performance.** Metrics such as Average Degree, Degree Entropy, PageRank, and Eigenvector Centrality correlate positively with Hits@10.
- **KG complexity should be measured with multiple complementary signals.** Semantic and structural metrics are more informative and interpretable than relying on CSG alone.

## Paper

The paper is available on IEEE Xplore:

[Evaluating Knowledge Graph Complexity via Semantic, Spectral, and Structural Metrics for Link Prediction](https://ieeexplore.ieee.org/abstract/document/11401467)

## Abstract

Understanding dataset complexity is fundamental to evaluating and comparing link prediction models on knowledge graphs (KGs). While the Cumulative Spectral Gradient (CSG) metric, derived from probabilistic divergence between classes within a spectral clustering framework, has been proposed as a classifier-agnostic complexity metric that scales with class cardinality and correlates with downstream performance, it has not been evaluated in KG settings. In this work, we critically examine CSG in the context of multi-relational link prediction, incorporating semantic representations via transformer-derived embeddings. Contrary to prior claims, we find that CSG is highly sensitive to parameterization and does not robustly scale with the number of classes. Moreover, it exhibits weak or inconsistent correlation with standard performance metrics such as Mean Reciprocal Rank (MRR) and Hits@1. To deepen the analysis, we introduce and benchmark a set of structural and semantic KG complexity metrics. Our findings reveal that global and local relational ambiguity, captured via Relation Entropy, node-level Maximum Relation Diversity, and Relation Type Cardinality, exhibit strong inverse correlations with MRR and Hits@1, suggesting these as more faithful indicators of task difficulty. Conversely, graph connectivity measures such as Average Degree, Degree Entropy, PageRank, and Eigenvector Centrality correlate positively with Hits@10. Our results demonstrate that CSG’s purported stability and generalization-predictive power do not hold in link-prediction settings, and underscore the need for more stable, interpretable, and task-aligned measures of dataset complexity in knowledge-driven learning.



## How to run the code:

### 1. Clone the repository

```bash
git clone https://github.com/YOUR_USERNAME/kg-complexity-metrics.git
cd kg-complexity-metrics
```

### 2. Create a virtual environment

```bash
python -m venv .venv
```

Activate it:

```bash
# Linux/macOS
source .venv/bin/activate

# Windows PowerShell
.venv\Scripts\Activate.ps1
```

### 3. Install dependencies

```bash
pip install --upgrade pip
pip install -r requirements.txt
pip install -e .
```

Optional FAISS acceleration:

```bash
pip install faiss-cpu
```

For GPU FAISS, install the version that matches your CUDA environment.

## Dataset Format

Each dataset should be stored in a folder containing one or more of:

```text
train.txt
valid.txt
test.txt
```

Each line must contain one triple:

```text
head<TAB>relation<TAB>tail
```

Example:

```text
alice	works_at	university
university	located_in	brunei
```

## Quick Start

Run the example dataset:

```bash
kg-complexity summarize --data-dir examples/sample_kg --out results/sample_metrics.csv
```

Compute CSG with deterministic hash embeddings:

```bash
kg-complexity csg \
  --data-dir examples/sample_kg \
  --group-by tail \
  --embedding-method hash \
  --samples-per-class 3 \
  --k-neighbors 3 \
  --out-dir results/sample_csg
```

Train a small TransE model and compute relation-based CSG:

```bash
kg-complexity transe-csg \
  --data-dir examples/sample_kg \
  --group-by relation \
  --epochs 20 \
  --samples-per-class 3 \
  --k-neighbors 3 \
  --out-dir results/sample_transe_csg
```

Run CSG with BERT embeddings:

```bash
kg-complexity csg \
  --data-dir datasets/FB15k-237 \
  --name FB15k-237 \
  --group-by tail \
  --embedding-method bert \
  --model-name bert-base-uncased \
  --samples-per-class 120 \
  --k-neighbors 50 \
  --out-dir results/FB15k-237_csg_bert
```

Run CSG with TransE embeddings:

```bash
kg-complexity transe-csg \
  --data-dir datasets/FB15k-237 \
  --name FB15k-237 \
  --group-by relation \
  --dim 100 \
  --epochs 50 \
  --samples-per-class 120 \
  --k-neighbors 50 \
  --out-dir results/FB15k-237_transe_csg
```

## Main CLI Commands

### `summarize`

Computes semantic and structural metrics.

```bash
kg-complexity summarize --data-dir DATASET_DIR --out results/metrics.csv
```

### `csg`

Computes CSG using concatenated `(head, relation)` text embeddings. Use `--embedding-method hash` for quick deterministic runs or `--embedding-method bert` for transformer-derived semantic embeddings.

```bash
kg-complexity csg --data-dir DATASET_DIR --embedding-method bert
```

### `transe-csg`

Trains TransE embeddings and computes CSG over relation or tail classes.

```bash
kg-complexity transe-csg --data-dir DATASET_DIR --group-by relation
```

## Output Files

The commands write CSV/TXT outputs to `results/`:

```text
results/
├── *_metrics.csv
├── csg_results.csv
├── csg_eigenvalues.txt
├── csg_similarity_matrix.csv
├── transe_csg_results.csv
├── transe_csg_eigenvalues.txt
└── transe_csg_similarity_matrix.csv
```

## Notes on the Recovered Legacy Code

The original scripts in `legacy/` are included exactly as recovered. They contain hard-coded local paths from the original machine and may require editing before direct execution. The portable implementation in `src/kg_complexity/` replaces those hard-coded paths with command-line arguments and adds a dependency-managed package structure suitable for GitHub.



## Repository Structure

```text
kg-complexity-metrics/
├── README.md
├── LICENSE
├── requirements.txt
├── pyproject.toml
├── examples/
│   └── sample_kg/
│       ├── train.txt
│       ├── valid.txt
│       └── test.txt
├── legacy/
│   ├── CSG_R_based.py
│   ├── CSG_diff_M2.py
│   ├── r_CSG_TransE.py
│   ├── spec_analysis_v4.py
│   └── IEEE_BigData__Complexity_Paper_.pdf
├── results/
├── scripts/
│   └── run_all_metrics.py
├── tests/
│   └── test_smoke.py
└── src/
    └── kg_complexity/
        ├── __init__.py
        ├── cli.py
        ├── csg.py
        ├── embeddings.py
        ├── io.py
        ├── metrics.py
        └── transe.py
```



## How to cite:

If you use this repository, please cite:

```bibtex
@INPROCEEDINGS{11401467,
  author={Gul, Haji and Naim, Abdul Ghani and Bhat, Ajaz Ahmad},
  booktitle={2025 IEEE International Conference on Big Data (BigData)},
  title={Evaluating Knowledge Graph Complexity via Semantic, Spectral, and Structural Metrics for Link Prediction},
  year={2025},
  pages={2833-2842},
  keywords={Correlation;Sensitivity;Semantics;Knowledge graphs;Predictive models;Performance metrics;Entropy;Data models;Complexity theory;Standards;Knowledge Graph Complexity; Link Prediction; CSG; Semantic Ambiguity;Structural Connectivity;Dataset Difficulty},
  doi={10.1109/BigData66926.2025.11401467}
}
```


## License
MIT License.
