---
title: "FedRW: Efficient Privacy-Preserving Data Reweighting for Enhancing Federated Learning of Language Models"
title_zh: FedRW：用于增强联邦语言模型训练的隐私保护数据重加权方法
authors: "Pukang Ye, Junwei Luo, Jiachen Shen, Saipan Zhou, Shangmin Dou, Zhenfu Cao, Hanzhe Yao, Xiaolei Dong, Yunbo Yang"
date: 2025-09-18
pdf: "https://openreview.net/pdf?id=cy6MGBwToV"
tags: ["query:daily"]
score: 9.0
evidence: 面向联邦大模型的隐私保护数据重加权
tldr: 联邦大模型训练中数据重复既损害性能又威胁隐私。本文提出FedRW，首个不需要可信第三方的隐私保护软去重框架，通过安全多方计算实现频率感知的样本重加权而非直接删除。实验表明FedRW在保护数据隐私的同时提升了模型质量，为联邦学习中的数据质量管理提供了隐私合规的新思路。
source: NeurIPS-2025-Accepted
selection_source: conference_retrieval
figures_json: "[{\"url\": \"assets/figures/openreview/openreview-neurips-2025-cy6mgbwtov/fig-001.webp\", \"caption\": \"\", \"page\": 4, \"index\": 1, \"width\": 2052, \"height\": 976}]"
motivation: 联邦大模型训练中数据重复导致模型性能下降和隐私风险，传统去重依赖可信第三方、易丢失信息且引入隐私漏洞。
method: 设计基于安全多方计算的频率感知重加权协议，实现训练样本的软去重。
result: 在联邦LLM训练中，FedRW在隐私保护下实现去重并提升模型性能，优于传统方法。
conclusion: FedRW为联邦学习中的数据质量管理提供了隐私保护的解决方案，验证了软去重的有效性。
---

## Abstract
Data duplication within large-scale corpora often impedes large language models' (LLMs) performance and privacy. In privacy-concerned federated learning scenarios, conventional deduplication methods typically rely on trusted third parties to perform uniform deletion, risking loss of informative samples while introducing privacy vulnerabilities. To address these gaps, we propose Federated ReWeighting (FedRW), the first privacy-preserving framework, to the best of our knowledge, that performs soft deduplication via sample reweighting instead of deletion in federated LLM training, without assuming a trusted third party. At its core, FedRW proposes a secure, frequency-aware reweighting protocol through secure multi-party computation, coupled with a parallel orchestration strategy to ensure efficiency and scalability. During training, FedRW utilizes an adaptive reweighting mechanism with global sample frequencies to adjust individual loss contributions, effectively improving generalization and robustness. Empirical results demonstrate that FedRW outperforms the state-of-the-art method by achieving up to $28.78\times$ speedup in preprocessing and approximately $11.42$\% improvement in perplexity, while offering enhanced security guarantees. FedRW thus establishes a new paradigm for managing duplication in federated LLM training.

---

## 论文详细总结（自动生成）

### 1. 论文的核心问题与整体含义

- **研究动机**：大规模语言模型（LLM）的训练语料中广泛存在数据重复现象。这些重复样本不仅会降低模型的泛化能力，增加记忆化风险，还容易引发模型反转（Model Inversion）、成员推断（Membership Inference）等隐私攻击。
- **核心矛盾与挑战**：在联邦学习（FL）场景下，由于数据分散在各个客户端且受隐私保护，传统的全局去重方法无法直接应用。
    - **本地去重**无法检测跨客户端的重复。
    - **全局去重**在无隐私泄露风险下难以实现。
    - 现有的联邦去重方法（如 EP-MPD）依赖**可信第三方**（TTP）进行加密去重，存在单点信任风险。且其“硬去重”（直接删除重复样本）方式可能丢失有价值的信息，损害模型在数据稀疏场景下的鲁棒性。
