---
name: lemo-opuscar
description: Direct and produce a short film made entirely in code, in one of the styles of the Lemo-Opuscar library (e.g. Impasto Oil Painting 油画厚涂, Watercolor Brush 水彩笔刷, Ukiyo-e 浮世绘, Satellite Briefing 卫星简报, Exploded Teardown 产品拆解). Use when the user asks for a video, film, short, promo, explainer or animation (视频、短片、动画、宣传片) in a named style, including explainers built from real material such as satellite imagery, laser scans, CAD files or archive scans (数据解说、科普、产品拆解), and new films cut from real archive footage and documents (剪辑纪实, e.g. 用档案影像剪一支新闻片); when they want a film about their own topic and haven't chosen a style (help them choose); when they want to change a style into their own, make their own style from a blank page, or use a style they saved (改风格、从空白开始、我的风格); when they start the skill without saying what they want; or when they ask which film styles there are. Not for plain editing, trimming or converting the user's existing video files.
---

# Lemo-Opuscar

The styles, guides and tools live in the Lemo-Opuscar library (github.com/lemomo-ai/lemo-opuscar). This skill fetches it and hands you over to it.

## 本机生成前的风格询问（用户指定流程）

本节优先于上游关于自动推荐后直接制作、跳过已答问题的默认流程。

- 每次开始一项新的影片生成任务，先读取 [中文风格选择目录](references/styles-zh.md)，并向用户询问本次要用什么风格。必须等待本次回复后，才进入创意方案、分镜或生成制作；不得把历史偏好、推荐项或等待超时当作选择。
- 用户尚未指定风格：依据题材推荐 2–3 个库中真实存在的风格，说明特点；按上游 Finding the style 展示完整分类名单和画廊链接，再问“这次想用哪种风格？可以回复中文名称或目录标识。”完整目录放在用户可见消息中，不能只留在工具输出。
- 用户已经指定风格：先核对名称，询问“这次确认使用「中文名（slug）」吗？”并等待回复。用户在这一询问后确认即可继续；同一影片的续作步骤或修改不重复询问，除非新建影片或更换风格。
- 所有选项、分类和名称以当前库 `$LIB/styles/README.md` 与 `styles/*/style.json` 为准，不自行合并、改名或捏造。目录与库版本不一致时，先核对当前索引再展示。本地保存的自定义风格单独列出；只有用户明确要求自定义时才走 MY-STYLES.md。
- 名称有歧义时列出最接近的 2–3 项让用户选择。标记 ✦ 的风格在推荐时说明需要图片生成工具。选定后读取对应完整 STYLE.md，遵循其视觉、动作、声音及素材约束。
- 在 Codex 中，上游 AskUserQuestion 用可用的用户输入工具代替；没有该工具则在最终回复中提问并等待。完整风格名单先展示，使用自由文本问题，不用少量按钮限制选择。
- 只查询风格或整理资料时不安装渲染依赖。生成任务在风格确认后执行下方安装与制作流程。

## 上游安装与制作流程

1. **Get the library.** Run `sh "<skill base directory>/scripts/setup.sh"`. It clones or updates the library (default `~/lemo-opuscar`; a clone the user is standing in is used as it is), lists any missing system tools (Node, ffmpeg, Python) and prints `LIB=<path>` on its last line.
2. **Install the core tools early.** Start `sh "<skill base directory>/scripts/setup.sh" deps` right away, in the background if you can: it takes a few minutes the first time. Add `deps voice` or `deps music` later, only if the film needs them (`$LIB/TECHNIQUE.md` §1). Report missing system tools (Node, ffmpeg, Python) in your one round of questions; don't install system software yourself. A style marked ✦ also needs an image generator the user provides (`$LIB/AGENTS.md`, Workflow, Brief). Packages a style needs (its `STYLE.md` lists them) you install yourself, into the project folder.
3. **Follow the library.** Read `$LIB/AGENTS.md` and do what it says, starting with **Start** (the user's own styles in `~/lemo-my-styles/`; when they started the skill without writing anything, the language question first, then the ways in): finding the style or making their own, the one round of questions, the treatment, production and delivery.

What changes in skill mode:

| | |
|---|---|
| Project folder | `<name>/` in the folder the user started from (lowercase letters, digits, hyphens; avoid `#` and `?` in the path). Wherever the guides say `films/<name>/`, read this folder |
| Running tools | from `$LIB`, with the project's absolute path: `cd "$LIB" && node core/render/still.mjs "<project>" 1.5 3` |
| Library files in pages | absolute URLs: `/core/lib.js`, `/node_modules/three/…` (the project is served at `/@film/`) |
| Library files in scripts and `build.sh` | `$LIB/…`, with `LIB=<path>` at the top of `build.sh`; never `../..` |
| Demo source | not downloaded. `sh "<skill base directory>/scripts/setup.sh" demo <slug>`, only after your `TREATMENT.md` is written, to read its techniques; it is not meant to be rendered. An Edit & Documentary style is the exception: fetch it before the treatment to use the material tools its `STYLE.md` names in `demo/tools/` (`$LIB/AGENTS.md`, "Treatment first") |

Deliver what `$LIB/DIRECTOR.md` §11 lists, in the project folder, and tell the user where it is.
