---
title: "Locally Optimal Private Sampling: Beyond the Global Minimax"
title_zh: 局部最优隐私采样：超越全局极小极大
authors: "Hrad Ghoukasian, Bonwoo Lee, Shahab Asoodeh"
date: 2025-09-18
pdf: "https://openreview.net/pdf?id=mImUMLEpdf"
tags: ["query:daily"]
score: 9.0
evidence: 局部差分隐私采样局部优化隐私-效用
tldr: 局部差分隐私下数据生成需在隐私与效用间平衡。本文从局部视角研究采样问题，刻画固定分布邻域内的局部极小极大误差精确值，表明该误差依赖分布和隐私水平，且局部方法在某些分布上优于全局最优，为个性化隐私数据生成提供了更精细的理论工具。
source: NeurIPS-2025-Accepted
selection_source: conference_retrieval
motivation: 全局极小极大无法捕捉分布局部特性，需实例自适应隐私采样。
method: 研究固定分布邻域内的局部极小极大误差，给出精确刻画。
result: 局部误差结构依赖隐私水平和分布，可实现超越全局最优。
conclusion: 为个性化隐私保护生成提供理论支撑。
---

## Abstract
We study the problem of sampling from a distribution under local differential privacy (LDP). Given a private distribution $P \in \mathcal{P}$, the goal is to generate a single sample from a distribution that remains close to $P$ in $f$-divergence while satisfying the constraints of LDP. This task captures the fundamental challenge of producing realistic-looking data under strong privacy guarantees. While prior work by Park et al. (NeurIPS'24) focuses on global minimax-optimality across a class of distributions, we take a local perspective. Specifically, we examine the minimax error in a neighborhood around a fixed distribution $P_0$, and characterize its exact value, which depends on both $P_0$ and the privacy level. Our main result shows that the local minimax error is determined by the global minimax error when the distribution class $\mathcal{P}$ is restricted to a neighborhood around $P_0$. To establish this, we (1) extend previous work from pure LDP to the more general functional LDP framework, and (2) prove that the globally optimal functional LDP sampler yields the optimal local sampler when constrained to distributions near $P_0$. Building on this, we also derive a simple closed-form expression for the locally minimax-optimal samplers which does not depend on the choice of $f$-divergence. We further argue that this local framework naturally models private sampling with public data, where the public data distribution is represented by $P_0$. In this setting, we empirically compare our locally optimal sampler to existing global methods, and demonstrate that it consistently outperforms global minimax samplers.

---

## 论文详细总结（自动生成）

好的，这是对论文《局部最优隐私采样：超越全局极小极大》的结构化总结。

### 1. 论文核心问题与整体含义

*   **研究背景**：该论文聚焦于**局部差分隐私（LDP）** 下的采样问题。用户（客户端）持有私有分布 $P$，希望在不依赖可信中心的条件下，生成一个既保护原始数据隐私、又能保留其统计特征的样本。
*   **核心问题**：现有工作（如 Park et al., 2024）追求的“全局极小极大最优性”，旨在寻找一个采样器，使其在整个分布类上的**最差情况表现最优**。然而，这是一种悲观的策略，因为真实的数据分布很少会是最差情况。
*   **研究动机**：本文提出了一个**局部极小极大**框架。给定一个可能代表公开数据的固定分布 $P_0$，目标不再是保护所有可能的分布，而是保护以 $P_0$ 为中心的一个邻域 $\mathcal{N}_\gamma(P_0)$ 内的所有分布。这更贴近实际，并能利用公开数据信息来提升效用。
*   **整体含义**：论文旨在超越悲观的全局最优解，为“个性化”或“有公开数据辅助”的隐私采样场景，提供一种效用更高、理论保证更精细的局部最优采样方法。

### 2. 方法论：核心思想与技术细节

*   **核心思想 - 局部极小极大风险**：定义了一个以固定分布 $P_0$ 的邻域 $\mathcal{N}_\gamma(P_0)$ 为保护范围的极小极大风险，并通过**零 $E_\gamma$-散度邻域**（即似然比几乎处处在 $[1/\gamma, \gamma]$ 内）来刻画该邻域。
*   **关键理论构建**：
    1.  **从纯 LDP 推广到函数式 LDP (fLDP)**： 论文首先将 Park et al. (2024) 的全局极小极大框架从纯 LDP 扩展到更通用的函数式 LDP，该框架统一了 $\varepsilon$-LDP、$(\varepsilon, \delta)$-LDP 和高斯差分隐私（GLDP）等不同隐私定义。
    2.  **全局与局部的桥梁**：证明了**局部极小极大风险等价于将分布类限制在邻域 $\mathcal{N}_\gamma(P_0)$ 内的全局极小极大风险**。这意味着，求解局部问题，只需将全局最优解中的“分布类”参数替换为邻域参数即可。
    3.  **最优采样器导出**：
        *   **通用fLDP局部最优采样器**：通过代入 $P_0$ 邻域的参数，可直接从全局 fLDP 最优采样器的定理中推出一个“线性采样器”，其形式为 $Q(P) = \lambda P + (1-\lambda)P_0$。
        *   **纯LDP点对点更优采样器**：在纯 LDP 下，本文推导出一个**非线性的、性能更优的采样器**。给定输入分布 $P$，该采样器的输出密度由一个裁剪操作定义：$q(x) = \text{clip}(\frac{1}{r_P}p(x); \frac{\gamma+1}{\gamma+e^\varepsilon}p_0(x), \frac{(\gamma+1)e^\varepsilon}{\gamma+e^\varepsilon}p_0(x))$。此操作将 $P$ 的密度“投影”到一个满足 LDP 约束的“软子”上，比线性混合能更好地保真。
    4.  **最优解特性**：重要的是，所有推导出的极小极大最优采样器均**不依赖于 $f$-散度的具体选择**（如KL散度、TV距离等），具有普适性。

### 3. 实验设计

*   **实验场景**：
    *   **有限样本空间**：类别数 $k$ 为 10, 20, 100，以均匀分布为参考。
    *   **连续样本空间（1维和2维）**：以拉普拉斯分布混合作为客户端输入分布。1维实验中，定义 $\tilde{\mathcal{P}}_{\text{local}} = \tilde{\mathcal{P}}_{1/3, 3, h_L}$ 和 $\tilde{\mathcal{P}}_{\text{global}} = \tilde{\mathcal{P}}_{1/9, 9, h_L}$。
*   **对比基准与方法**：
    *   **基准**：Park et al. (2024) 提出的**全局极小极大最优采样器**。
    *   **方法**：本文提出的**局部极小极大最优采样器**（纯 LDP 下为非线性采样器）。
*   **评估指标**：评估采样器输出的私有化分布与原始分布之间的**最差情况 $f$-散度**，具体包含了 KL 散度、总变分距离（TV）和平方海林格距离（Sq. Hel）。
*   **隐私设置**：对比了在不同隐私预算下的表现，包括 $\varepsilon$-LDP ($\varepsilon \in \{0.1, 0.5, 1, 2\}$) 和 $\nu$-GLDP ($\nu \in \{0.1, 0.5, 1, 2\}$)。

### 4. 资源与算力

*   论文中明确提供了实验的计算资源和运行时间。
    *   **硬件环境**：一台运行 Ubuntu 22.04.4 LTS 的机器，配备 Intel(R) Xeon(R) CPU @ 2.20GHz 和 16GB RAM。**没有提及使用 GPU**，算法运行主要在 CPU 上。
    *   **运行时长**：
        *   生成论文**图1（2D可视化）** 的采样过程约需 **300 秒**。
        *   连续空间的 1D 拉普拉斯实验（生成图4），并行运行 4 个不同 $\varepsilon$ 的任务，总耗时约 **600 秒**。
        *   1D 拉普拉斯实验的 GLDP 版本（生成图10），并行运行 4 个不同 $\nu$ 的任务，总耗时约 **80 秒**。
        *   2D 拉普拉斯实验（生成图11），并行运行 4 个不同 $\varepsilon$ 的任务，总耗时约 **40 秒**。

### 5. 实验数量与充分性

*   **实验数量**：论文包含了较丰富的实验，覆盖了：
    *   两种隐私框架（纯LDP和GLDP）。
    *   三种数据空间（离散 $k=10, 20, 100$，连续 1D，连续 2D）。
    *   多个隐私预算级别（每种框架下4个值）。
    *   多种 $f$-散度评估指标。
*   **充分性与客观性**：
    *   实验设计**充分且公平**。离散空间的实验直接比较了闭式解的理论风险，无可争议。连续空间的实验通过随机生成 100 个客户分布并取最差散度值来经验性估计极小极大风险，对比基准是领域内最新、最强的全局最优方法。
    *   结论（局部优于全局）在**所有**测试场景和隐私预算下均一致成立，说服力强。
    *   论文公开了代码和完整的复现指南，确保了透明度和可复现性。

### 6. 主要结论与发现

*   **理论结论**：局部极小极大风险完全由屏蔽邻域后的全局风险决定，实现了从全局到局部的优雅过渡。
*   **最优采样器特性**：推导出简单、封闭形式的最优采样器，且在纯LDP下找到了点对点优于线性采样的非线性采样器。所有最优采样器均与 $f$-散度选择无关。
*   **实证结论**：在所有实验设置（有限/连续空间、纯LDP/GLDP）下，本文提出的**局部极小极大采样器在各类 $f$-散度指标上，均一致且显著地优于全局极小极大采样器**。尤其是在 $\varepsilon$ 或 $\nu$ 较小（隐私保护强）时，性能差距更加明显。

### 7. 论文优点

*   **视角新颖**：摒弃了悲观的全局最差情况，引入符合实际（如包含公开数据）的局部邻域视角，为个性化隐私提供了理论支撑。
*   **理论严密且美**：揭示了局部问题与全局问题之间的深刻联系，使得局部最优解可以通过修改全局最优解的参数直接获得，过程十分精妙。
*   **结论普适**：得出的最优采样器与具体的 $f$-散度选择无关，这是一个非常强且实用的性质。
*   **方法具体且可实操**：给出了纯LDP下性能更优的非线性采样器的精确闭式解（基于裁剪操作），便于实现和应用。
*   **实验稳健**：对比基准强，实验场景多样，结论一致性好，且代码开源，具有很高的可信度。

### 8. 不足与局限

*   **计算复杂度问题**：论文明确指出，非线性采样器中的裁剪操作在高维数据设定下计算复杂度高，难以直接扩展应用，目前仅限于合成数据实验。论文将此列为重要的未来工作。
*   **实验局限于合成数据**：所有实验均在人工生成的拉普拉斯混合或离散均匀分布上进行，缺少在真实世界高维数据集（如图像、文本）上的验证，其实际应用潜力尚不明确。
*   **邻域定义的敏感性**：模型的核心假设是存在一个已知的、有界似然比的邻域 $\mathcal{N}_\gamma(P_0)$。在实际中，如何选取 $P_0$ 和 $\gamma$ 来准确刻画真实数据的范围，同时保证理论前提成立，可能具有挑战性。
*   **单样本设定的限制**：论文聚焦于“每个客户端生成一个样本”的设定。作者指出，扩展到多样本场景是一个重要的未来方向，因为在实际中，客户端可能需要进行多次查询或发布。
*   **对 $(\alpha, t, u)$-可分解性的依赖**：一些理论证明（如一般空间下的定理3.6）依赖于测度 $\mu$ 是 $(\alpha, 1/\alpha, 1)$-可分解的这一技术性假设，虽然作者认为该假设在连续分布下自然成立，但仍是对理论普适性的一种约束。

（完）
