---
title: Optimal Regret of Bandits under Differential Privacy
title_zh: 差分隐私下赌博机的最优遗憾
authors: "Achraf Azize, Yulian Wu, Junya Honda, Francesco Orabona, Shinji Ito, Debabrota Basu"
date: 2025-09-18
pdf: "https://openreview.net/pdf?id=rmL109fdAJ"
tags: ["query:daily"]
score: 9.0
evidence: 差分隐私下的随机赌博机
tldr: 本文研究全局差分隐私下随机赌博机的遗憾最小化问题。现有理论虽给出了阶次匹配的上下界，但两者差距显著。本文通过引入一个新颖的信息论量——该量能够平滑地刻画隐私机制对学习难度的影响，插值于KL散度与另一极端情形之间——推导出更紧的遗憾下界，并设计了与之匹配的算法实现上界改进。实验结果表明，新界限大幅缩小了既有差距，几乎达到紧致。这一结果为差分隐私在线学习提供了更精确的性能保证。
source: NeurIPS-2025-Accepted
selection_source: conference_retrieval
motivation: 现有差分隐私赌博机遗憾界虽阶次匹配但存在显著差距，需要更紧的界以精确刻画隐私代价。
method: 提出新颖信息论量刻画隐私难度，推导更紧遗憾下界并设计匹配算法实现上界改进。
result: 新界限显著缩小既有差距，数值实验验证理论改进。
conclusion: 为差分隐私在线学习提供了更精确的性能保证。
---

## Abstract
As sequential learning algorithms are increasingly applied to real life, ensuring data privacy while maintaining their utilities emerges as a timely question. In this context, regret minimisation in stochastic bandits under $\epsilon$-global Differential Privacy (DP) has been widely studied. 
The present literature poses a significant gap between the best-known regret lower and upper bound in this setting, though they ``match in order''.
Thus, we revisit the regret lower and upper bounds of $\epsilon$-global DP bandits and improve both. 
First, we prove a tighter regret lower bound involving a novel information-theoretic quantity characterising the hardness of $\epsilon$-global DP in stochastic bandits. This quantity smoothly interpolates between Kullback–Leibler divergence and Total Variation distance, depending on the privacy budget $\epsilon$.
Then, we choose two asymptotically optimal bandit algorithms, i.e., KL-UCB and IMED, and propose their DP versions using a unified blueprint, i.e., (a) running in arm-dependent phases, and (b) adding Laplace noise to achieve privacy. For Bernoulli bandits, we analyse the regrets of these algorithms and show that their regrets asymptotically match our lower bound up to a constant arbitrary close to 1.
At the core of our algorithms lies a new concentration inequality for sums of Bernoulli variables under Laplace mechanism, which is a new DP version of the Chernoff bound.
Finally, our numerical experiments validate that DP-KLUCB and DP-IMED achieve lower regret than the existing $\epsilon$-global DP bandit algorithms.

---

## 论文详细总结（自动生成）

## 一、论文核心问题与整体含义

- **研究背景**：随机多臂赌博机中的遗憾最小化（regret minimisation）是序列决策的经典问题，而现实医疗、推荐系统等应用要求保护用户隐私，差分隐私（DP）因此被引入。
- **现有缺口**：在 $\epsilon$‑全局差分隐私的随机赌博机中，已知的最优遗憾下界与上界仅“阶次匹配”，但两者之间仍存在显著差距（乘法常数不紧）。这导致隐私代价的精确刻画不足。
- **本文目标**：重新审视并同时改进 $\epsilon$‑全局差分隐私下 Bernoulli 赌博机的遗憾下界与上界，使其**渐近地匹配到任意接近 $1$ 的乘法常数**，从而给出隐私‑效用权衡的精确理论界限。

## 二、方法论

