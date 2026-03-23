# Explain

生成项目解释文档，保存到 `explain/` 目录。

## Usage

```
/explain                    探索整个项目，生成架构总览（含功能清单）
/explain feature            显示功能清单，供选择后深入探索
/explain feature upload     深入讲解某个具体功能的实现
/explain changelog          这次改了什么（变更记录）
/explain decision           设计决策与取舍
/explain concept            背后的技术原理
```

## Steps

解析 ARGUMENTS，按以下规则路由：

---

### 无参数

依次调用两个 skill：

1. 调用 `explain-explore` skill，传入：
   ```
   type: architecture
   working_dir: {当前工作目录绝对路径}
   ```
2. 将返回的 findings 传入 `explain-write` skill：
   ```
   type: architecture
   working_dir: {当前工作目录绝对路径}
   findings: {explain-explore 的输出}
   ```

---

### `feature`（无 topic）

读取 `{working_dir}/explain/architecture.md`：

**如果文件存在**：提取 `## 功能清单` 章节内容，直接展示给用户，并提示：
```
以上是当前功能清单。运行 `/explain feature {topic}` 深入了解某个功能。
如需重新生成，运行 `/explain` 更新 architecture.md。
```

**如果文件不存在**：提示用户先运行 `/explain` 生成架构总览，再使用此命令。

---

### `feature {topic}` / `changelog` / `decision` / `concept`

依次调用两个 skill：

1. 调用 `explain-explore` skill，传入：
   ```
   type: {type}
   topic: {topic，如未指定则留空}
   working_dir: {当前工作目录绝对路径}
   ```
2. 将返回的 findings 传入 `explain-write` skill：
   ```
   type: {type}
   topic: {topic，如未指定则留空}
   working_dir: {当前工作目录绝对路径}
   findings: {explain-explore 的输出}
   ```
