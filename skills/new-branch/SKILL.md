---
name: new-branch
description: Help the user create a new Git branch following best practices. Use when the user asks to create a new branch, start a feature branch, or switch to a new branch with a specific type and name.
---

# New Branch Workflow

Help the user start a new Git branch following conventional naming.

## Supported Branch Types

| Type | Prefix | When to use |
|------|--------|-------------|
| `feat` | `feat/` | New feature |
| `fix` | `fix/` | Bug fix |
| `refactor` | `refactor/` | Code refactoring |
| `style` | `style/` | Code style, formatting |
| `perf` | `perf/` | Performance improvements |
| `chore` | `chore/` | Maintenance, dependencies, tooling |
| `build` | `build/` | Build system changes |
| `ci` | `ci/` | CI/CD configuration changes |
| `test` | `test/` | Adding or updating tests |
| `docs` | `docs/` | Planning documents, specs, design docs |

## Workflow

1. **Parse args**: Determine `<type>` and `<name>` from the user's request.
   - If `<type>` is missing or invalid, ask the user to choose from the supported types.
   - If `<name>` is missing, ask for a short, lowercase, hyphen-separated name (e.g., `login-crash`).

2. **Check current git status**. If there are uncommitted changes, warn the user and ask whether to continue anyway.

3. **Create and switch to the branch**:
   ```bash
   git checkout -b <type>/<name>
   ```

4. **Confirm success** and show:
   - The current branch name
   - Reminder to make small, atomic commits using `/commit`
   - How to merge back when done:
     ```bash
     git checkout main
     git merge <type>/<name>
     git branch -d <type>/<name>
     ```

5. **Suggest next steps**（根据分支类型）：

   **feat/refactor/test/docs 等：**
   ```
   /plan → /task → /execute → /commit → /merge-to-main
   ```

   **fix（Bug 修复）：**
   ```
   /analyze-bug → /task → /execute → /commit → /merge-to-main
   ```
   - `fix` 分支**必须先运行 `/analyze-bug`** 进行 Bug 分析和根因定位
   - `/analyze-bug` 会输出 `ANALYSIS.md`，然后 `/task` 基于此生成修复任务
   - 修复必须遵循 TDD：先写复现测试（红）→ 再写修复（绿）→ 回归测试

   **快捷方式：**
   - 如果 `PLAN.md` 或 `ANALYSIS.md` 已存在，可直接运行 `/task` 生成任务
