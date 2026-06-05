---
title: Differential Privacy Guarantees of Markov Chain Monte Carlo Algorithms
title_zh: 马尔可夫链蒙特卡罗算法的差分隐私保障
authors: "Andrea Bertazzi, Tim Johnston, Gareth O. Roberts, Alain Oliviero Durmus"
date: 2025-05-01
pdf: "https://openreview.net/pdf?id=lLnAua5poB"
tags: ["query:daily"]
score: 9.0
evidence: 为MCMC算法建立差分隐私保障
tldr: 针对马尔可夫链蒙特卡罗（MCMC）算法，本文建立了差分隐私（DP）保障。文章首先在一般MCMC框架下，给出样本及蒙特卡罗估计量的DP界，并揭示目标分布需满足隐私性这一关键条件。随后，专门分析非调整朗之万算法和随机梯度朗之万动力学，利用Girsanov定理与扰动技巧得到Rényi DP界。该结果为采样算法的隐私分析提供了理论工具。
source: ICML-2025-Accepted
selection_source: conference_retrieval
motivation: 现有MCMC算法的差分隐私分析缺乏统一框架。
method: 提出基于Girsanov定理和扰动技巧的新方法，建立MCMC的Rényi差分隐私界。
result: 得到针对朗之万类型算法的具体隐私界，并揭示目标分布隐私性的重要性。
conclusion: 为MCMC算法提供了系统化的差分隐私分析路径。
---

## Abstract
This paper aims to provide differential privacy (DP) guarantees for Markov chain Monte Carlo (MCMC) algorithms. In a first part, we establish DP guarantees on samples output by MCMC algorithms as well as Monte Carlo estimators associated with these methods under assumptions on the convergence properties of the underlying Markov chain. In particular, our results highlight the critical condition of ensuring the target distribution is differentially private itself. In a second part, we specialise our analysis to the unadjusted Langevin algorithm and stochastic gradient Langevin dynamics and establish guarantees on their (Rényi) DP. To this end, we develop a novel methodology based on Girsanov's theorem combined with a perturbation trick to obtain bounds for an unbounded domain and in a non-convex setting. We establish: (i) uniform in $n$ privacy guarantees when the state of the chain after $n$ iterations is released, (ii) bounds on the privacy of the entire chain trajectory. These findings provide concrete guidelines for privacy-preserving MCMC.

---

## 论文详细总结（自动生成）

好的，以下是对论文《Differential Privacy Guarantees of Markov Chain Monte Carlo Algorithms》的详细中文总结，按照要求逐点展开。

---

### 1. 论文的核心问题与整体含义

- **研究背景**：差分隐私（DP）已成为设计统计和机器学习算法时的标准框架，用于量化输出结果泄露数据信息的风险。马尔可夫链蒙特卡罗（MCMC）算法常用于贝叶斯推断中近似采样后验分布，因此其隐私性也受到广泛关注。
- **核心问题**：本文旨在为 MCMC 算法（特别是基于扩散过程的算法）建立系统的差分隐私保障，包括输出单次采样状态、整个轨迹以及蒙特卡罗估计量时的隐私界。
- **整体含义**：研究揭示了一个关键条件——**目标后验分布本身必须满足差分隐私**，否则 MCMC 算法无法在收敛到后验的同时保持良好隐私性。此外，针对非凸情形，提出了一种基于 Girsanov 定理和扰动技巧的新方法，得到了与迭代次数无关的单点隐私界以及针对轨迹的紧致界。

---

### 2. 提出的方法论

- **总体框架**：将 MCMC 算法视为一个随机机制 \(A(D)\)，通过比较相邻数据集下输出分布的差异来定义差分隐私。论文分为两部分：
    1. **一般 MCMC 的 DP 分析**：利用总变差距离建立收敛性与 DP 之间的联系，证明当后验具有 \((\epsilon,\delta)\)-DP 时，MCMC 算法的输出也近似满足 \((\epsilon,\delta+\kappa R(n))\)-DP；反之，若后验不满足某 DP 水平而算法收敛到后验，则算法必然违反该 DP 水平。
    2. **针对扩散类算法的 DP 界**：通过 Radon-Nikodym 导数和高概率界证明 DP。利用 Girsanov 定理在概率空间上构造一个等价测度 \(Q\)，使得在 \(Q\) 下算法输出与在原始测度 \(P\) 下的相邻数据集输出同分布。通过控制 Radon-Nikodym 导数的尾部或矩，得到 \((\epsilon,\delta)\)-DP 和 \((\alpha,\epsilon)\)-Rényi DP。

- **关键技术细节**：
    - **Girsanov 定理**：对两个漂移相差 \(c\) 的 SDE，其路径测度的 Radon-Nikodym 导数由随机积分给出，可精确控制。
    - **扰动技巧（Perturbation trick）**：当只释放最终状态 \(X_T\) 时，在时间 \([T-1,T]\) 之间加入一个精心设计的控制项 \(u_t\)，使两个过程的终态相同，并利用两个过程轨迹的几乎必然接近性（来自梯度 Lipschitz 和强凸/非凸条件）来限定 \(u_t\) 的界，从而获得与 \(T\) 无关的隐私界。
    - **对 ULA 和 noisy SGD 的具体应用**：假设目标势函数可分解为 \(U=V+K\)，其中 \(\nabla K\) 是 Lipschitz 且强凸的，\(\nabla V\) 有界。通过迭代收缩不等式得到两个相邻数据集下轨迹的最大距离界，将其代入上述扩散框架，获得不随迭代次数增加的 \((\epsilon,\delta)\)-DP 和 Rényi DP 界。

