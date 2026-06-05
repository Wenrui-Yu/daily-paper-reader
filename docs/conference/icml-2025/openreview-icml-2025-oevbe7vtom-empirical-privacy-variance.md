---
title: Empirical Privacy Variance
title_zh: 经验隐私方差
authors: "Yuzheng Hu, Fan Wu, Ruicheng Xian, Yuhang Liu, Lydia Zakynthinou, Pritish Kamath, Chiyuan Zhang, David Forsyth"
date: 2025-05-01
pdf: "https://openreview.net/pdf?id=oEvbe7vtOm"
tags: ["query:daily"]
score: 9.0
evidence: DP-SGD微调中的经验隐私方差
tldr: 提出经验隐私方差概念，研究差分隐私语言模型微调中，相同DP保证下不同超参数配置会导致实际隐私水平显著变化，通过记忆化量化这一现象，揭示了隐私-效用权衡的复杂性。
source: ICML-2025-Accepted
selection_source: conference_retrieval
figures_json: "[{\"url\": \"assets/figures/openreview/openreview-icml-2025-oevbe7vtom/fig-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 1401, \"height\": 406, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-icml-2025-oevbe7vtom/fig-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 1764, \"height\": 549, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-icml-2025-oevbe7vtom/fig-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 825, \"height\": 601, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-icml-2025-oevbe7vtom/fig-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 837, \"height\": 491, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-icml-2025-oevbe7vtom/fig-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 1783, \"height\": 367, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-icml-2025-oevbe7vtom/fig-006.webp\", \"caption\": \"\", \"page\": 0, \"index\": 6, \"width\": 453, \"height\": 305, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-icml-2025-oevbe7vtom/fig-007.webp\", \"caption\": \"\", \"page\": 0, \"index\": 7, \"width\": 850, \"height\": 403, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-icml-2025-oevbe7vtom/fig-008.webp\", \"caption\": \"\", \"page\": 0, \"index\": 8, \"width\": 354, \"height\": 308, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-icml-2025-oevbe7vtom/fig-009.webp\", \"caption\": \"\", \"page\": 0, \"index\": 9, \"width\": 854, \"height\": 431, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-icml-2025-oevbe7vtom/fig-010.webp\", \"caption\": \"\", \"page\": 0, \"index\": 10, \"width\": 456, \"height\": 355, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-icml-2025-oevbe7vtom/fig-011.webp\", \"caption\": \"\", \"page\": 0, \"index\": 11, \"width\": 431, \"height\": 307, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-icml-2025-oevbe7vtom/fig-012.webp\", \"caption\": \"\", \"page\": 0, \"index\": 12, \"width\": 1637, \"height\": 408, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-icml-2025-oevbe7vtom/fig-013.webp\", \"caption\": \"\", \"page\": 0, \"index\": 13, \"width\": 1586, \"height\": 779, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-icml-2025-oevbe7vtom/fig-014.webp\", \"caption\": \"\", \"page\": 0, \"index\": 14, \"width\": 885, \"height\": 1049, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-icml-2025-oevbe7vtom/fig-015.webp\", \"caption\": \"\", \"page\": 0, \"index\": 15, \"width\": 534, \"height\": 653, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-icml-2025-oevbe7vtom/fig-016.webp\", \"caption\": \"\", \"page\": 0, \"index\": 16, \"width\": 788, \"height\": 570, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-icml-2025-oevbe7vtom/fig-017.webp\", \"caption\": \"\", \"page\": 0, \"index\": 17, \"width\": 1780, \"height\": 1311, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-icml-2025-oevbe7vtom/fig-018.webp\", \"caption\": \"\", \"page\": 0, \"index\": 18, \"width\": 1180, \"height\": 914, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-icml-2025-oevbe7vtom/fig-019.webp\", \"caption\": \"\", \"page\": 0, \"index\": 19, \"width\": 1594, \"height\": 1350, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-icml-2025-oevbe7vtom/fig-020.webp\", \"caption\": \"\", \"page\": 0, \"index\": 20, \"width\": 1326, \"height\": 411, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-icml-2025-oevbe7vtom/fig-021.webp\", \"caption\": \"\", \"page\": 0, \"index\": 21, \"width\": 1597, \"height\": 761, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-icml-2025-oevbe7vtom/fig-022.webp\", \"caption\": \"\", \"page\": 0, \"index\": 22, \"width\": 1597, \"height\": 744, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-icml-2025-oevbe7vtom/fig-023.webp\", \"caption\": \"\", \"page\": 0, \"index\": 23, \"width\": 1218, \"height\": 731, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-icml-2025-oevbe7vtom/fig-024.webp\", \"caption\": \"\", \"page\": 0, \"index\": 24, \"width\": 535, \"height\": 604, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-icml-2025-oevbe7vtom/fig-025.webp\", \"caption\": \"\", \"page\": 0, \"index\": 25, \"width\": 1088, \"height\": 529, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-icml-2025-oevbe7vtom/fig-026.webp\", \"caption\": \"\", \"page\": 0, \"index\": 26, \"width\": 1778, \"height\": 888, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-icml-2025-oevbe7vtom/fig-027.webp\", \"caption\": \"\", \"page\": 0, \"index\": 27, \"width\": 1768, \"height\": 360, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-icml-2025-oevbe7vtom/fig-028.webp\", \"caption\": \"\", \"page\": 0, \"index\": 28, \"width\": 1767, \"height\": 363, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-icml-2025-oevbe7vtom/fig-029.webp\", \"caption\": \"\", \"page\": 0, \"index\": 29, \"width\": 1772, \"height\": 863, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-icml-2025-oevbe7vtom/fig-030.webp\", \"caption\": \"\", \"page\": 0, \"index\": 30, \"width\": 1243, \"height\": 569, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-icml-2025-oevbe7vtom/fig-031.webp\", \"caption\": \"\", \"page\": 0, \"index\": 31, \"width\": 1466, \"height\": 584, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-icml-2025-oevbe7vtom/fig-032.webp\", \"caption\": \"\", \"page\": 0, \"index\": 32, \"width\": 1778, \"height\": 998, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-icml-2025-oevbe7vtom/fig-033.webp\", \"caption\": \"\", \"page\": 0, \"index\": 33, \"width\": 1779, \"height\": 1439, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-icml-2025-oevbe7vtom/fig-034.webp\", \"caption\": \"\", \"page\": 0, \"index\": 34, \"width\": 1779, \"height\": 1553, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-icml-2025-oevbe7vtom/fig-035.webp\", \"caption\": \"\", \"page\": 0, \"index\": 35, \"width\": 1598, \"height\": 568, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-icml-2025-oevbe7vtom/fig-036.webp\", \"caption\": \"\", \"page\": 0, \"index\": 36, \"width\": 1596, \"height\": 546, \"label\": \"Figure\"}]"
tables_json: "[{\"url\": \"assets/tables/openreview/openreview-icml-2025-oevbe7vtom/table-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 861, \"height\": 460, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-icml-2025-oevbe7vtom/table-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 1771, \"height\": 1202, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-icml-2025-oevbe7vtom/table-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 1676, \"height\": 494, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-icml-2025-oevbe7vtom/table-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 1772, \"height\": 755, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-icml-2025-oevbe7vtom/table-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 1765, \"height\": 613, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-icml-2025-oevbe7vtom/table-006.webp\", \"caption\": \"\", \"page\": 0, \"index\": 6, \"width\": 406, \"height\": 255, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-icml-2025-oevbe7vtom/table-007.webp\", \"caption\": \"\", \"page\": 0, \"index\": 7, \"width\": 462, \"height\": 241, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-icml-2025-oevbe7vtom/table-008.webp\", \"caption\": \"\", \"page\": 0, \"index\": 8, \"width\": 520, \"height\": 164, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-icml-2025-oevbe7vtom/table-009.webp\", \"caption\": \"\", \"page\": 0, \"index\": 9, \"width\": 883, \"height\": 283, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-icml-2025-oevbe7vtom/table-010.webp\", \"caption\": \"\", \"page\": 0, \"index\": 10, \"width\": 1418, \"height\": 237, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-icml-2025-oevbe7vtom/table-011.webp\", \"caption\": \"\", \"page\": 0, \"index\": 11, \"width\": 1244, \"height\": 314, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-icml-2025-oevbe7vtom/table-012.webp\", \"caption\": \"\", \"page\": 0, \"index\": 12, \"width\": 1246, \"height\": 317, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-icml-2025-oevbe7vtom/table-013.webp\", \"caption\": \"\", \"page\": 0, \"index\": 13, \"width\": 540, \"height\": 196, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-icml-2025-oevbe7vtom/table-014.webp\", \"caption\": \"\", \"page\": 0, \"index\": 14, \"width\": 855, \"height\": 494, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-icml-2025-oevbe7vtom/table-015.webp\", \"caption\": \"\", \"page\": 0, \"index\": 15, \"width\": 540, \"height\": 191, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-icml-2025-oevbe7vtom/table-016.webp\", \"caption\": \"\", \"page\": 0, \"index\": 16, \"width\": 1062, \"height\": 394, \"label\": \"Table\"}]"
motivation: 相同DP保证下，不同超参数配置的实际隐私表现差异显著，缺乏研究。
method: 定义经验隐私方差，通过记忆化度量实际隐私，并进行回归分析。
result: 超参数调优中存在隐私-效用无免费午餐的折衷，某些配置下隐私泄露更高。
conclusion: 仅关注隐私预算无法保证实际隐私，需考虑超参数的影响。
---

