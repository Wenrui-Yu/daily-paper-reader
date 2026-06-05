---
title: Gradient Inversion of Multimodal Models
title_zh: 多模态模型的梯度反演攻击
authors: "Omri Ben Hemo, Alon Zolfi, Oryan Yehezkel, Omer Hofman, Roman Vainshtein, Hisashi Kojima, Yuval Elovici, Asaf Shabtai"
date: 2025-05-01
pdf: "https://openreview.net/pdf?id=j4IELrBhoG"
tags: ["query:daily"]
score: 8.0
evidence: 探索联邦学习中多模态模型的梯度反演攻击
tldr: 联邦学习共享梯度易受反演攻击，但现有工作主要针对单模态任务。本文针对多模态文档视觉问答（DQA）模型，提出GI-DQA梯度反演攻击方法，利用模态间的关联重构私密文档信息。实验证明多模态模型比单模态模型泄露更多隐私，揭示了多模态联邦学习的严重安全风险，为防御研究提供重要警示。
source: ICML-2025-Accepted
selection_source: conference_retrieval
figures_json: "[{\"url\": \"assets/figures/openreview/openreview-icml-2025-j4ielrbhog/fig-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 718, \"height\": 391, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-icml-2025-j4ielrbhog/fig-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 1334, \"height\": 564, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-icml-2025-j4ielrbhog/fig-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 596, \"height\": 134, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-icml-2025-j4ielrbhog/fig-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 1673, \"height\": 754, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-icml-2025-j4ielrbhog/fig-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 629, \"height\": 580, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-icml-2025-j4ielrbhog/fig-006.webp\", \"caption\": \"\", \"page\": 0, \"index\": 6, \"width\": 802, \"height\": 501, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-icml-2025-j4ielrbhog/fig-007.webp\", \"caption\": \"\", \"page\": 0, \"index\": 7, \"width\": 1824, \"height\": 1496, \"label\": \"Figure\"}]"
tables_json: "[{\"url\": \"assets/tables/openreview/openreview-icml-2025-j4ielrbhog/table-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 1709, \"height\": 278, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-icml-2025-j4ielrbhog/table-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 890, \"height\": 440, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-icml-2025-j4ielrbhog/table-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 860, \"height\": 245, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-icml-2025-j4ielrbhog/table-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 725, \"height\": 187, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-icml-2025-j4ielrbhog/table-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 1069, \"height\": 253, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-icml-2025-j4ielrbhog/table-006.webp\", \"caption\": \"\", \"page\": 0, \"index\": 6, \"width\": 1250, \"height\": 386, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-icml-2025-j4ielrbhog/table-007.webp\", \"caption\": \"\", \"page\": 0, \"index\": 7, \"width\": 1049, \"height\": 326, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-icml-2025-j4ielrbhog/table-008.webp\", \"caption\": \"\", \"page\": 0, \"index\": 8, \"width\": 926, \"height\": 215, \"label\": \"Table\"}]"
motivation: 多模态联邦学习的隐私风险缺乏深入研究。
method: 设计GI-DQA攻击，利用视觉和文本模态的联合信息重建私有文档。
result: 成功从梯度中恢复文档文本和布局，隐私泄露显著。
conclusion: 多模态模型加剧梯度反演风险，需强化隐私保护。
---

## Abstract
Federated learning (FL) enables privacy-preserving distributed machine learning by sharing gradients instead of raw data. However, FL remains vulnerable to gradient inversion attacks, in which shared gradients can reveal sensitive training data. Prior research has mainly concentrated on unimodal tasks, particularly image classification, examining the reconstruction of single-modality data, and analyzing privacy vulnerabilities in these relatively simple scenarios. As multimodal models are increasingly used to address complex vision-language tasks, it becomes essential to assess the privacy risks inherent in these architectures. In this paper, we explore gradient inversion attacks targeting multimodal vision-language Document Visual Question Answering (DQA) models and propose GI-DQA, a novel method that reconstructs private document content from gradients. Through extensive evaluation on state-of-the-art DQA models, our approach exposes critical privacy vulnerabilities and highlights the urgent need for robust defenses to secure multimodal FL systems.

---

## 论文详细总结（自动生成）

### 1. 检索相关性
探索联邦学习中多模态模型的梯度反演攻击。

### 2. 核心内容
联邦学习共享梯度易受反演攻击，但现有工作主要针对单模态任务。本文针对多模态文档视觉问答（DQA）模型，提出GI-DQA梯度反演攻击方法，利用模态间的关联重构私密文档信息。实验证明多模态模型比单模态模型泄露更多隐私，揭示了多模态联邦学习的严重安全风险，为防御研究提供重要警示。

### 3. 对应检索需求
privacy in distributed machine learning。

### 4. 来源与原文
- Source：ICML-2025-Accepted
- OpenReview：[https://openreview.net/forum?id=j4IELrBhoG](https://openreview.net/forum?id=j4IELrBhoG)
