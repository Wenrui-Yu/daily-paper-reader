---
title: Lightweight Protocols for Distributed Private Quantile Estimation
title_zh: 分布式私有分位数估计的轻量级协议
authors: "Anders Aamand, Fabrizio Boninsegna, Abigail Gentle, Jacob Imola, Rasmus Pagh"
date: 2025-05-01
pdf: "https://openreview.net/pdf?id=zL6ljQvPzZ"
tags: ["query:daily"]
score: 10.0
evidence: 本地差分隐私和洗牌差分隐私下的分布式分位数估计
tldr: "针对分布式领域中用户数据分散且隐私需求高的问题,设计自适应的分位数估计协议,分别在本地差分隐私和洗牌差分隐私模型下达到接近最优的样本复杂度,为分布式隐私数据分析提供轻量级方案。"
source: ICML-2025-Accepted
selection_source: conference_retrieval
figures_json: "[{\"url\": \"assets/figures/openreview/openreview-icml-2025-zl6ljqvpzz/fig-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 853, \"height\": 1040, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-icml-2025-zl6ljqvpzz/fig-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 1736, \"height\": 1139, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-icml-2025-zl6ljqvpzz/fig-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 1753, \"height\": 1193, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-icml-2025-zl6ljqvpzz/fig-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 1495, \"height\": 1044, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-icml-2025-zl6ljqvpzz/fig-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 1498, \"height\": 2322, \"label\": \"Figure\"}]"
tables_json: "[{\"url\": \"assets/tables/openreview/openreview-icml-2025-zl6ljqvpzz/table-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 1778, \"height\": 288, \"label\": \"Table\"}]"
motivation: 分布式数据分析中用户隐私保护与统计效率难以兼顾。
method: "提出自适应算法,在LDP和shuffle DP下估计分位数。"
result: 算法达到低通信和最佳样本复杂度。
conclusion: 轻量级协议为分布式隐私分析提供了实用工具。
---

## Abstract
Distributed data analysis is a large and growing field driven by a massive proliferation of user devices, and by privacy concerns surrounding the centralised storage of data. 
We consider two \emph{adaptive} algorithms for estimating one quantile (e.g.~the median) when each user holds a single data point lying in a domain $[B]$ that can be queried once through a private mechanism; one under local differential privacy (LDP) and another for shuffle differential privacy (shuffle-DP). 
In the adaptive setting we present an $\varepsilon$-LDP algorithm which can estimate any quantile within error $\alpha$ only requiring $O(\frac{\log B}{\varepsilon^2\alpha^2})$ users, and an $(\varepsilon,\delta)$-shuffle DP algorithm requiring only $\widetilde{O}((\frac{1}{\varepsilon^2}+\frac{1}{\alpha^2})\log B)$ users. Prior (nonadaptive) algorithms require more users by several logarithmic factors in $B$. We further provide a matching lower bound for adaptive protocols, showing that our LDP algorithm is optimal in the low-$\varepsilon$ regime. Additionally, we establish lower bounds against non-adaptive protocols which paired with our understanding of the adaptive case, proves a fundamental separation between these models.

---

## 论文详细总结（自动生成）

## 1. 论文的核心问题与整体含义
- **研究动机**：随着用户设备激增和数据隐私法规收紧，分布式数据分析亟需在保护用户隐私的前提下实现统计推断。分位数（如中位数）估计是基础任务之一。
- **核心问题**：当每个用户仅持有一个离散域 $[B]$ 内的数据点，且只能被查询一次时，如何在**本地差分隐私 (LDP)** 和**洗牌差分隐私 (shuffle DP)** 模型下，以自适应协议（即分析器可根据前序响应动态调整查询）高效估计一个分位数。
- **整体含义**：论文揭示了自适应交互在分位数估计中的巨大优势——与非自适应算法相比，自适应 LDP 协议可将所需用户数量的对数因子从 $\log^2 B$ 降低到 $\log B$，并提供了相应的匹配下界，证明了自适应与非自适应模型之间的根本性分离。同时，给出了一种结合洗牌模型与有限交互轮次的实用方案。

