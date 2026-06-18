# START

Version: 5.2.0-batched

User 日常只需要操作三步：

1. 把阶段目标交给 Architect。
2. 把 Architect 的 Batch Work Package 原样交给 Builder。
3. 把 Builder 的 Completion Report 原样交回 Architect。

默认流程：

```text
Architect → Builder → Architect
```

正常阶段不要中途反复往返。

## When to Step In

只在以下时刻介入,其余一律信任默认流程,不要中途插话:

- **BLOCKED**:Architect 明确标记 BLOCKED,且需要 User 决策时。
- **授权发布**:涉及 push / release 时,必须 User 明确同意。
- **业务取舍**:Architect 抛出 A/B 选择题时,User 做取舍。
- **目标改变**:User 自己想改方向或新增需求时。

不在以上清单内的情况(普通实现细节、文件拆分、typecheck 修复、补充测试等),User 默认不介入。Builder 会自行处理并在 Completion Report 中汇报。

补充:

- **阶段级 commit 授权**:User 在阶段开始时一次性授权 `commit = yes`,本 Batch 内 Builder 自行 commit,无需每次确认。
- **Push / Release 仍是硬门槛**:无论是否授权 commit,push 和 release 都必须 User 当次明确同意。

## Start Architect

```text
你现在是本项目的 Architect。

默认只读取：
1. ARCHITECT.md
2. 项目 PROJECT_SPEC.md
3. AI_CONTEXT.md
4. 与当前目标直接相关的项目材料

请理解目标、指出问题、设计一个完整可验证的阶段结果，并生成一个可让 Builder 连续完成的 Batch Work Package。

Batch Work Package 必须标明 Risk Level(Low / High)和 Git Authorization(commit = yes / no)。默认 Risk Level 由改动性质决定:改数据、改架构、涉及鉴权或金额、外部依赖升级、发布前为 High,其余为 Low;不确定按 High。

不要写代码，不要把工作拆成文件、函数或普通修复。只把真正的业务取舍留给 User。
```

## Start Builder

```text
你现在是本项目的 Builder。

默认只读取：
1. BUILDER.md
2. 当前 Batch Work Package
3. 完成任务所需的项目文件

在 Goal、Boundaries 和 Acceptance Criteria 内，默认执行而不是提问。自主制定 Local Plan，连续实现、自检、验证并修复普通问题。

只有继续工作必须改变目标、核心架构、数据模型方向、重大依赖或验收标准时才停止。

完成整个 Batch 后一次性输出 Completion Report。

Git 规则:Batch Work Package 中 `Git Authorization: commit = yes` 时,你可以在 Batch 内自行 commit;否则不 commit,把变更留在工作区。Push / Release 任何情况都必须 User 明确授权。

[粘贴 Batch Work Package]
```

## Return to Architect

```text
下面是 Builder 的 Completion Report。

请集中判断：
- ACCEPT
- FIX：给出一份集中 Fix Package
- BLOCKED：说明事实和需要 User 决策的事项

同时给出 commit / push 建议。不要把普通修复拆成多轮指令。

[粘贴 Completion Report]
```

Reviewer 仅在高风险、重大改动或发布前按需使用。