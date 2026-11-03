---
title: Troubleshooting
nav_order: 5
---

# Troubleshooting
{: .no_toc }

1. TOC
{:toc}

If your problem isn't here, [report it](report-an-issue.md). The log is the first thing to look at.

New to Parth, or not sure what a message means? The [FAQ](faq.md) explains the messages in the chat box, such as **Open a folder or workspace to use Parth.**

## Logs

### VS Code, Cursor, Windsurf, VSCodium and other VS Code-based editors

| What | How to open it |
|---|---|
| **Parth log**: provider errors, agent start and stop, every tool call | **⚙ → About → Show logs**, or `/logs` in the chat box, or Command Palette (<kbd>Cmd</kbd>+<kbd>Shift</kbd>+<kbd>P</kbd>) → **Parth: Show Logs**. It opens the Output panel on the *Parth* channel |
| The same log as a file | Command Palette → **Developer: Open Logs Folder** → `<session>/window1/exthost/ameyllc.parth/Parth.log`. On macOS, under `~/Library/Application Support/Code/logs/` (the folder carries the editor's name, for example `Cursor`) |
| Extension crashes | Output panel → choose **Extension Host** in the drop-down |
| Chat panel (UI) errors | Command Palette → **Developer: Open Webview Developer Tools** → Console |

A normal log looks like this:

```
2026-09-26 08:32:44.762 [info] [mcp] IDE MCP server on http://127.0.0.1:50715/mcp
2026-09-26 08:32:44.948 [info] [core] ready, version 0.1.0
2026-09-26 08:32:45.003 [info] [mcp] read_file
2026-09-26 08:32:45.106 [info] [mcp] edit_file → error: old_string matches 2 places. …
```

### IntelliJ IDEA and other JetBrains IDEs

| What | How to open it |
|---|---|
| **IDE log** (Parth writes to it) | **⚙ → About → Show logs** (or `/logs`) opens `idea.log` in an editor tab. Or **Help → Show Log in Finder** (Windows: *Show Log in Explorer*). Search for `rslakra.parth`. Agent output lines start with `core:` |
| Log file location | macOS `~/Library/Logs/JetBrains/<IDE><version>/idea.log` (for example `IntelliJIdea2025.3`, `PyCharm2025.3`) · Windows `%LOCALAPPDATA%\JetBrains\<IDE><version>\log\idea.log` · Linux `~/.cache/JetBrains/<IDE><version>/log/idea.log` |
| More detail | **Help → Diagnostic Tools → Debug Log Settings…** → add a line `#rslakra.parth` → OK |
| Plugin failed to load | **Settings → Plugins**: Parth shows an error. Details are in `idea.log` |

A normal start looks like this in `idea.log`:

```
INFO - #rslakra.parth.intellij.ParthService - Parth IDE MCP server on http://127.0.0.1:63208/mcp
INFO - #rslakra.parth.intellij.core.CoreProcess - Starting the agent core: …
INFO - #rslakra.parth.intellij.ParthService - Parth agent core ready (core 0.1.0, 10 providers)
```

The logs never contain API keys.

## Known issues

### VS Code 1.140.0: drag and drop stops working {#vs-code-1140-drag-and-drop-stops-working}

**Symptom (VS Code only):** dragging files from the Explorer onto the Parth chat does nothing, even with <kbd>Shift</kbd> held, and the "Drop to add to chat" outline never shows.

**Cause:** VS Code **1.140.0** (auto-updated on 2026-09-30) broke dropping files into the chat. Going back to **1.139.0** restores it. Editors built on VS Code (Cursor, Windsurf, VSCodium, …) may be affected once they're based on 1.140.0: check their About dialog. JetBrains IDEs are not affected.

**Workaround (no downgrade needed):** attach files another way: type **`@`**, click **📎**, or right-click a file or editor tab → **Add to Parth Chat** (see [Attach files](setup/attach-context.md)).

**Fix: go back to VS Code 1.139.0.** This version is verified to work (build `2242ebbb54efeeb0129e08e919e7e8d43033cd83`).

1. **Quit VS Code** completely (<kbd>Cmd</kbd>+<kbd>Q</kbd> on macOS).
2. **Download 1.139.0** for your system:

   | System | Download |
   |---|---|
   | macOS (Apple Silicon and Intel) | <https://update.code.visualstudio.com/1.139.0/darwin-universal/stable> |
   | Windows 64-bit (user installer) | <https://update.code.visualstudio.com/1.139.0/win32-x64-user/stable> |
   | Linux 64-bit (`.tar.gz`) | <https://update.code.visualstudio.com/1.139.0/linux-x64/stable> |

   To get exactly the verified build, use its commit instead of the version, for example for macOS: `https://update.code.visualstudio.com/commit:2242ebbb54efeeb0129e08e919e7e8d43033cd83/darwin-universal/stable`.
3. **Install it over the current one.** On macOS, unzip it and move **Visual Studio Code.app** to **Applications**, choosing **Replace**. On Windows, run the installer. Your settings, extensions and Parth chats are kept.
4. **Stop it updating again.** Before you reopen VS Code, open **Settings**, search for `update.mode`, and set it to **none**. Or in `settings.json`: `"update.mode": "none"`. Without this, VS Code downloads 1.140.0 again.
5. **Check the version.** Open VS Code → **Help → About** (macOS: **Code → About Visual Studio Code**). It should show **Version: 1.139.0** and **Commit: 2242ebbb54efeeb0129e08e919e7e8d43033cd83**.
6. Hold <kbd>Shift</kbd>, drag a file from the Explorer onto the Parth chat, and check that the "Drop to add to chat" outline appears.

When a later VS Code release fixes drag and drop, set `update.mode` back to its default (`default`) and update. If drag and drop still fails on 1.139.0, [report it](report-an-issue.md) with the Parth log and your VS Code version.

## Common problems

| You see | Cause | Fix |
|---|---|---|
| Drag and drop onto the chat does nothing in VS Code, and no "Drop to add to chat" outline shows | VS Code updated to 1.140.0, which broke drops into the chat panel | Attach with `@`, 📎 or right-click → **Add to Parth Chat**, or go back to 1.139.0: see [above](#vs-code-1140-drag-and-drop-stops-working) |
| "Starting the agent…" never goes away | The agent process didn't start | Open the log (above). Then **⚙ → About → Restart agent** (or **Parth: Restart Agent Core** in VS Code's Command Palette, or **Tools → Parth → Restart Agent Core** in a JetBrains IDE) |
| "Node.js 20 or newer is needed…" (JetBrains, plugin installed from a file) | Node.js isn't installed, or the IDE can't find it | Install Node.js 20+, or set its path in **Settings → Tools → Parth → Node.js path** (for example `/opt/homebrew/bin/node`, from `which node`) |
| "Open a folder or workspace to use Parth." (and no providers listed under **Available Providers**) | No project is open, so Parth's agent hasn't started | **File → Open Folder…**, then connect a provider. See [the FAQ](faq.md#open-a-folder) |
| "Unable to install extension … not compatible with VS Code 1.x" (Cursor, Windsurf, …) | The editor is built on a VS Code older than 1.95 | Update the editor. See [Install in Cursor](install/cursor.md) |
| No Parth icon in Cursor or Windsurf | The Activity Bar is at the top of the side bar, or the icon is hidden behind **⋯** | Command Palette → **Parth: Focus on Chat View** |
| The chat doesn't open in Android Studio | Its bundled Java runtime has no embedded browser (JCEF) | Use VS Code or another JetBrains IDE. See [Install in a JetBrains IDE](install/jetbrains.md) |
| "… rejected the credentials (401)" | Wrong or expired API key | **Providers → Change key** |
| "… terminated — ECONNRESET", usually on a company gateway | The sign-in behind the gateway expired, so it dropped the connection | Parth gets the credential again and retries the step once on its own. If it still fails, sign in again with your company's tool (or **Providers → Sign out**, then connect again) |
| "… rate limit reached" | Too many requests for your plan | Wait, or pick another model |
| "Can't reach Ollama (local): …" (or LM Studio) | The local server isn't running | Start it (`ollama serve`, or turn the server on in LM Studio's **Developer** tab), then click ⟳ in the model menu. See [Local models](guides/local-models.md) |
| No models in the model menu for a provider | The list couldn't load, or the models are hidden | Click ⟳ in the model menu. Check **⚙ → Models** (switches) and **⚙ → Providers** (the row shows the error) |
| Sign-in button is greyed out | That provider's sign-in needs an app ID | Hover the button, or open the row with **›**, for the reason. Or use **API key** |
| The context ring is red, or the provider says the request is too long | The conversation is close to, or over, the model's context window | Click **New chat** for a new task |
| An earlier chat isn't in the history | Chats are saved per project and per computer, and only the newest 100 are kept. A chat with no message sent isn't saved | Open the project the chat was held in. Check that `~/.parth/chats` (or `PARTH_CHATS_DIR`) can be written to |
| "That chat isn't saved any more." | The chat's file was deleted, or it belongs to another project | Pick another from the list |
| A command asks for approval in **Auto** | It didn't pass the safety check. The card's **Why it asks** line says which part | Click **Allow once**, or **for this chat** / **Always allow** on the card. You can also add its start under **⚙ → Agent → Commands**. Deleting commands always ask |
| The agent says it can't read a file | The file is outside the project, or it's a secret (`.env`, keys, `.git`) | Expected: those are blocked on purpose. To give it a file from outside the project, attach it (📎, drag and drop, or right-click → **Add to Parth Chat**) |
| The chat panel is blank | The panel didn't load | Restart the IDE. If it stays blank, reinstall Parth, and [report it](report-an-issue.md) with the log |

## Still stuck?

[Report a bug](report-an-issue.md) with your IDE and Parth versions and the log from around the time it happened.