## 2. 论文提出的方法论
### 2.1 自适应 LDP 中位数估计
- **核心思想**：将分位数估计归约到**噪声二分搜索 (Noisy Binary Search)**。每个用户的响应相当于一枚未知概率的硬币，通过二分法定位 CDF 接近目标分位数的位置。
- **关键技术步骤**：
  - **随机排列与不放回采样**：将用户随机打乱，依次查询，避免重复使用同一用户。
  - **概率稳定性分析 (Lemma 3.1)**：证明在采样过程中，剩余用户的经验 CDF 不会变化超过 $\alpha$，只要总用户数 $n \ge C \frac{\log B}{\alpha^2}$。
  - **对抗性噪声二分搜索 (AdvMonotonicNBS, Theorem 3.2)**：将状态‑of‑the‑art 的 Bayes Screening Search (BayeSS) 推广到每一轮硬币的真实偏置可以被对手至多扰动 $c\alpha$ 的场景 ($c\le1$)。证明该算法仍能以高概率返回一个 $(\frac12, \alpha(1+c))$-好硬币。
  - **隐私化实现**：每次查询时使用**随机响应**机制对 $[x_i \le j]$ 进行 $\varepsilon$-LDP 扰动，从而将整个交互过程转化为满足 $\varepsilon$-LDP 的自适应协议。
- **样本复杂度**：达到 $O\!\left(\frac{\log B}{\varepsilon^2\alpha^2}\right)$ 用户，与下界匹配（在 $\varepsilon<1$ 的高隐私区最优）。

### 2.2 Shuffle DP 协议
- **核心思路**：将 “重复二分搜索” 与 **隐私放大 (privacy amplification by shuffling)** 结合。由于自适应按单个用户查询无法发挥洗牌威力，改为将用户分成 $r=\log_2 B$ 批，每批内部使用同一随机化器，整批输出经过洗牌，从而获得更优的 $(\varepsilon,\delta)$-DP 保证。
- **样本复杂度**：$\widetilde{O}\!\left(\left(\frac{1}{\varepsilon^2} + \frac{1}{\alpha^2}\right)\log B\right)$，且仅需 $r=\log_2 B$ 轮交互，同时获得自适应与洗牌隐私放大的双重好处。

### 2.3 下界
- **自适应下界 (Theorem 1.2)**：基于 (Duchi et al., 2013) 的互信息框架，构造一族分布 $P_\beta$，证明任何自适应 $\varepsilon$-LDP 协议若成功概率 $\ge 3/4$，必须使用 $\Omega\!\left(\frac{\log B}{\varepsilon^2\alpha^2}\right)$ 用户。
- **非自适应下界 (Theorem 1.3)**：通过将非自适应中位数估计算法归约到 CDF 学习问题，并应用 (Edmonds et al., 2020) 关于非交互 CDF 学习的下界，证明非自适应 LDP 协议至少需要 $\Omega\!\left(\frac{\log^2 B}{\varepsilon^2\alpha^2\log^4(1/\alpha)}\right)$ 用户，揭示了交互性的根本优势。

## 3. 实验设计
- **数据集**：
  - **Pareto 分布**（形状参数 1.5，乘数 2000，取整并裁剪至 $[B]$）：模拟收入等偏态数据。
  - **均匀分布**：从 $[B]$ 内随机区间采样，避免中位数恰好位于域中心。
- **对比方法**：
  - `DpBayeSS`：本文提出的自适应 LDP 算法（基于 BayeSS）。
  - `DpNaiveNBS`：经典噪声二分搜索 + 随机响应（基准）。
  - `Hierarchical Mechanism`（Cormode et al. 2019）：非自适应 LDP 层次查询（状态‑of‑the‑art 非交互方法）。
- **实验参数**：
  - 数据集大小 $n \in \{2500, 5000, 7500, 10^7\}$。
  - 域大小 $B \in \{4^9, 4^8, 10^3, 10^4, 10^5, 10^6\}$。
  - 隐私预算 $\varepsilon \in [0.1, 5]$。
  - Shuffle DP 实验中 $\delta = 10^{-8}$。
