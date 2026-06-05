---
title: Privacy amplification by random allocation
title_zh: 随机分配的隐私放大
authors: "Moshe Shenfeld, Vitaly Feldman"
date: 2025-09-18
pdf: "https://openreview.net/pdf?id=MiPIjE5onj"
tags: ["query:daily"]
score: 9.0
evidence: 用于差分隐私优化与聚合的隐私放大
tldr: 针对差分隐私优化与私有聚合中随机分配采样方案的隐私分析难题，首次给出其隐私放大的理论保证与高效数值估计算法，显著改进了以往依赖洗牌分析或蒙特卡洛方法的束缚。该成果为高维私有聚合与通信高效的分布式优化提供了更紧的隐私预算计算工具，推动了差分隐私在分布式系统中的应用。
source: NeurIPS-2025-Accepted
selection_source: conference_retrieval
figures_json: "[{\"url\": \"assets/figures/openreview/openreview-neurips-2025-mipije5onj/fig-001.webp\", \"caption\": \"\", \"page\": 2, \"index\": 1, \"width\": 1600, \"height\": 900}, {\"url\": \"assets/figures/openreview/openreview-neurips-2025-mipije5onj/fig-002.webp\", \"caption\": \"\", \"page\": 10, \"index\": 2, \"width\": 2000, \"height\": 800}, {\"url\": \"assets/figures/openreview/openreview-neurips-2025-mipije5onj/fig-003.webp\", \"caption\": \"\", \"page\": 22, \"index\": 3, \"width\": 1600, \"height\": 900}, {\"url\": \"assets/figures/openreview/openreview-neurips-2025-mipije5onj/fig-004.webp\", \"caption\": \"\", \"page\": 22, \"index\": 4, \"width\": 1600, \"height\": 900}, {\"url\": \"assets/figures/openreview/openreview-neurips-2025-mipije5onj/fig-005.webp\", \"caption\": \"\", \"page\": 23, \"index\": 5, \"width\": 1600, \"height\": 900}, {\"url\": \"assets/figures/openreview/openreview-neurips-2025-mipije5onj/fig-006.webp\", \"caption\": \"\", \"page\": 23, \"index\": 6, \"width\": 1600, \"height\": 900}, {\"url\": \"assets/figures/openreview/openreview-neurips-2025-mipije5onj/fig-007.webp\", \"caption\": \"\", \"page\": 30, \"index\": 7, \"width\": 1600, \"height\": 900}, {\"url\": \"assets/figures/openreview/openreview-neurips-2025-mipije5onj/fig-008.webp\", \"caption\": \"\", \"page\": 31, \"index\": 8, \"width\": 1600, \"height\": 900}, {\"url\": \"assets/figures/openreview/openreview-neurips-2025-mipije5onj/fig-009.webp\", \"caption\": \"\", \"page\": 33, \"index\": 9, \"width\": 5149, \"height\": 3570}, {\"url\": \"assets/figures/openreview/openreview-neurips-2025-mipije5onj/fig-010.webp\", \"caption\": \"\", \"page\": 33, \"index\": 10, \"width\": 4768, \"height\": 3571}, {\"url\": \"assets/figures/openreview/openreview-neurips-2025-mipije5onj/fig-011.webp\", \"caption\": \"\", \"page\": 34, \"index\": 11, \"width\": 4768, \"height\": 3571}, {\"url\": \"assets/figures/openreview/openreview-neurips-2025-mipije5onj/fig-012.webp\", \"caption\": \"\", \"page\": 35, \"index\": 12, \"width\": 1600, \"height\": 900}, {\"url\": \"assets/figures/openreview/openreview-neurips-2025-mipije5onj/fig-013.webp\", \"caption\": \"\", \"page\": 36, \"index\": 13, \"width\": 2011, \"height\": 604}]"
motivation: 现有随机分配采样的隐私分析依赖保守的洗牌放大或计算昂贵的蒙特卡洛方法，缺乏实用且紧的隐私保证。
method: 给出随机分配采样的首次理论隐私放大保证，并开发高效的数值估计算法来计算隐私界限。
result: 得到比以往方法更紧的隐私保证，适用于差分隐私优化和通信高效的高维私有聚合场景。
conclusion: 为随机分配采样的隐私放大提供了严格且实用的分析工具，有益于分布式隐私优化。
---

