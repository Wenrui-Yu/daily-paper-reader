---
title: Leveraging Randomness in Model and Data Partitioning for Privacy Amplification
title_zh: 利用模型与数据划分中的随机性实现隐私放大
authors: "Andy Dong, Wei-Ning Chen, Ayfer Ozgur"
date: 2025-05-01
pdf: "https://openreview.net/pdf?id=3K6BkFZ7ka"
tags: ["query:daily"]
score: 9.0
evidence: 证明联邦学习中的模型切分和dropout提供隐私放大效果
tldr: 联邦学习中，客户端每次仅更新部分模型或处理部分数据，这种随机划分可提供隐私放大。本文为数据和模型划分建立了统一的隐私放大分析框架，证明模型并行中的子网络更新和dropout等技术能显著增强差分隐私保障，该增益未被先前分析捕捉。实验验证了理论结果，为高效且私密的联邦学习设计提供了新视角。
source: ICML-2025-Accepted
selection_source: conference_retrieval
figures_json: "[{\"url\": \"assets/figures/openreview/openreview-icml-2025-3k6bkfz7ka/fig-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 843, \"height\": 644, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-icml-2025-3k6bkfz7ka/fig-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 843, \"height\": 657, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-icml-2025-3k6bkfz7ka/fig-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 848, \"height\": 648, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-icml-2025-3k6bkfz7ka/fig-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 843, \"height\": 622, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-icml-2025-3k6bkfz7ka/fig-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 795, \"height\": 590, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-icml-2025-3k6bkfz7ka/fig-006.webp\", \"caption\": \"\", \"page\": 0, \"index\": 6, \"width\": 794, \"height\": 603, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-icml-2025-3k6bkfz7ka/fig-007.webp\", \"caption\": \"\", \"page\": 0, \"index\": 7, \"width\": 793, \"height\": 602, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-icml-2025-3k6bkfz7ka/fig-008.webp\", \"caption\": \"\", \"page\": 0, \"index\": 8, \"width\": 792, \"height\": 603, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-icml-2025-3k6bkfz7ka/fig-009.webp\", \"caption\": \"\", \"page\": 0, \"index\": 9, \"width\": 796, \"height\": 592, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-icml-2025-3k6bkfz7ka/fig-010.webp\", \"caption\": \"\", \"page\": 0, \"index\": 10, \"width\": 798, \"height\": 586, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-icml-2025-3k6bkfz7ka/fig-011.webp\", \"caption\": \"\", \"page\": 0, \"index\": 11, \"width\": 800, \"height\": 582, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-icml-2025-3k6bkfz7ka/fig-012.webp\", \"caption\": \"\", \"page\": 0, \"index\": 12, \"width\": 800, \"height\": 586, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-icml-2025-3k6bkfz7ka/fig-013.webp\", \"caption\": \"\", \"page\": 0, \"index\": 13, \"width\": 793, \"height\": 616, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-icml-2025-3k6bkfz7ka/fig-014.webp\", \"caption\": \"\", \"page\": 0, \"index\": 14, \"width\": 791, \"height\": 614, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-icml-2025-3k6bkfz7ka/fig-015.webp\", \"caption\": \"\", \"page\": 0, \"index\": 15, \"width\": 792, \"height\": 614, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-icml-2025-3k6bkfz7ka/fig-016.webp\", \"caption\": \"\", \"page\": 0, \"index\": 16, \"width\": 789, \"height\": 620, \"label\": \"Figure\"}]"
tables_json: "[{\"url\": \"assets/tables/openreview/openreview-icml-2025-3k6bkfz7ka/table-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 863, \"height\": 623, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-icml-2025-3k6bkfz7ka/table-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 850, \"height\": 405, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-icml-2025-3k6bkfz7ka/table-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 851, \"height\": 403, \"label\": \"Table\"}]"
motivation: 联邦学习中的随机划分带来的隐私放大效应未被充分量化。
method: 建立统一框架分析数据划分和模型划分的隐私放大，应用至模型并行。
result: 证明模型切分和dropout能提供额外的隐私放大，提升DP保障。
conclusion: 利用训练随机性可有效增强联邦学习的隐私性，无需额外开销。
---

