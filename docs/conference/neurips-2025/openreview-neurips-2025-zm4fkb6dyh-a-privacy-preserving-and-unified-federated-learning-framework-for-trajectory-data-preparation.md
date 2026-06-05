---
title: A Privacy-Preserving and Unified Federated Learning Framework for Trajectory Data Preparation
title_zh: 面向轨迹数据准备的隐私保护统一联邦学习框架
authors: "Zhihao Zeng, Ziquan Fang, Wei Shao, Lu Chen, Yunjun Gao"
date: 2025-05-08
pdf: "https://openreview.net/pdf?id=zm4FKB6DYh"
tags: ["query:daily"]
score: 9.0
evidence: 轨迹数据准备的隐私保护联邦学习
tldr: 轨迹数据质量提升面临数据隐私和模型通用性两大挑战。本工作提出统一的隐私保护联邦学习框架，在避免原始轨迹数据共享的同时，通过协同训练提升数据质量，支持多种轨迹数据准备任务。实验证明该方法在隐私保护下有效提高轨迹分析准确性。
source: NeurIPS-2025-Rejected-Public
selection_source: conference_retrieval
figures_json: "[{\"url\": \"assets/figures/openreview/openreview-neurips-2025-zm4fkb6dyh/fig-001.webp\", \"caption\": \"\", \"page\": 2, \"index\": 1, \"width\": 1111, \"height\": 388}, {\"url\": \"assets/figures/openreview/openreview-neurips-2025-zm4fkb6dyh/fig-002.webp\", \"caption\": \"\", \"page\": 9, \"index\": 2, \"width\": 3079, \"height\": 564}, {\"url\": \"assets/figures/openreview/openreview-neurips-2025-zm4fkb6dyh/fig-003.webp\", \"caption\": \"\", \"page\": 23, \"index\": 3, \"width\": 2979, \"height\": 1131}, {\"url\": \"assets/figures/openreview/openreview-neurips-2025-zm4fkb6dyh/fig-004.webp\", \"caption\": \"\", \"page\": 24, \"index\": 4, \"width\": 3034, \"height\": 544}, {\"url\": \"assets/figures/openreview/openreview-neurips-2025-zm4fkb6dyh/fig-005.webp\", \"caption\": \"\", \"page\": 24, \"index\": 5, \"width\": 3116, \"height\": 1184}, {\"url\": \"assets/figures/openreview/openreview-neurips-2025-zm4fkb6dyh/fig-006.webp\", \"caption\": \"\", \"page\": 24, \"index\": 6, \"width\": 3121, \"height\": 1214}]"
motivation: 轨迹数据准备需考虑隐私，且现有方法缺乏通用性。
method: 提出统一的隐私保护联邦学习框架，解决隐私和通用性问题。
result: 在保护隐私的同时提升数据质量，适用于多种任务。
conclusion: 为位置隐私轨迹分析提供了新途径。
---

## Abstract
Trajectory data, which captures the movement patterns of people and vehicles over time and space, is crucial for applications such as traffic optimization and urban planning. However, issues such as noise and incompleteness often compromise data quality, leading to inaccurate trajectory analyses and limiting the potential of these applications. While Trajectory Data Preparation (TDP) can enhance data quality, existing methods suffer from two key limitations: (i) they do not address data privacy concerns, particularly in federated settings where trajectory data sharing is prohibited, and (ii) they typically design task-specific models that lack generalizability across diverse TDP scenarios. To overcome these challenges, we propose FedTDP, a privacy-preserving and unified framework that leverages the multi-task learning capabilities of Large Language Models (LLMs) for TDP in federated environments. Specifically, we: (i) design a trajectory privacy autoencoder for secure data transmission to protect data privacy with theoretical analysis, (ii) introduce a trajectory knowledge enhancer to develop TDP-oriented LLMs by improving model learning of TDP knowledge, and (iii) propose federated parallel optimization to enhance training efficiency by reducing data transmission and enabling parallel model training. Experiments on 6 real datasets and 10 mainstream TDP tasks demonstrate that FedTDP consistently outperforms 13 state-of-the-art baselines. All code and data are available at https://anonymous.4open.science/r/FedTDP.

---

## 论文详细总结（自动生成）

### 1. 论文的核心问题与整体含义

- **研究背景**：轨迹数据（如 GPS 轨迹）在交通优化、城市规划等应用中至关重要，但常受到噪声、缺失、不一致等质量问题影响，导致分析结果不准确。
- **现有局限**：
  - **隐私缺失**：现有轨迹数据准备（TDP）方法假设数据集中可用，无法应对联邦场景下数据共享受限的隐私约束。
  - **任务孤立**：传统方法为单一 TDP 任务设计，缺乏跨任务的通用性，每个任务需独立训练模型，成本高、泛化差。
- **研究目标**：提出 **FedTDP**，一个隐私保护、统一的多任务联邦学习框架，利用大语言模型（LLMs）的多任务能力，在保护各客户端轨迹数据隐私的同时，高效完成多种轨迹数据准备任务。

### 2. 方法论

FedTDP 框架包含服务端 LLM 与各客户端部署的小规模语言模型（SLM），通过三个核心模块应对挑战：

- **轨迹隐私自编码器（TPA）**
  - 作用：在跨客户端联合处理时保护原始轨迹数据隐私。
  - 关键技术：
    - 使用轻量三层 MLP 编码器将轨迹点编码为嵌入向量传输，保留时空相关性。
    - 引入基于秘密共享的**去中心化聚合**，客户端两两共享密钥，通过加掩码方式聚合模型参数块，保证聚合结果与原始参数聚合相等，同时抵抗嵌入与梯度反演攻击。
    - 提供互信息与 Fano 不等式的理论隐私分析，证明恢复原始数据的概率极低。

