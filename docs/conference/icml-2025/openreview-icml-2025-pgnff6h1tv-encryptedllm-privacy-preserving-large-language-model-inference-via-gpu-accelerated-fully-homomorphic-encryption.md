---
title: "EncryptedLLM: Privacy-Preserving Large Language Model Inference via GPU-Accelerated Fully Homomorphic Encryption"
title_zh: "EncryptedLLM: 基于GPU加速全同态加密的隐私保护大语言模型推理"
authors: "Leo de Castro, Daniel Escudero, Adya Agrawal, Antigoni Polychroniadou, Manuela Veloso"
date: 2025-05-01
pdf: "https://openreview.net/pdf?id=PGNff6H1TV"
tags: ["query:daily"]
score: 9.0
evidence: 使用全同态加密保护LLM推理隐私
tldr: "针对大语言模型云端推理的查询隐私泄露风险,通过GPU加速全同态加密实现加密推理,速度比CPU基线提高200倍以上,使隐私保护推理走向实用。"
source: ICML-2025-Accepted
selection_source: conference_retrieval
figures_json: "[{\"url\": \"assets/figures/openreview/openreview-icml-2025-pgnff6h1tv/fig-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 677, \"height\": 424, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-icml-2025-pgnff6h1tv/fig-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 901, \"height\": 465, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-icml-2025-pgnff6h1tv/fig-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 809, \"height\": 463, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-icml-2025-pgnff6h1tv/fig-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 856, \"height\": 980, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-icml-2025-pgnff6h1tv/fig-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 852, \"height\": 474, \"label\": \"Figure\"}]"
tables_json: "[{\"url\": \"assets/tables/openreview/openreview-icml-2025-pgnff6h1tv/table-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 1543, \"height\": 451, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-icml-2025-pgnff6h1tv/table-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 771, \"height\": 237, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-icml-2025-pgnff6h1tv/table-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 838, \"height\": 194, \"label\": \"Table\"}]"
motivation: LLM云端推理可能泄露用户查询信息。
method: "利用GPU加速实现全同态加密,对GPT-2进行加密前向计算。"
result: 加密推理速度比CPU实现快200倍以上。
conclusion: GPU加速FHE使得隐私保护LLM推理变得可行。
---

## Abstract
As large language models (LLMs) become more powerful, the computation required to run these models is increasingly outsourced to a third-party cloud. While this saves clients' computation, it risks leaking the clients' LLM queries to the cloud provider. Fully homomorphic encryption (FHE) presents a natural solution to this problem: simply encrypt the query and evaluate the LLM homomorphically on the cloud machine. The result remains encrypted and can only be learned by the client who holds the secret key. In this work, we present a GPU-accelerated implementation of FHE and use this implementation to benchmark an encrypted GPT-2 forward pass, with runtimes over $200\times$ faster than the CPU baseline. We also present novel and extensive experimental analysis of approximations of LLM activation functions to maintain accuracy while achieving this performance.

---

## 论文详细总结（自动生成）

### 1. 论文的核心问题与整体含义
- **研究背景**：大语言模型（LLM）推理正越来越多地被外包至云端，但存在客户端查询隐私泄露的风险。
- **核心问题**：如何在不泄露用户输入的前提下，利用云端强大的算力完成LLM推理？
- **整体含义**：全同态加密（FHE）允许在加密数据上直接计算，是解决上述隐私问题的天然方案。然而，FHE运行LLM的巨大计算开销使其长期不切实际。本文旨在通过GPU加速，大幅缩短密文推理时间，探索FHE在隐私保护LLM服务中的实用化路径。

### 2. 论文提出的方法论
- **核心思路**：基于CKKS近似同态加密方案，将GPT‑2的前向传播全部转换为密文下的算术运算，并利用GPU并行计算实现显著加速。
- **关键技术细节**：
    - **GPU加速FHE库**：在OpenFHE库的基础上实现端到端的GPU加速CKKS方案，将耗时的数论变换（NTT）、RNS基变换及自举（bootstrapping）等操作迁移至GPU，并缓存所有计算密钥以避免数据搬运瓶颈。
    - **激活函数的FHE友好近似**（非多项式运算均用低次多项式逼近）：
        - **比较运算**：利用两组合成的9次多项式（f、g）逼近符号函数。
        - **GeLU**：采用分段三次和六次多项式拟合，并用上述比较函数判断分段区间。
        - **LayerNorm**：用泰勒展开初始化$1/\sqrt{z}$，再通过牛顿迭代（16~18次）精炼。
        - **Softmax**：用$(1+x/2^r)^{2^r}$近似指数函数；除法采用Goldschmidt迭代（14~22次）；最大值（max）改为预计算的查表固定值（经验估计），避免复杂的密文求最大值电路。
    - **计算流**：客户端将文本转为嵌入并加密，服务器在密文上逐层执行线性运算和上述近似非线性函数，最终返回加密结果。