### 1. 新颖的信息论量 $d_\epsilon$
- 定义：
  \[
  d_\epsilon(x, y) = \inf_{z \in [x\land y, x\lor y]}\{\epsilon|z - x| + \operatorname{kl}(z, y)\},
  \]
  其中 $\operatorname{kl}$ 是 Bernoulli 分布的 KL 散度。
- 性质：根据隐私预算 $\epsilon$ 的大小，$d_\epsilon$ 在 KL 散度与总变差（TV）距离之间平滑插值：
  - **低隐私区间**（$\epsilon$ 足够大）：$d_\epsilon(\mu_a, \mu^\star) = \operatorname{kl}(\mu_a, \mu^\star)$，隐私几乎无额外代价。
  - **高隐私区间**（$\epsilon$ 较小）：$d_\epsilon$ 退化为 KL 项加 TV 项，$\epsilon \to 0$ 时趋于 $\epsilon\Delta_a$。

### 2. 更紧的遗憾下界（Theorem 1）
- 结果：对任意一致的 $\epsilon$‑全局 DP 策略，
  \[
  \liminf_{T\to\infty} \frac{\operatorname{Reg}_T(\pi, \nu)}{\log T} \ge \sum_{a:\Delta_a>0} \frac{\Delta_a}{d_\epsilon(\mu_a, \mu^\star)}.
  \]
- 证明**关键技巧**：“双重环境替换”引理（Lemma 1），先利用群隐私进行 TV 测度变换，再通过经典的 Lai‑Robbins 方法做 KL 替换，最终在优化“中间环境”后得到比纯 KL 或纯 TV 更小的传输代价。

### 3. 核心集中不等式（Proposition 1）
- 考虑 $n$ 个 Bernoulli 变量与 $m$ 个 Laplace 噪声之和 $\tilde{S}_{n,m}$，当 $m/n = o(1)$ 时，存在常数 $A_a$ 使得
  \[
  \Pr\!\left(\frac{\tilde{S}_{n,m}}{n} \le x\right) \le A_a e^{-n(d_\epsilon(x,\mu)-a)}, \quad x \le \mu,
  \]
  对称地也有上尾界。
- **创新性**：对信号与噪声进行**耦合处理**，而非先前工作中分开加性界的做法，使主导项中的 Laplace 噪声数量效应等价于仅加一个噪声。

### 4. 算法设计：DP‑KLUCB 与 DP‑IMED
- **统一蓝图**：
  1. 采用**依赖臂（arm‑dependent）的几何增长批次**，比率为 $\alpha > 1$（可任意接近 $1$）。
  2. 在各阶段**不忘记历史奖励**，而是对累积和添加新的 Laplace 噪声（Line 10），从而利用单一 $\epsilon$ 通过并行组合与后处理仍保持 $\epsilon$‑DP（Proposition 2）。
  3. 基于 $d_\epsilon$ 设计新的**私有索引**：
     - DP‑KLUCB：$\bar{\mu}_i(t) = \max\{\mu : d_\epsilon([\tilde{\mu}_{i,m_i}]_{10}, \mu) \le \frac{\log t}{n_{m_i}}\}$。
     - DP‑IMED：$I_i(t) = n_{m_i} d_\epsilon([\tilde{\mu}_{i,m_i}]_{10}, [\tilde{\mu}^*(t)]_{10}) + \log n_{m_i}$。
- **遗憾上界（Theorem 2）**：对两个算法，遗憾上界均为
  \[
  \operatorname{Reg}_T \le \sum_{i\neq i^*}\frac{\alpha \Delta_i \log T}{d_\epsilon(\mu_i, \mu^\star)} + o(\log T),
  \]
  常数 $\alpha$ 可任意接近 $1$，因而**彻底匹配下界**。

## 三、实验设计

- **环境**：Bernoulli 多臂赌博机，$K=5$ 条臂，4 种均值配置：
  - $\mu_1 = [0.75, 0.7, 0.7, 0.7, 0.7]$
  - $\mu_2 = [0.75, 0.625, 0.5, 0.375, 0.25]$
  - $\mu_3 = [0.75, 0.53125, 0.375, 0.28125, 0.25]$
  - $\mu_4 = [0.75, 0.71875, 0.625, 0.46875, 0.25]$
