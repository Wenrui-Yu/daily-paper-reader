---
title: Sketched Gaussian Mechanism for Private Federated Learning
title_zh: 用于隐私联邦学习的草图高斯机制
authors: "Qiaobo Li, Zhijie Chen, Arindam Banerjee"
date: 2025-09-18
pdf: "https://openreview.net/pdf?id=AUs0rScwK0"
tags: ["query:daily"]
score: 9.0
evidence: 提出草图高斯机制，结合草图与高斯噪声用于联邦学习隐私保护，直接解决私有分布式机器学习
tldr: 针对联邦学习中通信效率与隐私保护的两难，提出草图高斯机制（SGM），将梯度压缩与高斯噪声直接结合，统一分析隐私，优化通信与隐私的权衡，在保持隐私的前提下提升效率。
source: NeurIPS-2025-Accepted
selection_source: conference_retrieval
motivation: 现有工作分别分析草图和GM的隐私，未能联合优化，导致效率与隐私权衡不佳。
method: 提出SGM，将草图和GM集成，统一隐私分析，通过草图维度与噪声协同调整。
result: 在相同隐私预算下，SGM比独立应用草图或GM降低通信成本或提高精度。
conclusion: SGM为隐私联邦学习提供了通信高效的隐私保护方案。
---

## Abstract
Communication cost and privacy are two major considerations in federated learning (FL). For communication cost, gradient compression by sketching the clients’ transmitted model updates is often used for reducing per‐round communication. For privacy, the Gaussian mechanism (GM), which consists of clipping updates and adding Gaussian noise, is commonly used to guarantee client‐level differential privacy. Existing literature on private FL analyzes privacy of sketching and GM in an isolated manner, illustrating that sketching provides privacy determined by the sketching dimension and that GM has to supply any additional desired privacy. 

In this paper, we introduce the Sketched Gaussian Mechanism (SGM), which directly combines sketching and the Gaussian mechanism for privacy. Using Rényi-DP tools, we present a joint analysis of SGM's overall privacy guarantee, which is significantly more flexible and sharper compared to isolated analysis of sketching and GM privacy. In particular, we prove that the privacy level of SGM for a fixed noise magnitude is proportional to $1/\sqrt{b}$, where $b$ is the sketching dimension, indicating that (for moderate $b$) SGM can provide much stronger privacy guarantees than the original GM under the same noise budget. We demonstrate the application of SGM to FL with either gradient descent or adaptive server optimizers, and establish theoretical results on optimization convergence, which exhibits only a logarithmic dependence on the number of parameters $d$. Experimental results confirm that at the same privacy level, SGM based FL is at least competitive with non‐sketching private FL variants and outperforms them in some settings. Moreover, using adaptive optimization at the server improves empirical performance while maintaining the privacy guarantees.

---

## 论文详细总结（自动生成）

### 1. 论文的核心问题与整体含义

联邦学习（FL）面临两大核心挑战：**通信开销大**与**隐私保护不足**。现有研究中，降低通信成本的草图压缩（sketching）与提供差分隐私（DP）的高斯机制（GM）往往被孤立地分析与应用——草图的隐私效应仅由草图维度 $b$ 决定，额外所需的隐私保障由 GM 单独提供。然而，这种做法未能挖掘两者联合的内在潜力。

本文旨在回答一个关键问题：**能否将草图操作和高斯噪声直接结合，并统一分析其整体隐私保障，从而获得比“各自为政”更优的通信–隐私权衡？** 在此基础上，论文提出**草图高斯机制（SGM）**，并随之构建一个兼具通信效率与强客户端级隐私保障的联邦学习框架，其优化收敛保证仅对数依赖于模型总参数 $d$，凸显了“将通信压缩与隐私加噪一体设计”的核心思想。

### 2. 论文提出的方法论

