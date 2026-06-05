---
title: Distributed Differentially Private Data Analytics via Secure Sketching
title_zh: 分布式差分隐私数据分析的安全草图方法
authors: "Jakob Burkhardt, Hannah Keller, Claudio Orlandi, Chris Schwiegelshohn"
date: 2025-05-01
pdf: "https://openreview.net/pdf?id=2Snksn3U47"
tags: ["query:daily"]
score: 9.0
evidence: 引入一种基于安全草图的分布式差分隐私数据分析模型
tldr: 该论文针对分布式场景中中心模型和本地模型在表达性与安全成本之间的权衡问题，提出了一种线性变换模型。该方法允许客户端通过安全多方计算将公开矩阵应用于输入，通过多个服务器分布计算，在保护隐私的同时实现高效数据分析。结果显示该模型为分布式隐私分析提供了一种实用且安全的中间方案，对隐私保护机器学习具有重要贡献。
source: ICML-2025-Accepted
selection_source: conference_retrieval
figures_json: "[{\"url\": \"assets/figures/openreview/openreview-icml-2025-2snksn3u47/fig-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 841, \"height\": 467, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-icml-2025-2snksn3u47/fig-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 528, \"height\": 499, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-icml-2025-2snksn3u47/fig-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 1528, \"height\": 408, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-icml-2025-2snksn3u47/fig-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 1722, \"height\": 1525, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-icml-2025-2snksn3u47/fig-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 1597, \"height\": 1528, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-icml-2025-2snksn3u47/fig-006.webp\", \"caption\": \"\", \"page\": 0, \"index\": 6, \"width\": 1713, \"height\": 1563, \"label\": \"Figure\"}]"
tables_json: "[{\"url\": \"assets/tables/openreview/openreview-icml-2025-2snksn3u47/table-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 1690, \"height\": 446, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-icml-2025-2snksn3u47/table-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 1752, \"height\": 243, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-icml-2025-2snksn3u47/table-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 1658, \"height\": 281, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-icml-2025-2snksn3u47/table-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 653, \"height\": 285, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-icml-2025-2snksn3u47/table-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 655, \"height\": 284, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-icml-2025-2snksn3u47/table-006.webp\", \"caption\": \"\", \"page\": 0, \"index\": 6, \"width\": 581, \"height\": 327, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-icml-2025-2snksn3u47/table-007.webp\", \"caption\": \"\", \"page\": 0, \"index\": 7, \"width\": 782, \"height\": 242, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-icml-2025-2snksn3u47/table-008.webp\", \"caption\": \"\", \"page\": 0, \"index\": 8, \"width\": 900, \"height\": 243, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-icml-2025-2snksn3u47/table-009.webp\", \"caption\": \"\", \"page\": 0, \"index\": 9, \"width\": 856, \"height\": 238, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-icml-2025-2snksn3u47/table-010.webp\", \"caption\": \"\", \"page\": 0, \"index\": 10, \"width\": 1790, \"height\": 241, \"label\": \"Table\"}]"
motivation: 解决分布式数据分析中中心模型安全性低、本地模型表达力弱的问题。
method: 提出线性变换模型，结合安全多方计算实现分布式差分隐私数据分析。
result: 实现了一种介于中心模型与本地模型之间的高效安全计算框架。
conclusion: 该模型为分布式差分隐私提供了更平衡的解决方案。
---

## Abstract
We introduce the *linear-transformation model*, a distributed model of differentially private data analysis. Clients have access to a 
trusted platform capable of applying a public matrix to their inputs. Such computations can be securely distributed across multiple servers using simple and efficient secure multiparty computation techniques. The linear-transformation model serves as an intermediate model between the highly expressive *central model* and the minimal *local model*. In the central model, clients have access to a trusted platform capable of applying any function to their inputs. However, this expressiveness comes at a cost, as it is often expensive to distribute such computations, leading to the central model typically being implemented by a single trusted server. In contrast, the local model assumes no trusted platform, which forces clients to add significant noise to their data. The linear-transformation model avoids the single point of failure for privacy present in the central model, while also mitigating the high noise required in the local model. We demonstrate that linear transformations are very useful for differential privacy, allowing for the computation of linear sketches of input data. These sketches largely preserve utility for tasks such as private low-rank approximation and private ridge regression, while introducing only minimal error, critically independent of the number of clients.

---

## 论文详细总结（自动生成）

## 1. 论文的核心问题与整体含义

