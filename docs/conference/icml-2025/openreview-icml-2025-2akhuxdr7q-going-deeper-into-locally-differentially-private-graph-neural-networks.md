---
title: Going Deeper into Locally Differentially Private Graph Neural Networks
title_zh: 更深层次的本地差分隐私图神经网络
authors: "Longzhu He, Chaozhuo Li, Peng Tang, Sen Su"
date: 2025-05-01
pdf: "https://openreview.net/pdf?id=2aKHuXdr7Q"
tags: ["query:daily"]
score: 4.0
evidence: 本地差分隐私图神经网络框架，增强图学习中的隐私保护效用
tldr: 图神经网络在处理敏感节点属性时面临隐私泄露风险，现有本地差分隐私方法常导致数据严重失真。本文提出UPGNET框架，采用三阶段流水线推广本地差分隐私协议，在保护用户数据隐私的同时大幅提升私有图学习的效用，特别是在节点分类任务上。该方法对分布式图数据隐私保护具有重要参考价值。
source: ICML-2025-Accepted
selection_source: conference_retrieval
figures_json: "[{\"url\": \"assets/figures/openreview/openreview-icml-2025-2akhuxdr7q/fig-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 824, \"height\": 421, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-icml-2025-2akhuxdr7q/fig-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 1734, \"height\": 358, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-icml-2025-2akhuxdr7q/fig-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 1782, \"height\": 1324, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-icml-2025-2akhuxdr7q/fig-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 853, \"height\": 360, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-icml-2025-2akhuxdr7q/fig-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 853, \"height\": 368, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-icml-2025-2akhuxdr7q/fig-006.webp\", \"caption\": \"\", \"page\": 0, \"index\": 6, \"width\": 1761, \"height\": 372, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-icml-2025-2akhuxdr7q/fig-007.webp\", \"caption\": \"\", \"page\": 0, \"index\": 7, \"width\": 775, \"height\": 379, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-icml-2025-2akhuxdr7q/fig-008.webp\", \"caption\": \"\", \"page\": 0, \"index\": 8, \"width\": 765, \"height\": 389, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-icml-2025-2akhuxdr7q/fig-009.webp\", \"caption\": \"\", \"page\": 0, \"index\": 9, \"width\": 453, \"height\": 333, \"label\": \"Figure\"}]"
tables_json: "[{\"url\": \"assets/tables/openreview/openreview-icml-2025-2akhuxdr7q/table-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 859, \"height\": 238, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-icml-2025-2akhuxdr7q/table-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 869, \"height\": 647, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-icml-2025-2akhuxdr7q/table-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 992, \"height\": 171, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-icml-2025-2akhuxdr7q/table-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 1150, \"height\": 207, \"label\": \"Table\"}]"
motivation: 解决本地差分隐私在图学习中导致数据失真、效用下降的问题。
method: 提出三阶段流水线UPGNET框架，推广本地差分隐私协议。
result: 显著提升节点分类准确性，保护用户隐私。
conclusion: 为隐私保护图学习提供了一种高效用框架。
---

## Abstract
Graph Neural Networks (GNNs) have demonstrated superior performance in a variety of graph mining and learning tasks. However, when node representations involve sensitive personal information or variables related to individuals, learning from graph data can raise significant privacy concerns. Although recent studies have explored local differential privacy (LDP) to address these concerns, they often introduce significant distortions to graph data, severely degrading private learning utility (e.g., node classification accuracy). In this paper, we present UPGNET, an LDP-based privacy-preserving graph learning framework that enhances utility while protecting user data privacy. Specifically, we propose a three-stage pipeline that generalizes the LDP protocols for node features, targeting privacy-sensitive scenarios. Our analysis identifies two key factors that affect the utility of privacy-preserving graph learning: *feature dimension* and *neighborhood size*. Based on the above analysis, UPGNET enhances utility by introducing two core layers: High-Order Aggregator (HOA) layer and the Node Feature Regularization (NFR) layer. Extensive experiments on real-world datasets indicate that UPGNET significantly outperforms existing methods in terms of both privacy protection and learning utility.

---

## 论文详细总结（自动生成）

### 1. 检索相关性
本地差分隐私图神经网络框架，增强图学习中的隐私保护效用。

### 2. 核心内容
图神经网络在处理敏感节点属性时面临隐私泄露风险，现有本地差分隐私方法常导致数据严重失真。本文提出UPGNET框架，采用三阶段流水线推广本地差分隐私协议，在保护用户数据隐私的同时大幅提升私有图学习的效用，特别是在节点分类任务上。该方法对分布式图数据隐私保护具有重要参考价值。

### 3. 对应检索需求
privacy in distributed machine learning。

### 4. 来源与原文
- Source：ICML-2025-Accepted
- OpenReview：[https://openreview.net/forum?id=2aKHuXdr7Q](https://openreview.net/forum?id=2aKHuXdr7Q)
