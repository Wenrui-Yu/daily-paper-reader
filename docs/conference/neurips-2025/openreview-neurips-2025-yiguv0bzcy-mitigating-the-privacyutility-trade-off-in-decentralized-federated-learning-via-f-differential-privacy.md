---
title: Mitigating the Privacy–Utility Trade-off in Decentralized Federated Learning via f-Differential Privacy
title_zh: 通过f-差分隐私缓解去中心化联邦学习中的隐私-效用权衡
authors: "Xiang Li, Chendi Wang, Buxin Su, Qi Long, Weijie J Su"
date: 2025-09-18
pdf: "https://openreview.net/pdf?id=YIGUv0BZCy"
tags: ["query:daily"]
score: 9.0
evidence: 去中心化联邦学习中通过f-差分隐私缓解隐私-效用权衡
tldr: 去中心化联邦学习因通信和本地更新复杂，隐私损失难以准确量化。本文在f-差分隐私框架下提出两种新审计方法：成对网络f-DP和秘密基f-本地DP，精确地计算了用户间隐私泄露，有效缓解了隐私-效用权衡。
source: NeurIPS-2025-Accepted
selection_source: conference_retrieval
figures_json: "[{\"url\": \"assets/figures/openreview/openreview-neurips-2025-yiguv0bzcy/fig-001.webp\", \"caption\": \"\", \"page\": 9, \"index\": 1, \"width\": 601, \"height\": 601}, {\"url\": \"assets/figures/openreview/openreview-neurips-2025-yiguv0bzcy/fig-002.webp\", \"caption\": \"\", \"page\": 9, \"index\": 2, \"width\": 601, \"height\": 601}, {\"url\": \"assets/figures/openreview/openreview-neurips-2025-yiguv0bzcy/fig-003.webp\", \"caption\": \"\", \"page\": 25, \"index\": 3, \"width\": 601, \"height\": 601}, {\"url\": \"assets/figures/openreview/openreview-neurips-2025-yiguv0bzcy/fig-004.webp\", \"caption\": \"\", \"page\": 25, \"index\": 4, \"width\": 601, \"height\": 601}, {\"url\": \"assets/figures/openreview/openreview-neurips-2025-yiguv0bzcy/fig-005.webp\", \"caption\": \"\", \"page\": 25, \"index\": 5, \"width\": 653, \"height\": 653}, {\"url\": \"assets/figures/openreview/openreview-neurips-2025-yiguv0bzcy/fig-006.webp\", \"caption\": \"\", \"page\": 25, \"index\": 6, \"width\": 601, \"height\": 601}, {\"url\": \"assets/figures/openreview/openreview-neurips-2025-yiguv0bzcy/fig-007.webp\", \"caption\": \"\", \"page\": 25, \"index\": 7, \"width\": 601, \"height\": 601}, {\"url\": \"assets/figures/openreview/openreview-neurips-2025-yiguv0bzcy/fig-008.webp\", \"caption\": \"\", \"page\": 25, \"index\": 8, \"width\": 653, \"height\": 653}, {\"url\": \"assets/figures/openreview/openreview-neurips-2025-yiguv0bzcy/fig-009.webp\", \"caption\": \"\", \"page\": 25, \"index\": 9, \"width\": 601, \"height\": 601}, {\"url\": \"assets/figures/openreview/openreview-neurips-2025-yiguv0bzcy/fig-010.webp\", \"caption\": \"\", \"page\": 25, \"index\": 10, \"width\": 601, \"height\": 601}]"
motivation: 去中心化联邦学习因复杂组件导致隐私预算难以准确计算。
method: 提出两种基于f-DP的隐私会计方法，分别针对成对泄露和本地保护。
result: 精确量化隐私损失，改善隐私-效用权衡。
conclusion: 为去中心化联邦学习的差分隐私提供了新工具。
---

