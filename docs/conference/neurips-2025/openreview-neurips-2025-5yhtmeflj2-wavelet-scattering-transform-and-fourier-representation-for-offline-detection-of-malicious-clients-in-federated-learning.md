---
title: Wavelet Scattering Transform and Fourier Representation for Offline Detection of Malicious Clients in Federated Learning
title_zh: 基于小波散射变换和傅里叶表示的联邦学习恶意客户端离线检测
authors: "Alessandro Licciardi, Davide Leo, Davide Carbone"
date: 2025-05-09
pdf: "https://openreview.net/pdf?id=5yhTMeFlj2"
tags: ["query:daily"]
score: 8.0
evidence: 联邦学习中的恶意客户端检测，涉及安全与信任
tldr: 针对联邦学习中异常或恶意客户端损害模型性能且难以在不访问原始数据的情况下检测的问题，提出Waffle算法，利用客户端本地数据的小波散射变换或傅里叶变换压缩表示，在训练前离线检测恶意客户端。实验表明该方法计算开销低、检测准确，有效保障了联邦学习的健壮性和安全性。
source: NeurIPS-2025-Rejected-Public
selection_source: conference_retrieval
motivation: 联邦学习中异常客户端严重影响模型性能，且无法直接访问原始数据，离线检测挑战大。
method: 使用小波散射变换或傅里叶变换计算本地数据的压缩表示，训练前基于表示离线标记恶意客户端。
result: 检测准确率高，计算开销低，能有效识别恶意客户端，提升联邦健壮性。
conclusion: 为联邦学习提供了一种轻量级、隐私友好的恶意客户端检测方法。
---

## Abstract
Federated Learning (FL) enables the training of machine learning models across decentralized clients while preserving data privacy. However, the presence of anomalous or corrupted clients—such as those with faulty sensors or non-representative data distributions—can significantly degrade model performance. Detecting such clients without accessing raw data remains a key challenge. We propose **Waffle** (**Wa**velet and **F**ourier representations for **F**ederated **Le**arning) a detection algorithm  that labels malicious clients before training, using locally computed compressed representations derived from either the Wavelet Scattering Transform (WST) or the Fourier Transform. Both approaches provide low-dimensional, task-agnostic embeddings suitable for unsupervised client separation. A lightweight detector, trained on a distillated public dataset, performs the labeling with minimal communication and computational overhead. While both transforms enable effective detection, WST offers theoretical advantages, such as non-invertibility and stability to local deformations, that make it particularly well-suited to federated scenarios. Experiments on benchmark datasets show that our method improves detection accuracy and downstream classification performance compared to existing FL anomaly detection algorithms, validating its effectiveness as a pre-training alternative to online detection strategies.

---

## 论文详细总结（自动生成）

## 论文总结：基于小波散射变换与傅里叶表示的联邦学习恶意客户端离线检测

### 1. 研究动机与核心问题
- **核心问题**：联邦学习（FL）中，某些客户端可能因传感器故障、数据污染或恶意攻击而产生异常数据，这些“恶意客户端”会显著降低全局模型的性能。由于无法直接访问原始数据，在训练前检测并剔除这些客户端极具挑战。
- **现有方法局限**：多数现有防御依赖在线检测模型更新（如梯度异常）或鲁棒聚合策略（如 Krum、TrimmedMean），但它们在训练开始后才能介入，计算开销大，且常假设大多数客户端为良性，在恶意客户端占比较高时效果下降。
- **本文动机**：提出一种**离线、轻量、隐私友好**的检测方法 Waffle，在 FL 训练开始前就标记出具有恶意数据的客户端，从而净化参与方集合，提高后续训练的稳定性和最终模型质量。

### 2. 方法论
- **整体思想**：利用客户端本地数据的光谱特征（傅里叶变换 FT 或小波散射变换 WST）构建低维、任务无关的嵌入，训练一个二分类检测器对恶意客户端进行识别。
- **关键技术细节**：
  - **客户端本地处理**：每个客户端对其本地样本执行主成分分析（PCA），提取前 \(r\) 个主成分及其解释方差，得到一个摘要向量 \(\hat{x}_k\)。然后对 \(\hat{x}_k\) 应用傅里叶变换或小波散射变换，得到固定大小的光谱嵌入 \(\phi_k = |\Phi[\hat{x}_k]|\)，并仅将该嵌入发送至服务器。
  - **服务器离线训练检测器**（Algorithm 1）：
    1. 使用辅助公开数据集 \(D_{\text{aux}}\) 生成模拟客户端数据，随机对其中一半样本施加**噪声攻击**（加性高斯噪声）或**模糊攻击**（高斯卷积），以此标注样本为恶意或良性。
    2. 将模拟数据划分给 \(\tilde{K}\) 个虚拟客户端（一半良性，一半恶意），对每个虚拟客户端计算 PCA 表示和光谱嵌入。
    3. 用这些 (嵌入, 标签) 对训练一个二分类器（使用 Binary Cross-Entropy 损失），得到检测器权重 \(w\)。
  - **在线检测与过滤**：在 FL 正式开始前，真实客户端本地计算并上传其光谱嵌入，服务器通过预训练的 \(w\) 进行分类，排除被判定为恶意的客户端。