## Abstract
We study how inherent randomness in the training process—where each sample (or client in federated learning) contributes only to a randomly selected portion of training—can be leveraged for privacy amplification. This includes (1) data partitioning, where a sample participates in only a subset of training iterations, and (2) model partitioning, where a sample updates only a subset of the model parameters. We apply our framework to model parallelism in federated learning, where each client updates a randomly selected subnetwork to reduce memory and computational overhead, and show that existing methods, e.g. model splitting or dropout, provide a significant privacy amplification gain not captured by previous privacy analysis techniques. Additionally, we introduce balanced iteration subsampling, a new data partitioning method where each sample (or client) participates in a fixed number of training iterations. We show that in certain regimes, this method yields stronger privacy amplification than Poisson (i.i.d.) sampling of data (or clients). Our results demonstrate that randomness in the training process, which is  structured rather than i.i.d. and interacts with data in complex ways, can be systematically leveraged for nontrivial privacy amplification.

---

## 论文详细总结（自动生成）

## 1. 论文的核心问题与整体含义

- **核心问题**：在差分隐私（DP）的机器学习训练中，除了注入大量噪声，能否利用训练过程中固有的、结构化的随机性来获得“隐私放大”效果，从而减少所需的噪声量、提升模型性能。
- **具体场景**：联邦学习与分布式训练中，客户端或样本只参与训练的某个随机部分，例如：
  - **数据划分**：每个样本只参与一部分训练迭代；
  - **模型划分**：每个样本（或客户端）只更新模型的一个随机子网络（如模型并行、dropout）。
- **研究动机**：
  - 现有隐私分析技术（如DP-SGD的标准核算）未考虑模型划分带来的隐私增益；
  - 常见的数据划分方法（如Poisson子采样）存在参与不均匀、系统负载不可预测等实际局限；
  - 亟需一套统一框架，将这类“与数据复杂交互的结构化随机性”系统地转化为可量化的隐私放大。

## 2. 论文提出的方法论

- **统一隐私放大框架**：基于Rényi差分隐私（RDP），建立了一个计算混合高斯分布与标准高斯分布之间Rényi散度上界的数学工具（Theorem 3.1）。
- **关键技术思路**：
  - 将隐私泄露建模为：攻击者区分训练时是否使用了特定样本，对应观察到的梯度分布是两个高斯混合的差异。
  - 通过引理分解Rényi散度，将“前向散度”与“反向散度”分别上界化，得到可数值计算或进一步简化的表达式。
  - 最终结果为两个可计算的上界公式（2）和更高效的（3）。
- **应用于模型并行（模型划分）**：
  - **不相交模型分割**（Disjoint Model Splitting）：模型被划分为$d$个不相交子网络，每个客户端随机选取一个子网络更新其梯度（梯度裁剪、加噪）。算法1描述了差分隐私的模型并行训练流程。
  - **部分模型分割**：将模型分为“拆分部分”和“不拆分部分”，分别核算隐私损失后加总（直接应用RDP的组合性）。
  - **Dropout**：揭示dropout可视为一种隐式模型并行（随机停用神经元），在dropout rate=0.5的特殊情况下，可套用模型分割的隐私放大结论（Algorithm 2，Corollary 3.7）。
  - 上述场景的隐私核算均可通过Theorem 3.1（k=1）完成。
- **应用于数据划分：平衡迭代子采样（Balanced Iteration Subsampling）**：
  - 每个样本（或客户端）在整个训练过程中恰好参与$k$个随机选择的迭代（共$T$次迭代）。
  - 与Poisson子采样相比，确保了每个样本的参与次数固定，具有更好的公平性和系统稳定性。
  - 通过Theorem 3.1（d=T）给出对应的RDP保证。

## 3. 实验设计

- **数据集**：CIFAR-10。
- **模型**：
  - 模型分割实验：ResNet-101（进行有预训练的半数据集微调）。
  - 子采样实验：WideResNet-40-4（从头训练）与ResNet-101（微调）。
- **隐私保护场景**：
  - 集中式：样本级(8,10^{-5})-DP；
  - 联邦式：用户级(8,10^{-5})-DP，每个用户持有2个样本。
