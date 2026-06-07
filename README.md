# Tutu Agent Collaboration Kit

Status: Stable
Version: 4.2.1

一个面向个人软件项目的轻量 AI 协作规则。目标是让不懂代码的 Project Owner 也能稳定协调多个可替换 AI，长期推进产品和代码，同时避免让 Human 变成消息中转和技术调度员。

## Core Flow

```text
Brainstorm / Architect Discovery Mode
-> PROJECT_SPEC.md or FEATURE_SPEC.md
-> Architect Planning
-> Builder Work Package / Task Card
-> Builder local plan
-> Builder execution
-> Verify / Self-Fix Loop
-> Builder Self Review
-> Completion Report
-> Architect Task Close Review
-> User-authorized commit / push
```

核心原则：

- Spec First, Plan Second, Code Last.
- Human is the Product Owner, not the Message Broker.
- Maximize AI autonomy while preserving human control.
- Delegate outcomes, not steps.
- Architect owns product, planning, work package boundaries, risk, review, and DONE.
- Builder owns local planning, implementation, verification, self-fix, self-review, and evidence inside the approved Work Package / Task Card.
- Reviewer is optional and verifies only what Architect requests. It is not a standing third role.
- User owns final authorization for commit / push / release / irreversible actions.
- Chat history is temporary cache. Durable state lives in project files.

## Files

- `START.md`: 启动方式与日常流程。
- `ARCHITECT.md`: Architect 规则、Discovery / Execution Mode、risk、handoff、review。
- `BUILDER.md`: Builder 执行、验证、自修复、报告与升级规则。
- `REVIEWER.md`: optional repo-aware 审查角色规则。
- `TEMPLATES.md`: Architect / Builder 输出模板，只在生成对应 block 时读取。
- `PROJECT_SPEC_TEMPLATE.md`: `PROJECT_SPEC.md` / `FEATURE_SPEC.md` 模板。
- `PROJECT_CONTEXT_TEMPLATE.md`: `AI_CONTEXT.md` 项目状态快照模板。

## Source Of Truth

- `PROJECT_SPEC.md` / `FEATURE_SPEC.md`: 产品目标、目标用户、用户流程、MVP、Not Now、Current Milestone、Next Milestone。
- `AI_CONTEXT.md`: 当前实现状态、已完成任务、架构/实现决策、风险、TODO、建议方向。
- Work Package / Task Card: Builder 的唯一执行接口。
- Git state / diff: 当前代码证据。

如果 Spec 和 `AI_CONTEXT.md` 冲突：产品意图以 Spec 为准；当前实现状态以 `AI_CONTEXT.md` 和代码为准；Architect 判断是否需要更新文件。

## Reading Model

Do not load every rule for every task.

- Every new session must reread the minimum role rules from current files. Do not rely on a previous chat's memory of the rules.
- Always-On Core: role boundary, source of truth, Work Package / Task Card, DONE, commit / push gate.
- Conditional Rules: read only when triggered by Discovery, Spec Quality Gate, Strict Gate, extended / overnight, Reviewer, closeout handoff, or commit-boundary work.
- Templates: read `TEMPLATES.md` only when generating the matching copy-once block.

Default to Fast Track unless risk triggers Strict Gate. Fast Track may still authorize a coherent Work Package when the work is low-risk and reviewable.

## Tool Adaptation

核心逻辑不变：Spec -> Architect planning -> Builder closed-loop execution -> Architect Review -> User authorization。具体编排方式按工具能力调整。

### Manual Mode

- 用于对话式 AI 或无 repo 访问的工具。
- User 手动复制 Work Package / Report 在不同会话之间传递。
- Transferable Blocks 必须完整、独立、可一次复制。

### Repo-Aware Single Agent Mode

- 用于 Cursor、Windsurf 等有 repo 访问的单 agent 工具。
- Agent 可以直接读取 `PROJECT_SPEC.md`、`AI_CONTEXT.md`、git diff 和相关文件。
- Transferable Blocks 可以更短，但 Work Package / Review / Commit Gate 不变。

### Native Multi-Agent Mode

- 用于 Codex、Antigravity 等支持多 agent 或子任务编排的工具。
- Architect 和 Builder 可以在同一环境中通过 agent message 传递 Work Package / Report。
- Reviewer 如被使用，仍然只审查 Architect 指定的 scope / diff / evidence。
- 工具可以自动化传递、整理和状态恢复；不能绕过 User 对 Spec、DONE、Work Package、commit / push、release、irreversible actions 的 gate。

## Quick Start

日常启动见 `START.md`。角色规则以 `ARCHITECT.md`、`BUILDER.md`、`REVIEWER.md` 为准；模板以 `TEMPLATES.md` 为准。

## Stable Rule

不要新增角色、流程或文档，除非它解决重复出现的真实问题。不要新增 `TASK_PACKAGE.md`、`SESSION_HANDOFF.md`、`NEXT_TASK.md` 等额外交接文件。
