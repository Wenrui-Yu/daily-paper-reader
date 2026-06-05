---
title: Convergent Differential Privacy Analysis for General Federated Learning
title_zh: 通用联邦学习的收敛差分隐私分析
authors: "Yan Sun, Qixin Zhang, Li Shen, Dacheng Tao"
date: 2025-05-06
pdf: "https://openreview.net/pdf?id=W8TB5rmbk1"
tags: ["query:daily"]
score: 9.0
evidence: 针对通用联邦学习的收敛差分隐私分析，超越标准组合的紧界，解决分布式机器学习中的隐私问题
tldr: 针对联邦学习中差分隐私组合定理导致的隐私界发散问题，提出收敛性隐私分析方法，得到长期训练下仍紧的隐私界，弥合理论与实验差距，验证FL-DP的可靠性。
source: NeurIPS-2025-Rejected-Public
selection_source: conference_retrieval
motivation: 标准组合定理在FL-DP中导致长期训练下隐私界发散，无法正确评估隐私。
method: 提出全面的收敛性隐私分析框架，利用新型隐私损失度量。
result: 证明在恒定噪声下，FL-DP的隐私保障最终收敛，保障长期训练的隐私。
conclusion: 收敛性分析为FL-DP的长期隐私可靠性提供了理论支持。
---

## Abstract
The powerful cooperation of federated learning (FL) and differential privacy (DP) provides a promising paradigm for the large-scale private clients. However, existing analyses in FL-DP mostly rely on the composition theorem and cannot tightly quantify the privacy leakage challenges, which is tight for a few communication rounds but yields an arbitrarily loose and divergent bound eventually. This also implies a counterintuitive judgment, suggesting that FL-DP may not provide adequate privacy support during long-term training under constant-level noisy perturbations, yielding discrepancy between the theoretical and experimental results. To further investigate the convergent privacy and reliability of the FL-DP framework, in this paper, we comprehensively evaluate the worst privacy of two classical methods under the non-convex and smooth objectives based on the $f$-DP analysis. With the aid of the shifted interpolation technique, we successfully prove that privacy in {\ttfamily Noisy-FedAvg} has a tight convergent bound. Moreover, with the regularization of the proxy term, privacy in {\ttfamily Noisy-FedProx} has a stable constant lower bound. Our analysis further demonstrates a solid theoretical foundation for the reliability of privacy in FL-DP. Meanwhile, our conclusions can also be losslessly converted to other classical DP analytical frameworks, e.g. $(\epsilon,\delta)$-DP and R$\acute{\text{e}}$nyi-DP~(RDP), to provide more fine-grained understandings for the FL-DP frameworks.

---

## 论文详细总结（自动生成）

好的，作为一名资深学术论文分析助手，我将以 Markdown 格式，对提供论文进行结构化、深入且客观的中文总结。

### **1. 论文的核心问题与整体含义**

*   **研究背景与动机**：联邦学习（FL）与差分隐私（DP）的结合为大规模隐私保护提供了强有力的范式。然而，现有的 FL-DP 分析大多依赖组合定理，这种分析方法在通信轮次较少时尚可，但随着长期训练，会推导出一个**任意宽松且发散的隐私界**（Privacy Bound）。
*   **核心矛盾**：这一发散的隐私界导致了一个违反直觉的判断：在恒定强度的噪声扰动下，长期的联邦学习可能无法提供足够的隐私保护。这与实证经验相矛盾，揭示出理论与实验之间的显著差距。
*   **研究目标**：本文旨在解决此矛盾，为通用的 FL-DP 框架建立**收敛的**（而非发散的）隐私分析理论，尤其是在非凸光滑目标函数下，填补该领域的理论空白，为 FL-DP 长期隐私保护的可靠性奠定坚实的理论基础。

### **2. 论文提出的方法论**

*   **核心分析框架**：论文基于**f-DP分析**（一种信息论无损的DP定义），以假设检验中 Type I/II 错误的 trade-off 曲线来精细衡量隐私，避免了传统(ϵ, δ)-DP 等定义中的松弛。
*   **关键技术一：移位插值**
    *   为避免传统方法中因重复的隐私放大导致界发散的问题，论文采用 **移位插值** 技术。
    *   **核心思想**：构造一个从相邻数据集上的模型状态 `w_t` 和 `w'_t` 开始的插值序列 `e_w_t`，该序列在最后的通信轮次收敛到目标模型 `w_T`。这使得隐私分析可以在一个缩短的“放大路径”上完成，从而获得更紧的界。
    *   **定理**：论文将此过程的隐私下界表述为取决于从 `t0` 到 `T` 轮全局敏感度加权和的 GDP (高斯差分隐私) 函数。
*   **关键技术二：全局敏感度分解**
    *   为解决多步本地更新带来的分析挑战，论文将全局更新函数的敏感度 `∥ϕ(wt) - ϕ(e_wt)∥` 拆解为两部分：
        *   **数据敏感度**：由在不同数据集上训练导致的差异。
        *   **模型敏感度**：由在不同初始模型上训练导致的差异。
    *   通过这种分解，论文成功地对 `Noisy-FedAvg` 和 `Noisy-FedProx` 两种方法在不同学习率策略下的敏感度进行了精细的界定。