- **公式/算法流程**（文字说明）：
    - **单点隐私**：对 ULA，步长 \(\gamma\in(0,2a/L^2)\)，通过比较两个链的差 \(e_n\)，得到 \(\sup_{n}|e_n|\le \frac{2c}{a-\gamma L^2/2}\)，然后利用连续时间插值和扰动技巧，得到 \((\epsilon_\delta,\delta)\)-DP 且 \(\epsilon_\delta\) 与迭代次数 \(n\) 无关。
    - **轨迹隐私**：在相同的梯度有界差异假设下，直接利用 Girsanov 定理得到整条路径的 DP 界，其 \(\epsilon\) 随步数 \(n\) 线性增长（\(O(n)\)）但在 Rényi DP 下匹配组合界。
    - **蒙特卡罗估计器**：通过对输出添加拉普拉斯噪声，并结合 MCMC 平均值的集中不等式，获得 DP 保障。

---

### 3. 实验设计

- **说明**：该论文为纯理论性工作，**没有进行计算机仿真实验**。
- 论文的方法论通过数学定理和证明展开，未涉及数据集、benchmark 对比或具体的数值实验。因此无法从实验设计方面评估。

---

### 4. 资源与算力

- 文中**未提及任何关于 GPU、算力或训练时长的信息**。因为该工作属于理论分析，不需要计算资源。

---

### 5. 实验数量与充分性

- **无实验**。理论结果的充分性通过定理和证明来保证，假设条件在文中被明确列出（例如强凸性、梯度有界、Lipschitz 等），并在非凸情形下进行了扩展。理论分析的覆盖范围包括：一般 MCMC、ULA、随机梯度 Langevin 动态，涵盖了最终状态、全轨迹和蒙特卡罗估计量的隐私性。由于没有实验，无法讨论实验覆盖、公平性等问题。

---

### 6. 主要结论与发现

- **后验隐私性是 MCMC 算法隐私的前提**：如果后验分布本身不满足 \((\epsilon,\delta')\)-DP，那么任何收敛到该后验的 MCMC 算法在一定步数后将不再满足 \((\epsilon,\delta)\)-DP（其中 \(\delta<\delta'\)）。同样，若 MCMC 算法的输出比后验具有更强的隐私保证，则其分布必然远离后验。
- **单点隐私与时间无关**：对于 ULA 和 noisy SGD，在满足非凸但具有强凸正则项的条件下，仅释放第 \(n\) 步状态时，其 \((\epsilon,\delta)\)-DP 和 \((\alpha,\epsilon)\)-Rényi DP 界与迭代次数 \(n\) 无关，从而克服了单纯使用组合界导致的隐私预算随步数增加的问题。
- **轨迹隐私的紧致性**：释放整个 Markov 链轨迹时，\((\epsilon,\delta)\)-DP 的 \(\epsilon\) 按 \(O(n+\sqrt{n\log(1/\delta)})\) 增长，Rényi DP 的 \(\epsilon\) 按 \(O(\alpha n)\) 增长，这些结果改进了 \((\epsilon,\delta)\) 组合界，并匹配了 Rényi 组合界。
- **实用指南**：为设计隐私保护的 MCMC 算法提供了具体准则：必须同时设计贝叶斯模型和采样算法，确保后验本身具有良好的 DP 性质。

---

### 7. 优点

- **理论创新**：首次将后验隐私性与 MCMC 算法隐私性明确联系起来，揭示了采样算法隐私的根本限制。
- **方法新颖**：基于 Girsanov 定理和扰动技巧的分析框架，适用于非凸、无界域上的扩散过程，避免了传统组合分析的隐私预算衰减。
- **结果优美**：得到了与步数无关的单点隐私界，具有实际的指导意义，如不需要根据迭代步数调整注入噪声。
- **覆盖面广**：同时考虑了最终状态、整条轨迹和蒙特卡罗估计量，并给出了 ULA 和随机梯度版本的具体界。

---

### 8. 不足与局限

- **缺乏实验验证**：纯理论，没有数值模拟来展示实际隐私参数与理论界的符合程度，难以直观感受常数因子的松紧。
- **假设条件较强**：分析依赖梯度 Lipschitz 和强凸性（或强凸正则项），对于一般非凸目标函数的扩展仍然是一个开放问题。
- **轨迹界依赖步数**：虽然单点界与时间无关，但轨迹界的线性增长可能在高维或长时间仿真中难以接受（尽管已匹配组合界）。
- **随机梯度分析的局限性**：在非强凸设定下，子采样带来的隐私放大效应未能充分体现；当梯度随数据变化而非常量时，隐私界未随 batch size 改善（对比定理 5.6 与定理 5.8）。
- **未考虑蒙特卡罗估计器的高维复杂性**：添加拉普拉斯噪声的方式在维度较高时可能导致噪声方差巨大，实用性受限。

（完）
