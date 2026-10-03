![婚礼学报 demo](https://github.com/user-attachments/assets/57f24fee-93a2-42c4-ad3c-3f65371d2fbf)

# Journal of Love · 婚礼学报 LaTeX 模板

![LaTeX](https://img.shields.io/badge/LaTeX-XeLaTeX-008080?logo=latex&logoColor=white)
![Language](https://img.shields.io/badge/Language-%E4%B8%AD%E6%96%87%20%7C%20English-4b8bbe)
![Output](https://img.shields.io/badge/Output-2%20pages-9e7bb5)

**把一段私人关系，排版成一篇 SCI 期刊论文。** / *Typeset your love story as a journal article.*

用 LaTeX 复刻 Elsevier 期刊首页版式的婚礼请柬 / 恋爱官宣模板：期刊刊头、卷期页码、ARTICLE INFO 与 ABSTRACT 分栏、通讯作者脚注、DOI、投稿—修回—接收日期，以及一枚手绘的 Cupid 出版社标志。

A LaTeX template that turns a wedding invitation or a relationship announcement into an Elsevier-style journal article — masthead, volume/issue/pages, split ARTICLE INFO & ABSTRACT panel, corresponding-author footnote, DOI, received/revised/accepted dates, and a hand-drawn Cupid publisher mark.

[中文文档](#中文文档) · [English Documentation](#english-documentation)

---

## 中文文档

### 这是什么

一份**可以直接改的 LaTeX 模板**：把两个人之间的故事写成一篇结构完整的研究论文。

- **两种场景**：`love_announcement.tex`（恋爱官宣）与 `wedding_journal.tex`（婚礼学报 / 请柬）。
- **唯一数据源**：所有人名、日期、地点都集中在 `couple-info.tex`，改一处，两份文档同步更新。
- **仿 SCI 版式**：页面 210 × 280 mm、双栏正文、页眉页脚、三线表、图注小字，全部按真实期刊页面用绝对坐标（bp）复刻。
- **中英混排**：正文同时使用西文与中文字体，`fontspec` + `xeCJK` 分别控制。
- **照片可选**：把照片放进 `assets/`，文件不存在时自动画一个灰色占位框，不会编译报错。

#### 关于 520 和 1314

模板里的期刊元数据都埋了数字梗：**520** = 我爱你，**1314** = 一生一世。所以卷号是 1314、期号是 520、页码从 520 开始、DOI 是 `10.1314/jlove.520.521`，版权行写着 *All hearts reserved*。不喜欢可以全部改掉（见「自定义」）。

### 效果预览

| 恋爱官宣版 | 婚礼学报版 |
| :---: | :---: |
| [![love announcement](preview/love-announcement-p1.png)](preview/love-announcement-p1.png) | [![wedding journal](preview/wedding-journal-p1.png)](preview/wedding-journal-p1.png) |
| `love_announcement.tex` | `wedding_journal.tex` |

仓库里已附带一份编译成品 [Journal of Love.pdf](Journal%20of%20Love.pdf)（恋爱官宣版，共 2 页）。

### 文件结构

```text
Journal-of-Wedding-Latex-Template/
├── couple-info.tex          # ★ 唯一需要修改的文件
├── love_announcement.tex    # 恋爱官宣版
├── wedding_journal.tex      # 婚礼学报版
├── journaloflove-sci.sty    # 版式与样式（仿 SCI 首页 + 双栏正文）
├── preview/                 # README 预览图
├── assets/                  # 照片目录（仓库未包含，需要自己新建）
│   ├── announcement-photo.jpg
│   └── wedding-photo.jpg
└── Journal of Love.pdf      # 已编译的示例成品
```

### 环境要求

| 项目 | 要求 |
| --- | --- |
| TeX 发行版 | TeX Live / MacTeX（**建议完整版**，需要 `xeCJK`、`titlesec` 等；实测 TeX Live 2025） |
| 编译引擎 | **XeLaTeX（必须）**，不能用 pdfLaTeX / LuaLaTeX |
| 编译次数 | 至少 **2 次**（首页用 `remember picture` 绝对定位，需第二遍才能定稳） |
| 宏包 | `fontspec`、`xeCJK`、`geometry`、`xcolor`、`tikz`、`graphicx`、`multicol`、`amsmath`、`amssymb`、`mathtools`、`booktabs`、`tabularx`、`array`、`caption`、`fancyhdr`、`titlesec`、`hyperref`、`microtype`、`enumitem`、`etoolbox`、`ragged2e`（以及文档类 `extarticle`） |

### 字体（最容易踩坑的一步）

`journaloflove-sci.sty` 在开头指定了 6 种字体。**缺少字体时 XeLaTeX 会直接报错中止**：

```
! Package fontspec Error: The font "Charis SIL" cannot be found.
```

| 字体 | 用途 | 来源 | 授权 | TeX Live 自带 |
| --- | --- | --- | --- | --- |
| Charis SIL | 正文西文 / 数学外文 | [software.sil.org/charis](https://software.sil.org/charis/) | SIL OFL 1.1 | ✅（TTF 在 `fonts/truetype/SIL/charissil/`） |
| Universalis ADF Std | 无衬线（标志、页眉小字） | [CTAN: universalis](https://ctan.org/pkg/universalis) | GPL v2+（含字体例外） | ✅ |
| Liberation Mono | 等宽（占位框里的路径文字） | [liberationfonts](https://github.com/liberationfonts/liberation-fonts) | SIL OFL 1.1 | ❌ |
| Noto Serif CJK SC | 中文正文 | [notofonts/noto-cjk](https://github.com/notofonts/noto-cjk) | SIL OFL 1.1 | ❌ |
| Noto Sans CJK SC | 中文无衬线 | 同上 | SIL OFL 1.1 | ❌ |
| Noto Sans Mono CJK SC | 中文等宽 | 同上 | SIL OFL 1.1 | ❌ |

**安装字体**：下载后双击安装即可（macOS 用「字体册 / Font Book」，Windows 右键“为所有用户安装”，Linux 放到 `~/.local/share/fonts/` 后执行 `fc-cache -f`）。

**不想装字体？** 用下面的片段整体替换 `journaloflove-sci.sty` 中第 40–46 行（从 `\defaultfontfeatures{Ligatures=TeX}` 到 `\setCJKmonofont` 那 7 行）。这段代码会让模板自动挑选本机存在的字体，**已在 TeX Live 2025 实测通过**（两份文档各 2 页，零报错）：

```latex
% ---- 字体自动回退：缺字体时也不会编译失败 ----
\defaultfontfeatures{Ligatures=TeX}

\IfFontExistsTF{Charis SIL}
  {\setmainfont{Charis SIL}}
  % TeX Live 自带 CharisSIL 的 TTF，可以直接按文件名调用
  {\setmainfont{CharisSIL-Regular.ttf}[
     BoldFont=CharisSIL-Bold.ttf,
     ItalicFont=CharisSIL-Italic.ttf,
     BoldItalicFont=CharisSIL-BoldItalic.ttf]}

\IfFontExistsTF{Universalis ADF Std}
  {\setsansfont{Universalis ADF Std}}
  {\setsansfont{Hiragino Sans GB}}
\IfFontExistsTF{Liberation Mono}
  {\setmonofont{Liberation Mono}}
  {\setmonofont{Menlo}}

\IfFontExistsTF{Noto Serif CJK SC}
  {\setCJKmainfont[AutoFakeBold=2.3,AutoFakeSlant=.16]{Noto Serif CJK SC}}
  {\setCJKmainfont[AutoFakeBold=2.3,AutoFakeSlant=.16]{Songti SC}}
\IfFontExistsTF{Noto Sans CJK SC}
  {\setCJKsansfont{Noto Sans CJK SC}}
  {\setCJKsansfont{PingFang SC}}
\IfFontExistsTF{Noto Sans Mono CJK SC}
  {\setCJKmonofont{Noto Sans Mono CJK SC}}
  {\setCJKmonofont{Menlo}}
```

如果想在别的系统上用，把回退字体换成对应平台的常见字体即可：

| 平台 | 中文正文回退 | 中文无衬线回退 | 等宽回退 |
| --- | --- | --- | --- |
| macOS | `Songti SC` | `PingFang SC` | `Menlo` |
| Windows | `SimSun` | `Microsoft YaHei` | `Consolas` |
| Linux | `Noto Serif CJK SC` / `Source Han Serif SC` | `Noto Sans CJK SC` | `Noto Sans Mono` |

> 小技巧：临时验证某个字体名是否可用，可以单独编译一个最小文档，看日志里有没有 `not loadable`。
> 最省事的做法仍是装齐上表字体，版式才能 100% 还原。

### 编译

```bash
# 恋爱官宣版
xelatex love_announcement.tex
xelatex love_announcement.tex     # 再跑一遍，首页绝对定位与超链接才准确

# 婚礼学报版
xelatex wedding_journal.tex
xelatex wedding_journal.tex
```

用 `latexmk` 一步到位：

```bash
latexmk -xelatex -interaction=nonstopmode wedding_journal.tex
```

输出为 `wedding_journal.pdf` / `love_announcement.pdf`（各 2 页：第 1 页是期刊首页，第 2 页是正文续页与参考文献）。

### 自定义

#### 1. 只改 `couple-info.tex`

| 变量 | 含义 | 官宣版 | 婚礼版 |
| --- | :--- | :---: | :---: |
| `\PartnerA`、`\PartnerB` | 两位主角的名字 | ✅ | ✅ |
| `\FirstMeetingDate` | 初次相遇 / 观察起点 | ✅ | ✅ |
| `\RelationshipDate` | 确认关系日期 | ✅ | ✅ |
| `\AnnouncementDate` | 公开（官宣）日期 | ✅ | — |
| `\WeddingDate` | 婚礼日期 | — | ✅ |
| `\WeddingCity`、`\WeddingVenue` | 城市与场地 | — | ✅ |
| `\ContactEmail` | 通讯邮箱 | ✅ | ✅ |
| `\DaysObserved`、`\SharedTrips`、`\SharedMeals` | 观察天数 / 共同旅行 / 共同用餐（正文与描述统计表用） | — | ✅ |
| `\FutureHorizon` | 随访期（默认「终身」） | ✅ | ✅ |
| `\OurMotto` | 备用签名句，**当前模板未引用**，可自行插到正文里 | — | — |

#### 2. 改标题、摘要、期刊信息

打开 `love_announcement.tex` / `wedding_journal.tex` 顶部的 `\setJOL...` 命令即可：

| 命令 | 作用 |
| --- | --- |
| `\setJOLTitle` | 论文标题（大字号，建议不超过 2 行） |
| `\setJOLAuthors` | 作者行，`\textsuperscript{a}`、`\textsuperscript{a,*}` 是单位与通讯标记 |
| `\setJOLAffilA` / `\setJOLAffilB` | 单位（`B` 为空则不显示） |
| `\setJOLKeywords` | 关键词，用 `\\` 换行 |
| `\setJOLAbstract` | 摘要（建议控制在 200 词以内，太长会溢出首页固定区域） |
| `\setJOLCoverSub` / `\setJOLCoverIssue` | 右上角迷你封面上的栏目标签与卷期 |
| `\setJOLMeta` | 顶部刊名行（同时会更新右侧页眉） |
| `\setRunningAuthor` | 页眉左侧的作者名 |
| `\setJOLCorrespondence`、`\setJOLEmail` | 通讯作者信息与邮箱 |
| `\setJOLDOI`、`\setJOLReceived`、`\setJOLOnline`、`\setJOLCopyright` | 页脚 DOI、日期戳与版权行 |
| `\setJOLFootnoteText` | 首页脚注（编号 ¹ 的那段） |

#### 3. 正文里的排版工具

| 命令 / 环境 | 说明 |
| --- | --- |
| `\begin{JOLtable}{标题} … \end{JOLtable}` | 期刊风格小号三线表（内部用 `tabularx`，表宽 = 栏宽） |
| `\JOLphoto{路径}{图注}` | 插图；文件不存在时自动画灰色占位框并显示路径 |
| `\JOLsource{来源}` | 图下小字 Source 注 |
| `\makeJOLfrontmatter` | 生成首页整套刊头版面，放在 `\begin{document}` 之后第一行 |

#### 4. 放照片

新建 `assets/` 目录，按下面的文件名放照片即可（其它文件名也行，改 `\JOLphoto` 的路径参数即可）：

- 官宣版：`assets/announcement-photo.jpg`
- 婚礼版：`assets/wedding-photo.jpg`

### 常见问题

**1. `! Package fontspec Error: The font "Charis SIL" cannot be found.`**
字体没装。见上面「字体」章节，或直接套用自动回退片段。

**2. 页眉 / 首页元素错位、标题和摘要重叠**
首页刊头是按参考期刊页面用**绝对坐标（bp）**画出来的，各区域高度固定。标题超过 2 行、摘要过长、作者行太长都会挤出边界。缩短文案即可，或微调 `journaloflove-sci.sty` 里 `\JOLPutText` 的坐标参数（前两个数字依次是「距左边」和「距上边」的 bp 值）。

**3. 中文显示成方框或空白**
中文（CJK）字体没装上，见「字体」章节。

**4. 超链接、定位不对**
只编译了一次。XeLaTeX 需要跑两遍。

**5. 页码不是从 1 开始**
模板刻意从 **520** 开始（数字梗）。改 `\setcounter{page}{520}` 即可。

**6. 图片 / 表格跑到奇怪的位置**
它们都是 `[t]` 浮动体，会排在栏顶。这是期刊排版的正常行为。

**7. 想在 Overleaf 上用**
上传整个项目 → 把编译器设为 **XeLaTeX** → 若报缺字体，套用上面的自动回退片段。

### 许可证与声明

- 本仓库**尚未声明许可证**，使用前请先与作者确认；建议补充一个（代码可用 MIT，文档可用 CC BY 4.0）。
- 所用字体各自遵循其原授权：Charis SIL、Liberation、Noto CJK 为 **SIL OFL 1.1**，Universalis ADF Std 为 **GPL v2+（含字体例外）**。分发含嵌入字体的 PDF 时请遵守相应条款。
- 版式是对学术期刊页面样式的**风格致敬**，请仅用于私人纪念用途，不要用于冒充真实出版物或商业出版。

### 致谢

感谢所有见证这段关系的人。如果这个模板帮你写完了属于自己的那篇“论文”，欢迎点个 Star ⭐。

---

## English Documentation

### What is this

A **ready-to-edit LaTeX template** that writes the story of two people as a full research article.

- **Two occasions**: `love_announcement.tex` (relationship announcement) and `wedding_journal.tex` (wedding invitation / wedding issue).
- **Single source of truth**: every name, date and place lives in `couple-info.tex` — edit once, both documents update.
- **Journal-grade layout**: 210 × 280 mm page, two-column body, running head/foot, three-line tables, small-type figure captions — all reconstructed at the exact absolute coordinates (bp) measured from a real journal page.
- **Bilingual typesetting**: Latin and CJK fonts are controlled separately through `fontspec` + `xeCJK`.
- **Photos are optional**: drop images into `assets/`; if a file is missing, a grey placeholder is drawn instead of failing the build.

#### About 520 and 1314

The journal metadata is a running pun: in Chinese, **520** sounds like “I love you” and **1314** like “forever”. Hence volume 1314, issue 520, first page 520, DOI `10.1314/jlove.520.521`, and a copyright line reading *All hearts reserved*. All of it is editable (see Customization).

### Preview

| Relationship announcement | Wedding issue |
| :---: | :---: |
| [![love announcement](preview/love-announcement-p1.png)](preview/love-announcement-p1.png) | [![wedding journal](preview/wedding-journal-p1.png)](preview/wedding-journal-p1.png) |
| `love_announcement.tex` | `wedding_journal.tex` |

A compiled sample — [Journal of Love.pdf](Journal%20of%20Love.pdf), the announcement version, 2 pages — ships with the repository.

### Repository layout

```text
Journal-of-Wedding-Latex-Template/
├── couple-info.tex          # ★ the only file you need to edit
├── love_announcement.tex    # relationship-announcement issue
├── wedding_journal.tex      # wedding issue
├── journaloflove-sci.sty    # layout & styling (journal front page + two-column body)
├── preview/                 # README preview images
├── assets/                  # photo folder (not in the repo — create it yourself)
│   ├── announcement-photo.jpg
│   └── wedding-photo.jpg
└── Journal of Love.pdf      # sample compiled output
```

### Requirements

| Item | Requirement |
| --- | --- |
| TeX distribution | TeX Live / MacTeX — a **full** install is recommended (`xeCJK`, `titlesec`, …); tested on TeX Live 2025 |
| Engine | **XeLaTeX (required)** — pdfLaTeX and LuaLaTeX will not work |
| Passes | At least **2** (the front page uses `remember picture` absolute positioning, which settles on the second pass) |
| Packages | `fontspec`, `xeCJK`, `geometry`, `xcolor`, `tikz`, `graphicx`, `multicol`, `amsmath`, `amssymb`, `mathtools`, `booktabs`, `tabularx`, `array`, `caption`, `fancyhdr`, `titlesec`, `hyperref`, `microtype`, `enumitem`, `etoolbox`, `ragged2e`, plus the `extarticle` class |

### Fonts (the most likely stumbling block)

`journaloflove-sci.sty` asks for 6 fonts. **If one is missing, XeLaTeX aborts:**

```
! Package fontspec Error: The font "Charis SIL" cannot be found.
```

| Font | Used for | Source | License | Ships with TeX Live |
| --- | --- | --- | --- | --- |
| Charis SIL | Latin body text & math | [software.sil.org/charis](https://software.sil.org/charis/) | SIL OFL 1.1 | ✅ (`fonts/truetype/SIL/charissil/`) |
| Universalis ADF Std | Sans (logo, headers, small print) | [CTAN: universalis](https://ctan.org/pkg/universalis) | GPL v2+ with font exception | ✅ |
| Liberation Mono | Monospace (placeholder path text) | [liberationfonts](https://github.com/liberationfonts/liberation-fonts) | SIL OFL 1.1 | ❌ |
| Noto Serif CJK SC | CJK body text | [notofonts/noto-cjk](https://github.com/notofonts/noto-cjk) | SIL OFL 1.1 | ❌ |
| Noto Sans CJK SC | CJK sans | same | SIL OFL 1.1 | ❌ |
| Noto Sans Mono CJK SC | CJK monospace | same | SIL OFL 1.1 | ❌ |

**Installing**: download and install at OS level (Font Book on macOS, right-click → “Install for all users” on Windows, or `~/.local/share/fonts/` + `fc-cache -f` on Linux).

**Prefer not to install anything?** Replace the 7 lines at `journaloflove-sci.sty` lines 40–46 (from `\defaultfontfeatures{Ligatures=TeX}` through `\setCJKmonofont`) with the snippet below. It picks whichever font is actually available on your machine, and has been **tested on TeX Live 2025** (both documents compile, 2 pages each, zero errors):

```latex
% ---- Automatic font fallback: never fails on a missing font ----
\defaultfontfeatures{Ligatures=TeX}

\IfFontExistsTF{Charis SIL}
  {\setmainfont{Charis SIL}}
  % TeX Live bundles CharisSIL TTFs, addressable by file name
  {\setmainfont{CharisSIL-Regular.ttf}[
     BoldFont=CharisSIL-Bold.ttf,
     ItalicFont=CharisSIL-Italic.ttf,
     BoldItalicFont=CharisSIL-BoldItalic.ttf]}

\IfFontExistsTF{Universalis ADF Std}
  {\setsansfont{Universalis ADF Std}}
  {\setsansfont{Hiragino Sans GB}}
\IfFontExistsTF{Liberation Mono}
  {\setmonofont{Liberation Mono}}
  {\setmonofont{Menlo}}

\IfFontExistsTF{Noto Serif CJK SC}
  {\setCJKmainfont[AutoFakeBold=2.3,AutoFakeSlant=.16]{Noto Serif CJK SC}}
  {\setCJKmainfont[AutoFakeBold=2.3,AutoFakeSlant=.16]{Songti SC}}
\IfFontExistsTF{Noto Sans CJK SC}
  {\setCJKsansfont{Noto Sans CJK SC}}
  {\setCJKsansfont{PingFang SC}}
\IfFontExistsTF{Noto Sans Mono CJK SC}
  {\setCJKmonofont{Noto Sans Mono CJK SC}}
  {\setCJKmonofont{Menlo}}
```

On other platforms, swap the fallbacks for that platform's usual faces:

| Platform | CJK serif fallback | CJK sans fallback | Mono fallback |
| --- | --- | --- | --- |
| macOS | `Songti SC` | `PingFang SC` | `Menlo` |
| Windows | `SimSun` | `Microsoft YaHei` | `Consolas` |
| Linux | `Noto Serif CJK SC` / `Source Han Serif SC` | `Noto Sans CJK SC` | `Noto Sans Mono` |

> Tip: to test whether a font name resolves, compile a minimal document and check the log for `not loadable`.
> For a pixel-accurate reproduction, install all six fonts listed above.

### Building

```bash
# relationship announcement
xelatex love_announcement.tex
xelatex love_announcement.tex     # run twice: front-page anchors and links need it

# wedding issue
xelatex wedding_journal.tex
xelatex wedding_journal.tex
```

Or with `latexmk`:

```bash
latexmk -xelatex -interaction=nonstopmode wedding_journal.tex
```

Output: `wedding_journal.pdf` / `love_announcement.pdf` — 2 pages each (page 1 is the journal front page, page 2 continues the body and carries the reference list).

### Customization

#### 1. Edit only `couple-info.tex`

| Variable | Meaning | Announcement | Wedding |
| --- | :--- | :---: | :---: |
| `\PartnerA`, `\PartnerB` | The two authors | ✅ | ✅ |
| `\FirstMeetingDate` | First encounter / start of observation | ✅ | ✅ |
| `\RelationshipDate` | Relationship confirmed | ✅ | ✅ |
| `\AnnouncementDate` | Public disclosure date | ✅ | — |
| `\WeddingDate` | Wedding date | — | ✅ |
| `\WeddingCity`, `\WeddingVenue` | City and venue | — | ✅ |
| `\ContactEmail` | Corresponding e-mail | ✅ | ✅ |
| `\DaysObserved`, `\SharedTrips`, `\SharedMeals` | Days observed / trips / meals (used in the descriptive table) | — | ✅ |
| `\FutureHorizon` | Follow-up horizon (default “终身” = lifelong) | ✅ | ✅ |
| `\OurMotto` | Reserved motto, **not referenced by the current templates** | — | — |

#### 2. Titles, abstract and journal metadata

Edit the `\setJOL...` commands at the top of `love_announcement.tex` / `wedding_journal.tex`:

| Command | Effect |
| --- | --- |
| `\setJOLTitle` | Article title (keep it to 2 lines) |
| `\setJOLAuthors` | Author line; `\textsuperscript{a}` / `\textsuperscript{a,*}` mark affiliation and corresponding author |
| `\setJOLAffilA` / `\setJOLAffilB` | Affiliations (`B` is hidden when empty) |
| `\setJOLKeywords` | Keywords, separated by `\\` |
| `\setJOLAbstract` | Abstract (keep it under ~200 words; longer text overflows the fixed front-page band) |
| `\setJOLCoverSub` / `\setJOLCoverIssue` | Section label and volume/issue on the miniature cover |
| `\setJOLMeta` | Top-of-page metadata line; also updates the running head |
| `\setRunningAuthor` | Author name in the running head |
| `\setJOLCorrespondence`, `\setJOLEmail` | Corresponding-author block |
| `\setJOLDOI`, `\setJOLReceived`, `\setJOLOnline`, `\setJOLCopyright` | Footer DOI, date stamps, copyright line |
| `\setJOLFootnoteText` | The footnote marked ¹ on the front page |

#### 3. Typesetting helpers

| Command / environment | Purpose |
| --- | --- |
| `\begin{JOLtable}{caption} … \end{JOLtable}` | Journal-style compact three-line table (`tabularx`, column width) |
| `\JOLphoto{path}{caption}` | Figure; a grey placeholder with the path is drawn if the file is missing |
| `\JOLsource{source}` | Small “Source.” note under a figure |
| `\makeJOLfrontmatter` | Renders the whole front page; place it right after `\begin{document}` |

#### 4. Adding photos

Create `assets/` and use these file names (any other name works too — just change the path in `\JOLphoto`):

- Announcement: `assets/announcement-photo.jpg`
- Wedding: `assets/wedding-photo.jpg`

### FAQ

**1. `! Package fontspec Error: The font "Charis SIL" cannot be found.`**
A font is missing — see [Fonts](#fonts-the-most-likely-stumbling-block), or apply the automatic fallback snippet.

**2. Front-page elements are misaligned or overlapping**
The masthead is drawn at **absolute coordinates (bp)** with fixed-height bands. A title longer than 2 lines, an overlong abstract or a long author line will overflow. Shorten the text, or nudge the coordinates passed to `\JOLPutText` in `journaloflove-sci.sty` (the first two numbers are the x/y offsets in bp from the page's top-left corner).

**3. Chinese text renders as boxes or is missing**
The CJK fonts are not installed — see [Fonts](#fonts-the-most-likely-stumbling-block).

**4. Links or positions are wrong**
You compiled only once. XeLaTeX needs two passes.

**5. The page number doesn't start at 1**
Intentional: it starts at **520** for the pun. Change `\setcounter{page}{520}`.

**6. Figures or tables jump somewhere unexpected**
They are `[t]` floats pinned to the top of a column — normal journal behaviour (`JOLtable` and `\JOLphoto` already request `[t]`).

**7. Using Overleaf**
Upload the project, set the compiler to **XeLaTeX**, and if a font error appears, apply the fallback snippet above.

### License & notices

- This repository **does not declare a license yet** — please confirm with the author before reuse; adding one is recommended (MIT for code, CC BY 4.0 for docs).
- The fonts keep their own licenses: Charis SIL, Liberation and Noto CJK are **SIL OFL 1.1**; Universalis ADF Std is **GPL v2+ with a font exception**. Respect those terms when distributing PDFs with embedded fonts.
- The layout is a stylistic homage to academic journal page design. Keep it for personal, commemorative use — do not use it to impersonate a real publication or for commercial publishing.

### Acknowledgements

Thanks to everyone who witnessed this relationship. If the template helped you finish a paper of your own, a ⭐ is appreciated.

---

*Journal of Love — Cupid Press. All hearts reserved.*
