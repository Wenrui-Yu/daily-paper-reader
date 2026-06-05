---
title: Efficient Federated Learning against Byzantine Attacks and Data Heterogeneity via Aggregating Normalized Gradients
title_zh: 通过聚合归一化梯度实现抗拜占庭攻击和数据异质性的高效联邦学习
authors: "Shiyuan Zuo, Xingrun Yan, Rongfei Fan, Li Shen, Puning Zhao, Jie Xu, Han Hu"
date: 2025-09-18
pdf: "https://openreview.net/pdf?id=Iyn0D3cFvt"
tags: ["query:daily"]
score: 8.0
evidence: 归一化梯度聚合对抗拜占庭攻击的联邦学习
tldr: 联邦学习易受拜占庭攻击，现有鲁棒方法计算开销大。Fed-NGA通过计算各客户端归一化梯度的加权平均进行聚合，时间复杂度仅O(pM)，在保证鲁棒性的同时显著加速训练。
source: NeurIPS-2025-Accepted
selection_source: conference_retrieval
motivation: 现有拜占庭鲁棒方法计算开销高，训练效率低。
method: 提出Fed-NGA，计算归一化梯度加权平均进行聚合。
result: 时间复杂度O(pM)，兼顾鲁棒性与效率。
conclusion: 为联邦学习提供了一种简单高效的防御机制。
---

## Abstract
Federated Learning (FL) enables multiple clients to collaboratively train models without sharing raw data, but is vulnerable to Byzantine attacks and data heterogeneity, which can severely degrade performance. Existing Byzantine-robust approaches tackle data heterogeneity, but incur high computational overhead during gradient aggregation, thereby slowing down the training process. To address this issue, we propose a simple yet effective Federated Normalized Gradients Algorithm (Fed-NGA), which performs aggregation by merely computing the weighted mean of the normalized gradients from each client. This approach yields a favorable time complexity of $\mathcal{O}(pM)$, where $p$ is the model dimension and $M$ is the number of clients. We rigorously prove that Fed-NGA is robust to both Byzantine faults and data heterogeneity. For non-convex loss functions, Fed-NGA achieves convergence to a neighborhood of stationary points under general assumptions, and further attains zero optimality gap under some mild conditions, which is an outcome rarely achieved in existing literature. In both cases, the convergence rate is $\mathcal{O}(1/T^{\frac{1}{2} - \delta})$, where $T$ denotes the number of iterations and $\delta \in (0, 1/2)$. Experimental results on benchmark datasets confirm the superior time efficiency and convergence performance of Fed-NGA over existing methods.

---

## 论文详细总结（自动生成）

好的，以下是基于论文内容生成的详细中文总结。

### 1. 论文的核心问题与整体含义

*   **研究背景**：联邦学习允许客户端在不共享原始数据的情况下协作训练模型，但面临两大挑战：
    *   **拜占庭攻击**：恶意客户端可发送任意错误信息破坏模型训练。
    *   **数据异质性**：各客户端数据为非独立同分布，导致模型收敛困难。
*   **核心问题**：现有拜占庭鲁棒的聚合方法虽能处理数据异质性，但其聚合过程计算开销巨大，严重拖慢了训练效率。
*   **整体含义**：本文旨在提出一种新算法，以极低的计算复杂度，同时抵御拜占庭攻击和数据异质性，实现高效、鲁棒的联邦学习。

### 2. 论文提出的方法论

*   **核心思想**：对客户端上传的梯度向量进行归一化处理，再计算其加权平均，以此作为全局模型的更新方向。
*   **关键技术细节**：
    *   **算法名称**：联邦归一化梯度算法。
    *   **算法流程**：
        1. **本地更新**：诚实客户端计算本地梯度并上传；拜占庭客户端可上传任意恶意向量。
        2. **聚合与广播**：服务器接收所有向量后，对每个向量进行归一化，即除以自身范数（`g_t^m / ||g_t^m||`）。然后，计算所有归一化向量的加权平均，得到聚合梯度 `g_t`。
        3. **模型更新**：使用聚合梯度 `g_t` 和学习率 `η_t` 更新全局模型参数 `w_{t+1} = w_t - η_t * g_t`。
    *   **计算复杂度**：该归一化聚合的过程时间复杂度仅为 `O(pM)`，其中 `p` 是模型维度，`M` 是客户端总数，显著低于已有方法。
