# concept-learning-skill

一个用于「概念学习资料生成」的个人学习仓库，也是《统计与数据分析》课程作业的项目仓库。

> 作者：王涵莹（西北民族大学 广告学专业）

它包含一个**可复用的项目级 Skill**，以及由该 Skill 生成、并经过人工核查的三份概念学习资料。这个仓库既可以继续迭代复用，也可以作为后续课程项目的个人工具基础与作品集材料。

---

## 一、仓库里有什么

```
concept-learning-skill/
├── .workbuddy/
│   └── skills/
│       └── concept-learning-generator/   # 项目级 Skill
│           └── SKILL.md
├── learning-materials/                   # 学习资料（由 Skill 生成 + 人工核查）
│   ├── agent.html                        # 概念一：Agent（智能体）
│   ├── llm-context.html                  # 概念二：大模型的上下文
│   ├── skill.html                        # 概念三：Skill（技能）
│   └── concept-relationship.md           # 三者关系说明（含 Mermaid 图）
├── README.md
└── .gitignore
```

---

## 二、Skill 的存放路径与说明

- **存放路径：** `.workbuddy/skills/concept-learning-generator/SKILL.md`
- **Skill 名称：** `concept-learning-generator`（概念学习资料生成器）
- **作用：** 接收任意一个（或多个）概念作为学习主题，按固定栏目自动生成结构化的学习资料。
- **它是"项目级 Skill"**：放在本仓库根目录的 `.workbuddy/skills/` 下，随仓库一起版本管理、可被团队/老师查看复用。
- **可复用性**：SKILL.md 顶部包含 YAML 元数据（`name` + `description`），正文写明了适用场景、输入信息、生成步骤、输出结构、资料来源要求和自检要求——它不是为本次三个概念写的一次性提示词，而是能处理"任何新概念"的通用流程。

---

## 三、如何在 WorkBuddy 中调用它

1. 用 WorkBuddy **打开本仓库目录**（项目级 Skill 会在本项目内自动生效）；
2. 用自然语言直接发起学习请求即可，例如：
   - `学习概念：正则化`
   - `帮我学习"注意力机制"，输出 Markdown`
   - `学习概念：过拟合 和 欠拟合，并比较它们的关系`
3. Skill 会按「学习目标 → 核心问题 → 个人解释 → 核心机制 → 应用场景 → 易混淆/边界 → 自测问题 → 可核查来源」的固定栏目生成资料。

> 说明：Skill 的 `description` 里写了触发条件（"学习/理解/搞懂一个概念""做学习笔记/复习提纲"等），因此只要你的请求命中这些意图，WorkBuddy 就会自动加载并使用它。

---

## 四、已生成的学习资料

| 概念 | 文件 | 覆盖内容 |
| --- | --- | --- |
| Agent（智能体） | `learning-materials/agent.html` | 个人解释、核心组成（大脑/工具/记忆/循环/环境）、编程 Agent 场景、易混淆点与边界、自测、来源 |
| 大模型的上下文 | `learning-materials/llm-context.html` | 上下文窗口与 Token、RAG 场景、"迷失在中间"、隐私边界、自测、来源 |
| Skill（技能） | `learning-materials/skill.html` | Skill 与提示词的区别、YAML 元数据、项目级 vs 用户级、自测、来源 |
| 三者关系 | `learning-materials/concept-relationship.md` | 文字 + 对比表 + Mermaid 流程图，说明上下文如何影响 Agent、Skill 如何沉淀知识 |

---

## 五、我使用 AI 后做了哪些人工核查与修改

按照作业要求，AI 生成的内容必须经本人阅读、理解并核查。本仓库中我做了以下人工工作：

1. **核查资料来源**：逐一确认文中所引用的链接真实存在（Anthropic《Building Effective Agents》、ReAct 论文、OpenAI Tokenizer、《Lost in the Middle》论文、Anthropic Agent Skills 文档、Agent Skills 开放标准等），没有伪造来源。
2. **重写个人解释**：三份资料的"个人解释"栏目均由我用自己的话重述，未整段照搬 AI 或任何原文。
3. **补充与修正**：核实并修正了「工作流 vs 自主 Agent」的区分、「上下文 ≠ 长期记忆」「token ≠ 字数」等易错点，确保概念准确、边界清晰。
4. **统一格式**：将三份资料统一为同一套 HTML 版式与 8 个栏目结构，使风格一致、便于阅读。
5. **关系图设计**：`concept-relationship.md` 中的 Mermaid 图和"一句话关系"为本人梳理后绘制，体现个人理解。

---

## 六、版本与安全说明

- 全部内容已通过本地 Git 提交并 push 到 GitHub，仓库保持**公开可访问**。
- **未上传**任何 API Key、密码、Token、个人隐私等敏感信息。
- `.gitignore` 已排除 `.env`、密钥文件、日志、`node_modules`、`__pycache__` 等，以及本地的 `.workbuddy/memory/`（个人工作日志，非作业内容）。

---

### 关于概念关系文件名的说明

作业示例目录中写的是 `concept-relationship.html`，但作业正文要求"在 `concept-relationship.md` 中说明"。由于 Mermaid 图在 Markdown 中可被 GitHub 原生渲染，且正文明确指定了 `.md`，本仓库采用 `concept-relationship.md`。
