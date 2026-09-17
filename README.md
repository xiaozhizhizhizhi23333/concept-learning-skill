# concept-learning-skill

一个关于「学习」的个人仓库：既包含**概念学习资料生成 Skill**（《统计与数据分析》课程作业），也包含我自己的**编程学习记录**。

> 作者：王涵莹（西北民族大学 广告学专业）

仓库主体是一个**可复用的项目级 Skill**，以及由该 Skill 生成、并经过人工核查的三份概念学习资料。在此基础上，我把自己零基础学编程的计划、环境配置和练习记录也放了进来（`programming/`），让学习过程本身也变成一份可回看的作品。

---

## 一、仓库里有什么

```
concept-learning-skill/
├── .workbuddy/
│   └── skills/
│       └── concept-learning-generator/   # 项目级 Skill
│           └── SKILL.md
├── learning-materials/                   # 概念学习资料（由 Skill 生成 + 人工核查）
│   ├── agent.html                        # 概念一：Agent（智能体）
│   ├── llm-context.html                  # 概念二：大模型的上下文
│   ├── skill.html                        # 概念三：Skill（技能）
│   └── concept-relationship.md           # 三者关系说明（含 Mermaid 图）
├── programming/                          # 编程学习板块
│   ├── README.md                         # 板块说明
│   ├── learning-plan.html                # 14 周 Python 学习计划表（可打卡）
│   ├── environment-setup.md              # 本地环境搭建记录（含踩坑与解决方式）
│   ├── notebooks/
│   │   ├── 环境测试.ipynb                 # 环境自检（版本/三件套/数据分析/图表/镜像源）
│   │   └── 第1周练习.ipynb                # 第 1 周练习（print/变量/input/BMI/if）
│   └── .vscode/
│       └── settings.json                 # VS Code 配置
├── README.md
└── .gitignore
```

> 说明：仓库主体（Skill + 三份概念学习资料 + 关系说明）是课程作业要求的完整内容；`programming/` 是我在作业之外自己延伸的学习记录，与作业评分内容相互独立、互不影响。

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

## 五、编程学习板块（`programming/`）

除了上面的课程作业内容，我还把这个仓库当作自己的**编程学习记录本**。

我在 2026 年 9 月定下了「Python → 数据分析与可视化」的学习路线，并把计划表、环境配置和每周练习都放进来了：

| 内容 | 文件 | 说明 |
| --- | --- | --- |
| 学习计划表 | `programming/learning-plan.html` | 14 周安排，浏览器打开可勾选打卡 |
| 环境搭建记录 | `programming/environment-setup.md` | Python 3.12 + pip 国内源 + VS Code + Jupyter 的完整配置与验证方式，含踩坑记录 |
| 环境自检 | `programming/notebooks/环境测试.ipynb` | 5 个测试块：版本、数据分析三件套、真实数据分析、图表、镜像源确认 |
| 第 1 周练习 | `programming/notebooks/第1周练习.ipynb` | print / 变量 / input / BMI 计算器 / if 判断，含分步提示与参考答案 |

选这条路的原因：它和《统计与数据分析》课程是同一套技能，作业可以互相复用；广告与营销岗位现在最需要「会看数据、能做图表」的人；而且 Python 也是后续接触 AI 应用的同一门语言。

板块详细说明见 [`programming/README.md`](./programming/README.md)。

---

## 六、我使用 AI 后做了哪些人工核查与修改

按照作业要求，AI 生成的内容必须经本人阅读、理解并核查。本仓库中我做了以下人工工作：

1. **核查资料来源**：逐一确认文中所引用的链接真实存在（Anthropic《Building Effective Agents》、ReAct 论文、OpenAI Tokenizer、《Lost in the Middle》论文、Anthropic Agent Skills 文档、Agent Skills 开放标准等），没有伪造来源。
2. **重写个人解释**：三份资料的"个人解释"栏目均由我用自己的话重述，未整段照搬 AI 或任何原文。
3. **补充与修正**：核实并修正了「工作流 vs 自主 Agent」的区分、「上下文 ≠ 长期记忆」「token ≠ 字数」等易错点，确保概念准确、边界清晰。
4. **统一格式**：将三份资料统一为同一套 HTML 版式与 8 个栏目结构，使风格一致、便于阅读。
5. **关系图设计**：`concept-relationship.md` 中的 Mermaid 图和"一句话关系"为本人梳理后绘制，体现个人理解。
6. **编程板块的实测核查**：`programming/` 里的结论全部是**实际运行验证**过的，不是照搬 AI 说法。例如「系统里只有一个 Python 版本」是查了 PATH 解析结果 + 注册表卸载项 + 常见安装目录三处才确认；「.ipynb 可用」是真的用命令行把 notebook 执行了一遍并检查输出（含图表 PNG 是否生成）；练习本里的参考答案也逐条跑过，包括 BMI 三档取值的边界测试。

---

## 七、版本与安全说明

- 全部内容已通过本地 Git 提交并 push 到 GitHub，仓库保持**公开可访问**。
- **未上传**任何 API Key、密码、Token、个人隐私等敏感信息。
- `.gitignore` 已排除 `.env`、密钥文件、日志、`node_modules`、`__pycache__` 等，以及本地的 `.workbuddy/memory/`（个人工作日志，非作业内容）。

---

## 八、遇到的问题与解决方式（过程记录）

1. **GitHub CLI 安装失败**：通过 winget 安装时因 Windows 符号链接权限报错。解决：从 winget 已下载的安装包中手动解压出 `gh.exe` 使用。
2. **`git push` 无法直连**：本机网络环境下 `github.com` 的 git 通道无法建立连接（CONNECT 隧道返回 502 / 连接超时）。解决：改用 `api.github.com` 的 GitHub REST API（Git Data API）将本地提交历史原样推送到远程仓库，作者、时间戳与本地提交一致。
3. **GitHub 设备授权被拦截**：设备授权接口（github.com/login/device/code）请求被网络重置。解决：改用浏览器创建个人访问令牌（PAT）完成认证，令牌仅用于本次推送、未写入任何仓库文件，使用后已删除/可随时在 GitHub 设置中吊销。
4. **VS Code 扩展市场无法访问 / Python 官网安装包 404 / pip 批量安装被中断**：这三个问题都与搭建编程环境有关，详细的现象、原因与解决办法已记录在 [`programming/environment-setup.md` 第四节](./programming/environment-setup.md)。

---

### 关于概念关系文件名的说明

作业示例目录中写的是 `concept-relationship.html`，但作业正文要求"在 `concept-relationship.md` 中说明"。由于 Mermaid 图在 Markdown 中可被 GitHub 原生渲染，且正文明确指定了 `.md`，本仓库采用 `concept-relationship.md`。
