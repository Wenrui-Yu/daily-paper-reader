---
title: Revisiting Differentially Private Algorithms for Decentralized Online Learning
title_zh: 重访去中心化在线学习中的差分隐私算法
authors: "Xiaoyu Wang, Wenhao Yang, Chang Yao, Mingli Song, Yuanyu Wan"
date: 2025-05-01
pdf: "https://openreview.net/pdf?id=12oD7HIckz"
tags: ["query:daily"]
score: 9.0
evidence: "去中心化在线学习算法实现(ε,0)-DP，获得接近最优遗憾界"
tldr: "现有去中心化在线学习的差分隐私算法无法同时实现T轮(ε,0)-DP、最优遗憾和轻量计算。本文提出一种新算法，在获得严格差分隐私保障的同时，对于凸函数与强凸函数分别达到了近优的遗憾界，且无需复杂约束下的高计算成本。该工作为隐私保护分布式优化开辟了可扩展的路线。"
source: ICML-2025-Accepted
selection_source: conference_retrieval
figures_json: "[{\"url\": \"assets/figures/openreview/openreview-icml-2025-12od7hickz/fig-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 1630, \"height\": 613, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-icml-2025-12od7hickz/fig-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 1600, \"height\": 653, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-icml-2025-12od7hickz/fig-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 1630, \"height\": 618, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-icml-2025-12od7hickz/fig-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 1638, \"height\": 616, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-icml-2025-12od7hickz/fig-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 1642, \"height\": 1311, \"label\": \"Figure\"}]"
tables_json: "[{\"url\": \"assets/tables/openreview/openreview-icml-2025-12od7hickz/table-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 1765, \"height\": 724, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-icml-2025-12od7hickz/table-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 814, \"height\": 326, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-icml-2025-12od7hickz/table-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 754, \"height\": 201, \"label\": \"Table\"}]"
motivation: 去中心化在线学习现有差分隐私算法在隐私性、最优性和计算效率上无法兼顾。
method: "提出满足(ε,0)-DP的新算法，结合去中心化优化与隐私噪声机制。"
result: 算法实现严格隐私保障的同时达到凸与强凸函数的最优遗憾界。
conclusion: 为隐私保护分布式在线学习提供了实用且可扩展的解决方案。
---

## Abstract
Although the differential privacy (DP) of decentralized online learning has garnered considerable attention recently, existing algorithms are unsatisfactory due to their inability to achieve $(\epsilon, 0)$-DP over all $T$ rounds, recover the optimal regret in the non-private case, and maintain the lightweight computation under complex constraints. To address these issues, we first propose a new decentralized online learning algorithm satisfying $(\epsilon, 0)$-DP over $T$ rounds, and show that it can achieve $\widetilde{O}(n(\rho^{-1/4}+\epsilon^{-1}\rho^{1/4})\sqrt{T})$ and $\widetilde{O}(n (\rho^{-1/2}+\epsilon^{-1}))$ regret bounds for convex and strongly convex functions respectively, where $n$ is the number of local learners and $\rho$ is the spectral gap of the communication matrix. As long as $\epsilon=\Omega(\sqrt{\rho})$, these bounds nearly match existing lower bounds in the non-private case, which implies that $(\epsilon, 0)$-DP of decentralized online learning may be ensured nearly for free. Our key idea is to design a block-decoupled accelerated gossip strategy that can be incorporated with the classical tree-based private aggregation, and also enjoys a faster average consensus among local learners. Furthermore, we develop a projection-free variant of our algorithm to keep the efficiency under complex constraints. As a trade-off, the above regret bounds degrade to $\widetilde{O}(n(T^{3/4}+\epsilon^{-1}T^{1/4}))$ and $\widetilde{O}(n(T^{2/3}+\epsilon^{-1}))$ respectively, which however are even better than the existing private centralized projection-free online algorithm.

---

## 论文详细总结（自动生成）

### 1. 检索相关性
去中心化在线学习算法实现(ε,0)-DP，获得接近最优遗憾界。

### 2. 核心内容
现有去中心化在线学习的差分隐私算法无法同时实现T轮(ε,0)-DP、最优遗憾和轻量计算。本文提出一种新算法，在获得严格差分隐私保障的同时，对于凸函数与强凸函数分别达到了近优的遗憾界，且无需复杂约束下的高计算成本。该工作为隐私保护分布式优化开辟了可扩展的路线。

### 3. 对应检索需求
privacy in distributed optimization。

### 4. 来源与原文
- Source：ICML-2025-Accepted
- OpenReview：[https://openreview.net/forum?id=12oD7HIckz](https://openreview.net/forum?id=12oD7HIckz)