- **核心机制（SGM）**  
  SGM 的输出定义为 $\mathrm{SG}(\theta; R, \xi) = R\theta + \xi$，其中 $R\in\mathbb{R}^{b\times d}$ 是各元素独立同分布从 $\mathcal{N}(0, 1/\sqrt{b})$ 采样的高斯草图矩阵，$\xi\sim\mathcal{N}(0, \sigma_g^2 I_b)$ 是高斯噪声。相比传统高斯机制（$\theta + \xi$），SGM 先压缩再扰动，从而改变了两邻近数据集输出的分布结构：**两者不再是不同均值、相同方差的高斯，而是相同均值 0、不同方差的高斯**。

- **隐私分析的新视角**  
  利用 Rényi DP（RDP）框架，论文推导出 SGM 的 Rényi 散度上界为 $\frac{\alpha^2 \tau^4}{(\alpha-1) b \sigma_g^4}$（$\tau$ 为裁剪阈值）。由此，组合成的最终隐私预算 $\epsilon_p$ 满足 $\epsilon_p = O\left(\frac{1}{\sqrt{b}\,\sigma_g^2}\right)$。这意味着在给定目标隐私 $\epsilon_p$ 下，草图维度 $b$ 越大，所需添加的高斯噪声方差 $\sigma_g^2$ 越小，**草图本身提供了可量化的隐私放大效应**，突破了先前分析（仅 $\approx 1+O(1/\sqrt{b})$ 的微弱增益）的局限。

- **联邦学习算法 Fed‑SGM**  
  将 SGM 嵌入联邦学习流程：每轮所选客户端进行 $K$ 步本地 SGD，将归一化后的本地更新 $\frac{\Delta_c}{\eta_{\text{local}}}$ 裁剪至 $\tau$，再经 SGM 压缩并上传；服务器聚合草图后，通过草图矩阵的转置 $R^\top$（近乎无偏升维）恢复至原维度，并由全局优化器 `GLOBAL_OPT`（支持 GD 或 AMSGrad 等自适应优化器）更新全局模型。该设计同时保障了客户端级 DP 与通信效率。

- **优化理论保证**  
  在梯度范数有界、随机噪声为子高斯、损失海森矩阵具有**小绝对本征维度** $I$（即 $\frac{\sum|\lambda_i|}{\max \lambda_i}$ 有界）等假设下，证明了 Fed‑SGM 收敛的上界仅包含对数级依赖 $\log d$，且额外项来自裁剪和加噪均可控制。无论采用 GD 还是 AMSGrad，均能给出依概率收敛的明确速率。

### 3. 实验设计

- **数据集与模型**
  - 视觉任务：完整 EMNIST ByClass（814K/140K 训练/测试，62 类），使用 ResNet101（约 42M 参数）。
  - 语言任务：GLUE 中的 SST‑2 情感分类（67349/1821 训练/测试，2 类），微调 BERT‑Base（约 100M 参数）。

- **联邦环境与超参数**
  - 客户端总数 $C=625$，每轮随机无放回采样 $N=4$ 个客户端，本地 $K=18$ 步 SGD，本地批量大小 64，裁剪阈值 $\tau=1$。
  - 视觉任务草图维度 $b=4\times10^5$（约 1% 压缩率），语言任务 $b=2\times10^5$（约 0.2%）。
  - 隐私参数 $\delta_p=10^{-5}$，对无草图基线（DP‑FedAvg 及其 Adam 变体），改变 $\sigma_g$ 并通过 Moments Accountant 计算对应 $\epsilon_p$；对 SGM，针对每个 $\epsilon_p$ 数值求解 RDP 以得到最小所需 $\sigma_g$。

- **对比方法**
  - **无草图 GD**：标准 DP‑FedAvg（高斯机制，无草图）。
  - **无草图 Adam**：将 DP‑FedAvg 的服务器优化器换为 Adam。
  - **DiffSketch**：此前将草图与 DP 结合的基线方法。
  - **Fed‑SGM (GD)** 和 **Fed‑SGM (Adam)**：论文所提方法。

- **消融实验**
  - 不同隐私预算 $\epsilon_p$（约 4 档）下的测试精度比较。
  - 不同草图维度（$4\times10^4, 4\times10^5, 4\times10^6, 4\times10^7$）对精度的影响。
  - 不同裁剪阈值 $\tau$（0.5, 1, 2）和不同本地步数 $K$（9, 18, 36）。
  - IID 与非 IID 数据划分（Dirichlet 分布，参数 0.05）的鲁棒性测试。
  - 优化器选择：Adam vs AMSGrad。

