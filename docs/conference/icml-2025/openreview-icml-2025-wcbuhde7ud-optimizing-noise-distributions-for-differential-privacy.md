---
title: Optimizing Noise Distributions for Differential Privacy
title_zh: 优化差分隐私的噪声分布
authors: "Atefeh Gilani, Juan Felipe Gomez, Shahab Asoodeh, Flavio Calmon, Oliver Kosut, Lalitha Sankar"
date: 2025-05-01
pdf: "https://openreview.net/pdf?id=wCBuHDe7Ud"
tags: ["query:daily"]
score: 9.0
evidence: 优化噪声分布以最小化Rényi差分隐私，获得更好的DP保障
tldr: "差分隐私机制通常使用高斯或拉普拉斯噪声，但并非最优。本文将噪声设计转化为凸优化问题，以最小化Rényi差分隐私为目标，考虑多种组合场景。通过梯度下降求解，得到优化的连续和离散噪声分布。数值实验表明，优化后的分布在中度组合下显著提升(ε,δ)-DP保障，为更高效的隐私机制设计提供了通用工具。"
source: ICML-2025-Accepted
selection_source: conference_retrieval
figures_json: "[{\"url\": \"assets/figures/openreview/openreview-icml-2025-wcbuhde7ud/fig-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 760, \"height\": 563, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-icml-2025-wcbuhde7ud/fig-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 1665, \"height\": 487, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-icml-2025-wcbuhde7ud/fig-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 1638, \"height\": 490, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-icml-2025-wcbuhde7ud/fig-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 1757, \"height\": 454, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-icml-2025-wcbuhde7ud/fig-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 1697, \"height\": 607, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-icml-2025-wcbuhde7ud/fig-006.webp\", \"caption\": \"\", \"page\": 0, \"index\": 6, \"width\": 1757, \"height\": 457, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-icml-2025-wcbuhde7ud/fig-007.webp\", \"caption\": \"\", \"page\": 0, \"index\": 7, \"width\": 1658, \"height\": 564, \"label\": \"Figure\"}]"
tables_json: "[{\"url\": \"assets/tables/openreview/openreview-icml-2025-wcbuhde7ud/table-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 1449, \"height\": 233, \"label\": \"Table\"}]"
motivation: 标准噪声分布（高斯、拉普拉斯）在组合DP下非最优。
method: 提出统一优化框架，将噪声设计建模为凸问题，通过梯度下降求解最优分布。
result: "优化分布相比传统分布，在Rényi DP和(ε,δ)-DP上均有显著改进。"
conclusion: 优化噪声分布可系统提升差分隐私的效率，适用于多种场景。
---

## Abstract
We propose a unified optimization framework for designing continuous and discrete noise distributions that ensure differential privacy (DP) by minimizing Rényi DP, a variant of DP, under a cost constraint. Rényi DP has the advantage that by considering different values of the Rényi parameter $\alpha$, we can tailor our optimization for any number of compositions. To solve the optimization problem, we reduce it to a finite-dimensional convex formulation and perform preconditioned gradient descent. The resulting noise distributions are then compared to their Gaussian and Laplace counterparts. Numerical results demonstrate that our optimized distributions are consistently better, with significant improvements in $(\varepsilon, \delta)$-DP guarantees in the moderate composition regimes, compared to Gaussian and Laplace distributions with the same variance.

---

## 论文详细总结（自动生成）

## 论文总结：优化差分隐私的噪声分布

### 1. 核心问题与整体含义
- **研究动机**：差分隐私（DP）中的噪声添加机制常采用高斯或拉普拉斯分布，但在重复查询（组合）的场景下，这些分布并非最优。
- **背景**：已有工作表明，在单次纯DP下Staircase分布最优，在大规模组合下Cactus分布最优，而中等组合次数（如10–40次）的场景缺乏系统的最优噪声设计。
- **整体含义**：本文提出一个统一优化框架，针对任意组合次数、给定方差约束，设计连续或离散噪声分布，以最小化Rényi差分隐私（RDP）参数，从而获得更优的$(\varepsilon, \delta)$-DP保障。

### 2. 方法论
- **核心思想**：将$(\varepsilon,\delta)$-DP的优化转化为Rényi DP（$\alpha$阶）的最小化问题，利用RDP的组合可加性简化目标；再通过限制分布族（分段常数PDF或对称PMF，带几何尾部）得到有限维凸优化问题。
- **关键技术细节**：
  - 目标函数：$\min_{P_Z} \max_{t\in S} D_\alpha(P_Z \| T_t P_Z)$，其中$T_t$为平移算子，$S$是敏感性范围。
  - 证明该函数是$P_Z$的凸函数，且最优分布可限定为对称分布。
  - 分布族：连续情况采用分段常数PDF，离散情况采用对称PMF，均引入几何尾部将变量数压缩至$N+1$维。
  - 约束条件：概率归一化、非负性以及给定方差（均方误差）限制。
  - 优化算法（Algorithm 3）：
    - 初始化：近似高斯分布（Algorithm 2），并通过二分法调整参数使得方差匹配目标$\sigma^2$。
    - 预条件梯度下降：使用变换矩阵$\mathbf{M} = \text{diag}(\mathbf{p}_{k-1})^{-1}$避免边界点导致无穷的目标值，而无需极小步长。
    - 投影：在变换后的空间投影到满足归一化和方差约束的子空间。
    - 回溯线搜索：尝试不同学习率，选择使目标函数下降最大的步长。
    - $\alpha$的自动更新：基于矩会计公式，每隔$T$步用牛顿法更新$\alpha$，使其适应组合次数和$\delta$。
