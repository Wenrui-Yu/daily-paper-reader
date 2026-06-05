---
title: "⁠When Data Can't Meet: Estimating Correlation Across Privacy Barriers"
title_zh: 当数据无法相遇：跨越隐私障碍估计相关性
authors: "Abhinav Chakraborty, Arnab Auddy, T. Tony Cai"
date: 2025-09-18
pdf: "https://openreview.net/pdf?id=36uy2GgAy6"
tags: ["query:daily"]
score: 9.0
evidence: 垂直分布式数据中隐私保护的相关性估计
tldr: 垂直分布式场景下，两个服务器各自持有变量部分观测且存在隐私约束。本文研究在差异化差分隐私预算下，通过交互或非交互机制进行相关性估计的极小极大最优速率，为分布式统计推理中的隐私保护提供了理论基准。
source: NeurIPS-2025-Accepted
selection_source: conference_retrieval
motivation: 垂直分布式数据中各服务器有隐私约束，无法共享数据。
method: 确定不同隐私预算下相关估计的极小极大最优速率。
result: 给出了隐私约束下相关估计的理论最优界限。
conclusion: 为分布式统计推理的隐私保护提供理论基础。
---

## Abstract
We consider the problem of estimating the correlation of two random variables $X$ and $Y$, where the pairs $(X,Y)$ are not observed together, but are instead separated co-ordinate-wise at two servers: server 1 contains all the $X$ observations, and server 2 contains the corresponding $Y$ observations. In this vertically distributed setting, we assume that each server has its own privacy constraints, owing to which they can only share suitably privatized statistics of their own component observations. We consider differing privacy budgets $(\varepsilon_1,\delta_1)$ and $(\varepsilon_2,\delta_2)$ for the two servers and determine the minimax optimal rates for correlation estimation allowing for both non-interactive and interactive mechanisms. We also provide correlation estimators that achieve these rates and further develop inference procedures, namely, confidence intervals, for the estimated correlations. Our results are characterized by an interesting rate in terms of the sample size $n$, $\varepsilon_1$, $\varepsilon_2$, which is strictly slower than the usual central privacy estimation rates. More interestingly, we find that the interactive mechanism is always better than its non-interactive counterpart whenever the two privacy budgets are different. Results from extensive numerical experiments support our theoretical findings.

---

## 论文详细总结（自动生成）

# 结构化论文总结：当数据无法相遇：跨越隐私障碍估计相关性

## 1. 论文的核心问题与整体含义
- **研究背景**：在联邦学习中，数据常因隐私或组织原因不能直接汇聚。传统横向联邦学习按样本分割数据，而**纵向联邦学习**则按特征分割，即不同服务器持有同一批样本的不同特征（如医院持有检查结果，药企持有药物反应数据）。这类场景下的统计推断理论尚不完善。
- **核心问题**：考虑双变量 $(X,Y)$ 的 $n$ 个样本，服务器 1 拥有所有 $X$ 值，服务器 2 拥有所有 $Y$ 值，两者只能共享满足**服务器级差分隐私（DP）**的统计量（隐私预算分别为 $(\varepsilon_1,\delta_1)$ 和 $(\varepsilon_2,\delta_2)$）。目标是从这些独立发布的私密统计中估计 Pearson 相关系数 $\rho = \mathbb{E}(XY)$（假设数据已标准化为零均值、单位方差）。
- **整体含义**：本文系统回答了在**垂直分布且隐私受限**的设置下，相关性估计的**极小极大最优速率**是什么，并揭示了交互（INT）与非交互（NI）协议在性能上的根本差异，为纵向联邦学习中的隐私保护推理提供了理论基准。

