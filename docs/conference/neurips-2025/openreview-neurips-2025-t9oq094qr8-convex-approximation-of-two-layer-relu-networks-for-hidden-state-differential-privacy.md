---
title: Convex Approximation of Two-Layer ReLU Networks for Hidden State Differential Privacy
title_zh: 两层ReLU网络的凸近似用于隐藏状态差分隐私
authors: "Rob Romijnders, Antti Koskela"
date: 2025-09-18
pdf: "https://openreview.net/pdf?id=T9OQ094qR8"
tags: ["query:daily"]
score: 8.0
evidence: 利用两层ReLU网络的凸近似实现隐藏状态差分隐私，训练机器学习模型
tldr: 针对隐藏状态差分隐私仅适用于凸优化问题的局限，提出用凸函数近似两层ReLU网络，在隐藏状态威胁模型下实现可比的隐私效用权衡，将该隐私分析扩展到多层神经网络训练。
source: NeurIPS-2025-Accepted
selection_source: conference_retrieval
motivation: 隐藏状态DP分析局限于凸问题，无法直接应用于多层网络。
method: 用凸函数近似两层ReLU网络，在凸优化框架下进行私有训练。
result: 在分类任务上，凸近似训练达到与DP-SGD训练的两层ReLU网络相当的隐私效用。
conclusion: 凸近似为隐藏状态差分隐私在深度学习中的扩展提供了新途径。
---

## Abstract
The hidden state threat model of differential privacy (DP) assumes that the adversary has access only to the final trained machine learning (ML) model, without seeing intermediate states during training. However, the current privacy analyses under this model are restricted to convex optimization problems, reducing their applicability to multi-layer neural networks, which are essential in modern deep learning applications. Notably, the most successful applications of the hidden state privacy analyses in classification tasks have only been for logistic regression models. We demonstrate that it is possible to privately train convex problems with privacy-utility trade-offs comparable to those of 2-layer ReLU networks trained with DP stochastic gradient descent (DP-SGD). This is achieved through a stochastic approximation of a dual formulation of the ReLU minimization problem, resulting in a strongly convex problem. This enables the use of existing hidden state privacy analyses and provides accurate privacy bounds also for the noisy cyclic mini-batch gradient descent (NoisyCGD) method with fixed disjoint mini-batches. Empirical results on benchmark classification  tasks demonstrate that NoisyCGD can achieve privacy-utility trade-offs on par with DP-SGD applied to 2-layer ReLU networks.

---

## 论文详细总结（自动生成）

这是一篇关于差分隐私机器学习的研究论文，核心贡献在于通过凸近似方法，将隐藏状态（hidden state）差分隐私分析扩展到了两层ReLU网络，并给出了实用的隐私-效用权衡。以下是对该论文的详细总结。

---

### 1. 论文的核心问题与整体含义

- **研究背景与动机**
  - 差分隐私下的隐藏状态威胁模型（Hidden State DP）假设攻击者只能访问最终训练好的模型，而无法获取训练过程中的中间状态，这比标准DP-SGD中“攻击者看到所有迭代中间结果”的假设更贴近现实。
  - 然而，现有的隐藏状态隐私分析方法（如隐私放大迭代）仅适用于凸优化问题，这导致其最成功的应用仅限于逻辑回归等简单模型，无法直接用于现代深度学习中至关重要的多层神经网络。
  - 挑战：如何将隐藏状态隐私分析的适用范围从凸模型扩展到神经网络，同时保持竞争力强的隐私-效用权衡。

- **核心问题**
  - 能否通过凸近似将两层ReLU网络的训练问题转化为一个强凸问题，从而利用现有隐藏状态隐私分析（如Bok等人的f-DP/GDP分析），在只发布最终模型的情况下，获得与DP-SGD训练的两层ReLU网络相当的分类精度？

### 2. 论文提出的方法论

- **核心思想**
  - 利用Pilanci和Ergen提出的两层ReLU网络的凸对偶公式。该公式通过枚举所有可能的ReLU激活模式，将非凸网络训练问题等价地转化为一个带有组稀疏约束的凸优化问题（当隐藏层宽度足够时）。
  - 为了适应隐私分析，论文提出了一种**随机化的强凸近似**：
    1. **随机近似**：随机采样P个高斯向量来生成对应的激活模式（对角布尔矩阵），用这P个模式构造一个无约束的随机近似问题，避免了对数据依赖的约束（如锥约束）。
    2. **强凸化**：在损失函数中加入L2正则化项（系数λ），使得样本级损失函数成为λ-强凸和β-光滑的广义线性模型（GLM）。
  - 这样，最终得到的损失函数满足定理2.7（Bok等人的NoisyCGD分析）所需的所有条件，从而可以严格地为最终模型提供f-DP/（ε,δ）-DP保证。

- **关键公式与流程**
  - **近似模型**：定义样本损失 ℓ(v, x_j, y_j) 为：
    ```
    ℓ = 1/2 * Σ_{i=1}^P [ (Λ_i)_{jj} x_j^T v_i − y_j ]^2 + λ/2 Σ_{i=1}^P ‖v_i‖^2
    ```
    其中Λ_i由随机采样的u_i ∈ N(0, I_d)决定：(Λ_i)_{jj} = 1(x_j^T u_i ≥ 0)，参数v = {v_i}_{i=1}^P ∈ R^{P·d}。
  - **隐私训练算法**：使用**NoisyCGD**（带噪声的循环小批量梯度下降），数据被划分为固定大小的不相交批次，仅对最终模型做隐私会计。该算法的GDP参数μ由学习率η、正则化常数λ、梯度敏感度L和噪声σ决定，其核心收缩因子c = max{|1-ηλ|, |1-ηβ|}。
  - **隐私会计**：利用Bok等人的定理2.7，NoisyCGD的μ-GDP保证可以转换成(ε,δ)-DP，且通过选择适当的ηλ，其隐私预算收敛速度可比甚至优于使用Poisson采样的DP-SGD。

