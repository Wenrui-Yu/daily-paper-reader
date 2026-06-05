---
title: "DictPFL: Efficient and Private Federated Learning on Encrypted Gradients"
title_zh: DictPFL：加密梯度上的高效隐私联邦学习
authors: "Jiaqi Xue, Mayank Kumar, Yuzhang Shang, Shangqian Gao, Mengxin Zheng, Xiaoqian Jiang, Qian Lou"
date: 2025-01-24
pdf: "https://openreview.net/pdf?id=lSTJ628SXl"
tags: ["query:daily"]
score: 9.0
evidence: 加密联邦学习中的共享梯度以保护隐私同时保持效率
tldr: 联邦学习中，梯度共享存在隐私风险，全同态加密开销大。本文提出DictPFL框架，采用基于字典的选择性加密策略，仅加密部分敏感梯度，在保证隐私的同时大幅降低计算和通信开销。实验表明DictPFL在多个模型上接近非加密基线性能。该方法为实现高效且隐私的联邦学习提供了新思路。
source: ICML-2025-Rejected-Public
selection_source: conference_retrieval
figures_json: "[{\"url\": \"assets/figures/openreview/openreview-icml-2025-lstj628sxl/fig-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 1835, \"height\": 588, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-icml-2025-lstj628sxl/fig-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 864, \"height\": 260, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-icml-2025-lstj628sxl/fig-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 871, \"height\": 250, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-icml-2025-lstj628sxl/fig-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 826, \"height\": 295, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-icml-2025-lstj628sxl/fig-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 872, \"height\": 294, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-icml-2025-lstj628sxl/fig-006.webp\", \"caption\": \"\", \"page\": 0, \"index\": 6, \"width\": 1761, \"height\": 383, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-icml-2025-lstj628sxl/fig-007.webp\", \"caption\": \"\", \"page\": 0, \"index\": 7, \"width\": 1601, \"height\": 460, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-icml-2025-lstj628sxl/fig-008.webp\", \"caption\": \"\", \"page\": 0, \"index\": 8, \"width\": 863, \"height\": 348, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-icml-2025-lstj628sxl/fig-009.webp\", \"caption\": \"\", \"page\": 0, \"index\": 9, \"width\": 868, \"height\": 455, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-icml-2025-lstj628sxl/fig-010.webp\", \"caption\": \"\", \"page\": 0, \"index\": 10, \"width\": 861, \"height\": 334, \"label\": \"Figure\"}]"
tables_json: "[{\"url\": \"assets/tables/openreview/openreview-icml-2025-lstj628sxl/table-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 865, \"height\": 239, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-icml-2025-lstj628sxl/table-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 844, \"height\": 222, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-icml-2025-lstj628sxl/table-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 861, \"height\": 236, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-icml-2025-lstj628sxl/table-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 816, \"height\": 239, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-icml-2025-lstj628sxl/table-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 929, \"height\": 189, \"label\": \"Table\"}, {\"url\": \"assets/tables/openreview/openreview-icml-2025-lstj628sxl/table-006.webp\", \"caption\": \"\", \"page\": 0, \"index\": 6, \"width\": 1139, \"height\": 369, \"label\": \"Table\"}]"
motivation: 全同态加密联邦学习计算和通信开销过高。
method: 设计基于字典的选择性梯度加密策略，识别并仅加密敏感梯度。
result: 在图像分类等任务上，DictPFL相比全加密方案显著提升效率，且隐私保护可证明。
conclusion: DictPFL平衡了联邦学习的隐私与效率，实用性强。
---

## Abstract
Federated learning (FL) enables institutions to collaboratively train machine learning models by aggregating local gradients without sharing sensitive data. However, sharing gradients still poses privacy risks, e.g., gradient inversion attacks. Homomorphic encryption (HE) is commonly used in FL to encrypt gradients at the data owner's side, enabling secure aggregation without decryption on the server. Existing HE-based FL methods are either fully encrypted or selectively encrypted: the former ensures privacy but incurs high overhead, while the latter improves efficiency by partially encrypting gradients, leaving shared unencrypted gradients vulnerable. To enable efficient and private FL, we propose DictPFL, a framework that encrypts shared gradients while keeping most gradients local without the need for sharing all, while preserving the performance of global gradient aggregation. DictPFL comprises two modules: Decompose-for-Partial-Encrypt (DePE) and Prune-for-Minimum-Encrypt (PrME). In DePE, we decompose pre-trained model weights into a dictionary and a lookup table. Only the gradients of the lookup table are encrypted and aggregated securely while the dictionary remains fixed and is not transmitted for aggregation. In PrME, we aim to further minimize the encrypted parameters with an encryption-aware pruning technique that ensures a consistent pruning mask across clients by leveraging the history of global gradients. Experimental results demonstrate that DictPFL significantly reduces communication overhead by 402 to 748 times and speeds training by 28 to 65 times compared to fully encrypted method. It also outperforms state-of-the-art selectively encrypted gradient by lowering overhead by 51 to 155 times and accelerating training by 4 to 19 times.

---

## 论文详细总结（自动生成）

## 1. 论文的核心问题与整体含义