## 2. 方法论
### 2.1 非交互（NI）协议
- **思路**：两个服务器独立地将样本分成批次（batch），每批计算裁剪后（或符号化）的均值，并添加 Laplace 噪声以满足差分隐私，最终通过批次乘积平均估计协方差，再利用方法矩或直接使用作为相关系数估计。
- **高斯情形**：利用符号函数 $\mathrm{sign}(X_i), \mathrm{sign}(Y_i)$ 计算批次均值，加噪后得到 $\hat{\eta}_{XY}$，利用关系 $\mathbb{E}[\hat{\eta}_{XY}] = 1 - \frac{2\arccos(\rho)}{\pi}$ 反解出 $\hat{\rho}_{\mathrm{NI}}^{(G)} = \sin(\pi\hat{\eta}_{XY}/2)$。批次大小取 $m = \lfloor 8/(\varepsilon_1\varepsilon_2) \rfloor \vee 1$。
- **亚高斯情形**：采用截断（clipping）代替符号，截断参数为 $\lambda_1,\lambda_2$，加噪尺度与截断值成正比，直接估计 $\hat{\rho}_{\mathrm{NI}}^{(SG)} = \frac{1}{k}\sum_{j=1}^k T_{1,j}T_{2,j}$。
- **置信区间**：基于批次乘积的样本方差，利用中心极限定理构造正态近似的置信区间。

### 2.2 交互（INT）协议
- **思路**：允许隐私预算较宽松的服务器（如 $\varepsilon_1 > \varepsilon_2$）先将其私密统计 $T_1(X)$ 发送给另一服务器，后者在收到 $T_1$ 后计算加入自己数据的协方差，并再加一次 Laplace 噪声输出 $T_2(Y,T_1)$。
- **高斯情形**：服务器 1 发送带随机符号翻转的私有符号向量 $T_1(X)_i = \frac{e^{\varepsilon_1}+1}{e^{\varepsilon_1}-1}(2S_i-1)\mathrm{sign}(X_i)$；服务器 2 据此与 $\mathrm{sign}(Y_i)$ 计算 $\hat{\eta}_{XY,\mathrm{int}}$，并加 Laplace 噪声得到最终统计量。估计量同样是 $\hat{\rho}_{\mathrm{INT}}^{(G)} = \sin(\pi\hat{\eta}_{XY,\mathrm{int}}/2)$。
- **亚高斯情形**：服务器 1 发送经截断并加 Laplace 噪声的 $[X_i]_{\lambda_1} + Z_{1i}$，服务器 2 再对 $([X_i]_{\lambda_1} + Z_{1i})Y_i$ 截断后求均值并加噪。
- **置信区间**：根据 $\sqrt{n}\varepsilon_2$ 的极限行为分两种情况构造：若收敛至有限常数则用卷积分布 $Z_{\mathrm{XY}} + c^* Z_{\mathrm{Lap}}$ 的分位数；若发散则用 Laplace 近似的分位数。

### 2.3 极小极大下界
- **技术路线**：基于 Le Cam 方法和 Van Trees 不等式，通过对私有统计量 Fisher 信息的精细控制导出下界。
- **关键引理**：在 $\rho=0$ 处，非交互转录的 Fisher 信息 $I_F(T;0) \le \frac{8}{\pi}(n\varepsilon_1^2 \wedge n\varepsilon_2^2)$；交互转录满足 $I_F(\Pi;0) \le (n\varepsilon_1^2 \wedge n^2\varepsilon_1^2\varepsilon_2^2) \vee (n\varepsilon_2^2 \wedge n^2\varepsilon_1^2\varepsilon_2^2)$。利用局部正则条件将 0 点信息推广至邻域，结合先验得到下界。

### 2.4 理论收敛速率总结
- **非交互极小极大速率**：$\displaystyle \frac{1}{n\varepsilon_1^2} + \frac{1}{n\varepsilon_2^2}$（忽略对数因子）。
- **交互极小极大速率**：$\displaystyle \frac{1}{n(\varepsilon_1\vee\varepsilon_2)^2} + \frac{1}{n^2\varepsilon_1^2\varepsilon_2^2}$。
- 交互协议总不劣于非交互，且当 $\varepsilon_1 \neq \varepsilon_2$ 时严格更优。

## 3. 实验设计
- **数据集/场景**：
  - **模拟实验**：① 双变量高斯分布 $\mathcal{N}\left(0,\begin{pmatrix}1&\rho\\\rho&1\end{pmatrix}\right)$；② 有界因子模型（子高斯）：$X=U+E_1$, $Y=U+E_2$，$U\sim\mathrm{Unif}[-\sqrt{3\rho},\sqrt{3\rho}]$，误差独立均匀分布，确保边缘零均值、单位方差。
  - **真实数据**：美国 Health and Retirement Study (HRS) Wave 2，约2万个体，变量为年龄和 BMI，估计两者的 Pearson 相关系数。先通过中心 DP 对边际均值和标准差进行私有化（$\varepsilon=0.1$），再应用 NI 和 INT 方法。
