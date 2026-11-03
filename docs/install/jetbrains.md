---
title: JetBrains IDEs
parent: Install
nav_order: 2
---

# Install Parth in IntelliJ IDEA and other JetBrains IDEs
{: .no_toc }

The Parth plugin works in any JetBrains IDE **2025.2 (build 252) or newer**: IntelliJ IDEA, PyCharm, WebStorm, GoLand, Rider, CLion and the rest. For example, PyCharm 2025.2, IntelliJ IDEA 2025.3 and IntelliJ IDEA 2026.1 all work.

1. TOC
{:toc}

## Before you start

- **IDE version 2025.2 or newer.** Check in **Help → About**.
- **A runtime with JCEF**, the embedded browser the chat panel runs in. The IDE's default runtime has it.
- **A project open.** Parth can only see and change files inside it.
- **An AI provider account**, or a local model server such as Ollama.
- **Node.js 20 or newer is only needed** if you install the plugin from a file instead of the Marketplace. The Marketplace version downloads what it needs, so you don't need Node.js.

### Android Studio

Android Studio **2025.2.1 or newer** installs the plugin, but its bundled Java runtime has no JCEF. The Parth tool window then says so, instead of showing the chat. Use VS Code, or a JetBrains IDE whose runtime has JCEF.

## Install

### From the JetBrains Marketplace (recommended)

1. Open **Settings** (<kbd>Cmd</kbd>+<kbd>,</kbd> on macOS; **File → Settings** or <kbd>Ctrl</kbd>+<kbd>Alt</kbd>+<kbd>S</kbd> on Windows and Linux) → **Plugins**.
2. Open the **Marketplace** tab and search for **Parth**.
3. Choose **Parth - AI Coding Agent** by **Amey LLC**, and click **Install**.
4. Click **Restart IDE** when it asks. Parth needs a restart to load.

<!-- screenshot needed: jetbrains-plugins-marketplace.png — Settings → Plugins → Marketplace with "Parth" searched and the Install button -->

### From a plugin zip file

If you were given a `parth-<version>.zip` file:

1. Open **Settings** → **Plugins**.
2. Click the **⚙** gear at the top → **Install Plugin from Disk…**.
3. Choose the zip. Don't unzip it.
4. Click **Restart IDE**.

A plugin installed this way needs **Node.js 20+** on the same computer. If the plugin says it can't find Node.js, set its path in **Settings → Tools → Parth → Node.js path** (for example `/opt/homebrew/bin/node`; `which node` in a terminal shows yours).

## Check that it's installed

- A **Parth** tool-window button appears on the **right** edge of the IDE.
- **Settings → Tools → Parth** exists.
- The **Tools → Parth** menu has *New Chat*, *Keep All Agent Changes*, *Undo All Agent Changes* and *Restart Agent Core*.
- **Settings → Plugins → Installed** lists **Parth - AI Coding Agent**.

<!-- screenshot needed: jetbrains-tool-window.png — an IDE with the Parth tool window open on the right edge -->

## Open the panel

Click **Parth** on the right edge. A new install asks you to **Connect an AI provider**: continue with [Connect a provider](../setup/connect-provider.md).

## Menus, shortcuts and settings

| What | Where |
|---|---|
| **New Chat**, **Keep All Agent Changes**, **Undo All Agent Changes**, **Restart Agent Core** | **Tools → Parth** |
| **Add to Parth Chat** | Right-click in the Project view, or on an editor tab |
| **Add Selection to Parth Chat** | Right-click in the editor, or <kbd>⌥</kbd>+<kbd>⌘</kbd>+<kbd>'</kbd> (<kbd>Ctrl</kbd>+<kbd>Alt</kbd>+<kbd>'</kbd> on Windows and Linux). <kbd>⌘</kbd>+<kbd>⌥</kbd>+<kbd>L</kbd> is *Reformat Code* in JetBrains IDEs, so Parth doesn't use it. Change the shortcut in **Settings → Keymap** |
| **Settings** | **Settings → Tools → Parth**: see [Settings](../setup/settings.md#settings-in-a-jetbrains-ide) |

<!-- screenshot needed: jetbrains-settings.png — Settings → Tools → Parth -->

## Update

Update the plugin from **Settings → Plugins → Installed → Parth → Update**, like any plugin, and restart. A plugin zip installed from disk is updated by installing the new zip the same way.

## Uninstall

**Settings → Plugins → Installed → Parth → ⚙ → Uninstall**, then restart the IDE. Your saved chats stay in `~/.parth/chats` until you delete that folder.

## Next

[Connect a provider](../setup/connect-provider.md) · [Set up Parth](../setup/index.md) · [Troubleshooting](../troubleshooting.md) · [Report a problem](../report-an-issue.md)
