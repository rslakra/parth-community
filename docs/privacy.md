---
title: Privacy
nav_order: 8
---

# Privacy
{: .no_toc }

Parth runs entirely on your machine. It has no servers and collects no telemetry.

## What leaves your machine

Your prompts, the files you attach (from the project or anywhere else you choose), and the file contents the agent reads to answer them, go to the AI provider **you** connect: Anthropic, OpenAI, Google, AWS, Microsoft, OpenRouter, or a server you run. The request uses your own account, under that provider's terms and privacy policy.

Local providers (Ollama, LM Studio) keep everything on your machine.

## What stays on your machine

- **Saved chats.** So you can reopen an earlier chat from the history menu, Parth saves each chat (your messages, the answers, and the files and command output in them) in `~/.parth/chats` on your computer, or in `PARTH_CHATS_DIR` if you set it. The files are readable only by you and are never uploaded. The newest 100 are kept. Delete one from the history menu, or delete the folder. Treat the folder like your project: it can contain your code and command output.
- **In your project.** The only file Parth writes there is `.parth/settings.json`, and only if you pick a project for a company gateway that bills per project. It holds that choice (one line per provider) and nothing else. See [Company providers](guides/company-providers.md#projects).
- **Credentials.** API keys and sign-in tokens are stored in your IDE's secure storage (VS Code SecretStorage and the OS keychain; JetBrains Password Safe). They're sent only to the provider they belong to. The chat panel only ever sees a masked key, and the logs never contain keys.
- **Local network.** The IDE runs a tool server on `127.0.0.1` (loopback only, protected by a token) that the agent uses to read and edit files. It isn't reachable from other machines.

## What the agent can and can't see

- The agent can only see and change files **inside the open project**. Secret files (`.env`, keys, `.git`) are never read or sent, and neither are binary files.
- Files you attach from outside the project are sent **read-only**.

## Downloads

The JetBrains plugin may download its agent-core binary once from the project's GitHub release, and verifies its SHA-256 checksum before using it.

## Questions

Ask in [Discussions](https://github.com/rslakra/parth-community/discussions), or see [Security](security.md) to report a vulnerability.
