# TEMPLATES

Version: 4.3.2-efficiency-slim

只保留日常最常用模板。模板字段可以英文，说明默认中文。

---

## Architect Work Package for Builder

```text
# Work Package for Builder

Role: Builder
Source: Architect

## Goal

[本次任务目标]

## Scope

Allowed:
- 

Out of scope:
- 

## Files / Areas

May modify:
- 

Do not modify:
- 

## Acceptance Criteria

- 
- 

## Constraints / Risks

- 

## Required Builder Output

1. Local Plan before implementation. Minimum fields: Understanding / Files to Touch / Steps / Risks.
2. Completion Report after implementation.
3. Do not commit or push.
4. Return to Architect for Close Review.
```

---

## Builder Completion Report

```text
# Completion Report

## Summary

[做了什么]

## Files Changed

- 

## Verification

- [运行了什么检查 / 未运行原因]

## Risks / Limitations

- 

## Architect Decisions Required

无。但仍需 Architect Close Review 才能判断 DONE / commit / push。

## User Decisions Required

无 / [需要用户判断的事项]

## Implementation Confidence

High / Medium / Low

说明：Implementation Confidence 只代表本地实现信心，不代表 DONE、验收或 commit / push 授权。

## Git Status

[git status --short，如可用]

## Handoff to Architect

请 Architect 基于本报告做 Task Close Review，并判断 DONE / NEEDS FIX / BLOCKED、Commit / Push Gate 和下一步。
```

---

## Architect Task Close Review

```text
# Task Close Review

Role: Architect

## Scope Check

- Matches Work Package: yes / no
- Out-of-scope changes: none / list
- For Nano Task: Nano boundary respected: yes / no / not applicable

## Verification Check

- Acceptable: yes / no / not enough evidence
- Notes:

## Decision

DONE / NEEDS FIX / BLOCKED

## Required Fixes

- None / list

## Commit / Push Gate

- Commit recommended: yes / no
- Push recommended: yes / no
- Commit boundary:
- Suggested commit message:
- User authorization required: yes / no
- If Architect cannot operate repo: provide exact commands for User to run manually

## AI_CONTEXT.md

- Needs update: yes / no
- Required update:

## Session Decision

continue current session / prepare Next Architect Session Starter / stop and wait for User

## Next Step

[下一步]
```

---

## Nano Task for Builder

```text
# Nano Task

Role: Builder

只做下面这一件事，不要扩大范围，不要 commit，不要 push。

## Task

[小任务]

## Output

完成后输出 Nano Task Report。
```

---

## Nano Task Report

```text
# Nano Task Report

## Done

[完成内容]

## Files Changed

- 

## Verification

- 

## Risks

- None / list

## Git Status

[git status --short，如可用]

Note: 仍需 Architect 按 Task Close Review 做 Nano Task Close Review，才可判断 DONE / commit / push。
```

---

## Next Architect Session Starter

```text
你现在是 Architect。

这是一个新的 Architect session。User 是 Project Owner，不是技术审查员或消息搬运工。请先恢复上下文，不要写代码，不要生成 Builder 执行任务，直到你完成状态判断。

请优先阅读：
1. ARCHITECT.md
2. AI_CONTEXT.md
3. PROJECT_SPEC.md（如存在）
4. 最近的 Task Close Review / Completion Report（如有）

如角色边界或日常流程不清楚，再参考 README.md / START.md。

恢复后请输出：
1. Current State Summary
2. Open Decisions
3. Suggested Next Step
4. 是否需要生成新的 Work Package for Builder

规则：
- Architect 负责判断和 Work Package。
- Builder 只按 active Architect Work Package 执行。
- 不要提前授权 Builder。
- 需要 Builder 工作时，由你先创建 Work Package，再生成 Work-authorizing Builder Starter。

请用中文为主，Protocol Keywords 保持英文。
```

---

## Work-authorizing Builder Starter

```text
你现在是 Builder。

这是 active Architect session 生成的 Work-authorizing Builder Starter。
你只能按下面的 Work Package 执行，不要扩大范围，不要 commit，不要 push。

执行前输出 Local Plan，执行后输出 Completion Report。

[粘贴 Work Package for Builder]
```

---

## Restore-only Builder Starter

```text
你现在是 Builder。

这是 Restore-only Builder Starter，只用于恢复上下文，不授权实现。

请阅读相关文档和上下文后，只输出：
1. 你理解的当前项目状态；
2. 你认为缺少哪些信息；
3. 等待 active Architect 的 Work Package。

不要修改文件，不要执行任务，不要 commit，不要 push。
```

---

## Release Gate Review

```text
你现在是 Reviewer。

请只做 Release Gate Review，不做开放式优化建议。

审查目标只有三个：
1. 是否存在会导致 Builder 越权的硬冲突；
2. 是否存在会导致流程无法闭环的硬冲突；
3. 是否存在会导致新会话提前授权 Builder 或绕过 commit / push gate 的硬冲突。

如果没有 blocking issue，请判定 Ready for Production。

输出：

## Verdict
Ready for Production / Not Ready

## Blocking Issues
None / list

## Required Fixes
None / list

## Final Recommendation
直接发布 / 修复后发布
```
