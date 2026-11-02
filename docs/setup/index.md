---
title: Set up Parth
nav_order: 3
has_children: true
permalink: /setup/
---

# Set up Parth
{: .no_toc }

This section walks through everything you do after installing, in order. It's the same in every supported IDE. Where a page says *VS Code*, it also means Cursor, Windsurf and the other editors built on VS Code. Where the IDEs differ, the page says how.

1. TOC
{:toc}

## The order

| Step | Page | You will |
|---|---|---|
| 1 | This page | Open a project and find your way around the panel |
| 2 | [Connect a provider](connect-provider.md) | Paste an API key or sign in, once per provider |
| 3 | [Models and modes](models-and-modes.md) | Pick a model, and Agent, Plan or Ask |
| 4 | [Attach files](attach-context.md) | Give Parth the files it needs |
| 5 | [Ask for a change](ask-for-a-change.md) | Send a request, watch it work, queue more |
| 6 | [Permissions](permissions.md) | Decide what Parth may do without asking |
| 7 | [Review changes](review-changes.md) | Keep or undo what it did |
| 8 | [Settings](settings.md) | Every setting, in the panel and in the IDE |

## Open a project and the Parth panel

Open a project folder (**File → Open…**). The agent can only see and change files inside it. Then open the panel:

- **VS Code** (and Cursor, Windsurf, …): click the **Parth** icon in the Activity Bar, or run **Parth: Focus on Chat View** from the Command Palette.
- **JetBrains IDEs:** click **Parth** on the right edge.

If no project is open, Parth says **Open a folder or workspace to use Parth.** and waits: open a folder first. Until you do, the Providers list is empty as well. See [the FAQ](../faq.md#open-a-folder).

## The panel, from top to bottom

- **The header:** the chat's title (the first line of your first message, or *New chat*), then three buttons: **🕘** (chat history), **new chat** (a speech bubble with a plus) and **⚙** (Settings).
- **The chat:** your messages and the agent's steps. An empty chat shows **Connect an AI provider** until you connect one, then a short *What should we build?* hint.
- **Above the composer**, when there's something to show: approval cards (**Allow** / **Deny**), the **files changed** card (Keep / Undo), and messages queued while the agent works.
- **The composer**, the rounded box at the bottom. You type your message in it, and attached files sit inside the text as pills. Under the text is the toolbar:

  | Left side | Right side |
  |---|---|
  | **∞ Agent ⌄** mode · **model and effort ⌄** · **Project ⌄** (company gateways that bill per project) · **Permissions ⌄** (Agent mode only) | **context ring** · **📎** attach · **↑** send (**■** stop while the agent works) |

  In a narrow panel, the model and the project move together to a second row, so the model name is never squeezed.

{% include screenshot.html src="composer.png" width="320" alt="An empty chat with two files attached as pills in the composer" %}

## No API key yet?

Turn on **⚙ → Agent → Offline Mock model**. It gives scripted answers, but they go through the real tool pipeline, so you can try attaching, reviewing and Keep / Undo without an account. Or run a [local model](../guides/local-models.md): no key and nothing leaves your computer.

## Next

[Connect a provider](connect-provider.md)
