---
title: Theoretically Unmasking Inference Attacks Against LDP-Protected Clients in Federated Vision Models
title_zh: 理论上揭露针对联邦视觉模型中LDP保护客户端的推理攻击
authors: "Quan Minh Nguyen, Minh N. Vu, Truc Nguyen, My T. Thai"
date: 2025-05-01
pdf: "https://openreview.net/pdf?id=R7gCixl2xR"
tags: ["query:daily"]
score: 10.0
evidence: 针对联邦学习中LDP保护的推理攻击
tldr: 针对联邦学习中本地差分隐私(LDP)保护的不足，该论文从理论上推导了低多项式时间成员推理攻击成功率的下界，揭示了LDP在联邦视觉模型中的脆弱性，为隐私保护提供了理论警醒。
source: ICML-2025-Accepted
selection_source: conference_retrieval
figures_json: "[{\"url\": \"assets/figures/openreview/openreview-icml-2025-r7gcixl2xr/fig-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 1679, \"height\": 346, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-icml-2025-r7gcixl2xr/fig-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 420, \"height\": 370, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-icml-2025-r7gcixl2xr/fig-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 355, \"height\": 365, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-icml-2025-r7gcixl2xr/fig-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 1412, \"height\": 255, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-icml-2025-r7gcixl2xr/fig-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 607, \"height\": 343, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-icml-2025-r7gcixl2xr/fig-006.webp\", \"caption\": \"\", \"page\": 0, \"index\": 6, \"width\": 460, \"height\": 334, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-icml-2025-r7gcixl2xr/fig-007.webp\", \"caption\": \"\", \"page\": 0, \"index\": 7, \"width\": 616, \"height\": 340, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-icml-2025-r7gcixl2xr/fig-008.webp\", \"caption\": \"\", \"page\": 0, \"index\": 8, \"width\": 1711, \"height\": 396, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-icml-2025-r7gcixl2xr/fig-009.webp\", \"caption\": \"\", \"page\": 0, \"index\": 9, \"width\": 1710, \"height\": 395, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-icml-2025-r7gcixl2xr/fig-010.webp\", \"caption\": \"\", \"page\": 0, \"index\": 10, \"width\": 1706, \"height\": 498, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-icml-2025-r7gcixl2xr/fig-011.webp\", \"caption\": \"\", \"page\": 0, \"index\": 11, \"width\": 688, \"height\": 342, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-icml-2025-r7gcixl2xr/fig-012.webp\", \"caption\": \"\", \"page\": 0, \"index\": 12, \"width\": 1746, \"height\": 1058, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-icml-2025-r7gcixl2xr/fig-013.webp\", \"caption\": \"\", \"page\": 0, \"index\": 13, \"width\": 1749, \"height\": 633, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-icml-2025-r7gcixl2xr/fig-014.webp\", \"caption\": \"\", \"page\": 0, \"index\": 14, \"width\": 793, \"height\": 476, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-icml-2025-r7gcixl2xr/fig-015.webp\", \"caption\": \"\", \"page\": 0, \"index\": 15, \"width\": 1028, \"height\": 545, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-icml-2025-r7gcixl2xr/fig-016.webp\", \"caption\": \"\", \"page\": 0, \"index\": 16, \"width\": 1713, \"height\": 396, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-icml-2025-r7gcixl2xr/fig-017.webp\", \"caption\": \"\", \"page\": 0, \"index\": 17, \"width\": 1364, \"height\": 930, \"label\": \"Figure\"}]"
tables_json: "[{\"url\": \"assets/tables/openreview/openreview-icml-2025-r7gcixl2xr/table-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 1780, \"height\": 234, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-icml-2025-r7gcixl2xr/table-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 1292, \"height\": 389, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-icml-2025-r7gcixl2xr/table-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 1176, \"height\": 257, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-icml-2025-r7gcixl2xr/table-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 1627, \"height\": 552, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-icml-2025-r7gcixl2xr/table-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 1627, \"height\": 552, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-icml-2025-r7gcixl2xr/table-006.webp\", \"caption\": \"\", \"page\": 0, \"index\": 6, \"width\": 1627, \"height\": 550, \"label\": \"Table\"}]"
motivation: 现有推理攻击研究多忽略LDP保护或缺少理论保证，本文弥补这一空白。
method: 推导低多项式时间成员推理攻击在完全联邦学习场景下成功率的下界。
result: 给出了攻击成功率的理论下界，揭示了LDP保护下的隐私漏洞。
conclusion: 即使是LDP保护，联邦学习仍面临成员推理攻击的理论威胁，需更强防御。
---

