---
title: RAG (检索增强生成)
created: 2026-04-07
updated: 2026-04-07
tags: [AI, 知识管理, 检索, LLM]
sources: [karpathy-llm-wiki.md]
---

# RAG (Retrieval-Augmented Generation)

检索增强生成，当前主流的 LLM + 文档方案。

## 工作方式

上传文档集合 → 查询时检索相关片段 → LLM 基于片段生成回答。

代表产品：NotebookLM、ChatGPT 文件上传、各类企业 RAG 系统。

## 局限性（[[Andrej Karpathy]] 的批评）

- **无积累**：每次查询都从头拼凑，不建立持久知识结构
- **重复劳动**：需要综合 5 篇文档的问题，每次都要重新发现和拼接
- **无矛盾检测**：不会主动发现文档间的冲突

## 对比：[[LLM Wiki]]

| | RAG | LLM Wiki |
|---|---|---|
| 知识处理 | 查询时检索 | 录入时编译 |
| 积累性 | 无 | 持续增长 |
| 交叉引用 | 无 | 自动维护 |
| 矛盾检测 | 无 | 主动标记 |
| 适用规模 | 任意 | 中小规模更优 |