## Abstract
We propose the notion of empirical privacy variance and study it in the context of differentially private fine-tuning of language models. Specifically, we show that models calibrated to the same $(\varepsilon, \delta)$-DP guarantee using DP-SGD with different hyperparameter configurations can exhibit significant variations in empirical privacy, which we quantify through the lens of memorization. We investigate the generality of this phenomenon across multiple dimensions and discuss why it is surprising and relevant. Through regression analysis, we examine how individual and composite hyperparameters influence empirical privacy. The results reveal a no-free-lunch trade-off: existing practices of hyperparameter tuning in DP-SGD, which focus on optimizing utility under a fixed privacy budget, often come at the expense of empirical privacy. To address this, we propose refined heuristics for hyperparameter selection that explicitly account for empirical privacy, showing that they are both precise and practically useful. Finally, we take preliminary steps to understand empirical privacy variance. We propose two hypotheses, identify limitations in existing techniques like privacy auditing, and outline open questions for future research.

---

## 论文详细总结（自动生成）

好的，以下是基于所提供论文《经验隐私方差》的结构化、深入、客观的中文总结。

### 1. 论文的核心问题与整体含义

*   **核心问题**：在大型语言模型（LLM）的微调中，差分隐私随机梯度下降（DP-SGD）是常用的隐私保护技术。一个关键但未被充分探究的问题是：**对于标定到完全相同的 \((\varepsilon, \delta)\)-DP 理论保证的多个模型，它们在实际应用中表现出的隐私保护水平（即“经验隐私”）是否一致？**
*   **研究动机与背景**：
    *   **理论与实践的鸿沟**：差分隐私（DP）提供的是最坏情况下的理论保证，但用户和开发者更关心模型在行为上是否真的泄露了敏感信息（如生成训练数据中的电话号码）。这种对模型行为的感知被作者称为“经验隐私”。
    *   **超参数调优的盲区**：目前DP-SGD的超参数调优（如批量大小、学习率）主要目标是最大化模型在固定隐私预算下的效用（utility），而忽视了这些选择对经验隐私的潜在影响。
