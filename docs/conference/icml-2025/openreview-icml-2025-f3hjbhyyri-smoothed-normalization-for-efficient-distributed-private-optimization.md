---
title: Smoothed Normalization for Efficient Distributed Private Optimization
title_zh: 通过平滑归一化实现高效分布式隐私优化
authors: "Egor Shulgin, Sarit Khirirat, Peter Richtárik"
date: 2025-01-16
pdf: "https://openreview.net/pdf?id=F3hjbhyyRI"
tags: ["query:daily"]
score: 10.0
evidence: 平滑归一化用于分布式隐私优化
tldr: 针对分布式非凸优化中缺乏差分隐私方法的问题，提出用平滑归一化替代传统裁剪来限制参与方贡献，结合误差反馈实现高效隐私保护优化，填补了理论空白。
source: ICML-2025-Rejected-Public
selection_source: conference_retrieval
figures_json: "[{\"url\": \"assets/figures/openreview/openreview-icml-2025-f3hjbhyyri/fig-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 782, \"height\": 488, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-icml-2025-f3hjbhyyri/fig-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 850, \"height\": 676, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-icml-2025-f3hjbhyyri/fig-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 895, \"height\": 707, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-icml-2025-f3hjbhyyri/fig-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 863, \"height\": 548, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-icml-2025-f3hjbhyyri/fig-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 888, \"height\": 549, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-icml-2025-f3hjbhyyri/fig-006.webp\", \"caption\": \"\", \"page\": 0, \"index\": 6, \"width\": 862, \"height\": 538, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-icml-2025-f3hjbhyyri/fig-007.webp\", \"caption\": \"\", \"page\": 0, \"index\": 7, \"width\": 1767, \"height\": 718, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-icml-2025-f3hjbhyyri/fig-008.webp\", \"caption\": \"\", \"page\": 0, \"index\": 8, \"width\": 938, \"height\": 753, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-icml-2025-f3hjbhyyri/fig-009.webp\", \"caption\": \"\", \"page\": 0, \"index\": 9, \"width\": 1767, \"height\": 707, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-icml-2025-f3hjbhyyri/fig-010.webp\", \"caption\": \"\", \"page\": 0, \"index\": 10, \"width\": 1776, \"height\": 703, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-icml-2025-f3hjbhyyri/fig-011.webp\", \"caption\": \"\", \"page\": 0, \"index\": 11, \"width\": 878, \"height\": 700, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-icml-2025-f3hjbhyyri/fig-012.webp\", \"caption\": \"\", \"page\": 0, \"index\": 12, \"width\": 885, \"height\": 569, \"label\": \"Figure\"}]"
tables_json: "[{\"url\": \"assets/tables/openreview/openreview-icml-2025-f3hjbhyyri/table-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 1595, \"height\": 331, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-icml-2025-f3hjbhyyri/table-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 723, \"height\": 471, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-icml-2025-f3hjbhyyri/table-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 965, \"height\": 473, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-icml-2025-f3hjbhyyri/table-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 703, \"height\": 470, \"label\": \"Table\"}]"
motivation: 现有分布式DP方法缺少对光滑非凸问题的支持，且裁剪操作破坏收敛性。
method: 采用平滑归一化控制更新范数，并与误差反馈机制结合。
result: 实现了分布式非凸优化的差分隐私保护，且具有高效收敛性。
conclusion: 平滑归一化是分布式隐私优化中裁剪的有效替代方案。
---

## Abstract
Federated learning enables training machine learning models while preserving the privacy of participants. Surprisingly, there is no differentially private distributed method for smooth non-convex optimization problems. The reason is that standard privacy techniques require bounding the participants' contributions, usually enforced via *clipping* of the updates. Existing literature typically ignores the effect of clipping by assuming the boundedness of gradient norms or analyzes distributed algorithms with clipping but ignores DP constraints. In this work, we study an alternative approach via *smoothed normalization* of the updates motivated by its favorable performance in the centralized setting. By integrating smoothed normalization with an error-feedback mechanism, we design a new distributed algorithm $\alpha$-${\sf NormEC}$. We prove that our method achieves a superior convergence rate over prior works. By extending $\alpha$-${\sf NormEC}$ to the DP setting, we obtain the first differentially private distributed optimization algorithm with provable convergence guarantees. Finally, we support our theoretical findings with experiments on practical machine learning problems.

---

## 论文详细总结（自动生成）

好的，以下是基于所提供论文的结构化中文总结。

### 1. 论文的核心问题与研究动机

*   **核心问题**：当前缺乏针对**光滑非凸优化问题**的**差分隐私（DP）分布式方法**。
*   **研究动机与背景**：
    *   联邦学习（FL）允许多方协作训练模型而不共享原始数据，但生成的全局模型仍可能泄露参与方的隐私信息。
    *   差分隐私（DP）是提供理论隐私保障的标准技术，其核心是**限制参与方贡献的敏感度**。
    *   限制敏感度的常用方法是**梯度裁剪（Clipping）**，但现有研究普遍存在两大问题：
        1.  **忽略裁剪偏差**：通过假设梯度范数有界来回避裁剪带来的收敛性影响。
        2.  **理论空白**：尚无分布式DP梯度方法能在标准假设下（无梯度有界假设）被证明适用于光滑非凸场景。
    *   此外，裁剪阈值的手动调优计算成本高，且可能导致额外隐私损失。

### 2. 论文提出的方法论

