<div align="center">
  <h1>Team AI</h1>
  <p><strong>Git-native tooling for consistent, team-wide GitHub Copilot capabilities.</strong></p>
  <p>
    <a href="#english">English</a> ·
    <a href="#zh-cn">简体中文</a>
  </p>
  <p>
    <a href="https://github.com/teamai-vault/teamai-cli-copilot">teamai CLI</a> ·
    <a href="https://github.com/teamai-vault/teamai-marketplace">Marketplace</a> ·
    <a href="https://teamai-vault.github.io/teamai-cli-copilot/">Docs site</a>
  </p>
</div>

<a id="english"></a>

## English

Team AI is a thin control layer for teams building with GitHub Copilot. A department keeps its shared Plugins, instructions, Skills, business context, and Learnings in one Git Marketplace; the `teamai` CLI converges them onto each engineer's machine and business repositories. It adds no second agent runtime, no custom plugin format, and no IDE-specific layer.

### Start here

| Goal | Repository |
| --- | --- |
| Install the `teamai` CLI: initialize, bind a repository, sync, recall, contribute, diagnose | [teamai-cli-copilot](https://github.com/teamai-vault/teamai-cli-copilot) |
| Start a department Marketplace from the reference template | [teamai-marketplace](https://github.com/teamai-vault/teamai-marketplace) |
| See the architecture, file layout, and command examples at a glance | [Docs site](https://teamai-vault.github.io/teamai-cli-copilot/) |

### How it fits

```text
teamai-marketplace (department-owned, one per department)
  main               plugins/  instructions/  skills/  manifest/projects.yaml  contexts/
  teamai-learnings   learnings/<project|shared>/<uuid>.md
        │ read                                        ▲ learning share / skill contribute
        ▼                                             │ isolated worktree → pull request
teamai CLI ─────────────────────────────────────────────┘
  init · projects set · sync · recall · status · doctor
        │                                   │
        ▼                                   ▼
your machine (~/.copilot)             your business repository
  common + 1 role Plugin enabled        .github/instructions/teamai/<id>/
  instructions/teamai/                  .teamai/context/   (docs, Learnings)
  skills/teamai/, teamai-recall Agent   project Plugin components, when declared
```

Plugins are installed and enabled through native Copilot commands, with a VS Code fallback when the Copilot CLI is absent. Everything else is mirrored into paths Team AI owns, with an ownership record for each write.

### Quick start

Requirements: Node.js 20+, Git, and the GitHub Copilot CLI (VS Code works as a fallback for Plugin convergence).

```bash
git clone https://github.com/teamai-vault/teamai-cli-copilot.git
cd teamai-cli-copilot
npm install && npm run build && npm link

teamai init --marketplace teamai-vault/teamai-marketplace --role api   # once per machine
cd <your-business-repo>
teamai projects set <logical-project-id>                               # once per repository
teamai sync                                                            # whenever the team updates
teamai recall payment retry                                            # search team knowledge locally
```

Use your own department's Marketplace in place of `teamai-vault/teamai-marketplace`. Every write command accepts `--dry-run`.

### What a Marketplace carries

- **Common Plugin**: capabilities shared by every role.
- **Role Plugins**: `api`, `ios`, `aos` (Android), `qa`, `design`. All are installed; only `common` plus the selected role are enabled.
- **Instructions**: department-wide `*.instructions.md`, mirrored to `~/.copilot/instructions/teamai/`.
- **Team Skills**: standalone Skills governed by `skills.yaml`, installed on demand by name or tag.
- **Logical Projects**: business context in `contexts/<id>/`, bound to a repository with `teamai projects set`, optionally with a `kind: project` Plugin as a component source.
- **Learnings**: troubleshooting notes published through pull requests to the `teamai-learnings` branch and searchable with `teamai recall` or the bundled `teamai-recall` Agent.

### Principles

- **Native first**: compose with GitHub Copilot's existing CLI, Marketplace, and Agent Plugin surfaces.
- **Git-native**: shared capabilities and Learnings are versioned and reviewed in Git; project context stays next to the code it serves.
- **Explicit ownership**: automation changes only what it installed or recorded as owned, and refuses occupied paths.
- **Small by default**: prefer a clear boundary over a clever overlay or another runtime.

### Learn and contribute

- [CLI README](https://github.com/teamai-vault/teamai-cli-copilot#readme) · [中文文档](https://github.com/teamai-vault/teamai-cli-copilot/blob/main/README.zh-CN.md) · [Docs site](https://teamai-vault.github.io/teamai-cli-copilot/)
- [Marketplace README](https://github.com/teamai-vault/teamai-marketplace#readme) · [Plugin Guide](https://github.com/teamai-vault/teamai-marketplace/blob/main/docs/PLUGIN-GUIDE.md) · [Contributing](https://github.com/teamai-vault/teamai-marketplace/blob/main/docs/CONTRIBUTING.md)
- For questions or changes, open an issue in the repository closest to the topic and follow its contribution guidance.

<a href="#team-ai">Back to top</a> · <a href="#zh-cn">简体中文</a>

<a id="zh-cn"></a>

## 简体中文

Team AI 是面向团队的 GitHub Copilot 轻量控制层。部门把共享的 Plugin、Instructions、Skill、业务上下文和团队经验（Learnings）放在一个 Git Marketplace 里，`teamai` CLI 负责把它们收敛到每位工程师的机器和业务仓库。它不引入第二套 Agent Runtime、自定义 Plugin 格式或 IDE 专属适配层。

### 从这里开始

| 目标 | 仓库 |
| --- | --- |
| 安装 `teamai` CLI：初始化、绑定仓库、同步、召回、贡献、诊断 | [teamai-cli-copilot](https://github.com/teamai-vault/teamai-cli-copilot) |
| 以参考模板创建部门自己的 Marketplace | [teamai-marketplace](https://github.com/teamai-vault/teamai-marketplace) |
| 一页看懂架构、文件位置和命令示例 | [文档站](https://teamai-vault.github.io/teamai-cli-copilot/) |

### 它们如何协作

```text
teamai-marketplace（部门自有，每个部门一个）
  main               plugins/  instructions/  skills/  manifest/projects.yaml  contexts/
  teamai-learnings   learnings/<project|shared>/<uuid>.md
        │ 读取                                        ▲ learning share / skill contribute
        ▼                                             │ 隔离 worktree → Pull Request
teamai CLI ─────────────────────────────────────────────┘
  init · projects set · sync · recall · status · doctor
        │                                   │
        ▼                                   ▼
你的机器（~/.copilot）                 你的业务仓库
  启用 common + 1 个 role Plugin         .github/instructions/teamai/<id>/
  instructions/teamai/                  .teamai/context/（Docs、Learnings）
  skills/teamai/、teamai-recall Agent   Project Plugin 声明的组件（按需）
```

Plugin 通过 Copilot 原生命令安装和启用，没有 Copilot CLI 时回退到 VS Code。其余内容镜像到 Team AI 自有的路径，每次写入都记录所有权。

### 快速开始

环境要求：Node.js 20+、Git，以及 GitHub Copilot CLI（Plugin 收敛也可回退到 VS Code）。

```bash
git clone https://github.com/teamai-vault/teamai-cli-copilot.git
cd teamai-cli-copilot
npm install && npm run build && npm link

teamai init --marketplace teamai-vault/teamai-marketplace --role api   # 每台机器一次
cd <your-business-repo>
teamai projects set <logical-project-id>                               # 每个仓库一次
teamai sync                                                            # 团队内容更新后
teamai recall 支付 重试                                                 # 本地检索团队知识
```

请把 `teamai-vault/teamai-marketplace` 换成你所在部门的 Marketplace。所有写命令都支持 `--dry-run`。

### Marketplace 里有什么

- **Common Plugin**：所有 Role 共用的能力。
- **Role Plugin**：`api`、`ios`、`aos`（Android）、`qa`、`design`。全部安装，只启用 `common` 和所选 Role。
- **Instructions**：部门级 `*.instructions.md`，镜像到 `~/.copilot/instructions/teamai/`。
- **Team Skills**：由 `skills.yaml` 治理的 standalone Skill，按名字或 Tag 按需安装。
- **Logical Project**：`contexts/<id>/` 中的业务上下文，用 `teamai projects set` 绑定到仓库，可选用 `kind: project` 的 Plugin 作为组件来源。
- **Learnings**：排障与踩坑记录，经 Pull Request 发布到 `teamai-learnings` 分支，可用 `teamai recall` 或内置的 `teamai-recall` Agent 检索。

### 原则

- **优先使用原生能力**：组合 GitHub Copilot 已有的 CLI、Marketplace 和 Agent Plugin。
- **Git-native**：共享能力和 Learnings 在 Git 中版本化并经过评审；项目上下文跟随它服务的代码。
- **边界明确**：自动化只修改自己安装或记录为拥有的资源，路径被占用时直接拒绝。
- **默认保持小巧**：优先清晰边界，不引入复杂 overlay 或另一套 runtime。

### 文档与参与

- [CLI 中文文档](https://github.com/teamai-vault/teamai-cli-copilot/blob/main/README.zh-CN.md) · [English](https://github.com/teamai-vault/teamai-cli-copilot#readme) · [文档站](https://teamai-vault.github.io/teamai-cli-copilot/)
- [Marketplace 中文说明](https://github.com/teamai-vault/teamai-marketplace/blob/main/README.zh-CN.md) · [Plugin Guide](https://github.com/teamai-vault/teamai-marketplace/blob/main/docs/PLUGIN-GUIDE.md) · [贡献指南](https://github.com/teamai-vault/teamai-marketplace/blob/main/docs/CONTRIBUTING.md)
- 如有问题或改进建议，请在最相关的仓库中提交 Issue，并遵循该仓库的贡献说明。

<a href="#team-ai">返回顶部</a> · <a href="#english">English</a>

<div align="center">
  <sub>Built around GitHub Copilot's native capabilities.</sub>
</div>
