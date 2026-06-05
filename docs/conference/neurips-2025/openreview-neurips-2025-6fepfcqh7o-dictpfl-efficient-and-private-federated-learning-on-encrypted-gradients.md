---
title: "DictPFL: Efficient and Private Federated Learning on Encrypted Gradients"
title_zh: 基于加密梯度的隐私保护与高效联邦学习
authors: "Jiaqi Xue, Mayank Kumar, Yuzhang Shang, Shangqian Gao, Rui Ning, Mengxin Zheng, Xiaoqian Jiang, Qian Lou"
date: 2025-09-18
pdf: "https://openreview.net/pdf?id=6FEpFCqH7o"
tags: ["query:daily"]
score: 9.0
evidence: 全梯度加密的高效隐私保护联邦学习
tldr: 联邦学习中梯度共享存在隐私泄露风险，全同态加密开销过大。DictPFL加密所有传输梯度而保留未传输参数本地更新，实现了全梯度保护且计算通信开销极低，兼顾了隐私与效率。
source: NeurIPS-2025-Accepted
selection_source: conference_retrieval
figures_json: "[{\"url\": \"assets/figures/openreview/openreview-neurips-2025-6fepfcqh7o/fig-001.webp\", \"caption\": \"\", \"page\": 8, \"index\": 1, \"width\": 717, \"height\": 717}, {\"url\": \"assets/figures/openreview/openreview-neurips-2025-6fepfcqh7o/fig-002.webp\", \"caption\": \"\", \"page\": 8, \"index\": 2, \"width\": 717, \"height\": 717}]"
motivation: 梯度共享存在隐私风险，全加密开销大，部分加密不安全。
method: DictPFL加密所有传输梯度，对未传输参数本地保持。
result: 实现全梯度保护，开销极小。
conclusion: 为联邦学习提供了实用的端到端加密方案。
---

## Abstract
Federated Learning (FL) enables collaborative model training across institutions without sharing raw data. However, gradient sharing still risks privacy leakage, such as gradient inversion attacks. Homomorphic Encryption (HE) can secure aggregation but often incurs prohibitive computational and communication overhead. Existing HE-based FL methods sit at two extremes: encrypting all gradients for full privacy at high cost, or partially encrypting gradients to save resources while exposing vulnerabilities. We present **DictPFL**, a practical framework that achieves full gradient protection with minimal overhead. DictPFL encrypts every transmitted gradient while keeping non-transmitted parameters local, preserving privacy without heavy computation. It introduces two key modules: **Decompose-for-Partial-Encrypt (DePE)**, which decomposes model weights into a static dictionary and an updatable lookup table—only the latter is encrypted and aggregated, while the static dictionary remains local and requires neither sharing nor encryption; and **Prune-for-Minimum-Encrypt (PrME)**, which applies encryption-aware pruning to minimize encrypted parameters via consistent, history-guided masks. Experiments show that DictPFL reduces communication cost by 402-748$\times$ and accelerates training by 28-65$\times$ compared to fully encrypted FL, while outperforming state-of-the-art selective encryption methods by 51-155$\times$ in overhead and 4-19$\times$ in speed. Remarkably, DictPFL’s runtime is within 2$\times$ of plaintext FL, demonstrating, for the first time, that HE-based private federated learning is practical for real-world deployment. The code is publicly available at https://github.com/UCF-ML-Research/DictPFL.

---

## 论文详细总结（自动生成）

好的，作为资深学术论文分析助手，我将以 Markdown 格式，用中文对论文 `DictPFL: Efficient and Private Federated Learning on Encrypted Gradients` 进行结构化、深入且客观的总结。

### 1. 论文的核心问题与整体含义

