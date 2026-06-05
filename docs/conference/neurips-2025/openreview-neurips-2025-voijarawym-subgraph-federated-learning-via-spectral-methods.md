---
title: Subgraph Federated Learning via Spectral Methods
title_zh: 基于谱方法的子图联邦学习
authors: "Javad Aliakbari, Johan Östman, Ashkan Panahi, Alexandre Graell i Amat"
date: 2025-09-18
pdf: "https://openreview.net/pdf?id=vOijARaWym"
tags: ["query:daily"]
score: 9.0
evidence: 子图联邦学习中的隐私保护
tldr: 现有子图联邦学习方法需交换敏感节点嵌入存在隐私风险，或计算量过大。FedLap框架利用谱域拉普拉斯平滑捕获全局结构信息，在保护隐私的同时高效建模节点间依赖。该工作形式化分析了隐私保障，为分布式图学习提供了安全可扩展的解决方案。
source: NeurIPS-2025-Accepted
selection_source: conference_retrieval
figures_json: "[{\"url\": \"assets/figures/openreview/openreview-neurips-2025-voijarawym/fig-001.webp\", \"caption\": \"\", \"page\": 4, \"index\": 1, \"width\": 800, \"height\": 800}, {\"url\": \"assets/figures/openreview/openreview-neurips-2025-voijarawym/fig-002.webp\", \"caption\": \"\", \"page\": 4, \"index\": 2, \"width\": 400, \"height\": 400}, {\"url\": \"assets/figures/openreview/openreview-neurips-2025-voijarawym/fig-003.webp\", \"caption\": \"\", \"page\": 4, \"index\": 3, \"width\": 400, \"height\": 400}, {\"url\": \"assets/figures/openreview/openreview-neurips-2025-voijarawym/fig-004.webp\", \"caption\": \"\", \"page\": 4, \"index\": 4, \"width\": 400, \"height\": 400}, {\"url\": \"assets/figures/openreview/openreview-neurips-2025-voijarawym/fig-005.webp\", \"caption\": \"\", \"page\": 4, \"index\": 5, \"width\": 400, \"height\": 400}, {\"url\": \"assets/figures/openreview/openreview-neurips-2025-voijarawym/fig-006.webp\", \"caption\": \"\", \"page\": 6, \"index\": 6, \"width\": 901, \"height\": 759}, {\"url\": \"assets/figures/openreview/openreview-neurips-2025-voijarawym/fig-007.webp\", \"caption\": \"\", \"page\": 6, \"index\": 7, \"width\": 898, \"height\": 755}, {\"url\": \"assets/figures/openreview/openreview-neurips-2025-voijarawym/fig-008.webp\", \"caption\": \"\", \"page\": 6, \"index\": 8, \"width\": 900, \"height\": 756}]"
motivation: 现有子图联邦学习存在隐私风险或计算开销大。
method: 提出FedLap，利用谱域拉普拉斯平滑捕获节点间依赖，保护隐私。
result: 形式化分析了隐私保障，并确保可扩展性。
conclusion: 为图结构分布式学习的隐私保护提供了新框架。
---

## Abstract
We consider the problem of federated learning (FL) with graph-structured data distributed across multiple clients. In particular, we address the common scenario of interconnected subgraphs, where interconnections between clients significantly influence the learning process. Existing approaches suffer from critical limitations, either requiring the exchange of sensitive node embeddings, thereby posing privacy risks, or relying on computationally-intensive steps, which hinders scalability.

To tackle these challenges, we propose FedLap, a novel framework that leverages global structure information via Laplacian smoothing in the spectral domain to effectively capture inter-node dependencies while ensuring privacy and scalability. We provide a formal analysis of the privacy of FedLap, demonstrating that it preserves privacy. Notably, FedLap is the first subgraph FL scheme with strong privacy guarantees. Extensive experiments on benchmark datasets demonstrate that the proposed method achieves competitive or superior utility compared to existing techniques.

---

## 论文详细总结（自动生成）

## 1. 论文的核心问题与整体含义

- 论文聚焦**子图联邦学习（Subgraph Federated Learning, SFL）** 中的隐私与通信挑战。在金融反洗钱、社交网络等场景中，图数据天然分布于多个客户端，客户端子图之间存在跨客户端连边（interconnections），这对全局预测至关重要。
- 现有SFL方法普遍存在两类缺陷：
  - 为获取跨客户端信息，需交换节点特征或嵌入，**造成严重隐私泄露**（如FedSAGE、FedGCN）。
  - 若采用结构共享（如FedStruct），**通信开销巨大且缺乏形式化隐私分析**，难以扩展。
- 本文旨在突破准确率‑隐私‑通信的“三难困境”，提出首个**具备强隐私保证**的SFL框架，同时维持与集中式方案可比拟的预测性能。

## 2. 方法论：FedLap 与 FedLap+

### 2.1 核心思想

- 利用谱域拉普拉斯平滑（Laplacian Smoothing）隐式捕捉节点间的结构依赖，避免直接交换敏感信息。
- 将学习过程分为：
  - **离线阶段**：一次性计算全局图结构频谱，不涉及模型训练，仅交换结构派生量（如Arnoldi迭代中的矩阵‑向量积）。
  - **在线阶段**：退化为标准联邦学习，仅共享模型参数，可结合差分隐私等保护。

### 2.2 关键技术细节

