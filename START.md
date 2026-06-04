# Start / 启动说明

## 1. Prepare the Project / 准备项目背景

Before starting, tell Architect the project context in plain language. / 开始前，用自然语言告诉 Architect 项目背景：

- What the project is / 这个项目是什么
- Who it is for / 给谁使用
- What problem it solves / 解决什么问题
- What should not be done now / 现在明确不做什么

Do not create extra project documents unless the project is long-term and truly needs them. / 除非项目长期维护且确实需要，否则不要额外创建项目文档。

## 2. Start Architect / 启动 Architect

Send this to the Architect session. / 把下面这段发给 Architect 会话：

```text
Please read / 请阅读:

ARCHITECT.md

You are the Architect for this project. / 你是这个项目的 Architect。

Project context / 项目背景:
[Describe the project here.]
[在这里描述项目。]

Your job is to decide Project Fit, Priority, Value / Cost, constraints, and Success Criteria.
你的职责是判断 Project Fit、Priority、Value / Cost、constraints 和 Success Criteria。

Do not implement. / 不要实现代码。
```

## 3. Start Builder / 启动 Builder

Send this to the Builder session. / 把下面这段发给 Builder 会话：

```text
Please read / 请阅读:

BUILDER.md

You are the Builder for this project. / 你是这个项目的 Builder。

Only implement approved tasks. / 只实现已经批准的任务。

Do not decide project fit, priority, architecture direction, dependencies, data model, security, payment, auth, or persistence.
不要决定 project fit、priority、architecture direction、dependencies、data model、security、payment、auth 或 persistence。

Do not commit or push unless User explicitly authorizes it. / 除非 User 明确授权，否则不要 commit 或 push。
```

## 4. Daily Flow / 日常流转

```text
User -> Architect -> Builder -> User
```

## 5. Stable Rule / 稳定规则

Do not add new roles, workflows, or documents unless there is a repeated real problem. / 除非出现重复的真实问题，否则不要新增角色、流程或文档。

When Architect gives a task to forward, copy only the complete forwardable instruction block. / 当 Architect 给出可转发任务指令时，只复制完整的可转发指令块。

When Builder asks User to forward content to Architect, Codex, or Reviewer, copy only the complete forwardable output block. / 当 Builder 要求 User 转发内容给 Architect、Codex 或 Reviewer 时，只复制完整的可转发输出块。

Builder completion reports should also be written as one complete block when they will be reviewed by Architect. / Builder 完成报告如果要交给 Architect 审查，也应写成一个完整块。