### 4. 资源与算力

论文在致谢中提及计算资源来自 NCSA 和 ICCP；附录 F.1 进一步说明所有实验均在搭载 **AMD EPYC 7713 64‑核处理器和 NVIDIA A100 Tensor Core GPU** 的集群上运行。但未明确给出所用 GPU 总量、单次实验时长及总 GPU 时数等详细指标。

### 5. 实验数量与充分性

实验覆盖了两个典型领域（视觉、语言）的大型模型，包含 **至少 4 种隐私等级 × 4 种方法（或更多）** 的组合，并额外进行了多组消融研究，总计实验组数可达数十组。  
从评估角度看，实验设计较为全面：  
- 对比了 sketch 与 non‑sketch、GD 与自适应优化器；  
- 通过严格计算确保所有方法在**相同（$\epsilon_p,\delta_p$）‑DP 保证**下比较，保证了公平性；  
- 增加了 IID/非 IID、超参数敏感性等分析，增强了结论的稳健性。  
综合而言，实验数量充足，且评估纬度多元，能较充分地支撑主要论断。

### 6. 论文的主要结论与发现

- SGM 的隐私分析揭示了 **$\epsilon_p \propto 1/\sqrt{b\sigma_g^2}$**，证明草图维度 $b$ 可直接贡献隐私放大，而非仅是近似工具。
- 在固定隐私预算下，Fed‑SGM 所需注入的高斯噪声方差**严格小于**标准（无草图）高斯机制，这在实际中表现为更高的模型精度或更低的噪声干扰。
- 结合自适应服务器优化器（Adam/AMSGrad）时，Fed‑SGM 的性能提升尤为明显，在多项设置下优于无草图基线；同时，自适应优化器本身相比 SGD 在所有方法中均带来增益。
- 联邦优化收敛证明中，通过利用 Hessian 小绝对本征维度的性质，将收敛界对参数维度 $d$ 的依赖从线性降为对数级，为高维模型下的理论保证提供了支持。

### 7. 优点

- **统一的隐私‑通信分析**：首次将草图与高斯机制融为一体进行 Rényi DP 分析，得到简洁且严格的隐私上界，理论上清晰地揭示了草图的隐私放大效应。
- **实际优势显著**：在相同隐私约束下，SGM 因减少噪声而提升模型质量，同时兼具通信压缩（$b\ll d$）的好处，实现了“一箭双雕”。
- **灵活的服务器优化**：框架支持 GD 和 AMSGrad 等自适应优化器，理论与实验均表明其兼容性。
- **细致的收敛理论**：通过引入海森绝地本征维度假设，回避了常规分析中缩放 $d$ 的瓶颈，使高维 FL 的理论分析更具现实意义。
- **实验全面且公平**：多任务、多隐私等级、多超参数的对比，并严格对齐所有方法的隐私会计，评价可靠。

### 8. 不足与局限

- **草图矩阵类型受限**：当前分析仅针对**各向同性高斯草图**，尚未推广至 Count‑Sketch、随机哈达玛等其他常用草图，其在一般矩阵下的隐私与收敛性质仍待探索。
- **非 IID 实验深度有限**：尽管展示了非 IID 下 SGD 和 Adam 的对比结果，但整体实验仍以 **IID 划分为主**，对强异构场景（如 Dirichlet 浓度远低于 0.05 的极端情况）的评估不够充分。
- **计算与通信开销的显式对比未量化**：论文未详细报告 SGM 的额外计算（QR/SVD 伪逆 vs 转置、草图矩阵生成）和实际通信时间，与基线在端到端耗时上的比较不够直观。
- **扩展性讨论不足**：未深入探讨与量化压缩、安全聚合等相结合时可能出现的交互问题，也未分析在超大规模模型（数十亿参数）下的适用性。
- **隐私分析中部分假设的实际验证**：如 Hessian 小绝对本征维度的假设虽有文献支撑，但在所测实验中缺乏直接谱分析验证，仅作为理论收敛的条件。

（完）
