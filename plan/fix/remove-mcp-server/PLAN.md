# 修复规划：移除 MCP 配置，添加待安装服务列表

## 1. Bug 描述

仓库中包含 `mcp/mcp-config.template.json` 配置模板，这些属于 Claude 官方内置功能，不应重复存放。作为一键配置工具，应记录**待安装的 MCP 服务列表**，方便在新环境快速配置。

## 2. 复现路径

查看 `mcp/` 目录发现配置文件：
```
mcp/
└── mcp-config.template.json
```

## 3. 根因分析

初始配置时未区分官方配置与自定义配置需求。实际需要的是**待安装服务清单**，而非配置文件本身。

## 4. 修复方案

### 4.1 删除官方配置
- **文件：** `mcp/mcp-config.template.json`
- **原因：** 官方配置可通过 Claude Code 内置功能获取

### 4.2 添加待安装服务记录
- **文件：** `mcp/INSTALL.md`
- **内容：** 列出待安装的 MCP 服务及安装命令
  - `web-search` — 网络搜索
  - `playwright` — 浏览器自动化

## 5. 回归测试

- [ ] 确认 `mcp/mcp-config.template.json` 已删除
- [ ] 确认 `mcp/INSTALL.md` 已创建
- [ ] 确认文档包含正确的安装命令

## 执行确认

是否执行以上修复方案？
- `y` — 执行删除和创建操作
- `n` — 调整方案
