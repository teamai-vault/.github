# .github

Organization profile and shared GitHub configuration for Team AI.

The organization's public homepage is [`profile/README.md`](profile/README.md), with English and Simplified Chinese sections. This root README is for repository maintainers.

Keep the profile aligned with the [CLI documentation](https://github.com/teamai-vault/teamai-cli-copilot#readme), its [current implementation status](https://github.com/teamai-vault/teamai-cli-copilot/blob/main/docs/HANDOFF.md), and the [Marketplace reference template](https://github.com/teamai-vault/teamai-marketplace#readme). CLI, Marketplace and Plugin package versions are independent; V4 is the product design line.

Prepare profile updates alongside the corresponding product branch. Merging this repository's changes into its default branch updates the organization profile; the CLI's GitHub Pages site is maintained separately in `teamai-cli-copilot/docs/index.html` and served from `main:/docs`.

维护时请同步更新首页的中英文内容，并以 CLI 源码、公开帮助和 Marketplace 实际声明为准。纯文档改动检查事实、链接和排版即可。历史测量、CI 通过和原生 consumer 验收应分别表述。