- **对比方法**：
  - DP‑SE（Sajed & Sheffet 2019）
  - AdaP‑KLUCB（Azize & Basu 2022）
  - Lazy‑DP‑TS（Hu & Hegde 2022）
  - 非隐私基准：IMED（Honda & Takemura 2015）
  - 本文提出的 DP‑KLUCB 和 DP‑IMED
- **隐私预算**：$\epsilon \in \{0.01, 0.1, 0.5, 1\}$，共 $4 \times 4 = 16$ 组主要对比实验。
- **补充实验**：
  - $\alpha$（几何批次比率）的影响分析。
  - 基于真实临床数据（COV‑BOOST 论文）构造的 20 臂 Bernoulli 环境测试。
  - 遗憾随 $\epsilon$ 平滑变化的图示。

## 四、资源与算力

- 实现语言：Python 3.8。
- 硬件：8 核 64‑位 Intel i5 @1.6 GHz CPU，**未使用 GPU**。
- 每次实验运行 100 次，时间步长为 $T = 10^6$（部分实验 $T=10^7$）。所需算力较低，属于普通的学术实验规模。

## 五、实验数量与充分性

- 进行了 **4 种环境 × 4 种隐私预算** 的主要对比，加上额外的消融与真实数据测试，合计约 20 余组实验。
- 每组实验重复 100 次，以均值 ±2 标准差汇报，展示了统计显著性。
- 实验涵盖了不同难度（gap 大小）和不同隐私等级，对理论结论提供了较为全面的数值验证，并能直观显示本文算法在绝大多数设置下遗憾最低且最接近理论下界。

## 六、主要结论与发现

1. 提出 $d_\epsilon$ 量，精确刻画了 $\epsilon$‑全局 DP 下 Bernoulli 赌博机的信息论难度，并得到严格改进的遗憾下界。
2. 基于耦合噪声‑信号的集中不等式，设计了 DP‑KLUCB 和 DP‑IMED，其遗憾上界与下界渐近匹配，匹配常数可任意接近 $1$。
3. 证明了“遗忘历史奖励”并非设计最优 DP 赌博机算法的必要条件，反驳了先前的猜想。
4. 数值实验表明，所提算法在多种 Bernoulli 环境和不同隐私预算下均显著优于文献中的 DP‑SE、AdaP‑KLUCB、Lazy‑DP‑TS。

## 七、优点

- **理论紧致性**：首次在 DP 赌博机中实现上下界匹配至同一常数，是领域内的重要理论进展。
- **方法创新**：$d_\epsilon$ 的信息论量简洁且能清晰划分高低隐私区间；集中不等式耦合分析信号与噪声，优于常见的分离加性上界；算法设计去除了遗忘机制，并给出与下界匹配的索引形式。
- **实验全面且可复现**：覆盖不同环境和隐私预算，给出误差棒，并提供代码。
- **贡献明确**：解决了 Azize & Basu (2022) 提出的开放问题。

## 八、不足与局限

- **分布假设**：算法及其遗憾上界目前仅严格适用于 Bernoulli 奖励分布（[0,1] 有界情形可扩展，但紧致上下界的匹配性质尚不明确）。
- **渐近性质**：上下界均为 $T \to \infty$ 的渐近结果，$o(\log T)$ 项的显式刻画未给出，有限样本性能无理论保证。
- **批次策略依赖**：算法依赖几何增长的批次，虽然理论允许任意 $n_T = o(T)$ 的批大小，但完全消除批次设计是否可能仍待探索，尤其对对抗性环境而言。
- **实验范围**：仅含 Bernoulli 环境与一个真实数据集；未在其他分布族（如高斯、指数族）或非平稳环境中测试。

（完）
