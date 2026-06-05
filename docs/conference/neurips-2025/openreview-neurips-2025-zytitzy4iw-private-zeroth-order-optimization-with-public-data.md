---
title: Private Zeroth-Order Optimization with Public Data
title_zh: 带公开数据的私有零阶优化
authors: "Xuchen Gong, Tian Li"
date: 2025-09-18
pdf: "https://openreview.net/pdf?id=zytITzY4IW"
tags: ["query:daily"]
score: 8.0
evidence: 利用公开数据改进差分隐私机器学习中零阶优化的梯度近似，与私有分布式机器学习相关
tldr: 针对一阶差分隐私优化（如DP-SGD）计算与内存开销大的瓶颈，提出利用公开数据引导零阶方法的梯度近似，在保证隐私的同时降低开销，并提升比纯零阶方法更佳的效用。
source: NeurIPS-2025-Accepted
selection_source: conference_retrieval
motivation: 一阶差分隐私优化计算和内存成本高，零阶方法虽有前景但效用较低。
method: 利用公开数据改进零阶梯度估计，结合函数评估与公开先验。
result: 在多个任务上，比现有零阶方法显著提升准确率，接近一阶方法效用。
conclusion: 公开数据辅助的零阶优化为实用差分隐私训练提供了轻量级替代方案。
---

## Abstract
One of the major bottlenecks for deploying popular first-order differentially private (DP) machine learning algorithms (e.g., DP-SGD) lies in their high computation and memory cost, despite the existence of optimized implementations.  Zeroth-order methods have promise in mitigating the overhead, as they leverage function evaluations to approximate the gradients, hence significantly easier to privatize. While recent works have explored zeroth-order approaches in both private and non-private settings,  they still suffer from relatively low utilities compared with DP-SGD, and have only been evaluated in limited application domains. 
In this work, we propose to leverage public information to guide and improve gradient approximation of private zeroth-order algorithms. We explore a suite of \underline{p}ublic-data-\underline{a}ssisted \underline{z}eroth-\underline{o}rder optimizers (PAZO) with minimal overhead. We provide theoretical analyses of the PAZO framework under an assumption of the similarity between public and private data. Empirically, we demonstrate that PAZO achieves superior privacy/utility tradeoffs across vision and text tasks in both pre-training and fine-tuning settings, outperforming the best first-order baselines (with public data) especially in highly private regimes, while offering up to $16\times$ runtime speedup.

---

## 论文详细总结（自动生成）

# 论文总结：《带公开数据的私有零阶优化》

## 1. 核心问题与整体含义
- **研究动机**：差分隐私（DP）训练的主流一阶方法（如 DP‑SGD）需要逐样本梯度裁剪，计算与内存开销巨大，难以在大规模场景下部署。
- **零阶优化的机会与瓶颈**：零阶方法通过函数值查询近似梯度，易于私有化且效率更高，但其梯度估计方差大，效用明显低于一阶方法（尤其在高维空间）。
- **本文目标**：利用少量、与私有数据分布相似的**公开数据**及其一阶梯度为私有零阶优化提供“先验”，在保留零阶方法轻量级优势的同时，大幅缩小与一阶 DP 方法的性能差距。

## 2. 方法论
- **核心思想**：在私有数据上使用零阶 oracle（函数查询）做差分隐私保护，同时引入公开数据的一阶梯度来引导或约束随机搜索方向。
- **三种具体算法（PAZO 系列）**：
  - **PAZO‑M（混合）**：将私有零阶估计与公开一阶梯度做凸组合，通过调节混合系数 α 控制公开信息的权重；提出合理对齐两者范数以简化调参。
  - **PAZO‑P（子空间采样）**：将随机扰动方向限制在由 k 个公开梯度张成的低维子空间内，通过零阶查询学习其组合系数。这一变化使问题维度从 $d$ 降为 $k(\ll d)$，极大降低估计方差。
  - **PAZO‑S（选择最优公开梯度）**：基于私有数据的函数查询值，从 k 个候选公开梯度中选择使损失最小的方向，并可加入一个噪声扰动向量以弥补残差。
- **隐私保护机制**：所有方法均直接在函数查询的标量值上加大噪声进行私有化（依赖高斯机制），不触碰私有数据的一阶梯度，保留了零阶方法的轻量隐私开销。
- **理论分析**：假设公有‑私有数据满足 γ‑相似性，给出三种算法在非凸条件下的收敛率，证明 PAZO‑M 的误差含 $O((1-α)/α·√d)$，PAZO‑P 为 $O(k)$（维度无关），PAZO‑S 更可达到与 $d$ 无关的常数界；同时还提供了有界损失假设下的改进界。

