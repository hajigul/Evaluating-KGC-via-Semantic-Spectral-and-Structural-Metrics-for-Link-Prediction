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

## What This Repository Contains

This repository contains materials related to the paper, including:

- implementations of **spectral**, **semantic**, and **structural** KG complexity metrics
- analysis of **relation-based CSG (r-CSG)** and **tail-based CSG (t-CSG)**
- benchmark-level complexity profiling for standard KG datasets
- correlation analysis between complexity metrics and link prediction performance
- figures, tables, and experiment outputs supporting the paper

## Complexity Metrics Studied

### Spectral Metrics
- Relation-based Cumulative Spectral Gradient (**r-CSG**)
- Tail-based Cumulative Spectral Gradient (**t-CSG**)
- Spectral Gap
- Algebraic Connectivity

### Semantic Metrics
- Relation Entropy
- Relation Type Cardinality
- Maximum Relation Diversity

### Structural Metrics
- Average Degree
- Degree Entropy
- Degree Centrality
- Betweenness Centrality
- Closeness Centrality
- Eigenvector Centrality
- PageRank
- Clustering Coefficients
- Modularity
- Structural Entropy
- Other graph-theoretic properties used in the paper

## Datasets

The study evaluates standard knowledge graph benchmarks, including:

- **FB15k-237**
- **WN18RR**
- **CoDEx-S**
- **CoDEx-M**
- **CoDEx-L**
- **WN18**
- **YAGO3-10**

These datasets are used to examine how different complexity measures relate to downstream link prediction performance.

## Methodology Summary

The overall workflow of the paper is:

1. Represent knowledge graph triples as structured inputs for spectral, semantic, and structural analysis.
2. Compute **relation-based** and **tail-based** CSG using transformer-derived semantic embeddings.
3. Extract semantic complexity measures such as relation entropy and relation diversity.
4. Extract structural graph measures such as degree statistics and centrality measures.
5. Compare all complexity measures against link prediction performance metrics such as **MRR**, **Hits@1**, and **Hits@10**.
6. Identify which metrics best reflect the intrinsic difficulty of a KG dataset.

## Repository Structure

A typical repository layout is as follows:




## Reproducibility  
This repository is intended to support reproduction of the main findings reported in the paper, including:

- sensitivity analysis of CSG with respect to the k parameter
- analysis of CSG under different class sampling sizes
- correlation analysis between complexity metrics and downstream link prediction performance
- complexity comparisons across widely used benchmark datasets
  
## Why This Work Matters  
Knowledge graph benchmark performance varies widely across datasets, but standard evaluation metrics alone do not explain why one dataset is harder than another. This work provides a more principled view of dataset difficulty by comparing spectral, semantic, and structural complexity measures. The results suggest that semantic ambiguity and structural connectivity are more reliable indicators of KG difficulty than CSG alone.






## Benchmark Results

We report link prediction performance in terms of **MRR**, **Hits@1**, and **Hits@10** across multiple standard knowledge graph datasets.

<details>
<summary>Show benchmark performance table</summary>

| Model | WN18 MRR | WN18 H@1 | WN18 H@10 | FB15k-237 MRR | FB15k-237 H@1 | FB15k-237 H@10 | WN18RR MRR | WN18RR H@1 | WN18RR H@10 | YAGO3-10 MRR | YAGO3-10 H@1 | YAGO3-10 H@10 | CoDEx-M MRR | CoDEx-M H@1 | CoDEx-M H@10 |
|---|---:|---:|---:|---:|---:|---:|---:|---:|---:|---:|---:|---:|---:|---:|---:|
| DistMult | 0.824 | 0.726 | 0.9461 | 0.313 | 0.224 | 0.4901 | 0.433 | 0.397 | 0.5022 | 0.501 | 0.413 | 0.6612 | 0.379 | 0.328 | 0.479 |
| ComplEx | 0.949 | 0.945 | 0.9550 | 0.349 | 0.257 | 0.5297 | 0.458 | 0.426 | 0.5212 | 0.576 | 0.505 | 0.7035 | 0.373 | 0.331 | 0.453 |
| ANALOGY | 0.934 | 0.926 | 0.9442 | 0.202 | 0.126 | 0.3538 | 0.366 | 0.358 | 0.3800 | 0.283 | 0.192 | 0.4565 | 0.314 | 0.246 | 0.441 |
| SimplE | 0.938 | 0.933 | 0.9458 | 0.179 | 0.100 | 0.3435 | 0.398 | 0.383 | 0.4265 | 0.453 | 0.356 | 0.6316 | 0.255 | 0.189 | 0.376 |
| HolE | 0.938 | 0.931 | 0.9494 | 0.303 | 0.214 | 0.4764 | 0.432 | 0.403 | 0.4879 | 0.502 | 0.418 | 0.6519 | -- | -- | -- |
| TuckER | 0.951 | 0.946 | 0.9580 | 0.352 | 0.259 | 0.5361 | 0.459 | 0.430 | 0.5140 | 0.544 | 0.466 | 0.6809 | 0.328 | 0.259 | 0.458 |
| TransE | 0.646 | 0.406 | 0.9487 | 0.310 | 0.217 | 0.4965 | 0.206 | 0.028 | 0.5623 | 0.401 | 0.378 | 0.5739 | 0.435 | 0.368 | 0.562 |
| STransE | 0.656 | 0.432 | 0.9345 | 0.315 | 0.225 | 0.4956 | 0.326 | 0.101 | 0.4221 | 0.049 | 0.328 | 0.0735 | -- | -- | -- |
| CrossE | 0.834 | 0.733 | 0.9503 | 0.298 | 0.212 | 0.4705 | 0.405 | 0.381 | 0.4499 | 0.446 | 0.331 | 0.6545 | -- | -- | -- |
| TorusE | 0.947 | 0.743 | 0.9544 | 0.281 | 0.196 | 0.4471 | 0.463 | 0.427 | 0.5335 | 0.342 | 0.274 | 0.4744 | -- | -- | -- |
| RotatE | 0.949 | 0.943 | 0.9602 | 0.336 | 0.238 | 0.5306 | 0.475 | 0.426 | 0.5735 | 0.498 | 0.405 | 0.6707 | 0.478 | 0.418 | 0.593 |
| ConvE | 0.945 | 0.939 | 0.9568 | 0.305 | 0.214 | 0.4762 | 0.427 | 0.390 | 0.5075 | 0.488 | 0.399 | 0.6575 | 0.318 | 0.239 | 0.464 |
| ConvKB | 0.709 | 0.529 | 0.9489 | 0.230 | 0.140 | 0.4146 | 0.398 | 0.585 | 0.6525 | 0.420 | 0.322 | 0.6047 | -- | -- | -- |
| ConvR | 0.950 | 0.946 | 0.9585 | 0.346 | 0.256 | 0.5263 | 0.4998 | 0.468 | 0.5987 | 0.4232 | 0.412 | 0.5766 | -- | -- | -- |
| RSN | 0.928 | 0.912 | 0.9510 | 0.280 | 0.198 | 0.4444 | 0.498 | 0.399 | 0.5834 | 0.441 | 0.409 | 0.6043 | -- | -- | -- |

</details>



## Feature Correlation Matrix

The full correlation matrix across semantic, structural, and spectral graph features is provided as a figure for readability.

![Correlation Matrix](figures/correlation_matrix.png)

For the complete numeric version, see the files in the `results/` directory.










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