*   **核心思想**：采用**平滑归一化（Smoothed Normalization）** 替代梯度裁剪，并将其与**误差反馈（Error Feedback，EF）机制**（具体为EF21）结合，设计出一个名为 **α-NormEC** 的新分布式算法。
*   **关键技术细节**：
    *   **平滑归一化算子（Normα(g)）**：
        *   **定义**：`Normα(g) := g / (α + ||g||)`，其中 `α ≥ 0`。
        *   **核心性质**：
            1.  **范数有界**：`||Normα(g)|| ≤ 1`，天然满足DP对敏感度的要求，无需手动设置裁剪阈值。
            2.  **收缩性（Contractive Property）**：类似于有偏压缩算子，保证了与误差反馈机制结合时的收敛性。
    *   **算法流程 (α-NormEC)**：
        1.  在每个通信轮次 `k`，客户端 `i` 计算本地梯度 `∇fi(xk)`。
        2.  应用平滑归一化到误差向量上：`Δki = Normα(∇fi(xk) - gki)`。
        3.  更新本地记忆向量：`gk+1 i = gk i + β * Δk i`，其中 `β` 是步长参数。
        4.  **非隐私版本**：客户端直接上传 `Δk i`。
        5.  **隐私版本 (DP-α-NormEC)**：客户端上传加入高斯噪声的 `Δk i + zk i`。
        6.  服务器聚合更新全局记忆向量和模型参数 `xk+1`。
*   **理论基础**：
    *   论文证明了 **α-NormEC** 在非隐私设置下，对光滑非凸问题能实现 **O(1/√K)** 的最优收敛速率（`K`为迭代次数）。
    *   通过将该方法扩展到DP设置，获得了**首个在标准假设下（无梯度有界假设）具备可证明收敛保证的DP分布式优化算法**。

### 3. 实验设计

*   **数据集与场景**：使用 **CIFAR-10** 数据集，在 **ResNet20** 模型上进行图像分类任务（典型的非凸优化问题）。
*   **对比方法**：
    *   **非隐私设置**：
        *   **DP-SGD（带平滑归一化）**：将α-NormEC与不采用误差反馈机制、直接进行平滑归一化的分布式DP-SGD进行对比，以验证误差补偿（EC）的效果。
        *   **Clip21**：与同样基于EF21机制但使用裁剪算子的方法进行比较。
    *   **隐私设置**：
        *   主要展示了**DP-α-NormEC**在不同超参数下的性能。

### 4. 资源与算力

*   **论文明确提及**：实验在配备**单块NVIDIA GeForce RTX 3090 GPU**的机器上运行。
*   **训练时长**：所有方法均在 **300个通信轮次**下进行训练。

### 5. 实验数量与充分性

*   **实验数量**：论文进行了多组实验来验证其观点，包括：
    1.  **超参数敏感性分析**：在非隐私设置下，研究了参数 `α`（平滑参数）和 `β`（步长参数）对α-NormEC性能的影响，测试了 `α ∈ {0.01, 0.1, 1.0}` 和 `β ∈ {0.01, 0.1, 1.0, 10.0}` 的交叉组合。
    2.  **消融实验**：
        *   对比了有无误差补偿（EC）机制的性能差异。
        *   研究了服务器端归一化对性能的影响。
    3.  **方法对比实验**：在非隐私场景下，将α-NormEC与Clip21进行了性能对比。
    4.  **隐私设置性能分析**：探索了DP-α-NormEC在不同 `β` 值下的表现。
*   **充分性与公平性**：
    *   实验覆盖了非隐私和隐私两种场景，并设置了多组超参数和消融研究，**设计较为全面**。
    *   对比时选择了核心相关的基线方法（DP-SGD, Clip21），**对比是客观公平的**。
    *   实验现象与理论发现（如EC机制的关键作用、对超参数的鲁棒性）相互印证，增强了结论的可信度。

### 6. 主要结论与发现

*   **α-NormEC收敛性优越**：在非隐私环境下，α-NormEC实现了 **O(1/√K)** 的收敛速率，其收敛系数优于Clip21，且超参数更易实现。
*   **解决了DP分布式优化的理论空白**：DP-α-NormEC是首个在不依赖梯度有界等强假设下，为光滑非凸问题提供可证明收敛保证的DP分布式算法。
*   **实证鲁棒性**：
    *   α-NormEC对超参数 `α` 和 `β` 具有稳健的收敛性能。
    *   误差补偿（EC）机制显著提升了分布式梯度方法的收敛速度和稳定性，尤其是在有挑战的参数设置下。
    *   在隐私设置中，较小的 `β` 值能带来更好的性能，因为更大的 `β` 需要注入更多噪声以满足隐私预算。

### 7. 优点

*   **理论创新性强**：解决了DP分布式优化中的一个重要理论空白，首次为光滑非凸问题提供了无需强假设的收敛保证。
*   **方法设计巧妙**：将平滑归一化视为“收缩算子”，使其能与EF21误差反馈框架自然结合，既解决了裁剪的收敛难题，又规避了裁剪阈值调参的困扰。
*   **实用性强**：超参数易于实现，性能对其较为鲁棒，有潜力应用于现实世界的FL任务。
*   **实验验证扎实**：通过系统的实验（敏感性分析、消融研究、方法对比），清晰地验证了理论和方法的优势。

### 8. 不足与局限

*   **实验规模有限**：
    *   仅在CIFAR-10/ResNet20这一种任务上验证，模型和数据集规模较小，未在更大规模（如ImageNet）或不同模态（如NLP任务）上检验其扩展性。
    *   实验全部基于全客户端参与和全梯度（非随机梯度）设置，未覆盖FL中常见的**客户端部分参与**和**本地多步SGD**（即FedAvg风格）的场景。
*   **理论假设限制**：目前的收敛理论要求所有客户端函数的平滑系数 `Li` 需全局已知并用于设置步长，这在实际联邦场景中可能难以满足。
*   **未与其他隐私技术比较**：实验部分仅与基础的DP-SGD和Clip21比较，未与更先进的自适应裁剪技术（如adaptive quantile clipping）在隐私设置下进行对比。

（完）
