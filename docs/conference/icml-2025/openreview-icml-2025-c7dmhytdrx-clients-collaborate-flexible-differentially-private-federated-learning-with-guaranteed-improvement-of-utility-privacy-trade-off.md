---
title: "Clients Collaborate: Flexible Differentially Private Federated Learning with Guaranteed Improvement of Utility-Privacy Trade-off"
title_zh: 客户端协作：灵活的差分隐私联邦学习及其效用-隐私权衡的改进保障
authors: "Yuecheng Li, Lele Fu, Tong Wang, Jian Lou, Bin Chen, Lei Yang, Jian Shen, Zibin Zheng, Chuan Chen"
date: 2025-05-01
pdf: "https://openreview.net/pdf?id=C7dmhyTDrx"
tags: ["query:daily"]
score: 9.0
evidence: 提出客户端协作的联邦学习框架，通过张量低秩优化改善差分隐私的效用-隐私权衡
tldr: 针对联邦学习中差分隐私加入噪声导致模型语义完整性受损且随通信轮次累积的问题，本文提出FedCEO框架。通过在服务器端对叠加的本地模型参数进行高效的张量低秩近端优化，灵活截断高噪声成分，从而在不牺牲隐私保障的前提下提升模型效用。实验证明该方法显著改善了隐私-效用的平衡，为隐私保护联邦学习提供了新思路。
source: ICML-2025-Accepted
selection_source: conference_retrieval
figures_json: "[{\"url\": \"assets/figures/openreview/openreview-icml-2025-c7dmhytdrx/fig-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 1663, \"height\": 731, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-icml-2025-c7dmhytdrx/fig-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 813, \"height\": 597, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-icml-2025-c7dmhytdrx/fig-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 848, \"height\": 334, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-icml-2025-c7dmhytdrx/fig-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 746, \"height\": 596, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-icml-2025-c7dmhytdrx/fig-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 1349, \"height\": 548, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-icml-2025-c7dmhytdrx/fig-006.webp\", \"caption\": \"\", \"page\": 0, \"index\": 6, \"width\": 1519, \"height\": 586, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-icml-2025-c7dmhytdrx/fig-007.webp\", \"caption\": \"\", \"page\": 0, \"index\": 7, \"width\": 1516, \"height\": 593, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-icml-2025-c7dmhytdrx/fig-008.webp\", \"caption\": \"\", \"page\": 0, \"index\": 8, \"width\": 1514, \"height\": 583, \"label\": \"Figure\"}]"
tables_json: "[{\"url\": \"assets/tables/openreview/openreview-icml-2025-c7dmhytdrx/table-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 1794, \"height\": 327, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-icml-2025-c7dmhytdrx/table-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 1601, \"height\": 432, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-icml-2025-c7dmhytdrx/table-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 1616, \"height\": 432, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-icml-2025-c7dmhytdrx/table-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 1104, \"height\": 327, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-icml-2025-c7dmhytdrx/table-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 1348, \"height\": 232, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-icml-2025-c7dmhytdrx/table-006.webp\", \"caption\": \"\", \"page\": 0, \"index\": 6, \"width\": 989, \"height\": 177, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-icml-2025-c7dmhytdrx/table-007.webp\", \"caption\": \"\", \"page\": 0, \"index\": 7, \"width\": 1422, \"height\": 387, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-icml-2025-c7dmhytdrx/table-008.webp\", \"caption\": \"\", \"page\": 0, \"index\": 8, \"width\": 1339, \"height\": 389, \"label\": \"Table\"}]"
motivation: 解决联邦学习差分隐私中噪声累积破坏模型效益的问题。
method: 提出FedCEO框架，通过张量低秩近端优化实现客户端参数协作。
result: 灵活截断高噪声成分，兼顾隐私保障与模型效用。
conclusion: 为联邦学习提供了一种改善隐私-效用权衡的有效方法。
---

## Abstract
To defend against privacy leakage of user data, differential privacy is widely used in federated learning, but it is not free. The addition of noise randomly disrupts the semantic integrity of the model and this disturbance accumulates with increased communication rounds. In this paper, we introduce a novel federated learning framework with rigorous privacy guarantees, named **FedCEO**, designed to strike a trade-off between model utility and user privacy by letting clients "***C**ollaborate with **E**ach **O**ther*". Specifically, we perform efficient tensor low-rank proximal optimization on stacked local model parameters at the server, demonstrating its capability to ***flexibly*** truncate high-frequency components in spectral space. This capability implies that our FedCEO can effectively recover the disrupted semantic information by smoothing the global semantic space for different privacy settings and continuous training processes. Moreover, we improve the SOTA utility-privacy trade-off bound by order of $\sqrt{d}$, where $d$ is the input dimension. We illustrate our theoretical results with experiments on representative datasets and observe significant performance improvements and strict privacy guarantees under different privacy settings. The **code** is available at https://github.com/6lyc/FedCEO_Collaborate-with-Each-Other.

