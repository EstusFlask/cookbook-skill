---
name: cookbook-skill
description: Summarize cooking videos, subtitle files, transcripts, or cooking demonstrations into faithful Markdown recipe files. Use when Codex needs to watch or inspect a cooking video, read subtitles or a transcript, extract ingredients, tools, steps, timings, temperatures, and cautions, and produce a complete recipe without omitting or distorting the source.
---

# Cookbook Skill

## Goal

Create a Markdown recipe file from a cooking video, subtitle file, or transcript. Preserve the source's meaning, especially required warnings, constraints, timings, temperatures, tool requirements, and order-sensitive steps.

## Workflow

1. Identify the source type: video, subtitle file, transcript, URL, or pasted text.
2. Prefer subtitles or transcripts for exact wording. Use video/audio inspection when subtitles are missing, incomplete, or when visual details are needed for tools, texture, color, doneness, or technique.
3. Extract evidence before writing:
   - Dish name, if stated or clearly visible.
   - Ingredients, including quantities, forms, brands, temperatures, or preparation states when given. In the ingredient list, mark every ingredient with its quantity; write `用量未知` when the source does not state or show a reliable quantity.
   - Tools and equipment, including containers, pans, strainers, mixers, thermometers, molds, and serving tools when mentioned or visibly required. Mark a tool count only when more than one of the same tool is required; omit the count for a single tool.
   - Ordered cooking steps, including prep, cooking, resting, cooling, serving, and storage.
   - Every caution, required condition, prohibition, timing, temperature, texture cue, substitution limit, and doneness cue.
4. Write or update one Markdown file. Put newly created recipe files in an `output/` directory unless the user explicitly requests another path; create `output/` first if it does not exist. If the user did not provide a filename, choose a concise filename from the dish name or source basename.
5. Verify completeness against the source before finalizing.

## Concise Mode

If the request includes `/cookbook-skill concise` or asks for concise output, write a clean recipe without source-provenance notes. Preserve useful cooking information, but remove parentheticals or clauses whose only purpose is to explain where the information came from, such as `字幕说明`, `视频里提到`, `画面看到`, or `原作者说`.

- Write `吐司或其他面包`, not `吐司或其他面包（字幕说明用吐司，其他面包也可以）`.
- Keep substantive recipe details: quantities, required tools, warnings, substitutions, timing, temperature, texture cues, and doneness cues.
- If an element is genuinely not stated, write `未明确说明` instead of `原视频/字幕未明确说明`.

## Markdown Format

Use this structure exactly:

```markdown
# 菜名

## 原材料
- 原材料 1：20mL
- 原材料 2：3个
- 原材料 3：用量未知

## 要用到的工具
- 工具 1
- 工具 2：2个

## 制作步骤
1. 步骤 1。
2. 步骤 2。
```

Keep all three required sections even if the source omits information. If an element is genuinely not stated or cannot be determined, write `原视频/字幕未明确说明` in that section rather than inventing details.

## Fidelity Rules

- Do not invent ingredients, quantities, tools, temperatures, timings, or substitutions.
- Every ingredient bullet must include a quantity, such as `20mL` or `3个`; if the quantity is not stated or reliably visible, write `用量未知`.
- Do not omit tools that the source says are required or clearly uses as part of the method.
- For tools, include counts only when more than one of the same tool is needed, such as `碗：2个`; write a single required tool without a count.
- Preserve modal strength:
  - If the source says something is required, write it as required, such as `必须` or `一定要`.
  - If the source only recommends something, write it as recommended.
  - If the source says something is optional, write it as optional.
- Do not weaken required instructions. For example, if the source says `一定要使用网筛`, do not write `推荐使用网筛`.
- Do not strengthen optional suggestions into requirements.
- Place source cautions inside the relevant numbered step, not only in a separate note.
- Preserve sequence when order matters. If the source says to add, heat, rest, strain, or cool before another action, keep that order.
- Include exact times, temperatures, ratios, visual cues, and texture cues when stated.
- If the source is ambiguous, state the uncertainty plainly instead of resolving it by guesswork.

## Completeness Check

Before returning the result, confirm:

- The Markdown file exists in the requested path, or in `output/` for newly created recipes when no other path was requested, and contains `原材料`, `要用到的工具`, and `制作步骤`.
- Ingredients include all items mentioned or visibly used in the source.
- Every ingredient includes a source-supported quantity or `用量未知`.
- Tools include all mentioned or visibly required equipment.
- Tools that require more than one item include a count, while single tools do not.
- Numbered steps cover the full cooking process from preparation through completion.
- Every caution or constraint from the source appears in the relevant step.
- Required, recommended, and optional instructions keep the same force as the source.
