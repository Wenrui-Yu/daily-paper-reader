---
title: "Generalization in Federated Learning: A Conditional Mutual Information Framework"
title_zh: "联邦学习中的泛化性: 条件互信息框架"
authors: "Ziqiao Wang, Cheng Long, Yongyi Mao"
date: 2025-05-01
pdf: "https://openreview.net/pdf?id=kOttDCDYJp"
tags: ["query:daily"]
score: 9.0
evidence: 分析联邦学习中的泛化性，联邦学习是一种隐私保护分布式机器学习框架
tldr: 针对联邦学习泛化性分析不足的问题，本文引入条件互信息框架，构建超客户端概念来量化参与方内部和参与方间的泛化误差，得到更紧致的泛化界。在典型联邦学习任务上的实验验证了理论的有效性。该成果为理解和改进分布式隐私保护学习的泛化性能提供了新工具。
source: ICML-2025-Accepted
selection_source: conference_retrieval
figures_json: "[{\"url\": \"assets/figures/openreview/openreview-icml-2025-kottdcdyjp/fig-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 856, \"height\": 710, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-icml-2025-kottdcdyjp/fig-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 1242, \"height\": 1337, \"label\": \"Figure\"}]"
tables_json: "[{\"url\": \"assets/tables/openreview/openreview-icml-2025-kottdcdyjp/table-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 1532, \"height\": 1426, \"label\": \"Table\"}]"
motivation: 联邦学习作为隐私保护分布式学习，其泛化性缺乏理论分析，尤其是参与方与非参与方间的泛化差异。
method: 引入条件互信息 (CMI) 框架，构建“超客户端”概念，同时量化参与方内部和参与方间的泛化误差上界。
result: 在多个联邦学习任务上验证了所提框架的有效性，所得泛化界比传统方法更紧致，且适用于异构数据场景。
conclusion: 该工作为联邦学习泛化性提供了新的理论工具，揭示了条件互信息分析的重要性，对隐私保护分布式学习有指导意义。
---

## Abstract
Federated learning (FL) is a widely adopted privacy-preserving distributed learning framework, yet its generalization performance remains less explored compared to centralized learning. In FL, the generalization error consists of two components: the out-of-sample gap, which measures the gap between the empirical and true risk for participating clients, and the participation gap, which quantifies the risk difference between participating and non-participating clients. In this work, we apply an information-theoretic analysis via the conditional mutual information (CMI) framework to study FL's two-level generalization. Beyond the traditional supersample-based CMI framework, we introduce a superclient construction to accommodate the two-level generalization setting in FL. We derive multiple CMI-based bounds, including hypothesis-based CMI bounds, illustrating how privacy constraints in FL can imply generalization guarantees. Furthermore, we propose fast-rate evaluated CMI bounds that recover the best-known convergence rate for two-level FL generalization in the small empirical risk regime. For specific FL model aggregation strategies and structured loss functions, we refine our bounds to achieve improved convergence rates with respect to the number of participating clients. Empirical evaluations confirm that our evaluated CMI bounds are non-vacuous and accurately capture the generalization behavior of FL algorithms.

---

## 论文详细总结（自动生成）

### 1. 检索相关性
分析联邦学习中的泛化性，联邦学习是一种隐私保护分布式机器学习框架。

### 2. 核心内容
针对联邦学习泛化性分析不足的问题，本文引入条件互信息框架，构建超客户端概念来量化参与方内部和参与方间的泛化误差，得到更紧致的泛化界。在典型联邦学习任务上的实验验证了理论的有效性。该成果为理解和改进分布式隐私保护学习的泛化性能提供了新工具。

### 3. 对应检索需求
privacy in distributed machine learning。

### 4. 来源与原文
- Source：ICML-2025-Accepted
- OpenReview：[https://openreview.net/forum?id=kOttDCDYJp](https://openreview.net/forum?id=kOttDCDYJp)
