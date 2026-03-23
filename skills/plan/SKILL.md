---
name: plan
description: 基于当前分支类型，结对生成对应的规划文档
allowed-tools:
  - Bash
  - Read
  - Write
  - Glob
---

# Plan Workshop

## 前置条件

1. 确认 `CLAUDE.md` 和 `.claude/constitution.md` 存在，否则暂停提示用户先运行 `/claude-md`
2. 读取当前分支名，提取类型前缀
3. 若无法识别类型，询问用户

## 执行

根据分支类型，读取对应文件并按其流程执行：

| 类型 | 文件 |
|------|------|
| feat | `reference/feat.md` |
| fix | `reference/fix.md` |
| refactor | `reference/refactor.md` |
| test | `reference/test.md` |
| docs | `reference/docs.md` |
| chore | `reference/chore.md` |
| style | `reference/style.md` |
| perf | `reference/perf.md` |
| build | `reference/build.md` |
| ci | `reference/ci.md` |

## 收尾规则

**必须运行 `/task`（业务逻辑类）：** `feat` / `fix` / `refactor` / `test`

**可选运行 `/task`（其他类型）：** `docs` / `chore` / `style` / `perf` / `build` / `ci`

PLAN.md 写完后询问用户：

```
是否需要生成 TASK.md？

  y — 运行 /task 生成任务清单（改动较多时推荐）
  n — 直接运行 /execute（改动简单时可跳过）
```

**通用：** 写入 PLAN.md 后提示使用 `/commit` 提交，完整链路：`/plan` → `(/task)` → `/execute` → `/commit` → `/merge-to-main`
