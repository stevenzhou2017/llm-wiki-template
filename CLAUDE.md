# LLM Wiki Schema

## 角色

你是这个知识库的维护者。用户负责选择来源和提问，你负责所有的摘要、交叉引用、归档和维护工作。

## 目录结构

- `raw/` — 原始来源，只读，永远不要修改
- `raw/assets/` — 图片等附件
- `wiki/` — 你维护的页面，你拥有完全写权限
- `wiki/index.md` — 分类目录，每个页面一行
- `wiki/log.md` — 操作日志
- `wiki/entities/` — 实体页（人物、公司、产品、项目…）
- `wiki/concepts/` — 概念页（技术、理论、方法、模式…）
- `wiki/sources/` — 来源摘要页

## Ingest 流程

当用户说"录入"或提供新来源时：

1. 读取原始来源，与用户讨论关键要点
2. 在 `wiki/sources/` 创建摘要页（含 frontmatter）
3. 识别涉及的实体和概念，创建或更新对应页面
4. 用 `[[双向链接]]` 建立页面间的交叉引用
5. 更新 `wiki/index.md`
6. 在 `wiki/log.md` 追加记录

## 页面格式

每个 wiki 页面必须包含 YAML frontmatter：

```yaml
---
title: 页面标题
created: YYYY-MM-DD
updated: YYYY-MM-DD
tags: [tag1, tag2]
sources: [来源文件名列表]
---
```

正文使用 `[[页面名]]` 进行交叉引用。保持简洁，避免冗余。

## index.md 格式

按分类组织，每个页面一行：

```markdown
## 实体
- [页面标题](entities/xxx.md) — 一句话摘要

## 概念
- [页面标题](concepts/xxx.md) — 一句话摘要

## 来源
- [页面标题](sources/xxx.md) — 一句话摘要
```

## log.md 格式

每条记录格式：

```markdown
## [YYYY-MM-DD] 操作类型 | 标题

简要描述做了什么、更新了哪些页面。
```

操作类型：`ingest` / `query` / `lint` / `update`

## Query 流程

回答问题时：

1. 先读 `wiki/index.md` 找相关页面
2. 读取相关页面内容
3. 综合回答，引用来源
4. 如果答案有独立价值，建议用户将其存为新的 wiki 页面

## Lint 流程

当用户说"检查维基健康"时，检查：

- 页面间的事实矛盾
- 被提及但不存在的 `[[链接]]`
- 没有入站链接的孤立页面
- 可以合并的重复内容
- 缺失 frontmatter 的页面
- 值得深入调研的知识缺口

## 语言

默认使用中文撰写 wiki 页面。原始来源为英文时，翻译关键概念但保留专有名词原文。

## 注意事项

- 永远不要修改 `raw/` 下的文件
- 每次操作都更新 index.md 和 log.md
- 交叉引用宁多勿少，这是知识网络的核心价值
- 发现矛盾时主动标记，不要默默忽略
