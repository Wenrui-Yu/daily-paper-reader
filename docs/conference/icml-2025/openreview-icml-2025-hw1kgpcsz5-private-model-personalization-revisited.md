---
title: Private Model Personalization Revisited
title_zh: 私有模型个性化再探
authors: "Conor Snedeker, Xinyu Zhou, Raef Bassily"
date: 2025-05-01
pdf: "https://openreview.net/pdf?id=hw1kGPcSZ5"
tags: ["query:daily"]
score: 9.0
evidence: 使用共享低维嵌入的用户级差分隐私联邦学习个性化
tldr: 针对用户数据异质的联邦个性化问题，本文在用户级差分隐私下重新审视共享表示框架。提出私有化FedRep算法，通过特定噪声机制保护用户隐私，同时学习共享嵌入和本地低维表示。理论证明其超额风险与高维参数维度无关，仅依赖于低维表示维度，在合成和真实数据上验证了隐私与效用兼得。
source: ICML-2025-Accepted
selection_source: conference_retrieval
figures_json: "[{\"url\": \"assets/figures/openreview/openreview-icml-2025-hw1kgpcsz5/fig-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 766, \"height\": 513, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-icml-2025-hw1kgpcsz5/fig-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 1025, \"height\": 764, \"label\": \"Figure\"}]"
motivation: 联邦个性化模型的用户级差分隐私研究不足。
method: 基于FedRep设计用户级DP算法，通过噪声扰动和低维表示控制隐私损失。
result: 获得维度无关的超额风险界，实验验证有效性。
conclusion: 该算法为隐私保护的联邦个性化提供了理论保障和实用方案。
---

## Abstract
We study model personalization  under user-level differential privacy (DP) in the shared representation framework. In this problem, there are $n$ users whose data is statistically heterogeneous, and their optimal parameters share an unknown embedding $U^* \in\mathbb{R}^{d\times k}$ that maps the user parameters in $\mathbb{R}^d$ to low-dimensional representations in $\mathbb{R}^k$, where $k\ll d$. Our goal is to privately recover the shared embedding and the local low-dimensional representations with small excess risk in the federated setting.  We propose a private, efficient federated learning algorithm to learn the shared embedding based on the FedRep algorithm in  (Collins et al.,
2021). Unlike  (Collins et al., 2021), our algorithm satisfies differential privacy, and our results hold for the case of noisy labels. In contrast to prior work on private model personalization (Jain et al., 2021), our utility guarantees hold under a larger class of users' distributions (sub-Gaussian instead of Gaussian distributions). Additionally, in natural parameter regimes, we improve the privacy error term in (Jain
et al., 2021) by a factor of $\widetilde{O}(dk)$. Next, we consider the binary classification setting. We  present an information-theoretic construction to privately learn the shared embedding and derive a  margin-based accuracy guarantee that is independent of $d$. Our method utilizes the Johnson-Lindenstrauss transform to reduce the effective dimensions of the shared embedding and the users' data. This result shows that dimension-independent risk bounds are possible in this setting under a margin loss.

---

## 论文详细总结（自动生成）

好的，以下是对论文《Private Model Personalization Revisited》的结构化、深入、客观的中文总结。

### 1. 论文的核心问题与整体含义

*   **研究问题**：论文聚焦于“模型个性化”（Model Personalization）问题，即在数据统计分布存在异质性（Heterogeneous）的多用户环境中，为每个用户训练定制化模型。
*   **隐私挑战**：该问题的核心挑战在于保护用户数据隐私。直接交换或集中处理原始数据会带来严重的隐私泄露风险。
*   **研究目标**：论文旨在设计一种算法，能够在保证严格**用户级别差分隐私（User-level DP）** 的前提下，利用所有用户的共享信息（一个低维嵌入矩阵），高效地学习到每个用户的个性化模型，并最小化其超额风险（Excess Risk）。
*   **整体含义**：本文为在隐私敏感且数据异构的联邦学习场景下，提供了一种理论保障更强、假设条件更宽松、实用性更高的模型个性化解决方案。

