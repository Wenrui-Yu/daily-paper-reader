---
title: Differentially Private Relational Learning with Entity-level Privacy Guarantees
title_zh: 具有实体级隐私保证的差分隐私关系学习
authors: "Yinan Huang, Haoteng Yin, Eli Chien, Rongzhe Wei, Pan Li"
date: 2025-09-18
pdf: "https://openreview.net/pdf?id=MZ25Rt5DiP"
tags: ["query:daily"]
score: 5.0
evidence: 关系学习的差分隐私，未明确体现分布式
tldr: 针对关系数据中实体级隐私保护难题，提出一种系统的差分隐私关系学习框架，解决了实体参与多关系导致的高敏感度以及多阶段耦合采样带来的隐私分析挑战。该框架适用于图神经网络等结构化学习任务，为敏感网络数据的隐私保护模型训练提供了新方案。
source: NeurIPS-2025-Accepted
selection_source: conference_retrieval
motivation: 关系学习在敏感领域应用广泛，传统DP-SGD因关系耦合和敏感度难以直接应用于实体级隐私保护。
method: 提出原则性的差分隐私关系学习框架，通过控制敏感度和设计适配采样过程来满足实体级DP。
result: 框架在多个图数据集上实现了有效的隐私保护，同时保持较好的模型效用。
conclusion: 为关系数据的实体级隐私保护提供了系统性的解决方案。
---

## Abstract
Learning with relational and network-structured data is increasingly vital in sensitive domains where protecting the privacy of individual entities is paramount. Differential Privacy (DP) offers a principled approach for quantifying privacy risks, with DP-SGD emerging as a standard mechanism for private model training. However, directly applying DP-SGD to relational learning is challenging due to two key factors: (i) entities often participate in multiple relations, resulting in high and difficult-to-control sensitivity; and (ii) relational learning typically involves multi-stage, potentially coupled (interdependent) sampling procedures that make standard privacy amplification analyses inapplicable. This work presents a principled framework for relational learning with formal entity-level DP guarantees. We provide a rigorous sensitivity analysis and introduce an adaptive gradient clipping scheme that modulates clipping thresholds based on entity occurrence frequency. We also extend the privacy amplification results to a tractable subclass of coupled sampling, where the dependence arises only through sample sizes. These contributions lead to a tailored DP-SGD variant for relational data with provable privacy guarantees. Experiments on fine-tuning text encoders over text-attributed network-structured relational data demonstrate the strong utility-privacy trade-offs of our approach.

---

## 论文详细总结（自动生成）

好的，请看以下对论文《Differentially Private Relational Learning with Entity-level Privacy Guarantees》的结构化总结。

### 1. 论文的核心问题与整体含义

*   **研究动机与背景**：在金融、医疗等敏感领域，利用实体间的关系数据（图数据）进行机器学习至关重要。差分隐私是保护个体数据隐私的黄金标准，DP-SGD 是训练深度学习模型的标准隐私保护方法。
*   **核心问题**：传统的 DP-SGD 无法直接应用于关系学习，面临两个根本性挑战：
    1.  **高敏感度**：一个实体（节点）可以参与多个关系（边），导致移除该实体会影响模型梯度中的多个损失项，使得敏感度极高且难以控制。
    2.  **耦合采样**：关系学习中的小批量构建通常包含多阶段、相互依赖的采样过程（如先采样正边，再基于正边采样负边），这使得标准的“通过子采样进行隐私放大”分析不再适用。
*   **整体含义**：本文旨在建立一个原则性的框架，为关系学习提供正式的**实体级差分隐私**保障，解决上述两大挑战，实现隐私与模型效用之间的良好权衡。

### 2. 方法论

*   **核心思想**：通过设计一种自适应的梯度裁剪策略来控制因实体出现在多个关系中导致的高敏感度，并将复杂的多阶段采样重新形式化为一种可分析的“基数依赖耦合采样”，从而推导出严格的隐私放大边界，最终得到一个适配关系数据的、具有可证明隐私保证的 DP-SGD 变体。
*   **关键技术细节**：
    1.  **敏感度分析与自适应裁剪**：
        *   **问题建模**：定义了相邻小批量数据（移除一个节点及其所有关联边）下的局部敏感度。移除节点 `u*` 的敏感度受其出现的正边 `B+(u*)` 和负边 `B-(u*)` 数量共同影响，最坏情况下敏感度极高。
        *   **自适应裁剪策略**：提出不固定裁剪阈值，而是根据一个节点在小批量中出现的频率动态调整裁剪阈值。出现频率越高，对其梯度项的裁剪越强。
        *   **策略实现**：公式上，对边元组 `\(T_i\)` 的梯度 `\(g(T_i)\)` 进行裁剪 `\(\bar{g}(T_i) = g(T_i) / \max(1, \|g(T_i)/C(T_i, B)\|)\)`，其中动态阈值 `\(C(T_i, B)\)` 与该元组中节点的出现频率 `\(sup_{u \in T_i} |B^+(u)| + |B^-(u)|\)` 成反比。
        *   **敏感度控制**：通过限制每个实体在负边中至多出现一次（`\(|B^-(u)| \le 1\)`），可将全局敏感度绑定到一个常数。
    2.  **耦合采样与隐私放大**：
        *   **形式化耦合采样**：将小批量构建定义为两阶段耦合采样 `\(S(D)\)`：先从 `\(D^{(1)}\)`（正边集合）采样 `\(B^{(1)}\)`，再从 `\(D^{(2)}\)`（节点集合）采样 `\(B^{(2)}\)` 以构建负边。
        *   **可处理子类：基数依赖采样**：将采样过程设计为 `\(B^{(2)}\)` 的采样仅依赖于 `\(B^{(1)}\)` 的基数（大小），而不依赖于其具体内容。例如，通过无放回地从节点集 `\(V\)` 中随机采样 `\(k_{neg} \cdot |B^{(1)}|\)` 个节点，并将其与正边的一端随机配对来构建负边。
        *   **隐私放大定理**：针对这种基数依赖的耦合采样，给出了组合机制 `\(f(S(D)) + \mathcal{N}(0, \sigma^2 C^2 I)\)` 的精确 RDP 边界，并给出了计算 RDP 参数 `\(\epsilon(\alpha)\)` 的公式。这一定理是核心理论贡献。

