# Lemo-Opuscar · 生成前选择风格

基于 [Lemo-Opuscar by Lemomo (LemoLab)](https://github.com/lemomo-ai/lemo-opuscar) 的技能修改版，增加每次开始新片生成前询问并确认风格的步骤。原库 99 种风格、15 个分类及规范不变。

## 增加的功能

- 未指定风格：依据主题推荐 2–3 项，展示完整分类名单，等待用户选择。
- 已指定风格：先确认一次，收到回复后制作。
- 同一影片后续修改不重复询问；新建影片或更换风格时重新确认。
- 选择依据原库，选定后读取完整 STYLE.md。

[查看完整中文风格目录](skills/lemo-opuscar/references/styles-zh.md)：中文名、英文名、画面特点、适用内容和原规范链接。目录依据上游文字资料整理，并非逐片观看评测。

## 安装到 Codex

将本仓库 `skills/lemo-opuscar` 文件夹复制到 `~/.codex/skills/`。已有同名技能时先备份再替换。

调用 `$lemo-opuscar`，例如：“用这个技能做一支 30 秒的科普视频。”AI 会先询问风格。

本仓库包含技能、上游安装脚本和中文目录。完整渲染库首次使用时由原安装脚本下载到 `~/lemo-opuscar`，依赖按影片需要安装；没有打包演示视频或渲染环境。原始工具面向 Claude，本版补充 Codex 的问答工具适配；本次验证涵盖技能格式与目录完整性，尚未端到端生成影片。

## 来源与许可

上游基准版本：`3a7132b996be0241c1ea0ab180d519f06e6f10b6`（2026-11-15 下载）。运行时库遵循原安装脚本的下载逻辑；目录与库版本不同须核对当前索引。

本版修改：SKILL.md 增加风格确认流程；新增中文分类及用途索引；目录中的规范链接改为固定上游版本链接。保留原 setup.sh。

原作者：Lemo-Opuscar by Lemomo (LemoLab)。贡献风格：Memphis Diorama by EianLu；Crayon World 3D by 2nd1st。

Markdown 文档及其改编依照 [CC BY-NC 4.0](LICENSES/CC-BY-NC-4.0.txt)；代码依照 [MIT](LICENSES/MIT.txt)。原库的额外许可、第三方材料及商标条款见 [上游许可说明](UPSTREAM-LICENSE)。本仓库不代表上游官方版本。