*   **整体含义**：本文揭示了**“经验隐私方差”** 这一现象——具有相同理论DP保证的模型，其实际隐私泄露风险会因超参数配置的不同而产生巨大差异。这意味着，仅凭 \((\varepsilon, \delta)\) 值不足以完全衡量和保证模型的真实隐私保护水平，对依赖DP进行标准化和认证构成了挑战。

### 2. 论文提出的方法论

*   **核心思想**：通过“记忆化”的视角来量化和研究经验隐私，并提出一套分析框架，用于评估DP-SGD的超参数如何影响模型对训练数据中敏感信息的记忆和泄露。
*   **关键技术细节与度量指标**：
    *   **经验隐私度量**：定义了三种量化模型记忆能力的指标，分数越高代表经验隐私越差。
        1.  **对抗压缩比（ACR）**：寻找能诱导模型生成完整秘密的最短提示（prompt），ACR = （秘密长度） / （最短提示长度）。ACR越高，模型越容易“泄露”秘密。
        2.  **逐字记忆比（VMR）**：用秘密的前缀作为提示，计算模型逐字生成完整剩余部分的概率。
        3.  **属性推断比（AIR）**：在问答任务中，衡量模型能否从提示中准确恢复出特定的秘密属性（如作者的写作风格）。
    *   **超参数影响分析**：
        1.  **回归分析**：以经验隐私分数为因变量，以超参数（批量大小 \(b\)、迭代次数 \(T\)、学习率 \(\eta\)）以及组合量（计算量 \(C = b \cdot T\)、更新步 \(U = C \cdot \eta\)）为自变量，进行多元回归，定性分析其影响。
        2.  **超参数选择启发式方法**：基于回归分析结论，提出了一套优化经验隐私的启发式规则（Algorithm 1），例如，在固定计算量（\(C\)）时，应选择更大的 \(b\) 和更小的 \(T\)；在固定更新步（\(U\)）时，应选择更小的 \(\eta\)。