- **算法流程**（Algorithm 1）：输入$\delta$、组合次数$N_c$、噪声标准差$\sigma$、敏感性$s$、类型（连续/离散），输出最优分布$\mathbf{P}^*$。

### 3. 实验设计
- **数据集与场景**：
  - 隐私曲线对比（图1、图5、图7）：固定组合次数$N_c$（多为10或20）、$\sigma$（如8或5）、$s=1$，比较不同$\delta$下的$(\varepsilon,\delta)$曲线，显示优化噪声曲线为各目标$\delta$最优分布的点态最小值。
  - 中等组合优势区域（图4、图6）：网格搜索组合数（1~60）和$\sigma$，固定$\delta=10^{-6}$或$10^{-9}$，标记优化噪声相比Gaussian/Laplace/Staircase/Cactus至少提升2% $\varepsilon$的区域。
  - 真实数据集查询（表1）：乳腺癌、糖尿病、心脏病（UCI）三个数据集，对10个均值查询加噪声，比较优化噪声与高斯噪声的均方误差（MSE）改进百分比（平均8–12%）。
- **对比方法**：高斯噪声、拉普拉斯噪声、Staircase分布、Cactus分布。
- **评估指标**：$(\varepsilon,\delta)$-DP曲线、MSE、$\varepsilon$值改善百分比。

### 4. 资源与算力
- 论文**未明确提及**使用的GPU型号、数量、训练时长或任何具体算力消耗。
- 算法实现依赖于预条件梯度下降，属于一阶优化，需要迭代$K$步；在给定的分布族维度$N$（如8000）下可能存在一定计算量，但无硬件和时间报告。

### 5. 实验数量与充分性
- 实验覆盖了多种组合次数（1~60）、不同目标$\delta$（$10^{-6}$, $10^{-9}$等）、连续与离散两种类型，并与多种基准分布比较。
- 展示了隐私曲线形状、最优区域热点图和真实数据MSE表格，包含了消融类分析（点态最小曲线表明对不同$\delta$重新优化分布的效果）。
- 实验设计较为全面，对比公平（相同方差约束），但局限于低维查询（均值），且未在大规模深度学习中验证。

### 6. 主要结论与发现
- 优化得到的噪声分布（RDP噪声）在中度组合（10–40次）下，$(\varepsilon,\delta)$-DP的$\varepsilon$值显著低于同等方差的高斯或拉普拉斯噪声。
- 该框架在大组合极限（$\alpha\to1$）下恢复Cactus分布，在单次纯DP（$\alpha\to\infty$）下恢复Staircase分布，验证了其通用性。
- 离散优化噪声同样优于离散高斯、离散拉普拉斯，可抵抗浮点攻击并适用于整数查询。
- 在真实数据查询中，MSE减少8–12%，表明可用更小的方差达成相同的隐私水平。

### 7. 优点
- **统一框架**：一个优化问题同时涵盖连续/离散，单次/多次组合，以及各种成本函数（文中以方差为例）。
- **凸化处理**：将非凸的$(\varepsilon,\delta)$优化转化为RDP下的凸问题，使求解可行且高效。
- **预条件梯度下降**：巧妙避免因零概率导致的梯度爆炸问题，无需极小步长即可保持严格正概率。
- **自动选择$\alpha$**：与矩会计结合，自动适应组合次数，无需人工调参。
- **理论严谨性**：证明了obj函数的凸性、对称性以及有限维近似的合理性。

### 8. 不足与局限
- **分布族限制**：假设分布为对称分段常数/PMF带几何尾部，可能无法精确表示某些复杂最优形式，但通过增加$N$可逼近。
- **损失函数单一**：仅以方差（MSE）作为成本约束，未探讨其他效用度量（如$L_1$距离、最大误差等）。
- **实验规模有限**：真实数据查询仅为低维平均值，未在机器学习训练（如梯度扰动）中验证，可能不能完全代表高维查询性能。
- **计算开销不明确**：预条件梯度下降的单步计算量随$N$和$s/\Delta$增长，对于大尺度问题效率未知。
- **与其他机制的“最优”边界**：在某些$\sigma$和组合数下，优化噪声的优势<2%，并不总是显著胜出。
- **适应性未讨论**：文中组合模型为独立同分布机制的简单叠加，未深入讨论自适应组合或隐私过滤器场景。

（完）
