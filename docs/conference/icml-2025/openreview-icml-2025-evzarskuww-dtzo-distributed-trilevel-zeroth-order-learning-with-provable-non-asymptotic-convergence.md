---
title: "DTZO: Distributed Trilevel Zeroth Order Learning with Provable Non-Asymptotic Convergence"
title_zh: "DTZO: 具有可证明非渐近收敛的分布式三层零阶学习"
authors: "Yang Jiao, Kai Yang, Chengtao Jian"
date: 2025-06-06
pdf: "https://openreview.net/pdf?id=EvzArsKUww"
tags: ["query:daily"]
score: 10.0
evidence: 分布式三层零阶学习保护数据隐私
tldr: 针对分布式场景下梯度不可得带来的隐私与优化难题，提出DTZO框架，利用零阶信息进行分布式三层学习，避免泄露梯度，并证明非渐近收敛速度，为隐私保护分布式优化提供了有效方法。
source: ICML-2025-Accepted
selection_source: conference_retrieval
figures_json: "[{\"url\": \"assets/figures/openreview/openreview-icml-2025-evzarskuww/fig-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 1175, \"height\": 417, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-icml-2025-evzarskuww/fig-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 1359, \"height\": 472, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-icml-2025-evzarskuww/fig-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 1361, \"height\": 473, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-icml-2025-evzarskuww/fig-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 596, \"height\": 485, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-icml-2025-evzarskuww/fig-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 650, \"height\": 466, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-icml-2025-evzarskuww/fig-006.webp\", \"caption\": \"\", \"page\": 0, \"index\": 6, \"width\": 635, \"height\": 472, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-icml-2025-evzarskuww/fig-007.webp\", \"caption\": \"\", \"page\": 0, \"index\": 7, \"width\": 637, \"height\": 532, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-icml-2025-evzarskuww/fig-008.webp\", \"caption\": \"\", \"page\": 0, \"index\": 8, \"width\": 635, \"height\": 470, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-icml-2025-evzarskuww/fig-009.webp\", \"caption\": \"\", \"page\": 0, \"index\": 9, \"width\": 638, \"height\": 533, \"label\": \"Figure\"}]"
tables_json: "[{\"url\": \"assets/tables/openreview/openreview-icml-2025-evzarskuww/table-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 1681, \"height\": 476, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-icml-2025-evzarskuww/table-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 877, \"height\": 1201, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-icml-2025-evzarskuww/table-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 1609, \"height\": 393, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-icml-2025-evzarskuww/table-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 1580, \"height\": 1411, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-icml-2025-evzarskuww/table-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 1319, \"height\": 420, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-icml-2025-evzarskuww/table-006.webp\", \"caption\": \"\", \"page\": 0, \"index\": 6, \"width\": 1264, \"height\": 304, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-icml-2025-evzarskuww/table-007.webp\", \"caption\": \"\", \"page\": 0, \"index\": 7, \"width\": 1371, \"height\": 359, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-icml-2025-evzarskuww/table-008.webp\", \"caption\": \"\", \"page\": 0, \"index\": 8, \"width\": 1528, \"height\": 448, \"label\": \"Table\"}]"
motivation: 数据隐私或模型不透明导致无法获取梯度，现有方法难以处理分布式三层优化。
method: 提出DTZO框架，基于零阶估计解决分布式三层学习问题。
result: 证明了DTZO的非渐近收敛性，有效保护数据隐私。
conclusion: DTZO为分布式隐私保护优化提供了一种可行的零阶方法。
---

## Abstract
Trilevel learning (TLL) with zeroth order constraints is a fundamental problem in machine learning, arising in scenarios where gradient information is inaccessible due to data privacy or model opacity, such as in federated learning, healthcare, and financial systems. These problems are notoriously difficult to solve due to their inherent complexity and the lack of first order information. Moreover, in many practical scenarios, data may be distributed across various nodes, necessitating strategies to address trilevel learning problems without centralizing data on servers to uphold data privacy. To this end, an effective distributed trilevel zeroth order learning framework DTZO is proposed in this work to address the trilevel learning problems with level-wise zeroth order constraints in a distributed manner. The proposed DTZO is versatile and can be adapted to a wide range of (grey-box) trilevel learning problems with partial zeroth order constraints. In DTZO, the cascaded polynomial approximation can be constructed without relying on gradients or sub-gradients, leveraging a novel cut, i.e., zeroth order cut. Furthermore, we theoretically carry out the non-asymptotic convergence rate analysis for the proposed DTZO in achieving the $\epsilon$-stationary point. Extensive experiments have been conducted to demonstrate and validate the superior performance of the proposed DTZO.

---

## 论文详细总结（自动生成）

### 1. 论文的核心问题与整体含义
- **研究问题**：在分布式环境中，由于数据隐私、模型黑箱等限制，无法获得梯度信息，需要零阶优化。同时，许多机器学习任务（如鲁棒超参数优化、后门攻击）本身呈现三层嵌套结构。现有分布式零阶优化方法仅能处理单层或双层问题，无法解决三层零阶学习问题。
- **核心贡献**：本文首次提出并解决了分布式三层零阶优化问题，设计了一个通用且具有可证明收敛性的框架 DTZO，填补了三层嵌套优化在零阶信息下的理论和方法空白。

