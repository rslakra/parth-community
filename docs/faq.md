---
title: FAQ
nav_order: 6
---

# Frequently asked questions
{: .no_toc }

Short answers to the things people ask in their first hour with Parth. For a fix to a specific error, see [Troubleshooting](troubleshooting.md).

1. TOC
{:toc}

## What the message in the chat box means

When Parth can't take a request yet, the chat box is greyed out and says why. These are the messages, and what to do about each:

| The chat box says | What it means | What to do |
|---|---|---|
| **Open a folder or workspace to use Parth.** | No project is open in your IDE | [Open a folder](#open-a-folder) |
| **Starting the agent…** | Parth's agent is starting. It takes a few seconds | Wait a moment. If it never goes away, see [the agent doesn't start](#agent-doesnt-start) |
| **Connect a provider to start** | No AI provider is connected yet | [Connect a provider](setup/connect-provider.md) |
| **Pick a model below to start** | A provider is connected, but no model is chosen | Click the model name in the box and pick one: [Models and modes](setup/models-and-modes.md) |

<!-- screenshot needed: faq-open-a-folder.png — the Parth panel in an IDE window with no folder open, the chat box greyed out and showing "Open a folder or workspace to use Parth." -->

### Why does the chat say "Open a folder or workspace to use Parth."? {#open-a-folder}

Parth works **inside a project**. It can only see and change files in the folder you have open, and that's a safety rule, not a limitation you can switch off. With no folder open there is nothing for it to work on, so it waits.

This is the usual state of a **new VS Code window** right after you install Parth, because VS Code opens empty.

1. Open a project: **File → Open Folder…** (<kbd>Cmd</kbd>+<kbd>O</kbd> on macOS, <kbd>Ctrl</kbd>+<kbd>K</kbd> <kbd>Ctrl</kbd>+<kbd>O</kbd> on Windows and Linux).
2. VS Code reloads the window, and Parth starts by itself.
3. Open the Parth panel and [connect a provider](setup/connect-provider.md).

{: .note }
**Until a folder is open, the Providers list is empty too.** Parth's agent isn't running yet, so it can't list the providers. If you open **⚙ → Providers** and see no **Available Providers**, open a folder first. They appear as soon as the message goes away.

In a JetBrains IDE you don't see this, because the Parth tool window only exists inside an open project.

### The agent doesn't start: "Starting the agent…" never goes away {#agent-doesnt-start}

Parth runs its agent as a separate process, and it normally starts in a few seconds. If the message stays:

1. Open the log: **Parth: Show Logs** (VS Code and forks) or **⚙ → About → Show logs** (JetBrains).
2. Restart the agent: **⚙ → About → Restart agent**, or **Parth: Restart Agent Core** in the Command Palette.
3. Still stuck? [Report it](report-an-issue.md) with the log lines.

## Getting started

### Do I need an account?

Not with Parth: it has no accounts and no servers. You connect **your own** account with an AI provider (Anthropic, OpenAI, Google, AWS, Microsoft, OpenRouter, and others), with an API key or by signing in. That's where the model runs and where you pay, if the provider charges. See [Connect a provider](setup/connect-provider.md).

### I don't have an API key. Can I still try it?

Yes, in two ways:

- **A local model.** Ollama and LM Studio run on your computer with no account and nothing sent to the cloud: [Local models](guides/local-models.md).
- **The Offline Mock model.** Turn it on in **⚙ → Agent**. It gives scripted answers, but they go through the real tool pipeline, so you can try attaching files and Keep / Undo.

### Which provider should I choose?

Any one will do, and you can connect several and switch with the model menu. If you're unsure: use the provider you already have a key for. To edit files, a model has to support tool calling: a model without it can chat but can't change your project (this matters most for [local models](guides/local-models.md)). If your company runs an AI gateway, ask your admin for its [providers file](guides/company-providers.md).

### Where do I find Parth after installing?

- **VS Code, Cursor, Windsurf and other VS Code-based editors:** the **Parth** icon in the Activity Bar, or **Parth: Focus on Chat View** in the Command Palette (<kbd>Cmd</kbd>+<kbd>Shift</kbd>+<kbd>P</kbd>). A **Parth** button in the editor's title bar also opens it.
- **JetBrains IDEs:** the **Parth** button on the right edge.

If you can't see it, see the install guide for your IDE: [Install](install/index.md).

### Do I need Node.js?

No. In VS Code and the editors built on it, Parth runs on the editor's own runtime. In a JetBrains IDE, the plugin from the Marketplace doesn't need it either. Only a plugin installed from a `.zip` file needs Node.js 20 or newer.

### Does it work in the browser (vscode.dev, github.dev)?

No. The agent runs as a program on your computer, so you need the desktop editor.

## Providers and models

### Sign in or API key: which button?

- **API key:** the IDE's password box opens, you paste the key, and Parth checks it and stores it in the IDE's secure storage.
- **Sign in:** for Anthropic, OpenAI and Google Gemini, it opens the provider's page where you create a key. For OpenRouter, it signs you in through your browser. Azure, AWS and Google Vertex AI sign in with your cloud login.

If **Sign in** is greyed out, that provider's sign-in needs an app ID. Use **API key** instead.

### Where is my API key stored? Does Parth send it anywhere?

In your IDE's secure storage (your operating system's keychain). It goes only to the provider it belongs to. It never appears in the chat or in the logs.

