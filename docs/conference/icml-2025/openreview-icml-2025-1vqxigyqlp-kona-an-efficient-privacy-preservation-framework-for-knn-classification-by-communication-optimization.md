---
title: "Kona: An Efficient Privacy-Preservation Framework for KNN Classification by Communication Optimization"
title_zh: Kona：基于通信优化的高效隐私保护KNN分类框架
authors: "Guopeng Lin, Ruisheng Zhou, Shuyu Chen, Weili Han, Jin Tan, Wenjing Fang, Lei Wang, Tao Wei"
date: 2025-05-01
pdf: "https://openreview.net/pdf?id=1VqxIgyQlp"
tags: ["query:daily"]
score: 9.0
evidence: 带有通信优化的隐私保护KNN分类框架
tldr: 针对分布式KNN分类的隐私保护问题，现有方案在线阶段通信低效。本文提出Kona框架，通过优化安全欧氏平方距离计算和减少交互轮次，显著降低通信开销。实验表明，Kona在保持精度和隐私的同时，实现了更高的在线效率。该方法为隐私保护KNN提供了实用的通信优化方案。
source: ICML-2025-Accepted
selection_source: conference_retrieval
figures_json: "[{\"url\": \"assets/figures/openreview/openreview-icml-2025-1vqxigyqlp/fig-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 840, \"height\": 531, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-icml-2025-1vqxigyqlp/fig-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 1599, \"height\": 750, \"label\": \"Figure\"}]"
tables_json: "[{\"url\": \"assets/tables/openreview/openreview-icml-2025-1vqxigyqlp/table-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 845, \"height\": 315, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-icml-2025-1vqxigyqlp/table-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 717, \"height\": 362, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-icml-2025-1vqxigyqlp/table-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 573, \"height\": 359, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-icml-2025-1vqxigyqlp/table-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 1745, \"height\": 498, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-icml-2025-1vqxigyqlp/table-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 1758, \"height\": 488, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-icml-2025-1vqxigyqlp/table-006.webp\", \"caption\": \"\", \"page\": 0, \"index\": 6, \"width\": 749, \"height\": 580, \"label\": \"Table\"}]"
motivation: 现有隐私保护KNN分类通信开销大，在线效率低。
method: 提出Kona框架，优化安全欧氏平方距离计算和交互轮次以降低通信量。
result: 在标准数据集上，Kona相比现有方案显著减少通信大小和轮次，提升效率。
conclusion: Kona实现了高效且隐私保护的KNN分类，适用于分布式数据场景。
---

## Abstract
K-nearest neighbors (KNN) classification plays a significant role in various applications due to its interpretability. The accuracy of KNN classification relies heavily on large amounts of high-quality data, which are often distributed among different parties and contain sensitive information. Dozens of privacy-preserving frameworks have been proposed for performing KNN classification with data from different parties while preserving data privacy. However, existing privacy-preserving frameworks for KNN classification demonstrate communication inefficiency in the online phase due to two main issues: (1) They suffer from huge communication size for secure Euclidean square distance computations. (2) They require numerous communication rounds to select the $k$ nearest neighbors.  In this paper, we present $\texttt{Kona}$, an efficient privacy-preserving framework for KNN classification. We resolve the above communication issues by (1) designing novel Euclidean triples, which eliminate the online communication for secure Euclidean square distance computations,  (2) proposing a divide-and-conquer bubble protocol, which significantly reduces communication rounds for selecting the $k$ nearest neighbors. Experimental results on eight real-world datasets demonstrate that $\texttt{Kona}$ significantly outperforms the state-of-the-art framework by  $1.1\times \sim 3121.2\times$ in communication size, $16.7\times \sim 5783.2\times$ in communication rounds, and $1.1\times \sim 232.6\times$ in runtime.

---

## 论文详细总结（自动生成）

### 1. 论文的核心问题与整体含义
在分布式场景下进行KNN分类时，多个参与方（如医院）的数据通常包含隐私信息，无法直接聚合。现有隐私保护KNN框架虽然能保证数据安全，但**在线阶段通信效率低下**，体现在：
- **安全欧氏平方距离计算**：现有方法需要为每个距离计算传输加密元素或秘密份额，通信量大。
- **选择k个最近邻**：现有顺序冒泡协议需要O(kn)轮交互，在高延迟网络下性能极差。
这些问题严重阻碍了隐私保护KNN在实际大规模场景中的部署。本文提出Kona框架，旨在通过**通信优化**解决上述两大瓶颈，在保持数据隐私和分类精度的同时，大幅提升在线效率。

### 2. 论文提出的方法论
Kona的核心优化分为两部分：

#### 2.1 欧几里得三元组（Euclidean Triples）
- **核心思想**：利用“与输入无关、但与函数相关”的预处理技术，设计三元组 `(⃗u, ⃗v, w)`，其中 `w = (⃗u − ⃗v)²`。结合掩码秘密共享（MSS），将距离计算 `d = (⃗x − ⃗a)²` 转化为仅依赖公开掩码 `⃗U, ⃗V` 和三元组的本地运算。
- **效果**：**在线通信完全消除**。计算方 `Pa` 和 `Pb` 可独立计算各自的份额 `JdK_a` 和 `JdK_b`，不再需要交互。

