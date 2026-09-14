<div align="center">
  <h1>Team AI</h1>
  <p><strong>Git-native tooling for consistent, team-wide GitHub Copilot capabilities.</strong></p>
  <p>
    <a href="https://github.com/teamai-vault/teamai-cli-customization">team-ai CLI</a> ·
    <a href="https://github.com/teamai-vault/teamai-marketplace">Plugin Marketplace</a> ·
    <a href="https://github.com/teamai-vault">Organization</a>
  </p>
</div>

Team AI is a lightweight control layer for teams building with GitHub Copilot. It standardizes shared capabilities without introducing a second agent runtime, a custom plugin format, or an IDE-specific integration layer.

## Start here

| Goal | Repository |
| --- | --- |
| Bootstrap a machine, select a role, sync shared plugins, and diagnose state | [teamai-cli-customization](https://github.com/teamai-vault/teamai-cli-customization) |
| Browse and validate reusable Copilot Agent Plugins | [teamai-marketplace](https://github.com/teamai-vault/teamai-marketplace) |

## How it fits

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

## Quick start

Requirements: Node.js 20+, Git, and the GitHub Copilot CLI.

```text
git clone https://github.com/teamai-vault/teamai-cli-customization.git
cd teamai-cli-customization
npm install
npm run build
npm link
team-ai init --role api
```

## Capability tracks

- **Common** — shared capabilities used across roles
- **API** — backend and API development
- **iOS** — iOS development
- **Android** — Android development
- **QA** — quality and test workflows
- **Design** — product and experience design

Product capabilities are added when a real cross-project use case exists.

## Principles

- **Native first** — compose with GitHub Copilot's existing CLI, Marketplace, and Agent Plugin surfaces.
- **Git-native** — shared capabilities are versioned in Git; project customization stays next to the code it serves.
- **Explicit ownership** — automation changes only the resources it installed or owns.
- **Small by default** — prefer a clear boundary over a clever overlay or another runtime.

## Learn and contribute

- [CLI documentation](https://github.com/teamai-vault/teamai-cli-customization#readme) · [中文文档](https://github.com/teamai-vault/teamai-cli-customization/blob/main/README.zh-CN.md)
- [Marketplace Plugin Guide](https://github.com/teamai-vault/teamai-marketplace/blob/main/docs/PLUGIN-GUIDE.md) · [中文说明](https://github.com/teamai-vault/teamai-marketplace/blob/main/README.zh-CN.md)
- For questions or changes, use the issue tracker and contribution guidance in the repository most closely related to the topic.

<div align="center">
  <sub>Built around GitHub Copilot's native capabilities.</sub>
</div>
