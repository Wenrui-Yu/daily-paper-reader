---
title: "DMM: Distributed Matrix Mechanism for Differentially-Private Federated Learning Based on Constant-Overhead Linear Secret Resharing"
title_zh: DMM：基于常数开销线性秘密再共享的分布式矩阵机制差分隐私联邦学习
authors: "Alexander Bienstock, Ujjwal Kumar, Antigoni Polychroniadou"
date: 2025-05-01
pdf: "https://openreview.net/pdf?id=Nv6mOSqUVA"
tags: ["query:daily"]
score: 10.0
evidence: 提出分布式矩阵机制，结合常数开销秘密再共享，实现差分隐私联邦学习
tldr: 针对联邦学习中心差分隐私效用高但隐私弱、分布式差分隐私隐私强但效用低的矛盾，本文提出分布式矩阵机制DMM。通过常数开销的线性秘密再共享协议，在保护分布式差分隐私的同时利用矩阵机制提升效用，并支持客户端动态参与。实验表明DMM取得了隐私与效用的最佳平衡，为隐私保护联邦学习提供了新范式。
source: ICML-2025-Accepted
selection_source: conference_retrieval
figures_json: "[{\"url\": \"assets/figures/openreview/openreview-icml-2025-nv6mosquva/fig-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 1735, \"height\": 521, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-icml-2025-nv6mosquva/fig-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 735, \"height\": 489, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-icml-2025-nv6mosquva/fig-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 1685, \"height\": 613, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-icml-2025-nv6mosquva/fig-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 742, \"height\": 490, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-icml-2025-nv6mosquva/fig-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 1510, \"height\": 972, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-icml-2025-nv6mosquva/fig-006.webp\", \"caption\": \"\", \"page\": 0, \"index\": 6, \"width\": 1492, \"height\": 970, \"label\": \"Figure\"}]"
tables_json: "[{\"url\": \"assets/tables/openreview/openreview-icml-2025-nv6mosquva/table-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 874, \"height\": 225, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-icml-2025-nv6mosquva/table-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 876, \"height\": 223, \"label\": \"Table\"}]"
motivation: 中心差分隐私效用高隐私弱，分布式差分隐私隐私强效用低，需兼顾两者。
method: 提出DMM，结合分布式矩阵机制与常数开销秘密再共享协议。
result: 实现分布式差分隐私与矩阵机制高效用的结合，支持动态参与。
conclusion: 为联邦学习提供了隐私性与效用兼得的最佳方案。
---

## Abstract
Federated Learning (FL) solutions with central Differential Privacy (DP) have seen large improvements in their utility in recent years arising from the matrix mechanism, while FL solutions with distributed (more private) DP have lagged behind. In this work, we introduce the distributed matrix mechanism to achieve the best-of-both-worlds; better privacy of distributed DP and better utility from the matrix mechanism. We accomplish this using a novel cryptographic protocol that securely transfers sensitive values across client committees
of different training iterations with constant communication overhead. This protocol accommodates the dynamic participation of users required by FL, including those that may drop out from the computation. We provide experiments which show that our mechanism indeed significantly improves the utility of FL models compared to previous distributed DP mechanisms, with little added overhead.

---

## 论文详细总结（自动生成）

好的，以下是根据您提供的论文内容生成的结构化中文总结。

### 1. 论文的核心问题与整体含义
*   **研究背景**：联邦学习在保护用户隐私方面面临挑战，差分隐私是主要的隐私度量标准。
*   **核心矛盾**：当前存在两种差分隐私范式的权衡困境。
    *   **中心差分隐私**：效用高（得益于矩阵机制可关联噪声），但需要信任中心服务器，隐私性相对较弱。
    *   **分布式差分隐私**：隐私性强（无需信任服务器），但噪声由客户端独立添加，无法跨轮次关联，效用远低于中心差分隐私。
*   **研究动机与目标**：本文旨在打破这一僵局，提出一种能兼顾“分布式DP的强隐私”与“中心DP矩阵机制的高效用”的解决方案，实现“两全其美”。