*   **核心问题**：联邦学习虽能保护原始数据，但共享的模型梯度仍存在隐私泄露风险（如梯度反转攻击）。使用全同态加密可以完全保护梯度，但会带来巨大的计算和通信开销，使其难以实际部署。现有的折衷方案（如选择性加密部分梯度）减少了开销，却以牺牲隐私为代价。
*   **研究动机**：打破当前全加密无效率、部分加密无隐私的僵局。
*   **整体含义**：论文旨在证明，通过巧妙的模型结构设计和加密感知的剪枝策略，**完全基于同态加密的隐私保护联邦学习可以在实现极低开销的同时确保完全隐私**，使其在实际应用中变得切实可行，为联邦学习的隐私保护提供高效且实用的方案。

### 2. 论文提出的方法论

论文提出的 **DictPFL** 框架，核心思想是通过**最小化需要加密和传输的参数量**来实现效率与隐私的兼顾。它主要由两个关键模块组成：

*   **模块 1：Decompose-for-Partial-Encrypt (DePE)**
    *   **核心思想**：将模型权重矩阵 $W \in \mathbb{R}^{n \times m}$ 分解为一个**静态的全局字典** $D \in \mathbb{R}^{n \times r}$ 和一个**可训练的查询表** $T \in \mathbb{R}^{r \times m}$，其中 $r$ 远小于 $n$ 和 $m$。
    *   **关键细节**：
        *   通过截断奇异值分解（SVD）初始化 $D$ 和 $T'$，然后冻结 $D$，并用零初始化 $T$，使权重 $W = W_0 + D \cdot T$（$W_0$ 为原始权重）。
        *   **字典 $D$ 跨客户端一致，保存在本地，永不传输或加密**。
        *   仅对规模远小于原始权重的**查询表 $T$ 的梯度进行加密和聚合**。这确保了所有传输的参数都是加密的，同时极大减少了加密对象。
*   **模块 2：Prune-for-Minimum-Encrypt (PrME)**
    *   **核心思想**：在DePE基础上，进一步识别并剪除查询表 $T$ 中那些梯度持续很小的参数，不再对他们的加密梯度进行上传和聚合。
    *   **关键细节**：
        *   **Temporal Inactivity Pruning (TIP)**：为解决客户端独立剪枝导致梯度无法对齐的问题，客户端基于**共享的历史全局梯度**（最近 $\tau$ 轮）做出一致的剪枝决策。若某参数梯度在连续 $\tau$ 轮内都属于最小的 $s\%$，则剪除它。
        *   **Holistic Reactivation Correction (HRC)**：为避免参数被永久性错误剪除，引入动态重激活概率 $p_i$。剪除的参数有概率被重新激活，上传其累积的本地梯度参与聚合。该概率根据重激活后的全局梯度大小动态调整，梯度大则提高概率，反之则降低，以此修正剪枝错误。

### 3. 实验设计

*   **数据集**：
    *   图像识别：CIFAR-10， 德国交通标志识别基准 (GTSRB)， 糖尿病性视网膜病变 (Diabetic Retinopathy)。
    *   文本任务：AG's News（句子分类）， MetaMathQA（文本生成）。
    *   数据划分：同时考虑了独立同分布（均匀划分）和非独立同分布（基于Dirichlet分布的异质性）场景。
*   **模型**：覆盖了主流的Transformer模型。
    *   视觉：ViT。
    *   语言：BERT， TinyLlama。
*   **对比基准 (Baselines)**：
    *   **FedHE-Full**：加密所有梯度的完全同态加密联邦学习。
    *   **FedHE-Top2**：仅微调并加密最后两层的联邦学习。
    *   **FedML-HE (FedHE-ML)**：最先进的选择性加密方法，仅加密敏感度最高的一部分梯度（默认为10%），其余以明文传输（存在隐私泄露风险）。

### 4. 资源与算力

*   论文明确说明了实验硬件环境：**AMD Ryzen Threadripper PRO 3955WX 处理器 (2.2 GHz)，125 GB 内存**。
*   **未提到使用 GPU**。论文主要关注同态加密的计算开销，通常在CPU上进行，因此实验是在强大的CPU环境中完成的。
*   具体训练时长在论文中有大量图表对比，例如在GTSRB上训练ViT，DictPFL的耗时为分钟级，远低于其他基准的数十分钟至数小时。

