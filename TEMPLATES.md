# Templates

Read this file only when generating the matching output block. Templates may repeat safety rules because they are copy-paste artifacts meant to travel between tools.

Template principle:

- Delegate outcomes, not steps.
- Human is the Product Owner, not the Message Broker.
- Architect authorizes coherent Work Packages and owns review / DONE.
- Builder owns local plan, implementation, verification, self-fix, self-review, and evidence inside the approved boundary.
- Reviewer is optional independent verification, not a standing third role.

## Architect Templates

### Compact Architect -> Builder Work Package

Use for Level 1 / tiny / docs-only / formatting-only / bounded maintenance.

````text
To: Builder
From: Architect
Role: Builder
Work Package: <任务名>
Mode: <implement-only | patch-only>
Execution Pace: Fast Track
Package Size: Compact
Goal:
- <要完成的结果>
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
Builder Responsibilities:
- Complete the approved result inside the boundary.
- Run the required verification or explain why it cannot run.
- Self-review before reporting when there is a meaningful diff.
Deliverable:
- Compact Completion Report: summary, files changed, verification, remaining risks, commit / push status.
- Spec alignment / drift flag only if product behavior or Spec Reference is involved.
Commit / Push:
- Not authorized unless User explicitly says otherwise.
````

### Standard / Detailed Architect -> Builder Work Package

Use for normal implementation, coherent feature packages, risky work, extended work, overnight work, resume, or reviewer-needed work.

````text
To: Builder
From: Architect
Role: Builder
Work Package: <任务名>
Mode: <implement-only | implement-extended | overnight-extended>
Execution Pace: <Fast Track | Strict Gate>
Package Size: <Standard | Detailed>
Outcome:
- <最终要交付的结果，不是逐步指令>
Authority:
- Builder may make local implementation decisions inside Scope as long as behavior, architecture direction, dependencies, and data/security boundaries do not change.
Scope:
- <允许范围>
Do Not:
- Do not commit or push unless User explicitly authorizes it.
- Do not expand scope.
- Do not modify files outside Expected Files To Change unless blocked.
- Do not make product, architecture, dependency, data model, auth, security, payment, or persistence decisions.
- If blocked, stop and report instead of guessing.
Context:
- Spec Reference: <PROJECT_SPEC.md / FEATURE_SPEC.md / AI_CONTEXT.md / README / User goal / N/A>
- Current Milestone:
- Next Milestone:
- Milestone Fit: matches Next Milestone / corrective maintenance / postponed exception approved by User
- Session Work Package Type:
- Work Package Rationale:
- Stop Point:
- Human Attention Cost: <low / medium / high and why>
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
Execution Principle:
- Complete the largest coherent portion of this approved Work Package before reporting.
- Do not stop after each small substep just to create extra handoffs.
- Delegate outcomes, not steps: use the implementation steps only as guidance, not as permission boundaries.
Implementation Guidance:
1. Create a brief local implementation plan before editing.
2. Implement the approved Work Package inside Scope.
3. Run required verification.
4. If verification fails for a local in-scope reason, fix and rerun.
5. Self-review the final diff / changed files before reporting.
6. Report final evidence for Architect Task Close Review.
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
- repeated validation failure after local repair attempts
- requirement unclear
- product / architecture / dependency / data / auth / security / persistence decision needed
- work no longer reviewable inside the approved boundary
Deliverable:
- Completion Report size: <Standard | Detailed>
- Summary
- Local implementation plan followed
- Files changed
- Verification results
- Verify / fix loop results, if any
- Self-review findings
- Remaining risks
- AI_CONTEXT.md updated: yes / no / not requested
- Commit / push status
- Spec alignment / drift flag when Spec Reference, product behavior, or drift risk is involved
Commit / Push:
- Do not commit or push unless User explicitly authorizes it.
````

### Architect -> Builder Resume Work Package

````text
To: Builder
From: Architect
Role: Builder
Work Package: <任务名> Resume
Mode: implement-extended-resume
Scope:
- Continue only the previously approved Work Package from checkpoint or reconstructed git diff.
Do Not:
- Do not commit or push unless User explicitly authorizes it.
- Do not expand scope.
- Do not modify files outside Expected Files To Change unless blocked.
- If the working state is unclear, stop and report instead of guessing.
Context:
- Previous approved Work Package:
- Last known checkpoint:
- Current git status / diff summary:
- Files already changed:
- Validation already run:
- Validation still needed:
- Known risks:
Instructions:
1. Reconstruct current state from files and git diff.
2. Compare against the previous approved Work Package.
3. Continue only remaining approved work.
4. Run verification and self-review before final report.
5. Stop if the current diff includes unrelated or unclear changes.
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
- Self-review findings
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
- Review only the implementation for the approved Work Package.
Do Not:
- Do not modify code.
- Do not command Builder.
- Do not expand review scope beyond requested files / diff.
- Do not make final architecture decisions.
Context:
- Approved Work Package:
- Task Risk Level:
- Builder Report:
- Files / diff to inspect:
- Verification evidence:
- Builder self-review evidence:
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
- Work Package satisfied: yes / no
- Scope expanded: no / details
- Verification acceptable: yes / no
- Self-review acceptable: yes / no / not needed
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
- Work Package satisfied: yes / no
- Scope expanded: no / details
- Prohibited files/actions respected: yes / no
## 2. Builder Evidence
- Local implementation plan reviewed: yes / no / not needed
- Verification reviewed: yes / no
- Verify / fix loop reviewed: yes / no / not triggered
- Self-review reviewed: yes / no / not needed
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
- Non-binding direction only. Not a Work Package / Task Card.
## 7. Design Alignment Review
- Not needed / completed / needed next
- Result if completed: STILL ALIGNED / DRIFT NEEDS CORRECTION / BETTER DIRECTION FOUND / N/A
## 8. Session Decision
- Continue current session / recommend fresh session / require fresh session
- Reason:
- Human attention cost next: low / medium / high
## 9. Next Session Starters