---

## 论文详细总结（自动生成）

## 论文结构化总结

### 1. 核心问题与研究动机
- **背景**：联邦学习（FL）在保护用户隐私方面存在梯度泄露风险，差分隐私（DP）成为主要防御手段。然而，DP 的随机加噪会破坏模型的语义完整性，且噪声随着通信轮次累积，严重降低模型效用。
- **核心挑战**：如何在不牺牲隐私保障的前提下，提升差分隐私联邦学习（DPFL）的模型准确率，实现更好的效用–隐私权衡。
- **动机观察**：
  - 不同客户端受 DP 噪声破坏的语义信息存在差异，但客户端间的数据分布具有相似性，语义空间存在互补性。
  - 可视化实验表明：DP 噪声使全局语义空间平滑性下降，部分客户端在某类别上的准确率大幅下降；而通过平滑全局语义空间可以恢复这些客户端的性能。
  - 现有工作多聚焦于限制本地更新，忽视利用客户端间的语义协作来缓解噪声影响。

### 2. 方法论：FedCEO 框架
- **核心思想**：让客户端“相互协作”（Collaborate with Each Other），在服务器端通过张量低秩近端优化挖掘客户端参数的语义互补性，平滑被噪声破坏的全局语义空间。
- **关键技术细节**：
  - **参数堆叠**：每 $I$ 轮通信，服务器将 $K$ 个客户端的模型参数堆叠成一个三阶张量 $\mathcal{W}_N \in \mathbb{R}^{d \times h \times K}$（$d$ 为输入维度，$h$ 为模型宽度，$K$ 为参与客户端数）。
  - **优化目标**：$\hat{\mathcal{W}} = \arg\min_{\mathcal{W}} \left\{ \frac{\lambda}{\vartheta^{t/I}} \|\mathcal{W} - \mathcal{W}_N\|_F^2 + \|\mathcal{W}\|_* \right\}$，其中 $\|\cdot\|_*$ 为张量核范数（TNN），用于约束低秩性；正则化系数 $\frac{\lambda}{\vartheta^{t/I}}$ 随训练轮次 $t$ 呈几何级数增长（$\vartheta > 1$），实现**自适应平滑**。
  - **等价性与可解释性**：该优化问题等价于带自适应阈值的截断张量奇异值分解（T‑tSVD），即 $\text{T-tSVD}(\mathcal{W}_N, \frac{1}{2\tau})$（$\tau = \frac{\lambda}{\vartheta^{t/I}}$）。通过在傅里叶域的每个 frontal slice 对矩阵奇异值进行软阈值化，可**灵活截断高频分量**，保留低频分量，从而平滑全局语义空间。
  - **退化性质**：当截断阈值选择使得仅保留第一频率分量时，FedCEO 退化为近似 FedAvg（仅最低频协作）。
  - **隐私嵌入**：客户端本地执行用户级 DP（UDP）剪切加噪，服务器端的低秩优化为确定性后处理，不削弱隐私保障。
- **理论贡献**：
  - 效用上界：$\epsilon_u \le O(\frac{\sqrt{r} + \sqrt{d}}{K})$，当参数张量低秩时（$r \ll d$），$\epsilon_u \le O(\frac{\sqrt{d}}{K})$。
  - 隐私分析：满足用户级 $(\epsilon_p, \delta)$-DP，且 $\epsilon_p = \frac{c_2 K \sqrt{T\log(1/\delta)}}{N\sigma}$。
  - 综合权衡：$\epsilon_u \cdot \epsilon_p \le O(\frac{\sqrt{d}}{N})$，相比现有 SOTA 的 $O(d/N)$ 有 $O(\sqrt{d})$ 数量级的改进。

### 3. 实验设计
- **数据集**：
  - **图像分类**：EMNIST（MLP‑2 层）、CIFAR‑10（LeNet‑5，部分实验扩展至 MLP 在异构设置下、AlexNet）。
  - **文本情感分析**：Sent140（LSTM）。
- **对比方法**：
  - UDP‑FedAvg（基线用户级 DP‑FL，无效用改进）
  - PPSGD（个性化隐私 SGD，采用加性模型）
  - CENTAUR（服务器对单个客户端表示矩阵做 SVD）
  - FedCEO（含固定系数 $\vartheta=1$ 和自适应系数 $\vartheta>1$ 两个变体）
- **隐私设置**：所有方法均采用用户级 DP，噪声乘子对应 $\sigma_g = 1.0, 1.5, 2.0$，$\delta = 10^{-5}$。
- **评估指标**：
  - **效用**：全局模型测试准确率。
  - **隐私保护**：用 DLG 攻击反推训练图像，计算 PSNR（越低隐私越强）。
  - **权衡曲线**：不同 $\sigma_g$ 下的准确率变化。

