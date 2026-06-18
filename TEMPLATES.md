# TEMPLATES

Version: 5.2.0-batched

只保留三个日常模板。

## Batch Work Package

```text
# Batch Work Package

## Goal
[本阶段完整结果]

## Context
[关键背景与已确认决定]

## Boundaries
- Must keep:
- Do not change:

## Acceptance Criteria
- 
- 

## Risks
- 

## Risk Level
[Low / High。改数据、改架构、涉及鉴权或金额、外部依赖升级、发布前为 High,其余为 Low;不确定按 High。]

## Git Authorization
[commit = yes / commit = no。yes 时 Builder 可在 Batch 内自行 commit;push / release 始终需 User 当次授权。]

## Required Evidence
- 变更摘要
- 逐项验收证据
- 实际验证结果
- 剩余风险

Builder 在以上边界内自主决定实现步骤、相关文件、测试和普通修复。完成整个 Batch 后一次性提交 Completion Report。
```

## Completion Report

```text
# Completion Report

## Summary
[完成的阶段结果]

## Files Changed
- 

## Acceptance Evidence
- AC1:
- AC2:

## Verification
- command / check:
- result:

## Risks / Limitations
- None / list

## Decisions Needed
- None / 仅列必须改变目标或架构才能继续的事项

## Git Status
[如可用]
```

## Architect Review

```text
# Architect Review

## Decision
ACCEPT / FIX / BLOCKED

## Evidence Assessment
[是否足以证明 Acceptance Criteria]

## Fix Package
[仅在 FIX 时提供一份集中修复清单]

## Git Recommendation
- Commit status: [已按 Git Authorization 执行 / 未 commit,说明原因]
- Push: yes / no(User 当次授权)
- Suggested message:
- User authorization required: push 或 release 时填 yes

## User Decision
[None,或以下形式之一]
- 是非题:建议 X,理由一句话。是否同意?
- 选择题:选项 A(权衡) / 选项 B(权衡)。推荐:?

## Next Step
[下一阶段完整结果]
```

正常阶段只使用：

```text
Architect → Builder → Architect
```