*   **收敛性证明**：
    *   通过求解一个关于插值系数 `λt` 的**最优化问题**，论文证明了通过精心选择 `λt`，可以缩放敏感度项，从而得到不随通信轮次 T 发散，而是**收敛至一个常数上界**的隐私下界。
    *   **Noisy-FedAvg**：论文分析了在恒定、循环衰减、阶段衰减和连续衰减四种学习率策略下的最差隐私，并证明其均可收敛。
    *   **Noisy-FedProx**：论文证明了由于其代理项的正则化作用，其模型敏感度系数小于1，这使得其最差隐私可以**不受本地更新步数 K 的影响，并收敛到一个稳定的常数下界**，比 Noisy-FedAvg 具有更优的隐私特性。

### **3. 实验设计**

*   **数据集与模型**：
    *   **数据集**：在 MNIST 和 CIFAR-10 基准数据集上进行实验。
    *   **模型**：分别使用 LeNet-5 和 ResNet-18 模型来匹配数据集。
*   **场景设定**：
    *   实验遵循标准的联邦学习设置，通过 **Dirichlet 分布**（Dir-0.1）划分数据，以引入较高的数据异构性。
    *   主要的变动参数包括：客户端规模 `m` (50, 100)、本地更新间隔 `K` (50, 100, 200) 以及噪声强度 `σ` (1.0, 10⁻¹, 10⁻², 10⁻³)。
*   **对比基准**：
    *   实验对比了 **Noisy-FedAvg** 和带有不同近端系数 **α** (0.01, 0.1, 1) 的 **Noisy-FedProx** 方法，旨在验证理论分析中关于正则化项能提升隐私性能的结论。

### **4. 资源与算力**

*   论文在其提供的文本内容中，**完全没有提及**所使用 GPU 的型号、数量或具体的训练时长等算力信息。

### **5. 实验数量与充分性**

*   **实验组别**：
    *   **性能对比实验**：测试了 2 个数据集 × 2 个客户端规模 × 3 个本地间隔 × 4 种噪声强度的组合，总计 48 组实验。每组实验重复 5 次报告均值和方差。
    *   **敏感度消融研究**：针对 `Noisy-FedAvg`，分别变化客户端规模 `m`、本地间隔 `K`、裁剪范数 `V` 来研究敏感度的变化；针对 `Noisy-FedProx`，变化近端系数 `α` 来研究其对敏感度的影响。
*   **充分性与客观性**：
    *   **充分性**：实验覆盖了关键的超参数（m, K, V, α, σ），并通过消融研究验证了理论推导中关于这些参数对灵敏度影响的结论，与理论分析高度一致，实验设计较为充分。
    *   **客观性与公平性**：在验证不同方法性能时（如 Table 5），论文保持了总通信轮次和本地间隔的乘积（T×K）不变，这在联邦学习中是对比不同 K 时常见的公平比较设置。实验结果汇报了均值和方差，增强了可信度。

### **6. 论文的主要结论与发现**

*   **理论核心**：首次在非凸光滑目标下，证明了 FL-DP 范式（Noisy-FedAvg, Noisy-FedProx）具有**收敛的隐私界**，成功挑战了“隐私预算必然随训练轮次增加”的长期认知。
*   **Noisy-FedAvg 隐私特性**：其隐私性能受裁剪范数 V、本地间隔 K、客户端规模 m 和噪声 σ 影响，但在合适的配置下，即使在恒定噪声下，其隐私下界也会收敛。
*   **Noisy-FedProx 隐私优越性**：证明通过引入近端正则化项，可以消除本地更新步数 K 对隐私的不利影响，并获得一个更优的常数级隐私下界，实现了**优化与隐私的双赢**。
*   **实验验证**：实验结果表明，理论分析预测的敏感度界限与实际观察高度吻合，验证了理论的正确性，并证实了 Noisy-FedProx 在隐私保护上相对 Noisy-FedAvg 的优势。

### **7. 优点**

*   **理论创新性强**：首次为非凸联邦学习中的 DP 提供了收敛性分析，填补了重要的理论空白。
*   **方法论严谨**：采用信息论无损的 f-DP 框架，并结合巧妙的移位插值和敏感度分解技术，所得结论具有高度精确性，且能无损转换到其他 DP 框架。
*   **洞察深刻**：不仅分析了 Noisy-FedAvg，还通过 Noisy-FedProx 的分析，深刻揭示了**近端正则化项在联邦学习隐私保护中的积极作用**，为算法设计提供了新的视角。
*   **理论与实践统一**：通过收敛性的理论结果，弥合了传统理论在长期训练中与现实观测结果的矛盾，为 FL-DP 的可靠性提供了有力担保。

### **8. 不足与局限**

*   **假设限制**：
    *   分析基于**非凸但 L-光滑**的目标函数假设，未覆盖更复杂的非光滑场景。
    *   对 Noisy-FedProx 的分析要求近端系数 **α > L**，这是一个较强的假设，在实际应用中可能需要精细调参。
*   **实验覆盖**：
    *   实验仅在图像数据集（MNIST, CIFAR-10）和两种模型上进行，未涉及 NLP 或其他领域的数据及模型（如 Transformer 等），通用性的实验验证有待加强。
    *   未汇报算力开销，无法评估该分析方法的计算成本或实验的复现效率。
*   **理论局限**：
    *   文中明确指出，分析方法目前**不能直接扩展到稳定性分析**，即无法从隐私下界直接推导出收敛性所需的稳定性界，这是其理论能力的一个边界。
*   **优化与隐私的权衡**：虽然指出了 Noisy-FedProx 中 α 的“双赢”特性，但 α 的选取仍是在优化精度和隐私强度（文中 Table 5 显示 α=1 时精度下降）之间的一个**不易权衡**的超参数，缺乏自适应或指导性的选取策略。

（完）
