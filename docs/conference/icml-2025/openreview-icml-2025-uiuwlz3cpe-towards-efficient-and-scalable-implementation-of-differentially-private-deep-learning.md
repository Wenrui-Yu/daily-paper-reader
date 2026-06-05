---
title: Towards Efficient and Scalable Implementation of Differentially Private Deep Learning
title_zh: 面向高效可扩展的差分隐私深度学习实现
authors: "Sebastian Rodriguez Beltran, Marlon Tobaben, Joonas Jälkö, Niki Andreas Loppi, Antti Honkela"
date: 2025-01-23
pdf: "https://openreview.net/pdf?id=uiuwlZ3cPe"
tags: ["query:daily"]
score: 8.0
evidence: 基准测试带有正确泊松子采样的高效DP-SGD实现
tldr: "差分隐私SGD（DP-SGD）的正确实现需要泊松子采样，但许多实现忽略此要求导致隐私保障不严格。本文系统基准测试了多种高效DP-SGD实现，发现原生Opacus吞吐量比普通SGD低2.6-8倍，而基于JAX的子程序可将差距缩小至10-20%。研究为实用DP深度学习提供了性能参考。"
source: ICML-2025-Rejected-Public
selection_source: conference_retrieval
figures_json: "[{\"url\": \"assets/figures/openreview/openreview-icml-2025-uiuwlz3cpe/fig-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 863, \"height\": 479, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-icml-2025-uiuwlz3cpe/fig-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 1755, \"height\": 392, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-icml-2025-uiuwlz3cpe/fig-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 1756, \"height\": 392, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-icml-2025-uiuwlz3cpe/fig-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 864, \"height\": 378, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-icml-2025-uiuwlz3cpe/fig-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 866, \"height\": 376, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-icml-2025-uiuwlz3cpe/fig-006.webp\", \"caption\": \"\", \"page\": 0, \"index\": 6, \"width\": 1787, \"height\": 460, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-icml-2025-uiuwlz3cpe/fig-007.webp\", \"caption\": \"\", \"page\": 0, \"index\": 7, \"width\": 865, \"height\": 373, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-icml-2025-uiuwlz3cpe/fig-008.webp\", \"caption\": \"\", \"page\": 0, \"index\": 8, \"width\": 900, \"height\": 499, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-icml-2025-uiuwlz3cpe/fig-009.webp\", \"caption\": \"\", \"page\": 0, \"index\": 9, \"width\": 1778, \"height\": 501, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-icml-2025-uiuwlz3cpe/fig-010.webp\", \"caption\": \"\", \"page\": 0, \"index\": 10, \"width\": 900, \"height\": 556, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-icml-2025-uiuwlz3cpe/fig-011.webp\", \"caption\": \"\", \"page\": 0, \"index\": 11, \"width\": 900, \"height\": 556, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-icml-2025-uiuwlz3cpe/fig-012.webp\", \"caption\": \"\", \"page\": 0, \"index\": 12, \"width\": 1794, \"height\": 905, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-icml-2025-uiuwlz3cpe/fig-013.webp\", \"caption\": \"\", \"page\": 0, \"index\": 13, \"width\": 1785, \"height\": 624, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-icml-2025-uiuwlz3cpe/fig-014.webp\", \"caption\": \"\", \"page\": 0, \"index\": 14, \"width\": 901, \"height\": 552, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-icml-2025-uiuwlz3cpe/fig-015.webp\", \"caption\": \"\", \"page\": 0, \"index\": 15, \"width\": 899, \"height\": 556, \"label\": \"Figure\"}]"
tables_json: "[{\"url\": \"assets/tables/openreview/openreview-icml-2025-uiuwlz3cpe/table-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 1778, \"height\": 344, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-icml-2025-uiuwlz3cpe/table-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 731, \"height\": 311, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-icml-2025-uiuwlz3cpe/table-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 868, \"height\": 278, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-icml-2025-uiuwlz3cpe/table-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 806, \"height\": 389, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-icml-2025-uiuwlz3cpe/table-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 1780, \"height\": 357, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-icml-2025-uiuwlz3cpe/table-006.webp\", \"caption\": \"\", \"page\": 0, \"index\": 6, \"width\": 1487, \"height\": 177, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-icml-2025-uiuwlz3cpe/table-007.webp\", \"caption\": \"\", \"page\": 0, \"index\": 7, \"width\": 609, \"height\": 316, \"label\": \"Table\"}]"
motivation: DP-SGD实践中常忽略泊松子采样要求，影响隐私保障与效率。
method: 对比多种DP-SGD实现，包括Opacus和JAX子程序，基准测试其吞吐量。
result: JAX实现接近非隐私训练速度，且严格满足泊松子采样。
conclusion: 高效可扩展的DP-SGD实现需关注采样正确性，JAX方案性能优越。
---

## Abstract
Differentially private stochastic gradient descent (DP-SGD) is the standard algorithm for training machine learning models under differential privacy (DP). The most common DP-SGD privacy accountants rely on Poisson subsampling to ensure the theoretical DP guarantees. Implementing computationally efficient DP-SGD with Poisson subsampling is not trivial, which leads to many implementations that ignore this requirement. We quantify the computational cost of training deep learning models under differential privacy by benchmarking efficient methods with the correct Poisson subsampling requirement. We find that using the naive implementation DP-SGD with Opacus in PyTorch has a throughput between 2.6 and 8 times lower than that of SGD. However, efficient gradient clipping implementations like Ghost Clipping can roughly halve this cost. We propose alternative computationally efficient ways of implementing DP-SGD with JAX that use Poisson subsampling and performs comparably with efficient clipping optimizations based on PyTorch. We highlight important implementation considerations with JAX. Finally, we study the scaling behavior using up to 80 GPUs and find that DP-SGD scales better than SGD.

---

## 论文详细总结（自动生成）

### 1. 检索相关性
基准测试带有正确泊松子采样的高效DP-SGD实现。

### 2. 核心内容
差分隐私SGD（DP-SGD）的正确实现需要泊松子采样，但许多实现忽略此要求导致隐私保障不严格。本文系统基准测试了多种高效DP-SGD实现，发现原生Opacus吞吐量比普通SGD低2.6-8倍，而基于JAX的子程序可将差距缩小至10-20%。研究为实用DP深度学习提供了性能参考。

### 3. 对应检索需求
d。

### 4. 来源与原文
- Source：ICML-2025-Rejected-Public
- OpenReview：[https://openreview.net/forum?id=uiuwlZ3cPe](https://openreview.net/forum?id=uiuwlZ3cPe)