## 3. 实验设计
- **任务与数据集**：
  - 图像分类：从头训练 NFResNet18@CIFAR‑10；微调 Places365 预训练的 ViT‑S@Tiny‑ImageNet。
  - 文本分类：从头训练 LSTM@IMDB；提示微调 RoBERTa‑base@MNLI。
- **公开数据构造**：引入分布偏移（类别不平衡、语义上下文变化），以模拟真实场景中的公私数据相似性差异。
- **对比基准**：
  - 纯私有方法：DP‑SGD、DPZero（无公开数据）。
  - 带公开数据的一阶方法：DPMD、DOPE‑SGD、GEP。
- **评估指标**：不同隐私预算 ε = 0.1, 0.5, 1, 2, 3 下的准确率，以及每迭代运行时间、收敛速度。

## 4. 资源与算力
- **硬件**：所有实验均在一张 48GB 的 L40S GPU 上运行。
- **优化实现**：为公平比较，对一阶 DP 算法使用了向量化（vmap）、即时编译（JIT）和静态图优化等加速手段，并选择在内存约束下最快的实现。
- **说明**：文中未报告训练所有模型的总 GPU 时，但提供了每迭代的平均时间（秒/迭代）来对比方法效率；算力需求整体不高，实验易于复现。

## 5. 实验数量与充分性
- **多维度评估**：覆盖 4 个数据集 ×（5 个隐私级别 + 非隐私），对比了 6‑7 种方法（包含 3 种 PAZO 变体），共形成数十项主实验结果（表 2‑5）。
- **消融与敏感性分析**：
  - 扰动采样次数 $q$ 的影响。
  - 混合系数 $\alpha$、公开批次大小 $b'$、候选数 $k$、噪声扰动尺度 $\epsilon$ 的鲁棒性测试（图 6、图 8）。
  - 不同公开数据与私有数据的相似程度 $\gamma$ 对性能的影响（表 7）。
- **公平性**：超参数按统一网格搜索，batch size 固定为 64，所有方法均采用 100‑200 轮训练，并采用一致的评价标准，实验设置客观、详实。

## 6. 主要结论与发现
- **性能提升**：在全部四个任务上，PAZO 均显著优于无公开数据的零阶基线 DPZero；在较小 ε 的高隐私区域，PAZO 可超越所有带公开数据的一阶方法，实现更好的隐私‑效用权衡。
- **鲁棒性**：零阶方法（包括 PAZO）在不同 ε 下准确率下降幅度远小于一阶方法，对隐私预算更不敏感。
- **效率优势**：PAZO 每轮迭代时间相比最优一阶方法加速高达 16×；且在较少训练轮数下即可收敛，积累噪声更少。
- **超参不敏感**：PAZO 对引入的超参数（$\alpha, k, b', \epsilon$）表现出很强的鲁棒性，易于调参。

## 7. 优点
- **方法设计巧妙**：将公开数据的一阶信息与零阶查询的隐私友好性有机结合，既保持轻量高效，又大幅提升效用。
- **理论扎实**：为三种变体都提供了清晰的收敛分析，并展示了对模型维度的不同依赖关系。
- **实验全面**：涵盖视觉与文本、预训练与微调、不同分布偏移，验证框架的通用性和实际价值。
- **可复现性强**：提供了详细实验设置、超参数搜索网格，并公开了代码。

## 8. 不足与局限
- **依赖相似性假设**：理论分析依赖于公有‑私有数据的 γ‑相似性，当实际中公开数据与私有数据分布差异较大时，性能提升可能受限。
- **大规模模型验证不足**：实验主要集中在中等规模的模型（如 ViT‑S、RoBERTa‑base），虽然讨论了内存效率，但未在数十亿参数级别的大模型上实际验证加速与效能。
- **收敛界可进一步锐化**：作者在结尾指出未来可考虑更精细的相似性度量以获得更紧的界。
- **部分场景加速有限**：在 MNLI 的任务上仅观察到约 2× 加速（可能受模型大小或任务特性影响），对极致加速的期待并非在所有设置下都成立。
- **未有错误条或多随机种子报告**：文内所有结果基于随机种子 0，缺少多轮运行的统计检验（但通过超参数鲁棒性实验部分弥补了这一不足）。

（完）
