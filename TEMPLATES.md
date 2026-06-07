# Templates

Read this file only when generating the matching output block. Templates may repeat safety rules because they are copy-paste artifacts meant to travel between tools.

## Architect Templates

### Compact Architect -> Builder Task

Use for Level 1 / tiny / docs-only / bounded maintenance.

````text
To: Builder
From: Architect
Role: Builder
Task: <任务名>
Mode: <implement-only | patch-only>
Execution Pace: Fast Track
Task Card Size: Compact
Scope:
- <允许范围>
Do Not:
- Do not commit or push unless User explicitly authorizes it.
- Do not expand scope.
- Do not modify files outside Expected Files To Change unless blocked.
- If blocked, stop and report instead of guessing.
Expected Files To Change:
- <文件路径或 N/A>
Not Expected / Prohibited Files:
- <文件路径或范围, only if explicit boundary matters>
Acceptance Criteria:
- <验收标准>
Verification:
- <命令或手动检查>
Deliverable:
- Compact Completion Report: summary, files changed, verification, remaining risks, commit / push status.
- Spec alignment / drift flag only if product behavior or Spec Reference is involved.
Commit / Push:
- Not authorized unless User explicitly says otherwise.
````

### Standard / Detailed Architect -> Builder Task

Use for normal, risky, extended, overnight, resume, or reviewer-needed work.

````text
To: Builder
From: Architect
Role: Builder
Task: <任务名>
Mode: <implement-only | implement-extended | overnight-extended>
Execution Pace: <Fast Track | Strict Gate>
Task Card Size: <Standard | Detailed>
Scope:
- <允许范围>
Do Not:
- Do not commit or push unless User explicitly authorizes it.
- Do not expand scope.
- Do not modify files outside Expected Files To Change unless blocked.
- If blocked, stop and report instead of guessing.
Context:
- Spec Reference: <PROJECT_SPEC.md / FEATURE_SPEC.md / AI_CONTEXT.md / README / User goal / N/A>
- Current Milestone:
- Next Milestone:
- Milestone Fit: matches Next Milestone / corrective maintenance / postponed exception approved by User
- Session Work Package Type:
- Work Package Rationale:
- Stop Point:
- Project Fit: CORE / EXTENSION
- Priority: NOW / NEXT / LATER / NOT NOW
- Value:
- Cost:
- Task Risk Level: Level 1 / Level 2 / Level 3 / Level 4
- Builder Mode Rationale:
- Timebox / Checkpoint Cadence: <required for extended / overnight, otherwise N/A>
- Overnight Task Queue: <required for overnight, otherwise N/A>
- Commit / Push Status: not requested / User authorized after DONE / N/A
- AI_CONTEXT.md Update Required: yes / no
- AI_CONTEXT.md Sections To Update: <Product State / Completed Tasks / Current Project Status / Latest Decisions / Current Architecture Notes / Design Alignment Notes / Known Risks / TODO / Suggested Next Direction / N/A>
Instructions:
1. <任务步骤>
2. <任务步骤>
Expected Files To Change:
- <文件路径或 N/A>
Not Expected / Prohibited Files:
- <文件路径或范围>
Acceptance Criteria:
- <验收标准>
Verification:
- <命令或手动验证项>
Stop Conditions:
- risk higher than Task Card
- prohibited file needed
- expected files insufficient
- new dependency needed
- repeated validation failure
- requirement unclear
- product / architecture decision needed
Deliverable:
- Completion Report size: <Standard | Detailed>
- Summary
- Files changed
- Verification results
- Remaining risks
- AI_CONTEXT.md updated: yes / no / not requested
- Commit / push status
- Spec alignment / drift flag when Spec Reference, product behavior, or drift risk is involved
Commit / Push:
- Do not commit or push unless User explicitly authorizes it.
````

### Architect -> Builder Resume Task

