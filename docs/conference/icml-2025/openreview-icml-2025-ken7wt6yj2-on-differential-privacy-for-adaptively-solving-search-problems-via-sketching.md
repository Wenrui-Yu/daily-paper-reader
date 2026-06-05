---
title: On Differential Privacy for Adaptively Solving Search Problems via Sketching
title_zh: 通过草图技术为自适应搜索问题提供差分隐私
authors: "Shiyuan Feng, Ying Feng, George Zhaoqi Li, Zhao Song, David Woodruff, Lichen Zhang"
date: 2025-05-01
pdf: "https://openreview.net/pdf?id=kEn7Wt6Yj2"
tags: ["query:daily"]
score: 9.0
evidence: 差分隐私用于搜索问题
tldr: 针对差分隐私多用于数值估计问题而无法直接返回解的不足，本文将差分隐私引入自适应搜索问题，通过草图技术实现私密搜索，拓宽了DP的应用范围。
source: ICML-2025-Accepted
selection_source: conference_retrieval
tables_json: "[{\"url\": \"assets/tables/openreview/openreview-icml-2025-ken7wt6yj2/table-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 1371, \"height\": 215, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-icml-2025-ken7wt6yj2/table-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 1758, \"height\": 230, \"label\": \"Table\"}]"
motivation: 现有DP应用局限于数值估计，无法直接给出搜索问题的解。
method: 利用差分隐私和草图技术，隐藏内部随机性以支持自适应查询。
result: 实现了对搜索问题的私密自适应求解，且保证了正确性。
conclusion: DP可以成功应用于搜索问题，为数据结构隐私保护提供新思路。
---

## Abstract
Recently differential privacy has been used for a number of streaming, data structure, and dynamic graph problems as a means of hiding the internal randomness of the data structure, so that multiple possibly adaptive queries can be made without sacrificing the correctness of the responses. Although these works use differential privacy to show that for some problems it is possible to tolerate $T$ queries using $\widetilde{O}(\sqrt{T})$ copies of a data structure, such results only apply to {\it numerical estimation problems}, and only return the {\it cost} of an optimization problem rather than the solution itself. In this paper we investigate the use of differential privacy for adaptive queries to {\it search} problems, which are significantly more challenging since the responses to queries can reveal much more about the internal randomness than a single numerical query. We focus on two classical search problems: nearest neighbor queries and regression with arbitrary turnstile updates. We identify key parameters to these problems, such as the number of $c$-approximate near neighbors and the matrix condition number, and use different differential privacy techniques to design algorithms returning the solution point or solution vector with memory and time depending on these parameters. We give algorithms for each of these problems that achieve similar tradeoffs.

---

## 论文详细总结（自动生成）

## 1. 论文的核心问题与整体含义
近年来，差分隐私（DP）被广泛用于流处理、数据结构和动态图问题，以隐藏数据结构的内部随机性，从而在自适应查询下仍能保障响应正确性。现有工作通常仅能处理**数值估计问题**，返回的是目标**代价**而非解本身，且对每个问题需要准备 \(\widetilde{O}(\sqrt{T})\) 个数据结构的副本。本文进一步将差分隐私引入更具挑战性的**搜索问题**（需要输出具体的解点或解向量），重点研究两种经典问题：
- **近似最近邻（ANN）**：给定查询，需要返回一个具体的近似最近邻点。
- **回归问题（Regression）**：在允许任意（turnstile）更新的情况下，输出近似的回归系数向量。
核心目标是设计自适应鲁棒的数据结构，使其副本数量少于 \(\min\{d, T\}\)，并给出对关键参数（如近似近邻数量、矩阵条件数）依赖的分析。

## 2. 方法论
论文分别对 ANN 和回归问题提出了基于差分隐私的自适应算法，核心思路如下：

### 2.1 自适应 ANN：从蒙特卡洛搜索到差分隐私选择
- **基本框架**：将 \(k\) 个独立的 oblivious ANN 数据结构视为“数据库”行，每次查询采样 \(l = \widetilde{O}(s)\) 个副本，将这些副本返回的点集编码为二进制向量，再通过差分隐私的“报告一侧噪最大（Report Noisy Arg Max）”机制选出最频繁出现的点。
- **关键假设**：对于任意自适应查询 \(v\)，其 \(c\)-近似近邻数量不超过 \(s\)（即 \(|f_v(U)| \le s\)），这可比于常数膨胀、倍增维数更弱。
- **隐私放大与效用论证**：通过下采样实现隐私放大，利用高级组合定理使整个 \(T\) 步交互满足 \((\varepsilon,\delta)\)-DP；再利用 DP 的泛化性质证明大多数副本输出正确，最终保证有至少 \(\frac{3}{4}l\) 个副本成功，使得真实信号能够从拉普拉斯/指数噪声中脱颖而出。
- **加速：稀疏噪声与顺序统计**：观察到真实计数向量是 \(s\)-稀疏的，提出一个高效的**稀疏 argmax 机制**，只需生成 \(O(s\log n)\) 个与最大次序统计量对齐的指数噪声，避免对全部 \(n\) 个类别加噪，将查询时间从 \(\Omega(n)\) 降至 \(\widetilde{O}(s)\)。
- **批量更新**：对递减ANN（如在线匹配），通过按块更新和快速矩形矩阵乘法来加速 JL 变换和 LSH 更新，复杂度得到进一步改善。