### 3. 实验设计

*   **应用场景**：在文本属性网络结构的关系数据上，对预训练的文本编码器进行微调，以进行关系预测任务。具体而言，是在一个私有图上微调模型，然后在一个分离的测试图上评估其零样本关系预测能力。
*   **数据集**：使用了四个来自两个领域的文本属性图数据集：
    *   引文网络：MAG-CHN 和 MAG-USA。
    *   共同购买网络：AMAZ-Sports 和 AMAZ-Cloth。
*   **对比方法**：
    *   **基础模型（无微调）**：直接应用预训练文本编码器，不进行关系学习。
    *   **非私有微调**：在训练图上进行标准微调，不施加隐私保护 (`\(\epsilon = \infty\)`)。
    *   **标准裁剪的DP-SGD**：使用标准的逐样本梯度裁剪替换本文提出的自适应裁剪方法。
*   **评估指标**：使用关系预测任务中常用的排序指标： **Top@1 精度**和**平均倒数排名**。

### 4. 资源与算力

*   **硬件配置**：
    *   对于 BERT 基础模型的实验：使用带有 **NVIDIA Quadro RTX 6000 (24GB)** GPU 的服务器。
    *   对于 Llama2-7B 模型的实验：使用 **NVIDIA A100 (80GB)** GPU。
*   **软件框架**：基于 **PyTorch 2.1.2**、**Transformers 4.23.0**、**PEFT 0.10.0** 和 **Opacus 1.4.1** 构建代码库。

### 5. 实验数量与充分性

*   **实验数量**：实验涵盖了多个维度，较为充分：
    *   **主实验**：在 4 个跨域迁移任务（如 MAG-CHN -> MAG-USA）上，对 **3 种不同规模的预训练模型**和 **3 种训练策略**，在 **2 个隐私预算** (`\(\epsilon=4, 10\)`) 下进行了性能对比，共数十组关键结果。
    *   **数值模拟实验**：通过数值计算对比了不同节点度 `\(K\)` 下，本文方法与朴素高斯机制、标准裁剪方法的**隐私边界**，验证了理论优势。
    *   **消融实验**：系统研究了关键超参数的影响，包括每正样本的负样本数 `\(k_{neg}\)`、节点度上限 `\(K\)` 以及噪声乘数 `\(\sigma\)`（即隐私-效用权衡）。
*   **客观性与公平性**：对比基线清晰，包括无隐私上限、标准 DP-SGD 方法和未微调模型。实验在同一应用场景和评估标准下进行，比较具有公平性。不过，由于微调大模型的成本，文中说明未报告误差棒。

### 6. 主要结论与发现

*   论文提出的 **DP-SGD 变体在所有隐私预算下，性能均显著优于未微调的基础模型**，证明了私有关系学习的有效性。
*   在相同的隐私预算下，本文提出的**自适应裁剪方法始终优于使用标准裁剪的 DP-SGD 方法**，实现了更好的隐私-效用权衡。
*   增大节点度上限 `\(K\)` 和负样本数量 `\(k_{neg}\)` 通常能在相同隐私预算下带来更好的模型效用。
*   理论分析表明，本文提出的隐私放大边界远比朴素的非放大边界紧凑，为实际应用中的隐私核算提供了更准确的依据。

### 7. 优点

*   **问题新颖且重要**：首次系统性地解决实体级 DP 关系学习中高敏感度和耦合采样的双重挑战。
*   **理论扎实**：提供了严格的敏感度分析和隐私放大定理，具有可证明的隐私保证。
*   **方法实用**：提出的自适应裁剪和负采样策略简单有效，易于实现。
*   **实验说服力强**：在真实的图数据集和主流的预训练模型上验证了方法的有效性，并通过消融实验提供了实用的洞见。

### 8. 不足与局限

*   **统计误差缺失**：由于大模型微调的计算成本，主实验结果未报告多次运行的误差棒，无法评估结果的统计显著性。
*   **自适应裁剪的探索有限**：文中主要探索了基于节点出现次数的特定自适应裁剪函数，对于更通用的、基于出现次数函数的裁剪策略的隐私-效用权衡，未做深入探讨。
*   **隐私放大边界的紧致性**：文中承认，对于基数依赖耦合采样的隐私放大边界的紧致性尚未被探索。
*   **负采样假设**：所设计的负采样策略（随机配对）可能会产生少量假负样本（将真正的边当作负样本），尽管在稀疏图中概率很低，但在稠密图中可能影响模型训练的准确性。

（完）
