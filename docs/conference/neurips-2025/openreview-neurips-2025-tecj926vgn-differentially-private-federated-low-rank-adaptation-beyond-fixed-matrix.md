---
title: Differentially Private Federated Low Rank Adaptation Beyond Fixed-Matrix
title_zh: 超越固定矩阵的差分隐私联邦低秩适配
authors: "Ming Wen, Jiaqi Zhu, Yuedong Xu, Yipeng Zhou, DINGDING HAN"
date: 2025-09-18
pdf: "https://openreview.net/pdf?id=TecJ926Vgn"
tags: ["query:daily"]
score: 9.0
evidence: 提出用于大模型的差分隐私联邦LoRA方法
tldr: 联邦大模型微调中传输适配器存在隐私泄露风险。本文提出FedASK，一种基于双草图化的差分隐私联邦低秩适配方法，将噪声注入与低秩结构解耦，在保护隐私的同时维持微调可学习性。实验表明，FedASK在提供差分隐私保障时性能接近非隐私联邦微调基线，为联邦大模型隐私保护训练提供了有效工具。
source: NeurIPS-2025-Accepted
selection_source: conference_retrieval
figures_json: "[{\"url\": \"assets/figures/openreview/openreview-neurips-2025-tecj926vgn/fig-001.webp\", \"caption\": \"\", \"page\": 2, \"index\": 1, \"width\": 1404, \"height\": 289}, {\"url\": \"assets/figures/openreview/openreview-neurips-2025-tecj926vgn/fig-002.webp\", \"caption\": \"\", \"page\": 4, \"index\": 2, \"width\": 1456, \"height\": 541}, {\"url\": \"assets/figures/openreview/openreview-neurips-2025-tecj926vgn/fig-003.webp\", \"caption\": \"\", \"page\": 10, \"index\": 3, \"width\": 1839, \"height\": 533}, {\"url\": \"assets/figures/openreview/openreview-neurips-2025-tecj926vgn/fig-004.webp\", \"caption\": \"\", \"page\": 28, \"index\": 4, \"width\": 4050, \"height\": 1200}, {\"url\": \"assets/figures/openreview/openreview-neurips-2025-tecj926vgn/fig-005.webp\", \"caption\": \"\", \"page\": 29, \"index\": 5, \"width\": 4050, \"height\": 1200}, {\"url\": \"assets/figures/openreview/openreview-neurips-2025-tecj926vgn/fig-006.webp\", \"caption\": \"\", \"page\": 29, \"index\": 6, \"width\": 4500, \"height\": 1500}, {\"url\": \"assets/figures/openreview/openreview-neurips-2025-tecj926vgn/fig-007.webp\", \"caption\": \"\", \"page\": 29, \"index\": 7, \"width\": 4500, \"height\": 1500}, {\"url\": \"assets/figures/openreview/openreview-neurips-2025-tecj926vgn/fig-008.webp\", \"caption\": \"\", \"page\": 31, \"index\": 8, \"width\": 1250, \"height\": 1039}, {\"url\": \"assets/figures/openreview/openreview-neurips-2025-tecj926vgn/fig-009.webp\", \"caption\": \"\", \"page\": 32, \"index\": 9, \"width\": 3571, \"height\": 1289}]"
motivation: 联邦大模型微调中传输本地适配器存在严重隐私泄露风险，现有差分隐私方法在噪声注入与可学习性之间难以平衡。
method: 提出FedASK框架，采用双草图化技术分别处理两个低秩矩阵，实现差分隐私联邦低秩适配。
result: 在多种语言模型和任务上，FedASK在满足差分隐私的同时微调性能接近非隐私联邦LoRA基线。
conclusion: FedASK为解决联邦LLM微调的隐私与效用平衡难题提供了一种有效方法。
---

## Abstract
Large language models (LLMs) typically require fine-tuning for domain-specific tasks, and LoRA offers a computationally efficient approach by training low-rank adaptors. LoRA is also communication-efficient for federated LLMs when multiple users collaboratively fine-tune a global LLM model without sharing their proprietary raw data. However, even the transmission of local adaptors between a server and clients risks serious privacy leakage. Applying differential privacy (DP) to federated LoRA encounters a dilemma: adding noise to both adaptors amplifies synthetic noise on the model, while fixing one adaptor impairs the learnability of fine-tuning. In this paper, we propose FedASK (Differentially Private Federated Low Rank Adaptation with Double SKetching) , a novel federated LoRA framework to enable effective updating of both low-rank adaptor matrices with robust differential privacy. Inspired by randomized SVD, our key idea is a two-stage sketching pipeline. This pipeline first aggregates carefully sketched, privacy-preserving local updates, and then reconstructs the global matrices on the server to facilitate effective updating of both adaptors. We theoretically prove FedASK's differential privacy guarantee and its exact aggregation property. Comprehensive experiments demonstrate that FedASK consistently outperforms baseline methods across a variety of privacy settings and data distributions.

