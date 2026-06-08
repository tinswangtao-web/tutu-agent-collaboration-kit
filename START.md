# START

Version: 4.3.2-efficiency-slim

这是日常使用入口。多数情况下，只需要按这里操作。

## 0. Project Owner Daily Flow

你不是技术审查员，也不是消息搬运工。日常只按这个顺序操作：

1. 有新需求或不确定下一步 → 找 Architect。
2. Architect 给 Work Package → 转给 Builder。
3. Builder 给 Completion Report → 原样转回 Architect。
4. Architect 判断 DONE / NEEDS FIX / BLOCKED。
5. 需要 commit / push / release → 你只做授权，不做技术验收。
6. 上下文变长 → 先开新 Architect，不直接开新 Builder。

如果不知道该找谁，默认找 Architect。

## 1. 开始新项目 / 新需求

给 Architect：

```text
你现在是 Architect。

请按 ARCHITECT.md 工作：先阅读项目目标和相关文档，不要写代码。
你的任务是澄清需求、判断最小可执行范围、生成 Work Package for Builder，并明确验收标准、风险和需要我决策的事项。

请用中文为主，Protocol Keywords 保持英文。
```

## 2. 给 Builder 执行任务

只有在 Architect 已经生成 Work Package 后，才给 Builder：

```text
你现在是 Builder。

请按 BUILDER.md 工作，只执行下面的 Architect Work Package。
不要扩大范围，不要重构无关代码，不要判断 DONE，不要 commit，不要 push。

执行前输出 Local Plan；执行后输出 Completion Report。

[粘贴 Architect Work Package]
```

## 3. Builder 完成后

把 Builder 的 Completion Report 转回 Architect：

```text
你现在继续作为 Architect。

下面是 Builder 的 Completion Report。请做 Task Close Review：检查 scope / verification，判断 DONE / NEEDS FIX / BLOCKED，处理 Commit / Push Gate、AI_CONTEXT.md 和下一步。

[粘贴 Builder Completion Report]
```

## 4. Nano Task

Nano Task 只适合小修、小文案、小配置、单点修改。

可以直接给 Builder：

```text
你现在是 Builder。

这是 Nano Task。只做下面这一件事，不要扩大范围，不要 commit，不要 push。
完成后输出 Nano Task Report。

Task:
[写清楚小任务]
```

Nano Task 完成后，仍然必须转 Architect 做 Nano Task Close Review。
如果需要 commit / push，也只能在 Architect Close Review 和 User Authorization 后进行：

```text
你现在是 Architect。

下面是 Builder 的 Nano Task Report。请按 Task Close Review 做 Nano Task Close Review，重点检查是否越过 Nano boundary，并判断 DONE / NEEDS FIX / BLOCKED、Commit / Push Gate 和下一步。

[粘贴 Nano Task Report]
```

## 5. 新会话交接

旧 Architect 会话关闭时，只让它生成：

```text
Next Architect Session Starter
```

不要让旧 Architect 直接生成新的 Work-authorizing Builder Starter。

新 Architect 会话恢复上下文后，再决定是否生成 Builder Starter。

## 6. AI_CONTEXT.md

`AI_CONTEXT.md` 记录项目状态、最近任务、当前决策、下一步建议。

它不是授权文件。只有 active Architect 生成的 Work Package 才能授权 Builder 实现。

## 7. 最小闭环

```text
Architect → Builder → Architect Close Review → User authorization → Commit / Push → AI_CONTEXT.md → Next Architect
```