- **整体含义**：论文旨在提出一种**无需可信第三方**、**不直接删除样本**的隐私保护“软去重”框架，通过为样本分配权重而非物理删除来管理冗余数据，从而在保护隐私的同时提升联邦 LLM 的训练质量。

### 2. 论文提出的方法论

- **核心思想**：用“软去重”替代“硬删除”。FedRW 框架的核心是根据样本在全体客户端中的**全局出现频率**来为每个样本动态分配权重，频率越高的样本对训练损失的贡献越低。整个过程通过安全多方计算（MPC）实现，无需任何可信第三方介入。

- **关键技术细节**：
    - **隐私保护多方重加权协议（PPMPR）**：
        - **目标**：在 n 个客户端间，安全地计算每个样本的全局频率，并据此生成权重向量。
        - **核心构建块——两方计算协议 (Π2PC)**：利用私有集合交集（PSI）技术，让两个客户端在不泄露各自完整数据集的条件下，互相告知对方自己持有多少对方的样本。流程为：双方执行 PSI 得到交集，交换交集样本的本地出现频率。
        - **全协议 (ΠPPMPR)**：每个客户端首先用本地频率初始化全局频率向量，然后执行 n-1 轮 Π2PC，与所有其他客户端依次进行交互，每次交互后更新自己的全局频率向量。
    - **并行加速策略**：朴素方式下，所有客户端两两交互的复杂度为 O(n²)。FedRW 提出一种分层并行调度策略，将客户端划分为不重叠的块，在每层内部并行执行多组 Π2PC，将整体协议的时间复杂度降至 O(⌈log₂ n⌉)。
    - **自适应重加权**：计算出全局频率 ⃗C 后，权重向量 ⃗W 通过公式 ⃗W = 1 / (ln(⃗C + ⃗1) + ⃗ε) 计算。此对数惩罚函数能够平缓地降低高频样本的损失贡献，避免极端权重。
    - **增强训练**：在训练时，每个批次的总损失按照样本权重的加权平均来计算，再通过 FedAvg 算法聚合模型更新。

### 3. 实验设计

- **数据集与场景**：
    - **协议性能评估**：在不同数据集大小（2¹⁰ 至 2²⁰ 样本）、客户端数量（10 – 50）和重复率（10% – 90%）下评测 Π2PC 和 PPMPR 的运行时间。
    - **FL 模型训练评估**：使用了 **8 个公开文本数据集**：**Haiku**、**Rotten Tomatoes**、**Short Jokes**、**Poetry**、**IMDB**、**Sonnets**、**Plays** 和 **Twitter Sentiment Analysis**。为模拟冗余，人为向训练数据中注入不同比例（10%, 20%, 30%）的重复样本，并均匀分配到 10 个客户端。
    - **非独立同分布（Non-IID）场景**：涵盖数量偏斜、标签偏斜、特征偏斜三种情况（基于 Qwen3-0.6B 模型测试）。
- **Benchmark 与对比方法**：
    - **主Baseline**：**EP-MPD**（当前最先进的联邦硬去重方法，依赖可信第三方）。
    - 还包含了**原始数据**（Raw Data，不经任何去重处理）作为对比。
    - **模型范围广**：从相对基础的 **GPT-2 Large** 和 **DistilGPT2**，到更新的主流模型 **Qwen3-0.6B**、**Qwen2.5-0.5B-Instruct**、**Llama-3.2-1B-Instruct**，再到大参数量的 **Qwen2.5-3B-Instruct**、**Qwen2.5-7B-Instruct**。
- **评价指标**：预处理阶段主要看**运行时间**（加速比）；模型性能主要看测试集上的**困惑度（Perplexity）**。

### 4. 资源与算力

- **协议（预处理）部分**：在一台配备 **4 核 Intel Xeon 2.20GHz CPU** 和 **32GB RAM** 的虚拟化服务器上执行。
- **模型训练部分**：在一台配备 **20 核 Intel Xeon Platinum 8457C CPU**、**200GB RAM** 和单张 **NVIDIA H20 GPU（96GB 显存）** 的机器上执行。
- **训练时长及能耗**：论文未明确报告具体的总训练时长（如 GPU 小时数）或能耗。