- **理论分析补充**
  - 在随机数据模型（X_ij ~ N(0,1)）下，当超平面数量P = O(n log n / d)且n/d ≥ 1时，凸近似问题的全局最小值可以趋近于0，结合经典DP-ERM边界，得到与特征维度d无关的效用界 ~O(1/√(nε))，优于现有DP-SGD在相同设置下的界。

### 3. 实验设计

- **数据集**
  - MNIST（6万训练/1万测试）、FashionMNIST（6万/1万）、CIFAR-10（5万/1万）。
  - 所有图像从原始像素直接向量化输入，不使用预训练卷积层。

- **对比方法**
  - **基线**：Sufficient Statistics Perturbation (SSP) 应用于三种特征（凸近似激活、随机ReLU特征、随机傅里叶特征（RFF））；DP-SGD训练的逻辑回归。
  - **主要比较对象**：
    1. DP-SGD + 标准两层ReLU网络（隐藏层宽度200-800）
    2. DP-SGD + 凸近似模型（无L2正则化，λ=0）
    3. NoisyCGD + 提出的强凸近似模型（λ>0）

- **评估设置**
  - 训练400个epoch，批大小固定在1000，DP噪声水平设为σ=5.0（对应ε≈1.33）和σ=15.0（对应ε≈4.76），δ=10^{-5}。
  - 超参数（学习率η、网络宽度P或W）通过差分隐私超参数调优选择，调优算法本身也消耗隐私预算，报告了调优后的总(ε,δ)。
  - 每个实验重复5次，报告均值和1.96倍标准误差。

### 4. 资源与算力

- **算力说明**
  - 文中明确指出，差分隐私超参数调优实验是整个项目中最耗时的部分。
  - 该部分实验使用了**8块NVIDIA GeForce RTX 3090 GPU**，每块运行约**3天**。
  - 其余常规训练部分的计算资源未具体说明，但基于上述描述，总体算力需求较高但可及。

### 5. 实验数量与充分性

- **实验组数**
  - **主要结果**：3个数据集 × 2种噪声水平 × 4-5种方法（含基线），共形成多组精度-ε曲线对比。
  - **隐私调优结果**：报告了在含调优隐私消耗下，三个数据集在两种最终ε水平（~2.88和~8.91）下各方法的准确率表格。
  - **消融研究**：包括随机超平面数量P的影响（P=32,64,128,256）、批大小的影响（从250到24000）、以及产品ηλ对ε收敛速度的影响分析。
  - **充分性与公平性**：实验覆盖了常见的分类基准，对比了同一任务下不同训练范式（非迭代SSP、迭代DP-SGD、迭代NoisyCGD）和网络结构（线性、ReLU、凸近似），并采用了统一的隐私会计方式和超参数调优流程，比较客观公正。不足是未在更大规模数据集或更复杂任务上验证。

### 6. 论文的主要结论与发现

- **可行性证明**：通过将两层ReLU网络凸近似并正则化，可以首次在隐藏状态威胁模型下，对图像分类任务获得高隐私-效用权衡，且效果显著优于逻辑回归。
- **实用性突破**：NoisyCGD在固定不相交批次上训练凸近似模型，其测试准确率在MNIST (92.4% @ ε=4.76)、FashionMNIST和CIFAR-10 (41.0% @ ε=4.76)上与DP-SGD训练的两层ReLU网络相当。
- **理论贡献**：给出了随机数据模型下，凸近似DP训练的效用界，显示出对特征维度d的不敏感性，理论上优于某些非凸DP-SGD分析。
- **计算优势**：NoisyCGD允许恒定批次大小，避免了Poisson采样的实现复杂性和吞吐量损失，更易于工程部署。

### 7. 优点

- **创新性结合**：巧妙地将“神经网络的凸对偶理论”与“隐私放大迭代分析”两个独立领域结合，解决了隐藏状态隐私分析无法用于神经网络的痛点。
- **分析严谨且实用**：
  - 为NoisyCGD提供了基于GDP的严格隐私保证，该方法计算效率高，解决了标准DP-SGD随机采样的实施困难。
  - 证明了加入L2正则化后的损失函数满足强凸和光滑性，使隐私分析无缝衔接。
- **理论-实验并重**：不仅给出了实证结果，还提供了随机数据模型下的理论效用界，增强了方法的理论说服力。
- **实验全面**：包含了丰富的消融实验、隐私超参数调优和与多个基线（线性模型、RFF、两层ReLU）的对比，结果稳定。

### 8. 不足与局限

- **模型深度限制**：当前方法仅针对两层全连接ReLU网络，尽管有提及可扩展到卷积层和更深网络的相关工作，但本文未实际拓展或验证。
- **凸近似维度开销**：随机超平面数P需随n和d增长（O(n log n / d)），当数据量大时，参数向量v维度为d×P×K，可能导致内存和计算负担增加。
- **理论假设较强**：效用界的推导依赖于随机数据模型（X服从独立高斯分布）和c=n/d≥1的假设，限制了其在实际非随机数据上的保障强度。
- **任务单一性**：实验仅集中在三个较小规模分类任务，未涉及更大图像数据集、NLP或生成任务，泛化性有待检验。
- **超参数敏感性**：隐私效用依赖于η和λ的乘积，该乘积需要平衡“遗忘”速度与模型精度，实践中需仔细调整。

（完）