*   **理论保证**：
    *   **一般假设**：在非凸损失函数下，算法能收敛到稳定点的一个邻域内。
    *   **温和条件**：在一些更温和的条件下，首次证明了算法能以零最优间隙收敛到真实稳定点。
    *   **收敛速度**：两种情况下收敛速度均为 `O(1/T^{1/2 - δ})`。

### 3. 实验设计

*   **数据集与场景**：
    *   **数据集**：TinyImageNet、CIFAR10、MNIST。
    *   **数据异质性**：采用狄利克雷分布划分数据，通过浓度参数 `β` 控制异质性程度。
    *   **模型**：MobileNetV3、LeNet、多层感知机。
*   **对比方法**：
    *   **非鲁棒基准**：FedAvg。
    *   **鲁棒基准**：Median, Krum, Geometric Median, MCA, CClip。
*   **攻击类型**：无攻击、高斯攻击、同值攻击、符号翻转攻击、LIE攻击、FoE攻击。

### 4. 资源与算力

*   **硬件配置**：实验使用4块NVIDIA RTX A6000 GPU和1个AMD 7702 CPU。
*   **软件环境**：Ubuntu 20.04, PyTorch 2.2.2。
*   **训练时长**：论文未明确说明完整的模型训练总耗时，但报告了聚合算法本身的运行时间，凸显了Fed-NGA在此环节的高效性。例如，在CIFAR10上，Fed-NGA聚合耗时约0.05秒，而其它鲁棒方法至少是其100倍以上。

### 5. 实验数量与充分性

*   **实验数量充足**：实验覆盖了3个不同复杂度的数据集、3种模型、3个数据异质性等级、5种拜占庭攻击类型以及多个攻击比例，构成了一个全面且多维度的评估体系。
*   **实验公平客观**：
    *   **公平性**：对比了7种算法，包括经典非鲁棒方法和近年先进的鲁棒方法。为所有方法针对性地调整了学习率，确保了对比的公平性。
    *   **充分性**：不仅提供了最终准确率表格，还展示了训练过程的准确率曲线和详细的聚合耗时对比图，从性能、鲁棒性和效率三个维度进行了充分论证。

### 6. 论文的主要结论与发现

*   **卓越的鲁棒性**：Fed-NGA在各类拜占庭攻击下均表现出色，尤其在FoE攻击下，当其他基线方法失效时，它仍能保持稳定收敛和高准确率。
*   **显著的高效性**：在聚合阶段的运行时间远低于其他鲁棒聚合算法，通常仅为它们的几十分之一甚至几百分之一，验证了其 `O(pM)` 的低时间复杂度优势。
*   **良好的适应性**：在不同程度的数据异质性下，Fed-NGA的性能虽有波动但相对稳定，表现优于或持平于基线方法。

### 7. 优点

*   **方法论简洁高效**：提出的Fed-NGA算法思想简单——仅通过归一化和加权平均实现聚合，但效果显著，使计算复杂度降至最低。
*   **理论创新性强**：首次为拜占庭鲁棒联邦学习算法证明了在温和条件下达到零最优间隙的可能性，这是重要的理论贡献。
*   **实验全面扎实**：实验设计考虑周全，覆盖多种攻击、多类数据集和模型，并与多种主流方法对比，结论极具说服力。

### 8. 不足与局限

*   **理论假设的局限性**：论文承认，保证零最优间隙需要依赖更一般的假设，文中虽然首次证明了这一可能，但该结论是在“一些温和条件”下成立的，其应用的普适性有待进一步拓宽。
*   **对新型攻击的防御**：在某些攻击类型（如Same-value, Sign-flip）下，尤其是攻击比例较高时，虽然仍能工作，但性能出现了比较明显的下降。
*   **代码未开源**：论文在设备、环境方面提供了信息，但目前并未提供开源代码。

（完）
