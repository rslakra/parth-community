---
title: Home
nav_order: 1
description: Install Parth, set it up, and get help.
---

# Parth: AI coding agent for your IDE
{: .no_toc }

**Parth is an AI coding agent inside your IDE.** Describe a change in the chat and it reads your code, edits it, **updates the files that depend on the change**, checks its work with the IDE's inspections, and shows every edit for review. Use **any AI provider or a local model** with your own account, and keep or undo each change.

{% include screenshot.html src="chat-and-changes.png" width="380" alt="The Parth chat panel: a request with two attached files, the agent's steps, a command approval card, and the list of changed files with Keep and Undo" %}

## Start here: pick your IDE

| Your IDE | Where you get Parth | Guide |
|---|---|---|
| **VS Code** | VS Code Marketplace | [Install in VS Code](install/vscode.md) |
| **Cursor** | Open VSX, from Cursor's Extensions view | [Install in Cursor](install/cursor.md) |
| **Windsurf, VSCodium, Trae, Positron**, and other editors built on VS Code | Open VSX | [Install in other VS Code-based editors](install/other-vscode-editors.md) |
| **IntelliJ IDEA, PyCharm, WebStorm, GoLand, Rider, CLion** and other JetBrains IDEs (2025.2 or newer) | JetBrains Marketplace | [Install in a JetBrains IDE](install/jetbrains.md) |

Not sure which one applies, or what Parth needs? See [Install: requirements and differences](install/index.md).

## Then, in five steps

1. **[Install it](install/index.md)** in your IDE and open the **Parth** panel.
2. **[Connect an AI provider](setup/connect-provider.md)**: paste an API key or sign in. Or run a [local model](guides/local-models.md) with no account at all.
3. **[Pick a model and a mode](setup/models-and-modes.md)**: Agent edits files, Plan and Ask are read-only.
4. **[Ask for a change](setup/ask-for-a-change.md)**, [attaching the files](setup/attach-context.md) that matter.
5. **[Review what changed](setup/review-changes.md)**: open a diff, then **Keep** or **Undo** each file.

You stay in control the whole time: [permissions](setup/permissions.md) decide what the agent may do without asking, and deleting files always asks.

## What you can do with it

- **Attach context your way:** `@` search, 📎, drag and drop, right-click → **Add to Parth Chat**, selected code, pasted code and screenshots.
- **Three modes:** **Agent** edits files and checks the result. **Plan** and **Ask** are read-only.
- **Any provider, your choice of model:** Anthropic, OpenAI, OpenRouter, Google Gemini and Vertex AI, AWS Bedrock, Azure OpenAI / Foundry, any OpenAI-compatible server, Ollama and LM Studio, and GitHub Copilot models in VS Code.
- **Your organization's AI gateway:** add a [company provider](guides/company-providers.md) and share one file with a team.
- **Edits that reach every affected file:** the agent uses the IDE's own language services: go to symbol, find references, rename, diagnostics.
- **Review everything:** every change is listed with a diff and **Keep** / **Undo**, per file or all at once.
- **Pick up where you left off:** the 🕘 button lists your earlier chats in the project.

## Need help?

| | |
|---|---|
| Something doesn't work | [Troubleshooting](troubleshooting.md) |
| You found a bug, or want a feature | [Report a bug or request a feature](report-an-issue.md) |
| What changed in each version | [Changelog](changelog.md) |
| How your data is handled | [Privacy](privacy.md) and [Security](security.md) |