### 3. 实验设计

*   **数据集与模型**：
    *   **Enron Email 数据集**（含33k样本）：提取了13个高频出现的秘密信息（如电话号码、邮箱地址）。用于微调 **GPT-2-Small (117M) 和 GPT-2-Large (774M)** 模型。
    *   **TOFU 数据集**（合成作者简介）：提取作者的“写作风格”作为秘密属性（共52个）。通过 LLM 释义创建了不同规模和密度的变体（TOFU-1, TOFU-2, TOFU-4 等）。用于微调 **Llama-2 (7B/13B)** 模型。
*   **DP 微调**：使用 LoRA 与 DP-Adam 在多种 \((\varepsilon, \delta)\) 预算（\(\varepsilon \in \{1, 2, 4, 8, 16\}\)， \(\delta = n^{-1.1}\)）下进行训练，实验了数十种 \((b, T, \eta)\) 组合。
*   **对比基础与基准**：
    *   **现象验证**：对比相同理论 \(\varepsilon\) 下，不同超参数配置模型的经验隐私分数（方差）。
    *   **启发式方法评估**：将提出的启发式选择方法（Algorithm 1）与两个基线进行对比：(1) 选择**最佳效用（Best-utility）** 的常见做法；(2) 独立的**最差效用（Worst-utility）** 启发式。比较它们在候选模型池中选出的模型与“神谕点”（经验隐私最优的模型）的相对隐私风险。同时，通过与随机猜测比较来评估成对比较启发式的准确性。

### 4. 资源与算力

*   **硬件环境**：实验主要在三种计算环境中进行：1) 配备4张NVIDIA H100 GPU (80GB) 的服务器；2) 配备4张NVIDIA A100 GPU (80GB) 的服务器；3) 一个包含100个节点的集群（每个节点含4张40GB A100 GPU）。
*   **算力消耗**：总计算量超过 **5,000 GPU 小时**（以H100算力为单位进行折算）。
    *   **训练**：GPT-2-S 的单次训练从15分钟（最小配置）到7.5小时（最大配置）不等；GPT-2-L 则从30分钟到17小时不等。Llama-2-7B 最大配置训练一次耗时5小时。
    *   **评估**：评估ACR指标非常耗时，GPT-2-S 平均每个秘密需1100秒，GPT-2-L 则需5300秒。评估总计算量也约合 **5,000 GPU 小时**。

### 5. 实验数量与充分性

*   **实验规模**：实验体量庞大且系统。
    *   **配置丰富**：对 GPT-2 模型探索了23/15种配置，对 Llama-2 模型进行了60/75种配置的全网格搜索。每个配置使用多个随机种子（3-4个）并过滤低效用模型。
    *   **多维度验证**：从模型大小（GPT-2 S vs L， Llama-2 7B vs 13B）、数据集（Enron vs TOFU）、隐私预算 (\(\varepsilon\))、数据集变体（规模、秘密密度）、微调范式（全量微调 vs LoRA）、经验隐私度量（ACR vs VMR）以及不同的秘密子集等多个维度验证了“经验隐私方差”现象的普遍性。
    *   **控制变量**：通过确保微调数据未出现在预训练语料、分离测试集与秘密集、固定裁剪阈值等手段，有效控制了干扰因素。
