---
title: Permissions
parent: Set up Parth
nav_order: 5
---

# Permissions and approving commands
{: .no_toc }

1. TOC
{:toc}

## Choose the permissions

The **Permissions** pill in the composer (Agent mode), **⚙ → Agent → Permissions**, or `/permissions` sets what the agent may do without asking:

| Permissions | Changes to files | Commands |
|---|---|---|
| **Manual** | Each change asks first, with a preview | Every command asks |
| **Auto Edit** (the default) | Apply straight away, still listed for Keep / Undo | Every command asks |
| **Auto** | Apply straight away, still listed for Keep / Undo | Commands that pass the **safety check** run. Anything else asks |

The same setting exists in the IDE's settings: `parth.approvalMode` in VS Code (`manual`, `autoEdit`, `auto`), and **Settings → Tools → Parth** in a JetBrains IDE.

## The approval card

When something needs your OK, a card appears: **"Run this command?"**, with the folder it runs in (if that isn't the project root) and, in Auto, a **Why it asks** line, for example *`git push` can change the repository*. Your choices:

| Button | What it does |
|---|---|
| **Allow once** (just **Allow** when there's nothing to remember) | Runs it this time |
| **Allow `npm test` for this chat** | Runs it, and commands starting the same way run without asking until you start a new chat |
| **Always allow `npm test`** | Runs it, and adds `npm test` to **⚙ → Agent → Commands**, so it never asks again. Remove it there |
| **Deny** | The agent is told you didn't allow it and carries on without it |

What gets remembered is the program and its subcommand, with any options in front of it: `npm test -- --run` → `npm test`, `git commit -m wip` → `git commit`, `make -C packages/core build` → `make -C packages/core build`. Allowing `git commit` doesn't allow `git push`.

Chains (`a && b`), redirection, and deleting commands can only be allowed once.

If the Parth panel is closed, the IDE asks in a dialog with the same choices.

## The safety check (Auto)

In Auto, a command runs without asking when **every part** of it is one of these:

- reading and searching: `ls`, `cat`, `head`, `tail`, `grep`, `rg`, `find` (without `-delete` or `-exec`), `wc`, `diff`, `tree`, …;
- git history: `git status`, `diff`, `log`, `show`, `blame`, `grep`, and listing branches, tags, remotes and stashes;
- `cd` into a folder of the project;
- the project's tests, builds, linters and type checks: `npm test`, `npm run build|lint|typecheck|…`, `pnpm` / `yarn` / `bun` scripts, `npx tsc|vitest|jest|eslint|prettier --check`, `pytest`, `python -m pytest|mypy|…`, `ruff check`, `black --check`, `./gradlew test|check|build|compile…`, `mvn test|verify|…`, `cargo test|build|check|clippy`, `go test|build|vet`, `dotnet build|test`, `swift build|test`, and `make test|check|build|lint|typecheck|all` (also with `-C <folder>` for a folder of the project).

Chains (`&&`, `||`, `;`, `|`) and subshells `( … )` are checked part by part. Text inside quotes is only text, so `grep -n 'a; b' src` is one command.

It **still asks** for:

- installing packages, pushing, and scripts it doesn't recognize;
- paths outside the project (`/…`, `~`, `..`);
- secret files (`.env`, keys);
- environment variables other than a few harmless ones (`CI`, `NODE_ENV`, …), and shell variables (`$HOME`);
- nested commands (`` `…` ``, `$( … )`);
- writing output to a file (`>`; `2>&1` and `>/dev/null` are fine);
- background processes (`&`), `sudo`, and anything it can't follow.

## Allowed commands

To stop being asked for commands you trust, add their start under **⚙ → Agent → Commands**, for example `npm test` or `git commit`. They run without asking in **every** mode.

- The match is on **whole words**: `npm test` allows `npm test -- --watch=false`, not `npm testing`.
- In a chain, **every part** must be allowed (or safe, in Auto). So `git add . && git push` still asks with only `git add` on the list.

In VS Code this is also the `parth.allowedCommands` setting.

## Deleting always asks

`rm`, `rmdir`, `git rm`, `git clean`, `find -delete`, `rimraf` and the like ask in **every** mode, even when they're on the allowed list. They can't be undone from the changes list.

## What the agent can never do

- Read `.env` files, keys, certificates or `.git`.
- Read or change files outside the project. Files you attach from outside are sent read-only.
- Run a command that deletes, without asking.

## Next

[Review changes](review-changes.md)