### A model I expect isn't in the model menu

Click **⟳** in the model menu to refresh it. Then check **⚙ → Models**: each model has a switch, and a model that's switched off is hidden. If the provider's row shows an error, fix that first: [Troubleshooting](troubleshooting.md).

### Can I use my company's AI gateway?

Yes. Add it as a **company provider**, or import the providers file your admin gave you: [Company providers](guides/company-providers.md).

## Working in a project

### Which files can Parth see and change?

Only the files inside the folder you have open. It never reads secret files (`.env`, keys, `.git`), and it can't touch anything outside the project. You can still attach a file from elsewhere on your computer to a message: it's sent **read-only**. See [Attach files](setup/attach-context.md) and [Permissions](setup/permissions.md).

### Parth changed my file, but it isn't saved

That's on purpose. Edits to existing files change the open editor but aren't saved until you click **Keep**. Click a file in the **files changed** card to see the diff, then **Keep** or **Undo**: [Review changes](setup/review-changes.md).

### How do I undo what Parth did?

Click **↺ Undo** on a file in the **files changed** card, or **Undo all**. Undo also puts back a file Parth deleted and removes one it created.

### Why does Parth ask before running a command?

By default, every command asks first. You choose how much it may do without asking with the **Permissions** pill: **Manual**, **Auto Edit** or **Auto**. Deleting files always asks, in every mode. See [Permissions](setup/permissions.md).

### Can I stop it?

Yes. **■ Stop** replaces the send button while it works. It cancels the request and ends any command it started.

### Where are my chats kept? How do I delete one?

On your computer only, in `~/.parth/chats`, readable only by you. Open the **🕘** history and click the bin next to a chat to delete it, or delete the folder. Nothing is uploaded. See [Ask for a change](setup/ask-for-a-change.md#chat-history).

## Other editors

### I use Cursor or Windsurf. Does Parth replace its AI?

No. Parth and the editor's own AI assistant run side by side. They don't share chats, models or settings. GitHub Copilot models only show up where the GitHub Copilot extension is installed and signed in.

### The chat panel doesn't open in Android Studio

Android Studio's bundled Java runtime has no embedded browser (JCEF), which the chat panel needs. Use VS Code or another JetBrains IDE.

## Your data

### What does Parth send, and to whom?

Your prompts, the files you attach, and the file contents the agent reads to answer you go to the AI provider **you** connected, under your own account. Parth has no servers of its own and collects no telemetry. With a local model, nothing leaves your computer. See [Privacy](privacy.md).

## Still have a question?

- Check [Troubleshooting](troubleshooting.md) for a specific error.
- Ask in [Discussions](https://github.com/rslakra/parth-community/discussions).
- [Report a bug or request a feature](report-an-issue.md).

## Enjoying Parth?

A short review helps other developers find it: [VS Code Marketplace](https://marketplace.visualstudio.com/items?itemName=ameyllc.parth&ssr=false#review-details) · [JetBrains Marketplace](https://plugins.jetbrains.com/plugin/35700-parth--ai-coding-agent/reviews) · [star the project on GitHub](https://github.com/rslakra/parth-community).
