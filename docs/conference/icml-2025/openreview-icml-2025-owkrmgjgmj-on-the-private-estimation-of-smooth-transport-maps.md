---
title: On the Private Estimation of Smooth Transport Maps
title_zh: 光滑传输映射的私有估计研究
authors: "Clément Lalanne, Franck Iutzeler, Jean-Michel Loubes, Julien Chhor"
date: 2025-05-01
pdf: "https://openreview.net/pdf?id=oWkRmgJgMJ"
tags: ["query:daily"]
score: 8.0
evidence: 差分隐私最优传输映射估计
tldr: "针对最优传输中隐私保护不足的问题,提出差分隐私下的光滑传输映射估计方法,给出L2误差界,实现了隐私与精度的良好平衡。"
source: ICML-2025-Accepted
selection_source: conference_retrieval
figures_json: "[{\"url\": \"assets/figures/openreview/openreview-icml-2025-owkrmgjgmj/fig-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 1664, \"height\": 904, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-icml-2025-owkrmgjgmj/fig-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 1602, \"height\": 586, \"label\": \"Figure\"}]"
motivation: 最优传输映射估计中样本隐私缺乏保护。
method: 提出基于Brenier势函数的差分隐私传输映射估计器。
result: "得到了近乎最优的L2误差界,平衡了隐私与准确性。"
conclusion: 差分隐私可有效应用于最优传输映射估计。
---

## Abstract
Estimating optimal transport maps between two distributions from respective samples is an important element for many machine learning methods. 
To do so, rather than extending discrete transport maps, it has been shown that estimating the Brenier potential of the transport problem and obtaining a transport map through its gradient is near minimax optimal for smooth problems. 
In this paper, we investigate the private estimation of such potentials and transport maps with respect to the distribution samples.
We propose a differentially private transport map estimator with $L^2$ error at most $n^{-1} \vee n^{-\frac{2 \alpha}{2 \alpha - 2 + d}} \vee (n\epsilon)^{-\frac{2 \alpha}{2 \alpha + d}} $ up do polylog terms where $n$ is the sample size, $\epsilon$ is the desired level of privacy, $\alpha$ is the smoothness of the true transport map, and $d$ is the dimension of the feature space. 
We also provide a lower bound for the problem.

---

## 论文详细总结（自动生成）

### 1. 检索相关性
差分隐私最优传输映射估计。

### 2. 核心内容
针对最优传输中隐私保护不足的问题,提出差分隐私下的光滑传输映射估计方法,给出L2误差界,实现了隐私与精度的良好平衡。

### 3. 对应检索需求
p。

### 4. 来源与原文
- Source：ICML-2025-Accepted
- OpenReview：[https://openreview.net/forum?id=oWkRmgJgMJ](https://openreview.net/forum?id=oWkRmgJgMJ)