- **轨迹知识增强器（TKE）**
  - 作用：让 LLM/SLM 理解轨迹数据并掌握 TDP 知识。
  - 关键技术：
    - **轨迹提示工程**：构造 `(任务, 数据, 信息, 格式)` 的统一提示，融合路网、天气等公开上下文。
    - **轨迹异地微调**：将 LLM 的适配器层分发给客户端 SLM，利用 LoRA 减少参数量，训练后聚合更新。
    - **LoRA 稀疏微调**：按参数变化率概率选取 Top-m 层进行训练，降低通信与计算开销。
    - **双向知识学习**：SLM 用逆 KL 散度对齐 LLM 输出，LLM 用前向 KL 散度对齐 SLM 输出，实现知识迁移。

- **联邦并行优化（FPO）**
  - 作用：减少数据往返传输，加速训练。
  - 关键技术：
    - **分裂学习**：客户端负责 TPA 和 SLM 训练，服务端负责 LLM 训练。
    - **交替优化**：冻结客户端上传的嵌入用于服务端训练，冻结服务端输出的结果用于客户端训练，避免重复传输。
    - **并行训练**：客户端同时优化 TPA 重构损失、SLM-LLM 逆 KL 损失和 SLM 标签损失；服务端优化前向 KL 损失和标签损失。

### 3. 实验设计

- **数据集**：6 个真实轨迹数据集
  - GeoLife（训练/测试多个任务）
  - Porto、T-Drive、Tencent、Gowalla、SHL（用于未见任务的测试）
- **任务**：10 个主流 TDP 任务（异常检测、轨迹插补、噪声过滤、停留点检测、地图匹配、轨迹-用户链接、出行模式识别、轨迹简化、轨迹分割、轨迹恢复），涵盖数据清洗、匹配、标注、缩减、增强多种类型。
- **对比方法**（共 13 个 SOTA）：
  - 单任务方法：ATROM、Kamel、GraphMM、AttnTUL、Estimator、S3、LightTR
  - LLM 表格数据准备：FM4DP、MELD、TableGPT
  - LLM 时空分析：PromptGAT、UniST、UrbanGPT
- **评估指标**：F1 分数（大多数任务），SED（轨迹简化），运行时间与通信量（效率）。

### 4. 资源与算力

- 联邦环境：9 个节点（1 服务器 + 8 客户端），每个节点配置：
  - 2 个 Intel Xeon CPU E5-2650 12 核处理器
  - 2 个 GeForce RTX 3090 GPU
  - 100 MB/s 网络
- 未报告总训练时长，但效率实验给出运行时间与通信量对比，FedTDP 训练运行时比 LLM 基线降低约 11.3–14.2 倍，通信量有所增加但仍在可接受范围。

### 5. 实验数量与充分性

- **实验规模**：
  - 6 数据集 × 10 任务的主实验，比较 13 个基线。
  - 消融实验（移除 TPA / TKE / FPO），评估性能、运行时间、通信成本变化。
  - 模型泛化研究（训练任务数量从 1 到 7 变化）。
  - 模型基础研究（LLM 对比 Llama、GPT3、Qwen；SLM 对比 GPT3-Small、GPT2-Small、T5-Small）。
  - 效率研究（训练与测试阶段的通信量和运行时间）。
  - 参数敏感性实验（LoRA 稀疏微调比例 m 从 25% 到 100%）。
- **充分性**：实验覆盖多个维度，任务和基线丰富，结果均报告多次重复（5 次取平均），对比公平（基线结合差分隐私扩展以适应联邦场景），消融和参数分析深入，整体实验设计充分、客观。

### 6. 主要结论与发现

- FedTDP 在所有 6 个数据集和 10 个 TDP 任务上持续超越 13 个先进基线，性能提升 4.84% 至 45.22%。
- 相比非 LLM 轨迹方法至少提升 18.38%，相比表格 LLM 方法至少提升 32.26%。
- 在未见任务上表现优异，证明强大的泛化能力。
- TKE 模块带来超过 27.52% 的性能增益，FPO 将训练通信和运行时间降低近 4 倍，TPA 在保护隐私的同时性能损失极小且通信成本增加有限。

### 7. 优点

- **隐私与效用兼顾**：TPA 与秘密共享聚合在不加噪的条件下提供理论隐私保障，同时保持数据可用性。
- **统一多任务框架**：利用 LLM 多任务能力一次性支持十大 TDP 任务，避免单任务建模，节省资源。
- **高效训练设计**：SLM 与 LLM 协同、LoRA 稀疏微调、分裂并行优化大幅降低通信与计算开销。
- **模块化与可扩展**：框架组件解耦，可灵活替换模型基座或扩展新任务。
- **实验扎实**：多种数据集、大量基线、详细消融与效率分析，结果可靠且复现性强（代码与数据开源）。

### 8. 不足与局限

- **任务范围局限**：当前仅覆盖轨迹数据准备（清洗、匹配等），未探索聚类、模式挖掘等下游分析任务。
- **模型可解释性不足**：LLM 在 TDP 中的决策过程缺乏解释，实际部署的可信度受限。
- **隐私分析假设**：理论分析基于半诚实对手模型，未充分考虑更强的攻击（如恶意服务端合谋）；同时未与其他隐私保护技术（如同态加密）直接对比。
- **资源要求较高**：尽管优化后效率提升，但仍需在服务端部署 LLM（如 Llama-8B），对客户端硬件（双 RTX 3090）也有一定要求，轻量化移动端部署待验证。
- **实验设定**：联邦节点固定为 9 个，未充分测试不同客户端规模和数据异质性下的表现。

（完）
