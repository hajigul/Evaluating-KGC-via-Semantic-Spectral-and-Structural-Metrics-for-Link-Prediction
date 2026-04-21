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

```text
.
├── data/          # datasets or dataset processing files
├── src/           # source code for metric computation and analysis
├── scripts/       # experiment and utility scripts
├── results/       # generated outputs, tables, and statistics
├── figures/       # plots and images used in the paper
├── notebooks/     # exploratory notebooks (if any)
└── README.md




















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