- **FedLap**：在本地损失函数中加入归一化拉普拉斯正则项 \( \lambda_\text{reg} \frac{\operatorname{Tr}(S^\top L_G S)}{\operatorname{Tr}(S^\top S)} \)，其中 \(S\) 为根据Hop2Vec生成的结构特征矩阵。该正则项可按局部邻居计算，无需全局 \(A\) 矩阵，从而降低通信并增强隐私。
- **FedLap+**：对图拉普拉斯矩阵进行谱分解 \(L_G = U\Lambda U^\top\)，将 \(S\) 表示为 \(S = UW\)，并截断保留最小的 \(r\) 个特征值（及其特征向量）。由此，正则项退化为低通滤波 \( \sum_{j=1}^r \lambda_j \|w_j\|^2 / \sum_{j=1}^r \|w_j\|^2 \)，迫使表示对齐平滑成分，同时将可学习参数缩减至小矩阵 \(W \in \mathbb{R}^{r \times d_s}\)。
- **去中心化 Arnoldi 迭代**：各客户端利用同态加密协同计算 \(L_G\) 的部分特征向量，无需向服务器或其它客户端暴露原始邻接信息。该过程仅涉及形如 \(A_{V_i,V_j} q_{V_j}\) 的加密和，计算复杂度 \(O(n r^2)\)（线性于节点数），适用于大规模稀疏图。

### 2.3 隐私分析概要

- 离线阶段唯一的泄露通道是边信息。论文在最强攻击假设（两客户端，攻击者已知自身邻接块并获取矩阵 \(U = \bar A \bar Q\)）下，通过似然比检验推导出攻击者的真阳率、假阳率、精确率与召回率。
- 理论分析表明，当截断秩 \(r\) 足够小、图足够稀疏（\(p\) 小）且节点数 \(n\) 大时，攻击者区分连边存在与否的能力极弱（精确率+召回率 ≤ 1），等价于随机猜测。
- 在线阶段与标准FL相同，可复用已有的隐私增强技术。

## 3. 实验设计

- **数据集**：6个基准图数据集——Cora、Citeseer、PubMed、Chameleon、Amazon Photo、Ogbn-Arxiv，覆盖不同边同质率（homophily）。
- **划分与标签**：图被随机划分（或 Louvain / KMeans 划分）为 5、10、20 个客户端；每个客户端取 10% 节点训练，10% 验证，80% 测试。
- **对比方法**：
  - 无隐私保护边界：FedSGD GNN、FedSAGE+、FedPUB；
  - 交换结构信息（有隐私风险）：FedGCN-2Hop、FedStruct；
  - 本文方法：FedLap、FedLap+（Arnoldi 截断）；
  - 上下界：Central GNN（完整图训练）和 Local GNN（仅本地子图）。
- **评估指标**：10 次随机运行的平均 top‑1 准确率及标准差。

## 4. 资源与算力

- 训练环境：2 块 NVIDIA Tesla V100 SXM2 GPU，每块 32GB 显存。
- 文中未提供具体训练时长，但强调所提方法在离线阶段仅需一次性 Arnoldi 迭代，复杂度为 \(O(n r^2)\)，且在线通信量与 FedAvg 持平，明显低于 FedStruct 等方案。

## 5. 实验数量与充分性

- 进行了 **多数据集 × 多客户端数 × 多划分方式 × 多训练比例** 的组合实验，并包含超参数敏感性分析（截断秩 \(r\)、正则系数 \(\lambda_\text{reg}\)）。
- 每个实验设置均独立运行 10 次，报告均值和标准差，结果表与消融曲线充分。
- 消融实验涵盖：
  - 训练比例对准确率的影响（0.1~0.5）；
  - 谱截断数 \(r\) 的影响（50~200）；
  - 正则化强度的影响（0~100）；
  - 不同划分策略的性能对比（Louvain、Random、KMeans）。
- 所有对比方法采用相同数据划分和评估协议，公平性较佳。部分方法（如 FedGCN）因实现细节可能有利偏差异被明确指出。

## 6. 主要结论与发现

- **FedLap/FedLap+ 在多种设置下均达到或超越当前最优的 SFL 方法**，且是首个提供形式化隐私保障的框架。
- 在同质图上，FedLap 表现优异；在异质图（如 Chameleon）上，谱截断的 FedLap+ 更具鲁棒性。
- 仅需很小的截断秩（如 \(r=100\)）即可捕捉足够全局结构，在保持隐私的同时大幅降低通信。
- 攻击理论分析与实际攻击对比表明，即使假设强攻击者，隐私泄露依然可控，实际攻击效果弱于理论预测。

## 7. 优点

- **首次实现强隐私保障**：理论推导了边推断攻击的精确率/召回率界限，给出明确的安全操作区间。
- **高效通信**：离线阶段只交换一次结构化信息，在线阶段与 FedAvg 等价，通信量显著低于 FedStruct 等。
- **可扩展性**：去中心化 Arnoldi 算法复杂度与节点数线性相关，可处理 Ogbn-Arxiv（17 万节点）等大图。
- **简洁且灵活**：将结构先验融入正则项，能与任意 FL 框架组合，截断机制自带正则化效果，减少超参调优需求。
- **全面的实验验证**：覆盖多个领域、划分方法和消融维度，证明了方法的通用性和稳定性。

## 8. 不足与局限

- **计算资源需求未详细说明**：虽给出 GPU 型号，但未公布具体训练时间或单次通信的耗时，难以评估实际部署开销。
- **仅针对节点分类任务**：论文仅测试了节点分类，未涉及边预测或图级任务，框架的通用性尚待验证。
- **假设已知跨客户端连边**：现实中某些场景（如严格数据隔离）可能无法获知 inter-client edges，这会限制方法适用性。
- **攻击模型简化**：隐私分析基于两个客户端且一定独立性假设，对多客户端合谋或更复杂的推断攻击未深入探讨。
- **在极端异质图上可能受限**：尽管 FedLap+ 通过截断改善了鲁棒性，但对于高度非平滑信号占主导的异质图，低通滤波可能去除有用的高频模式。

(完)

给出的上一次输出已经完整，末尾包含 “（完）”，无明显截断。无需补充。

（完）