### 5. 实验数量与充分性

*   **实验数量**：实验较为丰富，涵盖了：
    1.  **主要性能对比**：在3个图像数据集上，比较了通信开销、训练时间与模型精度（图6、图7）。
    2.  **效率分解分析**：在LAN和WAN下，对各方法的训练、通信、加解密、聚合时间进行了详细分解（图8）。
    3.  **可扩展性**：测试了从LeNet到Llama2-7B等不同规模模型的通信开销（图7）。
    4.  **隐私安全性**：对比了DictPFL与FedML-HE在梯度反转攻击下的图像相似度得分（图7）。
    5.  **消融实验**：系统研究了DePE的字典大小 $r$，PrME的剪枝比例 $s\%$、剪枝耐心值 $\tau$、重激活概率系数 $\beta$ 对性能的影响。
    6.  **鲁棒性与泛化性实验**：验证了在不同客户端数量、数据异质性程度、以及在文本分类和文本生成任务上的效果。
*   **充分性与公平性**：**实验设计十分充分且客观**。它不仅与主流的HE-FL方法在多个维度和场景下进行了公平对比，还细致分析了各部分的效率瓶颈。对FedML-HE的隐私分析揭示了其“效率换隐私”的本质缺陷，使与DictPFL的对比更加深刻。

### 6. 论文的主要结论与发现

*   DictPFL首次成功地在**确保完全隐私**的前提下，将基于HE的联邦学习开销降低到了可实用的水平。
*   与全加密基准相比，DictPFL将通信成本降低了 **402-748倍**，训练速度提升了 **28-65倍**。
*   与性能最好的选择加密方法相比，它在**不泄露任何隐私**的同时，仍将通信开销降低了 **51-155倍**，速度提升了 **4-19倍**。
*   DictPFL的训练总耗时仅为明文联邦学习的**2倍以内**，这标志着基于HE的隐私保护联邦学习具备了真正落地的潜力。

### 7. 优点

*   **概念上的突破**：方法巧妙地结合了权重分解和加密感知剪枝，从根本上解决问题，而非对加密方案的修补，实现了**隐私（全加密）与效率（低沟通/计算）的兼得**。
*   **设计精巧**：
    *   **DePE模块**利用SVD一次性分解，将加密负担有效转嫁到更小的查找表上，构思巧妙。
    *   **PrME模块**的TIP和HRC机制漂亮地解决了HE场景下梯度协同剪枝和对齐的独特挑战，并避免了不可逆剪枝带来的精度损失。
*   **实验论证极具说服力**：实验覆盖了视觉和语言任务，多种模型规模，并且特别通过**攻击实验直接量化了选择加密方案的隐私风险**，直观地凸显了自身方案的安全性优势。
*   **强实用性**：训练耗时接近明文FL这一结论，对未来实际应用具有很强的指导意义和吸引力。

### 8. 不足与局限

*   **客户端资源假设**：实验在拥有125GB内存的高性能CPU上完成，这与潜在资源受限的跨设备联邦学习场景（如手机、IoT设备）仍有差距。尽管通信开销降低了，客户端的本地加解密计算负荷并未在资源受限设备上测试。
*   **模型架构通用性**：论文主要验证了Transformer类模型，对其他主流模型架构（如CNN、RNN，文中仅提及但未做详测）的兼容性和效果有待进一步验证。
*   **字典的动态性局限**：静态且全局一致的字典在面对**高度异构**的客户端数据分布时，其表示能力可能成为瓶颈。论文在讨论中也指出了这一点，并认为动态字典是未来方向。
*   **攻击模型假设**：威胁模型设定为半诚实服务器，这虽然符合大多数HE-FL研究的设定，但在恶意服务器参与的更强威胁模型下的安全性未做讨论。

（完）
