---
name: task
description: 基于当前分支类型和 PLAN.md，结对生成符合 TDD 结构的任务清单
allowed-tools:
  - Bash
  - Read
  - Write
  - Glob
---

# Task Workshop

## 前置条件

1. 确认 `CLAUDE.md` 和 `.claude/constitution.md` 存在，否则提示用户先运行 `/claude-md`
2. 读取当前分支名，提取类型前缀
3. 查找 `plan/<type>/<branch-name>/PLAN.md`，读取内容
4. 若 PLAN.md 不存在，提示用户先运行 `/plan`

## TDD 铁律

- 每个有业务逻辑的模块，**测试任务排在实现任务之前**
- 测试任务未完成，对应实现任务不允许开始
- 测试名称描述行为（`test_xxx_returns_yyy_when_zzz`），不描述函数名
- 无业务逻辑的模块（常量、配置）注明"无需测试"

## 执行

根据分支类型，读取对应文件并按其格式生成任务清单：

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

TASK.md 文件头格式见 `templates/task_header.md`。

## 收尾

- 全部任务逐一与用户确认后，写入 `plan/<type>/<branch-name>/TASK.md`
- 提示使用 `/commit` 提交
- 提示下一步运行 `/execute` 开始实现
