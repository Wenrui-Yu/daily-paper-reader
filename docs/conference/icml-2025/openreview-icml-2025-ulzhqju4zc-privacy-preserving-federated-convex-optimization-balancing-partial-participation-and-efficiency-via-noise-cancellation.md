---
title: "Privacy-Preserving Federated Convex Optimization: Balancing Partial-Participation and Efficiency via Noise Cancellation"
title_zh: 隐私保护联邦凸优化：通过噪声消除平衡部分参与和效率
authors: "Roie Reshef, Kfir Yehuda Levy"
date: 2025-05-01
pdf: "https://openreview.net/pdf?id=ULZHqJU4ZC"
tags: ["query:daily"]
score: 10.0
evidence: 通过噪声消除在部分参与下实现联邦凸优化的最优差分隐私
tldr: 联邦学习中部分参与场景下的差分隐私（DP）保障面临挑战。本文提出一种新颖的噪声消除机制，在随机凸优化框架下，通过特定噪声设计抵消部分参与带来的额外方差，实现最优收敛速度且不影响计算效率。理论分析与实验验证了该方法在齐次和异质数据下均达到最优性能，为联邦优化中的隐私与效率平衡提供了解决方案。
source: ICML-2025-Accepted
selection_source: conference_retrieval
tables_json: "[{\"url\": \"assets/tables/openreview/openreview-icml-2025-ulzhqju4zc/table-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 841, \"height\": 278, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-icml-2025-ulzhqju4zc/table-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 839, \"height\": 278, \"label\": \"Table\"}]"
motivation: 现有联邦凸优化DP方案在部分参与下性能下降或效率低。
method: 提出噪声消除机制，设计特定噪声结构以抵消部分参与引入的方差。
result: 在合成和真实数据上实现最优收敛速度，通信和计算效率高。
conclusion: 噪声消除方法为联邦凸优化中的部分参与隐私保护提供了理论和实践最优方案。
---

## Abstract
This paper addresses the challenge of achieving Differential Privacy (DP) in Federated Learning (FL) under the partial-participation setting, where each machine participates in only some of training rounds.
While earlier work achieved optimal performance and efficiency in full-participation scenarios, these methods could not extend effectively to cases with partial-participation.
Our approach addresses this gap by introducing a novel noise-cancellation mechanism that ensures privacy without compromising convergence rates or computational efficiency.
We analyze our method within the Stochastic Convex Optimization (SCO) framework and demonstrate that it achieves optimal performance for both homogeneous and heterogeneous data distributions.
This work broadens the applicability of DP in FL, providing a practical and efficient solution for privacy-preserving learning in distributed systems with partial participation.

---

## 论文详细总结（自动生成）

## 一、研究动机与核心问题

本文针对**联邦凸优化中部分参与（partial-participation）场景下的差分隐私（DP）保障**展开。在真实联邦学习中，每轮只有部分设备可用，如何在保护个体数据隐私的同时维持模型性能是一个关键挑战。以往工作要么仅在**全参与**场景下达到最优，要么在部分参与下牺牲了收敛速率或计算效率（例如复杂度高达 \(O(n^{3/2})\) 或 \(O(n^{9/8})\)）。本文旨在**填补这一空白**，提出一种既保证最优理论收敛速度又保持**线性计算复杂度**的隐私保护联邦优化方法。

---

## 二、方法论

### 2.1 核心思想

方法建立在 \(\mu^2\text{-SGD}\) 及其隐私扩展（DP-\(\mu^2\)-FL）之上，**核心创新是“噪声消除”机制**：每台参与设备在发出梯度修正时加入一个新噪声，同时减去上一轮自己加入的旧噪声，使服务器聚合时噪声相互抵消，最终仅余留当前轮的总新鲜噪声。这既保证了隐私，又有效控制了噪声累积。

### 2.2 关键技术细节与算法

- **梯度修正**：在第 \(t\) 轮，参与设备 \(i\) 计算  
  \[
  s_{t,i} = \alpha_t \nabla f_i(x_t; z_{t,i}) - \alpha_{t-1} \nabla f_i(x_{t-1}; z_{t,i})
  \]  
  其中 \(\alpha_t = t\) 为加权系数，\(z_{t,i}\) 为本地新样本。
- **噪声注入与消除**：设备生成本轮新噪声 \(y_{t,i} \sim \mathcal{N}(0, I\sigma_{t,i}^2)\)，并保存当前噪声 \(Y_i = y_{t,i}\)，上传  
  \[
  \tilde{s}_{t,i} = s_{t,i} + y_{t,i} - Y_i
  \]
