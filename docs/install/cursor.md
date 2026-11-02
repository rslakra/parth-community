---
title: Cursor
parent: Install
nav_order: 2
---

# Install Parth in Cursor
{: .no_toc }

Cursor is built on VS Code, so it runs the **same Parth extension**. Cursor gets extensions from the **Open VSX** registry.

1. TOC
{:toc}

## Before you start

- **A Cursor built on VS Code 1.95 or newer.** Open Cursor's **About** dialog (on macOS: **Cursor → About Cursor**). It shows the VS Code version Cursor is built on. An older one refuses the install with *"Unable to install extension … as it is not compatible with VS Code 1.x"*: update Cursor.
- **A folder open.** Parth can only see and change files inside it.
- **An AI provider account**, or a local model server such as Ollama.

## Install

### From Cursor's Extensions view (recommended)

1. Open the **Extensions** view: <kbd>Cmd</kbd>+<kbd>Shift</kbd>+<kbd>X</kbd> (<kbd>Ctrl</kbd>+<kbd>Shift</kbd>+<kbd>X</kbd> on Windows and Linux).
2. Search for **Parth**.
3. Choose **Parth — AI Coding Agent** by **ameyllc**, and click **Install**.
4. Reload the window if Cursor asks (Command Palette → **Developer: Reload Window**).

<!-- screenshot needed: cursor-extensions.png — Cursor's Extensions view showing Parth with the Install button -->

### From a terminal

Use Cursor's own command-line tool instead of `code`:

```bash
cursor --install-extension ameyllc.parth
```

If `cursor` isn't on your PATH, run **Shell Command: Install 'cursor' command in PATH** from the Command Palette, or call it by its full path. On macOS that is:

```bash
/Applications/Cursor.app/Contents/Resources/app/bin/cursor --install-extension ameyllc.parth
```

### From a `.vsix` file

If you were given a `parth.vsix` file:

1. Open the **Extensions** view.
2. Click **⋯** at the top → **Install from VSIX…**. Or open the Command Palette → **Extensions: Install from VSIX…**. You can also drag the file onto the Extensions view.
3. Choose the file, then reload the window if asked.

Or from a terminal: `cursor --install-extension parth.vsix --force`.

## Check that it's installed

- **Parth — AI Coding Agent** is listed under *Installed* in the Extensions view.
- A **Parth** icon appears in the Activity Bar. Cursor shows the Activity Bar as a row of icons at the top of the side bar, and may hide some of them behind **⋯**.

If you can't see it, open the Command Palette and run **Parth: Focus on Chat View**.

## Open the panel and connect a provider

Click the **Parth** icon, or run **Parth: Focus on Chat View**. Then follow [Connect a provider](../setup/connect-provider.md). GitHub Copilot models aren't available in Cursor.

## What's different from VS Code

- **GitHub Copilot models** only appear when the GitHub Copilot extension is installed and signed in, which Cursor doesn't offer. Connect another provider.
- **Keyboard shortcuts.** If Parth's <kbd>Cmd</kbd>+<kbd>Alt</kbd>+<kbd>L</kbd> (*Add Selection to Parth Chat*) clashes with one of Cursor's own, change it in **Keyboard Shortcuts** (search for *Parth*).
- **Logs** are in the same places as in VS Code, but the logs folder carries Cursor's name, for example `~/Library/Application Support/Cursor/logs/` on macOS. The quickest way is still Command Palette → **Parth: Show Logs**.
- **Cursor's own AI and Parth run side by side.** They don't share chats, models or settings.

The commands, the right-click menus and the settings are the same as in VS Code: see [Install in VS Code](vscode.md#the-commands) and [Settings](../setup/settings.md#settings-in-vs-code).

## The Cursor plugin (optional)

Parth also has a small Cursor plugin with a Cursor *rule* for working with Parth. It does **not** contain the chat panel: the extension above is what makes Parth work in Cursor, and you don't need the plugin.

## Update and uninstall

- **Update:** Cursor updates extensions by itself. To update now, open the Extensions view → **Parth** → **Update**. Installing a newer `.vsix` the same way as before replaces the old one.
- **Uninstall:** Extensions view → **Parth** → **Uninstall**.

## Next

[Connect a provider](../setup/connect-provider.md) · [Set up Parth](../setup/index.md) · [Troubleshooting](../troubleshooting.md) · [Report a problem](../report-an-issue.md)