````text
To: Builder
From: Architect
Role: Builder
Task: <任务名> Resume
Mode: implement-extended-resume
Scope:
- Continue only the previously approved task from checkpoint or reconstructed git diff.
Do Not:
- Do not commit or push unless User explicitly authorizes it.
- Do not expand scope.
- Do not modify files outside Expected Files To Change unless blocked.
- If the working state is unclear, stop and report instead of guessing.
Context:
- Previous approved Task:
- Last known checkpoint:
- Current git status / diff summary:
- Files already changed:
- Validation already run:
- Validation still needed:
- Known risks:
Instructions:
1. Reconstruct current state from files and git diff.
2. Compare against the previous approved Task.
3. Continue only remaining approved work.
4. Stop if the current diff includes unrelated or unclear changes.
Expected Files To Change:
- <文件路径或 N/A>
Not Expected / Prohibited Files:
- <文件路径或范围>
Acceptance Criteria:
- <验收标准>
Verification:
- <命令或手动验证项>
Deliverable:
- Detailed Completion Report
- Summary
- Files changed
- Verification results
- Remaining risks
- Context pollution flag
- Commit / push status
Commit / Push:
- Do not commit or push unless User explicitly authorizes it.
````

### Architect -> Reviewer Review

````text
To: Reviewer
From: Architect
Role: Reviewer
Task: <审查任务名>
Mode: review-only
Scope:
- Review only the implementation for the approved task.
Do Not:
- Do not modify code.
- Do not command Builder.
- Do not expand review scope beyond requested files / diff.
- Do not make final architecture decisions.
Context:
- Approved Task:
- Task Risk Level:
- Builder Report:
- Files / diff to inspect:
- Verification evidence:
Review Focus:
1. Scope match.
2. Correctness.
3. Missing edge cases.
4. Risk level mismatch.
5. Validation gaps.
6. Spec / design drift if relevant.
Expected Output:
- Recommendation: PASS / PASS WITH FIXES / BLOCKED
- Findings ordered by severity.
- File / line references when possible.
- Remaining risk.
````

### Task Close Review

Compact close:

````text
# Task Close Review
## Decision
DONE / NEEDS FIX / NEEDS REVIEWER / BLOCKED
## Scope / Verification
- Task satisfied: yes / no
- Verification acceptable: yes / no
- Remaining risks: none / details
- AI_CONTEXT.md: updated / not needed / follow-up needed
## Commit / Push Gate
- Commit recommended: yes / no
- Push recommended: yes / no
- User authorization: required / already provided
## Session Decision
- Continue current session / recommend fresh session / require fresh session
- Reason:
````

Full close:

````text
# Task Close Review
## 1. Scope Check
- Task Card satisfied: yes / no
- Scope expanded: no / details
- Prohibited files/actions respected: yes / no
## 2. Verification
- Builder verification reviewed: yes / no
- Additional review needed: no / Reviewer / Architect repo check
- Remaining risks:
## 3. AI_CONTEXT.md / Spec
- AI_CONTEXT.md status: current / needs update / N/A
- Spec status: current / needs update / N/A
- Required follow-up before DONE: none / details
## 4. Decision
DONE / NEEDS FIX / NEEDS REVIEWER / BLOCKED
## 5. Commit / Push Gate
- Commit recommended: yes / no
- Push recommended: yes / no
- User authorization: required / already provided
## 6. Suggested Next Direction
- Non-binding direction only. Not a Task Card.
## 7. Design Alignment Review
- Not needed / completed / needed next
- Result if completed: STILL ALIGNED / DRIFT NEEDS CORRECTION / BETTER DIRECTION FOUND / N/A
## 8. Session Decision
- Continue current session / recommend fresh session / require fresh session
- Reason:
## 9. Next Session Starters

Required when fresh session is recommended or required.

Provide both:
- Next Architect Session Starter
- Next Builder Session Starter

Only omit one if User explicitly asked for only one.

Both starters must be complete, standalone, continuous, and copy-once usable.

The Builder Starter must not authorize implementation by itself unless the Architect is also intentionally issuing a Task Card in the same closeout. If no next task is authorized yet, Builder Starter must say: wait for Architect Task Card.
````

### Next Architect Session Starter

Output when fresh session is recommended or required.

````text
请进入 Architect 模式。
请先阅读并遵守：
- ARCHITECT.md
- PROJECT_SPEC.md / FEATURE_SPEC.md（如存在）
- legacy PROJECT_DESIGN.md（如存在）
- AI_CONTEXT.md（如存在）
产品目标、MVP、Not Now、Current Milestone、Next Milestone 以 PROJECT_SPEC.md / FEATURE_SPEC.md 为准。
当前实现状态、已完成任务、风险和 TODO 以 AI_CONTEXT.md 为准。
历史聊天记录视为可能失效，只能作为临时参考。
请先恢复项目状态，然后等待我提供下一步目标。
不要直接生成 Builder Task Card，除非我明确提出下一步需求。
不要把 AI_CONTEXT.md 的 Suggested Next Direction 当成正式任务；它只能作为讨论方向。
````