---

## 论文详细总结（自动生成）

好的，作为一名资深学术论文分析助手，我将对这篇论文进行结构化、深入、客观的总结。

### 1. 论文的核心问题与整体含义

*   **研究动机与背景**：
    *   大语言模型（LLM）的联邦微调，结合参数高效微调（PEFT）方法如LoRA，允许多个客户端在不共享原始数据的情况下协作微调模型，同时降低了计算和通信开销。
    *   然而，即使在联邦学习中，传输LoRA适配器（低秩矩阵A和B）也存在严重的隐私泄露风险，因为模型更新可能编码了敏感信息。
    *   为解决隐私问题，引入差分隐私（DP）是标准的做法。但在联邦LoRA中应用差分隐私面临一个核心困境：
        *   **方案一**：同时对矩阵A和B的梯度加噪声。这会因其乘积更新（ ∆W = B A）导致**二次噪声放大**，严重损害模型效用。
        *   **方案二**：固定其中一个矩阵（通常是A），只对另一个矩阵（B）的梯度加噪声。这虽然避免了二次噪声，但严重**限制了模型的可学习性**，因为它将参数更新约束在了固定的子空间内。
*   **核心问题**：能否设计一个联邦LoRA框架，在保证差分隐私的同时，实现对两个低秩矩阵的有效更新，从而同时兼顾隐私性、可学习性和通信效率？
*   **整体含义**：本文提出了FedASK框架，旨在解决上述困境。它开创性地允许在严格的DP保障下动态更新两个LoRA矩阵，克服了前人方法中噪声放大与学习能力受限的权衡，实现了隐私保护下更高质量的联邦LLM微调。

### 2. 论文提出的方法论

*   **核心思想**：FedASK（Differentially Private Federated Low Rank Adaptation with Double SKetching）的核心是一个**两阶段草图化（Two-Stage Sketching）流程**，其灵感来源于随机化SVD。该流程在客户端计算并上传本地LoRA更新的压缩草图，由服务器精确重建全局更新，以此将噪声注入与低秩结构重建解耦。
*   **关键技术细节与算法流程**：
    1.  **第一阶段：随机化子空间草图化（Randomized Subspace Sketching）**
        *   客户端进行本地LoRA训练，得到更新的矩阵A和B。
        *   客户端利用一个共享的随机投影矩阵 ** Ω **，计算并上传一个压缩后的草图： **Yproj = B * (A * Ω) **。
        *   服务器聚合所有客户端上传的草图，并对其结果进行**QR分解**，获得一个正交基 ** Q **。这个基Q捕捉了全局更新矩阵的行空间信息。
    2.  **差分隐私局部更新**：
        *   在启用DP的训练轮次中，为了防止本地产生二次噪声项，客户端**固定矩阵A**，仅使用**DP-SGD**对**矩阵B**进行本地训练。这意味着噪声只被注入到B的更新中。
    3.  **第二阶段：全局对齐投影（Global Alignment Projection）**
        *   服务器将正交基 ** Q ** 广播给所有参与客户端。
        *   客户端根据Q进行二次投影，得到另一个草图： **˜Yproj = A.T * (B.T * Q) **，并上传到服务器。
        *   服务器聚合所有二次草图，对其结果进行**SVD分解**，得到三个矩阵 U, Σ, V.T 。最后，利用这些因子和第一阶段得到的正交基Q，重构并更新全局的两个低秩矩阵： **B.global = Q * U * Σ^(½) **和 **A.global = Σ^(½) * V.T **。
    *   **关键点**：尽管本地DP只扰动B，但通过服务器端的SVD重构，全局的A矩阵也得到了有效更新，因为SVD将聚合的隐私保护信息重新分配给了A和B。这也从理论上保证了聚合的精确性，即全局重建的更新 ∆W 等于所有本地更新 ∆W 的真实平均值。

### 3. 实验设计

*   **数据集与场景**：
    *   **NLP与数学推理任务**：
        *   模型：Llama-2-7B 和 Llama-2-13B。
        *   数据集：Llama-2-7B在**dolly-15K**上微调；Llama-2-13B在**MetaMathQA**上进行思维链（CoT）微调。
        *   评估基准：MMLU、DROP、HumanEval（针对7B模型）；GSM8K、GSM8K-hard、MATH（针对13B模型）。
    *   **视觉语言与人类反馈强化学习（RLHF）任务**：
        *   模型：Llava-1.5-7b。
        *   任务：在**SPA-VL**安全偏好数据集上进行直接偏好优化（DPO）。
        *   评估基准：MM-SafetyBench、SIUO、BeaverTails-V。