### 5. 实验数量与充分性

- **实验组数**：实验设计**相对充分**，覆盖了多个维度：
    - **预处理效率评估**：3 组实验（数据集大小、客户端数量、重复率的影响）。
    - **模型性能评估**：在 8 个数据集上，针对 6 种不同参数量级和架构的模型，进行了 3 种不同重复率下的测试，外加一组 Non-IID 场景实验，总计**至少数十组**对比。
    - **可复现性**：文中详细说明了数据集来源、切分方式、超参数（学习率、epoch、批大小等）和硬件环境，实验可复现性较高。
- **公平性与客观性**：
    - 与 EP-MPD 基线对比时，遵循了其原始实验设置，并使用官方开源代码和一致的下游训练配置，保证了比较的公平性。
    - 对预处理运行时间进行了多次重复（4 次）取平均，增强了结果的可靠性。
    - 有一个小的局限性：在进行模型性能对比时，实验结果表格中基线 EP-MPD 的数据仅报告了单一值，未像 FedRW 那样报告不同重复率下的结果，这可能是因为硬去重结果与初始重复率无关，但仍构成一定的信息不对称。

### 6. 论文的主要结论与发现

- **显著的效率提升**：相比依赖可信第三方的 SOTA 基线 EP-MPD，FedRW 的 PPMPR 协议凭借高效的 Π2PC 和并行调度，在 10 到 50 个客户端的规模下实现了**最高 28.78 倍的处理加速**。
- **稳定的模型性能改进**：FedRW 在几乎所有测试配置下均优于硬去重基线，在结构严谨的数据集上效果尤为突出，如在 Haiku 数据集上困惑度相对降低了**约 11.42%**。同时，其性能在不同重复率下表现稳定，而硬去重可能导致性能波动。
- **资源受限场景下的鲁棒性**：在小模型（DistilGPT2）和数据稀疏的文学数据集上，硬去重因剔除大量样本反而可能损害性能，而 FedRW 的软重加权策略能保持数据完整性，获得更好的泛化效果。
- **良好的泛化性**：在多个最新的 LLM 架构（Qwen, Llama）和异构非独立同分布数据场景下，FedRW 均展现出持续的优势，证明了其作为一种通用模块的有效性。

### 7. 优点

- **新颖的范式**：首次在联邦 LLM 训练中提出“软去重”的隐私保护框架，填补了从“硬删除”到“频率感知重加权”的空白。
- **强大的隐私与去中心化设计**：方案不依赖任何可信第三方，所有交互仅发生在客户端之间，通过成熟的 PSI 协议实现，并提供半诚实模型下的形式化安全证明，安全性更强。
- **精妙的可扩展性设计**：通过分层并行的编排策略，将协议复杂度从 O(n²) 降至对数级，展现出优秀的横向扩展能力。
- **全面的实验验证**：实验设计维度丰富，涵盖多种模型规模（0.5B 到 7B）、多种数据类型和 Non-IID 场景，论证充分，令人信服。

### 8. 不足与局限

- **安全模型假设**：目前方案基于**半诚实（Semi-honest）** 敌手模型，假设所有参与者会遵守协议但试图窥探信息。这在某些高安全性要求的场景中可能不足，论文未实现对抗恶意客户端的机制（如零知识证明）。
- **缺乏训练成本分析**：论文重点关注预处理阶段的加速，但未报告引入样本重加权后的**总训练时长**、**通信开销**和**计算开销**是否增加，缺少端到端的成本收益比分析。
- **朴素频率启发式**：权重与全局频率反相关是一个直观但可能不是最优的策略，未探索更复杂的、与模型训练动态结合的自适应加权方法。
- **语义重复的局限**：目前的协议基于精确匹配，无法解决近义或语义层面的重复问题，这可能限制了在真实世界复杂语料上的应用效果。

（完）