## Abstract
Federated Learning (FL) enables collaborative learning among clients via a coordinating server while avoiding direct data sharing, offering a perceived solution to preserve privacy. However, recent studies on Membership Inference Attacks (MIAs) have challenged this notion, showing high success rates against unprotected training data. While local differential privacy (LDP) is widely regarded as a gold standard for privacy protection in data analysis, most studies on MIAs either neglect LDP or fail to provide theoretical guarantees for attack success against LDP-protected data.
    
To address this gap, we derive theoretical lower bounds for the success rates of low-polynomial-time MIAs that exploit vulnerabilities in fully connected or self-attention layers, regardless of the LDP mechanism used. We establish that even when data are protected by LDP, privacy risks persist, depending on the privacy budget. Practical evaluations on models like ResNet and Vision Transformer confirm considerable privacy risks, revealing that the noise required to mitigate these attacks significantly degrades models' utility.

---

## 论文详细总结（自动生成）

好的，我将按照您的要求，对提供的论文进行结构化、深入、客观的总结。

### 1. 论文的核心问题与整体含义
*   **研究背景**：联邦学习允许客户端在不共享原始数据的情况下协作训练模型，但模型更新（如梯度）仍可能泄露隐私。成员推理攻击旨在判断特定数据记录是否属于客户端的本地训练集。
*   **核心问题**：现有研究大多忽略本地差分隐私，或未能从理论上证明在LDP保护下，成员推理攻击的成功率下限。本文旨在填补这一空白，从理论和实践上证明，即使是受LDP保护的数据，在面对不诚实服务器的主动成员推理攻击时，依然存在根本性的隐私风险。
*   **整体含义**：论文揭示了联邦学习中隐私保护的一个根本性权衡：使用LDP来防御强力的推理攻击，所需添加的噪声水平将严重损害模型的可用性，这意味着仅靠LDP可能无法在维持模型性能的同时，提供足够的隐私保障。

### 2. 方法论
论文的核心方法论是构建并分析了两种低多项式时间复杂度的主动成员推理攻击，并推导其在LDP保护下的理论攻击成功率下界。

*   **威胁模型**：采用主动敌手模型，即联邦学习服务器是不诚实的，它会恶意篡改全局模型的参数（如特定层的权重和偏置）下发至客户端，以诱使客户端的本地更新暴露其隐私数据。
*   **核心攻击机制**：
    *   **基于全连接层的攻击 (ADFC)**：
        *   **原理**：服务器精心构造两个全连接层的参数，使其能够检测客户端输入与某个目标样本之间的L1距离。
        *   **推理逻辑**：若输入中存在目标样本，该层计算出的特定偏置项的梯度将非零；反之，梯度为零。服务器通过观察该梯度值推断成员信息。
    *   **基于自注意力层的攻击 (ADAttn)**：
        *   **原理**：利用自注意力层的记忆能力。服务器配置两个注意力头：一个过滤掉目标模式，另一个不过滤。
        *   **推理逻辑**：当客户端数据包含目标模式时，两个注意力头输出的差异会增大，导致相关权重的梯度非零，从而暴露成员信息。针对视觉Transformer (ViT)，攻击直接作用于图像块嵌入。
*   **理论分析**：论文在标准安全博弈框架下，推导出攻击优势的理论下界。
    *   **定理1 (FC层下界)**：针对离散数据，攻击优势 `Adv_FC >= 1 - (n+|X|-1)/(|X|-1) * P_Mε`。其中 `P_Mε` 是LDP机制将数据点移出其邻域的概率，与隐私预算 `ε` 成反比。
    *   **定理2 (攻击上限)**：对于任何攻击者，其优势上限为 `(e^ε - 1) / (e^ε + 1)`。
    *   **定理3 (注意力层下界)**：引入“模式分离度 (Δε)”概念，推导出攻击优势的下界，表明随机噪声增大会导致受保护数据的嵌入在中心区域重叠，减少各模式区分度，从而降低攻击成功率，但也同时损害模型性能。

### 3. 实验设计
*   **数据集**：
    *   **合成数据**：独热编码数据和球面数据，用于验证理论下界的渐近行为。
    *   **真实世界数据（视觉）**：CIFAR10、CIFAR100、ImageNet。针对CNN模型（如ResNet），使用Img2Vec提取特征嵌入；针对ViT模型，使用预训练基础模型提取图像块嵌入。
    *   **真实世界数据（自然语言处理，附录中）**：IMDB、Yelp、Twitter、Finance，模型包括BERT、RoBERTa、GPT-1、DistilBERT。
*   **对比方法**：
    *   **攻击方法**：对比了基于全连接层的 `ADFC` 和基于注意力层的 `ADAttn` 两种攻击。
    *   **LDP防御机制**：评估了BitRand, Generalized Randomized Response (GRR), RAPPOR, dBitFlipPM 和 OME 等多种LDP算法，在不同隐私预算 `ε` 下的防御效果。
