---
title: On-Device Collaborative Language Modeling via a Mixture of Generalists and Specialists
title_zh: 基于通才与专才混合的端侧协同语言建模
authors: "Dongyang Fan, Bettina Messmer, Nikita Doikov, Martin Jaggi"
date: 2025-05-01
pdf: "https://openreview.net/pdf?id=Eog0kXX7hW"
tags: ["query:daily"]
score: 7.0
evidence: 采用混合专家模型进行端侧隐私保护语言模型的联邦学习
tldr: 端侧大语言模型训练面临计算资源异质和数据异质挑战。本文提出CoMiGS方法，首次结合混合专家模型与双层优化，通过路由器在独立验证集上对齐目标分布，实现通才与专才的协同学习。实验表明，该方法在个性化语言建模中优于现有联邦学习方案，在保护隐私的同时提升了异构环境下的性能。
source: ICML-2025-Accepted
selection_source: conference_retrieval
figures_json: "[{\"url\": \"assets/figures/openreview/openreview-icml-2025-eog0kxx7hw/fig-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 786, \"height\": 341, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-icml-2025-eog0kxx7hw/fig-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 866, \"height\": 323, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-icml-2025-eog0kxx7hw/fig-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 869, \"height\": 187, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-icml-2025-eog0kxx7hw/fig-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 1303, \"height\": 552, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-icml-2025-eog0kxx7hw/fig-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 842, \"height\": 340, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-icml-2025-eog0kxx7hw/fig-006.webp\", \"caption\": \"\", \"page\": 0, \"index\": 6, \"width\": 850, \"height\": 197, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-icml-2025-eog0kxx7hw/fig-007.webp\", \"caption\": \"\", \"page\": 0, \"index\": 7, \"width\": 852, \"height\": 198, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-icml-2025-eog0kxx7hw/fig-008.webp\", \"caption\": \"\", \"page\": 0, \"index\": 8, \"width\": 851, \"height\": 204, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-icml-2025-eog0kxx7hw/fig-009.webp\", \"caption\": \"\", \"page\": 0, \"index\": 9, \"width\": 1728, \"height\": 410, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-icml-2025-eog0kxx7hw/fig-010.webp\", \"caption\": \"\", \"page\": 0, \"index\": 10, \"width\": 1572, \"height\": 975, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-icml-2025-eog0kxx7hw/fig-011.webp\", \"caption\": \"\", \"page\": 0, \"index\": 11, \"width\": 1728, \"height\": 719, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-icml-2025-eog0kxx7hw/fig-012.webp\", \"caption\": \"\", \"page\": 0, \"index\": 12, \"width\": 1741, \"height\": 391, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-icml-2025-eog0kxx7hw/fig-013.webp\", \"caption\": \"\", \"page\": 0, \"index\": 13, \"width\": 1740, \"height\": 391, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-icml-2025-eog0kxx7hw/fig-014.webp\", \"caption\": \"\", \"page\": 0, \"index\": 14, \"width\": 1742, \"height\": 394, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-icml-2025-eog0kxx7hw/fig-015.webp\", \"caption\": \"\", \"page\": 0, \"index\": 15, \"width\": 1743, \"height\": 1362, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-icml-2025-eog0kxx7hw/fig-016.webp\", \"caption\": \"\", \"page\": 0, \"index\": 16, \"width\": 1743, \"height\": 1362, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-icml-2025-eog0kxx7hw/fig-017.webp\", \"caption\": \"\", \"page\": 0, \"index\": 17, \"width\": 1743, \"height\": 1362, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-icml-2025-eog0kxx7hw/fig-018.webp\", \"caption\": \"\", \"page\": 0, \"index\": 18, \"width\": 1744, \"height\": 1366, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-icml-2025-eog0kxx7hw/fig-019.webp\", \"caption\": \"\", \"page\": 0, \"index\": 19, \"width\": 1744, \"height\": 1367, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-icml-2025-eog0kxx7hw/fig-020.webp\", \"caption\": \"\", \"page\": 0, \"index\": 20, \"width\": 1744, \"height\": 1367, \"label\": \"Figure\"}]"
tables_json: "[{\"url\": \"assets/tables/openreview/openreview-icml-2025-eog0kxx7hw/table-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 852, \"height\": 364, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-icml-2025-eog0kxx7hw/table-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 849, \"height\": 472, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-icml-2025-eog0kxx7hw/table-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 680, \"height\": 176, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-icml-2025-eog0kxx7hw/table-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 1413, \"height\": 682, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-icml-2025-eog0kxx7hw/table-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 1416, \"height\": 1036, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-icml-2025-eog0kxx7hw/table-006.webp\", \"caption\": \"\", \"page\": 0, \"index\": 6, \"width\": 1131, \"height\": 316, \"label\": \"Table\"}]"
motivation: 端侧联邦学习存在资源异质和数据异质，影响模型性能。
method: 提出CoMiGS，通过混合专家模型和双层优化实现路由器的个性化对齐。
result: 在语言建模任务上，CoMiGS比现有联邦方法准确率更高。
conclusion: CoMiGS有效缓解端侧异构性问题，提升隐私保护的协作学习效果。
---

## Abstract
On-device LLMs have gained increasing attention for their ability to enhance privacy and provide a personalized user experience. To facilitate private learning with scarce data, Federated Learning has become a standard approach. However, it faces challenges such as computational resource heterogeneity and data heterogeneity among end users. We propose CoMiGS ($\textbf{Co}$llaborative learning  with a $\textbf{Mi}$xture of $\textbf{G}$eneralists and $\textbf{S}$pecialists), the first approach to address both challenges. A key innovation of our method is the bi-level optimization formulation of the Mixture-of-Experts learning objective, where the router is optimized using a separate validation set to ensure alignment with the target distribution. We solve our objective with alternating minimization, for which we provide a theoretical analysis. Our method shares generalist experts across users while localizing a varying number of specialist experts, thereby adapting to users’ computational resources and preserving privacy. Through extensive experiments, we show CoMiGS effectively balances general and personalized knowledge for each token generation. We demonstrate that CoMiGS remains robust against overfitting—due to the generalists' regularizing effect—while adapting to local data through specialist expertise. We open source our codebase for collaborative LLMs.

---

## 论文详细总结（自动生成）

### 1. 检索相关性
采用混合专家模型进行端侧隐私保护语言模型的联邦学习。

### 2. 核心内容
端侧大语言模型训练面临计算资源异质和数据异质挑战。本文提出CoMiGS方法，首次结合混合专家模型与双层优化，通过路由器在独立验证集上对齐目标分布，实现通才与专才的协同学习。实验表明，该方法在个性化语言建模中优于现有联邦学习方案，在保护隐私的同时提升了异构环境下的性能。

### 3. 对应检索需求
privacy in distributed machine learning。

### 4. 来源与原文
- Source：ICML-2025-Accepted
- OpenReview：[https://openreview.net/forum?id=Eog0kXX7hW](https://openreview.net/forum?id=Eog0kXX7hW)
