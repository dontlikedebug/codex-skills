# Codex Skills

这个仓库用于存放可复用的 Codex Skills。每个 Skill 都是一个独立目录，包含 `SKILL.md` 及其必要的模板、参考资料或脚本。

## 当前 Skills

### `research-weekly-report`

从指定时间窗内的对话记录和项目文件变化中整理可追溯的研究周报，适合研究生、科研助理或需要向导师汇报进展的工作场景。

它会按以下顺序工作：

1. 按用户指定的起止时间和时区筛选可访问对话。
2. 将对话按工作方向归类，并由用户确认本周报告范围。
3. 检查相关项目目录中最后保存时间落在同一时间窗内的文件，区分最终成果、研究资料和构建或渲染过程文件。
4. 交叉核对对话与文件证据，避免把计划、调研或中间产物写成已完成的实验结果。
5. 生成便于导师快速阅读的 Markdown 周报，包含摘要、各工作方向的目标和结论、下周计划，以及可选的待确认问题。

### 使用方式

将 `research-weekly-report` 目录放入 Codex 的 Skills 目录后，可直接使用：

```text
$research-weekly-report
```

调用时请提供时间窗、时区、需要读取的对话来源和相关项目目录。若未指定输出位置，Skill 默认将 Markdown 周报写入当前工作区。

## 目录结构

```text
research-weekly-report/
|- SKILL.md
|- agents/
|  `- openai.yaml
`- references/
   `- supervisor-markdown-template.md
```