*   **基准**：以无LDP保护时的攻击成功率（接近100%）作为基准。同时，将模型在相应分类任务上的准确率作为效用基准，以直观展示隐私-效用权衡。
*   **评估指标**：攻击成功率（Success Rate）和敌手优势（Advantage）。自然语言处理实验中还使用了准确率（ACC）、F1分数和AUC。

### 4. 资源与算力
*   论文明确说明了实验的计算资源配置：实验在配备Linux 64位操作系统的单个GPU节点上执行。该节点拥有36个CPU核心（每核2线程）、384GB内存，以及2块48GB显存的 NVIDIA RTX A6000 GPU。
*   论文未提供总体的训练时长或单次实验耗时。

### 5. 实验数量与充分性
*   **实验数量**：
    *   合成数据实验（图5、图6）：每组数据点运行1000次博弈。
    *   图7-图9 (a,b) 的FC和注意力层攻击：每组配置进行20次试验，每次试验包含200次安全博弈，总计4000次博弈。
    *   图9(c) 的ImageNet实验：每组配置进行40次试验，每次试验包含100次博弈，总计4000次博弈。
*   **充分性与客观性**：实验设计是充分且客观的。
    *   **广度**：覆盖了合成数据、多个标准图像和文本数据集、多种模型架构（FC层、ResNet、ViT、BERT系），以及多种主流LDP机制，验证了攻击和理论的普适性。
    *   **深度**：不仅报告了不同隐私预算下的攻击成功率，还探讨了批量大小、攻击超参数（如注意力攻击的 `β`）对成功率的影响，并与理论上下界进行了比较。
    *   **公平性**：实验结果明确揭示了为了将攻击成功率降至可接受水平（如低于80%），需要将隐私预算 `ε` 设置得非常小，但这会带来超过20%的模型准确率损失，公平地反映了隐私和效用之间无法调和的矛盾。

### 6. 主要结论与发现
*   **LDP的脆弱性**：LDP保护无法完全消除成员隐私泄露风险。即使在严格的LDP保护下（较小的隐私预算 ε），主动成员推理攻击仍能取得显著高于随机猜测（50%）的成功率。
*   **理论与实证一致**：推导出的理论下界与实证攻击成功率高度吻合，验证了理论分析的正确性。
*   **隐私-效用根本性权衡**：要有效缓解此类攻击，必须添加极大的噪声（即 ε 非常小），但这会导致模型效用（分类准确率）急剧下降。例如，为防止BitRand保护下CIFAR-10数据的攻击成功率超过80%，模型需承受至少20%的精度损失。
*   **高维数据更脆弱**：随着数据维度增加，随机样本几乎正交，使得数据点位于边界，基于注意力层的攻击理论下界更高（独热编码数据表现出最强攻击性）。
*   **最佳攻击超参数**：对于基于注意力层的攻击，并非超参数 β 越大越好。在LDP保护下，增大的 β 会增加模式重叠概率，从而降低攻击成功率。实验表明较小的 β（如0.01）通常效果更好。

### 7. 优点
*   **理论严谨性**：首次为LDP保护下的低复杂度成员推理攻击提供了理论成功率的上下界，这是一个重要的理论贡献。
*   **攻击方法高效**：所分析的攻击只需单轮联邦学习迭代即可完成，且具有低多项式时间复杂度，具有很强的现实威胁性。
*   **研究范围广泛**：分析覆盖了联邦学习中最基本的两种层类型（FC和自注意力），并延伸至现代视觉模型（ViT）和自然语言的参数高效微调场景，以及多种LDP机制。
*   **清晰的权衡展示**：通过理论和实验，强有力地论证了在诚实但可能不服从的服务器的联邦学习设置中，仅靠本地差分隐私实现隐私与效用双赢的困难性。

### 8. 不足与局限
*   **噪声模型简化**：在分析基于注意力的攻击时，将LDP引入的非线性、离散噪声简化为连续的、有界范数的加性噪声，这可能与实际机制（尤其是在自然语言处理的离散嵌入中）存在偏差，使得理论分析不能直接应用于自然语言处理等场景。
*   **特定威胁模型**：结论高度依赖于“不诚实服务器”这一强假设。文章虽然讨论了安全聚合（SMPC/HE）可能是无效的，但未讨论其他针对模型投毒或异常梯度检测的防御机制。
*   **超参数选择依赖知识**：攻击成功与否高度依赖于超参数（如 `τ_D`， `β`， `γ`）的正确选择，而这通常需要攻击者了解数据分布和LDP机制的先验知识，这可能不完全符合所有现实场景。
*   **只关注了特定攻击**：研究聚焦于两种特定的攻击方法，尽管它们是当前最优的，但不能排除存在其他尚未被发现的、需要不同理论分析的攻击路径。

（完）
