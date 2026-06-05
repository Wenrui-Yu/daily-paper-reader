---
title: Towards Trustworthy Federated Learning with Untrusted Participants
title_zh: 面向不可信参与者的可信联邦学习
authors: "Youssef Allouah, Rachid Guerraoui, John Stephan"
date: 2025-05-01
pdf: "https://openreview.net/pdf?id=PjadKnUson"
tags: ["query:daily"]
score: 10.0
evidence: 具有隐私和抗恶意参与者的联邦学习
tldr: "针对联邦学习中恶意参与者和隐私泄露且无需可信服务器的难题,提出CafCor算法,利用参与方之间的共享随机性注入相关噪声,实现鲁棒聚合与差分隐私,在弱信任假设下显著优于本地差分隐私方法。"
source: ICML-2025-Accepted
selection_source: conference_retrieval
figures_json: "[{\"url\": \"assets/figures/openreview/openreview-icml-2025-pjadknuson/fig-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 1676, \"height\": 818, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-icml-2025-pjadknuson/fig-002.webp\", \"caption\": \"\", \"page\": 0, \"index\": 2, \"width\": 1661, \"height\": 816, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-icml-2025-pjadknuson/fig-003.webp\", \"caption\": \"\", \"page\": 0, \"index\": 3, \"width\": 1594, \"height\": 919, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-icml-2025-pjadknuson/fig-004.webp\", \"caption\": \"\", \"page\": 0, \"index\": 4, \"width\": 1587, \"height\": 904, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-icml-2025-pjadknuson/fig-005.webp\", \"caption\": \"\", \"page\": 0, \"index\": 5, \"width\": 1568, \"height\": 917, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-icml-2025-pjadknuson/fig-006.webp\", \"caption\": \"\", \"page\": 0, \"index\": 6, \"width\": 1565, \"height\": 912, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-icml-2025-pjadknuson/fig-007.webp\", \"caption\": \"\", \"page\": 0, \"index\": 7, \"width\": 1568, \"height\": 913, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-icml-2025-pjadknuson/fig-008.webp\", \"caption\": \"\", \"page\": 0, \"index\": 8, \"width\": 1571, \"height\": 913, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-icml-2025-pjadknuson/fig-009.webp\", \"caption\": \"\", \"page\": 0, \"index\": 9, \"width\": 1570, \"height\": 910, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-icml-2025-pjadknuson/fig-010.webp\", \"caption\": \"\", \"page\": 0, \"index\": 10, \"width\": 1567, \"height\": 910, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-icml-2025-pjadknuson/fig-011.webp\", \"caption\": \"\", \"page\": 0, \"index\": 11, \"width\": 1572, \"height\": 916, \"label\": \"Figure\"}, {\"url\": \"assets/figures/openreview/openreview-icml-2025-pjadknuson/fig-012.webp\", \"caption\": \"\", \"page\": 0, \"index\": 12, \"width\": 1568, \"height\": 914, \"label\": \"Figure\"}]"
tables_json: "[{\"url\": \"assets/tables/openreview/openreview-icml-2025-pjadknuson/table-001.webp\", \"caption\": \"\", \"page\": 0, \"index\": 1, \"width\": 841, \"height\": 197, \"label\": \"Table\"}]"
motivation: "现有方法需可信服务器才能同时实现鲁棒性和隐私,假设过强。"
method: "利用参与方对间共享随机种子注入相关噪声,结合鲁棒梯度聚合。"
result: "CafCor在无信任假设下提供了强隐私-效用权衡,超越本地DP方法。"
conclusion: "弱化信任假设即可实现可信联邦学习,为实际部署提供可能。"
---