## Abstract
We consider the privacy amplification properties of a sampling scheme in which a user's data is used in $k$ steps chosen randomly and uniformly from a sequence (or set) of $t$ steps. This sampling scheme has been recently applied in the context of differentially private optimization [Chua et al., 2024a, Choquette-Choo et al., 2024] and is also motivated by communication-efficient high-dimensional private aggregation [Asi et al., 2025]. Existing analyses of this scheme either rely on privacy amplification by shuffling which leads to overly conservative bounds or require Monte Carlo simulations that are computationally prohibitive in most practical scenarios.

We give the first theoretical guarantees and numerical estimation algorithms for this sampling scheme. In particular, we demonstrate that the privacy guarantees of random $k$-out-of-$t$ allocation can be upper bounded by the privacy guarantees of the well-studied independent (or Poisson) subsampling in which each step uses the user's data with probability $(1+o(1))k/t$. Further, we provide two additional analysis techniques that lead to numerical improvements in several parameter regimes. Altogether, our bounds give efficiently-computable and nearly tight numerical results for random allocation applied to Gaussian noise addition.

---

## 论文详细总结（自动生成）

### 1. 论文的核心问题与整体含义（研究动机和背景）
- 研究背景：在差分隐私（DP）分析中，**隐私放大**（privacy amplification）是一项核心技术，通常通过对数据进行随机采样来实现。常见的采样方式包括**泊松采样**（Poisson subsampling，每个元素独立以一定概率参与）和**洗牌**（shuffling）。泊松采样分析简单但会丢弃约37%数据且增加方差；洗牌模型在实践中更常用，但其分析对高斯噪声等近似DP算法会产生保守的界限。  
- 核心问题：论文聚焦于一种**随机分配采样方案**（random k-out-of-t allocation）：每个用户的数据被随机均匀地分配到总共 $t$ 个步骤中的恰好 $k$ 个步骤中。该方案已被应用于 DP-SGD 和高效高维私有聚合，但现有分析要么依赖于洗牌放大的保守界限，要么需要计算开销极高的蒙特卡洛模拟。  
- 整体目标：首次为这种采样方案提供**理论隐私保证**和**高效的数值估计算法**，证明其隐私上限可与泊松采样相比拟，并给出在不同参数区域下更紧的界限。

### 2. 论文提出的方法论
- **核心思想**：将随机分配的隐私分析归约到泊松采样的隐私分析，并在此基础上提供两种额外的分析技术以在部分参数区域获得数值改进。
- **关键技术细节**：
  - **支配随机化归约**（Domination Reduction）：利用支配分布对（dominating pair）将通用自适应多步算法归约到对单元素、非自适应随机化器的分析，并进一步将一般 $k$ 归约到 $k=1$ 的情形。
  - **截断泊松界（主定理）**：证明随机分配的隐私损失分布可以被泊松采样（采样概率 $\eta \approx k/t$）的隐私分布所上界，外加一项随 $t/k$ 渐近消失的低阶项。具体地，$\delta_{A_{t,k}}(\varepsilon) \le \delta_{P_{t,\eta}}(\varepsilon) + t\delta_0 + \delta$，其中 $\eta = \frac{k}{t(1-\gamma)}$，$\gamma$ 由隐私参数和 $t$ 决定。同时提供递归版本显著提升数值。
  - **泊松分解定理**：证明随机分配（$k=1$）的 $\varepsilon$ 不超过泊松采样（率 $1/t$）$\varepsilon$ 的约 1.6 倍，适用于所有参数区域。证明利用了泊松采样是一种随机分配方案的混合，以及分配数越多隐私越差的单调性。
  - **直接分析**：通过推导随机分配方案 Rényi DP 的闭式表达式（对移除方向精确，对添加方向给出近似界）。移除方向给出了基于整数分区（integer partitions）的精确 RDP 计算公式；添加方向则通过调整的随机化器进行上界。
- **通用性**：上述方法适用于任意被高斯或拉普拉斯噪声等常见算法支配的随机化器。

