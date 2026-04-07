# LLM Wiki Template

让 LLM 帮你持续维护的个人知识库。灵感来自 [Andrej Karpathy 的 LLM Wiki 概念](https://gist.github.com/karpathy/442a6bf555914893e9891c11519de94f)。

## 这是什么？

与 RAG（每次查询时从文档重新拼凑答案）不同，LLM Wiki 让 AI **在录入时就把知识编译成结构化的维基页面**，知识持续积累、自动交叉引用、主动检测矛盾。

你负责喂素材和提问，LLM 负责所有的摘要、归档和维护工作。

## 快速开始

### 1. 克隆模板

```bash
git clone https://github.com/stevenzhou2017/llm-wiki-template.git my-wiki
cd my-wiki
```

### 2. 用 Claude Code 打开

```bash
claude
```

`CLAUDE.md` 已经定义好了所有工作流规则，Claude 会自动按照 schema 工作。

### 3. 录入你的第一篇文章

把文章复制到 `raw/` 目录下，然后告诉 Claude：

```
录入 raw/articles/xxx.md
```

Claude 会自动：
- 创建来源摘要页
- 识别并创建实体页和概念页
- 建立 `[[双向链接]]` 交叉引用
- 更新目录索引和操作日志

### 4. 提问

直接问 Claude 关于你知识库中的任何问题，它会查阅 wiki 页面后综合回答。

### 5. 健康检查

```
检查维基健康
```

Claude 会检查矛盾、断链、孤立页面、知识缺口等问题。

## 目录结构

```
raw/                    # 原始来源（只读，LLM 不会修改）
  articles/             # 文章
  assets/               # 图片等附件
wiki/                   # LLM 维护的知识页面
  index.md              # 分类目录
  log.md                # 操作日志
  sources/              # 来源摘要页
  entities/             # 实体页（人物、公司、产品…）
  concepts/             # 概念页（技术、理论、方法…）
CLAUDE.md               # LLM 行为规范（schema）
```

## 推荐搭配

- **[Obsidian](https://obsidian.md/)** — 浏览维基、查看图谱视图、可视化知识网络
- **Obsidian Web Clipper** — 一键剪藏网页到 `raw/`

## 自定义

编辑 `CLAUDE.md` 可以调整：

- 页面分类（增加 `wiki/events/` 等新类别）
- 页面格式（修改 frontmatter 字段）
- 语言偏好
- 工作流规则

## 为什么不用 RAG？

| | RAG | LLM Wiki |
|---|---|---|
| 知识处理 | 查询时检索 | 录入时编译 |
| 积累性 | 无，每次从零开始 | 持续增长 |
| 交叉引用 | 无 | 自动维护 |
| 矛盾检测 | 无 | 主动标记 |

> 人类放弃维基是因为维护成本太高。LLM 不会累，一次能更新十几个页面，维护成本趋近于零。

## License

MIT
