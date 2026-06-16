# Tutu Agent Kit

Version: 5.0.0-batched

一套给非程序员 Project Owner 使用的双 AI 协作规则。

目标很简单：

- 用较强、较贵的 AI 做方向、方案和验收；
- 用较便宜的 AI 批量完成实现；
- 尽量减少 User 在两个 AI 之间来回传话。

## Roles

- **User / Project Owner**：提出目标，决定业务取舍，授权 commit / push / release。
- **Architect**：理解需求，设计完整方案，创建批量 Work Package，验收结果。
- **Builder**：在既定目标和边界内自主实现、自检、自修，一次性交付。
- **Reviewer**：可选。只在高风险、重大改动或发布前提供独立检查。

## Default Flow

```text
User goal
→ Architect designs one complete stage
→ Builder implements the whole batch
→ Architect reviews once
→ optional focused fix
→ User authorization
```

正常阶段只应有两次人工转发：

1. Architect Work Package → Builder
2. Builder Completion Report → Architect

## Core Rules

1. **Architect owns outcome, architecture, boundaries and acceptance.**
2. **Builder owns execution, implementation details and self-fix.**
3. **One Work Package should produce one complete, testable stage result.**
4. **Do not split normal work by file, function, route, service or minor fix.**
5. **Builder stops only when the goal or architecture must change.**
6. **Reviewer is optional, not part of the default loop.**
7. **User is not a technical reviewer or message coordinator.**

## Files

- `START.md`：最短使用流程。
- `ARCHITECT.md`：贵 AI 的角色和行为。
- `BUILDER.md`：便宜 AI 的角色和行为。
- `TEMPLATES.md`：三个常用交接模板。
- `REVIEWER.md`：可选独立审查规则。
- `AI_CONTEXT_TEMPLATE.md` / `PROJECT_SPEC_TEMPLATE.md`：可选项目文档模板。

规则是否值得保留，只看一件事：它是否让两个 AI 更清楚、更自主，并减少 User 的操作成本。