Required when fresh session is recommended or required.

Provide both:
- Next Architect Session Starter
- Next Builder Session Starter

Only omit one if User explicitly asked for only one.

Both starters must be complete, standalone, continuous, and copy-once usable.

The Builder Starter must not authorize implementation by itself unless the Architect is also intentionally issuing a Work Package / Task Card in the same closeout. If no next work is authorized yet, Builder Starter must say: wait for Architect Work Package / Task Card.
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

你的实际角色是 Tech Lead。Human 是 Product Owner，不是 Message Broker。
产品目标、MVP、Not Now、Current Milestone、Next Milestone 以 PROJECT_SPEC.md / FEATURE_SPEC.md 为准。
当前实现状态、已完成任务、风险和 TODO 以 AI_CONTEXT.md 为准。
历史聊天记录视为可能失效，只能作为临时参考。

请先恢复项目状态，然后等待我提供下一步目标。
不要直接生成 Builder Work Package / Task Card，除非我明确提出下一步需求。
不要把 AI_CONTEXT.md 的 Suggested Next Direction 当成正式任务；它只能作为讨论方向。
````

### Next Builder Session Starter

Output when fresh session is recommended or required.

````text
To: Builder
From: Architect
Role: Builder
Practical role: Senior Engineer
Mode: <implement-only | patch-only | implement-extended | overnight-extended | implement-extended-resume>

Required files to read:
- BUILDER.md
- AI_CONTEXT.md（如存在）
- <PROJECT_SPEC.md / FEATURE_SPEC.md only if named as Spec Reference>

Source of truth:
- Current implementation state: AI_CONTEXT.md and current files.
- Product goal / MVP / Not Now / Milestone: PROJECT_SPEC.md / FEATURE_SPEC.md when named as Spec Reference.
- This Builder Starter is execution context only unless Architect intentionally includes a Work Package / Task Card in this same closeout.
- If no Work Package / Task Card is included, Builder must restore repo state and wait for Architect authorization.
- Chat history is temporary reference only.

Current work:
- <具体下一步执行工作, or: No work authorized yet. Wait for Architect Work Package / Task Card.>

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

Builder Responsibilities:
- Create a brief local plan when meaningful.
- Implement only the approved work.
- Run verification.
- Self-fix local in-scope failures and rerun verification.
- Self-review before final report.

Deliverable:
- <Compact / Standard / Detailed> Completion Report
- Summary
- Local implementation plan followed, when meaningful
- Files changed
- Verification results
- Verify / fix loop results, if any
- Self-review findings
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
- Human attention cost:
## 5. Task Risk Level
Level 1 / Level 2 / Level 3 / Level 4
## 6. Builder Mode
implement-only / implement-extended / overnight-extended / implement-extended-resume / patch-only / N/A
## 7. Work Package
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
Work Package: <任务名> Completion Report
Mode: architect-gate
Report Size: Compact
Summary:
- <what changed>
Files changed:
- <path>: <purpose>
Verification:
- <commands or manual check>
- result: passed / failed / not run with reason
Self-review:
- passed / not needed / issue found: <details>
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
Work Package: <任务名> Completion Report
Mode: architect-gate
Report Size: <Standard | Detailed>
Scope:
- Report implementation result for the approved Work Package only.
Context:
- Branch:
- Commit:
- Push status:
- Git status:
- Approved Work Package:
Expected Files To Change:
- <approved expected files, only if Task Card named them or scope would otherwise be ambiguous>
Not Expected / Prohibited Files:
- <prohibited files, only if Task Card named them or explicit boundary matters>
Acceptance Criteria:
- <criteria from work authorization>
Local Implementation Plan Followed:
1. <step actually followed>
2. <step actually followed>
Verification:
- commands run:
- key result or key error output:
- manual check:
Verify / Fix Loop, if triggered:
- failure:
- fix:
- rerun result:
Self-review findings:
- scope check:
- behavior/regression check:
- validation check:
- remaining concerns:
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
Work Package: Resume <任务名>
Mode: implement-extended-resume
Scope:
- Continue only the previously approved Work Package.
Do Not:
- Do not expand scope.
- Do not commit or push unless User explicitly authorizes it.
- Do not modify files outside Expected Files To Change unless blocked.
- If working state is unclear, stop and report instead of guessing.
Checkpoint:
- Completed:
- Files changed so far:
- Validation already run:
- Validation not yet run:
- Known risks:
- Exact next step:
````

### Architect Escalation

````text
To: Architect
From: Builder
Role: Architect
Work Package: <任务名> Escalation
Mode: architect-decision-needed
Reason:
- <why Builder cannot safely continue inside the approved boundary>
Current State:
- Files changed:
- Validation run:
- Current blocker:
Boundary Check:
- Scope issue:
- Prohibited file/action issue:
- Risk level mismatch:
Decision Needed:
- <specific Architect decision needed>
Commit:
- Do not commit or push.
````

## Stable Rule

Do not add templates, roles, workflow stages, or handoff documents unless they solve a repeated real problem.

Templates should reduce Human coordination cost. If a template makes User carry messages that Architect or Builder should handle, the template is wrong.