### 2.2 自适应回归：私密中位数与 \(\ell_\infty\) 保证
- **坐标级私密中位数**：准备好 \(k = \widetilde{O}(\sqrt{T d})\) 个草图矩阵（Count Sketch + SRHT），对每次查询采样 \(s = \widetilde{O}(1)\) 个草图并求解相应的小规模回归，得到候选解向量 \(\{\mathbf{x}^{(i)}\}\)。对每个坐标单独调用差分私有中位数（Private Median），输出聚合向量 \(\mathbf{g}\)。
- **效用分析依赖 \(\ell_\infty\) 保证**：所用的 SRHT+Count Sketch 分布不仅提供子空间嵌入，还满足强 \(\ell_\infty\) 保证，即 \(\|\mathbf{x}^{(i)} - \mathbf{x}^*\|_\infty \le \frac{\alpha}{\sqrt{d}}\frac{\|\mathbf{U}\mathbf{x}^* - \mathbf{b}\|_2}{\sigma_{\min}(\mathbf{U})}\)。利用该保证和私有中位数的性质，可证明 \(\|\mathbf{U}\mathbf{g} - \mathbf{b}\|_2 \le (1 + \alpha)\min_{\mathbf{x}}\|\mathbf{U}\mathbf{x} - \mathbf{b}\|_2\)，代价是需将近似参数 \(\alpha\) 按条件数 \(\kappa\) 放缩。
- **去除条件数依赖**：当 \(\kappa\) 极大时，采用“有界计算路径”技术，根据所有可能的输出序列 \(|\mathcal{P}|\) 的数量生成一个足够大的高斯草图，并利用伪随机生成和舍入技术，使依赖从 \(\kappa^2\) 转为 \(\log|\mathcal{P}|\)。
- **稀疏标签漂移**：若设计矩阵 \(\mathbf{U}\) 固定，仅响应向量 \(\mathbf{b}\) 有稀疏更新，可先对 \(\mathbf{U}\) 做预处理降低条件数，并配合批处理重启草图，获得仅依赖于 \(\sqrt{T d}\) 和稀疏度 \(s\) 的更新复杂度。

## 3. 实验设计
**本文为纯理论论文，未包含任何实验部分。** 文中既没有列出数据集，也没有定义基准或对比方法，所有结果均以定理、复杂度和算法描述的形式呈现。

## 4. 资源与算力
**未提及任何 GPU 型号、数量、训练时长等算力信息。** 论文工作完全基于理论分析与算法设计，不涉及实验计算资源。

## 5. 实验数量与充分性
由于没有实验，不存在实验组数、消融实验或对比方法。文中通过两份表格（Table 1 和 Table 2）定性地给出了算法在空间、预处理、查询和更新时间上的理论比较，但未进行任何数值验证。

## 6. 论文的主要结论与发现
- 在 ANN 问题中，若查询的近似近邻数有界（\(s \le n^\rho\)），可用 \(\widetilde{O}(\sqrt{T} \cdot s)\) 个 oblivious 数据结构的副本响应 \(T\) 次自适应查询，空间和预处理时间均优于直接用 \(T\) 或 \(d\) 个副本的方案；查询时间仅增加 \(\widetilde{O}(s)\) 倍。
- 对于回归问题，当设计矩阵条件数有界时，可使用 \(\widetilde{O}(\sqrt{T d})\) 个草图副本实现自适应鲁棒解输出，查询时间极低（\(\widetilde{O}(d^{\omega+1}\kappa^2/\alpha^2)\)）；在移除条件数假设或利用计算路径技术时，也有相应改进。
- 将这些自适应数据结构应用于在线加权匹配、终端嵌入等，可获得更优的理论运行时间。

## 7. 优点
- **创新性强**：首次将差分隐私从数值估计推广到高维搜索问题，成功输出解点/向量。
- **框架通用**：将 ANN 问题巧妙地规约为差分隐私选择问题，并通过稀疏噪声算法提升效率。
- **参数化处理**：对 ANN 和回归分别引入自然结构参数（近似近邻数 \(s\)、条件数 \(\kappa\)），揭示了在这些温和假设下可获得的改进。
- **技术组合巧妙**：对回归问题结合了草图矩阵的 \(\ell_\infty\) 保证与坐标级私密中位数，利用“泛化性质”将隐私保证转化为效用保证。
- **应用案例丰富**：给出了在线匹配、终端嵌入等具体场景的分析，展示了方法的潜在影响。

## 8. 不足与局限
- **无实验验证**：作为纯理论研究，缺乏数值实验来支撑理论声称的常量隐藏、实际性能，无法评估在真实数据上的表现。
- **依赖性假设**：ANN 的有效性依赖每个查询点的近似近邻数不超过 \(s\)，这虽比倍增维数等假设弱，但在高密度区域可能失效，且需额外的计数数据结构定位“稀疏等级”；回归算法对条件数 \(\kappa\) 有二次依赖（除非使用有限路径技术，后者又依赖 \(|\mathcal{P}|\)）。
- **查询成本**：ANN 的查询时间放大了 \(s\) 倍，若 \(s\) 较大（接近 \(n^\rho\)），实用性下降；回归虽有快速查询时间，但更新及预处理仍涉及较大多项式因子。
- **有限路径技术的局限性**：当更新非常频繁或输出序列数目 \(|\mathcal{P}|\) 极大时，依赖 \(\log|\mathcal{P}|\) 的算法可能失去优势。
- **攻击分析有限**：仅在汉明空间结合 Kapralov et al. 的攻击给出了一个推论，对更一般的几何攻击鲁棒性缺乏深入讨论。

（完）
