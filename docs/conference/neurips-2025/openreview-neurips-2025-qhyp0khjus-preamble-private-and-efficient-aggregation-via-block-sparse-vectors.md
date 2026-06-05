---
title: "PREAMBLE: Private and Efficient Aggregation via Block Sparse Vectors"
title_zh: PREAMBLE：基于块稀疏向量的私密高效聚合
authors: "Hilal Asi, Vitaly Feldman, Hannah Keller, Guy N. Rothblum, Kunal Talwar"
date: 2025-09-18
pdf: "https://openreview.net/pdf?id=qhYp0kHjUS"
tags: ["query:daily"]
score: 9.0
evidence: 提出PREAMBLE方法，实现私有联邦学习中高维向量的通信高效安全聚合，支持私有分布式机器学习
tldr: 针对私有联邦学习中高维梯度聚合通信开销大的问题，提出PREAMBLE方法，基于扩展分布式点函数处理块稀疏向量，实现通信和计算高效的安全聚合，使高维向量处理可行。
source: NeurIPS-2025-Accepted
selection_source: conference_retrieval
figures_json: "[{\"url\": \"assets/figures/openreview/openreview-neurips-2025-qhyp0khjus/fig-001.webp\", \"caption\": \"\", \"page\": 9, \"index\": 1, \"width\": 614, \"height\": 452}]"
motivation: 现有安全聚合方案（如Prio）通信开销随维度线性增长，限制高维向量处理。
method: 利用分布式点函数扩展，针对块稀疏向量设计通信高效聚合机制。
result: 通信复杂度显著降低，支持更高维度的私有聚合。
conclusion: PREAMBLE为高维私有联邦学习提供了实用的聚合方案。
---

## Abstract
We revisit the problem of secure aggregation of high-dimensional vectors in a two-server system such as Prio. These systems are typically used to aggregate vectors such as gradients in private federated learning, where the aggregate itself is protected via noise addition to ensure differential privacy. Existing approaches require communication scaling with the dimensionality, and thus limit the dimensionality of vectors one can efficiently process in this setup. 

We propose PREAMBLE: {\bf Pr}ivate {\bf E}fficient {\bf A}ggregation {\bf M}echanism via  {\bf BL}ock-sparse {\bf E}uclidean Vectors. PREAMBLE builds on an extension of distributed point functions that enables communication- and computation-efficient aggregation of {\em block-sparse vectors}, which are sparse vectors where the non-zero entries occur in a small number of clusters of consecutive coordinates. We show that these block-sparse DPFs can be combined with random sampling and privacy amplification by sampling results, to allow asymptotically optimal privacy-utility trade-offs for vector aggregation, at a fraction of the communication cost. When coupled with recent advances in numerical privacy accounting, our approach incurs a negligible overhead in noise variance, compared to the Gaussian mechanism used with Prio.

---

## 论文详细总结（自动生成）

# PREAMBLE 论文详细总结

## 1. 论文的核心问题与整体含义
- **研究动机**：在私有联邦学习等场景中，常需对高维向量（如梯度）进行安全聚合，现有两服务器方案（如 Prio）要求客户端发送整个向量，通信开销随维度线性增长（例如 800 万维需 64 MB），限制了可处理的模型规模。
- **核心问题**：如何在保证差分隐私的前提下，大幅降低高维向量聚合的设备到服务器通信量，同时保持近优的隐私-效用平衡。
- **整体含义**：提出 PREAMBLE，利用“块稀疏”这一结构化稀疏性，结合密码学工具与隐私放大技术，在通信只与稀疏度成正比的条件下，实现与全量高斯机制几乎等同的聚合精度。

## 2. 论文提出的方法论
- **核心思想**：将 D 维向量按块大小 B 划分成 Δ = D/B 块，要求客户端只发送 k 个非零块（k‑块稀疏向量），利用扩展的分布式点函数（DPF）在两服务器间高效秘密共享这些块稀疏向量，同时隐藏稀疏模式以启用隐私放大。
- **隐私保护机制**：
  - 使用**分区子采样**或**截断泊松子采样**：每个客户端随机选择 k 个块，并乘以系数 Δ/k 以保证无偏估计。
  - 采样模式对服务器不可见，从而通过“隐私放大采样”将块级大敏感度转换为接近完整向量高斯机制的隐私开销。
- **密码学构造（k‑块稀疏 DPF）**：
  - 基于 [BGI16] 的树形 DPF，修改最后一层 PRG 输出长度为 B 个群元素，避免为每个坐标单独构建 DPF。
  - 使用**布谷鸟哈希**将每层 k 个非零节点分配到约 3k 个校正字中，使每个节点最多应用 w=2 个校正字，将服务器计算从 O(k·D) 降至 O(D)，且通信接近 kB·log|G|。
  - 提供**零知识证明**验证客户端贡献的块稀疏性和范数边界，证明显著效率，且不泄漏诚实客户端信息。
