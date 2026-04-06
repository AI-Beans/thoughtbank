# ThoughtBank 📚

> 把知识编译成持续存在的中间层，而不是每次提问时临时检索。
> Compile knowledge into a persistent middle layer — don't rediscover it on every query.

**ThoughtBank** — 基于 [Karpathy LLM Wiki](https://gist.github.com/karpathy/442a6bf555914893e9891c11519de94f) 理念的 AI 驱动个人知识库。把知识编译成持续存在的中间层，让 LLM 代替你完成整理、关联、复盘的工作。知识不复利，每一次问答都在为未来积累。

> ThoughtBank is an AI-powered personal knowledge base built on Karpathy's LLM Wiki concept. Instead of rediscovering knowledge on every query, it compiles insights into a persistent middle layer that grows over time. LLM handles all the bookkeeping — structuring, cross-referencing, and maintenance — while you focus on what matters: asking the right questions. Knowledge compounds. Every answer you save today becomes context for tomorrow.

---

## 核心区别 | Core Difference

## 核心区别 | Core Difference

| 传统知识库 | ThoughtBank |
|---|---|
| 提问 → 检索 → 回答 | 提问 → **编译** → **复用** |
| 每次重新发现知识 | 知识持续积累 |
| 答案随聊天消失 | 有价值的答案回写到 wiki |

---

## 工作流 | Workflow

```
RAW ──► INGEST ──► WIKI ──► QUERY ──► FILE BACK ──► LINT
              │                           │
              └── 分析 ──► 整理 ──► 记录 ─────┘
```

- **RAW** — 源素材放入（永不可变）
- **INGEST** — 分析内容 → 创建/更新 wiki 页面 → 记录 log
- **WIKI** — LLM 维护的结构化知识层
- **QUERY** — 读 wiki → 综合回答
- **FILE BACK** — 有价值的回答存到 outputs
- **LINT** — 健康检查 → 修正矛盾和孤立页面

---

## 目录结构 | Structure

```
.
├── AGENTS.md      # Schema 规范（OpenCode 自动读取）
├── index.html     # 知识图谱可视化（浏览器打开）
├── raw/           # 原始材料（不可变）
├── wiki/          # AI 整理的知识层
│   ├── index.md  # 内容目录
│   └── log.md    # 时间线日志
└── outputs/       # AI 产出物（报告、分析、简报）
```

---

## 快速开始 | Quick Start

```bash
# 1. Clone
git clone https://github.com/AI-Beans/thoughtbank.git
cd thoughtbank

# 2. Configure
# 编辑 AGENTS.md，填入你的主题和兴趣点

# 3. Start
# 将素材放入 raw/，告诉 AI："处理 raw/ 中的内容"
# AI 自动完成 ingest → wiki → index → log 全流程
```

---

## 图谱可视化 | Graph Visualization

用浏览器打开 `index.html`，查看知识图谱：

- 点击节点 → 查看详情
- 双击节点 → 打开 wiki 页面
- 拖拽节点 → 调整布局

---

## 为什么需要 ThoughtBank？| Why ThoughtBank?

1. **知识不复利** — 传统 RAG 每次重新发现，ThoughtBank 让知识持续积累
2. **LLM 维护** — 不需要人工整理，LLM 负责所有 bookkeeping
3. **默会知识外化** — 那些无法被规则捕获的判断瞬间，记录下来
4. **可追溯** — 每个声明注明来源，矛盾可自查

---

## 参考资料 | References

- [Karpathy LLM Wiki](https://gist.github.com/karpathy/442a6bf555914893e9891c11519de94f)
- [Polanyi Tacit Knowledge](https://en.wikipedia.org/wiki/Tacit_knowledge)
- [Vanevar Bush - As We May Think (1945)](https://www.theatlantic.com/magazine/archive/1945/07/as-we-may-think/303881/)

---

**MIT License** — 可以自由使用、修改、分享。
