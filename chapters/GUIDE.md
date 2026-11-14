# 编译与写作规范（供各章撰写使用）

## 0. 任务性质
把 Greg Egan 官网 `ORTHOGONAL/` 下英文物理注记，编译为**中文 LaTeX 章节**，
面向**物理学专业研究生**。要求：忠实、严谨、硬核；不臆造原文没有的结论；
公式必须用 LaTeX 正确排版；正文流畅的中文，术语首次出现时在括号内保留英文原词。

## 1. 源文件
- 英文正文（含公式）的转换稿已迁移至相邻网站项目的 `../html_orthogonal/sources/md/`，
  例如 `../html_orthogonal/sources/md/04__EMExtra.md`。本规范下文的 `md/` 均指该目录。
- 原始 HTML 在 `../html_orthogonal/sources/raw/`。优先使用 Markdown 阅读；
  公式、上下标、图注或内容覆盖有疑问时，应回查原始 HTML 或官方网页，而不是仅依赖转换稿。
- 如果只克隆 LaTeX 仓库，原文档案可能不在本地，请先取得网站素材工作区或查看官网。
- 原文中的公式已被转成近 LaTeX 记法。注意其常见"毛刺"，需你在排版时修正：
  - `–` / `—`（连字符）出现在数学里时一律改为减号 `-`。
  - `\sqrt[...]` 或 `\sqrt(...)` 一律改为正确形式 `\sqrt{...}`。
  - 下标/上标有时被压平，如 `vx` 其实是 `v^{x}`、`∂x2A` 是 `\partial_x^2 A`；
    请按物理含义还原为规范的上下标。
  - `\emph{...}`（斜体变量）与 `\textbf{...}`（粗体矢量）来自原文强调，
    正文里应改写为数学模式，如 `\emph{x}` → `$x$`，`\textbf{v}` → `$\mathbf{v}$`。
  - 图片标记 `@@IMG::文件名::英文alt@@`（见第 3 节）。

## 2. LaTeX 环境与可用宏
- 只用 `ctexbook` 提供的章节命令。**不要**写导言区、`\begin{document}`、`\documentclass`。
- 结构命令：`\chapter{...}`、`\section{...}`、`\subsection{...}`、`\subsubsection{...}`。
- 已定义的宏（可直接用）：
  - `\orthofig[宽度]{图片路径}{中文图注}`：插图（默认宽 0.62\textwidth）。**所有插图都用它。**
  - `\inlinefig[宽度]{图片路径}{说明}`：不浮动的居中图（少用）。
  - 中文提示框：`\begin{keybox}[标题] ... \end{keybox}`、`\begin{notebox}[标题] ... \end{notebox}`。
  - 常用符号宏：`\wms`=ω_m，`\ii`=i（虚数单位），`\ee`=e，`\half`=1/2，`\dd`=d，
    `\Riem`=R 下标、`\Lor`=L 下标；粗体矢量：`\bA \bE \bB \bF \bj \bk \bp \bv \bu \bw \bx \be \bP \bq \bzero`。
  - 算符：`\Tr \diag \sgn \Span \rank`（已定义 `\DeclareMathOperator`）。
- 数学包已载入：amsmath、amssymb、amsfonts、mathrsfs、bm。可直接用 `\begin{equation}`、
  `align`、`gather`、`cases`、`pmatrix`、`\mathbb`、`\mathcal`、`\mathscr`、`\bm` 等。
- 行内公式用 `$...$`，独立公式用 `\[ ... \]` 或 `equation` 环境。**不要**使用 `$$...$$`
  （会把源文件里的 `$$...$$` 改写为 `\[ ... \]` 或 `equation`）。

## 3. 插图规则（重要）
源里每个 `@@IMG::ref::英文说明@@` 都要转成一张插图。
图片路径换算规则：
1. 若 `ref` 中含 `/`（跨目录引用，如 `../04/003.png` 或 `02/007.png`）：
   去掉开头的 `../`，把 `/` 全部换成 `__`，得到文件名。例：`../04/003.png` → `images/04__003.png`。
2. 否则：取当前 md 文件名第一个 `__` 之前的部分加 `__` 作前缀。
   例：在 `md/02__MotionExtra.md` 中，`001.png` → `images/02__001.png`。
   在 `md/E1__ClockworkRocketExcerpt.md` 中，`StarTrails.png` → `images/E1__StarTrails.png`。
   在 `md/ORTHOGONAL.md` 中（无 `__`），`Orthogonal200.gif` → `images/Orthogonal200.gif`。
把英文 alt 翻译成简洁、准确的中文图注，写成：
```latex
\orthofig{images/02__001.png}{洛伦兹时空中的方向}
```
若某图是纯数学公式截图（alt 为公式名），图注写"图：<公式含义>"即可，正文仍应把该公式
用 LaTeX 完整重写一遍。

## 4. 内容与写法要求
- **完整覆盖**：你负责范围内原文的每一节（`###`/`####`）都要有对应内容，
  不能遗漏主题。原文冗长的口语化叙述可压缩，但**所有定义、结论、公式、方程编号、
  数值与物理量关系必须保留**。凡原文给出推导的，要给出关键步骤，不能只写结论。
- **忠实**：不添加原文没有的物理结论；若你知道的标准物理知识有助于解释，可简要补充，
  但需明确是补充说明。
- **术语**：首次出现的中文术语后括注英文，如“黎曼矢量波方程（Riemannian Vector Wave equation, RVW）”。
- **公式编号**：原文用 (RVW)、(1)、(2) 之类标签，请沿用这些标签，
  用 `\begin{equation} ... \tag{RVW} \end{equation}` 或 `\tag{...}`。
- **原文中的方括号补充说明**（如 `[...]` 段落）属于正文，要译出。
- **参考文献**：原文 "References" 段落，用无序列表列出（保留作者、标题；URL 可省或保留）。
- 每章开头写一段 2–4 句的中文导语，说明本章要解决的问题。

## 5. 章节维护
- 修改时明确对应的输入 md 文件（可含**行号范围**）与输出 tex 文件路径。
- 同一章节的续篇文件只写 `\section`/`\subsection`，
  以便接在上一文件之后。
- 输出为**完整可编译**的 LaTeX 片段，写入指定路径。写完后用 Read 复查一遍：确认
  环境配对（`\begin`/`\end`）、括号平衡、图片路径存在（见 `images/` 目录）。
- 调整全书宏、字体或章节顺序时，集中修改 `preamble.tex` 或 `main.tex`，并验证全书编译。

## 6. 数学记号约定（全书统一）
- 时空坐标 `(x,y,z,t)`；矢量分量用上标 `v^x, v^y, v^z, v^t`。
- 黎曼度规 `(+,+,+,+)`；洛伦兹度规 `(-,+,+,+)`（官网部分处用 `(+,-,-,-)`，保留原文所标）。
- 质量频率 `\wms`（=mc²/ħ）。
- 黎曼标量波方程（RSW）：`\partial_x^2 A+\partial_y^2 A+\partial_z^2 A+\partial_t^2 A+\wms^2 A=0`。
- 黎曼矢量波方程（RVW）在此基础上加横波条件 `\partial_x A^x+\partial_y A^y+\partial_z A^z+\partial_t A^t=0`。
- 电磁场张量 `F^{ab}=\partial^a A^b-\partial^b A^a`；四维电流 `j=\rho u`。