*   **充分性与公平性**：实验设计充分且公平。它并非要证明哪个模型更好，而是通过控制变量暴露出一个普遍存在的、由超参数引起的不一致性，对比是在公平的 (\(\varepsilon, \delta\)) 前提下进行的。现象验证和启发式评估覆盖了多场景、多基线，结论具有说服力。

### 6. 论文的主要结论与发现

*   **现象存在且显著**：“经验隐私方差”是一个普遍且重大的现象。在固定的 (\(\varepsilon, \delta\)) 下，不同超参数配置会导致模型的经验隐私（记忆化程度）产生巨大差异，在某些情况下模型可能几乎完全泄露秘密，而另一些则表现良好。
*   **方差变化趋势**：经验隐私方差随着模型尺寸、数据集规模、秘密密度以及隐私预算 (\(\varepsilon\)) 的增大而增加。全量微调的方差大于LoRA微调。
*   **超参数的无免费午餐**：现有的以优化效用为目标的超参数调优实践（如推荐更大的批量、更高的学习率、更多迭代）往往会损害经验隐私，揭示了效用与经验隐私之间的权衡。
*   **超参数影响规律**：回归分析表明，增加 \(b, T, \eta\) 中的任何一个都会损害经验隐私。在固定计算量 \(C\) 时，增大 \(b\) 并减小 \(T\) 有助于经验隐私；在固定更新步 \(U\) 时，减小 \(\eta\) 有助于经验隐私。
*   **启发式方法有效**：基于上述规律提出的超参数选择启发式在成对比较和模型选择任务中均显著优于基线方法（如选择最佳效用），能够更鲁棒地选出经验隐私更优的模型。
*   **原因初步探究**：
    1.  **“真实” ε 差异**：隐私审计得到的 \(\hat{\varepsilon}\) 在不同配置间确实存在差异，但它与效用强相关，而与经验隐私（记忆）不相关，表明现有的基于损失的审计方法可能无法有效捕捉经验隐私风险。
    2.  **隐私轮廓差异**：即使 (\(\varepsilon, \delta\)) 相同，不同配置的完整隐私轮廓（privacy profile）也存在交叉，这可能解释了其行为差异，但它对经验隐私的具体影响尚不明确。

### 7. 优点

*   **视角新颖且重要**：从一个实践性极强的角度审视差分隐私，揭示了理论与实践之间的关键鸿沟，对DP的标准化和实际部署具有重要意义。
*   **研究系统且深入**：不仅证明了现象的存在，还通过多维度实验、回归分析和启发式设计，系统解析了超参数的具体影响，并提出了缓解方案。
*   **实验扎实全面**：在多种模型、数据集、DP参数下进行了大量实验，控制变量严谨，结论的普遍性得到了很好的验证。
*   **提供了实用工具**：提出的启发式方法对实践者选择超参数具有直接的指导意义，能够在效用可接受的前提下，选择经验隐私风险更低的模型配置。
*   **诚实面对局限性**：文章坦诚地讨论了隐私审计、隐私轮廓等现有工具在解释该现象时的不足，并给出了清晰、有意义的研究方向。

### 8. 不足与局限

*   **评价指标的依赖**：经验隐私的定义和量化高度依赖于实验定义的具体“秘密”及其度量方式，这可能无法涵盖所有类型的隐私泄露场景。
*   **实验设置的简化**：研究基于标准LoRA微调、特定数据集和有限的 \(\varepsilon\) 范围，其结果向其他DP算法（如DP-FTRL）、不同任务和更严格隐私预算的泛化能力待进一步考证。
*   **“秘密”的统计特性**：研究中使用的秘密在数据集中高频出现，这与样本级DP的单元设定存在细微出入，尽管作者论证了这对“方差”研究的影响较小。
*   **理论解释尚浅**：对现象底层原因的探讨仅停留于“初步”阶段，未能完全解开为什么相同的理论保证会导致不同的经验表现，特别是“真实 \(\varepsilon\)”与记忆化的脱节问题未能得到解释。
*   **安全假设**：实验未考虑超参数搜索本身带来的额外隐私成本，这在实际安全审计中是需要考虑的因素。

（完）