- **Benchmark/对比方法**：NI 与 INT 方法直接对比，同时对比有无私有化标准化步骤（normalized vs. non-normalized）对结果的影响。真实数据中与无隐私的全样本估计作为基准。
- **评价指标**：均方误差 (MSE)、平均置信区间 (CI) 长度、经验覆盖概率（标称 $1-\alpha=0.95$）以及置信区间偏移带。

## 4. 资源与算力
- 文中明确说明：“All experiments were done on a desktop with 32 GB RAM, and were done over the course of 1 hour.”
- **未使用 GPU**，计算量小，仅涉及 CPU 运算和统计模拟。

## 5. 实验数量与充分性
- **模拟参数网格**：
  - 样本量 $n \in \{1000, 1500, 2500, 4000, 6000, 9000\}$；
  - 相关系数 $\rho \in \{0, 0.15, 0.3, 0.4, 0.5, 0.65, 0.8, 0.9\}$；
  - 隐私预算组合 $(\varepsilon_1,\varepsilon_2) \in \{(0.5,0.5), (1,1), (1.5,0.5)\}$；
  - 每种配置重复 250 次。
- **内容覆盖**：高斯和子高斯两种分布，NI/INT 两种协议，有无标准化步骤，MSE、CI 长度、覆盖率等多维指标。
- **客观公平性**：设置合理，涵盖对称/非对称隐私预算，样本量与隐私预算范围较广；重复次数充足使得统计结果稳定；真实数据补充了实践可行性。实验相对充分，对比公平。

## 6. 主要结论与发现
- **速率分离**：交互协议在隐私预算不相等时严格优于非交互协议，其主导项取决于较宽松的预算 $\varepsilon_1\vee\varepsilon_2$，而较严格预算的影响因 $n^{-2}$ 衰减。
- **隐私代价**：纵向分布且服务器级 DP 下的相关性估计速率慢于集中式 DP（速率 $1/(\sqrt{n}\varepsilon)$），但快于本地化 DP（速率 $1/(n\varepsilon_1^2\varepsilon_2^2)$）。
- **私有化标准化无额外代价**：数值实验表明，对边际进行私有标准化后，MSE、区间长度和覆盖率几乎不受影响，验证了理论判断。
- **置信区间有效性**：构建的置信区间在大多数设置下经验覆盖概率保持在标称 95% 附近，且在真实数据中，交互区间在 $\varepsilon=1$ 时已能排除零相关，而非交互区间不能。
- **理论下界匹配上界**：通过 Fisher 信息控制得到的信息论下界与提出的估计量速率一致（至多差对数因子），证实所提方法的极小极大最优性。

## 7. 优点
- **理论深度与完备性**：同时给出匹配上界的算法和下界证明，且覆盖高斯和亚高斯分布，处理了非交互和交互两种模式，并提供置信区间推断。
- **清晰的隐私分析**：通过批处理、截断、随机符号翻转与 Laplace 机制精确控制敏感度和隐私预算，估计量同时满足纯 $\varepsilon$-DP。
- **实验验证全面**：模拟覆盖多维度参数，纳入真实数据验证，且特别考察了私有标准化步骤的影响，支撑理论结论。
- **对实践的指导意义**：明确指出当隐私预算不对称时应优先采用交互协议，且隐私较宽松的一方可主动分享信息以获得更优估计。

## 8. 不足与局限
- **分布假设**：主要针对高斯和子高斯分布，对于更重尾或复杂依赖结构的有效性尚不明确；估计量构造依赖方差归一化和对称性假设。
- **单特征简化**：每个服务器仅含一个特征，未考虑多维特征间相关性以及高维设置下的计算与隐私挑战。
- **交互方向固定**：交互协议假定已知哪一方隐私预算更宽松，实际可能需自适应选择方向，文中未展开讨论。
- **δ > 0 的近似处理**：理论结果多在 $\delta=o(n^{-1})$ 下阐述，高维或小样本时 $\delta$ 的影响需更细致分析。
- **非线性关系**：仅考虑 Pearson 相关系数，未涉及更一般的关联度量。

（完）