### 4. 资源与算力
- **硬件**：实验使用 **单块 NVIDIA GeForce RTX 4090** 进行训练及运行时测量。
- **耗时**：
  - EMNIST (MLP‑2)：UDP‑FedAvg 约 5.436 小时，FedCEO 约 5.445 小时。
  - CIFAR‑10 (LeNet‑5)：UDP‑FedAvg 约 3.876 小时，FedCEO 约 3.908 小时。
  - PPSGD 和 CENTAUR 耗时均超过 24 小时，FedCEO 计算效率明显优于这两者，且仅略慢于无优化的 UDP‑FedAvg。

### 5. 实验的充分性与公平性
- **实验组数充足**：
  - 在 **2 个基准数据集（EMNIST、CIFAR‑10）** 上，针对 **3 种隐私强度**，对比 **3 个现有方法 + 2 个 FedCEO 变体**，形成至少 30 组主要结果。
  - 额外包括：隐私攻击实验（3 个隐私级别 × 3 种框架）、效用‑隐私权衡曲线、异构联邦设置（iid 与 non‑iid），不同模型架构（EMNIST 用 MLP，CIFAR‑10 用 LeNet、MLP、AlexNet，Sent140 用 LSTM），以及参数控制实验（间隔 $I$ 对准确率的影响）。
  - 超参数 $\lambda, \vartheta, I$ 通过网格搜索确定，搜索范围明确，鲁棒性较好。
- **公平性**：所有方法均采用用户级 DP 剪裁加噪，差别仅在服务器聚合/后处理策略。对比方法均来自 ICML/CVPR 等顶会，代表当时 SOTA。
- **充分性**：实验覆盖了同构与异构数据分布、不同模型容量、图像与文本模态，验证了方法的泛化能力。消融实验（固定 vs 自适应系数、不同操作间隔）也提供了方法内部的合理性支撑。

### 6. 主要结论与发现
- FedCEO 在所有测试设置下均取得了 **最高的测试准确率**，尤其在强隐私环境下（$\sigma_g=2.0$）优势更为显著。
- 服务器端张量低秩优化能 **有效恢复被 DP 噪声破坏的语义信息**，同时在 DLG 攻击下保持了与原 UDP‑FedAvg 相当的高隐私保护水平（PSNR 值接近）。
- 实现了 **更优的效用–隐私权衡**：相较于 CENTAUR 等 SOTA 方法，准确率随隐私增强的下降幅度更小，理论上的 $O(\sqrt{d})$ 改进得到实证支持。
- FedCEO 的训练开销较小，接近基础 UDP‑FedAvg，远优于 PPSGD 和 CENTAUR，实用性更强。

### 7. 优点
- **视角创新**：首次从**客户端间语义互补协作**的角度缓解 DP 噪声问题，区别于传统的本地约束或独立去噪方法。
- **理论基础扎实**：明确证明优化目标与 T‑tSVD 的等价性，并提供严格的效用上界、隐私保证以及整合后的权衡改进（量级提升）。
- **自适应与灵活性**：通过几何级数衰减的正则化系数，随训练进度和噪声水平自动调整平滑强度，无需手动干预。
- **高效率**：张量操作仅在服务器端进行，且频率为每 $I$ 轮，计算复杂度可控，实际运行时仅略高于基础 FedAvg，显著优于同类进阶方法。
- **实验全面**：覆盖多数据集、多模型、非独立同分布、异构性以及梯度泄露攻击，证据链完整。

### 8. 不足与局限
- **大规模模型的扩展性验证缺失**：论文提出可仅对最后几层做 T‑tSVD 以扩展到更大模型，但实验仅验证了 LeNet、MLP、AlexNet 等中小模型，未在 VLMs 或大型 ResNet 上测试。
- **超参数敏感性**：虽然搜索范围较窄且结论鲁棒，但 $\lambda$ 需根据隐私强度调整，$\vartheta$ 和 $I$ 也需微调，可能对全新任务需要额外调参成本。
- **攻击评估单一**：隐私实验仅采用 DLG 一种梯度反转攻击，未测试更先进的攻击方法（如基于生成模型的攻击），隐私保护强度的下限尚需更完善评估。
- **通信效率未讨论**：方法不增加通信次数，但张量构建与分解均发生在服务器，客户端的计算和通信开销未受影响，文中未专门量化，但已说明复杂度可接受。
- **理论假设**：效用分析基于强凸、光滑等假设，实际深度网络非凸，虽然可引入 FedProx 等处理，但当前分析仍有一定理想化。

---
（完）