- **核心问题**：在分布式数据分析中，能否设计一种介于“中心化差分隐私（central DP，高效用但依赖单一可信服务器）”和“本地化差分隐私（local DP，无需信任但噪声大、效用低）”之间的中间模型，既能避免单点信任风险，又能通过特定受限的可信计算获得接近中心模型的效用？
- **整体含义**：论文提出**线性变换模型（linear-transformation model, LTM）** 作为答案。该模型假设存在一个仅能执行公开线性变换（如矩阵乘法）的“可信平台”，该平台可通过简单的安全多方计算（MPC）分布到多个服务器上，从而在隐私、效用和计算效率之间取得更好的折衷。论文将该模型应用于低秩近似和岭回归等数值线性代数问题，并证明仅需一轮客户端到服务器的通信，即可在引入极小误差的条件下实现接近中心模型的差分隐私效用。

## 2. 方法论

### 2.1 核心思想
- **线性变换模型（LTM）** 包含三个算法：
  - `R`：客户端端的随机化编码器，在本地对数据进行加噪。
  - `T`：可信的线性变换功能，对全体客户端消息施加一个公开矩阵（如 Johnson‑Lindenstrauss 变换或 OSNAP 素描矩阵）。
  - `A`：分析算法，对变换结果进行下游分析（如低秩近似、回归）。
- 关键优势：线性变换可以利用 **线性秘密共享（LSS）** 无交互、高效地分布到多个服务器上，无需公钥密码操作，且支持信息论安全（抗量子攻击）；同时，利用噪声分布的**无限可分性（infinite divisibility）**，可以将中心模型所需的总噪声“分摊”到每个客户端本地添加的微小噪声中，使得最终聚合后的总噪声仅与隐私参数、数据维度等相关，而与客户端数量无关。

### 2.2 关键技术细节
- **素描矩阵**：采用具有子空间保持性质的稀疏 OSNAP 矩阵（Definition 2.1）或稠密 Rademacher 矩阵，分解为多个单非零元矩阵之和进行分布式计算。
- **随机化器设计**：
  - 高斯机制：客户端本地添加独立高斯噪声，方差设计使得聚合后整体噪声满足 \((\epsilon, \delta)\)-DP（式4）。
  - 拉普拉斯/伽马机制：利用 Gamma 分布的无限可分性构造纯 \(\epsilon\)-DP 机制（式5）。
- **隐私分析**（Theorem 3.4, 3.5）：通过 Chernoff 界保证每条行中足够多的诚实客户端贡献噪声，进而利用顺序组合和无限可分性，将差分隐私保障从单个条目扩展到整个线性变换输出。
- **效用分析**：
  - **低秩近似**（Theorem 4.3, 4.4）：基于 OSNAP 的谱界（Lemma 4.1, 4.2），得到乘法误差 \(1+\alpha\) 和与维度相关的加性误差，且加性误差与客户端数 \(n\) 无关。
  - **岭回归**（Theorem 4.5）：在正则化参数 \(\lambda\) 相对较大时，可获得乘法误差接近 \(1\)、加性误差为多项式量级的界。

## 3. 实验设计

### 3.1 数据集
- **合成数据**：人为生成具有明确谱间断（前 \(k\) 个奇异值远大于其余）的矩阵，用来突出不同隐私机制的差异。
- **真实数据集**（来自 UCI 机器学习库）：
  - Power（电力消耗，\(n=2,049,280,\ d=6\)）
  - Elevation（高程，\(n=434,874,\ d=2\)）
  - Ethylene（气体传感器，\(n=4,178,504,\ d=18\)）
  - Songs（歌曲音频特征，\(n=515,345,\ d=89\)）

### 3.2 基准与对比方法
- **对比模型**：
  - 中心化差分隐私基准（低秩近似用 MOD‑SULQ，回归用 SSP）。
  - 本地差分隐私基准（将 LTM 的噪声方差的依赖阶数设为 \(p=0\)，即噪声不随 \(n\) 减少）。
  - LTM 机制内部：放大噪声的方差相对于 \(n^{-p}\) 可实现从本地（\(p=0\)）到 LTM（\(p=1\)）的平滑插值；另外对比了高斯/拉普拉斯两种噪声机制。
- 评估指标：
  - 低秩近似：超额风险 \(\psi = \frac{1}{n}(\|A-AX'X'^T\|_F^2 - \|A-AX_{OPT}X_{OPT}^T\|_F^2)\)。
  - 回归：近似因子 \(\phi = \frac{\|Ax'-b\|_2^2+\lambda\|x'\|_2^2}{\|Ax_{OPT}-b\|_2^2+\lambda\|x_{OPT}\|_2^2}\)。