#### 2.2 分治冒泡协议（Divide-and-Conquer Bubble Protocol）
- **核心思想**：将列表两两分组，并行执行安全比较与交换（CompareSwap），每次迭代将候选最小元素“冒泡”到前半部分，列表长度减半。
- **效果**：选择1个最近邻的交互轮数从 `O(l)` 降至 `O(log l)`。重复k次后，总轮数为 `O(k log n)`，而通信量仍为 `O(kn)`（与顺序方法相同）。
- **注意**：该协议不依赖距离度量的具体形式，可适配任意度量。

整体工作流程：数据拥有者离线将数据用MSS共享给计算方；用户同样共享查询样本；计算方先用三元组零通信算出距离，再用分治冒泡协议选出k近邻，最后多数投票返回标签。

### 3. 实验设计
- **数据集**：8个UCI真实数据集，覆盖不同规模与维度：
  Toxicity (120样本, 1203属性), Iris (150, 4), Arcene (200, 10000), PEMS-SF (440, 137710), RNA-seq (800, 20532), Spambase (4601, 57), Mnist (70000, 784), Dota2 Games (102944, 115)。
- **精度基准**：scikit-learn的明文KNN实现。
- **效率基准**：SecKNN（基于函数秘密共享的最新安全KNN框架），作者复现为C++实现。
- **实验环境**：单服务器（32核CPU, 128GB RAM），用`tc`工具模拟WAN（40Mbps, 40ms RTT）和LAN（1024Mbps, 亚毫秒RTT）。每个计算方一个单线程进程。
- **超参数**：默认k=5；为研究k的影响，选取Arcene数据集测试k=1,5,10,...,100。

### 4. 资源与算力
- 文中明确说明使用**CPU-only**环境：Linux服务器，配备32核2.4 GHz Intel Xeon CPU和128GB内存。未使用GPU。
- 每个计算方用**单线程**进程模拟，最多使用两个核心。
- 无GPU相关训练或推理过程，所有计算均为多方安全计算（MPC）协议运行，不涉及深度学习训练。因此**无需GPU算力**。

### 5. 实验数量与充分性
- **主实验**：8个数据集 × (Kona vs. SecKNN) × (WAN, LAN)，总共16组核心对比，评估通信量、通信轮数、运行时间。
- **k变化实验**：在Arcene上测试k=1,5,10,20,40,60,80,100，展示性能变化趋势。
- **消融实验**：分离两个优化，构建SecKNN-Triples（仅用三元组）和SecKNN-DQBubble（仅用分治冒泡），与原始SecKNN对比通信量/轮数/运行时间，分别验证各自贡献。
- **充分性评价**：实验覆盖了从极小到中等规模（超过10万样本）、从低维到超高维的数据，兼顾了不同网络条件以及参数影响，对比基线为复现的最先进方法，并进行了详细的消融分析。整体实验设计**充分、公平且系统性强**。

### 6. 论文的主要结论与发现
- **精度无损**：Kona在所有数据集上与scikit-learn明文KNN的准确率完全一致（如表3所示）。
- **通信开销显著降低**：与SecKNN相比，通信量减少1.1×~3121.2×（尤其高维数据收益极大），通信轮数减少16.7×~5783.2×（样本量越大收益越明显）。
- **运行时间大幅缩短**：在WAN下加速14.36×~232.60×；在LAN下也取得了1.15×~11.36×的加速。
- **消融实验证实**：三元组主要降低通信量（1.10×~3064.94×），分治冒泡主要降低轮数（16.16×~5688.51×），两者协同使得Kona在各类场景均高效。
- 结论：Kona是一个实用且可扩展的隐私保护KNN分类方案。

### 7. 优点
- **精巧的通信优化**：欧几里得三元组将在线距离计算通信降为零，分治冒泡协议以对数级轮数完成k近邻选择，理论分析与实验结果高度吻合。
- **安全性有保障**：基于半诚实模型和UC组合安全性证明，不泄露中间信息（除最终分类结果外）。
- **架构灵活**：支持任意数量数据拥有者水平分布，可扩展至垂直分布、多计算方和其他距离度量。
- **工程实现完整**：开源代码，实验涵盖丰富的数据集与消融对比，复现性强。
- **精度保持**：优化完全等价转换，不改变原始KNN的计算语义。

### 8. 不足与局限
- **安全模型假设**：仅考虑半诚实且不共谋的两方/多方场景，未涉及恶意敌手、共谋或隐私泄露边界更严格的需求。
- **数据集规模**：虽然最大数据集超过10万样本，但仍未触及工业界亿级样本或更高维度的极端规模，可扩展性仍需在大规模分布式集群中验证。
- **预处理成本**：欧几里得三元组生成需要离线通信（同态加密），虽然开销与SecKNN的随机对生成相当，但在数据集频繁变动时可能引入额外负担。
- **度量适配**：对于非欧氏距离（如马氏距离）或更复杂的相似度，三元组需要重新设计，文中仅给出思路而未实现。
- **垂直分布的扩展**：需先执行私有集合求交，增加了前置步骤和成本。
- **实验环境**：仅在单机模拟多进程，未在真实多机分布式环境中测试，可能低估网络异构、节点故障等因素的影响。
- **k值鲁棒性**：随着k增大，Kona相对SecKNN的倍数收益逐渐下降（如k=100时加速比降至16.02×），表明在k极大时，优化效果会减弱。

（完）
