# Start Branch Workflow

Help the user start a new branch following Git best practices.

## Usage

```
/new-branch <type> <name>
/new-branch feat due-date
/new-branch fix login-crash
/new-branch refactor storage-layer
/new-branch chore update-deps
/new-branch build docker-setup
/new-branch test add-api-tests
/new-branch docs mvp-plan
```

Supported types and their branch prefixes:

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

## Steps

1. **Parse args**: extract `<type>` and `<name>` from the command arguments.
   - If `<type>` is missing or invalid, ask the user to choose from: `feat`, `fix`, `refactor`, `style`, `perf`, `chore`, `build`, `ci`, `test`, `docs`.
   - If `<name>` is missing, ask the user for a short, lowercase, hyphen-separated name (e.g., `due-date`).

2. **Check current git status** — if there are uncommitted changes, warn the user and ask whether to continue anyway.

3. **Create and switch to the branch**:
   ```bash
   git checkout -b <type>/<name>
   ```

4. **Confirm success** and show the user:
   - Current branch name
   - Reminder to make small, atomic commits using `/commit`
   - How to merge back when done:
     ```bash
     git checkout main
     git merge <type>/<name>
     git branch -d <type>/<name>
     ```

5. **提示下一步：** 运行 `/plan` 开始规划，或如果已有 PLAN.md 直接运行 `/task` 生成任务清单。

   完成开发后，根据场景选择收尾方式：

   ```
   /new-branch → /plan → /task → /execute → /commit → /merge-to-main  # 直接合并（个人项目）
   /new-branch → /plan → /task → /execute → /commit → /create-pr       # 开 PR（需要 Review）
   ```
