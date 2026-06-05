---
title: Certification for Differentially Private Prediction in Gradient-Based Training
title_zh: 梯度训练中差分隐私预测的认证
authors: "Matthew Robert Wicker, Philip Sosnin, Igor Shilov, Adrianna Janik, Mark Niklas Mueller, Yves-Alexandre de Montjoye, Adrian Weller, Calvin Tsay"
date: 2025-05-01
pdf: "https://openreview.net/pdf?id=viXwXCkA7N"
tags: ["query:daily"]
score: 4.0
evidence: 差分隐私预测认证，与机器学习隐私相关
tldr: 针对现有差分隐私预测依赖全局敏感度导致效用下降的问题，本文提出基于数据集特定敏感度上界的认证方法，利用凸松弛和边界传播技术计算平滑敏感度，从而在预测时获得更优的隐私-效用权衡。在医学图像分类和自然语言处理任务上的实验表明，该方法优于基于全局敏感度的方案。该工作为梯度训练模型的安全部署提供了隐私保证新途径。
source: ICML-2025-Accepted
selection_source: conference_retrieval
figures_json: "[{\"url\": \"assets/figures/openreview/openreview-icml-2025-vixwxcka7n/fig-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 1724, \"height\": 377, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-icml-2025-vixwxcka7n/fig-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 1699, \"height\": 377, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-icml-2025-vixwxcka7n/fig-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 759, \"height\": 495, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-icml-2025-vixwxcka7n/fig-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 1701, \"height\": 482, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-icml-2025-vixwxcka7n/fig-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 1689, \"height\": 365, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-icml-2025-vixwxcka7n/fig-006.webp\", \"caption\": \"\", \"page\": 0, \"index\": 6, \"width\": 803, \"height\": 413, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-icml-2025-vixwxcka7n/fig-007.webp\", \"caption\": \"\", \"page\": 0, \"index\": 7, \"width\": 1703, \"height\": 476, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-icml-2025-vixwxcka7n/fig-008.webp\", \"caption\": \"\", \"page\": 0, \"index\": 8, \"width\": 758, \"height\": 458, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-icml-2025-vixwxcka7n/fig-009.webp\", \"caption\": \"\", \"page\": 0, \"index\": 9, \"width\": 681, \"height\": 427, \"label\": \"Figure\"}]"
tables_json: "[{\"url\": \"assets/tables/openreview/openreview-icml-2025-vixwxcka7n/table-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 849, \"height\": 323, \"label\": \"Table\"}]"
motivation: 现有差分隐私预测方法使用全局敏感度，导致噪声过大、效用低下，无法满足实际应用需求。
method: 提出基于凸松弛和边界传播的数据集特定敏感度上界计算方法，结合平滑敏感度机制实现认证。
result: 在医学图像和文本分类上，该方法显著提升了隐私-效用权衡，优于基于全局敏感度的现有方案。
conclusion: 该认证方法为差分隐私预测提供了更精细的敏感度控制，可推广至各种梯度训练模型，增强安全部署。
---

## Abstract
We study private prediction where differential privacy is achieved by adding noise to the outputs of a non-private model. Existing methods rely on noise proportional to the global sensitivity of the model, often resulting in sub-optimal privacy-utility trade-offs compared to private training. We introduce a novel approach for computing dataset-specific upper bounds on prediction sensitivity by leveraging convex relaxation and bound propagation techniques. By combining these bounds with the smooth sensitivity mechanism, we significantly improve the privacy analysis of private prediction compared to global sensitivity-based approaches. Experimental results across real-world datasets in medical image classification and natural language processing demonstrate that our sensitivity bounds are can be orders of magnitude tighter than global sensitivity. Our approach provides a strong basis for the development of novel privacy preserving technologies.

---

## 论文详细总结（自动生成）

### 1. 检索相关性
差分隐私预测认证，与机器学习隐私相关。

### 2. 核心内容
针对现有差分隐私预测依赖全局敏感度导致效用下降的问题，本文提出基于数据集特定敏感度上界的认证方法，利用凸松弛和边界传播技术计算平滑敏感度，从而在预测时获得更优的隐私-效用权衡。在医学图像分类和自然语言处理任务上的实验表明，该方法优于基于全局敏感度的方案。该工作为梯度训练模型的安全部署提供了隐私保证新途径。

### 3. 对应检索需求
privacy in distributed machine learning。

### 4. 来源与原文
- Source：ICML-2025-Accepted
- OpenReview：[https://openreview.net/forum?id=viXwXCkA7N](https://openreview.net/forum?id=viXwXCkA7N)