## Abstract
Resilience against malicious participants and data privacy are essential for trustworthy federated learning, yet achieving both with good utility typically requires the strong assumption of a trusted central server. This paper shows that a significantly weaker assumption suffices: each pair of participants shares a randomness seed unknown to others.  
In a setting where malicious participants may collude with an untrusted server, we propose CafCor, an algorithm that integrates robust gradient aggregation with correlated noise injection, using shared randomness between participants.
We prove that CafCor achieves strong privacy-utility trade-offs, significantly outperforming local differential privacy (DP) methods, which do not make any trust assumption, while approaching central DP utility, where the server is fully trusted.  
Empirical results on standard benchmarks validate CafCor's practicality, showing that privacy and robustness can coexist in distributed systems without sacrificing utility or trusting the server.

---

## 论文详细总结（自动生成）

好的，以下是根据您提供的论文内容生成的结构化、深入、客观的中文总结。

### 1. 论文的核心问题与整体含义

-   **核心问题**：在分布式机器学习（尤其是联邦学习）中，同时实现三个目标是巨大挑战：（1）**鲁棒性**（抵御恶意参与者的攻击）；（2）**数据隐私**（防止服务器窥探数据）；（3）**高模型效用**（保证模型性能）。
-   **现有困境**：通常，要取得好的隐私-效用权衡，需要**强信任假设**，即服务器完全可信（中心化差分隐私）。而在不信任服务器的本地差分隐私设置下，模型效用会大幅下降，尤其是同时还需要鲁棒性时。
-   **本文突破**：本文证明了实现上述三个目标所需的信任假设可以**显著弱化**。只需一个轻量级的假设：**每对参与者之间共享一个其他方不知的随机种子**。基于此，论文提出了一个在不可信服务器与恶意参与者共谋场景下，能够同时保证**可证明隐私、鲁棒性和高模型效用**的算法，填补了本地与中心化隐私模型之间的鸿沟。

### 2. 论文提出的方法论

论文提出了 `CAFCOR` 算法，其核心思想是结合**基于共享随机性的相关噪声注入**与一种**新型鲁棒梯度聚合**方法。

-   **核心思想与关键技术**：
    -   **相关噪声机制 (SecLDP)**：利用参与者之间预共享的随机种子，生成成对抵消的高斯噪声。这使得服务器在不知道所有秘密的情况下，无法消除特定参与者的噪声，从而为隐私保护创造了条件。这比完全不信任的本地差分隐私效用高，但又比完全信任服务器的中心化差分隐私假设弱。
    -   **CAF鲁棒聚合器**：为了在噪声环境中过滤恶意梯度，设计了 `CAF`（协方差边界无关过滤器）。该聚合器仅需恶意参与者数量的上限 `f`，通过迭代地识别并降低对最大方差方向贡献过高的输入向量的权重，最终输出一个鲁棒均值估计。
-   **算法流程 (`CAFCOR`)**：
    1.  **本地计算**：诚实参与者在本地计算梯度，进行裁剪以满足敏感度要求。
    2.  **噪声注入**：参与者向裁剪后的梯度中注入两类高斯噪声：（a）独立噪声；（b）与其它参与者成对抵消的相关噪声（基于共享随机种子生成）。
    3.  **动量更新**：参与者用加噪后的梯度更新本地动量。
    4.  **鲁棒聚合**：服务器使用 `CAF` 算法聚合所有参与者上传的向量，更新全局模型。
-   **理论保证**：
    -   **隐私**：证明了 `CAFCOR` 满足 `SecLDP` 隐私定义，且隐私成本的噪声量级为 `σ² = Θ(1 / (nε²))`，显著优于本地差分隐私的 `Θ(1/ε²)`。
    -   **效用**：给出了在强凸和非凸设置下的收敛速率，展示了其隐私-效用权衡可达到 `Õ((f+1)d / (n²ε²))`，当恶意参与者数量 `f` 为常数或次线性于 `n` 时，接近中心化差分隐私的性能，远优于本地差分隐私。

### 3. 实验设计