### Next Builder Session Starter

Output when fresh session is recommended or required.

````text
To: Builder
From: Architect
Role: Builder
Mode: <implement-only | patch-only | implement-extended | overnight-extended | implement-extended-resume>

Required files to read:
- BUILDER.md
- AI_CONTEXT.md（如存在）
- <PROJECT_SPEC.md / FEATURE_SPEC.md only if named as Spec Reference>

Source of truth:
- Current implementation state: AI_CONTEXT.md and current files.
- Product goal / MVP / Not Now / Milestone: PROJECT_SPEC.md / FEATURE_SPEC.md when named as Spec Reference.
- This Builder Starter is execution context only unless Architect intentionally includes a Task Card in this same closeout.
- If no Task Card is included, Builder must restore repo state and wait for Architect Task Card.
- Chat history is temporary reference only.

Current task:
- <具体下一步执行任务, or: No task authorized yet. Wait for Architect Task Card.>

Scope:
- <允许范围>

Do Not:
- Do not implement anything outside this Starter.
- Do not expand scope.
- Do not modify files outside Expected Files To Change unless blocked.
- Do not commit or push unless User explicitly authorizes it.
- If blocked or unclear, stop and report instead of guessing.

Expected Files To Change:
- <文件路径或 N/A>

Not Expected / Prohibited Files:
- <文件路径或范围>

Acceptance Criteria:
- <验收标准>

Verification:
- <命令或手动验证项>

Deliverable:
- <Compact / Standard / Detailed> Completion Report
- Summary
- Files changed
- Verification results
- Remaining risks
- Commit / push status

Commit / Push status:
- <not authorized / User authorized commit only / User authorized commit and push / N/A>

Commit-boundary closeout, if applicable:
- Commit count target: <N / N/A>
- Exact commit messages:
  1. <message / N/A>
- File boundary per commit:
  1. <files / N/A>
- Pre-commit cleanup items:
  - <items / none>
- Staging instructions:
  - <instructions / N/A>
- Final git status expectation:
  - <clean / specific remaining files / N/A>
- Explicit push status:
  - <push authorized / push not authorized / N/A>
````

### Design Alignment Review

````text
# Design Alignment Review
## Baseline
- Spec / user goal:
- Current milestone:
## Current Direction
- What implementation now does:
- What changed:
## Alignment Status
STILL ALIGNED / DRIFT NEEDS CORRECTION / BETTER DIRECTION FOUND
## Evidence
- Files / behavior / Builder report / Reviewer report:
## Recommendation
- Keep / correct / update Spec:
## User Decision Needed
- yes / no
````

### Architect Decision Output

````text
# Architect Decision
## 1. Access Mode
Remote Architect Mode / Repo-aware Architect Mode
## 2. Project Fit
CORE / EXTENSION / OUT / NEVER
## 3. Priority
NOW / NEXT / LATER / NOT NOW
## 4. Value / Cost
- Value:
- Cost:
## 5. Task Risk Level
Level 1 / Level 2 / Level 3 / Level 4
## 6. Builder Mode
implement-only / implement-extended / overnight-extended / implement-extended-resume / patch-only / N/A
## 7. Session Work Package
- Type:
- Why this size:
- Stop point:
## 8. Review Support
- Reviewer: needed / optional / not needed
- Required Reviewer capability:
## 9. Decision
DO NOW / POSTPONE / REJECT
## 10. Transferable Block
[only if needed]
````

## Builder Templates

### Nano Report

````text
用户需关注：
✅ 做了什么：<一句话>
⚠️ 需要决策：<无 / 有，说明>
🔐 是否授权提交：<等你授权 / 已授权 / 无需操作>
Files changed: <path(s)>
Verification: <passed / failed / not run with reason>
Remaining risk: <none / details>
Commit / push status: <not authorized / User authorized / N/A>
````

### Compact Completion Report

