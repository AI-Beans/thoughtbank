# ThoughtBank 📚

> 把知识编译成持续存在的中间层，而不是每次提问时临时检索。
> Compile knowledge into a persistent middle layer — don't rediscover it on every query.

**ThoughtBank** — 基于 [Karpathy LLM Wiki](https://gist.github.com/karpathy/442a6bf555914893e9891c11519de94f) 理念的 AI 驱动个人知识库。把知识编译成持续存在的中间层，让 LLM 代替你完成整理、关联、复盘的工作。知识复利，每一次问答都在为未来积累。

> ThoughtBank is an AI-powered personal knowledge base built on Karpathy's LLM Wiki concept. Instead of rediscovering knowledge on every query, it compiles insights into a persistent middle layer that grows over time. LLM handles all the bookkeeping — structuring, cross-referencing, and maintenance — while you focus on what matters: asking the right questions. Knowledge compounds. Every answer you save today becomes context for tomorrow.

---

## 核心区别 | Core Difference

| 传统知识库 | ThoughtBank |
|---|---|
| 提问 → 检索 → 回答 | 提问 → **编译** → **复用** |
| 每次重新发现知识 | 知识持续积累 |
| 答案随聊天消失 | 有价值的答案回写到 wiki |

---

## 工作流 | Workflow

```
                           ┌─────────────────────┐
                           │  多种来源输入 RAW     │
                           │  (手动/浏览器/导入)   │
                           └──────────┬──────────┘
                                      ▼
┌──────────────────────────────────────────────────────────────┐
│  RAW ──► INGEST ──► WIKI ──► QUERY ──► FILE BACK ──► LINT │
└──────────────────────────────────────────────────────────────┘
                                      │                │
                                      └────◀──────────┘
                                        (循环)
```

- **RAW** — 源素材（永不可变），来源：手动放入、agent-browser、复制粘贴、书签导入…
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

## OpenCode 使用指南 | OpenCode Usage

ThoughtBank 可以在 OpenCode 中开箱即用，AGENTS.md 会被自动读取。

### 启动新会话

```
cd your-thoughtbank
opencode
# AI 自动读取 AGENTS.md，所有操作遵循规范
```

### 核心操作指令

| 操作 | 指令示例 |
|---|---|
| **Ingest** | "处理 raw/ 中的内容" / "分析这个项目的源码" |
| **Query** | "关于 [主题] 的情况？" / "总结我最近的进展" |
| **File Back** | "把这个分析保存到 outputs/" |
| **Lint** | "检查知识库的完整性" / "健康检查" |

### 调用 LLM Wiki Skill

如果已安装 `/llm-wiki` skill，可以直接使用：

```
/llm-wiki
```

会返回 skill 指引，帮助你执行 ingest/query/lint 操作。

> **提示**：如果 `/llm-wiki` 不可用，AGENTS.md 已经包含完整的工作流程规范，AI 仍会遵循。

### 工作模式

```
你: "处理 raw/ 里的内容"
AI:  ✓ 读取 AGENTS.md 了解规范
     ✓ 分析 raw/ 中的文件
     ✓ 创建/更新 wiki/ 页面
     ✓ 更新 wiki/index.md
     ✓ 追加到 wiki/log.md
     ✓ 返回处理摘要

你: "关于 [项目X] 的进度？"
AI:  ✓ 读取 wiki/index.md 定位相关页面
     ✓ 综合 wiki/ 中的信息回答
     ✓ 有价值的内容自动存到 outputs/
```

### 自动抓取网页 | Automated Web Collection

**agent-browser** — Vercel Labs 发布的 AI 浏览器操控工具，让 AI 直接抓取任意网页。

```bash
# 安装（两条命令）
npm install -g agent-browser
npx agent-browser install

# AI 抓取网页示例
你: "把这个 URL 抓下来存到 raw/：https://example.com/article"
AI:  agent-browser open https://example.com/article
     agent-browser get text "article"
     # AI 打开页面，抓取文本，保存到 raw/
```

**优势**：
- 告别手动复制粘贴
- 处理 JS 动态加载、需登录、交互式图表的页面
- 比 Playwright MCP 省 **82% token**，同样对话可抓 5-6 倍页面

**适用场景**：竞品文章、热门话题、研究文档、社交媒体讨论、任何 AI 需要但你懒得手动保存的内容。

---

## 快速开始 | Quick Start

```bash
# 1. Clone
git clone https://github.com/AI-Beans/thoughtbank.git
cd thoughtbank

# 2. Configure
# 编辑 AGENTS.md，填入你的主题和兴趣点

# 3. (可选) 安装 agent-browser
npm install -g agent-browser
npx agent-browser install

# 4. Start
# 告诉 AI："处理 raw/ 中的内容" 或 "把这个 URL 抓下来存到 raw/"
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

1. **知识复利** — 传统 RAG 每次重新发现，ThoughtBank 让知识持续积累，每次回答都为未来复利
2. **LLM 维护** — 不需要人工整理，LLM 负责所有 bookkeeping
3. **默会知识外化** — Polanyi 说"我们知道的多于能表达的"，那些无法被规则捕获的判断瞬间，记录下来成为可传承的知识
4. **可追溯** — 每个声明注明来源，矛盾可自查

---

## 参考资料 | References

- [Karpathy LLM Wiki](https://gist.github.com/karpathy/442a6bf555914893e9891c11519de94f)
- [agent-browser by Vercel Labs](https://github.com/vercel/agent-browser)
- [Nick Spisak - LLM Wiki Workflow](https://x.com/NickSpisak_/status/2040448463540830705)
- [Polanyi Tacit Knowledge](https://en.wikipedia.org/wiki/Tacit_knowledge)
- [Vanevar Bush - As We May Think (1945)](https://www.theatlantic.com/magazine/archive/1945/07/as-we-may-think/303881/)

---

**MIT License** — 可以自由使用、修改、分享。