- **理论支撑**：
  - FT 的线性性质使噪声攻击在频域表现为可加的干扰，而卷积定理则将模糊攻击转化为频谱上的点乘，便于区分。
  - WST 具有**非膨胀性**、**局部平移不变性**以及对小形变的 Lipschitz 连续性，且**不可逆**，有利于隐私保护和扰动鲁棒性。
  - 文中证明了剔除恶意客户端后，全局模型估计的偏差得以消除，方差显著降低（Proposition 1）。

### 3. 实验设计
- **数据集**：FashionMNIST、CIFAR-10、CIFAR-100，均在联邦非独立同分布设置下评估。
- **攻击场景**：系统随机生成噪声攻击和模糊攻击，并设定恶意客户端占比为 40% 和 90% 两种极端情况。
- **对比方法**：
  - **检测性能对比**：Waffle 的两种变体（基于 WST 和基于 FT）之间的比较（见表 1）。
  - **下游分类性能对比**：将 Waffle 与标准 FedAvg 结合，同以下鲁棒聚合基线进行比较：FedAvg（无防御）、Krum、mKrum、GeoMed、TrimmedMean。同时验证 Waffle 与这些聚合算法的正交性，即在其上叠加 Waffle 后的性能提升（见表 2）。
- **评价指标**：恶意客户端检测的 F1 分数、精确率、召回率、准确率；全局模型的测试准确率。

### 4. 资源与算力
- 论文正文和提供的材料中**未明确说明**使用的 GPU 型号、数量、具体训练时长等算力资源。仅提到实验细节见附录 B，但附录未包含在当前文本中，因此无法从中提取计算资源相关信息。

### 5. 实验数量与充分性
- **实验组数**：至少包含 3 个图像数据集 × 2 种攻击比例（40%，90%）× 2 种光谱变体（WST、FT）的检测实验，以及多个聚合算法 ×（不叠加/叠加 Waffle）的分类对比实验，总体实验较为丰富。
- **充分性与公平性**：
  - 考察了极端恶意多数（90%）场景，这在以往鲁棒聚合研究中较为少见，能体现方法的鲁棒性。
  - 对比基线涵盖主流拜占庭鲁棒聚合算法，且均采用相同的训练设置和超参数（附于附录），保证了比较的公平。
  - 提供了统计显著性验证（附录 B 提及三随机种子结果），增加了结果的可信度。

### 6. 主要结论与发现
- Waffle 能有效在 FL 训练前离线检测出恶意客户端，**无需访问原始数据**，计算和通信开销小。
- 在检测精度上，**WST 变体通常精确率更高**（极端 90% 恶意场景下可达 100% 精确率），而 FT 变体召回率更高。
- 将 Waffle（尤其是 WST 版本）与 FedAvg 结合后，下游分类准确率**全面超越**现有拜占庭鲁棒聚合方法，且能接近无恶意客户端时的理想性能。
- Waffle 与任何聚合算法正交，可在其之上叠加使用，进一步提升鲁棒性。

### 7. 优点
- **隐私保护设计**：仅传输聚合后的光谱嵌入，且 WST 不可逆，难以恢复原始数据。
- **离线与轻量**：检测在训练前完成，不干扰 FL 训练循环，适合资源受限的边缘设备。
- **无良性多数假设**：在恶意客户端占 90% 时仍可高精度检测，突破了传统鲁棒聚合的限制。
- **模型无关性**：不依赖具体的全局模型架构，可应用于各类 FL 任务。
- **坚实的理论基础**：从信号处理和统计估计角度分析了变换的适用性及剔除恶意客户端的益处。

### 8. 不足与局限
- **攻击类型受限**：目前仅针对数据层面的噪声和模糊攻击有效，对模型中毒、后门攻击、梯度操纵等高级威胁不具备防御能力。
- **依赖辅助数据集**：需要服务器拥有与目标任务相关的代表性公开数据来训练检测器，若辅助数据分布与真实客户端数据差异较大，检测器性能可能下降。
- **实验覆盖有限**：
  - 仅在较小的图像基准（FashionMNIST、CIFAR）上验证，未在更大规模或更复杂的数据集（如 ImageNet、文本/语音数据）上测试。
  - 攻击参数（噪声强度、模糊半径）的设定范围是否足够贴近现实故障值得进一步探讨。
- **潜在偏差风险**：若检测器误将某些罕见的良性数据分布（如少数群体数据）标记为恶意，可能引入公平性问题，文章虽提及但未做深入分析。
- **原理性局限**：PCA 压缩和光谱嵌入可能丢失对某些精细异常敏感的判别信息，方法的检测粒度有待更细致的研究。

（完）
