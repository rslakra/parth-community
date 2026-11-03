---
title: Windsurf, VSCodium and other editors
parent: Install
nav_order: 4
---

# Install Parth in Windsurf, VSCodium and other VS Code-based editors
{: .no_toc }

Editors built on VS Code run VS Code extensions, so they install the **same Parth extension**. This page covers Windsurf, VSCodium, Trae, Positron and other VS Code forks. For Cursor, see [its own page](cursor.md).

1. TOC
{:toc}

## Which editors work

Any editor based on **VS Code 1.95 or newer**. To check, open the editor's **About** dialog: it shows the VS Code version it's built on. An older base refuses the install with *"Unable to install extension … as it is not compatible with VS Code 1.x"*: update the editor.

These editors don't use Microsoft's VS Code Marketplace. They use the **Open VSX** registry, so search for Parth in the editor's own Extensions view.

## Install

### From the editor's Extensions view (recommended)

1. Open the **Extensions** view: <kbd>Cmd</kbd>+<kbd>Shift</kbd>+<kbd>X</kbd> (<kbd>Ctrl</kbd>+<kbd>Shift</kbd>+<kbd>X</kbd> on Windows and Linux).
2. Search for **Parth**.
3. Choose **Parth — AI Coding Agent** by **ameyllc**, and click **Install**.
4. Reload the window if the editor asks (Command Palette → **Developer: Reload Window**).

### From a terminal

Use the editor's own command-line tool instead of `code`:

| Editor | Command | Where it is on macOS, if it isn't on your PATH |
|---|---|---|
| Windsurf | `windsurf` | `/Applications/Windsurf.app/Contents/Resources/app/bin/windsurf` |
| VSCodium | `codium` | `/Applications/VSCodium.app/Contents/Resources/app/bin/codium` |
| Another fork | look in the editor's `bin` folder | `Contents/Resources/app/bin/` inside the app (Windows and Linux: the `bin` folder next to the program) |

```bash
windsurf --install-extension ameyllc.parth
codium --install-extension ameyllc.parth
```

Most of these editors also have a Command Palette entry such as **Shell Command: Install 'windsurf' command in PATH**.

### From a `.vsix` file

If you were given a `parth.vsix` file:

1. Open the **Extensions** view.
2. Click **⋯** at the top → **Install from VSIX…**. Or Command Palette → **Extensions: Install from VSIX…**. You can also drag the file onto the Extensions view.
3. Choose the file, then reload the window if asked.

Or from a terminal: `windsurf --install-extension parth.vsix --force` (use your editor's command).

## Check that it's installed

- **Parth — AI Coding Agent** is listed under *Installed* in the Extensions view.
- A **Parth** icon appears in the Activity Bar. Some editors (Windsurf, for example) show the Activity Bar as a row of icons at the top of the side bar, or hide some behind **⋯**.

If you can't see it, open the Command Palette and run **Parth: Focus on Chat View**.

## What's different from VS Code

- **GitHub Copilot models** only appear when the GitHub Copilot extension is installed and signed in. Most forks don't offer it, so connect another provider.
- **Keyboard shortcuts.** If one of Parth's (for example <kbd>Cmd</kbd>+<kbd>Alt</kbd>+<kbd>L</kbd>, *Add Selection to Parth Chat*) is already used by the editor's own AI features, change it in **Keyboard Shortcuts** (search for *Parth*).
- **Logs** are in the same places as in VS Code, with the editor's name in the logs folder, for example `~/Library/Application Support/Windsurf/logs/`. The quickest way is Command Palette → **Parth: Show Logs**.
- **The editor's own AI assistant and Parth run side by side.** They don't share chats, models or settings.

The commands, the right-click menus and the settings are the same as in VS Code: see [Install in VS Code](vscode.md#the-commands) and [Settings](../setup/settings.md#settings-in-vs-code).

## Update and uninstall

- **Update:** the editor updates extensions by itself, or use Extensions view → **Parth** → **Update**. A newer `.vsix` installed the same way replaces the old one.
- **Uninstall:** Extensions view → **Parth** → **Uninstall**.

## Next

[Connect a provider](../setup/connect-provider.md) · [Set up Parth](../setup/index.md) · [Troubleshooting](../troubleshooting.md) · [Report a problem](../report-an-issue.md)