````text
用户需关注：
✅ 做了什么：<一句话>
⚠️ 需要决策：<无 / 有，说明>
🔐 是否授权提交：<等你授权 / 已授权 / 无需操作>
To: Architect
From: Builder
Role: Architect
Task: <任务名> Completion Report
Mode: architect-gate
Report Size: Compact
Summary:
- <what changed>
Files changed:
- <path>: <purpose>
Verification:
- <commands or manual check>
- result: passed / failed / not run with reason
Remaining risks:
- none / details
Commit / push status:
- not authorized / User authorized / N/A
Commit:
- Do not commit or push unless User explicitly authorizes it.
````

### Standard / Detailed Completion Report

````text
用户需关注：
✅ 做了什么：<一句话>
⚠️ 需要决策：<无 / 有，说明>
🔐 是否授权提交：<等你授权 / 已授权 / 无需操作>
To: Architect
From: Builder
Role: Architect
Task: <任务名> Completion Report
Mode: architect-gate
Report Size: <Standard | Detailed>
Scope:
- Report implementation result for the approved task only.
Context:
- Branch:
- Commit:
- Push status:
- Git status:
- Approved task:
Expected Files To Change:
- <approved expected files, only if Task Card named them or scope would otherwise be ambiguous>
Not Expected / Prohibited Files:
- <prohibited files, only if Task Card named them or explicit boundary matters>
Acceptance Criteria:
- <criteria from task instruction>
Verification:
- commands run:
- key result or key error output:
- manual check:
Summary:
- <what changed>
Files changed:
- <path>: <purpose>
Human-readable behavior verification, only if user-facing behavior changed:
- input / action:
- expected result:
- observed result:
Issues encountered:
- none / details
Remaining risks:
- none / details
Spec alignment / drift flag, only if Spec Reference, product behavior, milestone scope, or drift is involved:
- details
AI_CONTEXT.md, only if update was requested, expected, or blocked:
- updated / blocked with reason
Context pollution flag, only if triggered:
- details
Design drift flag, only if user-facing design direction is involved:
- details
Decision needed from Architect, only if needed:
- details
Commit / push status:
- not requested / User authorized / N/A
Commit:
- Do not commit or push unless User explicitly authorizes it.
````

### Checkpoint / Handoff

````text
To: Builder
From: Previous Builder
Role: Builder
Task: Resume <任务名>
Mode: implement-extended-resume
Scope:
- Continue only the previously approved task.
Do Not:
- Do not expand scope.
- Do not commit or push unless User explicitly authorizes it.
- Do not modify files outside Expected Files To Change unless blocked.
- If working state is unclear, stop and report instead of guessing.
Context:
- Current task:
- Completed steps:
- Files changed so far:
- Remaining steps:
- Validation already run:
- Validation not yet run:
- Known risks / blockers:
- Exact next step:
Instructions:
1. Inspect current git diff.
2. Compare diff against this handoff note.
3. Continue from the exact next step.
4. Run required verification before final report.
5. If this note and working tree disagree, stop and report.
Expected Files To Change:
- <files>
Not Expected / Prohibited Files:
- <files or ranges>
Acceptance Criteria:
- <criteria>
Verification:
- <commands>
Deliverable:
- Summary
- Files changed
- Verification results
- Remaining risks
Commit:
- Do not commit or push unless User explicitly authorizes it.
````

### Architect Escalation

````text
To: Architect
From: Builder
Role: Architect
Task: <升级事项>
Mode: architect-gate
Scope:
- Decide whether Builder may continue, narrow scope, request Reviewer, or stop.
Do Not:
- Do not treat this as implemented approval.
- Do not ask Builder to expand scope without explicit Architect decision.
Context:
- Current task:
- What I changed or found:
- Validation evidence:
- Risk or uncertainty:
Instructions:
1. Review the risk or boundary issue.
2. Decide whether to continue, change scope, request Reviewer, or stop.
Expected Files To Change:
- N/A
Not Expected / Prohibited Files:
- N/A
Acceptance Criteria:
- Architect gives an explicit next-step decision.
Verification:
- <commands already run or N/A>
Deliverable:
- Summary
- Decision
- Allowed scope if continuing
- Remaining risks
Commit:
- Do not commit or push unless User explicitly authorizes it.
````