- **服务器聚合**：服务器收集 \(\tilde{s}_{t} = \frac{1}{m}\sum_{i\in M_t}\tilde{s}_{t,i}\)，累加得到加权梯度估计 \(\tilde{q}_t = \tilde{q}_{t-1} + \tilde{s}_t\)，然后以此更新参数 \(w_t, x_t\)（采用类似 Anytime-GD 的加权平均更新规则）。
- **噪声方差调度**：每台设备的噪声方差 \(\sigma_{t,i}^2\) 与其到第 \(t\) 轮的累计参与次数 \(N_{t,i}\) 成正比，以平衡不同活跃度下的隐私与精度。

完整算法见 Algorithm 1（DP-\(\mu^2\)-FL with Partial-Participation）。理论分析证明该算法满足 \(\rho^2/2\text{-zCDP}\) 隐私，且收敛速率为  
\[
\mathcal{O}\left(\frac{1}{\sqrt{n}} + \frac{\sqrt{Md}}{\epsilon n}\right)
\]  
其中 \(n = mT\) 为总数据点，\(M\) 为总机器数，\(d\) 是模型维度，\(\epsilon\) 为隐私预算。该速率匹配不可信服务器场景下的已知下界，并且算法的计算复杂度与标准训练一致，为 \(\mathcal{O}(n)\)。

---

## 三、实验设计

- **数据集**：MNIST 手写数字分类，使用逻辑回归模型。
- **模型与参数**：问题维度 \(d = 7850\)，Lipschitz 常数 \(G = 39.6\)，光滑性常数 \(L = 392.5\)，定义域直径 \(D = 0.1\)。总数据用量固定为 \(n = 60,000\)，单次遍历数据。
- **对比方法**：
  - **Our Work**：本文提出的噪声消除方法。
  - **Noisy SGD**：受 Abadi et al. (2016) 启发，对梯度直接加噪的 SGD。
  - **Other Work**：Lowy & Razaviyayn (2023) 的 ISRL-DP 方法，达到最优界但复杂度为 \(O(n^{3/2})\)。
- **评测指标**：测试准确率与运行时间。
- **实验设置**：
  - **隐私水平消融**：固定 \(m = 50, M = 100\)，比较 \(\rho = 4, 8, 12\) 下的性能。
  - **参与机器数消融**：固定 \(\rho=8, M=100\)，比较 \(m = 20, 50, 80\) 的影响。

---

## 四、资源与算力

论文未明确说明实验所用的 GPU 类型、数量、内存等硬件资源，仅给出运行时间的相对数值（秒）。无法推断绝对算力需求。

---

## 五、实验数量与充分性

- 实验包含 **2 种消融**配置下的 3 种方法对比，共 6 组结果（见 Table 1、Table 2）。
- 实验仅在**单数据集、单模型（凸逻辑回归）**上进行，**未涉及非凸任务**（如深层网络）或多数据集（如 CIFAR-10、Sent140 等）验证。
- 比较的基准方法限于两种，没有包含更高效的最新工作（如 Gao et al. 2024 的 \(O(n^{9/8})\) 算法）。
- 实验可以初步验证所提方法的有效性和效率优势，但**覆盖度和泛化性验证尚不充分**，缺少在更复杂场景下的鲁棒性考察。

---

## 六、主要结论与发现

- 在相同总数据量下，**本文方法在准确率上接近或超过 Lowy & Razaviyayn (2023) 的最优方法**，尤其在中等隐私要求下表现突出。
- 运行时间远低于对比的“Other Work”，与简单的“Noisy SGD”相近，**体现了线性复杂度的实际收益**。
- 参与机器数 \(m\) 增大时，准确率趋势上升，符合理论预期，且对隐私预算 \(\rho\) 的影响更敏感。
- 实验印证了噪声消除机制在部分参与下既能**维持严格的 DP 保护**，又能**避免性能大幅下降**。

---

## 七、优点

- **理论完备**：在不可信服务器和部分参与下达到已知下限，同时保持计算复杂度与标准训练一致，这是该领域的首次突破。
- **设计新颖**：通过本地记录并抵消上次噪声的方式，缓解了部分参与带来的额外方差，原理简洁清晰。
- **实现简单**：算法流程仅需对梯度修正做两次梯度计算和一次噪声注入，适合实际部署。
- **分析严谨**：给出了隐私和收敛的完整证明，噪声方差依据参与次数调整，理论依据充分。

---

## 八、不足与局限

- **实验局限性明显**：仅在 MNIST + 逻辑回归这一个简单场景下验证，未展示在更复杂模型或非凸问题上的表现。
- **隐私模式单一**：依赖 zCDP 框架，未探讨与其他 DP 机制（如 ADP、Local DP）的结合。
- **假设较强**：要求目标函数凸且光滑，实际联邦学习常处理非凸神经网络，直接推广存在困难。
- **样本使用假设**：每台机器每轮仅使用一个新样本，可能不适合需要多轮本地更新的联邦优化变体（如 FedAvg）。
- **缺乏更多 SOTA 对比**：未将 Gao et al. (2024) 等改进方法作为基准，对比说服力稍弱。

（完）
