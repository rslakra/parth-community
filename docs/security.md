---
title: Security
nav_order: 10
---

# Security
{: .no_toc }

1. TOC
{:toc}

## Reporting a vulnerability

Please report vulnerabilities **privately**, not in public issues, pull requests or discussions:

- Use GitHub's **Report a vulnerability** button on this repository's [Security tab](https://github.com/rslakra/parth-docs/security/advisories/new), or
- email **lakra.amey@gmail.com**.

Please include:

- the product and version (the VS Code extension, or the JetBrains plugin; **⚙ → About** in the Parth panel shows the version), and your IDE and operating system;
- what you found and its impact: what an attacker can read, change or run;
- steps to reproduce, or a proof of concept. Remove any API keys or tokens from logs and screenshots. Parth's logs never contain them.

What to expect:

- We aim to **acknowledge a report within 3 business days**.
- We aim to confirm and assess it within 10 business days, and tell you our plan.
- We aim to ship a fix within 90 days, sooner for serious issues. We agree a disclosure date with you, and credit you in the release notes unless you prefer not to be named.
- Please don't disclose publicly before then, and don't access data that isn't yours. Good-faith research within this policy won't be pursued.

## Supported versions

Only the **latest release** of each product gets security fixes. A fix ships as a new patch version.

| Product | Where it's published | Fixed in |
|---|---|---|
| VS Code extension | VS Code Marketplace, Open VSX | The latest version |
| JetBrains plugin | JetBrains Marketplace | The latest version |

## What's in scope

In scope: Parth's own code. For example:

- escaping the workspace sandbox (reading or writing files outside the project, or blocked files such as `.env`, keys and `.git/`);
- running a command without the approval the permission mode requires, or getting past the safety check or the deleting-commands rule;
- reaching the IDE tool server without its token, or from another machine or web page;
- leaking API keys, sign-in tokens or file contents anywhere other than the provider they belong to, including into logs;
- starting project MCP servers (`.parth/mcp.json`) without you turning the setting on;
- a tampered download being accepted (the agent binary's checksum, or the plugin's signature).

Out of scope:

- what an AI model does with the data you send it, and the provider's own terms (see [Privacy](privacy.md));
- anything that needs the attacker to already control your machine, your IDE settings, or your user-level `~/.parth/providers.json` (an entry in that file can run a command by design: only use a file you trust);
- bugs in VS Code, JetBrains IDEs, Node.js or a model provider. Report those to their vendors;
- findings from automated scanners with no demonstrated impact.

## How Parth protects you

- **The tool server is local and locked.** The IDE's tool server binds to `127.0.0.1` on a random port and requires a per-session token. Requests with an `Origin` header or an unexpected `Host` are rejected.
- **A sandbox around the project.** Every file path the agent uses is resolved (symlinks included) and must stay inside the project. `.env*`, keys, certificates and `.git/` are blocked.
- **Commands ask first.** Running a command needs your approval every time, unless it matches your allowed list or, in Auto mode, passes the [safety check](setup/permissions.md#the-safety-check-auto). Deleting always asks.
- **Project MCP servers don't start by themselves.** Servers in `.parth/mcp.json` never start unless you turn that on in your own settings.
- **Keys stay in secure storage.** Credentials live only in the IDE's secret storage, and the chat panel only ever receives masked values.

## What you can rely on in a release

- **The JetBrains plugin is published signed.** The IDE and the Marketplace check the signature.
- **The downloaded agent binary is checked.** The JetBrains plugin accepts it only if its SHA-256 matches the manifest bundled in the signed plugin.
- **Every release goes through a manual approval** before it reaches a store.

## Keeping safe

- Only use a `providers.json` from someone you trust: a `command` credential in it runs on your computer.
- Only turn on **MCP servers from the project** for projects you trust.
- Keep Parth and your IDE up to date.
