---
title: "LLM Wiki: 用 LLM 构建个人知识库的模式"
created: 2026-04-07
updated: 2026-04-07
tags: [知识管理, LLM, wiki, RAG, Obsidian]
sources: [karpathy-llm-wiki.md]
---

# LLM Wiki: 用 LLM 构建个人知识库的模式

**来源：** [GitHub Gist](https://gist.github.com/karpathy/442a6bf555914893e9891c11519de94f)
**作者：** [[Andrej Karpathy]]
**日期：** 2026-04-02

## 核心思想

与 [[RAG]] 的根本区别：RAG 在每次查询时从原始文档重新拼凑答案，没有知识积累；LLM Wiki 让 LLM **持续构建和维护一个结构化的 Markdown 维基**，知识被编译一次后持续更新，而非每次重新推导。

> The wiki is a persistent, compounding artifact.

## 三层架构

1. **Raw Sources（原始来源）**：不可变的源文档，LLM 只读不写
2. **The Wiki（维基）**：LLM 生成和维护的 Markdown 页面——摘要、实体页、概念页、比较分析
3. **The Schema（模式）**：配置文件（如 CLAUDE.md），定义 LLM 的行为规范和工作流

## 三个核心操作

- **Ingest（录入）**：新来源 → LLM 读取 → 写摘要 → 更新 10-15 个相关页面 → 维护交叉引用
- **Query（查询）**：先读 index.md 找相关页 → 综合回答 → 有价值的答案反写回维基
- **Lint（校验）**：定期健康检查——矛盾、孤立页、缺失引用、知识缺口

## 应用场景

个人成长、学术研究、读书笔记、团队内部知识库、竞品分析、尽职调查等。

## 关键工具

- [[Obsidian]]：浏览和可视化维基（图谱视图）
- Obsidian Web Clipper：网页剪藏到 raw/
- [[qmd]]：本地 Markdown 搜索引擎（BM25 + 向量 + LLM 重排序）
- Marp：Markdown 生成幻灯片
- Dataview：对 frontmatter 做查询

## 为什么有效

人类放弃维基是因为维护成本增长快于价值。LLM 不会厌倦，不会忘记更新交叉引用，一次可以修改 15 个文件。维护成本趋近于零。

## 思想渊源

与 Vannevar Bush 的 [[Memex]]（1945）一脉相承——私人策展的知识库，文档间的关联与文档本身同等重要。Bush 没解决的问题是"谁来维护"，LLM 解决了。

## 与 [[Vibe Coding]] 的关系

同一作者提出的两个概念，代表了 LLM 时代人机协作的两个方向：[[Vibe Coding]] 是"让 LLM 写代码，人只看结果"；LLM Wiki 是"让 LLM 维护知识，人只负责策展和思考"。
