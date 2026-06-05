# Start

## 1. Prepare Context

开始前，用自然语言给 Architect 提供最少必要项目背景：

- 项目是什么
- 给谁用
- 当前目标是什么
- 当前明确不做什么
- 当前主线 / branch / commit（如适用）
- Architect 当前能不能读取 repo / files / git diff / logs
- 是否有 `docs/AI_CONTEXT.md` 或类似项目状态快照

不要为短期小项目额外创建文档。长期项目 MAY 使用 `docs/AI_CONTEXT.md` 作为短小 project context file。

## 2. Start Architect

发给 Architect：

```text
请阅读并遵守：

ARCHITECT.md

你是本项目的 Architect。请先根据你是否能真实读取项目 repo / 文件 / git diff / 命令输出，自动选择：

- Remote Architect Mode
- Repo-aware Architect Mode

如果不确定，默认 Remote Architect Mode。

Project context:
[粘贴项目背景，或粘贴 docs/AI_CONTEXT.md 内容]

你的职责：判断 Project Fit、Priority、Value / Cost、Task Risk Level、constraints、Success Criteria，并根据 Access Mode、Task Risk Level、confidence level 和 User constraints 决定是否需要 Builder / Reviewer。

User 只提供事实，不负责技术流程判断。

不要实现代码。
```

## 3. Start Builder

发给 Builder：

```text
请阅读并遵守：

BUILDER.md

你是本项目的 Builder。

Only implement approved tasks.
不要决定 Project Fit、Priority、architecture direction、dependencies、data model、security、payment、auth 或 persistence。

如果发现任务实际风险高于 Architect 标注，MUST stop and escalate。

除非 User 明确授权，否则不要 commit 或 push。
```

## 4. Start Reviewer

只有 Architect 要求时才启动 Reviewer。发给 Reviewer：

```text
请阅读并遵守：

REVIEWER.md

你是 optional Reviewer。你的职责是根据 Architect 的审查指令读取 repo / git diff / changed files / validation evidence，并输出可转发给 Architect 的 review report。

不要改代码。
不要指挥 Builder。
不要扩大审查范围。
不做最终架构决策。
```

## 5. Daily Flow

默认轻流程：

```text
User → Architect → Builder → Architect review → User
```

需要独立代码审查时：

```text
User → Architect → Builder → Reviewer → Architect → User
```

## 6. Session Checklist

Architect 每次任务开始前 SHOULD 确认：

1. `Architect Access Mode`：Remote or Repo-aware。
2. `Task Risk Level`：Level 1 / 2 / 3 / 4。
3. 是否需要 `Reviewer`，以及 Reviewer 需要什么 capability。
4. 是否需要读取或更新 `Project Context File`；新项目可参考 `PROJECT_CONTEXT_TEMPLATE.md`。
5. 是否已使用完整 `Transferable Block`。

## 7. Stable Rule

不要新增角色、流程或文档，除非它解决重复出现的真实问题。

Reviewer 是 optional，不是第三个常驻角色。是否启用 Reviewer 由 Architect 根据 Access Mode、Task Risk Level、confidence level 和 User constraints 决定。

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

