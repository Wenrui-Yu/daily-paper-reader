---
title: Online Locally Differentially Private Conformal Prediction via Binary Inquiries
title_zh: 基于二进制询问的在线本地差分隐私共形预测
authors: "Qiangqiang Zhang, Chenfei Gu, Xinwei Feng, Jinhan Xie, Ting Li"
date: 2025-09-18
pdf: "https://openreview.net/pdf?id=GqzMEkVp2i"
tags: ["query:daily"]
score: 4.0
evidence: 在线本地差分隐私共形预测，使用二进制询问，与隐私机器学习略有相关但非分布式优化
tldr: 针对流数据环境中隐私保护不确定性量化需求，提出在线本地差分隐私共形预测框架，通过随机二进制询问动态构建预测集，具有O(1)空间复杂度和高计算效率，适用于实时应用。
source: NeurIPS-2025-Accepted
selection_source: conference_retrieval
figures_json: "[{\"url\": \"assets/figures/openreview/openreview-neurips-2025-gqzmekvp2i/fig-001.webp\", \"caption\": \"\", \"page\": 3, \"index\": 1, \"width\": 1222, \"height\": 534}, {\"url\": \"assets/figures/openreview/openreview-neurips-2025-gqzmekvp2i/fig-002.webp\", \"caption\": \"\", \"page\": 9, \"index\": 2, \"width\": 3855, \"height\": 3301}, {\"url\": \"assets/figures/openreview/openreview-neurips-2025-gqzmekvp2i/fig-003.webp\", \"caption\": \"\", \"page\": 9, \"index\": 3, \"width\": 3766, \"height\": 3219}, {\"url\": \"assets/figures/openreview/openreview-neurips-2025-gqzmekvp2i/fig-004.webp\", \"caption\": \"\", \"page\": 10, \"index\": 4, \"width\": 3857, \"height\": 1517}, {\"url\": \"assets/figures/openreview/openreview-neurips-2025-gqzmekvp2i/fig-005.webp\", \"caption\": \"\", \"page\": 10, \"index\": 5, \"width\": 1185, \"height\": 735}, {\"url\": \"assets/figures/openreview/openreview-neurips-2025-gqzmekvp2i/fig-006.webp\", \"caption\": \"\", \"page\": 10, \"index\": 6, \"width\": 3855, \"height\": 1804}, {\"url\": \"assets/figures/openreview/openreview-neurips-2025-gqzmekvp2i/fig-007.webp\", \"caption\": \"\", \"page\": 10, \"index\": 7, \"width\": 1185, \"height\": 735}, {\"url\": \"assets/figures/openreview/openreview-neurips-2025-gqzmekvp2i/fig-008.webp\", \"caption\": \"\", \"page\": 22, \"index\": 8, \"width\": 4612, \"height\": 2536}, {\"url\": \"assets/figures/openreview/openreview-neurips-2025-gqzmekvp2i/fig-009.webp\", \"caption\": \"\", \"page\": 22, \"index\": 9, \"width\": 4612, \"height\": 2536}, {\"url\": \"assets/figures/openreview/openreview-neurips-2025-gqzmekvp2i/fig-010.webp\", \"caption\": \"\", \"page\": 23, \"index\": 10, \"width\": 4612, \"height\": 2536}, {\"url\": \"assets/figures/openreview/openreview-neurips-2025-gqzmekvp2i/fig-011.webp\", \"caption\": \"\", \"page\": 25, \"index\": 11, \"width\": 4612, \"height\": 2590}, {\"url\": \"assets/figures/openreview/openreview-neurips-2025-gqzmekvp2i/fig-012.webp\", \"caption\": \"\", \"page\": 25, \"index\": 12, \"width\": 4612, \"height\": 2590}, {\"url\": \"assets/figures/openreview/openreview-neurips-2025-gqzmekvp2i/fig-013.webp\", \"caption\": \"\", \"page\": 26, \"index\": 13, \"width\": 4612, \"height\": 2590}, {\"url\": \"assets/figures/openreview/openreview-neurips-2025-gqzmekvp2i/fig-014.webp\", \"caption\": \"\", \"page\": 26, \"index\": 14, \"width\": 4612, \"height\": 2590}, {\"url\": \"assets/figures/openreview/openreview-neurips-2025-gqzmekvp2i/fig-015.webp\", \"caption\": \"\", \"page\": 27, \"index\": 15, \"width\": 4613, \"height\": 2551}, {\"url\": \"assets/figures/openreview/openreview-neurips-2025-gqzmekvp2i/fig-016.webp\", \"caption\": \"\", \"page\": 27, \"index\": 16, \"width\": 4516, \"height\": 2514}, {\"url\": \"assets/figures/openreview/openreview-neurips-2025-gqzmekvp2i/fig-017.webp\", \"caption\": \"\", \"page\": 28, \"index\": 17, \"width\": 4515, \"height\": 2514}]"
motivation: 现有隐私保护预测方法无法在线处理流数据，且计算和存储要求高。
method: 提出随机二进制询问机制，在线构建隐私保护预测集。
result: 实现高效的一遍式在线预测，保证隐私且精度可控。
conclusion: 该方法为实时隐私保护预测提供了实用方案。
---

