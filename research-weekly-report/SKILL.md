---
name: research-weekly-report
description: "Build evidence-backed research weekly reports from conversations and project-file changes within a user-specified time window. Use for research or work weekly-report workflows, not generic writing-only requests."
metadata:
  short-description: "Evidence-backed research weekly reports"
---

# Research Weekly Report

Create a concise, evidence-backed Markdown weekly report from the user's activity. The workflow is designed to separate what was discussed, what the user chooses to report, and what is supported by saved project files.

## Required Inputs

Establish these inputs before auditing:

- **Time window:** explicit start, end, and timezone. Treat both endpoints as inclusive. For example, a named week may be expressed as `2026-11-09 00:00:00` through `2026-11-15 23:59:59` in `Asia/Shanghai`.
- **Conversation sources:** use all sources that are accessible in the current environment. State any unavailable source instead of silently omitting it.
- **Project roots:** identify only the folders relevant to the scope the user selects.
- **Output location:** use a user-specified folder when supplied. Otherwise write the Markdown report in the current workspace and state that location before writing.

The user may specify any time window. Do not hard-code a calendar week or infer a timezone from the execution host. When the user says “standard week,” use the convention they explicitly give; if no convention is available, ask for the intended dates before reading records.

Normalize ambiguous end-of-day shorthand before filtering: when the user gives an end time such as `23:59` for a date, treat it as the final representable instant of that local minute (`23:59:59.999...`) unless the user specifies a narrower cutoff. Preserve the requested timezone in the report.

If the end of the requested window is still in the future, report the requested range and clearly state the actual coverage cutoff. Do not present future days as completed work.

## Workflow

### 1. Audit Conversations

1. Inventory accessible conversation sources before searching them, for example Codex threads and ChatGPT conversations when the environment exposes them. State which sources were searched and which were unavailable.
2. List threads from each accessible source and select candidates with activity in the requested window.
3. Identify the timezone or epoch basis of each conversation timestamp, convert it to the requested reporting timezone, and then apply the inclusive time-window comparison. A thread's title, summary, or last-update time is only a discovery aid, not proof that all of its content belongs in the window.
4. Paginate until the relevant interval is covered. Exclude older turns from long-lived threads.
5. Group the verified activity by workstream. For each group, distinguish:
   - the user's objective;
   - completed work and concrete conclusions;
   - work that is planned, blocked, or still unverified.

Keep unrelated topics separate. Do not silently merge different projects just because they occurred in the same week.

### 2. Confirm Reporting Scope

Present the grouped workstreams and ask the user which ones belong in this report, unless the user has already specified the scope. Do not draft the report from every detected conversation by default.

Treat scope confirmation as a decision point: topics excluded by the user must not reappear as background, achievements, or next-week plans. Map every selected workstream to one or more relevant project roots or subdirectories before the file audit. If a selected workstream has no known root, ask for it or explicitly report that its file evidence could not be checked.

### 3. Audit File Evidence

For the project roots tied to the confirmed scope:

1. First inspect the project tree and identify the subdirectories relevant to each selected workstream. Do not treat every time-matched file under a broad project root as report evidence.
2. Recursively find files whose `LastWriteTime` falls inside the same inclusive window. Do not recurse into reparse points or symbolic links. Skip `.git`, virtual environments, dependency directories, caches, browser profiles, and obvious build/render folders by default; include them only when a representative artifact is needed to substantiate completed work.
3. Use `CreationTime` only to classify a file as newly created during the interval versus an older file modified during it. Do not claim that a file was newly authored when timestamps only prove that it was saved or copied.
4. Query the filesystem host timezone. If it differs from the requested reporting timezone, convert the requested interval to the host-local time used by `LastWriteTime` before filtering; do not assume filesystem timestamps are UTC. State any timestamp ambiguity that cannot be resolved.
5. Classify matches into:
   - final deliverables and editable source artifacts;
   - research data, experimental outputs, or newly collected references;
   - scripts, logs, intermediate reconstructions, render previews, build artifacts, caches, and dependencies.
6. Inspect representative final artifacts and the smallest set of process files needed to substantiate claims. Use document, presentation, PDF, or image inspection tools when their contents matter. For very large result sets, summarize counts by class first, then inspect targeted artifacts rather than opening every file.

When a file is used as evidence, map it back to a selected workstream. Do not carry a same-folder file into the report merely because its timestamp falls inside the window.

Do not count duplicated exports, rendered pages, build copies, logs, virtual environments, or dependency files as separate research achievements. Summarize large artifact sets by category and retain representative paths and metrics.

### 4. Reconcile Evidence

Cross-check reportable claims against the conversation audit and file evidence:

- Preserve exact numbers, dates, completion state, uncertainty, and comparison scope.
- Distinguish an implemented or tested result from a proposal, design, or literature review.
- If two runs have different metrics, identify them as separate runs instead of implying a direct before-and-after comparison.
- If a claim cannot be confirmed from accessible evidence, either qualify it or leave it out.

Never edit, move, or delete project artifacts while auditing them unless the user separately asks for that operation.

### 5. Draft for a Busy Supervisor

Read [the supervisor Markdown template](references/supervisor-markdown-template.md) when creating a new report or restructuring one for a supervisor.

Lead with the conclusion, not the activity log. A supervisor should be able to identify within roughly 30 seconds:

1. what each selected workstream is trying to accomplish;
2. what the work established this period;
3. what remains unresolved and what happens next;
4. any focused decision or confirmation requested from the supervisor.

Default to a three-bullet `30 秒摘要`, followed by one compact section per workstream using `Goal`, `Completed This Period`, and `Current Assessment`. Keep the summary to three bullets and normally use three to six evidence-backed bullets per workstream. Put detailed file paths in a short appendix rather than the main narrative. Expand only when the user requests a more detailed report.

Apply a manual editorial pass:

- Use direct verbs and concrete subjects; remove generic claims, decorative framing, and repeated restatements.
- Retain technical terms when they carry necessary meaning.
- Do not turn plans into completed work, literature review into experimental validation, or a current artifact into a final project result.
- Preserve useful constraints, negative results, limitations, and conditions rather than polishing them away.
- Keep independent facts even when condensing lists. Do not add unsupported metrics, causal explanations, or claims of advisor approval.

## Output

Unless the user requests another format, create one Markdown report in the requested output folder. Use a descriptive filename based on the specified window, such as `2026-11-09_2026-11-15_周报.md`.

In the final response, link the report and state any meaningful coverage limitation, such as an inaccessible conversation source or a requested time window that has not yet ended. Do not include raw audit logs unless the user asks for them.
