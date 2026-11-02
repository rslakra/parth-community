---
title: Company providers
parent: Guides
nav_order: 1
---

# Company providers (your organization's AI gateway)
{: .no_toc }

If your organization runs its own AI gateway or proxy, you can connect Parth to it. Typically the gateway keeps usage per team, holds the upstream keys, and has its own sign-in tool. Each gateway is a **company provider**. It works like the built-in providers: people connect it once under **⚙ → Providers**, and its models appear in the model picker.

1. TOC
{:toc}

A company provider needs three things:

- **An endpoint** that speaks the Anthropic Messages API or the OpenAI Chat Completions API.
- **A credential**, from a command, a file, an environment variable, a key each person pastes, or none.
- **Optional extras:** headers for every request, fields each person fills in (a team, for example), and a fixed list of models.

## Add one in the panel

### Step 1: Open the Providers tab

In the Parth panel, click **⚙** in the header and open the **Providers** tab. Built-in providers are listed under *Connected* and *Available Providers*. Click **›** on a row, as on the AWS Bedrock row here, to open a provider's details.

{% include screenshot.html src="settings-providers.png" width="300" alt="Settings, Providers tab: Anthropic connected with an API key, other providers with Sign in and API key buttons, AWS Bedrock's details open" %}

### Step 2: Click Add custom provider

Scroll to the bottom of the **Providers** tab. Company providers are in the **Custom Providers** card. Each one you've added is a row with a **Connect** button and **›** (here, *Amey AI*, not connected yet). Under the rows are three buttons:

