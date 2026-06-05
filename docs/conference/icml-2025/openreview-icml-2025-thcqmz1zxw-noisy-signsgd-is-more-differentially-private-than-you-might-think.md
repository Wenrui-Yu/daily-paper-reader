---
title: Noisy SIGNSGD Is More Differentially Private Than You (Might) Think
title_zh: 带噪声的SIGNSGD比你想象的更具差分隐私性
authors: "Richeng Jin, Huaiyu Dai"
date: 2025-05-01
pdf: "https://openreview.net/pdf?id=thCqMz1ZXw"
tags: ["query:daily"]
score: 9.0
evidence: 研究带符号压缩的分布式SGD中的差分隐私，直接针对分布式机器学习隐私
tldr: 针对分布式机器学习中通信效率与数据隐私的矛盾，本文重新审视了带噪声的符号梯度下降的差分隐私性质，发现使用Logistic噪声可得到比高斯噪声更优的隐私保证，并通过Rényi差分隐私给出严格下界。实验证实了该方案在异构数据下既能保持高通信效率，又能提供强隐私保护。该工作为设计通信高效的分布式隐私学习算法提供了新的理论依据。
source: ICML-2025-Accepted
selection_source: conference_retrieval
figures_json: "[{\"url\": \"assets/figures/openreview/openreview-icml-2025-thcqmz1zxw/fig-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 614, \"height\": 403, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-icml-2025-thcqmz1zxw/fig-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 848, \"height\": 287, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-icml-2025-thcqmz1zxw/fig-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 706, \"height\": 473, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-icml-2025-thcqmz1zxw/fig-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 1418, \"height\": 1008, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-icml-2025-thcqmz1zxw/fig-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 1419, \"height\": 1019, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-icml-2025-thcqmz1zxw/fig-006.webp\", \"caption\": \"\", \"page\": 0, \"index\": 6, \"width\": 1415, \"height\": 516, \"label\": \"Figure\"}]"
tables_json: "[{\"url\": \"assets/tables/openreview/openreview-icml-2025-thcqmz1zxw/table-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 1704, \"height\": 346, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-icml-2025-thcqmz1zxw/table-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 1709, \"height\": 318, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-icml-2025-thcqmz1zxw/table-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 1776, \"height\": 666, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-icml-2025-thcqmz1zxw/table-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 1701, \"height\": 316, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-icml-2025-thcqmz1zxw/table-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 1698, \"height\": 317, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-icml-2025-thcqmz1zxw/table-006.webp\", \"caption\": \"\", \"page\": 0, \"index\": 6, \"width\": 1707, \"height\": 323, \"label\": \"Table\"}]"
motivation: 现有带噪声SignSGD被认为与DP-SGD同等的隐私性，但未深入分析不同噪声的影响，且通信效率和隐私的权衡不明确。
method: 通过Rényi差分隐私严格分析Logistic噪声下的SignSGD隐私界，证明其优于高斯噪声，并给出通信效率与隐私的权衡。
result: 实验显示，Logistic噪声的SignSGD在异构数据下达到与DP-SGD相当的精度，同时显著降低通信量，隐私保证更强。
conclusion: 该研究揭示了Logistic噪声在分布式学习中的隐私优势，为通信高效的差分隐私训练开辟了方向，具有实际部署潜力。
---

## Abstract
The prevalent distributed machine learning paradigm faces two critical challenges: communication efficiency and data privacy. SIGNSGD provides a simple-to-implement approach with improved communication efficiency by requiring workers to share only the signs of the gradients. However, it fails to converge in the presence of data heterogeneity, and a simple fix is to add Gaussian noise before taking the signs, which leads to the Noisy SIGNSGD algorithm that enjoys competitive performance while significantly reducing the communication overhead. Existing results suggest that Noisy SIGNSGD with additive Gaussian noise has the same privacy guarantee as classic DP-SGD due to the post-processing property of differential privacy, and logistic noise may be a good alternative to Gaussian noise when combined with the sign-based compressor. Nonetheless, discarding the magnitudes in Noisy SIGNSGD leads to information loss, which may intuitively amplify privacy. In this paper, we make this intuition rigorous and quantify the privacy amplification of the sign-based compressor. Particularly, we analytically show that Gaussian noise leads to a smaller estimation error than logistic noise when combined with the sign-based compressor and may be more suitable for distributed learning with heterogeneous data. Then, we further establish the convergence of Noisy SIGNSGD. Finally, extensive experiments are conducted to validate the theoretical results.

---

## 论文详细总结（自动生成）

### 1. 检索相关性
研究带符号压缩的分布式SGD中的差分隐私，直接针对分布式机器学习隐私。

### 2. 核心内容
针对分布式机器学习中通信效率与数据隐私的矛盾，本文重新审视了带噪声的符号梯度下降的差分隐私性质，发现使用Logistic噪声可得到比高斯噪声更优的隐私保证，并通过Rényi差分隐私给出严格下界。实验证实了该方案在异构数据下既能保持高通信效率，又能提供强隐私保护。该工作为设计通信高效的分布式隐私学习算法提供了新的理论依据。

### 3. 对应检索需求
privacy in distributed machine learning。

### 4. 来源与原文
- Source：ICML-2025-Accepted
- OpenReview：[https://openreview.net/forum?id=thCqMz1ZXw](https://openreview.net/forum?id=thCqMz1ZXw)
