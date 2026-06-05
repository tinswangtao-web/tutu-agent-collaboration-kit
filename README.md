# Tutu Agent Collaboration Kit

Status: Stable
Version: 3.2.1

一个面向个人软件项目的轻量 AI 协作规则。目标是让不懂代码的 Project Owner 也能稳定协调多个可替换 AI 进行长期开发。

默认主线：

```text
User → Architect → Builder → Architect review → User
```

低风险小任务可以继续当前会话。独立阶段、高风险任务、长任务、过夜任务、复杂 resume 或上下文明显变脏时，推荐或要求开启新的 Architect 会话和新的 Builder 会话：

```text
Architect closes Task → session decision → continue current session OR fresh Architect / Builder sessions
```

当任务风险较高、Architect 无法直接读取 repo，或代码级证据不足时，Architect 可以按需启用 Reviewer：

```text
User → Architect → Builder → Reviewer → Architect → User
```

核心原则：

```text
默认轻流程；按能力和风险逐级加审查。
AI_CONTEXT.md 只记录长期状态变化；聊天记录只是临时缓存。
```

## Files

- `START.md`：启动方式与日常流程。
- `ARCHITECT.md`：Architect 规则、Access Mode、Task Risk Level、handoff。
- `BUILDER.md`：Builder 执行、验证、报告与升级规则。
- `REVIEWER.md`：optional repo-aware 审查角色规则。
- `PROJECT_CONTEXT_TEMPLATE.md`：`AI_CONTEXT.md` 项目状态快照模板。

## Roles

### Primary roles

- `Architect`：决策、拆任务、定边界、判断流程、最终验收。
- `Builder`：执行已批准的实现任务。
- `User`：提供事实、转发信息、最终授权 commit / push / release / irreversible actions。

### Optional support

- `Reviewer`：按 Architect 要求进行独立审查，通常需要 repo / diff / file access。Reviewer 不是常驻角色，不做最终架构决策，不直接指挥 Builder，不擅自改代码。

### Session handoff boundaries

- Old Architect：Task Close Review、确认 `AI_CONTEXT.md` 是否需要更新，并判断继续当前会话、建议新会话或要求新会话；只有新会话被建议或要求时才输出下一 Architect / Builder 会话启动词。
- New Architect：先等待用户新的下一阶段目标，再进行 Planning 并生成新的 Task Card。
- Builder：只执行 approved Task Card；新 Builder 会话读取规则和 `AI_CONTEXT.md` 后等待任务。
- `AI_CONTEXT.md`：长期项目状态记忆。
- Chat history：临时缓存，不作为长期项目记忆。
- Context pollution：Architect 最终判断是否需要新会话；Builder 负责 flag；User 可以要求新会话但不负责技术判断。

Fresh sessions are:

- optional for tiny / Level 1 work with clean context
- recommended for independent normal tasks or phase changes
- required for Level 3 / Level 4, long / overnight / complex resume work, dirty context, or explicit User reset request

### Design alignment

Architect SHOULD periodically run a lightweight Design Alignment Review after several related tasks, milestone / phase boundaries, long / overnight work, complex resume work, or when Builder / User flags drift.

Design baseline, in order:

- `PROJECT_DESIGN.md`, if present
- `AI_CONTEXT.md` latest decisions and architecture notes
- README / product docs / explicit User goals
- current Task Card

Possible outcomes:

- `STILL ALIGNED`：continue.
- `DRIFT NEEDS CORRECTION`：open a correction Task Card before further expansion.
- `BETTER DIRECTION FOUND`：present a design update proposal to User; do not silently accept the new direction.

Builder may flag design drift, but Architect owns the review and User confirms accepted direction changes.

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

### Task Granularity

User MAY request preferred task granularity:

- `short task`：先快速验证方向，减少不确定性。
- `extended task`：让 Builder 连续执行一个完整工作包，提高效率。
- `overnight task` / `过夜任务`：让 Builder 在睡前执行一组有限、低风险、预先批准的 unattended task queue。
- `Architect decides`：由 Architect 按风险和清晰度决定。

Architect MUST treat User granularity as preference, not automatic approval.

如果 User 用自然语言说“给 Builder 开一个过夜任务”、“overnight task”、“睡前让 Builder 跑一晚”、“长任务跑一晚上”，Architect 应识别为 `overnight-extended` 偏好，但只能在低风险、范围清楚、可频繁 checkpoint、无需 Builder 自行规划时批准。

Use short task when:

- Scope is unclear.
- Risk is Level 3 with uncertainty, or Level 4.
- Expected files cannot be listed.
- Verification cannot be named.
- Task requires product / architecture judgment.
- User needs quick confirmation before more work.

Use extended task when:

- Scope is clear.
- Risk is Level 1 or Level 2.
- Expected and prohibited files can be listed.
- Acceptance criteria are concrete.
- Verification commands are known.
- Work can be split into resumable checkpoints.
- Builder can continue without making new product / architecture decisions.

Extended task is for batching already-decided work. Short task is for reducing uncertainty.

Builder modes include:

- `implement-only`
- `implement-extended`
- `overnight-extended`
- `implement-extended-resume`
- `patch-only`
- `review-only`
- `architect-gate`

`overnight-extended` 不是让 Builder 自己设计下一步；它只能执行 Architect 预先列出的有限队列。队列完成、风险升高、验证失败或需要架构判断时，Builder 必须停止并输出 completion report / handoff，等待 morning Architect review。

## Project Context File

长期项目 SHOULD 维护短小状态快照，例如：

```text
AI_CONTEXT.md
```

它只记录项目状态，不复制本规则。Remote Architect 无法读本地文件时，User 可以把该文件内容粘贴进新会话。

具体项目知识，例如业务实体、技术栈、数据库、模块边界、当前任务状态，应该写入 `AI_CONTEXT.md`，不要写入本协议主体。

推荐结构：

```md
# AI_CONTEXT

## Current Project Status

## Completed Tasks

## Latest Decisions

## Current Architecture Notes

## Known Risks / TODO

## Suggested Next Direction
```

`Suggested Next Direction` 只是建议方向，不等同于正式下一任务。不要新增 `TASK_PACKAGE.md`、`SESSION_HANDOFF.md`、`NEXT_TASK.md` 等额外交接文件。

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
Mode: <implement-only | implement-extended | overnight-extended | implement-extended-resume | review-only | architect-gate | patch-only>

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

给 Builder 的 extended task 还 MUST 明确：

- Timebox / checkpoint cadence，例如 30-90 minutes，或每 20-40 minutes 形成 checkpoint。
- Resume safety：中断后必须能通过 git diff、checkpoint、handoff note 续上。
- Stop conditions：风险升高、expected files 不够、需要改 prohibited files、需要新增 dependency、连续验证失败、需要猜需求时停下报告。
- Checkpoint fields：current task、completed steps、files changed so far、remaining steps、validation run、validation pending、known risks / blockers、exact next step。
- Level 4 MUST NOT use extended task / overnight task。

给 Builder 的 overnight task 还 MUST 明确：

- finite pre-approved task queue。
- per-item expected files / prohibited files。
- per-item acceptance criteria / verification。
- checkpoint after every queue item。
- maximum unattended duration or stop-after queue rule。
- morning review instruction。

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