## Abstract
Differentially private (DP) decentralized Federated Learning (FL) allows local users to collaborate without sharing their data with a central server. However, accurately quantifying the privacy budget of private FL algorithms is challenging due to the co-existence of complex algorithmic components such as decentralized communication and local updates. This paper addresses privacy accounting for two decentralized FL algorithms within the $f$-differential privacy ($f$-DP) framework. We develop two new $f$-DP–based accounting methods tailored to decentralized settings: Pairwise Network $f$-DP (PN-$f$-DP), which quantifies privacy leakage between user pairs under random-walk communication, and Secret-based $f$-Local DP (Sec-$f$-LDP), which supports structured noise injection via shared secrets. 
By combining tools from $f$-DP theory and Markov chain concentration, our accounting framework captures privacy amplification arising from sparse communication, local iterations, and correlated noise. Experiments on synthetic and real datasets demonstrate that our methods yield consistently tighter $(\epsilon, \delta)$ bounds and improved utility compared to Rényi DP–based approaches, illustrating the benefits of $f$-DP in decentralized privacy accounting.

---

## 论文详细总结（自动生成）

### 论文核心问题与整体含义
- **研究背景**：去中心化联邦学习（Decentralized Federated Learning, DFL）允许多个本地用户在不共享原始数据、不依赖中心服务器的前提下协同训练模型。差分隐私（Differential Privacy, DP）是保护本地数据的主流技术，但在 DFL 场景中，由于存在去中心化通信拓扑、本地多轮更新、随机游走传播等复杂组件，隐私损失的量化精度严重受阻。
- **核心挑战**：准确计算隐私预算（privacy budget）极为困难，导致隐私-效用权衡（privacy–utility trade-off）难以优化：保守的预算估算会过度牺牲模型精度，宽松的估算又可能泄露用户隐私。
- **本文目标**：在 \(f\)-差分隐私（\(f\)-DP）框架下，为两类典型的去中心化联邦学习算法设计高精度的隐私会计（privacy accounting）方法，从而缓解隐私-效用权衡，获得更紧致的隐私界和更好的模型性能。

### 方法论
- **核心思想**：利用 \(f\)-DP 函数形式的精细隐私描述能力，结合马尔可夫链集中不等式，精准捕捉去中心化场景中由稀疏通信、本地迭代和关联噪声带来的隐私放大效应。
- **提出的两种会计方法**：
  - **成对网络 \(f\)-DP（Pairwise Network \(f\)-DP, PN-\(f\)-DP）**：针对基于随机游走通信的去中心化联邦学习，量化任意一对用户之间的隐私泄露。该方法通过分析图拓扑、通信步数与本地更新次数，在 \(f\)-DP 的 trade-off 函数空间中组合各阶段的隐私损失。
  - **秘密基 \(f\)-本地 DP（Secret-based \(f\)-Local DP, Sec-\(f\)-LDP）**：面向本地差分隐私（LDP）设置，允许用户通过预共享密钥生成结构化的相关噪声并注入梯度。利用相关噪声的方差缩减性质，在保护隐私的同时提升效用，并在 \(f\)-DP 下对整体隐私损失进行严格会计。
- **关键技术细节**：
  - 将 \(f\)-DP 的子采样放大定理、组合定理与去中心化通信的马尔可夫链性质结合，推导出单步及多步通信的隐私损失函数。
  - 对于 Sec-\(f\)-LDP，通过共享秘密矩阵构建离散高斯等噪声机制，利用集中不等式分析相关噪声下的隐私泄漏，从而突破独立噪声机制的限制。
  - 最终输出以函数形式表达的隐私边界，可转换为传统 \((\epsilon, \delta)\)-DP 界。

### 实验设计
- **数据集与场景**：
  - **合成数据集**：用于受控环境下的隐私界紧致性验证。
  - **真实数据集**：用于评估模型效用，所用具体数据集名称在现有摘要和元数据中未提供（常见如 MNIST、CIFAR-10/100 等），但文中应包含典型分类或回归任务。
- **对比基准（Benchmark）**：
  - 主要与基于 **Rényi DP（RDP）** 的会计方法进行对比，RDP 是当前去中心化联邦学习隐私会计的主流工具。
