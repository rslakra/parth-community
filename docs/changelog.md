---
title: Changelog
nav_order: 7
---

# Changelog
{: .no_toc }

What changed in each version of Parth. The version numbers are the same for the VS Code extension, the JetBrains plugin and the Cursor plugin. To see which one you have, click **⚙ → About** in the Parth panel.

Found something that isn't fixed? [Report it](report-an-issue.md).

## 0.1.34

### Features

- A Parth button in the editor's title bar opens the chat in the sidebar, without hunting for the view.
- New Parth logo and icons in the editor, the activity bar and the marketplace listing.

## 0.1.33

### Features

- Company providers: connect to your organization's AI gateway or proxy (Anthropic or OpenAI API), and pick the project a provider should use.

### Bug fixed

- A dropped connection (ECONNRESET) restarts the session instead of ending the chat.
- Scrolling up while a command runs no longer snaps you back to the bottom of the chat.
- Provider and agent failures are reported with a clear message instead of a silent stop.
- The chat no longer scrolls sideways, has no dead space, and tool steps keep their labels.

## 0.1.32

### Bug fixed

- Replaced deprecated Kotlin and IntelliJ platform APIs, so the plugin runs on current IDE builds.

## 0.1.31

### Features

- Chats no longer stop at 90% of the model's context window; the usage ring turns red as it fills, and the chat keeps going.
- Edit your last message and send it again.
- The newest chat of the workspace reopens when the IDE starts, without a banner.

## 0.1.28

### Features

- Parth can be installed as a Cursor plugin, with its rules, commands and skills.

## 0.1.27

### Features

- Paste code copied from an editor to attach it as a selection.
- Notebook cell selections attach with their cell number.
- Chat history: reopen earlier chats in the workspace and carry on where you stopped.
- A notification offers Reload Window after Parth is installed, updated or reinstalled.

## 0.1.20

### Features

- Code blocks follow the IDE's icons and colours.
- Review in the editor: changed lines are highlighted, with Keep / Undo for each block.

### Bug fixed

- The chat uses the full width of the panel.

## 0.1.16

### Features

- A close (x) button on attachment pills, to drop a file before you send.
- Copy and Add to Parth Chat buttons on code blocks and commands.

### Bug fixed

- Fixed a rendering bug in the IntelliJ chat panel.

## 0.1.11

### Features

- Reasoning effort per model in the model picker.

### Bug fixed

- A failed request now shows the provider's own message and HTTP status instead of a generic error, and logs the full error.
- Errors from the model are reported instead of ending the turn silently, and composer icons no longer overlap.
- The provider settings page lays out correctly.
- The right default model is selected when you connect a provider.

## 0.1.4

### Features

- Attach files, folders and selections from anywhere on disk (sent read-only).
- A permission drop-down chooses how command approvals are handled.
- Queued messages and an editor for the message you're about to send.

### Bug fixed

- Markdown in answers renders correctly: lists, code and links.
- A command approval that can't be shown (no dialog available) now counts as declined instead of failing the turn.
- Approvals, attachments from outside the workspace and the message queue behave reliably.
- Long turns stay inside the model's per-request limit, so fewer runs stop with a context error.
- The chat panel stays usable when it's docked narrow.

## 0.0.7

### Features

- Clearer provider names in settings.

### Bug fixed

- Saving a custom provider applies straight away (the agent restarts), and its ID field is gone.

## 0.0.5

### Features

- Chat panel with drag-and-drop context, Add to Chat commands and selections.
- Agent loop that reads, edits, finds references, renames and checks diagnostics.
- Many AI providers: Anthropic, OpenAI, OpenRouter, Gemini, Vertex AI, Bedrock, Azure OpenAI, Ollama, LM Studio, GitHub Copilot and OpenAI-compatible endpoints.
- Model picker with reasoning effort.
- Per-file diff review with Keep and Undo.
- Command approvals, a workspace path sandbox, and API keys kept in the IDE's secret storage.
- Add Selection to Parth Chat moves the cursor to the message box.
- Queue messages while the agent is working, instead of waiting for the turn to end.
- Import and export your provider settings.

### Bug fixed

- Drag & drop into the chat works in IntelliJ.
- Whole-line selections no longer count the line after them, and the same selection isn't attached twice.
- The chat stays responsive while a long answer streams in.
