---
title: VS Code
parent: Install
nav_order: 1
---

# Install Parth in VS Code
{: .no_toc }

1. TOC
{:toc}

## Before you start

- **VS Code 1.95 or newer.** Check in **Help → About** (on macOS: **Code → About Visual Studio Code**).
- **Desktop VS Code.** vscode.dev and github.dev can't run Parth.
- **A folder or workspace to open.** Parth can only see and change files inside it, and it doesn't start until one is open. A new VS Code window is empty, so use **File → Open Folder…** first (see [the FAQ](../faq.md#open-a-folder)).
- **An AI provider account**, or a local model server such as Ollama. You connect it after installing.

## Install

Use any one of these.

### From the Extensions view (recommended)

1. Open the **Extensions** view: <kbd>Cmd</kbd>+<kbd>Shift</kbd>+<kbd>X</kbd> (<kbd>Ctrl</kbd>+<kbd>Shift</kbd>+<kbd>X</kbd> on Windows and Linux).
2. Type **Parth** in the search box.
3. Choose **Parth — AI Coding Agent** by **Amey LLC** (the ID is `ameyllc.parth`), and click **Install**.

<!-- screenshot needed: vscode-extensions-search.png — the Extensions view with "Parth" typed in the search box and the Install button -->

### From the Marketplace website

Open the [Parth page on the VS Code Marketplace](https://marketplace.visualstudio.com/items?itemName=ameyllc.parth) and click **Install**. Your browser asks to open VS Code, which then shows the extension. Click **Install** there.

### From a terminal

```bash
code --install-extension ameyllc.parth
```

If `code` isn't found, run **Shell Command: Install 'code' command in PATH** from the Command Palette first.

### From a `.vsix` file

If you were given a `parth.vsix` file (for example by your organization):

1. Open the **Extensions** view.
2. Click **⋯** at the top of the view → **Install from VSIX…**.
3. Choose the file. Click **Reload** if VS Code asks.

Or from a terminal: `code --install-extension parth.vsix --force`.

## Check that it's installed

- A **Parth** icon (a chat bubble with `</>`) appears in the **Activity Bar** on the left.
- A **Parth** button also appears in the editor's title bar. It opens the chat in the sidebar.
- In the Extensions view, **Parth — AI Coding Agent** is listed under *Installed*.

If you don't see the icon, open the Command Palette (<kbd>Cmd</kbd>+<kbd>Shift</kbd>+<kbd>P</kbd>) and run **Parth: Focus on Chat View**.

<!-- screenshot needed: vscode-activity-bar.png — the Activity Bar with the Parth icon, and the Parth panel open -->

## Open the panel

Click the **Parth** icon, or run **Parth: Focus on Chat View**. A new install asks you to **Connect an AI provider**: continue with [Connect a provider](../setup/connect-provider.md).

{% include screenshot.html src="connect-provider.png" width="300" alt="First run: the chat asks you to connect an AI provider" %}

## The commands

Open the Command Palette and type **Parth**:

| Command | What it does |
|---|---|
| **Parth: Open Chat** | Opens the chat in the sidebar (the title-bar button does the same) |
| **Parth: Focus on Chat View** | Moves the focus to the chat |
| **Parth: New Chat** | Starts a new chat. The old one stays in the history |
| **Parth: Clear Attachments** | Removes every file attached to the next message |
| **Parth: Keep All Changes** / **Parth: Undo All Changes** | Keeps or undoes every change the agent made |
| **Parth: Set Provider API Key** | Opens the password prompt for a provider's key |
| **Parth: Sign Out of a Provider** | Signs out of a provider |
| **Parth: Restart Agent Core** | Restarts the agent process, if it's stuck |
| **Parth: Show Logs** | Opens the Parth log in the Output panel |

**Add to Parth Chat** is in the right-click menu of the Explorer and of editor tabs. **Add Selection to Parth Chat** is in the editor's right-click menu, and is bound to <kbd>Cmd</kbd>+<kbd>Alt</kbd>+<kbd>L</kbd> (<kbd>Ctrl</kbd>+<kbd>Alt</kbd>+<kbd>L</kbd> on Windows and Linux). Change the shortcut in **Keyboard Shortcuts** (search for *Parth*).

## Settings

Open **Settings** (<kbd>Cmd</kbd>+<kbd>,</kbd>) and search for **Parth**, or edit `settings.json`. The options are listed in [Settings](../setup/settings.md#settings-in-vs-code).

## Update

VS Code updates extensions by itself. To update now, open the **Extensions** view, click **Parth**, and click **Update**. A notification offers **Reload Window** after an install or update: click it.

## Uninstall

**Extensions** view → **Parth** → **Uninstall**. Your saved chats stay in `~/.parth/chats` until you delete that folder.

## Known issue: VS Code 1.140.0 and drag and drop

On VS Code **1.140.0**, dropping files onto the chat doesn't work. Attach files with `@`, 📎 or right-click → **Add to Parth Chat** instead, or see the [fix](../troubleshooting.md#vs-code-1140-drag-and-drop-stops-working).

## Next

[Connect a provider](../setup/connect-provider.md) · [Set up Parth](../setup/index.md) · [Troubleshooting](../troubleshooting.md) · [Report a problem](../report-an-issue.md)