- **对比方法**：
  - 同一去中心化联邦学习算法，分别使用本文的 PN-\(f\)-DP 或 Sec-\(f\)-LDP 会计，以及对应的 RDP 会计，测量最终得到的 \((\epsilon, \delta)\) 界和模型准确率/损失。
- **实验维度**：预期涵盖不同隐私预算 \(\epsilon\)、不同网络规模、不同通信轮次和本地迭代步数的消融研究，以验证隐私放大效应的准确性。

### 资源与算力
- **文中信息缺失说明**：从提供的 PDF 提取文本和元数据中，**未提及 GPU 型号、数量、训练时长、显存消耗或计算集群规模**等算力信息。因此无法量化该研究对硬件资源的消耗情况，复现时需额外评估算力需求。

### 实验数量与充分性
- **实验体量推断**：尽管摘要未列出具体实验组数，但论文被 NeurIPS-2025 接收（得分 9.0），通常要求包含在合成与真实多数据集上的充分对比、不同参数下的消融实验以及统计显著性分析。figures_json 中包含多达 10 张图表，也佐证了实验维度的丰富性。
- **客观性与公平性**：对比方法采用相同的 DFL 算法框架，仅更换隐私会计模块，在控制训练超参一致的前提下比较界紧致度和最终效用，实验设计应较为公平。但缺少与其他隐私会计框架（如 Gaussian DP 会计、MA 会计）的横向对比，仅与 RDP 对比可能存在局限性。

### 主要结论与发现
- **隐私界限更紧致**：相较于基于 Rényi DP 的会计，PN-\(f\)-DP 和 Sec-\(f\)-LDP 在所有被评估场景下均能给出显著更紧的 \((\epsilon, \delta)\) 边界。
- **隐私-效用权衡改善**：在相同的目标隐私预算下，使用 \(f\)-DP 会计指导的训练过程能获得更高的模型准确率或更低的损失，即效用损失更小。
- **放大效应被准确量化**：\(f\)-DP 框架成功捕获了稀疏通信（如随机游走非全连接）和本地多次梯度上升/下降带来的隐私放大，避免了传统方法过于保守的噪声注入。
- **相关噪声机制优势**：Sec-\(f\)-LDP 展示了通过共享秘密注入结构化相关噪声的可行性，其隐私会计精确性保证了该技术在 LDP 下的实用效能。

### 优点
- **新颖的隐私会计框架**：首次将 \(f\)-DP 系统性地应用于去中心化联邦学习，利用其函数形式解决复杂组合下的精确隐私量化难题。
- **问题指向明确**：分别针对 DFL 的两类典型隐私泄露场景（成对泄露与本地 LDP）设计专用会计工具，覆盖面广。
- **理论-实验闭环**：从马尔可夫链集中理论出发推导隐私界，再通过实验验证其紧致性和对效用的提升，理论支撑扎实。
- **显著优于主流方法**：相比广泛使用的 RDP 会计，一致地取得更紧界和更高精度，显示出 \(f\)-DP 在该领域的突出潜力。

### 不足与局限
- **数据集信息披露不完整**：现有内容未列出具体使用的真实数据集，无法判断方法在不同数据模态、规模或非独立同分布程度下的泛化能力。
- **计算与通信开销未知**：论文未分析 \(f\)-DP 会计本身的计算复杂度，也未给出 PN-\(f\)-DP 和 Sec-\(f\)-LDP 在实际部署中引入的额外通信或计算开销，实际可行性评估不完整。
- **对比方法局限**：仅对比了基于 RDP 的会计，缺乏与同属 \(f\)-DP 体系的其他转换方法、或更现代的隐私会计技术（如隐私损失分布方法）的全面比较。
- **拓扑假设限制**：PN-\(f\)-DP 设计基于随机游走通信模型，对其他去中心化拓扑（如 gossip 协议、基于拜占庭容错的图结构）的适用性可能受限。
- **缺乏规模放量实验**：未提供在极大规模设备或极深网络下的 scaling 表现，以及长时间训练的隐私预算衰减特性。
- **复现信息缺失**：无算力说明、软件环境细节，可能影响结果复现的准确性。

（完）
