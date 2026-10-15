# Cookbook Skill · 菜谱整理技能

从烹饪视频、字幕文件、逐字稿或演示中提取信息，生成忠实于来源的 Markdown 菜谱，保留原材料、用量、工具、步骤、时间、温度和注意事项。

A Codex skill that turns cooking videos, subtitles, transcripts, and demonstrations into faithful Markdown recipes, preserving ingredients, quantities, tools, ordered steps, timings, temperatures, and cautions.

## 使用

将本仓库作为本地技能安装到所用助手的技能目录，确保保留 [`SKILL.md`](SKILL.md) 和 [`agents/`](agents/)，并在新会话中使用。提供视频、字幕或逐字稿作为输入：

```text
使用 $cookbook-skill，把这份字幕整理成完整菜谱。
```

原有的命令式写法也可用于表达模式：

| 模式 | 请求示例 | 输出 |
| --- | --- | --- |
| 默认 | `/cookbook-skill` | 保留必要的来源说明，方便核对 |
| 简洁 | `/cookbook-skill concise` | 去掉来源说明，保留全部实质做法与限制 |

## 输出约定

默认写入 `output/` 目录，包含以下三节：

1. **原材料**：每项标注用量；来源未说明时写“用量未知”。
2. **要用到的工具**：保留必要工具，多件同类工具才标数量。
3. **制作步骤**：按实际顺序整理，相关警示直接写在对应步骤中。

不会补造来源中没有的配方、温度或时长，也不会把可选项改成必需项。视频读取能力取决于当前助手可用的工具；本仓库提供整理规则，不附带视频下载或转录程序。

查看 [`output/example.md`](output/example.md) 了解输出示例，完整规则见 [`SKILL.md`](SKILL.md)。

## English overview

Install the repository as a local skill in your agent's configured skills directory, then start a new session and supply the source material. Ask to use `$cookbook-skill`; add `concise` for a recipe without provenance notes. Output defaults to `output/` and keeps the Chinese section headings defined in the skill. Missing quantities and uncertain details are marked explicitly rather than invented.