## 4. 资源与算力

- 论文中**未明确提到 GPU 使用**，所有机器学习/数据分析计算均为基于 CPU 的 Python 实现（使用 numpy）。
- **运行时间实验**使用了 MP‑SPDZ 框架在 AWS **t3.large 实例**上测量线性变换的分布式计算开销，评估了不同客户端数量（10 万到 100 万）和不同稀疏度 \(s\)、服务器数量（2 或 3）下的计算耗时和通信量，每个参数配置重复 10 次取平均。
- 因此，总体算力需求很低，主要由 CPU 服务器和简单矩阵运算构成，**未披露 GPU 型号与训练时长**。

## 5. 实验数量与充分性

- **实验组数较多且设计合理**：
  - 隐私参数 \(\epsilon \in \{0.01,0.03,0.05,0.1,0.5\}\)（不同实验场景覆盖）。
  - \(p \in \{0,0.5,0.6,0.7,0.8,0.9,1\}\) 覆盖本地到 LTM 的连续谱。
  - 合成数据集：17 种样本量（指数增长），多种 \(k,d,\lambda,\mu^2\) 组合。
  - 4 个真实数据集。
  - 每种配置运行 20~30 次并报告均值和标准差。
  - 另有专门的运行时间实验测试 MPC 计算开销随 \(n,s\) 的变化。
- **充分性与客观性**：实验覆盖的隐私范围、数据集类型和度量维度较广，能够系统展示 LTM 在效用和可扩展性方面的优势。对比基准包括经典的中心化 DP 算法和本地 DP 变体，对比相对公平。

## 6. 主要结论与发现

- LTM 在误差上**严格介于中心模型和本地模型之间**，且当客户端数 \(n\) 增大时，LTM 的误差趋向于中心模型水平（如合成数据所示）。
- 对真实数据集，**Gaussian 机制的 LTM 误差远小于本地模型**，且通常非常接近中心模型 MOD‑SULQ/SSP；拉普拉斯机制的 LTM 也优于本地模型，但为纯 \(\epsilon\)-DP 付出了更高的误差代价。
- 安全分布式实现（MPC）**额外计算开销极低**：对于百万级客户端，单个服务器仅需约 1.6 秒，且服务器之间无需通信，总通信量与矩阵稀疏度成线性关系。
- 理论分析表明，所提 LTM 机制对低秩近似和岭回归均可实现**独立于客户端数量 \(n\) 的加性误差**，并给出了具体的维度和隐私参数依赖关系。

## 7. 优点

- **模型新颖且实用**：提出了一个介于中心与本地之间的明确模型，并展示了其通过高度并行的 MPC 实现的实际可行性。
- **理论与实验结合紧密**：不仅给出了严谨的隐私和效用界，还通过大量实验验证了理论预测的渐近行为。
- **安全性增强**：明确定义了抵抗“半诚实+部分客户端/服务器腐化”的差分隐私安全模型，避免了一般洗牌模型中由于定义不严谨可能出现的弱隐私构造。
- **高效分布式实现**：利用线性秘密共享实现无交互、极低延迟的安全聚合，比基于公钥加密的洗牌/安全聚合方案在计算和通信上更具优势。
- **适应性强**：同一框架可同时支持 \((\epsilon,\delta)\)-DP（高斯机制）和纯 \(\epsilon\)-DP（拉普拉斯/伽马机制），且可插值于本地与中心之间。

## 8. 不足与局限

- **适用范围限制**：仅适用线性变换所能支持的运算和分析任务（如线性素描），对于非线性机器学习模型或复杂查询的扩展性未作讨论。
- **假设诚实但好奇的服务器多数派**：虽然容忍部分客户端腐化，但安全模型要求所有参与方半诚实执行协议；未讨论恶意敌手或主动攻击。
- **对输入数据范围 \(\eta\) 有先验界线**：噪声方差依赖于数据范围的先验上界，实际中可能需要人工截断或估计，可能影响效用与隐私。
- **回归结果与正则化强度强耦合**：岭回归的误差界仅在 \(\lambda\) 相对于维度较大时才获得优良的乘法/加法误差，限制了应用场景。
- **实验仅在合成数据和少量 UCI 数据集上进行**，未包含大规模高维图像或 NLP 数据，也未与其他可能的洗牌模型方案在相同任务下进行横向实验对比。
- **没有进行完整的超参数消融**（如素描矩阵目标维度 \(m\) 的影响）的详细实验报告，尽管理论上有参数依赖分析。

（完）
