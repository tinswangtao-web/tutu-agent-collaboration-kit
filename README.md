# Tutu Agent Kit

Version: 4.3.2-efficiency-slim

一套给非程序员 Project Owner 使用的 AI 协作规则。目标不是完美协议，而是让用户更省心地推进小型软件项目。

## Core Idea

User 是 **Project Owner**，不是技术审查员，也不是 Architect 和 Builder 之间的人工中转站。

只保留四个角色：

- **User / Project Owner**：提出目标，确认业务取舍，授权 commit / push / release。
- **Architect**：判断方向，拆任务，创建 Work Package，验收，决定下一步。
- **Builder**：按 Work Package 实现，提交 Completion Report，不做验收和授权。
- **Reviewer**：独立检查问题，只给证据和建议，不决策、不实现、不授权。

拿不准下一步时，默认回到 Architect。

## Five Hard Rules

1. **Architect owns decisions and Work Package.**
2. **Builder owns implementation and Local Plan.**
3. **Builder never accepts DONE.**
4. **Builder never authorizes commit / push.**
5. **Every task returns to Architect for Close Review.**

补充硬边界：新会话永远先开 Architect；AI_CONTEXT.md 只记录状态，不授权实现。

## Files

- `START.md`：日常入口和最短操作路径。
- `ARCHITECT.md`：Architect 规则。
- `BUILDER.md`：Builder 规则。
- `REVIEWER.md`：Reviewer 规则。
- `TEMPLATES.md`：可复制模板。
- `AI_CONTEXT_TEMPLATE.md`：项目状态模板。
- `PROJECT_SPEC_TEMPLATE.md`：项目设计模板。

日常操作先看 `START.md`。角色边界看对应角色文件。

## Release Principle

新增规则必须明显帮助：防止 Builder 越权、防止任务不验收、防止未授权 commit / push、防止新会话丢上下文、减少 User 技术判断负担。
