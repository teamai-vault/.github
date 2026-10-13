<a id="top"></a>

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

Team AI is a thin control layer for teams building with GitHub Copilot. Each user selects one department Marketplace for shared Plugins, instructions, Skills, business context, and Learnings. The `teamai` CLI delivers user capabilities and projects context into explicitly bound Git workspaces, using native Copilot formats and a VS Code fallback for Plugin convergence.

**TeamAI V4 · CLI 0.5.1.** V4 names the product design; CLI, Marketplace and Plugin packages have independent versions. See the [implementation status and verification limits](https://github.com/teamai-vault/teamai-cli-copilot/blob/main/docs/HANDOFF.md) for the current delivery and remaining acceptance work.

### Start here

| Goal | Repository |
| --- | --- |
| Install the `teamai` CLI: initialize, bind a repository, sync, recall, contribute, diagnose | [teamai-cli-copilot](https://github.com/teamai-vault/teamai-cli-copilot) |
| Start a department Marketplace from the reference template | [teamai-marketplace](https://github.com/teamai-vault/teamai-marketplace) |
| See the architecture, file layout, and command examples at a glance | [Docs site](https://teamai-vault.github.io/teamai-cli-copilot/) |

### How it fits

```text
teamai-marketplace (department-owned, one per department)
  resource ref       plugins/  instructions/  skills/  manifest/projects.yaml  contexts/
  teamai-learnings   learnings/<project|shared>/<uuid>.md
        │ read
        ▼
teamai CLI + bundled teamai Skill / teamai-recall Agent
  init · projects set · sync · recall · status · doctor
        │                                   │
        ▼                                   ▼
your machine (~/.copilot)             your bound Git workspace
  common + 1 role Plugin enabled        .github/instructions/teamai/<id>/
  instructions/teamai/                  .teamai/context/   (docs, Learnings)
  skills/teamai/, teamai-recall Agent   project Plugin components, when declared
```

The CLI installs `common` and all role Plugins, enabling `common` plus the selected role. It uses native Copilot commands, or the VS Code fallback only when Copilot CLI is unavailable. A manifest-selected project package supplies workspace components; it is not installed as a user Plugin. The `teamai` Skill and `teamai-recall` Agent ship with the CLI.

Marketplace resources follow the configured source/ref. Published Learnings come only from `teamai-learnings`; Learning contributions open PRs there, while Skill contributions target the Marketplace's default branch. Both use isolated Git worktrees.

### Quick start

Requirements: Node.js 20+, Git, and the GitHub Copilot CLI (or a working `code` command for fallback Plugin convergence). The Marketplace maintainer must prepare its `teamai-learnings` branch. Contributions also require authenticated GitHub CLI (`gh`) access and a Git author identity.

```bash
git clone https://github.com/teamai-vault/teamai-cli-copilot.git
cd teamai-cli-copilot
npm install
npm run build
npm link

teamai init --marketplace teamai-vault/teamai-marketplace --role api   # once per machine
teamai projects list                                                  # discover logical project IDs
cd <your-business-repo>
teamai projects set <logical-project-id>                               # once per repository
teamai sync                                                            # whenever the team updates
teamai recall payment retry                                            # search team knowledge locally
```

Use your own department's Marketplace in place of `teamai-vault/teamai-marketplace`, and select a role and project ID from its catalog. To try V4 before it is merged, run `git switch teamai-v4` after cloning and before installing. After the merge, the normal default-branch installation above is sufficient.

`init` configures user scope only. `projects set <ids...>` replaces the current workspace binding; `projects set` with no IDs unbinds it. `sync` follows that workspace's saved binding. Every write command accepts `--dry-run`; it may read the network and use temporary directories, but does not persist product-state changes.

An absolute `COPILOT_HOME` can change the Copilot profile root; Team AI state still lives under `~/.teamai`. Keep the same profile when managing resources already owned by Team AI.

### What a Marketplace carries

- **Common Plugin**: capabilities shared by every role.
- **Role Plugins**: catalog-defined roles; the reference template includes `api`, `ios`, `aos` (Android), `qa`, and `design`. All role Plugins are installed; only `common` plus the selected role are enabled.
- **Instructions**: department-wide `*.instructions.md`, mirrored to `~/.copilot/instructions/teamai/`.
- **Team Skills**: standalone Skills governed by `skills.yaml`, installed on demand by name or tag.
- **Logical Projects**: business context in `contexts/<id>/`, explicitly bound with `teamai projects set`; optional `kind: project` packages supply native workspace Agents, Skills, rules, Hooks, MCP declarations and assets.
- **Learnings**: troubleshooting notes published through pull requests to the `teamai-learnings` branch and searchable with `teamai recall` or the bundled `teamai-recall` Agent.

### Recall and contribute

`teamai recall` searches verified local context and published Learnings without fetching or calling a model. V4 supports weighted lexical BM25 ranking, repeated literal `--require` filters, explicit user/workspace scopes with `--project` narrowing, and traceable file/line snippets. It uses the current binding to determine the default scope. Pending Learnings are excluded unless `--include-pending` is requested within the permitted source and scope.

The bundled `teamai-recall` Agent is instructed to invoke the CLI, read the cited originals and explain evidence gaps. `teamai learning share` freezes a local operation and payload before remote publication; `learning pending` lists local state, and `learning retry <operation-id>` resumes it. An open PR is not a published Learning. See the [CLI guide](https://github.com/teamai-vault/teamai-cli-copilot#readme) for commands, scope rules and recovery details.

### Principles

- **Native first**: compose with GitHub Copilot's existing CLI, Marketplace, and Agent Plugin surfaces.
- **Git-native**: shared capabilities and Learnings are versioned and reviewed in the Marketplace. Local context projections are excluded from Git using repository-local rules; this does not untrack existing files.
- **Explicit ownership**: reserved paths and ownership records separate managed resources from personal configuration. User-owned Plugins and unknown settings are preserved; keep personal instructions outside the managed `instructions/teamai/` subtree.
- **Small by default**: prefer a clear boundary over a clever overlay or another runtime.

### Learn and contribute

- [CLI README](https://github.com/teamai-vault/teamai-cli-copilot#readme) · [中文文档](https://github.com/teamai-vault/teamai-cli-copilot/blob/main/README.zh-CN.md) · [Docs site](https://teamai-vault.github.io/teamai-cli-copilot/)
- [Marketplace README](https://github.com/teamai-vault/teamai-marketplace#readme) · [Plugin Guide](https://github.com/teamai-vault/teamai-marketplace/blob/main/docs/PLUGIN-GUIDE.md) · [Contributing](https://github.com/teamai-vault/teamai-marketplace/blob/main/docs/CONTRIBUTING.md)
- For questions or changes, open an issue in the repository closest to the topic and follow its contribution guidance.

<a href="#top">Back to top</a> · <a href="#zh-cn">简体中文</a>

<a id="zh-cn"></a>

## 简体中文

Team AI 是面向团队的 GitHub Copilot 轻量控制层。每个用户选择一个部门 Marketplace，获取共享的 Plugin、Instructions、Skill、业务上下文和团队经验（Learnings）。`teamai` CLI 交付用户级能力，并向显式绑定的 Git workspace 投影项目上下文，沿用 Copilot 原生格式，也提供用于 Plugin 收敛的 VS Code fallback。

**TeamAI V4 · CLI 0.5.1。** V4 是产品方案名称；CLI、Marketplace 和 Plugin 包各自独立发版。[实现与验证状态](https://github.com/teamai-vault/teamai-cli-copilot/blob/main/docs/HANDOFF.md)列出了当前交付范围与尚未完成的验收。

### 从这里开始

| 目标 | 仓库 |
| --- | --- |
| 安装 `teamai` CLI：初始化、绑定仓库、同步、召回、贡献、诊断 | [teamai-cli-copilot](https://github.com/teamai-vault/teamai-cli-copilot) |
| 以参考模板创建部门自己的 Marketplace | [teamai-marketplace](https://github.com/teamai-vault/teamai-marketplace) |
| 一页看懂架构、文件位置和命令示例 | [文档站](https://teamai-vault.github.io/teamai-cli-copilot/) |

### 它们如何协作

```text
teamai-marketplace（部门自有，每个部门一个）
  resource ref       plugins/  instructions/  skills/  manifest/projects.yaml  contexts/
  teamai-learnings   learnings/<project|shared>/<uuid>.md
        │ 读取
        ▼
teamai CLI + 内置 teamai Skill / teamai-recall Agent
  init · projects set · sync · recall · status · doctor
        │                                   │
        ▼                                   ▼
你的机器（~/.copilot）                 已绑定的 Git workspace
  启用 common + 1 个 role Plugin         .github/instructions/teamai/<id>/
  instructions/teamai/                  .teamai/context/（Docs、Learnings）
  skills/teamai/、teamai-recall Agent   Project Plugin 声明的组件（按需）
```

CLI 安装 `common` 和全部 Role Plugin，只启用 `common` 与所选 Role。优先使用 Copilot 原生命令，仅当 Copilot CLI 不可用时选择 VS Code fallback。Manifest 选中的 Project package 提供 workspace 组件，不作为用户级 Plugin 安装。`teamai` Skill 与 `teamai-recall` Agent 随 CLI 交付。

Marketplace 资源遵循配置的 source/ref。已发布 Learnings 只来自 `teamai-learnings`；Learning 贡献向该分支提交 PR，Skill 贡献向 Marketplace 默认分支提交 PR。两种贡献都使用隔离的 Git worktree。

### 快速开始

环境要求：Node.js 20+、Git，以及 GitHub Copilot CLI（或用于 fallback Plugin 收敛的可用 `code` 命令）。Marketplace 维护者需要先准备 `teamai-learnings` 分支。贡献还需要已认证的 GitHub CLI（`gh`）及 Git 作者身份。

```bash
git clone https://github.com/teamai-vault/teamai-cli-copilot.git
cd teamai-cli-copilot
npm install
npm run build
npm link

teamai init --marketplace teamai-vault/teamai-marketplace --role api   # 每台机器一次
teamai projects list                                                  # 查看可绑定的逻辑项目 ID
cd <your-business-repo>
teamai projects set <logical-project-id>                               # 每个仓库一次
teamai sync                                                            # 团队内容更新后
teamai recall 支付 重试                                                 # 本地检索团队知识
```

请把 `teamai-vault/teamai-marketplace` 换成所在部门的 Marketplace，并从其 catalog 中选择 Role 和项目 ID。V4 合并前，如需试用该分支，请在 clone 后、安装前运行 `git switch teamai-v4`；合并后直接按上面的默认分支安装即可。

`init` 只配置用户范围。`projects set <ids...>` 替换当前 workspace 的绑定；不带 ID 的 `projects set` 解除绑定。`sync` 按当前 workspace 已保存的绑定同步。所有写命令都支持 `--dry-run`；预演可能读取网络和使用临时目录，但不会持久化产品状态变更。

绝对路径形式的 `COPILOT_HOME` 可改变 Copilot profile 根目录，Team AI 状态仍位于 `~/.teamai`。管理已有的 Team AI 资源时，应保持相同的 profile。

### Marketplace 里有什么

- **Common Plugin**：所有 Role 共用的能力。
- **Role Plugin**：由 catalog 定义；参考模板包含 `api`、`ios`、`aos`（Android）、`qa`、`design`。全部 Role Plugin 都会安装，只启用 `common` 和所选 Role。
- **Instructions**：部门级 `*.instructions.md`，镜像到 `~/.copilot/instructions/teamai/`。
- **Team Skills**：由 `skills.yaml` 治理的 standalone Skill，按名字或 Tag 按需安装。
- **Logical Project**：`contexts/<id>/` 中的业务上下文，用 `teamai projects set` 显式绑定；可选的 `kind: project` package 提供原生 workspace Agent、Skill、rules、Hook、MCP 声明及 assets。
- **Learnings**：排障与踩坑记录，经 Pull Request 发布到 `teamai-learnings` 分支，可用 `teamai recall` 或内置的 `teamai-recall` Agent 检索。

### 召回与贡献

`teamai recall` 检索经过校验的本地 context 和已发布 Learnings，不拉取远端，也不调用模型。V4 支持加权词法 BM25 排序、可重复的字面量 `--require` 过滤、显式 user/workspace scope 及 `--project` 缩小范围，以及可追溯到文件和行号的片段。默认范围取决于当前绑定。Pending Learnings 默认排除，只有显式传入 `--include-pending` 才会在允许的来源与范围内纳入。

内置 `teamai-recall` Agent 的指令要求调用 CLI、读取引用原文，并说明证据缺口。`teamai learning share` 在远端发布前冻结本地 operation 与 payload；`learning pending` 列出本地状态，`learning retry <operation-id>` 续跑同一条操作。PR 已打开不等于 Learning 已发布。命令、Scope 和恢复细节见 [CLI 中文指南](https://github.com/teamai-vault/teamai-cli-copilot/blob/main/README.zh-CN.md)。

### 原则

- **优先使用原生能力**：组合 GitHub Copilot 已有的 CLI、Marketplace 和 Agent Plugin。
- **Git-native**：共享能力和 Learnings 在 Marketplace 中版本化并经过评审。本地 context 投影通过仓库本地规则排除，不会因此取消已有文件的 Git 跟踪。
- **边界明确**：保留路径与 ownership 记录区分受管资源和个人配置。保留用户自有 Plugin 及未知设置；个人 instructions 应放在受管 `instructions/teamai/` 子树之外。
- **默认保持小巧**：优先清晰边界，不引入复杂 overlay 或另一套 runtime。

### 文档与参与

- [CLI 中文文档](https://github.com/teamai-vault/teamai-cli-copilot/blob/main/README.zh-CN.md) · [English](https://github.com/teamai-vault/teamai-cli-copilot#readme) · [文档站](https://teamai-vault.github.io/teamai-cli-copilot/)
- [Marketplace 中文说明](https://github.com/teamai-vault/teamai-marketplace/blob/main/README.zh-CN.md) · [Plugin Guide](https://github.com/teamai-vault/teamai-marketplace/blob/main/docs/PLUGIN-GUIDE.md) · [贡献指南](https://github.com/teamai-vault/teamai-marketplace/blob/main/docs/CONTRIBUTING.md)
- 如有问题或改进建议，请在最相关的仓库中提交 Issue，并遵循该仓库的贡献说明。

<a href="#top">返回顶部</a> · <a href="#english">English</a>

<div align="center">
  <sub>Built around GitHub Copilot's native capabilities.</sub>
</div>
