# Tutu Agent Collaboration Kit

Status: Stable
Version: 4.0.6

一个面向个人软件项目的轻量 AI 协作规则。目标是让不懂代码的 Project Owner 也能稳定协调多个可替换 AI，长期推进产品和代码。

## Core Flow

```text
Brainstorm / Architect Discovery Mode
→ PROJECT_SPEC.md
→ Architect Execution Mode
→ Builder Task Card
→ Builder implementation
→ Architect review
→ User-authorized commit / push
```

核心原则：

- Spec First, Plan Second, Code Last.
- Architect owns product, planning, task boundaries, risk, review, and DONE.
- Builder executes approved Task Cards only.
- Reviewer is optional and only verifies what Architect requests.
- User provides facts and owns final authorization for commit / push / release / irreversible actions.
- Chat history is temporary cache. Durable state lives in project files.

## Files

- `START.md`: 启动方式与日常流程。
- `ARCHITECT.md`: Architect 规则、Discovery / Execution Mode、risk、handoff、review。
- `BUILDER.md`: Builder 执行、验证、报告与升级规则。
- `REVIEWER.md`: optional repo-aware 审查角色规则。
- `PROJECT_SPEC_TEMPLATE.md`: Brainstorm / Discovery Mode 输出的 `PROJECT_SPEC.md` 模板。
- `PROJECT_CONTEXT_TEMPLATE.md`: `AI_CONTEXT.md` 项目状态快照模板。

## Source Of Truth

- `PROJECT_SPEC.md` / `FEATURE_SPEC.md`: 产品目标、目标用户、用户流程、MVP、Not Now、Current Milestone、Next Milestone。
- `AI_CONTEXT.md`: 当前实现状态、已完成任务、架构/实现决策、风险、TODO、建议方向。
- Task Card: Builder 的唯一执行接口。
- Git state / diff: 当前代码证据。

如果 Spec 和 AI_CONTEXT 看起来冲突：

- 产品意图以 Spec 为准。
- 当前实现状态以 AI_CONTEXT 和代码为准。
- Architect 负责判断是否需要更新 Spec 或 AI_CONTEXT。

## Modes

Architect 只有一个角色，但有两个工作状态：

- `Discovery Mode` / Brainstorm: 产品发现、用户流程、MVP、Not Now、milestone 定义。
- `Execution Mode`: 读取 Spec，判断 fit / priority / risk，拆 Task，验收 Builder。

Brainstorm 只有在产出可审查的 `PROJECT_SPEC.md` / `FEATURE_SPEC.md` 草稿，并由 User 确认或要求具体修改后，才算完成。

## Session Work Package

一个会话不是机械地等于一个小 Task，而是一个可控、可验收的 work package。

- 小型、低风险、强相关任务可以合并在同一会话。
- 中等风险任务聚焦一个 coherent milestone 或少量强相关任务。
- 高风险、关键或复杂任务拆成 gated tasks，并在每个 gate 后 review。
- 避免两个极端：为每个 tiny task 开新会话，或把太多无关/高风险任务塞进同一会话。

Architect planning should state:

```text
Session Work Package Type:
Why this size:
Stop point:
```

Task Card and Completion Report should be sized by risk:

- Compact: Level 1 / tiny / docs-only.
- Standard: Level 2 / normal implementation.
- Detailed: Level 3-4 / extended / overnight / resume / reviewer-needed.

## Risk And Sessions

- Level 1: docs / comments / formatting. Usually current session.
- Level 2: small service / simple API / small infra. Current or fresh session by scope.
- Level 3: high-risk business logic / core flow. Default gated; may stay current only when narrow, understood, verifiable, and reviewable.
- Level 4: schema / migration / auth / permission / security / ledger / production data. Short gated tasks; fresh session strongly preferred and required when context is noisy or irreversible risk exists.

## Commit / Push Gate

Task completion and git publication are separate.

```text
Builder implementation
→ Builder Self Check
→ Architect Task Close Review
→ Architect Decision: DONE
→ User authorizes commit / push
```

Rules:

- Builder never commits or pushes unless User explicitly authorizes it.
- Architect may recommend commit / push after `DONE`.
- Commit / push is not proof of task completion.
- Task completion is decided by Architect review, not by git state.

## Minimal Context

Read only the smallest reliable context needed:

- Discovery: User rules, product input, existing Spec if present.
- Architect Execution: `ARCHITECT.md`, relevant Spec, `AI_CONTEXT.md`, current User goal.
- Builder: `BUILDER.md`, `AI_CONTEXT.md`, approved Task Card; read Spec only when Task Card names it.
- Reviewer: `REVIEWER.md`, Architect review instruction, requested diff/files/evidence.

## Stable Rule

不要新增角色、流程或文档，除非它解决重复出现的真实问题。

不要新增 `TASK_PACKAGE.md`、`SESSION_HANDOFF.md`、`NEXT_TASK.md` 等额外交接文件。产品规格写入 `PROJECT_SPEC.md` / `FEATURE_SPEC.md`；长期项目状态写入 `AI_CONTEXT.md`。

Transferable blocks must be complete, standalone, continuous, and copy-once usable.
