# gstack

> "我觉得我大概从十二月起就没怎么手动敲过代码了，基本上都是用 AI，这变化太大了。" — [Andrej Karpathy](https://fortune.com/2026/03/21/andrej-karpathy-openai-cofounder-ai-agents-coding-state-of-psychosis-openclaw/)，No Priors 播客，2026年3月

听到 Karpathy 这么说，我特别想知道他是怎么做到的。一个人怎么可能以一当二十？Peter Steinberger 构建了 [OpenClaw](https://github.com/openclaw/openclaw) — 24.7万 GitHub stars — 基本上是独自用 AI 代理完成的。革命已经到来。一个配备合适工具的独立 builder，比传统团队走得更快。

我是 [Garry Tan](https://x.com/garrytan)，[Y Combinator](https://www.ycombinator.com/) 的总裁兼 CEO。我跟数千家初创公司合作过 — Coinbase、Instacart、Rippling — 他们在车库里还只有一两个人的时候。在加入 YC 之前，我是 Palantir 最早的工程师/产品/设计师之一，联合创立了 Posterous（被 Twitter 收购），还构建了 YC 内部的社交网络 Bookface。

**gstack 就是我的答案。** 我做产品二十年了，现在我写的代码比以往任何时候都多。过去 60 天：**60万+ 行生产代码**（35% 是测试），**每天 1-2 万行**，兼职完成，同时还在全职运营 YC。以下是我最近 `/retro` 跨 3 个项目的统计：**一周内新增 140,751 行，362 次提交，约 11.5万净 LOC**。

**2026 — 1,237 次贡献且持续增长：**

![GitHub 2026 年贡献 — 1,237 次贡献，1-3 月大幅加速](docs/images/github-2026.png)

**2013 — 我在 YC 构建 Bookface 时（772 次贡献）：**

![GitHub 2013 年贡献 — 772 次贡献构建 Bookface](docs/images/github-2013.png)

同一个人。不同的时代。差异在于工具。

**gstack 就是我的方法。** 它把 Claude Code 变成了一支虚拟工程团队 — 一个重新思考产品的 CEO，一个锁定架构的工程经理，一个发现 AI 敷衍内容的设计师，一个找出生产环境 Bug 的评审员，一个打开真实浏览器的 QA 负责人，一个运行 OWASP + STRIDE 审计的安全官，以及一个发布 PR 的发布工程师。二十个专家和八个强力工具，全是斜杠命令，全是 Markdown，全免费，MIT 许可证。

这是我的开源软件工厂。我每天都在用。分享出来是因为这些工具应该每个人都能用。

去 fork，去改进，让它成为你的。如果你非要说免费开源软件的坏话 — 随你便，但我更希望你先试试。

**谁适合用：**
- **创始人和 CEO** — 特别是那些仍想自己动手开发的技术型创始人
- **初次使用 Claude Code 的用户** — 结构化的角色分工，而非空白提示词
- **技术 leader 和资深工程师** — 每次 PR 都有的严格评审、QA 和发布自动化

## 快速上手

1. 安装 gstack（30 秒 — 见下文）
2. 运行 `/office-hours` — 描述你在做什么
3. 对任何功能想法运行 `/plan-ceo-review`
4. 对任何有变更的分支运行 `/review`
5. 对你的 staging URL 运行 `/qa`
6. 到此为止。你自然会知道这适不适合你。

## 安装 — 30 秒

**要求：** [Claude Code](https://docs.anthropic.com/en/docs/claude-code)、[Git](https://git-scm.com/)、[Bun](https://bun.sh/) v1.0+、[Node.js](https://nodejs.org/)（仅 Windows）

### 第一步：安装到你的机器

打开 Claude Code 并粘贴这个。Claude 会完成剩下的工作。

> 安装 gstack：运行 **`git clone https://github.com/garrytan/gstack.git ~/.claude/skills/gstack && cd ~/.claude/skills/gstack && ./setup`** 然后在 CLAUDE.md 中添加一个 "gstack" 部分，说明使用 gstack 的 /browse skill 进行所有网页浏览，永不使用 mcp\_\_claude-in-chrome\_\_\* 工具，并列出可用的 skills：/office-hours, /plan-ceo-review, /plan-eng-review, /plan-design-review, /design-consultation, /review, /ship, /land-and-deploy, /canary, /benchmark, /browse, /qa, /qa-only, /design-review, /setup-browser-cookies, /setup-deploy, /retro, /investigate, /document-release, /codex, /cso, /autoplan, /careful, /freeze, /guard, /unfreeze, /gstack-upgrade。然后问用户是否也想把 gstack 添加到当前项目，这样队友也能用到。

### 第二步：添加到你的仓库，让队友也能用（可选）

> 添加 gstack 到这个项目：运行 **`cp -Rf ~/.claude/skills/gstack .claude/skills/gstack && rm -rf .claude/skills/gstack/.git && cd .claude/skills/gstack && ./setup`** 然后在这个项目的 CLAUDE.md 中添加一个 "gstack" 部分，说明使用 gstack 的 /browse skill 进行所有网页浏览，永不使用 mcp\_\_claude-in-chrome\_\_\* 工具，列出可用的 skills：/office-hours, /plan-ceo-review, /plan-eng-review, /plan-design-review, /design-consultation, /review, /ship, /land-and-deploy, /canary, /benchmark, /browse, /qa, /qa-only, /design-review, /setup-browser-cookies, /setup-deploy, /retro, /investigate, /document-release, /codex, /cso, /careful, /freeze, /guard, /unfreeze, /gstack-upgrade，并告诉 Claude 如果 gstack skills 不能工作，运行 `cd .claude/skills/gstack && ./setup` 来构建二进制文件和注册 skills。

真实文件会提交到你的仓库（不是子模块），所以 `git clone` 直接能用。一切都在 `.claude/` 里面。不碰你的 PATH，不在后台运行。

### Codex、Gemini CLI 或 Cursor

gstack 可以在任何支持 [SKILL.md 标准](https://github.com/anthropics/claude-code) 的代理上工作。Skills 放在 `.agents/skills/` 中，会自动被发现。

安装到一个仓库：

```bash
git clone https://github.com/garrytan/gstack.git .agents/skills/gstack
cd .agents/skills/gstack && ./setup --host codex
```

从 `.agents/skills/gstack` 运行 setup 时，它会把生成的 Codex skills 安装到同一仓库的旁边，不会写入 `~/.codex/skills`。

为你的用户账户安装一次：

```bash
git clone https://github.com/garrytan/gstack.git ~/gstack
cd ~/gstack && ./setup --host codex
```

`setup --host codex` 在 `~/.codex/skills/gstack` 创建运行时根目录，并把生成的 Codex skills 链接到顶层。这样可以避免从源仓库 checkout 重复发现 skills。

或者让 setup 自动检测你安装了哪些代理：

```bash
git clone https://github.com/garrytan/gstack.git ~/gstack
cd ~/gstack && ./setup --host auto
```

对于 Codex 兼容的主机，setup 现在支持从 `.agents/skills/gstack` 的仓库本地安装，以及从 `~/.codex/skills/gstack` 的用户全局安装。所有 28 个 skills 都能在所有支持的代理上工作。基于钩子的安全 skills（careful、freeze、guard）在非 Claude 主机上使用内联安全建议文本。

## 看它如何工作

```
你：    我想做一个日历的每日简报应用。
你：    /office-hours
Claude：[询问痛点 — 具体例子，不是假设]

你：    多个 Google 日历，活动信息过期，地点错误。
        准备时间太长，结果还不够好……

Claude：我来挑战一下你的框架。你说"每日简报应用"。
        但你实际描述的是一个个人首席助理 AI。
        [提取了 5 个你自己都没意识到的能力]
        [挑战了 4 个前提 — 你认同、不认同或调整]
        [生成了 3 种实施方案并估计工作量]
        建议：明天发布最窄的切入点，从真实使用中学习。
        完整愿景是 3 个月的项目 — 从一个真正能用的每日简报开始。
        [写了设计文档 → 自动流入下游 skills]

你：    /plan-ceo-review
        [阅读设计文档，挑战范围，运行 10 节评审]

你：    /plan-eng-review
        [ASCII 数据流图、状态机、错误路径图]
        [测试矩阵、故障模式、安全问题]

你：    计划通过。退出计划模式。
        [写了 11 个文件共 2,400 行。大约 8 分钟。]

你：    /review
        [自动修复] 2 个问题。[询问] 竞态条件 → 你批准修复。

你：    /qa https://staging.myapp.com
        [打开真实浏览器，点击流程，发现并修复了一个 bug]

你：    /ship
        测试：42 → 51（+9 个新的）。PR：github.com/you/app/pull/42
```

你说的是"每日简报应用"。代理说"你在做一个首席助理 AI" — 因为它倾听了你的痛点，而不是你的功能请求。八个命令，端到端。这不是副驾驶。这是一支团队。

## 冲刺流程

gstack 是一个流程，不是一堆工具。skills 按冲刺的顺序运行：

**思考 → 计划 → 构建 → 评审 → 测试 → 发布 → 反思**

每个 skill 衔接到下一个。`/office-hours` 写的设计文档被 `/plan-ceo-review` 读取。`/plan-eng-review` 写的测试计划被 `/qa` 接手。`/review` 发现的 bug 被 `/ship` 验证已修复。没有什么会漏掉，因为每一步都知道前面发生了什么。

| Skill | 你的专家 | 职责 |
|-------|---------|------|
| `/office-hours` | **YC Office Hours** | 从这里开始。六个强制问题，在你写代码之前重新审视产品。挑战你的框架，质疑前提，产生替代方案。设计文档流入每个下游 skill。 |
| `/plan-ceo-review` | **CEO / 创始人** | 重新思考问题。找出请求中隐藏的 10 星产品。四种模式：扩张、选择性扩张、保持范围、收缩。 |
| `/plan-eng-review` | **工程经理** | 锁定架构、数据流、图表、边缘情况和测试。把隐藏的假设暴露出来。 |
| `/plan-design-review` | **资深设计师** | 对每个设计维度打分 0-10，解释 10 分是什么样的，然后修改计划达到那个分数。AI 敷衍内容检测。交互式 — 每个设计选择一次提问。 |
| `/design-consultation` | **设计搭档** | 从头构建完整的设计系统。研究领域现状，提出创意风险，生成逼真的产品模型。 |
| `/review` | **资深工程师** | 找出那些 CI 通过但生产环境爆炸的 bug。自动修复明显的。标记完整性缺口。 |
| `/investigate` | **调试专家** | 系统性根因调试。铁律：没有调查就没有修复。追踪数据流，测试假设，三次失败修复后停止。 |
| `/design-review` | **会编码的设计师** | 与 /plan-design-review 相同的审计，然后修复发现的问题。原子提交，前后截图。 |
| `/qa` | **QA 负责人** | 测试你的应用，找 bug，用原子提交修复，重新验证。每个修复自动生成回归测试。 |
| `/qa-only` | **QA 报告员** | 与 /qa 方法论相同，但只报告不修复。纯 bug 报告，不改代码。 |
| `/cso` | **首席安全官** | OWASP Top 10 + STRIDE 威胁模型。零噪音：17 个误报排除，8/10+ 置信度门槛，独立的发现验证。每个发现都包含具体的漏洞利用场景。 |
| `/ship` | **发布工程师** | 同步 main，运行测试，审计覆盖率，推送，打开 PR。如果你没有测试框架，它会引导你搭建。 |
| `/land-and-deploy` | **发布工程师** | 合并 PR，等待 CI 和部署，验证生产环境健康。一条命令从"已批准"到"生产环境验证通过"。 |
| `/canary` | **SRE** | 发布后监控循环。监控控制台错误、性能回归和页面失败。 |
| `/benchmark` | **性能工程师** | 基准页面加载时间、Core Web Vitals 和资源大小。每次 PR 前后对比。 |
| `/document-release` | **技术写作** | 更新所有项目文档以匹配你刚发布的内容。自动捕获过时的 README。 |
| `/retro` | **工程经理** | 团队感知的周回顾。每人统计、发布连续性、测试健康趋势、成长机会。`/retro global` 跨所有项目和 AI 工具运行（Claude Code、Codex、Gemini）。 |
| `/browse` | **QA 工程师** | 真实 Chromium 浏览器，真实点击，真实截图。每条命令约 100ms。 |
| `/setup-browser-cookies` | **会话管理器** | 从你的真实浏览器（Chrome、Arc、Brave、Edge）导入 cookies 到无头会话。测试需要认证的页面。 |
| `/autoplan` | **评审管道** | 一条命令，完全评审的计划。自动运行 CEO → 设计 → 工程评审，编码决策原则。只把品味决策浮出水面等你批准。 |

### 强力工具

| Skill | 功能 |
|-------|------|
| `/codex` | **第二意见** — 来自 OpenAI Codex CLI 的独立代码评审。三种模式：评审（通过/失败门控）、对抗性挑战、开放咨询。当 `/review` 和 `/codex` 都运行过时，进行跨模型分析。 |
| `/careful` | **安全护栏** — 在破坏性命令前警告（rm -rf、DROP TABLE、force-push）。说"be careful"激活。可以覆盖任何警告。 |
| `/freeze` | **编辑锁** — 限制文件编辑到单个目录。防止调试时意外修改范围外的内容。 |
| `/guard` | **全面安全** — `/careful` + `/freeze` 合二为一。做生产环境工作时的最高安全等级。 |
| `/unfreeze` | **解锁** — 移除 `/freeze` 边界。 |
| `/setup-deploy` | **部署配置器** — `/land-and-deploy` 的一次性设置。检测你的平台、生产 URL 和部署命令。 |
| `/gstack-upgrade` | **自动更新** — 升级 gstack 到最新版本。检测全局安装 vs Vendored 安装，同步两者，显示变更内容。 |

**[每个 skill 的深度解析，包含示例和理念 →](docs/skills.md)**

## 并行冲刺

gstack 在一个冲刺中表现出色。在十个同时运行时变得有趣。

[Conductor](https://conductor.build) 并行运行多个 Claude Code 会话 — 每个都在自己隔离的工作空间中。一个会话在 `/office-hours`，另一个在 `/review`，第三个在实现功能，第四个在运行 `/qa`。全部同时进行。冲刺结构是并行工作得以实现的原因 — 没有流程，十个代理就是十个混乱源头。有流程的话，每个代理确切知道要做什么以及何时停止。

---

免费，MIT 许可证，开源。没有高级版，没有等待列表。

我开源了我构建软件的方式。你可以 fork 它，让它成为你的。

> **我们正在招聘。** 想每天发布 1 万+ LOC 并帮助强化 gstack？
> 来 YC 工作 — [ycombinator.com/software](https://ycombinator.com/software)
> 极具竞争力的薪资和股权。旧金山，Dogpatch 区。

## 文档

| 文档 | 内容 |
|-----|------|
| [Skill 深度解析](docs/skills.md) | 每个 skill 的理念、示例和工作流（包括 Greptile 集成） |
| [Builder 理念](ETHOS.md) | Builder 哲学：Boil the Lake、Search Before Building、三层知识 |
| [架构](ARCHITECTURE.md) | 设计决策和系统内部原理 |
| [浏览器参考](BROWSER.md) | `/browse` 的完整命令参考 |
| [贡献指南](CONTRIBUTING.md) | 开发设置、测试、贡献者模式和开发模式 |
| [更新日志](CHANGELOG.md) | 每个版本的新内容 |

## 隐私与遥测

gstack 包含**可选加入**的使用遥测来帮助改进项目。以下是具体说明：

- **默认关闭。** 除非你明确同意，否则什么都不发送。
- **首次运行时，** gstack 询问你是否愿意分享匿名使用数据。你可以说否。
- **发送的内容（如果你选择加入）：** skill 名称、时长、成功/失败、gstack 版本、操作系统。就这些。
- **永不发送的内容：** 代码、文件路径、仓库名、分支名、提示词或任何用户生成内容。
- **随时更改：** `gstack-config set telemetry off` 立即关闭一切。

数据存储在 [Supabase](https://supabase.com)（开源的 Firebase 替代品）。schema 在 [`supabase/migrations/001_telemetry.sql`](supabase/migrations/001_telemetry.sql) — 你可以验证收集了什么。仓库中的 Supabase 发布键是公钥（像 Firebase API 密钥）— 行级安全策略限制为仅插入访问。

**本地分析始终可用。** 运行 `gstack-analytics` 查看本地 JSONL 文件的个人使用仪表板 — 不需要远程数据。

## 故障排除

**Skill 没显示出来？** `cd ~/.claude/skills/gstack && ./setup`

**`/browse` 失败？** `cd ~/.claude/skills/gstack && bun install && bun run build`

**安装过时了？** 运行 `/gstack-upgrade` — 或在 `~/.gstack/config.yaml` 中设置 `auto_upgrade: true`

**Windows 用户：** gstack 通过 Git Bash 或 WSL 在 Windows 11 上工作。除了 Bun 还需要 Node.js — Bun 在 Windows 上有一个已知的 Playwright pipe transport bug（[bun#4253](https://github.com/oven-sh/bun/issues/4253)）。浏览服务器自动回退到 Node.js。确保 `bun` 和 `node` 都在你的 PATH 上。

**Claude 说看不到 skills？** 确保你项目的 `CLAUDE.md` 有 gstack 部分。添加这个：

```
## gstack
Use /browse from gstack for all web browsing. Never use mcp__claude-in-chrome__* tools.
Available skills: /office-hours, /plan-ceo-review, /plan-eng-review, /plan-design-review,
/design-consultation, /review, /ship, /land-and-deploy, /canary, /benchmark, /browse,
/qa, /qa-only, /design-review, /setup-browser-cookies, /setup-deploy, /retro,
/investigate, /document-release, /codex, /cso, /autoplan, /careful, /freeze, /guard,
/unfreeze, /gstack-upgrade.
```

## 许可证

MIT。永久免费。去构建点什么吧。