### 3. 实验设计
- **测试场景与模型**：以GPT‑2 small为主要评测对象，同时用GPT‑2 medium和large验证近似函数的通用性。
- **精度基准**：在8个多样化自然语言理解任务（HellaSwag、ARC Easy、PIQA、Social IQa、MNLI、SST‑2、ANLI、WiC）上，对比未修改的原始模型与替换了近似激活函数的修改模型。
- **速度基准**：
    - 对比**CPU基线**（OpenFHE原实现）与**GPU加速实现**（本文方案）完成GPT‑2 small单token（位置128）加密前向传播的端到端时间。
    - 进一步测试**安全级别**（λ=128 vs. 80）和**批处理**（利用密文空闲槽位同时评估多个独立样本）对运行时间的影响。

### 4. 资源与算力
- **硬件环境**：CPU为Intel Xeon（2.4GHz）配2TB内存；GPU为单块NVIDIA A100 80GB PCIe。所有FHE推理基准均在此单GPU上运行。
- 论文不涉及任何训练过程，仅关注推理。算力开销主要来自密文下的多项式计算和自举操作。

### 5. 实验数量与充分性
- **实验数量**：涵盖了3种模型尺寸、8项下游任务精度评估、2种安全级别、以及批处理与非批处理的运行时间对比，并对核心的自举组件进行了独立的CPU/GPU性能对比（图4）。
- **充分性评价**：精度方面的实验较为全面，证明了近似函数对模型能力的损伤极小。速度评测聚焦于GPT‑2 small的单步解码，且假设前缀token已预先处理完毕。缺少对更大规模模型（如GPT‑2 XL）或端到端多token生成（含输入处理开销）的完整加密时延测量，也并未与同期其他FHE指型工作（如Zhang et al. 2024）进行直接横向对比。但作为一项以系统加速和可行性验证为主的工作，实验设计相对充分且公平。

### 6. 论文的主要结论与发现
- GPU加速的FHE将GPT‑2 small的单次加密前向传播时间从数小时缩短至几分钟，**相比CPU基准提速超过200倍**。
- 采用的多项式近似和固定最大值查表等优化，在维持极小精度损失的前提下，显著降低了密文计算深度和开销。
- 通过批处理和安全级别的灵活调整，能够进一步提升吞吐量，使得基于FHE的隐私保护文档摘要、定制微调等**非实时应用走向现实可行**。

### 7. 优点
- **工程贡献突出**：首次开源了与OpenFHE集成的GPU加速CKKS方案，并给出了完整的自举和模型层实现，对同态加密社区有独立价值。
- **近似方案系统且有效**：对transformer中所有关键非线性层（GeLU、LayerNorm、Softmax）均给出了适配FHE的低深度近似，并通过多任务实验严格验证了精度保持性。
- **优化策略多样**：综合运用了密钥缓存、密文槽批处理、安全级别与速度的权衡，体现了实用的系统设计思想。

### 8. 不足与局限
- **延迟仍远非实时**：加密推理仍需要分钟级，无法满足聊天机器人等实时交互场景。
- **模型规模和扩展性未验证**：仅对GPT‑2 small进行了完整的密文推理基准，未在更大尺寸（如medium、large）或其它架构的LLM上展示端到端运行时间，其“线性扩展”的说法未得到实验支撑。
- **依赖低精度假设**：整套方法成立的前提是LLM对低精度计算具有鲁棒性。若需高精度推理（如图像模型），则多项式次数和自举开销将急剧上升，方法优势会衰减。
- **威胁模型与实验局限**：不保障服务器模型的私有性（仅保护客户端输入），且实验中仅测量了单token生成，未涵盖完整输入序列的首遍编码开销及长序列生成的累计时间。
- **比较基线单一**：速度对比仅针对OpenFHE CPU实现，未与其它FHE LLM推理系统（如Zhang等人的工作）进行直接比较。

（完）
