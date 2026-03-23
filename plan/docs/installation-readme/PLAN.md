# PLAN: 安装插件的 README.md

## 文档目标

面向想要复用这套 Claude 插件配置的开发者，解决"如何将仓库中的 commands/skills/agents/MCP 配置安装到本地 Claude 环境"的信息缺口。

## 文档结构

1. ✅ **项目简介** — 这个仓库包含什么
2. ✅ **前置要求** — Claude Code 版本、Node.js 等
3. ✅ **安装 Commands** — 复制到 `~/.claude/commands/`
4. ✅ **安装 Skills** — 复制到 `~/.claude/skills/`
5. ✅ **安装 Agents** — 复制到 `~/.claude/agents/`
6. ✅ **配置 MCP 服务** — 编辑 `~/.claude.json`，填入 API Key
7. ✅ **全局 Settings（可选）** — 合并 `settings/settings.json`
8. ✅ **验证安装** — 如何确认插件生效

## 内容来源

- 仓库目录结构（commands/skills/agents/mcp/settings）
- `mcp/mcp-config.template.json` — MCP 配置说明
- `settings/settings.json` — 全局设置说明
- Claude Code 官方文档中关于 commands/skills/agents 的安装路径约定
