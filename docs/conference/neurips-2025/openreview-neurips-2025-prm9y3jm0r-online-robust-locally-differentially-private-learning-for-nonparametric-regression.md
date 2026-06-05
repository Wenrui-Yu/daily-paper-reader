---
title: Online robust locally differentially private learning for nonparametric regression
title_zh: 在线鲁棒本地差分隐私非参数回归学习
authors: "Chenfei Gu, Qiangqiang Zhang, Ting Li, Jinhan Xie, Niansheng Tang"
date: 2025-09-18
pdf: "https://openreview.net/pdf?id=prm9Y3jM0R"
tags: ["query:daily"]
score: 8.0
evidence: 在线鲁棒本地差分隐私非参数回归学习，直接解决隐私机器学习问题
tldr: 针对流式数据中非参数回归的隐私和鲁棒性挑战，提出基于Huber损失的在线功能随机梯度下降（H-FSGD），进而扩展为本地差分隐私版本PH-FSGD，实现实时隐私保护估计，并提供非渐近收敛分析。
source: NeurIPS-2025-Accepted
selection_source: conference_retrieval
figures_json: "[{\"url\": \"assets/figures/openreview/openreview-neurips-2025-prm9y3jm0r/fig-001.webp\", \"caption\": \"\", \"page\": 3, \"index\": 1, \"width\": 616, \"height\": 544}, {\"url\": \"assets/figures/openreview/openreview-neurips-2025-prm9y3jm0r/fig-002.webp\", \"caption\": \"\", \"page\": 3, \"index\": 2, \"width\": 388, \"height\": 620}]"
motivation: 传统非参数回归难以适应在线、隐私保护场景，且对异常值敏感。
method: 设计Huber损失引导的在线功能随机梯度下降（H-FSGD），并引入本地差分隐私机制（PH-FSGD）。
result: 理论证明PH-FSGD在异常值和隐私约束下仍保持收敛，实验验证有效性。
conclusion: 提供了一种实时鲁棒且隐私保护的非参数回归方案。
---

## Abstract
The growing prevalence of streaming data and increasing concerns over data privacy pose significant challenges for traditional nonparametric regression methods, which are often ill-suited for real-time, privacy-aware learning. In this paper, we tackle these issues
by first proposing a novel one-pass online functional stochastic gradient descent algorithm that leverages the Huber loss (H-FSGD), to improve robustness against outliers and heavy-tailed errors in dynamic environments. To further accommodate privacy constraints, we introduce a locally differentially private extension, Private H-FSGD (PH-FSGD), designed to real-time, privacy-preserving estimation. Theoretically, we conduct a comprehensive non-asymptotic convergence analysis of the proposed estimators, establishing finite-sample guarantees and identifying optimal step size schedules that achieve optimal convergence rates. In particular, we provide practical insights into the impact of key hyperparameters, such as step size and privacy budget, on convergence behavior. Extensive experiments validate our theoretical findings, demonstrating that our methods achieve strong robustness and privacy protection without sacrificing efficiency.

---

## 论文详细总结（自动生成）

好的，以下是基于论文内容的中文结构化总结。

### 1. 论文的核心问题与整体含义

*   **研究背景**：在流数据（如自动驾驶、传感器网络）普遍化和数据隐私日益受重视的背景下，传统的非参数回归方法面临三大挑战：
    *   **在线学习需求**：数据实时顺序到达，无法一次性存储并处理整个数据集。
    *   **隐私保护需求**：原始数据可能包含敏感信息，需要在不依赖可信第三方的前提下进行保护。
    *   **鲁棒性需求**：复杂动态环境中的数据常包含异常值或呈现重尾分布，传统基于最小二乘的方法容易失效。
*   **核心问题**：设计一种**在线、隐私保护、且对重尾噪声鲁棒的**非参数回归算法，同时不牺牲统计效率。
*   **整体含义**：本文旨在解决上述挑战，提出一个新框架，在再生核希尔伯特空间（RKHS）中，实现满足本地差分隐私（LDP）的单次遍历在线鲁棒估计。

### 2. 论文提出的方法论

**核心思想**：利用Huber损失函数替代平方损失，实现在线功能随机梯度下降（FSGD），并进一步引入高斯过程噪声以满足本地差分隐私（LDP）。

*   **Huber损失函数 (`L_τ`)**：
    *   **定义**：结合了平方损失（对小残差）和绝对损失（对大残差）的优点。`L_τ(u) = 1/2 * u² * I(|u| ≤ τ) + (τ|u| - 1/2 τ²) * I(|u| > τ)`。
    *   **作用**：其梯度有界（最大为 `τ`），不仅天然抵抗异常值和重尾噪声，还确保了后续添加的隐私噪声可被精确校准，无需额外梯度裁剪。
*   **算法流程**：
    1.  **H-FSGD（非隐私）**：在每收到一个新样本 `(X_n, Y_n)` 时，利用当前估计 `f̂_{n-1}` 和Huber损失的Fréchet梯度（公式 4）进行一次梯度下降更新，得到 `f̂_n`。然后，通过对历次迭代的估计进行Polyak平均，得到更稳定的估计 `f̄_n`（公式 5）。
    2.  **PH-FSGD（本地差分隐私）**：引入隐私保护机制。`f̂_n` 的更新项中增加一个**经过校准的高斯过程噪声 `γ_n * ξ_n`**（公式 7）。噪声的协方差函数与隐私预算 `(ε_n, δ_n)` 和梯度敏感度 `(2τB)` 直接相关。
    3.  **隐私保障**：该算法被证明在每个迭代步骤都满足 `(max ε_n, max δ_n)`-LDP（定理 1），即个体数据在源头就被加噪保护。