- **对比方法**：
  - **Baseline**：使用模型分割/子采样进行训练，但隐私核算采用标准DP-SGD方法（不享受模型划分带来的放大）。
  - **Amplification (Ours)**：采用本文的隐私核算框架，放大效果被计入。
  - **Relaxation**：不使用模型分割，每个客户端训练完整模型，隐私核算为标准DP-SGD。
  - 平衡迭代子采样与Poisson子采样进行对比（均达到相同DP预算时比较所需噪声和准确率）。
- **评估指标**：验证准确率、所需噪声标准差。

## 4. 资源与算力

- 文中仅在致谢部分提到“部分计算在斯坦福大学的Sherlock集群上完成”，但**未明确给出**所使用的GPU型号、数量、训练总时长等具体算力信息。

## 5. 实验数量与充分性

- **模型分割**：在集中式和联邦两种设置下，分别测试了子模型数量$d=3$和$d=8$，每组重复3个随机种子（标准差约0.7%）。共给出两张对比表格。
- **平衡迭代子采样**：
  - 在两种不同的训练任务（从零训练WideNet、微调ResNet）上，与Poisson子采样进行对比，每种方法重复3个随机种子。
- **理论分析可视化**：附录中补充了大量不同参数（$T$、$k$、$\epsilon$、$\delta$、噪声标准偏差、迭代次数）下的曲线对比（模型分割与无放大、平衡迭代子采样与Poisson子采样）。
- **综合评估**：实验量中等，聚焦于验证理论发现而非大规模的基准测试。实验对比直接、公平，能够支撑“模型分割带来额外隐私增益”和“平衡迭代子采样与大T下的Poisson子采样性能相近、小T时更优”的核心结论。但未涉及更多样化的数据集或模型结构。

## 6. 论文的主要结论与发现

- **模型划分的隐私放大**：模型并行中普遍使用的模型分割和dropout（rate=0.5）存在之前未被核算的显著隐私放大效应。应用本文理论后，可在同等DP预算下降低注入的噪声量，从而提升联邦/分布式场景下的模型准确率。
- **平衡迭代子采样**：提供了一种Poisson子采样的实用替代方案。当$T$较大时，其隐私保证与Poisson子采样极其接近；当$T$较小时，其在Rényi DP高阶矩（$\alpha$大）下显著优于Poisson子采样，并在$( \epsilon, \delta)$-DP域下允许更多的训练迭代。
- **统一框架的价值**：证明了随机性（无论是数据层面还是模型层面的结构化随机）可以通过同一套数学工具转化为可量化的隐私增益，该框架为后续进一步挖掘训练过程中的其他随机性来源奠定了分析基础。

## 7. 优点

- **创新性强**：首次系统量化了模型并行（模型分割、dropout）的隐私放大效应，在此之前该增益未被现有技术捕获。
- **理论坚实**：给出了严谨的RDP界推导，从混合高斯-高斯散度入手，为后续工作提供了可参考的分析模板。
- **实用导向**：直接应用于联邦学习中常见的模型并行策略和dropout，无需改变训练算法即可享受隐私增益；提出的平衡迭代子采样兼顾公平性、稳定性和隐私保护，具有落地潜力。
- **实验验证**：在真实的联邦和集中训练设置下验证了理论增益，增益幅度具有实际意义。

## 8. 不足与局限

- **理论紧致性**：作者指出子网络生成方式为不相交划分的随机混合时，当前界可能还有收紧空间（Theorem 3.5的注记）。
- **实验覆盖范围**：
  - 仅在CIFAR-10单一数据集上进行了实验，未在更大规模或更多样化数据上验证。
  - 模型分割实验基于ResNet-101微调，未涉及不同架构（如Transformer）的广泛测试。
- **dropout分析的适用范围**：当前严格的分析仅针对dropout rate=0.5的情况，更一般的dropout率下的隐私放大仍有待分析。
- **平衡迭代子采样在大T时的优势**：当迭代次数极大时，该方法的实际隐私益处与Poisson子采样几乎无差异，其实操价值主要体现在小或中等$T$的场景。

（完）
