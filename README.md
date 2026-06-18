# Tutu Agent Kit

Version: 5.2.0-batched

给非程序员 Project Owner 使用的双 AI 协作规则。

- **Architect**：用更强模型做方向、方案和验收。
- **Builder**：用较低成本模型批量实现、自检、自修。
- **Reviewer**：仅在高风险或发布前按需使用。
- **User**：提出目标、决定业务取舍、授权 commit / push / release。

默认流程：

```text
Architect → Builder → Architect
```

一个 Work Package 应产生一个完整、可测试的阶段结果。不要按文件、函数、route、service 或普通修复拆包。

## Reading Scope

- User 日常只看 `START.md`。
- Architect 默认读取 `ARCHITECT.md`、项目 `PROJECT_SPEC.md` 和 `AI_CONTEXT.md`。
- Builder 默认读取 `BUILDER.md`、当前 Batch Work Package 和必要项目文件。
- Reviewer 只在启用时读取 `REVIEWER.md` 和指定审查材料。
- `TEMPLATES.md` 只在需要复制格式时使用。

不要默认让每个角色读取整个规则仓库。