| Button | What it does |
|---|---|
| **Add custom provider** | Opens the form in [Step 3](#step-3-fill-in-the-form) |
| **Open providers file** | Opens the providers file in the editor (and creates it if it doesn't exist yet) |
| **Import settings…** | Loads providers from a file instead of filling in the form |

{% include screenshot.html src="settings-custom-provider-01.png" width="320" alt="Settings, Providers tab: the Custom Providers card with an Amey AI row marked Not connected, a Connect button, and the buttons Add custom provider, Open providers file and Import settings" %}

Click **Add custom provider** to start. If you already have a providers file from an admin, click **Import settings…** instead, choose the file, and skip to [Step 4](#step-4-test-save-and-connect). There's a ready-made file to copy and change in [Try it: import an example gateway with projects](../setup/models-and-modes.md#try-it-import-an-example-gateway-with-projects).

### Step 3: Fill in the form

The form is one page with a card for each part, from top to bottom: **Provider**, **Endpoint**, **Credential**, **Headers**, **Fields people fill in**, **Models**, **Projects** and **Backup**. **Delete**, **Test connection** and **Save** are at the very bottom.

The next three screenshots go through it from top to bottom. They show a provider named *Amey AI* that reads its key from a file. The **Example** column in each table has the values used there. Replace them with your gateway's. Every field has a matching key in the providers file (shown in brackets), so the same values work in either place.

#### 3a. Provider and endpoint

A line at the top says which file the provider is saved in (`~/.parth/providers.json`), so one file can set it up for a whole team.

{% include screenshot.html src="settings-custom-provider-02.png" width="320" alt="The form's Provider card with the Name field set to Amey AI and an optional Description, and the Endpoint card with the API switch on Anthropic Messages and the Base URL field set to https://ai.ameyllc.com" %}

| Field (JSON key) | What to enter | Example |
|---|---|---|
| **Name** (`name`) | A label for people. It's shown in **⚙ → Providers**, in the model picker and in error messages | `Amey AI` |
| **Description** (`description`), optional | One line under the name | left empty |
| **API** (`api`) | A switch for the API your gateway speaks: **Anthropic Messages** or **OpenAI Chat Completions** | **Anthropic Messages** |
| **Base URL** (`baseUrl`) | The gateway's address. For Anthropic Messages, give the root: requests go to `/v1/messages` under it, so leave out `/v1`. For OpenAI Chat Completions, it usually ends in `/v1`. It can use `${env:NAME}` | `https://ai.ameyllc.com` |

#### 3b. Credential, headers and fields

The **Credential** card has five tabs: **Command**, **File**, **Variable**, **API key** and **None**. Pick the one that says where the credential comes from. The fields below the tabs change with it.

{% include screenshot.html src="settings-custom-provider-03.png" width="320" alt="The form's Credential card with the File tab selected, the File field set to ~/config.json, the JSON field set to api_key and Send it as set to Authorization Bearer; below it the Headers card with one header X-AMEY-PROJECT set to AMEY-PROJECT-NAME, and the Fields people fill in card with an Add field link" %}

| Field (JSON key) | What to enter | Example |
|---|---|---|
| **Credential** tab (`credential.type`) | **Command:** your company's sign-in tool, which prints a token. **File:** a file another tool keeps the credential in. **Variable:** an environment variable. **API key:** nothing now, each person pastes their own key when they connect. **None:** a gateway that needs no credential | **File** |
| **File** (`credential.path`), on the File tab | The path of the file. `~` is your home folder | `~/config.json` |
| **JSON field** (`credential.field`), optional | If the file is JSON, the one value to use. Without it, the whole file is the credential | `api_key` |
| **Send it as** (`authHeader`) | A drop-down for how the credential is sent: `Authorization: Bearer …` (the default), or a header such as `x-api-key` that gets the credential as it is | `Authorization: Bearer …` |
| **Headers** (`headers`), optional | Click **Add header** for a name and a value, sent with every request (for example, which team the usage belongs to). The **×** removes a row. A value can use `${env:NAME}` or `${setting:key}`, and a header whose value is empty isn't sent | `X-AMEY-PROJECT` = `AMEY-PROJECT-NAME` |
| **Fields people fill in** (`settings`), optional | Click **Add field** for a value each person types when they connect, such as a team. Use it as `${setting:key}` in the base URL or a header | none |

The card also reminds you that the credential stays on this computer and goes only to this endpoint, and that Parth never saves or logs it.

#### 3c. Models and projects

{% include screenshot.html src="settings-custom-provider-04.png" width="320" alt="The form's Models card with empty Model IDs and Default model fields, the Projects card with Parth entered as the only project and empty Default project and Header fields, the Backup card with an Export settings button, and the Delete, Test connection and Save buttons at the bottom" %}

| Field (JSON key) | What to enter | Example |
|---|---|---|
| **Model IDs** (`models`), optional | The models to offer, separated by commas. **Leave it empty to list them from the endpoint** | left empty (or `claude-sonnet-5, claude-opus-5`) |
| **Default model** (`defaultModel`), optional | The model listed first in the model picker | left empty (or `claude-sonnet-5`) |
| **Projects** (`allowedProjects`), optional | Only for a gateway that bills per project: one project per line. The usage of a chat is counted against the project picked next to the model | `Parth` |
| **Default project** (`defaultProject`), optional | Used until someone picks another for their own repository. Empty: no project header is sent until someone picks one | left empty (or `Project 1`) |
| **Header** (`projectHeader`), optional | The header the project is sent in. Empty: `X-Project` | left empty |
| **Backup** → **Export settings…** | Saves your company providers to a `.json` file. API keys and sign-ins aren't included. See [Backup and restore](#backup-and-restore) | |

#### The same provider as a providers file entry

What the three screenshots add up to, written as an entry of `~/.parth/providers.json`:

```json
{
  "providers": {
    "amey-ai": {
      "name": "Amey AI",
      "api": "anthropic",
      "baseUrl": "https://ai.ameyllc.com",
      "credential": { "type": "file", "path": "~/config.json", "field": "api_key" },
      "headers": { "X-AMEY-PROJECT": "AMEY-PROJECT-NAME" },
      "allowedProjects": ["Parth"]
    }
  }
}
```

All the keys are explained in [Fields](#fields) and [Credentials](#credentials).

### Step 4: Test, save and connect

The three buttons are at the bottom of the form (last screenshot above):

1. Click **Test connection** to check the credential and see the models. It gets the credential and lists the models without saving anything, and shows only the last four characters of the credential.
2. Click **Save**.
3. Find the provider's row in the **Custom Providers** card (first screenshot) and click **Connect**. If you added **fields people fill in**, it asks for them now.

To change it later, click **›** on its row: that opens this same form. **Delete** at the bottom removes the provider. If an import changes a provider while its form is open, a banner offers **Load the new version** or **Keep my edits**: see [Backup and restore](#backup-and-restore).

### Step 5: Pick a model

Click the model name in the composer, and choose one of the gateway's models. If the provider lists projects, a **Project** button next to the model picks the project to bill: see [Projects](#projects).

{% include screenshot.html src="model-menu.png" width="300" alt="The model menu: search, Claude models with context sizes, the Effort row, and Manage models and providers" %}

If a model you expect is missing, turn it on in **⚙ → Models**.

An admin can instead write one **providers file** and hand it out, so that everyone gets the same setup without any steps.

## The providers file

| | |
|---|---|
| Default location | `~/.parth/providers.json` |
| Another location | VS Code: the `parth.providersFile` setting. JetBrains: **Settings → Tools → Parth → Providers file**. Either IDE: the `PARTH_PROVIDERS_FILE` environment variable |
| Format | JSON. Comments and trailing commas are allowed, and saving or importing from Settings keeps them: only the entries that change are rewritten |
| When changes apply | Straight away. Parth checks the file every couple of seconds and refreshes **⚙ → Providers** |

Parth reads this file only from your user folder, or from the path you set. It **never reads one from a project**, because an entry can run a command and decides where your prompts and code are sent. A repository you clone can't add a provider.

**⚙ → Providers → Open providers file** opens it in the editor (and creates it if it doesn't exist yet). **Add custom provider** and the edit screen (click **›** on a company provider) write to the same file, and they keep any fields the form doesn't show.

### Backup and restore

**Import settings…** is in the Custom Providers card. **Export settings…** is at the bottom of the add/edit screen (click **›** on a company provider).

{% include screenshot.html src="providers-backup.png" src2="company-provider-edit.png" width="300" alt="Settings, Providers tab: the Custom Providers card with the Import settings button" alt2="Editing a company provider after an import replaced it: a banner offers Load the new version or Keep my edits" %}

- **Export** saves the providers file, exactly as it is (comments included), to a `.json` file you choose (default name `parth-providers-<date>.json`).
- **Import** adds the providers from a file you choose: an export, or a `providers.json` from another computer or from an admin. A provider with the same ID as one you already have replaces it. The others are left alone. Entries that aren't valid are skipped, and the result lists them.
- API keys, sign-in tokens and the values people fill in when they connect are stored by the IDE, not in the file, so they aren't exported. After an import, connect any provider that needs them.
- If an import (or a hand edit of the file) changes a provider while its edit screen is open, a banner says so. **Load the new version** puts the changed provider into the form. **Keep my edits** keeps what you typed, and saving then replaces the changed version. If the provider was removed, the banner says that saving adds it back.

### Example

```jsonc
{
  "providers": {
    // Claude models through the company gateway. The sign-in tool prints a short-lived token.
    "amey-ai": {
      "name": "Amey LLC AI",
      "description": "Company models through the Amey LLC Gateway.",
      "api": "anthropic",
      "baseUrl": "https://ameyllc.com",
      "credential": { "type": "command", "command": "amey-ai token --json", "field": "access_token", "refreshMinutes": 30 },
      "headers": { "X-Team": "${setting:team}", "X-Client": "parth" },
      "settings": [{ "key": "team", "label": "Team", "required": true, "placeholder": "platform" }],
      "defaultModel": "claude-sonnet-5",
      // The gateway bills per project: what the Projects picker offers, and the one used until someone
      // picks another for their own repository. "projectHeader" renames the header; it is X-Project by default.
      "allowedProjects": ["Project 1", "Project 2"],
      "defaultProject": "Project 1",
      "docsUrl": "https://ameyllc.com/"
    },

    // An OpenAI-style endpoint that takes the key another tool already saved, in its own header.
    "amey-open": {
      "name": "Amey LLC Open Model",
      "api": "openai",
      "baseUrl": "https://ameyllc.com/v1",
      "credential": { "type": "file", "path": "~/.amey/credentials.json", "field": "api_key" },
      "authHeader": "X-Amey-Key",
      "models": ["team-coder", { "id": "team-small", "name": "Team small", "contextWindow": 32000, "tools": false }]
    }
  }
}
```

The key under `providers` is the provider's **id**. Use lowercase letters, digits and dashes, and don't reuse a built-in provider's id (`anthropic`, `openai`, `ollama`, …).

### Fields

| Field | Required | What it does |
|---|---|---|
| `name` | yes | Shown in **⚙ → Providers**, in the model picker, and in error messages |
| `description` | | One line under the name |
| `api` | yes | `anthropic` (Messages API) or `openai` (Chat Completions API) |
| `baseUrl` | yes | Anthropic: the root, for example `https://ameyllc.com`, which requests go to `/v1/messages` under. OpenAI: usually ends in `/v1`, and requests go to `/chat/completions` under it. Can use `${env:NAME}` and `${setting:key}` |
| `credential` | yes | Where the credential comes from (see [Credentials](#credentials)) |
| `authHeader` | | How the credential is sent. `bearer` (the default) sends `Authorization: Bearer <credential>`. Any other value is a header name, such as `x-api-key`, that gets the credential as it is. No other auth header is sent then |
| `headers` | | Sent with every request. Values can use `${env:NAME}` and `${setting:key}`, and a header whose value ends up empty isn't sent |
| `settings` | | Fields each person fills in when they connect: `key`, `label`, and optionally `required`, `placeholder`, `defaultValue`. Use them as `${setting:key}` |
| `models` | | The models to offer: ids, or objects with `id`, `name`, `contextWindow`, `maxOutputTokens`, `vision`, `tools` (`false` for a model that can't call tools, so it can't edit files), `efforts` (the effort levels the model accepts, lowest first, for example `["low", "medium", "high"]`, or `[]` for none) and `defaultEffort` (the level it uses when none is sent, one of `efforts`). `efforts` and `defaultEffort` override Parth's built-in table, for gateways that offer different levels. Without `models`, the list comes from the endpoint (`GET /v1/models`) |
| `defaultModel` | | Listed first in the model picker |
| `allowedProjects` | | The projects usage can be billed to, offered in the **Projects** picker next to the model: `["Project 1", "Project 2"]` |
| `defaultProject` | | The one used until someone picks another for their workspace. Without it, no project header is sent until someone picks one |
| `projectHeader` | | The header the project is sent in. Default `X-Project` |
| `docsUrl` | | A **Documentation** link on the provider's edit screen and with its fields |

### Credentials

| `type` | Fields | Where the credential comes from |
|---|---|---|
| `command` | `command`, and optionally `field`, `refreshMinutes` (default 10), `timeoutSeconds` (default 30) | What the command prints, trimmed. If it prints JSON, `field` picks one value, as a dotted path such as `token` or `data.key`. The output is reused for `refreshMinutes` minutes (`0` runs the command for every request). The command runs in your shell, in your home folder |
| `file` | `path`, and optionally `field` | A file another tool keeps its credential in. `~` is your home folder. With `field`, the file is JSON and only that value is used |
| `env` | `variable` | An environment variable the IDE was started with |
| `apiKey` | optionally `keysUrl` | Each person pastes their own key into the IDE's password prompt. It's checked against this endpoint and stored in the IDE's secure storage. **Sign in** opens `keysUrl` first |
| `none` | | Nothing: a gateway on a trusted network, or one that only needs `headers` |

If the endpoint rejects a credential (401 or 403), Parth runs the command again for the next request, so a token that expired early is replaced. During a message it goes further: if the gateway rejects the credential or drops the connection (`terminated — ECONNRESET`), which is what an expired sign-in usually looks like, Parth runs the command again and retries that step once, so the request carries on.

## Projects

Gateways that split the bill per project (a cost center, a client, a budget line) read it from a header such as `X-Project`. When a provider lists projects, Parth shows a **Projects** picker next to the model, and whichever project is in use goes in that header on every request, so the spend is counted against it.

**1. The provider.** `allowedProjects` and `defaultProject` go next to `models` and `defaultModel`, as in the `amey-ai` entry of the example above. You can fill them in without touching the file, in the **Projects** card of the provider's edit screen (**⚙ → Providers → ›**, or **Add custom provider**): one project per line, the default below them, and the header name if it isn't `X-Project`. Leave `defaultProject` out and nothing is sent until someone picks a project. Leave both out and the picker offers **Default** only, which sends no header, as for every built-in provider.

{: .note }
**Already pinning the project in `headers`?** A file written before the picker existed usually has `"headers": { "X-Project": "Project 1" }`. Move that name to `defaultProject` and delete it from `headers`: it's the same request, and now people can choose. While both are there, the project in use wins, so only one project header is ever sent.

**2. A different project for one of your repositories.** The choice belongs to the code you're working on, not to the IDE, so Parth keeps it in that workspace's own folder, and only when it differs from the provider's default. Pick `Project 2` in the picker while that repository is open and it writes `<your-project>/.parth/settings.json`. This is the whole file:

```json
{
  "selectedProjects": {
    "amey-ai": "Project 2"
  }
}
```

- **Where:** the root of the workspace folder you have open. Each repository has its own, and nothing is written outside it.
- **When:** the moment you pick a project that differs from the one already recorded for that provider in this repository. Opening a repository, switching model, provider or mode, or picking the same project again leaves the folder alone, and that repository simply uses the provider's `defaultProject`.
- **One line per provider**, so switching provider keeps each one's project. Picking the first item in the menu again, the one tagged **Default**, removes that line and hands the choice back to `defaultProject`.
- **What's never in it:** keys, tokens or anything secret (those stay in the IDE's secure storage), and chat history (that's in `~/.parth/chats`).
- **Writing it by hand** works too, and committing it gives everyone on the repository the same project. Or add `.parth/` to `.gitignore` to keep it to yourself. Deleting it is safe: the repository goes back to each provider's `defaultProject`. A name the provider no longer lists in `allowedProjects` is ignored the same way.
- Both the VS Code and JetBrains versions read and write it, and they read each other's.

## How people use it

1. In **⚙ → Providers**, company providers are listed first, under **Custom Providers**.
2. **Connect** asks for any fields the provider declares, then gets the credential and lists the models. If something is wrong, the IDE shows why. **Fields** changes them later, and **›** opens the provider's edit screen.
3. Pick one of its models in the model picker, and chat as usual.

## Security

- The credential is fetched on this computer and sent only to that provider's `baseUrl`. Parth doesn't save it, except a key pasted into the IDE's password prompt, which goes to the IDE's secure storage. It never appears in logs, and the chat panel shows at most its last four characters.
- Keys in the environment for the built-in providers, such as `ANTHROPIC_API_KEY`, are never sent to a company provider.
- A `command` runs with your permissions. Use a providers file only from someone you trust, as you would a shell script.
- Settings people fill in (like a team) aren't secret. They're stored with the other provider settings.

## Roll it out to a team

1. Write the providers file and check it with **Test connection**, or connect it yourself.
2. Put it on everyone's machine at `~/.parth/providers.json`, with your dotfiles or device management. To use a location you manage, set `PARTH_PROVIDERS_FILE` or the IDE setting.
3. If a `command` relies on a tool, install that tool first, and use its full path if the IDE might not have your shell's `PATH`. On macOS, apps started from the Dock don't always have it.
4. People open **⚙ → Providers** and click **Connect**.

## Troubleshooting

| What you see | What to do |
|---|---|
| "Some entries in … were skipped" under **Custom Providers** | Each line says which entry and field is wrong. Fix the file, and the list refreshes by itself |
| "The credential command … wasn't found" | Use the command's full path (`which amey-ai` in a terminal shows it) |
| "The credential command … failed (exit N): …" | Run the command in a terminal. You may need to sign in with that tool first |
| "`$NAME` isn't set where the IDE can see it" | Set the variable where the IDE picks it up (your shell profile, then quit and reopen the IDE), or use a `file` or `command` credential |
| "… rejected the credentials (401)" | The gateway refused the credential. Check `authHeader`: some gateways want `x-api-key`, not `Authorization: Bearer` |
| "… terminated — ECONNRESET" | The gateway dropped the connection, usually because the sign-in behind it expired. Parth gets the credential again and retries the step once. If it still fails, sign in again with the tool your `command` credential uses |
| "… doesn't have this model or endpoint (404)" | Check `baseUrl`: for `anthropic`, leave out `/v1`. For `openai`, it usually needs it. If the gateway doesn't list models, name them in `models` |

The logs (**⚙ → About → Show logs**) have the full error. If it still doesn't work, [report it](../report-an-issue.md).