*   **关键超参数选择**：
    *   `τ`（Huber参数）：通过一个基于中位数绝对离差（MAD）的初始鲁棒估计量来数据驱动地选择。
    *   `γ_n`（步长）：理论分析提供了在不同函数光滑性 (`r`, `α`) 下的最优常数或衰减步长方案（推论 1, 3），以实现最优收敛速度。

### 3. 实验设计

*   **数据集/场景**：
    *   **合成数据**：模拟两个真实函数 `f*(x)`，一个是简单的正弦函数（Case 1），另一个是复杂的Beta密度函数组合（Case 2）。
    *   **噪声模型**：测试了轻尾（`N(0, 0.25)`）和重尾（`t(3)`, `t(2.5)`, 甚至无穷方差的 `Cauchy(0,1)`）噪声。还测试了Huber的 `ε*`-污染模型。
    *   **真实数据**：使用Kaggle上的“健康与健身数据集”进行验证。
*   **对比方法**：
    *   L2-FSGD：基于平方损失的在线FSGD。
    *   Offline：基于平方损失的一次性离线核岭回归。
    *   **自身变体**：比较非隐私H-FSGD与不同隐私强度（`(3,0.1)-LDP`, `(2,0.2)-LDP`）下的PH-FSGD。
*   **评估指标**：主要使用均方误差（MSE）评估函数估计精度，用箱线图展示多次重复实验的分布，并绘制了拟合函数图。

### 4. 资源与算力

*   **文中描述**：论文在“计算时间”部分提到，实验在一台配备 **3.20 GHz AMD Ryzen 7 5800H CPU 和 16GB RAM** 的笔记本电脑上运行。
*   **分析**：此任务未使用GPU。实验展示了所提出的H-FSGD和PH-FSGD方法具有**线性时间复杂度 `O(n)`**，而对比的离线方法为立方复杂度 `O(n³)`，计算效率优势明显，单机CPU即可胜任。

### 5. 实验数量与充分性

*   **实验数量**：实验覆盖了**非隐私和隐私两种设置**，两种**真实函数场景**，多种**噪声类型**（包括重尾和异常值污染），两种**步长策略**（常数与非常数），并测试了**不同样本量**（n = 2000 到 40000）下的表现。
*   **充分性与客观性**：实验设计较为充分，覆盖了核心理论假设内外的多种场景。每个实验重复**200次**并报告MSE的分布，保证了统计显著性。
*   **消融/敏感性分析**：通过热图形式研究了关键超参数 `γ₀` 和 `ζ` 对算法性能的影响，表明方法在较宽参数范围内均稳定。

### 6. 论文的主要结论与发现

*   **鲁棒性**：H-FSGD和PH-FSGD在重尾噪声（如`t(3)`，`Cauchy`）和异常值污染下，显著优于基于平方损失的基线方法（L2-FSGD, Offline），尤其是在小样本情况。
*   **隐私-效用的权衡**：PH-FSGD以增加估计方差为代价实现LDP，更强的隐私保护（更小的`ε`）会导致更大的MSE。但这种精度损失可通过**增加样本量**有效弥补。
*   **收敛性与最优性**：理论证明，在合适的步长选择下，所提方法的收敛速度在多种光滑性设定下均达到**极小极大最优**。
*   **计算效率**：作为单次遍历算法，H-FSGD/PH-FSGD计算复杂度为`O(n)`，远低于离线方法的`O(n³)`。

### 7. 优点

*   **问题新颖**：首次在同个框架下同时解决在线非参数回归的鲁棒性、本地差分隐私和计算效率问题，填补了研究空白。
*   **方法论契合**：巧妙利用Huber损失的有界梯度特性，“一石二鸟”地解决了鲁棒性和LDP的敏感度校准问题，设计精巧。
*   **理论扎实**：提供了全面的非渐进收敛性分析，清晰阐述了步长、隐私预算及函数空间光滑性对收敛速度的影响，并给出了最优步长选择方案。
*   **实践指导性强**：实验验证了理论，并展示了方法在极端重尾噪声下的经验鲁棒性，还讨论了其在医疗、金融等领域的应用前景。

### 8. 不足与局限

*   **隐私机制的单一性**：仅探索了高斯机制实现LDP，未探讨如拉普拉斯机制或指数机制等其他可能更适合特定场景的隐私保护方法。
*   **损失函数的限制**：方法基于Huber损失，未能拓展到更广泛的M-估计族，限制了其在其他鲁棒性场景下的通用性。
*   **理论的局限性**：理论分析假设噪声具有有限方差，尽管实验证明对无穷方差（如Cauchy）也有效，但缺乏严格的理论保证。同时，理论未显式考虑网格离散化引入的近似误差。
*   **应用场景局限**：方法设计基于独立同分布（i.i.d.）假设，尚未扩展到存在概念漂移或非i.i.d.的现实动态流数据环境中。

（完）
