# Claude Plugins

个人 Claude Code 插件配置仓库，包含自定义 Commands、Skills 及全局 Settings。

## 项目结构

| 目录 | 内容 |
|------|------|
| `commands/` | 自定义斜杠命令（commit、new-branch、plan 等） |
| `skills/` | 工作流 Skill（plan、task、execute、explain-explore、explain-write） |
| `settings/` | 全局 Claude Code 设置 |
| `mcp/` | MCP 服务安装说明 |

## 前置要求

- [Claude Code](https://claude.ai/code) 已安装
- `rsync`（macOS 自带）
- `python3`（macOS 自带）

## 一键安装

```bash
./install.sh sync
```

首次安装或后续同步均可使用，幂等执行。

### 可选参数

```bash
./install.sh sync --dry-run              # 预览变更，不实际写入
./install.sh sync --only commands        # 只同步 commands
./install.sh sync --only skills          # 只同步 skills
./install.sh sync --only settings        # 只合并 settings
```

## 跨平台配置同步（实验性）

使用 `sync.sh` 可以在不同 AI 工具之间同步配置（如从 Kimi 同步到 Claude）：

```bash
./sync.sh
```

### 功能特性

- 支持 kimi / codex / claude 三种工具配置同步
- 自动检测默认路径（`~/.kimi`、`~/.codex`、`~/.claude`）
- 路径不存在时提示输入自定义路径
- 交互式选择要同步的目录
- 智能排除选择：
  - 内容 ≤5 项：交互式选择排除
  - 内容 >5 项：提示使用 `.syncignore`
- 支持 `.syncignore` 过滤（类似 `.gitignore` 语法）

### 使用示例

```bash
./sync.sh --list                    # 列出支持的 AI 工具
./sync.sh --dry-run                 # 预览同步（不实际执行）
./sync.sh kimi                      # 直接指定工具
./sync.sh --path ~/.custom/kimi kimi  # 使用自定义路径
```

### 交互式示例

```bash
$ ./sync.sh

Claude Plugins 跨平台同步工具
===========================

请选择要同步的 AI 工具（输入数字，多个用空格分隔）：
  1) kimi   - Kimi CLI 配置 (~/.kimi)
  2) codex  - Codex CLI 配置 (~/.codex)
  3) claude - Claude Code 配置 (~/.claude)
  4) 全部

你的选择: 1
已选择: kimi

[kimi]
检查默认路径 /Users/xxx/.kimi ... ✓ 存在
路径: /Users/xxx/.kimi

~/.kimi 目录内容：
  1) skills/   - 11 个项目
  2) 全部

请选择要同步的目录（输入数字）: 1
已选择目录: skills

~/.kimi/skills 目录下发现以下内容（共 11 项）：
  analyze-bug commit execute explain ...

内容较多，如需排除特定内容，请在仓库创建 .syncignore 文件：
  echo "draft/" >> skills/.syncignore
  echo "test-*.md" >> skills/.syncignore

按回车继续...

发现 .syncignore，以下内容将被排除:
  ✗ draft/

同步: kimi/skills
来源: /Users/xxx/.kimi/skills
目标: ~/.claude/skills/
排除: draft/
```

### 过滤配置

在源目录创建 `.syncignore` 文件（类似 `.gitignore` 语法）：

```bash
# 排除整个目录
draft/

# 排除特定文件
explain/TASK.md

# 排除模式
*.tmp
```

**注意**: `.syncignore` 文件仅在仓库内生效，不会同步到目标目录。

### 同步策略

| 资产 | 策略 |
|------|------|
| `commands/` | 覆盖已有同名文件，保留用户自有文件，不删除 |
| `skills/` | 覆盖已有同名文件，保留用户自有文件，不删除 |
| `settings/settings.json` | 深度合并，仓库 key 写入本地，本地独有 key 保留 |

### 示例输出

```
==> Summary
    commands: 7 file(s) → ~/.claude/commands/
        - commit.md
        - new-branch.md
        - ...
    skills  : 41 file(s) → ~/.claude/skills/
        - plan/SKILL.md
        - task/SKILL.md
        - ...
    settings: merged → ~/.claude/settings.json

Done. Target: /Users/yourname/.claude
```

## 配置 MCP 服务

MCP 服务需手动配置，详见 `mcp/INSTALL.md`。

## 验证安装

重启 Claude Code 后，在任意项目中输入 `/commit` 或 `/new-branch`，若命令补全出现则安装成功。