## Abstract
We propose an online conformal prediction framework under local differential privacy to address the emerging challenge of privacy-preserving uncertainty quantification in streaming data environments. Our method constructs dynamic, model-free prediction sets based on randomized binary inquiries, ensuring rigorous privacy protection without requiring access to raw data. Importantly, the proposed algorithm can be conducted in a one-pass online manner, leading to high computational efficiency and minimal storage requirements with $\mathcal{O}(1)$ space complexity, making it particularly suitable for real-time applications. The proposed framework is also broadly applicable to both regression and classification tasks, adapting flexibly to diverse predictive settings. We establish theoretical guarantees for long-run coverage at a target confidence level, ensuring statistical reliability under strict privacy constraints. Extensive empirical evaluations on both simulated and real-world datasets demonstrate that the proposed method delivers accurate, stable, and privacy-preserving predictions across a range of dynamic environments.

---

## 论文详细总结（自动生成）

好的，作为一名资深学术论文分析助手，我将使用中文、以Markdown形式，对这篇题为《Online Locally Differentially Private Conformal Prediction via Binary Inquiries》的论文进行结构化、深入、客观的总结。

### **1. 论文的核心问题与研究动机**
*   **核心问题**: 在医疗监控、实时竞价等流数据环境中，数据分布随时间动态变化，现有的预测不确定性量化方法（如共形预测）存在两个主要缺陷：一是缺乏内置的隐私保护机制，容易泄露用户敏感信息；二是其在线扩展通常假设能获取真实结果标签以更新模型，这在隐私敏感场景下不可行。
*   **研究动机**: 为了解决上述挑战，论文旨在开发一个**在本地差分隐私（LDP）约束下、完全在线的共形预测框架**。其核心目标是消除对可信中心服务器的依赖，在单个用户数据离开本地设备前就进行隐私保护处理，同时实现对动态数据流的实时、高效不确定性量化，且无需获取原始真实数据。

### **2. 论文提出的方法论**
*   **核心思想**: 将共形预测中分位数阈值的更新过程，转化为一个基于**私有化二进制反馈**的在线学习问题。服务器向每个用户发出一个简单的“是/否”型二进制询问（例如，预测区间是否覆盖了真实值），用户通过一个本地随机化机制（`LRBR`算法）返回一个加噪后的二进制响应，服务器利用这个私有化信息进行分位数的在线更新。
*   **关键技术细节**:
    *   **本地随机化二进制响应 (LRBR)**: 用户以概率 `r` 返回真实答案，以概率 `1-r` 返回一个公平硬币抛掷的随机结果。`r` 值越小，隐私保护越强。
    *   **硬币下注 (Coin-Betting) 在线优化**: 采用一种无参数的在线凸优化框架，将分位数估计过程建模为重复的下注游戏。算法基于历史反馈（`ct = -gt`，其中 `gt` 为私有化次梯度）自适应地调整“下注比例” `λt`，并以此更新财富 `Wt`，最终将分位数阈值 `qt` 更新为 `λt+1 * Wt`。
    *   **算法流程（回归任务为例）**:
        1.  服务器对当前数据点 `Xt` 给出预测 `Ŷt`，并根据当前分位数阈值 `qt` 构建预测区间 `[Ŷt - qt, Ŷt + qt]`。
        2.  用户本地计算非一致性分数 `St = |Yt - Ŷt|`。
        3.  服务器向用户发起二进制询问，用户执行 `LRBR(St, qt, r)` 并返回私有化响应 `L`。
        4.  服务器根据 `L` 计算私有化次梯度 `gt`，并通过硬币下注算法更新 `qt+1`，以用于下一轮预测。
*   **扩展到分类任务**: 采用与回归类似的逻辑，将预测区间构建替换为预测集构建，非一致性分数定义为 `1 - 预测概率`，并使用相同的二进制询问和分位数更新机制。

### **3. 实验设计**
*   **数据集与场景**:
    *   **模拟数据 (回归)**: 模拟了四种数据漂移场景：突变漂移（同方差/异方差）、平滑漂移和无漂移。这些场景覆盖了动态环境的主要类型。
    *   **模拟数据 (分类)**: 模拟了平滑漂移、放大漂移、类别涌现和静态场景。
    *   **真实数据 (回归)**: 使用电力需求预测数据集 **ELEC2**。
    *   **真实数据 (分类)**: 使用智能手机活动识别的 **WISDM** 数据集。
