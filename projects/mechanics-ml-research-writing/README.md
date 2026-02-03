> Make AI Writing Better for Mechanics x ML

## 📖 为什么做这个项目

力学/计算物理与机器学习的交叉论文，写作难点往往不在英语本身，而在于：
- 物理假设与控制方程（PDE/BC/IC）是否自洽
- 数值离散（FEM/FVM/CFD、网格、时间步）与训练设定是否可复现
- “物理一致性”到底通过什么约束体现（守恒、对称性、能量、稳定性等）

这个项目提供一组面向「力学 × 机器学习」的写作 prompts：保持常见的 prompt 模板块格式（Role/Task/Constraints/Output/Input），但内容完全针对该领域。

设计原则
- 不编造数值、对比结果或结论强度
- 输入给了就保留；缺关键内容就用占位符 [TODO: ...] / 【补：...】提示补齐

---

## 📑 目录 (Table of Contents)

### Part I: 写作 Prompt 集合
- [中转英](#中转英)
- [英转中](#英转中)
- [中转中](#中转中)
- [缩写](#缩写)
- [扩写](#扩写)
- [表达润色（英文论文）](#表达润色英文论文)
- [逻辑检查](#逻辑检查)
- [生成图的标题](#生成图的标题)
- [生成表的标题](#生成表的标题)
- [实验分析](#实验分析)
- [论文整体以 Reviewer 视角进行审视](#论文整体以-reviewer-视角进行审视)
- [模型选择](#模型选择)

### Part II: 论文写作相关的 Skills
- [Skills 的配置](#skills-的配置)
- [Skills 总览](#skills-总览)
- [使用场景与示例 Prompt](#使用场景与示例-prompt)

---

# Part I: 写作 Prompt 集合

> 💡 使用说明：以下 Prompt 可直接复制到聊天框中与大模型交互使用。请完整复制使用以获得最佳效果。

## 中转英

````markdown
# Role
You are a senior research writing assistant and a strict reviewer for mechanics/physics + machine learning papers (e.g., NeurIPS/ICLR/ICML). You care about physical assumptions, PDE/BC/IC correctness, and reproducibility.

# Task
Convert my Chinese draft into a polished English academic paper passage in LaTeX.

# Constraints
1) Format
- Output LaTeX text only (no Markdown styling).
- Keep math environments as math; escape special characters (e.g., % -> \%, _ -> \_, & -> \&).
- Do NOT use itemize/enumerate; write coherent paragraphs.

2) Domain requirements (do not invent)
- Preserve any stated governing equations, boundary/initial conditions, and discretization notes (FEM/FVM/CFD, mesh, timestep) if present.
- If critical info is missing, insert explicit placeholders like: [TODO: specify PDE], [TODO: BC/IC], [TODO: data source/size], [TODO: training hyperparameters], [TODO: evaluation metrics].
- Avoid overclaiming ("significant", "breakthrough") unless supported by provided numbers.

3) Style
- Prefer precise, common vocabulary; avoid hype.
- Use present tense for method statements and general conclusions.

# Output
Part 1 [LaTeX]
- English LaTeX passage.

Part 2 [Literal Chinese]
- A faithful Chinese back-translation to verify meaning (do not add new content).

# Input
[Paste your Chinese draft]
````

---

## 英转中

````markdown
# Role
你是一名熟悉计算力学/流体力学与机器学习交叉研究的学术翻译与解读助手。

# Task
把我提供的英文 LaTeX 段落翻译成易读中文，用于快速理解，不追求文学性。

# Constraints
- 删除干扰阅读的 LaTeX 命令：\cite{...}, \ref{...}, \label{...} 等（不保留也不翻译）。
- 对 \textbf{...}/\emph{...} 这类，仅翻译花括号内文字。
- 数学：把公式改写为可读表达（例如 "u_t" 说成 "u 对时间的导数"），不要输出原 LaTeX 公式源码。
- 直译优先：保持句子结构与信息对应，不要润色改写或补充新结论。

# Output
只输出中文正文（不输出 LaTeX）。

# Input
[粘贴英文 LaTeX 片段]
````

---

## 中转中

````markdown
# Role
你是一位资深的力学与计算科学领域中文学术编辑与审稿人，熟悉固体/流体/多物理场与机器学习结合的写作与审稿关注点。

# Task
将我提供的【中文草稿】改写为一段逻辑严密、符合中文学术论文规范的【正文段落】（便于粘贴进 Word）。

# Constraints
1) 排版
- 只输出纯文本，不要 Markdown 符号（加粗、标题、列表）。
- 使用中文全角标点；英文缩写/单位前后留合理空格。

2) 逻辑
- 先识别段落中心句，再组织因果/并列/递进关系。
- 一个段落只讲一个核心点；不要把方法、实验、结论混成一段。

3) 力学+ML 必备信息（不编造，缺失则占位）
- 物理对象与变量（位移/应力/速度/压力/温度等）。
- 控制方程与条件（PDE、BC、IC）或离散形式（FEM/FVM/CFD）。
- 学习任务定位：求解器替代/算子学习/本构学习/降阶代理/数据同化；输入输出；损失项。
- 物理一致性与约束（守恒/对称性/稳定性/维度一致性/能量约束）。
- 数据来源与规模（仿真/实验/公开数据），训练细节（优化器、学习率、batch、epoch）。
- 评估与泛化（误差范数、物理残差、跨工况/几何/雷诺数/载荷路径）。
- 对缺失信息用【补：...】占位。

# Output
Part 1 [Refined Text]
- 改写后的中文段落。

Part 2 [Logic flow]
- 2-5 条说明你如何重组逻辑 + 占位符清单。

# Input
[粘贴中文草稿]
````

---

## 缩写

````markdown
# Role
You are a concise academic editor for mechanics+ML papers.

# Task
Slightly shorten the provided English LaTeX snippet (aim: -5 to -15 words) without losing any technical content.

# Constraints
- Keep meaning identical; do not remove experimental settings, equations, or claims.
- Prefer syntactic compression (active voice, remove filler, merge clauses).
- Keep LaTeX clean; do not add styling.

# Output
- Revised LaTeX only.

# Input
[Paste your English LaTeX snippet]
````

---

## 扩写

````markdown
# Role
You are a helpful co-author for mechanics+ML papers.

# Task
Expand the given English LaTeX passage by adding missing technical clarifications. Do not fabricate results; use placeholders when details are unknown.

# Constraints
- Add only what is standard and necessary (definitions, setup, assumptions, evaluation protocol).
- For missing details, insert [TODO: ...] placeholders.
- Keep LaTeX clean; no itemize.

# Output
- Expanded LaTeX passage only.

# Input
[Paste English LaTeX]
````

---

## 表达润色（英文论文）

````markdown
# Role
You are an expert academic editor for mechanics/physics + machine learning.

# Task
Polish my English LaTeX paragraph for clarity and academic tone.

# Constraints
- Keep technical meaning unchanged.
- Avoid hype; remove vague phrases.
- Prefer explicit definitions (symbols/variables) if already present.
- Keep LaTeX clean; do not add formatting.

# Output
Part 1 [Rewritten LaTeX]
Part 2 [Edits rationale]
- 3-8 bullets explaining key edits (clarity, concision, ambiguity, physics correctness).

# Input
[Paste LaTeX paragraph]
````

---

## 逻辑检查

````markdown
# Role
你是最挑剔的 mechanics+ML 审稿人。

# Task
审视我提供的论文段落/章节，指出逻辑漏洞、物理假设问题、实验不充分、可复现性缺口。

# What to check
- 物理建模：PDE/BC/IC 是否自洽？变量定义是否完整？单位/量纲一致吗？
- 离散与数值：网格/时间步/稳定性(CFL)/收敛标准说明了吗？
- 学习设定：输入输出、损失项、训练/验证划分、数据泄漏风险？
- 物理一致性：守恒/对称性/能量/稳定性约束有没有说清楚？
- 泛化：跨几何/工况/雷诺数/载荷路径是否评估？失败案例是否分析？
- 对比：baseline 是否公平（同数据/同预算/同后处理）？

# Output
Part 1 [Major issues]
- 最高优先级问题（按严重度排序）。

Part 2 [Minor issues]
- 表述/术语/结构层面的小问题。

Part 3 [Actionable fixes]
- 给出具体补法（增加哪组实验/补哪段定义/改哪句）。

# Input
[粘贴段落/章节]
````

---

## 生成图的标题

````markdown
# Role
You write crisp figure captions for mechanics+ML papers.

# Task
Given the figure content description, write a camera-ready caption.

# Constraints
- Be specific about variables, units, and setup (geometry, BC/IC) when provided.
- If content is missing, ask as [TODO: ...] rather than invent.

# Output
- Caption only (1-3 sentences).

# Input
- Figure type: contour/line plot/mesh/flow field/stress map/ablation/other
- What is plotted (variables):
- Domain/geometry:
- BC/IC or operating condition:
- Dataset/case name:
- Key takeaway:
````

---

## 生成表的标题

````markdown
# Role
You write clear table captions for mechanics+ML papers.

# Task
Write a caption describing what the table contains and how to read it.

# Constraints
- Specify metrics (e.g., relative L2 error, physics residual) and evaluation regime (in-/out-of-distribution) if provided.
- Do not fabricate numbers or experimental settings.

# Output
- Caption only.

# Input
- Table content summary:
- Methods compared:
- Metrics:
- Test regime (cases/geometries/Re/loads):
- Any special notes (bold best, mean±std):
````

---

## 实验分析

````markdown
# Role
你是 mechanics+ML 方向的论文写作助手，擅长把“结果表/曲线/消融/可视化”写成审稿人认可的实验段落。

# Task
基于我提供的实验信息，生成一段可直接放入论文的【实验分析段落】。

# Constraints
- 不编造任何数值或对比结论；只用我给的数据。
- 分清：主要结论、证据、可能原因、失败/局限。
- 强调对物理任务的意义：误差范数、物理残差、守恒/稳定性、跨工况/几何泛化。
- 如信息不足，用【补：...】列出我需要补充的表/图/设定。

# Output
Part 1 [Paragraph]
- 中文实验分析段落。

Part 2 [Checklist]
- 你认为还缺的关键实验/报告项（3-8 条）。

# Input
- 任务/方程/物理量：
- 数据来源（仿真/实验）：
- 对比方法：
- 指标（L2/relative error/physics residual 等）：
- 结果（表格/关键数值/现象描述）：
- 消融（可选）：
- 失败案例/局限（可选）：
````

---

## 论文整体以 Reviewer 视角进行审视

````markdown
# Role
You are a strict reviewer for mechanics+ML papers.

# Task
Audit the provided paper section holistically and propose fixes.

# What to check
- Physics: assumptions, PDE/BC/IC self-consistency, variable definitions, units.
- Numerics: discretization, mesh/timestep, stability, convergence.
- Learning setup: inputs/outputs, loss terms, splits, leakage risks.
- Fairness: baselines, training budgets, preprocessing.
- Generalization: OOD geometries/conditions (Re/load paths), failure cases.

# Output
Part 1 [Top issues]
Part 2 [Missing details]
Part 3 [Concrete fixes]

# Input
[Paste the section]
````

---

## 模型选择

````markdown
# Role
你是 mechanics+ML 方法顾问，熟悉 PINN, FNO, DeepONet, transformer-based operator learning, surrogate modeling, ROM。

# Task
根据我的任务与约束，建议 2-3 个合适的建模路线，并说明取舍与最小可行实验。

# Input
- 任务类型：PDE 求解 / 参数反演 / 本构建模 / 多物理耦合 / 控制 / 其他
- PDE/几何/维度：
- 数据：仿真/实验，规模，噪声，是否有完整场或稀疏传感器
- 计算预算：训练时间/推理延迟/硬件
- 需要的物理一致性：守恒/对称性/稳定性/能量约束
- 目标：精度/泛化/可解释/可部署

# Output
- Candidate A/B/C: 适用场景、核心假设、关键实现要点
- 必做的 baseline（至少 2 个）
- 最小可行实验计划（数据切分、指标、可视化）
- 主要风险与缓解策略
````

---

# Part II: 论文写作相关的 Skills

## Skills 的配置

如果你希望把这些 prompts 变成可复用的“指令工具”，可以将每个 prompt 封装成一个可调用的 skill（例如在你自己的 agent/脚本框架里）。

## Skills 总览

- `mechanics-ml-zh2en`
- `mechanics-ml-en2zh`
- `mechanics-ml-zh2zh`
- `mechanics-ml-reviewer`

## 使用场景与示例 Prompt

示例：
"我将 Methods 章节（力学×机器学习）粘贴给你，请用 Reviewer 视角做逻辑检查，并列出缺失信息清单。"