<div align="center">
  <h1>Team AI</h1>
  <p><strong>Git-native tooling for consistent, team-wide GitHub Copilot capabilities.</strong></p>
  <p>
    <a href="#english">English</a> ·
    <a href="#zh-cn">简体中文</a>
  </p>
  <p>
    <a href="https://github.com/teamai-vault/teamai-cli-customization">team-ai CLI</a> ·
    <a href="https://github.com/teamai-vault/teamai-marketplace">Plugin Marketplace</a>
  </p>
</div>

<a id="english"></a>

## English

Team AI is a lightweight control layer for teams building with GitHub Copilot. It standardizes shared capabilities without introducing a second agent runtime, a custom plugin format, or an IDE-specific integration layer.

### Start here

| Goal | Repository |
| --- | --- |
| Bootstrap a machine, select a role, sync shared plugins, and diagnose state | [teamai-cli-customization](https://github.com/teamai-vault/teamai-cli-customization) |
| Browse and validate reusable Copilot Agent Plugins | [teamai-marketplace](https://github.com/teamai-vault/teamai-marketplace) |

### How it fits

```text
teamai-marketplace
  shared Common / Role / Product capabilities
              ↓ native Copilot Marketplace + Agent Plugins
team-ai CLI
  bootstrap · sync · role · status · doctor
              ↓
your business repository
  project-specific .github/* customization
```

Shared capabilities live in the Marketplace. Project-specific behavior stays with the business repository. `team-ai` connects the two while managing only the state it owns.

### Quick start

Requirements: Node.js 20+, Git, and the GitHub Copilot CLI.

```text
git clone https://github.com/teamai-vault/teamai-cli-customization.git
cd teamai-cli-customization
npm install
npm run build
npm link
team-ai init --role api
```

### Capability tracks

- **Common** — shared capabilities used across roles
- **API** — backend and API development
- **iOS** — iOS development
- **Android** — Android development
- **QA** — quality and test workflows
- **Design** — product and experience design

Product capabilities are added when a real cross-project use case exists.

### Principles

- **Native first** — compose with GitHub Copilot's existing CLI, Marketplace, and Agent Plugin surfaces.
- **Git-native** — shared capabilities are versioned in Git; project customization stays next to the code it serves.
- **Explicit ownership** — automation changes only the resources it installed or owns.
- **Small by default** — prefer a clear boundary over a clever overlay or another runtime.

### Learn and contribute

- [CLI documentation](https://github.com/teamai-vault/teamai-cli-customization#readme) · [中文文档](https://github.com/teamai-vault/teamai-cli-customization/blob/main/README.zh-CN.md)
- [Marketplace Plugin Guide](https://github.com/teamai-vault/teamai-marketplace/blob/main/docs/PLUGIN-GUIDE.md) · [中文说明](https://github.com/teamai-vault/teamai-marketplace/blob/main/README.zh-CN.md)
- For questions or changes, use the issue tracker and contribution guidance in the repository most closely related to the topic.

<a href="#team-ai">Back to top</a> · <a href="#zh-cn">简体中文</a>

<a id="zh-cn"></a>

## 简体中文

Team AI 是面向团队的 Git-native 工具，用于让 GitHub Copilot 能力变得一致、可复用、可诊断。它不引入第二套 Agent Runtime、自定义 Plugin 格式或 IDE 专属适配层，而是围绕 Copilot 原生能力提供轻量控制层。

### 从这里开始

| 目标 | 仓库 |
| --- | --- |
| 初始化机器、选择 Role、同步共享 Plugin、诊断状态 | [teamai-cli-customization](https://github.com/teamai-vault/teamai-cli-customization) |
| 浏览并验证可复用的 Copilot Agent Plugin | [teamai-marketplace](https://github.com/teamai-vault/teamai-marketplace) |

### 它们如何协作

```text
teamai-marketplace
  共享 Common / Role / Product capabilities
              ↓ Copilot 原生 Marketplace + Agent Plugin
team-ai CLI
  bootstrap · sync · role · status · doctor
              ↓
真实业务仓库
  项目专属 .github/* customization
```

共享能力放在 Marketplace 中；项目专属行为跟随真实业务仓库。`team-ai` 负责连接两者，并且只管理自己拥有的状态。

### 快速开始

环境要求：Node.js 20+、Git，以及 GitHub Copilot CLI。

```text
git clone https://github.com/teamai-vault/teamai-cli-customization.git
cd teamai-cli-customization
npm install
npm run build
npm link
team-ai init --role api
```

### 能力方向

- **Common** —— 跨 Role 共用的能力
- **API** —— 后端与 API 开发
- **iOS** —— iOS 开发
- **Android** —— Android 开发
- **QA** —— 质量与测试流程
- **Design** —— 产品与体验设计

只有出现真实的跨项目场景时，才会增加 Product capabilities。

### 原则

- **优先使用原生能力** —— 组合 GitHub Copilot 已有的 CLI、Marketplace 和 Agent Plugin 能力。
- **Git-native** —— 共享能力在 Git 中版本化；项目定制跟随它服务的代码。
- **边界明确** —— 自动化只修改自己安装或拥有的资源。
- **默认保持小巧** —— 优先清晰边界，不引入复杂 overlay 或另一套 runtime。

### 文档与参与

- [CLI 中文文档](https://github.com/teamai-vault/teamai-cli-customization/blob/main/README.zh-CN.md) · [English](https://github.com/teamai-vault/teamai-cli-customization#readme)
- [Marketplace 中文说明](https://github.com/teamai-vault/teamai-marketplace/blob/main/README.zh-CN.md) · [Plugin Guide](https://github.com/teamai-vault/teamai-marketplace/blob/main/docs/PLUGIN-GUIDE.md)
- 如有问题或改进建议，请在最相关的仓库中提交 Issue，并遵循该仓库的贡献说明。

<a href="#team-ai">返回顶部</a> · <a href="#english">English</a>

<div align="center">
  <sub>Built around GitHub Copilot's native capabilities.</sub>
</div>