### 2. 提出的方法论
- **总体框架**：将分布式三层零阶学习问题转化为带共识变量的等价形式，并借助**级联零阶多项式近似**（内层 + 外层）将下层优化约束放松为多项式不等式。
- **关键技术创新：零阶割**  
  - 核心操作是生成**零阶割**，即无需使用梯度或次梯度即可构造切割平面：通过对约束函数进行高斯平滑，并利用双点零阶梯度估计器获得近似切线，从而生成二次多项式的切割平面。
  - 内层割用于逼近第三层优化的最优性条件约束；外层割用于逼近第二层优化的约束。  
  - 随着割的加入，可行域不断被收紧，形成对原问题的级联多项式松弛。
- **算法流程**  
  - **本地 Worker**：利用零阶梯度估计器更新三层局部变量，并上传至 Master。
  - **Master**：更新全局共识变量，并广播更新后的共识变量及外层割的梯度信息。
  - 每 T 次迭代，Master 会生成新的内/外层零阶割，并剔除不活跃的割，以动态调整多项式近似。
  - 采用外部惩罚函数法将级联约束问题转化为无约束优化问题。
- **理论保证**  
  - 给出非渐近收敛分析，证明 DTZO 达到 $\epsilon$-稳定点的迭代复杂度为 $\mathcal{O}(1/\epsilon^2)$，通信复杂度为 $\mathcal{O}(T(\epsilon)(d_1 + d_2 + d_3)N + \text{割更新开销})$。
  - 该结果是首次为三层零阶优化提供收敛性保证。

### 3. 实验设计
- **场景一：黑盒大语言模型的三层学习**  
  - 任务：在黑盒 Qwen‑2-7B、Llama‑3.1‑8B、Qwen‑1.8B‑Chat 上实现后门攻击，同时保持清洁样本性能。
  - 数据集：GLUE 基准中的 SST‑2、COLA、MRPC。
  - 指标：攻击成功率（ASR）和清洁样本准确率（ACC）。
  - 主要对比方法：FedRZO_bl（分布式双层零阶优化）。
- **场景二：鲁棒超参数优化**  
  - 任务：鲁棒超参数优化，对抗 PGD‑7 攻击。
  - 数据集：MNIST、QMNIST、Fashion‑MNIST、USPS、MelbournePedestrian、Crop、UWaveGestureLibraryAll。
  - 对比方法：FedZOO、FEDNEST+ZO、ADBO+ZO、FedRZO_bl、AFTO+ZO（将现有分布式嵌套优化方法配备零阶估计器，无理论保证）。
  - 指标：平均清洁准确率与对抗鲁棒性的综合得分。
- **消融与敏感性实验**  
  - 分析级联近似控制参数 T1、平滑参数 μ 的影响。
  - 验证去除不活跃割对训练效率的提升。
  - 对比 DTZO 的变体（如使用线性割、仅用单层多项式近似），证明非线性割与级联近似的增益。

### 4. 资源与算力
- 所有模型使用 PyTorch 实现。
- 实验环境：**两台 NVIDIA RTX 4090 GPU** 服务器。
- 未具体报告训练总时长、GPU 显存消耗等细节。

### 5. 实验数量与充分性
- 涵盖 **2 个主要应用场景、7 个不同数据域**（3 个 NLP + 4 个图像 + 3 个时间序列）。
- 对比 **5 种以上分布式零阶/嵌套优化方法**，包括直接与现有零阶方法比较以及将一阶方法强制适配零阶。
- 包含参数敏感性分析、消融实验、不活跃割剪枝效果验证，实验设计较完整，评估角度较公平客观。

### 6. 主要结论与发现
- DTZO 在所有任务上均明显优于现有分布式零阶优化方法，特别是在三层嵌套任务上展现了解决高层嵌套零阶问题的能力。
- 级联多项式近似与非线性的零阶割是实现高性能和可证明收敛的关键。
- 通过调节单参数 T1 可灵活权衡近似精度与计算通信开销。
- 去除不活跃割能显著降低训练时间，而对最终性能影响甚微。

### 7. 优点
- **首次**填补了三层零阶优化理论与方法的空白，并给出正式收敛分析。
- 零阶割设计新颖，不依赖梯度，适用于完全黑箱或灰箱场景。
- 框架可扩展至部分梯度可用的灰箱三层优化及双层零阶优化。
- 分布式实现基于参数服务器，贴合物联网、联邦学习等隐私敏感场景。
- 实验覆盖场景广，验证充分，且提供了良好的可调节性。

### 8. 不足与局限
- **维数依赖较高**：收敛复杂度为 $\mathcal{O}(d^6/\epsilon^2)$，变量维度高时计算负担大。
- **假设较强**：理论依赖有界域和 Lipschitz 光滑性，在非光滑或高度非凸问题中可能受限。
- **实验硬件细节不足**：未报告单个实验的训练时间与显存占用，难以评估实际部署成本。
- **比较基线缺少更深度的零阶方法**：对于黑盒 LLM 场景，仅对比了双层零阶方法，未与专门的单层零阶 prompt 攻击方法等进行横向比较。
- **未处理三层以上的更高层嵌套问题**。
- 外部罚函数法虽降低了复杂度，但可能引入超参数调优负担，且文中未充分讨论罚参数的选择指导。

（完）
