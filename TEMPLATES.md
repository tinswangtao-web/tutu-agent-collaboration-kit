# TEMPLATES

Version: 5.0.0-batched

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
- Commit: yes / no
- Push: yes / no
- Suggested message:
- User authorization required: yes

## User Decision
[None / 需要的业务取舍或授权]

## Next Step
[下一阶段完整结果]
```

正常阶段只使用：

```text
Architect → Builder → Architect
```