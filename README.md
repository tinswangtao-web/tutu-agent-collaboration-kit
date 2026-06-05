# Tutu Agent Collaboration Kit

Status: Stable
Version: v3.1.3

一个面向个人软件项目的轻量 AI 协作规则。目标是让不懂代码的 Project Owner 也能稳定协调多个可替换 AI 进行长期开发。

默认主线：

```text
User → Architect → Builder → Architect review → User
```

当任务风险较高、Architect 无法直接读取 repo，或代码级证据不足时，Architect 可以按需启用 Reviewer：

```text
User → Architect → Builder → Reviewer → Architect → User
```

核心原则：

```text
默认轻流程；按能力和风险逐级加审查。
```

## Files

- `START.md`：启动方式与日常流程。
- `ARCHITECT.md`：Architect 规则、Access Mode、Task Risk Level、handoff。
- `BUILDER.md`：Builder 执行、验证、报告与升级规则。
- `REVIEWER.md`：optional repo-aware 审查角色规则。
- `PROJECT_CONTEXT_TEMPLATE.md`：具体项目状态快照模板。

## Roles

### Primary roles

- `Architect`：决策、拆任务、定边界、判断流程、最终验收。
- `Builder`：执行已批准的实现任务。
- `User`：提供事实、转发信息、最终授权 commit / push / release / irreversible actions。

### Optional support

- `Reviewer`：按 Architect 要求进行独立审查，通常需要 repo / diff / file access。Reviewer 不是常驻角色，不做最终架构决策，不直接指挥 Builder，不擅自改代码。

## Operating Model

### Architect Access Mode

Architect 每次会话或任务开始时，MUST 根据实际 repo access 判断模式：

- `Remote Architect Mode`：不能直接读取本地 repo、文件、git diff 或命令输出。
- `Repo-aware Architect Mode`：可以直接读取 repo、查看代码 / diff。

如果不确定，默认 `Remote Architect Mode`。

### Task Risk Level

Architect MUST 在 handoff 前判断任务风险等级，并根据 Access Mode、Task Risk Level、confidence level 和 User constraints 决定是否启用 Reviewer。

| Level | Typical tasks | Reviewer |
|---|---|---|
| Level 1 Low-risk | docs / comments / formatting | No |
| Level 2 Normal | simple API / small service / small infra | Optional |
| Level 3 High-risk | multi-file business logic / core flow | Recommended when Architect lacks repo confidence |
| Level 4 Critical | schema / migration / auth / permission / ledger / security / production data risk | Strongly recommended / required when Architect lacks repo confidence |

## Project Context File

长期项目 MAY 维护短小状态快照，例如：

```text
docs/AI_CONTEXT.md
```

它只记录项目状态，不复制本规则。Remote Architect 无法读本地文件时，User 可以把该文件内容粘贴进新会话。

具体项目知识，例如业务实体、技术栈、数据库、模块边界、当前任务状态，应该写入 `AI_CONTEXT.md`，不要写入本协议主体。

## Transferable Blocks

所有跨 AI 交接内容 MUST 是完整、独立、连续、可一次复制的 block，包括：

- Architect → Builder task instruction
- Architect → Reviewer review instruction
- Builder → Architect completion report
- Builder → Architect escalation request
- Reviewer → Architect review report

块外只保留给 User 的简短判断。

## Collaboration Language

协作语言默认使用中文。代码标识、文件路径、命令、API 路径、字段名、错误码、技术术语、任务标题或简短标签，如果使用英文能减少歧义或提升效率，可以保留英文或中英混用。

不要为了格式化而整段改成英文；除非该角色判断英文更适合被直接粘贴到工具、issue、commit 或代码上下文中。

Architect / Builder / Reviewer 的任务单、评审报告、patch instruction、handoff note 和验收说明均遵守该约定。

## One-copy Forwarding

当需要 User 把内容转发给 Architect、Builder、Reviewer 或其他角色时，MUST 提供一个完整、独立、可一键复制的 fenced code block。

转发块之外可以有解释，但真正要转发的内容 MUST 在 fenced code block 内完整自洽，不能依赖块外说明。尤其是给 Builder 的任务单，MUST 避免散落在普通段落里。

给其他角色的转发指令至少包含：

```text
To: <Architect | Builder | Reviewer>
From: <User | Architect | Reviewer>
Role: <接收方角色>
Task: <任务名>
Mode: <implement-only | review-only | architect-gate | patch-only>

Scope:
- <允许范围>

Do Not:
- <禁止事项>

Context:
- <必要背景>

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

Deliverable:
- Summary
- Files changed
- Verification results
- Remaining risks

Commit:
- Do not commit unless explicitly instructed.
```

如果某项不适用，可以写 `N/A`，但不要省略关键边界。

给 Builder 的任务单还 MUST 明确：

- Do not commit，除非任务明确允许。
- Do not expand scope。
- Do not modify files outside expected list unless blocked。
- If blocked, stop and report instead of guessing。
- Expected files to change。
- Not expected / prohibited files。
- Verification commands。
- Builder 必须返回 summary、files changed、verification results、remaining risks。

---

## Design Philosophy

This protocol describes roles and capabilities, not specific AI products.

Core priorities:

1. Correctness
2. Transparency
3. Human Control
4. Efficiency
5. Token Cost

Never trade correctness for token savings.

The human project owner provides facts. Architect owns workflow decisions.

AI agents are interchangeable.

Transferable blocks MUST be self-contained. The receiver SHOULD NOT depend on hidden conversation context.
