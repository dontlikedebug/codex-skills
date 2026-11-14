# Supervisor Markdown Template

Use this as a compact structure for an evidence-backed research weekly report. Adapt headings when the user has an established format; do not invent a workstream, metric, conclusion, or request for guidance.

```markdown
# 周报（<start date> 至 <end date>）

> 记录截至 <coverage cutoff>，时区为 <timezone>。

## 一、30 秒摘要

- **<workstream 1>**：<what the work is for>。本周<established result>；<current limitation or status>。
- **<workstream 2>**：<what the work is for>。本周<established result>；<current limitation or status>。
- **下周重点**：<one concise action sequence>。

## 二、<workstream 1>

**本周目标**：<question, deliverable, or decision being addressed>。

**本周完成**：

- <verified action or artifact>
- <verified result, metric, or design decision>

**当前判断**：<what the evidence supports, including limits and what has not been implemented or tested>。

## 三、<workstream 2>

**本周目标**：<question, deliverable, or decision being addressed>。

**本周完成**：

- <verified action or artifact>
- <verified result, metric, or design decision>

**当前判断**：<what the evidence supports, including limits and what has not been implemented or tested>。

## 四、下周重点<and request for confirmation when needed>

1. <next action>
2. <next action>

<Only include this line when the user wants a supervisor decision:>
**请老师确认**：<one decision the supervisor can answer directly>？

## 五、可追溯成果文件（备查）

- `<path to a representative report, model, dataset, or source artifact>`
- `<path to another representative artifact>`
```

## Writing Checks

- Place the conclusion and current state before implementation detail.
- Keep the `30 秒摘要` to at most three bullets unless the user explicitly requests a more detailed executive summary.
- Use three to six bullets per workstream by default; move raw paths, logs, and repeated artifact variants to the appendix.
- Label separate experimental runs explicitly; do not compare their metrics unless the evidence supports that comparison.
- State a negative result directly when it changes the next action.
- Keep paths, code identifiers, dates, and measured values unchanged.
- Omit the confirmation prompt when the report does not need a decision from the supervisor.