### 2. 论文提出的方法论

论文的核心方法论包括一个用于回归问题的私有联邦学习算法，以及一个用于分类问题的信息论构建。

#### 2.1 回归问题：私有化联邦表示学习算法 (Private FedRep)
*   **核心思想**：该算法是基于`FedRep`（Collins et al., 2021）的交替最小化（Alternating Minimization）框架。其核心是迭代更新共享的全局嵌入矩阵 `U` 和每个用户本地的表示向量 `v_i`。
*   **技术关键细节**：
    *   **离散数据批次与隐私保护**：用户每次迭代会抽取**不相交**的本地数据批次，分别用于更新本地向量和计算共享嵌入的梯度。此举有助于更紧地控制梯度范数，从而减少为保证差分隐私所需注入的噪声量。
    *   **隐私机制**：用户在本地计算完梯度后，将其发送给服务器。服务器对所有用户的梯度进行裁剪 (`clipping`) 后聚合，并注入校准后的高斯噪声，然后更新全局共享嵌入 `U`。这保证了用户级别DP。
    *   **梯度公式**：用户 `i` 在迭代 `t` 计算关于 `U` 的梯度 `∇_{i,t}`，其形式基于平方损失函数`ℓ = (y − x^T U v)^2`对 `U` 求导。服务器的更新规则为 `Û_{t+1} = U_t - η * (1/n * Σ_i clip(∇_{i,t}) + ξ_{t+1})`，其中 `ξ_{t+1}` 是高斯噪声。
    *   **私有初始化**：论文还设计了一个基于子空间恢复（Subspace Recovery）的私有初始化算法，通过对用户数据构造的统计量添加高斯噪声后进行SVD分解(Top-k SVD)，为 `FedRep` 提供一个良好的 `U_0`。

#### 2.2 分类问题：基于降维的构建
*   **核心思想**：将学习共享嵌入的问题视为训练一个2层线性神经网络，利用 Johnson-Lindenstrauss (JL) 变换进行降维，得到与原始数据维度 `d` 无关的风险界。
*   **关键技术细节**：
    *   **JL 变换**：矩阵 `M ∈ R^{k'×d}` (`k' ≪ d`) 将高维特征向量 `x` 映射为低维向量 `Mx`。
    *   **指数机制**：在低维空间中的一个覆盖集合 (cover) `N_γ` 上运行指数机制（Exponential Mechanism），根据一个基于间隔损失的评分函数选择一个最优的低维嵌入矩阵 `Ũ`。
    *   **最终模型**：高维空间的共享嵌入通过 `M^T Ũ` 重构得到，然后每个用户基于此计算个性化向量。

### 3. 实验设计

*   **数据集与场景**：论文通过**合成数据实验** (Synthetic Data Experiment) 对提出的算法进行了验证。
*   **场景设定**：
    *   用户数 `n = 20,000`。
    *   特征维度 `d = 50`，低维嵌入维度 `k = 2`。
    *   每用户样本数 `m = 10`。
    *   数据特征服从高斯分布 `N(0, I_d)`，标签噪声 `ζ` 服从 `N(0, R^2)`，其中 `R = 0.01`。
*   **对比基线方法 (Benchmarks)**：
    *   `Priv-AltMin`：(Jain et al., 2021) 提出的中心化隐私模型个性化算法。
    *   **Local GD (Non-Private)**：在本地数据上运行非隐私的梯度下降，作为非个性化的基线。
    *   **FedRep (Non-Private)**：原始的非隐私版 FedRep 算法，作为个性化效果的“天花板”。

### 4. 资源与算力

*   **文中未明确说明**：论文全文（包括正文和附录）**没有提及**任何关于实验所使用的 GPU 型号、GPU 数量、或训练总时长的具体信息。由于是合成数据实验，其算力需求相对较低，但作者未提供确切数据。