-   **数据集与场景**：在标准图像分类基准 **MNIST** 和 **Fashion-MNIST** 上进行评估。考虑了同质和异质（Dirichlet分布）的数据分布。
-   **基准方法与对比**：
    -   **不同隐私模型下的基线**：比较了在LDP、CDP、SecLDP（本文提出的）以及一个更强的变体ByzLDP下，使用`CAFCOR`与传统分布式SGD的性能。
    -   **不同鲁棒聚合器对比**：在CDP隐私模型下，将`CAF`与一系列标准鲁棒聚合方法对比，包括**CWTM**、**CWMED**、**GM（几何中位数）**、**MK（Multi-Krum）**、**Meamed**等。
-   **攻击类型**：测试了四种主流的拜占庭攻击：**FOE**、**ALIE**（小即为足）、**LF**（标签翻转）和**SF**（符号翻转）。

### 4. 资源与算力

-   **文中未明确提及**具体的GPU型号、数量和训练总时长。这是论文在实验报告方面的一个不足之处。

### 5. 实验数量与充分性

-   **实验数量**：实验覆盖了**2个数据集**、**4种攻击**、**多种鲁棒聚合器对比**、**2种异构性设置**、以及**2-3种不同的恶意参与者数量**，并考虑了从用户级到样本级的不同DP定义。实验设置较为丰富。
-   **充分性与客观性**：
    -   **充分性**：实验系统地验证了论文的核心主张，即 `CAFCOR` 在不同威胁模型下均能有效平衡隐私、鲁棒性和效用，且 `CAF` 聚合器优于多种现有鲁棒聚合器。附录中补充了大量额外实验，增强了说服力。
    -   **客观性**：使用了5个随机种子并报告了标准差，保证了可复现性。同时对比了最强基线，包括在特定设置下表现优异的 `MK` 和 `Meamed`，客观展示了 `CAF` 的优越性。同时指出了算力密集型聚合器 `SMEA` 的计算成本过高问题。

### 6. 论文的主要结论与发现

-   在联邦学习中，无需完全信任服务器，仅通过轻量级的**参与者对间共享随机种子**，就能构建**同时具备鲁棒性和强隐私保证且高实用性的可信系统**。
-   `CAFCOR` 算法在理论和实验上均证实了这一点。其性能**显著超越**了不信任服务器的本地隐私方法，并**逼近**了完全信任服务器的中心化隐私方法的效用，尤其当恶意参与方数量较少时优势更明显。
-   提出的 `CAF` 鲁棒聚合器，在理论上消除了对诚实输入协方差边界的依赖，且在实践中的性能一致且显著地优于现有鲁棒聚合算法。

### 7. 优点

-   **理论创新**：首次在敌手分布式学习框架下分析了基于秘密共享的本地差分隐私，并给出了紧的隐私-效用权衡界。
-   **算法创新**：`CAF` 聚合器无需依赖诚实数据协方差上界这一不切实际的假设，仅需恶意方数量上界，且计算复杂度为多项式时间，兼具理论优美性和实用性。
-   **假设弱化**：显著弱化了实现可信联邦学习所需的信任假设，具有很强的现实意义。
-   **实验扎实**：实验设计全面，覆盖了多种攻击、异构性和隐私模型，充分验证了理论发现，并与最先进的方法进行了公平对比。

### 8. 不足与局限

-   **算力报告缺失**：论文未报告实验所使用的具体算力资源，不利于复现成本评估。
-   **通信开销**：为交换随机种子，系统需在训练前进行一轮全连接通信，其通信复杂度为 `O(n²)`。虽然论文指出这是一次性开销且传输内容（整数种子）远小于迭代传输的模型，但在超大规模跨设备联邦学习中仍可能构成挑战。
-   **假设的适用范围**：论文假设恶意参与者和服务器是“诚实但好奇”或可以任意偏离协议，但未考虑更复杂的组合攻击，例如恶意参与者在共谋时不会主动暴露自己，这在现实中可能不完全成立。
-   **CAF效率**：尽管 `CAF` 相比指数复杂度的方法有了巨大进步，其 `O(f(nd² + d³))` 的复杂度在模型维度 `d` 极高时（如大语言模型）可能依然是瓶颈，虽然论文使用了幂法来近似加速。

（完）
