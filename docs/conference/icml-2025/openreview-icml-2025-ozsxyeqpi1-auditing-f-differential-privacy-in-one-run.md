---
title: Auditing $f$-differential privacy in one run
title_zh: 单次运行审计 f-差分隐私
authors: "Saeed Mahloujifar, Luca Melis, Kamalika Chaudhuri"
date: 2025-05-01
pdf: "https://openreview.net/pdf?id=OZSXYeqpI1"
tags: ["query:daily"]
score: 9.0
evidence: 高效审计差分隐私
tldr: 针对现有差分隐私审计方法需多次运行或准确度不足的问题，提出一种只需单次运行的紧致经验审计方法，能更准确地评估机制的真实隐私水平，提高了审计效率。
source: ICML-2025-Accepted
selection_source: conference_retrieval
figures_json: "[{\"url\": \"assets/figures/openreview/openreview-icml-2025-ozsxyeqpi1/fig-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 1758, \"height\": 456, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-icml-2025-ozsxyeqpi1/fig-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 641, \"height\": 524, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-icml-2025-ozsxyeqpi1/fig-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 637, \"height\": 519, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-icml-2025-ozsxyeqpi1/fig-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 684, \"height\": 538, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-icml-2025-ozsxyeqpi1/fig-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 1731, \"height\": 671, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-icml-2025-ozsxyeqpi1/fig-006.webp\", \"caption\": \"\", \"page\": 0, \"index\": 6, \"width\": 862, \"height\": 523, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-icml-2025-ozsxyeqpi1/fig-007.webp\", \"caption\": \"\", \"page\": 0, \"index\": 7, \"width\": 857, \"height\": 522, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-icml-2025-ozsxyeqpi1/fig-008.webp\", \"caption\": \"\", \"page\": 0, \"index\": 8, \"width\": 857, \"height\": 524, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-icml-2025-ozsxyeqpi1/fig-009.webp\", \"caption\": \"\", \"page\": 0, \"index\": 9, \"width\": 857, \"height\": 525, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-icml-2025-ozsxyeqpi1/fig-010.webp\", \"caption\": \"\", \"page\": 0, \"index\": 10, \"width\": 784, \"height\": 632, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-icml-2025-ozsxyeqpi1/fig-011.webp\", \"caption\": \"\", \"page\": 0, \"index\": 11, \"width\": 781, \"height\": 620, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-icml-2025-ozsxyeqpi1/fig-012.webp\", \"caption\": \"\", \"page\": 0, \"index\": 12, \"width\": 784, \"height\": 620, \"label\": \"Figure\"}]"
tables_json: "[{\"url\": \"assets/tables/openreview/openreview-icml-2025-ozsxyeqpi1/table-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 862, \"height\": 715, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-icml-2025-ozsxyeqpi1/table-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 860, \"height\": 642, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-icml-2025-ozsxyeqpi1/table-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 1783, \"height\": 259, \"label\": \"Table\"}]"
motivation: 现有审计方法要么计算量大需多次运行，要么经验隐私计算不紧致。
method: 利用输入数据集的随机性，设计单次运行的紧致分析程序。
result: 实现了更紧致、更高效的 f-差分隐私经验审计。
conclusion: 该方法显著提升了DP审计的效率和准确性，有助于发现隐私实现缺陷。
---

## Abstract
Empirical auditing has emerged as a means of catching some of the flaws in the implementation of privacy-preserving algorithms. Existing auditing mechanisms, however, are either computationally inefficient -- requiring multiple runs of the machine learning algorithms —- or suboptimal in calculating an empirical privacy. In this work, we present a tight and efficient auditing procedure and analysis that can effectively assess the privacy of mechanisms. Our approach is efficient; Similar to the recent work of Steinke, Nasr and Jagielski (2023), our auditing procedure leverages the randomness of examples in the input dataset and requires only a single run of the target mechanism. And it is more accurate; we provide a novel analysis that enables us to achieve tight empirical privacy estimates by using the hypothesized $f$-DP curve of the mechanism, which provides a more accurate measure of privacy than the traditional $\epsilon,\delta$ differential privacy parameters. We use our auditing procure and analysis to obtain empirical privacy, demonstrating that our auditing procedure delivers tighter privacy estimates.