- **核心问题**：联邦学习（FL）中共享本地模型梯度存在隐私泄漏风险（如梯度反转攻击）；使用同态加密（HE）保护梯度虽能保证隐私，但引入巨大的计算与通信开销。现有的选择性加密方法（如 FedML-HE）虽降低了开销，但其未加密的梯度依然暴露隐私。
- **研究动机**：在完全加密与部分加密之间寻找平衡点，既要保证所有共享梯度都被加密（避免隐私泄漏），又要大幅减少需要加密的参数数量，从而实现效率与隐私兼得的联邦学习框架。
- **整体含义**：提出 DictPFL 框架，将模型参数分解为静态字典与可训练查表，并通过加密感知剪枝进一步压缩加密梯度，最终在完全保护共享梯度隐私的前提下，将通信与计算开销降低至接近明文训练的水平。

## 2. 论文提出的方法论

DictPFL 包含两个核心模块：

### 2.1 Decompose-for-Partial-Encrypt (DePE)
- **核心思想**：利用预训练权重的低秩冗余，将权重矩阵 \(W\) 分解为全局一致的字典 \(D \in \mathbb{R}^{n \times r}\) 和客户本地训练的查表 \(T \in \mathbb{R}^{r \times m}\)。
- **构造方式**：对预训练权重 \(W_0\) 进行截断 SVD，取前 \(r\) 个奇异值/向量，得到 \(D = U_r \Sigma_r\) 和 \(T' = V_r^\top\)。实际训练时保持 \(D\) 不变，将 \(T\) 初始化为零，权重表示为 \(W = W_0 + D \cdot T\)。
- **隐私保护**：\(D\) 全局一致且无需传输；只有查表 \(T\) 的梯度需要加密、上传和聚合。由于 \(r\) 可以远小于原始维度，需加密的参数量显著减少（例如 \(r=4\)）。
- **公式**：
  \[
  W[:][i] = \sum_{k=0}^{r} D[:][k] \cdot T[k][i]
  \]
  其中 \(W[:][i]\) 表示第 \(i\) 列权重，由字典向量的线性组合构成。

### 2.2 Prune-for-Minimum-Encrypt (PrME)
- **核心思想**：训练后期大量参数梯度极小，继续加密传输产生冗余。因此在客户端对查表 \(T\) 的梯度进行加密前剪枝，但要求所有客户端剪枝位置一致以支持同态聚合的 SIMD 操作。
- **Temporal Inactivity Pruning (TIP)**：利用过去 \(\tau\) 轮的全局梯度历史进行统一决策，将连续 \(\tau\) 轮梯度幅度均处于最小的 \(s\%\) 的参数剪除。
  \[
  M_{i,t} = 0 \quad \text{if} \quad \sum_{k=1}^{\tau} \mathbb{1}(|\delta w_{i,t-k}| < \theta_{s,t-k}) = \tau
  \]
  其中 \(\delta w_{i,t-k}\) 为参数 \(w_i\) 在第 \(t-k\) 轮的全局梯度，\(\theta_{s,t-k}\) 为相应轮次的百分位阈值。
- **Holistic Reactivation Correction (HRC)**：为防止过度剪枝导致重要参数永久失活，为每个被剪枝参数分配动态重新激活概率 \(p_i\)，根据其累计全局梯度大小自适应调整：
  \[
  p_i[t+1] = \begin{cases}
  p_i[t] \times \beta & \text{if } |\delta w_{i,t}| < \theta_{s,t} \\
  \min(p_i[t]/\beta, 1) & \text{otherwise}
  \end{cases}
  \]
  重新激活时上传自上次被剪枝以来的累积梯度，保证参数能重新参与聚合。
- **一致性保证**：客户端基于相同的全局梯度历史生成剪枝掩码，并通过共享随机种子使重新激活概率同步，从而无需额外索引同步即可在服务器端正确聚合。

## 3. 实验设计

- **数据集**：
  - 图像分类：CIFAR-10、GTSRB、Diabetic Retinopathy
  - 文本分类：AG's News
  - 文本生成（指令微调）：MetaMathQA（评估用 GSM8K）
  - 数据划分提供同质（随机分配）和异质（Dirichlet 分布，\(\alpha=0.3,0.6,0.9\)）两种场景。
- **模型**：ViT（图像）、BERT（文本分类）、TinyLlama（文本生成）。
- **对比基线**：
  - **FedHE-Full**：训练完整模型并全加密所有梯度（全同态加密）。
  - **FedHE-Top2**：仅微调最后两层并全加密。
  - **FedML-HE (Select-and-Encrypt)**：根据预计算的敏感度分数仅加密 10% 最敏感梯度，其余明文传输。
- **评估指标**：通讯量（GB）、总训练时间（秒/分/小时）、模型准确率/精度，以及利用梯度反转攻击后的图像恢复分数（1−LPIPS）衡量隐私风险。
- **超参数默认值**：字典大小 \(r=4\)，剪枝比率 \(s\%=70\%\)，剪枝耐心 \(\tau=3\)，重新激活概率缩放因子 \(\beta=0.2\)。

## 4. 资源与算力

- **硬件环境**：所有实验在 **AMD Ryzen Threadripper PRO 3955WX 处理器（2.2 GHz）** 上运行，配备 **125 GB 内存**。文中未提及使用 GPU，HE 相关的加密、解密与聚合均在 CPU 上完成，这符合同态加密方案的实际部署特征（主要依赖 CPU 的大整数运算和 SIMD 指令）。
- **HE 实现**：基于 OpenFHE 库，采用支持自举的 CKKS 全同态加密方案，环维度 \(N=2^{16}\)，密文模数 1555 比特，乘法深度 \(L=12\)，安全级别 128 位。
- **说明**：该实验强调 HE 带来的开销，因此选用高频多核 CPU 而非 GPU，也反映出 DictPFL 降低密文数量对减少 CPU 计算开销的直接效果。未提供 GPU 型号印证了计算瓶颈在于 HE 操作而非模型训练本身。

## 5. 实验数量与充分性

- **主要实验组数**：
  - 3 个图像数据集上 ViT 模型的全面对比（图 7、图 9）
  - 5 种不同规模模型（LeNet 到 Llama2-7B）的通信开销对比（图 8(b)）
  - 训练时间分解分析（LAN/WAN 环境，图 9）
  - 消融实验：字典大小 \(r\in\{2,4,8,16\}\)、剪枝比率 0%/20%/70%/70%+HRC、剪枝耐心 \(\tau\in\{1,3,5,10\}\)、重新激活因子 \(\beta\in\{0.2,0.5,0.8\}\)
  - 不同客户端数量（3,5,10,20）
  - 不同数据异质性程度（Dirichlet \(\alpha\)=0.3,0.6,0.9,同质∞）
  - NLP 任务（BERT 和 TinyLlama）的对比实验（附录 B.2）
  - 隐私风险评估实验（梯度反转攻击恢复图像分数，图 8(a)）
- **充分性**：实验覆盖了图像和语言任务、不同规模模型、多种系统参数，消融研究详尽，对比基线包含全加密和选择性加密的代表方法，且公开了隐私攻击验证，整体设计客观、公平，能够支撑论文结论。

## 6. 论文的主要结论与发现

- DictPFL 相较于完全加密框架 FedHE-Full，**通讯量降低 402～748 倍**，**训练速度提升 28～65 倍**。
- 相较于最先进的选择性加密框架 FedML-HE，通讯量降低 51～155 倍，训练加速 4～19 倍，同时**完全避免了明文梯度传输导致的隐私泄漏**。
- 通过 DePE 将梯度压缩至查表后，即便字典很小（\(r=4\)）也可保持与全量微调相近的准确率（如在 GTSRB 上 95.27% vs. 58.9% 仅调最后两层）。
- PrME 中 TIP + HRC 的组合既能大幅压低通讯量（70% 剪枝率），又能将准确率恢复至接近轻量剪枝（20%）的水平。
- 方法在不同客户端数量、数据异质性下表现稳定，且在大型语言模型（TinyLlama）上训练时间减少高达 99.4%，显示出极强的压缩能力。

## 7. 优点

- **隐私计算与效率的融合**：首创“分解-加密-剪枝”三级压缩路径，大幅缩减密文数量，同时保证所有共享梯度均为加密状态，无隐私折衷。
- **加密友好的剪枝机制**：利用历史全局梯度统一剪枝掩码，避免了传统剪枝在 HE 下的索引对齐难题；HRC 动态重激活机制有效弥补了过度剪枝造成的精度损失。
- **广泛的适用性与可扩展性**：支持图像和文本多种模型，尤其在大模型上效果突出；实验覆盖不同网络带宽、异构数据等多种实际场景。
- **低秩分解的巧思**：借用预训练权重的 SVD 分解构建全局字典，既保留了关键知识，又显著压缩了需加密的可训练参数量，实现隐私与性能的平衡。

## 8. 不足与局限

- **依赖预训练模型与低秩假设**：DePE 的分解质量和压缩效果严重依赖预训练权重的低秩性质，若预训练模型不适用或任务与预训练数据差异过大，字典可能难以表达必要的参数更新，导致性能下降。
- **超参数敏感性**：字典大小 \(r\)、剪枝率 \(s\%\)、耐心系数 \(\tau\)、重激活因子 \(\beta\) 等均需手工调节，文中虽进行了消融分析，但未提供自动调整策略。
- **威胁模型有限**：仅考虑半诚实（honest-but-curious）服务器，未讨论恶意客户端或服务器、共谋攻击等更强的威胁模型。
- **实验环境单一**：所有 HE 实验均在 AMD CPU 上完成，未评估实际部署时客户端异构算力（如移动端、FPGA 加速器等）下的效果；也未测量单轮延迟和端侧加解密带来的额外负载。
- **剪枝收益依赖于训练收敛**：PrME 的剪枝在训练后期才有显著收益，前期通讯节省有限；且当模型本身参数更新剧烈时，剪枝可能过早移除重要参数。
- **未探讨对模型可解释性和公平性的影响**：梯度剪枝和低秩分解是否引入额外偏差未作讨论。

（完）
