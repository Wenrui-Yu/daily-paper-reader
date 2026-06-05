---
title: Scalable Private Partition Selection via Adaptive Weighting
title_zh: 可扩展的私有分区选择：自适应加权方法
authors: "Justin Y. Chen, Vincent Cohen-Addad, Alessandro Epasto, Morteza Zadimoghaddam"
date: 2025-05-01
pdf: "https://openreview.net/pdf?id=NEfIaE4BI5"
tags: ["query:daily"]
score: 7.0
evidence: 提出一种自适应加权的私有分区选择算法，作为隐私保护机器学习的核心构建模块
tldr: 在差分隐私分区选择问题中，现有方法难以同时兼顾高发现率与强隐私保护。本文提出MaxAdaptiveDegree (MAD)算法，通过自适应权重转移，将超出隐私阈值的项目权重重定向至低频项目，从而提高低频项的选取概率。该方法作为隐私保护机器学习（如私有语料库词汇提取）的核心构建模块，显著提升了数据利用率，为分布式隐私数据分析提供了基础工具。
source: ICML-2025-Accepted
selection_source: conference_retrieval
figures_json: "[{\"url\": \"assets/figures/openreview/openreview-icml-2025-nefiae4bi5/fig-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 761, \"height\": 884, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-icml-2025-nefiae4bi5/fig-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 1373, \"height\": 801, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-icml-2025-nefiae4bi5/fig-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 1370, \"height\": 794, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-icml-2025-nefiae4bi5/fig-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 1376, \"height\": 806, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-icml-2025-nefiae4bi5/fig-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 1374, \"height\": 810, \"label\": \"Figure\"}]"
tables_json: "[{\"url\": \"assets/tables/openreview/openreview-icml-2025-nefiae4bi5/table-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 776, \"height\": 418, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-icml-2025-nefiae4bi5/table-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 1618, \"height\": 433, \"label\": \"Table\"}]"
motivation: 提升差分隐私分区选择中低频项的发现率，支撑隐私保护ML应用。
method: 提出MAD算法，通过自适应权重转移实现高效私有分区选择。
result: 提高了低频项目的选取概率，增强了数据隐私保护下的利用率。
conclusion: 为隐私保护机器学习提供了实用的基础算法组件。
---

## Abstract
In the differentially private partition selection problem (a.k.a. set union, key discovery), users hold subsets of items from an unbounded universe. The goal is to output as many items as possible from the union of the users' sets while maintaining user-level differential privacy. Solutions to this problem are a core building block for many privacy-preserving ML applications including vocabulary extraction in a private corpus, computing statistics over categorical data and learning embeddings over user-provided items. We propose an algorithm for this problem, MaxAdaptiveDegree (MAD), which adaptively reroutes weight from items with weight far above the threshold needed for privacy to items with smaller weight, thereby increasing the probability that less frequent items are output.  Our algorithm can be efficiently implemented in massively parallel computation systems allowing scalability to very large datasets. We prove that our algorithm stochastically dominates the standard parallel algorithm for this problem. We also develop a two-round version of our algorithm, MAD2R, where results of the computation in the first round are used to bias the weighting in the second round to maximize the number of items output. In experiments, our algorithms provide the best results among parallel algorithms and scale to datasets with hundreds of billions of items, up to three orders of magnitude larger than those analyzed in prior works.

---

## 论文详细总结（自动生成）

### 1. 检索相关性
提出一种自适应加权的私有分区选择算法，作为隐私保护机器学习的核心构建模块。

### 2. 核心内容
在差分隐私分区选择问题中，现有方法难以同时兼顾高发现率与强隐私保护。本文提出MaxAdaptiveDegree (MAD)算法，通过自适应权重转移，将超出隐私阈值的项目权重重定向至低频项目，从而提高低频项的选取概率。该方法作为隐私保护机器学习（如私有语料库词汇提取）的核心构建模块，显著提升了数据利用率，为分布式隐私数据分析提供了基础工具。

### 3. 对应检索需求
Papers central to -, especially work that connects or combines: S; t; c; m; d; p; privacy in distributed optimization; privacy in distributed machine learning.

### 4. 来源与原文
- Source：ICML-2025-Accepted
- OpenReview：[https://openreview.net/forum?id=NEfIaE4BI5](https://openreview.net/forum?id=NEfIaE4BI5)
