---
title: "Hot PATE: Private Aggregation of Distributions  for Diverse Tasks"
title_zh: Hot PATE：面向多样性任务的分布私有聚合
authors: "Edith Cohen, Benjamin Cohen-Wang, Xin Lyu, Jelani Nelson, Tamas Sarlos, Uri Stemmer"
date: 2025-01-22
pdf: "https://openreview.net/pdf?id=T2ujAPFA4C"
tags: ["query:daily"]
score: 6.0
evidence: 拓展PATE框架处理多样性任务，解决私有聚合中多样性与隐私的冲突
tldr: 针对PATE框架在文本生成等多样输出任务中面临输出多样性增大则隐私损失高的困境，本文提出Hot PATE方法，通过改进聚合策略，在保证差分隐私的同时维持输出多样性。该技术对分布式环境下的隐私保护大模型知识提取等任务具有重要价值。
source: ICML-2025-Rejected-Public
selection_source: conference_retrieval
figures_json: "[{\"url\": \"assets/figures/openreview/openreview-icml-2025-t2ujapfa4c/fig-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 853, \"height\": 224, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-icml-2025-t2ujapfa4c/fig-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 868, \"height\": 400, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-icml-2025-t2ujapfa4c/fig-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 790, \"height\": 303, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-icml-2025-t2ujapfa4c/fig-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 802, \"height\": 271, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-icml-2025-t2ujapfa4c/fig-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 763, \"height\": 880, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-icml-2025-t2ujapfa4c/fig-006.webp\", \"caption\": \"\", \"page\": 0, \"index\": 6, \"width\": 668, \"height\": 1083, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-icml-2025-t2ujapfa4c/fig-007.webp\", \"caption\": \"\", \"page\": 0, \"index\": 7, \"width\": 1501, \"height\": 391, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-icml-2025-t2ujapfa4c/fig-008.webp\", \"caption\": \"\", \"page\": 0, \"index\": 8, \"width\": 1408, \"height\": 537, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-icml-2025-t2ujapfa4c/fig-009.webp\", \"caption\": \"\", \"page\": 0, \"index\": 9, \"width\": 1638, \"height\": 203, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-icml-2025-t2ujapfa4c/fig-010.webp\", \"caption\": \"\", \"page\": 0, \"index\": 10, \"width\": 1640, \"height\": 201, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-icml-2025-t2ujapfa4c/fig-011.webp\", \"caption\": \"\", \"page\": 0, \"index\": 11, \"width\": 1639, \"height\": 395, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-icml-2025-t2ujapfa4c/fig-012.webp\", \"caption\": \"\", \"page\": 0, \"index\": 12, \"width\": 1734, \"height\": 1243, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-icml-2025-t2ujapfa4c/fig-013.webp\", \"caption\": \"\", \"page\": 0, \"index\": 13, \"width\": 1795, \"height\": 1816, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-icml-2025-t2ujapfa4c/fig-014.webp\", \"caption\": \"\", \"page\": 0, \"index\": 14, \"width\": 1497, \"height\": 592, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-icml-2025-t2ujapfa4c/fig-015.webp\", \"caption\": \"\", \"page\": 0, \"index\": 15, \"width\": 1708, \"height\": 462, \"label\": \"Figure\"}]"
tables_json: "[{\"url\": \"assets/tables/openreview/openreview-icml-2025-t2ujapfa4c/table-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 827, \"height\": 420, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-icml-2025-t2ujapfa4c/table-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 1787, \"height\": 218, \"label\": \"Table\"}]"
motivation: PATE框架在多样性任务中输出多样性与隐私保护存在冲突。
method: 提出Hot PATE方法，改进聚合机制以平衡多样性与隐私。
result: 在保证隐私前提下有效维持了输出的多样性。
conclusion: 为分布式隐私机器学习中的多样性任务提供了新解决方案。
---

## Abstract
The Private Aggregation of Teacher Ensembles (PATE) framework is a versatile approach to privacy-preserving machine learning. In PATE, responses made based on different parts of sensitive data are aggregated into a single response in a privacy-preserving way. Recently, multiple works applied PATE for tasks such as sequential text generation that are inherently
 diverse (or "hot"), with multiple valid responses. These designs, however, suffer from
  tension between diversity and privacy -- since diversity in the responses reduces agreement which forces the aggregation to use smaller noise scales and thus incur higher privacy loss. But limiting diversity of the aggregate response is undesirable since in modern large language models, the very knowledge we want to transfer is encapsulated in the response distribution.
   We propose \emph{hot PATE} that is tailored for the diverse setting where responses are distributions. We formally define \emph{preserving diversity} and design an efficient aggregation method that provably transfers the diversity to the (randomized) aggregate response while incurring no privacy penalty. The method can be implemented using an API access to proprietary models and used as a plug-in replacement for the baseline ``cold'' PATE in existing tools. We demonstrate empirically the potential of hot PATE for an order of magnitude improvement in a task of in-context learning via prompts.

---

## 论文详细总结（自动生成）

### 1. 检索相关性
拓展PATE框架处理多样性任务，解决私有聚合中多样性与隐私的冲突。

### 2. 核心内容
针对PATE框架在文本生成等多样输出任务中面临输出多样性增大则隐私损失高的困境，本文提出Hot PATE方法，通过改进聚合策略，在保证差分隐私的同时维持输出多样性。该技术对分布式环境下的隐私保护大模型知识提取等任务具有重要价值。

### 3. 对应检索需求
privacy in distributed machine learning。

### 4. 来源与原文
- Source：ICML-2025-Rejected-Public
- OpenReview：[https://openreview.net/forum?id=T2ujAPFA4C](https://openreview.net/forum?id=T2ujAPFA4C)
