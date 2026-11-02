---
title: Install
nav_order: 2
has_children: true
permalink: /install/
---

# Install Parth
{: .no_toc }

Parth comes as **one extension or plugin per kind of IDE**. You install it the way you install anything else in that IDE, from its own marketplace. There is no server to set up: each person connects **their own** AI provider account inside Parth.

1. TOC
{:toc}

## Which guide do I need?

| Your IDE | What you install | Where it comes from | Guide |
|---|---|---|---|
| VS Code | The Parth extension | VS Code Marketplace (`ameyllc.parth`) | [VS Code](vscode.md) |
| Cursor | The same extension | Open VSX | [Cursor](cursor.md) |
| Windsurf, VSCodium, Trae, Positron, other VS Code forks | The same extension | Open VSX | [Other VS Code-based editors](other-vscode-editors.md) |
| IntelliJ IDEA, PyCharm, WebStorm, GoLand, Rider, CLion and other JetBrains IDEs | The Parth plugin | JetBrains Marketplace | [JetBrains IDEs](jetbrains.md) |

Other editors (Visual Studio, Eclipse, Xcode, Zed, Neovim, …) aren't supported: they can't load either one. Browser editors such as vscode.dev and github.dev can't run it either, because the agent runs as a local process.

## What you need

| | VS Code and editors built on it | JetBrains IDEs |
|---|---|---|
| **IDE version** | VS Code **1.95** or newer (for a fork, the VS Code version it's built on) | **2025.2** (build 252) or newer |
| **A project open** | A folder or workspace. The agent can only see and change files inside it | A project. Same rule |
| **An AI provider** | An account (API key or sign-in), or a local model server such as Ollama. No account is needed for local models | Same |
| **Node.js** | Not needed. The agent runs on the editor's own runtime | Not needed for the Marketplace version. A plugin installed from a file needs **Node.js 20+** on the same computer |
| **Internet** | To reach your provider (not for local models) | Same |

## How the IDEs differ

The chat, modes, providers and review work the same everywhere. These details differ:

| | VS Code and forks | JetBrains IDEs |
|---|---|---|
| **Where the panel is** | The **Parth** icon in the Activity Bar on the left | The **Parth** tool window on the right edge |
| **Open it with** | Command Palette → **Parth: Focus on Chat View** | Click **Parth** on the right edge |
| **Where settings are** | Settings → search *Parth*, or `settings.json` (`parth.*`) | **Settings → Tools → Parth** |
| **Menu commands** | Command Palette → type *Parth* | **Tools → Parth** |
| **Add selection to chat** | <kbd>Cmd</kbd>+<kbd>Alt</kbd>+<kbd>L</kbd> (<kbd>Ctrl</kbd>+<kbd>Alt</kbd>+<kbd>L</kbd> on Windows and Linux) | <kbd>⌥</kbd>+<kbd>⌘</kbd>+<kbd>'</kbd> (<kbd>Ctrl</kbd>+<kbd>Alt</kbd>+<kbd>'</kbd> on Windows and Linux) |
| **Drag and drop files** | Hold <kbd>Shift</kbd> and drop on the chat. Files dragged from Finder or Windows Explorer can't be attached | Drop on the chat. No <kbd>Shift</kbd>. Files from Finder or Explorer work |
| **GitHub Copilot models** | Listed if the GitHub Copilot extension is installed and signed in | Not available |
| **Review in the editor** | Changed lines are highlighted, with **Keep** / **Undo** above each block | Per-file diff in the IDE's diff viewer |
| **Show the log** | **Parth: Show Logs** | **⚙ → About → Show logs** |

## After you install

Open the panel, then continue with [Set up Parth](../setup/index.md). If the install didn't work, see [Troubleshooting](../troubleshooting.md).