### 3. 实验设计
- **实验场景**：论文主要进行**数值评估**，而不是基于实际数据集训练模型。评估聚焦于高斯机制下的隐私参数 $\varepsilon$ 与噪声尺度 $\sigma$、步数 $t$、分配数 $k$ 的关系。
- **基准与对比方法**：
  - 泊松采样（Poisson subsampling with $\lambda = k/t$）作为性能上限/理想参考。
  - 直接组合（无采样）的本地算法。
  - 洗牌放大界限。
  - Chua et al. (2024a) 的蒙特卡洛模拟估计。
  - Dong et al. (2025) 的 RDP-based 近似界。
- **展示形式**：绘制 $\varepsilon$ 随 $\sigma$、$t$、$k$ 等变化的曲线，比较各种隐私分析方法的紧密程度。

### 4. 资源与算力
- 论文**未明确提及**使用了多少 GPU 型号、数量或训练时长。
- 本文工作以理论分析和数值计算为主，不涉及大规模模型训练。提到数值评估时，代码实现可以在个人电脑上运行，最长运行时间在几分钟内。因此，算力资源需求极低。

### 5. 实验数量与充分性
- **实验数量**：论文中包含多组数值比较图（例如图 1、2、5-11），覆盖了不同 $\delta$（$10^{-10}$, $10^{-7}$ 等）、$t$（$10^3$, $10^4$, $10^6$ 等）、$k$（$1$ 和 $10$）、$\sigma$ 等参数组合，以及多轮组合（epochs）的设置。
- **充分性与客观性**：
  - 实验主要围绕高斯机制展开，参数覆盖从高隐私（大 $\sigma$）到低隐私（小 $\sigma$）的广泛区域。
  - 对比了作者提出的三种方法（截断泊松、泊松分解、直接分析）与同期工作（Dong et al.）及蒙特卡洛下界，多角度验证了界限的紧密性。
  - 在附录中还探讨了隐私-效用权衡（均值估计），从理论上和数值上说明了随机分配相比泊松采样在方差上的优势。
  - 总体而言，实验设计充分且客观，但局限在理论上常见的基准（高斯机制），没有在实际机器学习任务（如图像分类）上验证，不过这并非本文重点。

### 6. 论文的主要结论与发现
- **随机分配的隐私放大效果可被泊松采样上界**，且二者差距在 $t/k$ 增大时渐近消失。数值上，在许多实际参数下随机分配的 $\varepsilon$ 与泊松采样相差通常在 10% 以内。
- **随机分配可在许多情况下替代泊松采样**，仅付出很小的隐私代价，但可改善效用（如消除额外方差、避免丢弃数据）。
- **直接 RDP 分析**在某些低隐私区域甚至能给出比泊松 PLD 分析更好的界限。
- **与同期工作相比**，本文的界限在大部分区域更紧，特别是在 $k$ 较小而 $\alpha$ 较大时。
- **提供了高效可计算的隐私核算工具**，支持组合（composition），可用于 DP-SGD 等多轮训练。

### 7. 优点
- **首次理论保证**：为随机分配采样提供了严格的隐私上界，填补了从“仅蒙特卡洛”到“可证明隐私”的空白。
- **多种互补技术**：主定理（渐近等价）、分解定理（常数倍界）、直接 RDP 分析（精确/近似）在不同参数区域互补，结合后给出总体很紧的数值结果。
- **归约高效**：通过支配随机化器，将复杂自适应算法简化到简单非自适应对，使得分析具有普适性。
- **数值实用**：生成可高效计算的边界，支持组合，便于集成到隐私会计工具中。

### 8. 不足与局限
- **主要针对 remove/add 邻接关系**，对更一般的邻接定义（如替换）需额外处理。
- **直接 RDP 分析**仅对整数阶 $\alpha \ge 2$ 精确，在极高隐私区域（$\varepsilon \ll 1$）需要的 $\alpha$ 很大，计算效率下降；对添加方向的界是近似的。
- **实验仅在高斯机制上详细展示**，尽管方法对一般算法成立，但数值演示范围有限，未展示拉普拉斯机制等。
- **隐私核算混合方法**：最终边界是三种方法的逐点最小值，缺乏统一的紧分布特征，在极低 $\delta$ 时仍可能有改进空间。
- **实际应用中的采样依赖性**未深入探讨，如不同用户之间分配的独立性假设。

（完）
