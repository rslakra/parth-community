---
title: Report a bug or request a feature
nav_order: 6
---

# Report a bug or request a feature
{: .no_toc }

Bugs, feature requests and documentation problems are all filed as **issues** in this repository. Everyone can read them and add to them, so you can see what's known and what's planned.

1. TOC
{:toc}

## Pick the right place

| I want to… | Go here |
|---|---|
| 🐞 Report something that doesn't work | [New bug report](https://github.com/rslakra/parth-community/issues/new?template=bug_report.yml) |
| 💡 Suggest something new | [New feature request](https://github.com/rslakra/parth-community/issues/new?template=feature_request.yml) |
| 📄 Tell us a page here is wrong or unclear | [New documentation issue](https://github.com/rslakra/parth-community/issues/new?template=docs_issue.yml) |
| ❓ Ask how to do something | [Discussions](https://github.com/rslakra/parth-community/discussions) |
| 🔒 Report a security vulnerability | **Privately**: see [Security](security.md#reporting-a-vulnerability). Never in a public issue |
| 👀 See what's already reported | [Open issues](https://github.com/rslakra/parth-community/issues) |

You need a free GitHub account to file an issue.

{: .tip }
Search the [open issues](https://github.com/rslakra/parth-community/issues?q=is%3Aissue) first. If someone already reported it, add a 👍 or a comment with your details instead of opening a new one. For a feature request, a 👍 on the existing issue is the best way to say you want it too.

## Report a bug

Click **New bug report** above. The form asks for the details below. Here is how to find each one.

### 1. Your IDE and its version

| IDE | How |
|---|---|
| VS Code | **Help → About** (macOS: **Code → About Visual Studio Code**) |
| Cursor, Windsurf, VSCodium, other forks | The editor's **About** dialog (macOS: its name menu → **About**). It shows both the editor's version and the VS Code version it's built on |
| IntelliJ IDEA, PyCharm, WebStorm, GoLand, Rider, CLion | **Help → About** |

### 2. Parth's version

In the Parth panel, click **⚙ → About**. Or:

- **VS Code and forks:** Extensions view → **Parth**.
- **JetBrains IDEs:** **Settings → Plugins → Installed → Parth**.

### 3. The Parth log

The log is the most useful thing you can attach. It records provider errors, the agent starting and stopping, and every tool call. **It never contains your API keys.**

| IDE | How to get it |
|---|---|
| **VS Code and forks** | Command Palette (<kbd>Cmd</kbd>+<kbd>Shift</kbd>+<kbd>P</kbd>) → **Parth: Show Logs**. Or type `/logs` in the chat box. The Output panel opens on the *Parth* channel: select the relevant lines and copy them |
| **JetBrains IDEs** | **⚙ → About → Show logs** in the Parth panel. It opens `idea.log` in an editor tab. Search for `rslakra.parth` and copy the lines around the time it happened |

Paste the lines from around the time of the problem into the **Parth log** box. Not the whole file: a few dozen lines around the error are enough. More ways to open the log are on the [troubleshooting page](troubleshooting.md#logs).

### 4. What happened

Describe, in this order:

1. **What you did.** The steps, and your mode (Agent, Plan, Ask) and permissions (Manual, Auto Edit, Auto).
2. **What you expected.**
3. **What happened instead.** Any error message, word for word. A screenshot helps: drag it into the form. Cover anything private first.
4. **Your provider and model**, for example *Anthropic, Claude Opus 5 High*, or *a company provider*.

A bug that always happens, with clear steps, gets fixed fastest.

{: .warning }
**Don't paste API keys, tokens or private code.** Parth's logs don't contain keys, but check your screenshots and anything you copy.

## Request a feature

Click **New feature request** above. The form asks:

- **Which IDE** it's for: all of them, VS Code and forks, JetBrains IDEs, or Cursor only.
- **Which part of Parth**: chat, providers and models, attaching files, modes, permissions, reviewing changes, settings, installing, or documentation.
- **What you're trying to do.** Describe the problem first. This helps more than a detailed design, because there may be a better fix than the one you have in mind.
- **What you'd like Parth to do**, and what you do instead today.
- **How much it matters to you.**

## What happens next

1. Your issue gets a label: `bug`, `enhancement` or `documentation`.
2. If something's missing (a version or a log), you may be asked for it in a comment.
3. Bugs we confirm and features we accept are tracked, and the issue is updated as work happens. Fixes are listed in the [changelog](changelog.md) for the version that ships them.
4. When it's released, the issue is closed with a note saying which version.

## Not sure which one it is?

- If something **used to work and doesn't**, or an error appears: it's a **bug**.
- If it works as described but you want it different: it's a **feature request**.
- If you're not sure how to do something: ask in [Discussions](https://github.com/rslakra/parth-community/discussions).