*   **对比方法（Benchmark）**：
    *   **FedAvg**：标准联邦平均。
    *   **FFA-LoRA**：固定矩阵A，只更新B的差分隐私LoRA方法。
    *   **FedSA-LoRA**：本地更新两个矩阵，但仅传输一个矩阵。
    *   **FedProx**、**Scaffold**：解决联邦学习中数据异质性的经典方法。

### 4. 资源与算力

*   **论文明确提及**：所有评估均在 **NVIDIA Tesla A100 GPU** 上进行，并采用**半精度（half-precision）** 以最大化计算效率。在附录的系统效率实验中，作者使用了**NVIDIA H100 GPU**来测量时间和内存消耗。
*   **未明确说明**：论文未提及实验使用的GPU总数量、每个实验的具体训练总时长或碳排放量。

### 5. 实验数量与充分性

*   **实验数量与多样性**：实验设计相当全面，涵盖了多个维度：
    1.  **模型与任务多样性**：7B和13B两种规模的模型，覆盖了NLP理解、数学推理、视觉语言安全对齐等多种任务。
    2.  **隐私预算变化**：在多个隐私预算水平（ ε = 1, 3, 6 及非隐私）下进行评估。
    3.  **数据异质性**：在IID和多种Dirichlet分布（ α = 0.1, 0.5, 1.0 ）的非IID场景下测试了算法鲁棒性。
    4.  **消融与分析实验**：研究了LoRA秩（ r ）和过草图化参数（ p ）对性能的影响；分析了聚合保真度和系统效率（通信量、运算时间、GPU内存）。
    5.  **误差棒**：附录中提供了五次独立运行的平均值和标准误差，增加了结果的统计可靠性。
*   **充分性与公平性**：实验设计非常充分、客观且公平。对比的主流Baseline涵盖了联邦学习、差分隐私LoRA以及解决数据异质性的代表性方法。超参数采用网格搜索，评估标准是领域内公认的基准数据集。

### 6. 论文的主要结论与发现

*   **性能显著提升**：FedASK在所有隐私设置和数据分布下，一致性地优于所有基线方法。在强隐私预算（ ε = 1 ）下，其性能优势尤其明显，例如在7B模型的MMLU任务上性能提升高达11.5%，在13B模型的GSM8K任务上性能提升高达46%。
*   **解决核心困境**：FedASK成功打破了差分隐私联邦LoRA中噪声放大与学习能力受限的权衡，是第一个能够在严格DP保证下有效更新两个低秩矩阵的框架。
*   **鲁棒性**：FedASK的性能对过草图化参数 p 不敏感，表现出很强的鲁棒性。同时，它在数据异质性较强的非IID环境中也展现了卓越的适应能力。
*   **有效性与效率**：理论证明和实证分析均表明，FedASK能以很小的计算和通信开销实现近乎精确的聚合，证明了其方法的高效性。

### 7. 优点

*   **方法创新性**：两阶段草图化流程巧妙地将差分隐私噪声限制在本地，同时利用服务器端的SVD重构同步更新两个全局低秩矩阵，思路新颖且有效。
*   **理论严谨性**：论文提供了严格的差分隐私保障证明（定理1）和精确聚合保证证明（定理2），理论与实验相互印证。
*   **实验全面性**：实验设计考虑周全，从不同模型、任务、隐私预算、数据分布、算法维度等多个角度进行了广泛的验证，结论可信度高。
*   **实用性强**：在显著提升模型性能的同时，该方法在计算和通信开销上相比基线方法仍具有竞争力或更有优势，证明了其在实际部署中的潜力。
*   **开源**：论文提供了代码，有助于研究社区的复现和后续研究。

### 8. 不足与局限

*   **本地更新策略局限**：在DP轮次中，FedASK本地仍然固定了矩阵A。作者将此列为未来可探索的方向，即研究在两个矩阵上都进行差分隐私本地更新的策略。
*   **任务覆盖范围**：目前实验主要集中于自然语言处理、数学推理和视觉语言模型的安全对齐。论文在结论中也提到，未来需将其扩展到更广泛的模型架构和更复杂的训练范式（如RLHF）中，其通用性有待进一步检验。
*   **缺乏收敛性理论分析**：论文的理论分析集中在隐私和聚合精度上，但未提供基于DP和草图化的联邦优化过程的收敛性分析。
*   **潜在的实现潜力局限**：尽管实验显示通信开销有优势，但在实际大规模跨设备联邦学习中，服务器端的QR和SVD分解可能会成为计算瓶颈，但论文指出这相比基线仍有优势。

（完）
