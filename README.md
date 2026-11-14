# 正交宇宙物理学

以 Greg Egan《正交》（*Orthogonal*）三部曲的官方物理注记为基础，面向物理学研究生的中文 LaTeX 整理稿。内容涉及黎曼时空、运动学、波动、电磁学、热力学、量子力学、广义相对论，以及数学工具与补充推导。

这是非官方翻译与整理项目，并非 Greg Egan 授权出版物；译文和补充说明仍需对照原文校订。

## 阅读

- [阅读 PDF](main.pdf)（当前版本 346 页）。
- [官方介绍与物理注记](https://www.gregegan.net/ORTHOGONAL/ORTHOGONAL.html)。
- [章节写作与公式规范](chapters/GUIDE.md)。

三部小说为 *The Clockwork Rocket*、*The Eternal Flame*、*The Arrows of Time*。

## 目录

```text
tex_orthogonal/
  README.md
  .gitignore
  main.tex          # 唯一编译入口，组织正文与三份附录
  preamble.tex      # 文档类、宏包、数学宏和页面样式
  main.pdf          # 保留的阅读版本
  chapters/         # 22 份正文/附录片段及写作规范
  images/           # 122 张被 LaTeX 正文实际引用的插图
```

章节按 `main.tex` 的 `\input` 顺序组合；文件名中的 `a`、`b`、`c` 等表示同一主题的分段，不应单独编译。正文从导论、加减号与对偶勾股定理进入运动、波动、电磁学、热力学、量子力学、引力和世界设定，最后附术语表及三份附录。

## 编译

推荐使用 TeX Live（本机验证环境为 TeX Live 2026），需要 XeLaTeX、`ctexbook` 及导言区列出的宏包。必须在本目录执行，以便解析章节和图片的相对路径。

```sh
latexmk -xelatex -interaction=nonstopmode -halt-on-error main.tex
```

没有 `latexmk` 时，连续运行三次：

```sh
xelatex -interaction=nonstopmode -halt-on-error main.tex
xelatex -interaction=nonstopmode -halt-on-error main.tex
xelatex -interaction=nonstopmode -halt-on-error main.tex
```

`preamble.tex` 当前使用 `fontset=windows`，依赖 Windows 中文字体。Linux/macOS 或 GitHub Actions 编译前，应改为适合环境的字体配置，例如安装 Fandol 字体后使用 `fontset=fandol`。本次整理未修改原有字体与正文排版。

删除可再生的辅助文件：

```sh
latexmk -c main.tex
```

不要使用 `latexmk -C`，它还会删除保留的 PDF。整理后已在临时目录完整重编译，成功生成 346 页 PDF，源目录未留下编译缓存，现有 `main.pdf` 未被覆盖。

当前文稿存在字体替代、列表宽度、部分盒子溢出/不足，以及重复公式 PDF 链接锚点（`Object @equation... already defined`）警告。重复锚点可能使公式链接跳到错误位置，需在后续排版校订中检查；编译成功不代表已经完成出版级排版与内容审校。本次未修改正文、公式编号或原有排版。

## 原文与网站素材

原始 HTML、英文 Markdown、完整的 128 张图片、图片 URL 清单及抓取/转换脚本已迁移至相邻的 `../html_orthogonal/`，不属于本 LaTeX 项目的编译依赖。网站目录目前是素材工作区，尚不是可发布网站。

如果只上传本目录，仍可独立编译，但不包含上述原文档案。若希望保存两个子项目的关联，可在同一 GitHub 仓库中并列放置 `tex_orthogonal/` 和 `html_orthogonal/`。

本次清理删除了编译日志与缓存、重复的 `text/` 和纯文本转换脚本；仅供网站或原文参考的 6 张图片已在网站素材中保留。

## 上传 GitHub

本目录尚未初始化 Git 仓库，也未关联远程仓库。本次未执行提交或推送。在确认下节版权事项后，可选择：

- **独立仓库**：将本目录作为仓库根目录，提交源文件、图片、README 与 `main.pdf`。
- **联合仓库**：将两个子项目放在同一仓库下，分别保留各自的 README 与忽略规则。

`.gitignore` 已排除编译缓存与系统临时文件，保留 `main.pdf`。后续可改为在 GitHub Releases 分发 PDF，以减少频繁更新二进制文件造成的仓库增长。GitHub Pages 只提供静态网站托管，不会自动编译 LaTeX。

## 来源与版权

原始英文文字和插图来自 [Greg Egan 官方网站](https://www.gregegan.net/ORTHOGONAL/ORTHOGONAL.html)。原网页标注 **Copyright © Greg Egan. All rights reserved.** 本地素材中没有记录公开再分发或译文发布的授权。

署名、非商业使用以及“学习研究用途”不自动构成全文翻译、图片或网页快照公开发布的许可。公开 GitHub 仓库、PDF 和 GitHub Pages 前，请确认适用的许可或取得必要授权；无法确认时，先使用私人仓库管理素材，并且不要发布包含这些内容的公开 Pages 网站。

项目没有添加 MIT、CC 或其他覆盖全仓库的开源许可证，避免错误授权第三方内容。后续如为自行编写的代码选择许可证，应明确排除原作文字、插图及其翻译，并区分原文翻译和原创补充说明。