*   **基准方法 (Benchmark)**:
    *   **DPCP (Angelopoulos et al.， 2022)**：一种离线的、基于中心差分隐私的共形预测方法。
    *   **DtACI (Gibbs and Candès， 2024)**：一种先进的在线共形预测方法，但不带隐私保护。
*   **对比指标**: 长期覆盖率、预测区间/集合的宽度/大小、计算时间。

### **4. 资源与算力**
*   论文在“实验计算资源”部分（附录）明确指出，所有实验均在配备**16GB RAM** 和 **AMD Ryzen 9 7940HX处理器**的笔记本电脑上运行，未使用GPU。这表明该方法计算资源需求极低，适合在边缘设备等资源受限环境中部署。
*   计算时间对比（表2）量化了其高效性：处理25,000个数据点，本文方法耗时**0.167秒**，而DtACI耗时19.34秒，DPCP耗时1.378秒。

### **5. 实验数量与充分性**
*   **实验数量**: 论文进行了较为全面的实验，主要包含以下几组：
    *   **回归模拟实验**: 4种数据漂移场景 × 4种隐私等级（无隐私， ε=3, 1, 0.5），共16组对比。
    *   **分类模拟实验**: 4种数据漂移场景 × 4种隐私等级，共16组对比。
    *   **真实数据实验**: 分别在回归（ELEC2）和分类（WISDM，包含2个独立用户任务）数据集上进行，并分别就不同隐私等级和方法（包含DtACI的初始化敏感性分析）进行了测试。
    *   **其他分析**: 还包括了私有预测模型与非私有模型的对比、不同初始化设置对方法鲁棒性的影响、隐私预算分配方式的影响等实验。
*   **充分性与公平性**:
    *   **充分性**: 实验覆盖了模拟和真实、回归和分类、多种数据漂移模式和多个隐私强度等级，对比了离线隐私方法和在线非隐私方法，从多个维度验证了方法的有效性、鲁棒性和高效性。分析也较为深入，不仅报告了最终结果，还探讨了方法的动态行为和敏感性。因此，实验设计是**充分**的。
    *   **公平性**: 对比基准虽然经典，但存在一定局限性。DPCP是离线的，其对比突显了在线方法的优势，但并非公平的在线对比；DtACI不包含隐私保护，其对比突显了本方法在实现隐私保护的同时仍能保持性能的优势，但同样不是完全的对等比较。严格来说，缺乏一个**在线的、具有隐私保护的对等基准**进行比较。

### **6. 论文的主要结论与发现**
*   **隐私与效用的平衡**: 提出的方法在严格的本地差分隐私约束下，能够实现有效的在线共形预测。预测集的长期覆盖率能够渐近地收敛到预设的置信水平。
*   **高计算效率**: 方法支持一遍式在线处理，具有`O(1)`的常数级空间复杂度和极低的计算延迟，非常适合实时流数据应用。
*   **方法的鲁棒性**: 与DtACI等方法相比，该方法对初始化参数不敏感，表现出更好的鲁棒性。
*   **端到端隐私**: 当与本地差分隐私训练的预测模型结合时，框架可以保证**端到端的隐私保护**。
*   **性能对比**: 在非平稳环境中，相较于离线的DPCP，本文方法能生成更窄（更高效）的预测区间，同时保持接近目标的覆盖率。相比非私有的DtACI，预测集效率相当或更优，且天然带隐私保护。

### **7. 优点：方法与实验设计的亮点**
*   **创新的问题设定**: 首次将在线共形预测与本地差分隐私结合，解决了动态环境中隐私保护与不确定性量化并存的挑战，具有重要的现实意义。
*   **精巧的算法设计**: 利用共形预测固有的二进制结构，设计了`LRBR`机制，巧妙地将复杂的隐私量化问题转化为简单的二进制询问，实现了隐私、效率与效用的良好平衡。
*   **坚实的理论保证**: 提供了详细的本地差分隐私证明、有限时间遗憾界分析和长期覆盖率渐近保证，理论支撑严密。
*   **强大的实用适应性**: 算法同时支持回归和分类任务，模型无关（No Free Lunch），计算和存储开销极低，适用于资源受限的实时应用。

### **8. 不足与局限**
*   **理论保证的局限性**: 论文提供的长期覆盖率保证（Theorem 3.5）是**渐近性**的，缺乏在有限样本下的非渐近理论分析，这对于实际部署中的可靠性保证至关重要。
*   **对比实验的不足**: 如前所述，实验缺少一个**兼具“在线”和“隐私保护”特性的直接竞争对手**，使得性能优势的论证不够完全对等。
*   **非一致性分数的普适性**: 方法采用的标准非一致性分数（如绝对残差）虽然应用广泛，但在某些任务中可能导致预测集过于保守，效率不高。
*   **二进制询问的依赖性**: 方法的核心依赖于用户提供私有化的二进制反馈，这在某些应用中可能增加交互负担，或者如果用户全都不响应，系统将完全无法更新。

（完）