---

## 论文详细总结（自动生成）

### 1. 论文的核心问题与整体含义（研究动机和背景）
- **核心问题**：实际部署的差分隐私（DP）算法常因数学分析失误或实现瑕疵而无法提供宣称的隐私保护。经验审计可用于检测此类问题，但现有审计方法要么需要多次运行目标机制（如多次训练大型模型），计算成本极高；要么对隐私参数的计算“不紧致”，即审计得出的隐私界与真实隐私之间存在较大差距。
- **研究动机**：近期工作（Steinke et al., 2023）首次实现了单次训练运行即可审计，但其方法仅基于传统的 $(ϵ, δ)$-DP，导致审计结果过于保守（尤其在金丝雀数量增多时性能下降）。因此，需要一种既能保持单次运行的高效率，又能给出更紧致、更准确的隐私下界的方法。
- **整体含义**：本文提出并实现了一种基于 $f$-差分隐私（$f$-DP）的单次运行审计框架，利用更精细的隐私曲线替代点状的 $(ϵ, δ)$ 参数，显著缩小了经验隐私与理论隐私之间的差距，为实用隐私审计提供了更强大的工具。

### 2. 论文提出的方法论
- **核心思想**：不局限于一对 $(ϵ, δ)$，而是审计整个 $f$-DP 曲线（即机制完整的隐私权衡函数），从而在攻击者不同成功概率事件上都能给出紧致的界。
- **关键技术细节与流程**：
  - **猜测游戏（Guessing Games）**：推广了成员推理和重建攻击。审计者在数据集中注入一组金丝雀，每只金丝雀可有多选项（范围 $k$），对手只能作有限次猜测（不超过 $c'$ 次）。输出为猜测次数 $c'$ 和正确次数 $c$。
  - **核心定理（Theorem 3.1）**：对于满足 $f$-DP 的机制，给出了攻击者恰好猜对 $i$ 只金丝雀的概率 $p_i$ 的递推约束关系。关键不等式为：对任意索引子集 $T \subseteq [c']$，有
    \[
    \sum_{i \in T} \frac{i}{m} p_i \le \bar{f}\!\left( \frac{1}{k-1} \sum_{i \in T} \frac{c'-i+1}{m} p_{i-1} \right).
    \]
    该定理的推导结合了对单一金丝雀的条件概率界（Lemma A.1）以及通过随机排列消除条件依赖的巧妙技巧，是整个理论贡献的核心。
  - **数值审计算法（Algorithm 3）**：基于上述递推关系，设计了一个决策算法，给定观测到的 $(c, c')$、金丝雀数量 $m$、字母表大小 $k$ 以及候选 $f$ 曲线，判断攻击者成功次数 $\ge c$ 的概率是否 $\le \tau$（默认 $\tau=0.05$）。算法核心是通过逆推计算出概率上界，若上界超出允许范围则拒绝该隐私假说。
  - **经验隐私计算**：对一系列由强到弱排序的 $f$-DP 曲线（如不同噪声等级的高斯机制），找到未能被拒绝的最强隐私曲线，再将其转换为传统 $(ϵ(δ), δ)$ 表示的经验 $ϵ$。

### 3. 实验设计
- **场景与数据集**：
  - **理想化设定**：模拟高斯机制，直接计算最优攻击的期望正确猜测数，然后审计。主要考察不同噪声标准差（0.5, 1.0, 2.0, 4.0）下随金丝雀数量 $m$ 变化的表现。
  - **真实数据 DP‑SGD（CIFAR‑10）**：使用修改的 WRN‑16‑4 架构训练带有 DP 保证的模型。白盒攻击：审计者可观察所有中间梯度，使用梯度点积作为攻击分数；黑盒攻击：仅使用最终模型损失作为分数。金丝雀数量分别为 5000 和 1000。
  - **非私有模型 + 鲁棒成员推理攻击（RMIA）**：在 CIFAR‑10 和 Purchase（表格数据）上，用非私有训练模型，配合 SOTA 黑盒成员推理攻击进行审计，验证框架对最强攻击的适用性。
- **对比方法**：始终以 **Steinke et al. (2023)**（记为 SNJ）为主要基线，两者在完全相同的审计游戏中运行攻击，只在“评估阶段”采用不同分析方法。
- **评估指标**：在特定 $δ$ 下（通常 $δ=10^{-5}$）的经验 $ϵ$ 下界，越大说明审计越紧致。

### 4. 资源与算力
- 论文未明确提及所使用的 GPU 型号、数量或具体训练时长。实验部分仅描述了模型架构和训练超参数（如 CIFAR‑10 上用 batch size 4096、倍增因子 $K=16$、2500 步 DP‑SGD 等），未给出硬件资源消耗。因此，无法从文中直接获取算力信息。

### 5. 实验数量与充分性
- **实验组数丰富**：
  - 理想化高斯机制：4 种噪声 × 多组金丝雀数量（$10^2$∼$10^7$）的对比。
  - CIFAR‑10 白盒与黑盒审计、不同理论 $ε$ 下的表现，以及与 SNJ 的对比曲线。
  - 非私有模型上针对 RMIA 的审计效果。
  - 消融实验：探讨“桶大小” $k$（重建攻击中的选项数）、猜测次数 $c'$、不同 $δ$ 和置信水平对经验 $ϵ$ 的影响。
  - 附加对比：展示了若使用 SNJ 方法但针对 $(ϵ(δ), δ)$ 逐点审计的“多假说测试”版本，证明即便利用相同随机性，基于单点 $(ϵ, δ)$ 的审计仍远不如直接审计 $f$ 曲线。
- **充分性与公平性**：对比基线一致、游戏设定共用，仅分析方法不同，公平性强。多种攻击设定（白盒、黑盒、SOTA）和超参数消融保证了结论的鲁棒性。实验数量足以支撑其核心主张。

### 6. 论文的主要结论与发现
- 在单次运行前提下，利用 $f$-DP 曲线进行审计能够显著提升经验隐私的紧致性。
- 与 Steinke et al. (2023) 相比，本文方法不会随金丝雀数量增加而退化，反而能持续获得更接近理论值的经验 $ϵ$。这是因为规避了 $(ϵ, δ)$ 线性近似在多个事件上无法同时紧致的根本缺陷。
- 审计框架对成员推理和重建攻击均适用，且能泛化到 SOTA 攻击（如 RMIA）上，依然保持优势。
- 即使是改进后的多假说 $(ϵ, δ)$ 测试，其性能仍远不如直接审计完整 $f$ 曲线，进一步说明了使用精细隐私表征的必要性。

### 7. 优点
- **高效且紧致**：仅需一次训练运行，且审计下界比现有方法更靠近理论值，大幅降低计算开销。
- **理论与算法创新**：利用 $f$-DP 的凸分析、随机排列消除依赖的技巧，推导出高维攻击成功概率的递推约束，并给出数值稳定的审计算法。
- **通用性强**：猜测游戏可涵盖多种攻击形式，且框架可配合不同 $f$ 曲线族（如高斯机制族），适用于多种隐私审计场景。
- **实验透彻**：覆盖理想模拟、真实 DP 训练、非私有模型+SOTA 攻击，以及多维消融，论述有力。

### 8. 不足与局限
- **经验‑理论差距依然存在**：尽管相比前人有大幅提升，但审计结果与理论隐私值之间仍有一定差距（作者归因于数值算法中某些松弛，例如假设正确/错误猜测的条件期望比恰好为 $c/c'$ 的放松）。
- **审计仅提供经验下界**：该方法不能给出隐私保证的严格上界，只能作为一种实用的“下限估计”，而非证明机制满足某一隐私等级的正式方法。
- **依赖先验 $f$ 曲线族**：经验隐私的计算需要预设一族有序的 $f$-DP 曲线（如不同噪声的高斯曲线）。若真实机制的隐私行为不符合该族，审计可能产生偏差。
- **未讨论算力成本**：论文没有提供具体的硬件资源消耗，使得评估单次运行的实际工程开销缺乏数据支持。
- **攻击假设可能偏理想**：部分实验为“理想化”设定（正交金丝雀、最优攻击），现实中的攻击可能无法达到假设的期望正确数，这会影响审计的绝对准确性（但通常只会让审计更保守）。

（完）