### 5. 实验数量与充分性

*   **实验数量**：论文报告了一项核心的合成数据实验，其结果绘制成图（Figure 1），展示了在不同隐私预算 `ϵ ∈ [1, 8]` 下，所提出算法与 `Priv-AltMin`、非隐私基线之间的**均方误差（MSE）** 比较。这相当于一组实验，包含三个算法在不同 `ϵ` 值下的性能曲线。
*   **充分性与客观性评估**：
    *   **不够充分**：实验**仅在一个**合成数据集和一组固定的问题参数（`n, d, k, m`）上进行。缺乏在真实世界数据集、不同参数规模（如 `n`、`m`、`k` 变化）以及更多对比算法下的消融实验和鲁棒性测试，这限制了其结论的普适性。
    *   **客观公平**：在单一设定下，对比的基线方法选择是合理和公平的，能够直接回应论文的理论贡献。

### 6. 论文的主要结论与发现

*   **回归问题**：提出的 `Private FedRep` 算法在 `n` 较大时，其超额风险界的隐私误差项比之前的最优工作（Jain et al., 2021）**改进了大约 `Õ(d/k)` 倍**。这在高维但低嵌入维度的情境下（即 `d ≫ k`）优势显著。
*   **假设条件放宽**：算法的效用保证成立的前提条件是数据分布为**次高斯（sub-Gaussian）**，而之前工作要求必须是**高斯**分布，适用范围更广。
*   **分类问题**：通过 JL 变换和指数机制，可以实现对二元分类问题的隐私保护模型个性化，并且得到了一种**与特征维度 `d` 无关**的、基于间隔（margin）的准确率保证。
*   **实验验证**：在合成数据实验中，`Private FedRep` 的表现**显著优于**中心化的 `Priv-AltMin`，且随着隐私预算 `ϵ` 增大，其性能能够接近非私有的 `FedRep` 基线。

### 7. 优点

*   **联邦与隐私的自然结合**：算法天然适配联邦学习场景（梯度本地算，服务器只聚合），同时满足了严格的用户级差分隐私，实用性更强。
*   **显著的理论提升**：在特定参数区域将隐私误差项改进了 `Õ(d/k)` 倍，并首次在私有模型个性化任务上得到了对分类问题的维度无关界。
*   **更宽松的假设**：将严格的“高斯数据”假设推广到更一般的“次高斯数据”假设，使其理论结果能覆盖更多实际应用场景。

### 8. 不足与局限

*   **实验验证薄弱**：仅在一个合成数据集上进行了对比实验，缺乏在**真实世界基准数据集**（如FEMNIST、CIFAR-10等联邦学习常用数据集）上的性能验证，这使得其实用性存疑。
*   **超参数敏感性未知**：算法的性能依赖于迭代轮数 `T`、学习率 `η`、裁剪阈值 `ψ` 以及隐私预算分配等众多超参数，论文未对这些超参数的影响进行充分的消融研究。
*   **协方差矩阵假设**：回归算法的分析仍然依赖于**单位协方差矩阵（Identity Covariance）** 的假设 (`Assumption 5`)，这在现实数据中很难成立，是一个较强的限制。
*   **损失函数限制**：有效的理论分析仅限于**平方损失（回归）** 和**0-1/间隔损失（分类）**，对于Logistic、Hinge等其他常用凸损失函数的扩展并非显而易见，文中将此列为开放问题。
*   **分类算法实用性**：分类算法虽然得到了维度无关的有效性界，但它是基于指数机制的**信息论构建**，相关效率较低，难以直接应用到大规模高维数据场景中。
*   **局部迭代次数**：`FedRep` 算法中，每个用户解决其本地参数 `v_i` 时，假设可以找到精确的最小化器（`arg min`），这在实践中通常需要通过多次梯度下降实现，但论文未讨论这部分迭代的隐私或计算成本。

（完）