- **隐私分析**：结合分区分配隐私放大和组合定理，证明当 k≥√Δ·log(1/δ)/σ 等条件成立时，隐私参数 ε = O(√Δ·log(1/δ)/σ)，与高斯机制渐近匹配。数值会计使用 RDP‑based 和 PRV 方法给出更紧的界。

## 3. 实验设计
- **数据集 / 场景**：
  - 合成数据：模拟 n=10⁵ 个 D=2²⁰~2²³ 维单位范数向量聚合，评估通信‑效用权衡。
  - 真实数据：MNIST（模型参数 69050）、CIFAR‑10（使用 CLIP 嵌入，两层网络 66954 参数），在 DP‑SGD 框架下训练。
- **对比方法**：基线为发送**完整向量 + 高斯机制**（Analytic Gaussian mechanism 会计）。
- **评价指标**：每坐标期望平方误差（含采样误差+隐私噪声）、通信量（kB 作为代理）、模型准确率。
- **参数设置**：块大小 B ∈ [2¹⁰, 2¹⁴]，ε=1.0 或 2.0，δ=10⁻⁶，样本数 n=10⁵ 或 6×10⁵。

## 4. 资源与算力
- 论文**未明确提及使用 GPU 集群**。实验在 MacBook Pro（Apple M1 Pro，10 核，32 GB RAM）上运行。
- 训练 MNIST/CIFAR 时，高斯机制每 epoch 数秒至 30 秒，PREAMBLE 约 1–2 分钟，属于可接受的开销。

## 5. 实验数量与充分性
- **实验图表**：正文含图 4a（通信 vs 块大小）、4b（截断误差）、4c（隐私‑效用权衡）、5a（噪声标准差比）、5b（MNIST 精度）、5c（CIFAR‑10 精度）；附录包括多维度、多样本量、两种采样方案对比、真实梯度估计等补充实验（图 10–14）。
- 整体实验覆盖了通信节省、截断影响、隐私‑效用 Pareto 前沿、不同维度、不同样本量、消融对比（分区 vs 截断泊松）、以及两轮机器学习任务，**较为充分**。对比基线单一但直接（全量发送），公平性有保证。

## 6. 论文的主要结论与发现
- **通信大幅降低**：在 800 万维、64 位域上，通信从 64 MB 降至约 1 MB，对应隐私噪声标准差仅增加约 10%（(1,10⁻⁶)‑DP，100K 向量）。
- **块稀疏是高效表达的“关键抽象”**：适当块大小（如 2¹⁰~2¹³）在截断误差、通信和隐私之间取得良好平衡。
- **隐私放大与块采样结合**可使隐私开销接近全量高斯机制，相比直接发送稀疏向量（敏感度增大 Δ/k 倍）有显著改善。
- 在 MNIST 和 CIFAR‑10 上 DP‑SGD 训练中，PREAMBLE 在仅通信约 2×10⁴ 个参数的情况下，准确率与高斯机制持平或略低，但通信节省数倍。

## 7. 优点
- **创新性**：首次将块稀疏概念与 DPF 结合，并配套隐私放大分析，解决两服务器模型下的高维聚合通信瓶颈。
- **密码学构造高效**：通过布谷鸟哈希减少服务器端 PRG 评估次数至 O(D)，且客户端计算仅依赖于 kB。
- **理论‑实践结合**：既有渐近最优分析，又有数值隐私会计和真实机器学习实验，证明可行性。
- **泛化能力**：方法可适配单可信服务器、频率估计（1‑热点向量）等场景。

## 8. 不足与局限
- **隐私分析仍可改进**：分区子采样的隐私界依赖 RDP，略松于 PRV；k‑out‑of‑Δ 随机子集的隐私界未被精确量化。
- **通信‑计算权衡**：使用更多哈希函数可降低通信，但增加节点操作次数；文中主要给出 w=2 的构造，存在常数因子开销。
- **失败概率**：布谷鸟哈希存在 O(1/k) 的失败概率，虽对统计应用影响小，但在安全关键场景可能需顾虑。
- **实验局限**：仅测试 MNIST 和 CIFAR‑10 的小模型，未在更大模型（如 ResNet50 完整训练）或更多样化的学习任务上验证；代码未开源。
- **范数假设**：要求块级范数有界，尽管通过随机旋转可放松至总范数约束，但实际应用中仍需额外处理。

（完）