- **评价指标**：成功率（返回 $\alpha_{\text{test}}$-好硬币的频率）和绝对分位数误差的累积分布函数 (CDF)。每次实验重复 200 次计算标准差。

## 4. 资源与算力
- 文中明确指出实验所用环境：**Intel Xeon Processor W‑2245 (8 核, 3.9GHz)，128GB RAM，Ubuntu 20.04.3，Python 3.11**。未使用任何 GPU 加速。训练时间未提及。

## 5. 实验数量与充分性
- **实验规模**：
  - 超参数选择实验（算法中 $\tilde{\alpha}=c\sqrt{\frac{\log B}{n}}$ 的常数 $c$ 调优），在不同 $n$、$B$、$\varepsilon$ 组合下进行。
  - 不同隐私预算的对比实验（针对 Pareto 和均匀数据集）。
  - 域大小 $B$ 的敏感性实验（$B$ 从 $10^3$ 到 $10^6$）。
  - 不同用户数 $n$ 条件下的对比（$2500$ 和 $7500$）。
  - Shuffle DP 环境下的对比实验（仅 `DpNaiveNBS` 与 `DpNaiveNBS-Shuffle`）。
- **公平性与客观性**：
  - 对比方法覆盖了自适应二分搜索、非自适应层次查询，较为全面。
  - 对随机性进行了 200 次重复，给出了置信区间。
  - Shuffle 实验中因计算资源限制未能对比 `DpBayeSS` 和 `Hierarchical Mechanism`，这一点作者明确指出了局限。
  - 总体实验参数组合较多，能支撑其核心论断，表现出较好的充分性。

## 6. 论文的主要结论与发现
- 提出了一种低通信（每用户 1 比特）的自适应 $\varepsilon$-LDP 中位数估计算法，样本复杂度 $O(\frac{\log B}{\varepsilon^2\alpha^2})$，在 $\varepsilon<1$ 时是最优的。
- 证明了自适应与非自适应 LDP 在分位数估计问题上的样本复杂度分离：非自适应至少需要多出一个 $\log B$ 因子。
- 给出了一种基于洗牌的有限轮交互协议，兼具自适应的高效性和洗牌模型的私密放大效果，样本复杂度 $\widetilde{O}((\frac{1}{\varepsilon^2}+\frac{1}{\alpha^2})\log B)$。
- 实验显示 `DpBayeSS` 在多种参数下显著优于 `Hierarchical Mechanism` 和 `DpNaiveNBS`。

## 7. 优点
- **理论贡献**：给出了自适应 LDP 分位数估计的紧上下界，并明确分离了自适应与非自适应模型，理论基础坚实。
- **算法实用性强**：每用户仅需 1 比特通信，总时间复杂度低，单轮更新仅需 $O(\log B)$。
- **方法论创新**：将噪声二分搜索的 BayeSS 算法成功推广到对抗性噪声设定，该结果具有独立价值；并将洗牌隐私放大与分批自适应结合，提供了新的协议范式。
- **实验全面**：对比了多种基线，覆盖不同隐私水平、域大小、样本数，并对关键超参数进行了调优。

## 8. 不足与局限
- **数据集均为合成数据**：仅使用了 Pareto 分布和随机区间均匀分布，缺乏真实世界数据集的验证，结论的外部有效性待考察。
- **Shuffle DP 实验不充分**：受限于计算资源，仅比较了基本的 `DpNaiveNBS`，未能展示 `DpBayeSS` 或 `Hierarchical Mechanism` 在洗牌模型下的表现，无法完整揭示该方法在全局对比中的位置。
- **连续域扩展的限制**：虽然在附录讨论了连续域场景，但需假设数据分布在预定义区间内 CDF 增长受控，无相应实验支撑，影响该设想的可操作性。
- **下界的假设条件**：部分下界要求 $\alpha \ge B^{-\Omega(1)}$ 或 $\varepsilon \le 1/\log(1/\alpha)$ 等，在极端参数区域可能不匹配。
- **隐私模型**：自适应协议每次查询一位用户，在大规模部署时需要精细的用户调度，实际工程实现有一定复杂性；shuffle 协议依赖可信洗牌器，信任假设介于本地和中心模型之间。

（完）