### 2. 论文提出的方法论
*   **核心思想**：提出 **分布式矩阵机制**。该机制允许客户端的噪声和梯度在跨训练轮次的不同委员会之间按矩阵机制的要求进行线性组合，从而引入噪声关联，提升模型最终效用。
*   **关键技术：常数开销线性秘密再共享协议**
    *   **问题**：在动态变化的客户端委员会间安全传递秘密份额，若使用朴素方法会导致 `O(n²)` 的通信开销，在联邦学习场景下不可行。
    *   **解决方案**：设计了一种新颖的密码学协议 **LRP**。它利用**打包秘密共享**技术，通过巧妙的批量处理，将跨委员会的份额传递通信开销降至**常数级 `O(1)`**（每个秘密），极大地提升了效率。
*   **算法流程**：
    1.  **初始化**：当前轮次的客户端接收到来自前一轮客户端的梯度与噪声的打包秘密份额。
    2.  **本地计算与分享**：客户端计算本地梯度、采样噪声，并生成其秘密份额分发给本委员会的其他成员。
    3.  **线性组合**：客户端将历史所有轮次的梯度份额与噪声份额，按照公开的矩阵分解（`A = BC`）进行线性组合，得到带有关联噪声的聚合梯度份额 `dAX`。
    4.  **结果重构**：将组合后的份额发送给服务器，服务器重构出带噪的模型更新。
    5.  **份额再共享**：客户端将其持有的当前及历史份额通过 **LRP** 协议再共享给下一轮次的委员会成员，确保流程连续。

### 3. 实验设计
*   **数据集与场景**：
    *   **Stack Overflow 下一个词预测**：大规模文本数据集，包含342,477个用户。
    *   **Federated EMNIST**：手写字符图像分类数据集，包含3,400个客户端。
*   **对标基准**：
    *   **分布式差分隐私方案**：当前最优的**分布式离散高斯机制**。
    *   **中心差分隐私方案**：采用最优矩阵分解（BandMF）和 Honaker 在线矩阵分解的中心化矩阵机制。
*   **对比方法**：实验中对比了本文提出的 **DMM**（分别使用最优和Honaker在线矩阵分解）与上述分布式和中心化DP基准方法的性能。

### 4. 资源与算力
*   论文中明确指出实验是在一台配备 **AMD EPYC 7R32 处理器和一块 A10G GPU** 的机器上运行的。除此外，未提及其他算力资源。

### 5. 实验数量与充分性
*   **实验数量**：主要实验覆盖了**两个标准数据集**，并在每个数据集上针对**多种隐私预算（`ε`）** 设置了多组实验。
*   **实验充分性评估**：
    *   **充分性**：实验设计遵循了先前工作的标准设置，对比了不同隐私范式下最具代表性的方法，并提供了详尽的效率（计算与通信开销）对比表格，能够有力支撑论文的核心论点。
    *   **客观公平性**：实验是在公开的基准数据集和代码库上进行，对比了公认的最优方法，具有较强的客观性和公平性。

### 6. 论文的主要结论与发现
*   **效用显著提升**：在相同隐私预算下，**DMM 的性能显著优于先前的分布式DP方法**（如在Stack Overflow任务上准确率提升5-6个百分点），达到了与先进中心DP方法相媲美甚至更好的水平。
*   **高效率和低开销**：DMM带来的额外计算和通信开销很小。与之前的分布式DP方案相比，使用高效的Honaker矩阵分解时，DMM增加的客户端计算时间不到10秒，通信量增加不到10 MB，极具实用性。

### 7. 优点
*   **创新性强**：首次在动态客户端的联邦学习场景下实现了分布式噪声关联，成功打破了分布式DP与矩阵机制之间的壁垒。
*   **技术突破**：提出的 **LRP 协议**是实现高效分布式矩阵机制的关键，将跨委员会秘密再共享的开销从不可行的 `O(n²)` 降至常数级，是密码学技术在联邦学习中的一次巧妙应用。
*   **实用价值高**：实验不仅展示了模型效用的提升，还详细分析了计算和通信开销，证明了该方法在实际系统中的可行性。

### 8. 不足与局限
*   **矩阵分解效率**：实验表明，效用最优的矩阵分解会显著增加通信和计算开销，而高效的Honaker在线分解虽然开销小，但效用略有下降。未来需设计更优的、能平衡效用与效率的矩阵分解策略。
*   **敌手模型**：与另一并发工作相比，本文的协议虽然能抵抗恶意敌手，但其基于秘密共享的技术路线在通信效率上可能低于基于密码学假设的加密方案。
*   **实现细节依赖**：效率表现依赖于参数选择（如打包参数 `k` 和容忍的恶意方比例 `μ`），实际部署时需仔细调优。

（完）
