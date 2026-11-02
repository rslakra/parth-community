---
title: Models and modes
parent: Set up Parth
nav_order: 2
---

# Pick a model and a mode
{: .no_toc }

1. TOC
{:toc}

## Pick a model

Click the model name in the composer. When you connect a provider, its first model is picked for you. The menu has:

- a **search** box and **⟳** to refresh the lists;
- the models of every provider you connected, grouped by provider, with their context size;
- **Effort** (Auto, Low, Med, High, XHigh, Max), shown only for models that support reasoning effort. The chosen level appears after the model name;
- **Manage models and providers…**, which opens Settings.

To keep the list short, open **⚙ → Models** and switch off the models you don't want in the menu.

{% include screenshot.html src="model-menu.png" src2="settings-models-dark.png" width="300" alt="The model menu: search, Claude models with context sizes, the Effort row, and Manage models and providers" alt2="Settings, Models tab in a dark theme: a switch for each model" %}

**The context ring.** Next to the send button, a ring and its percentage show how much of the model's context window the chat uses, updated after every step. Click it for the numbers. It turns red as it fills. When it's high, start a **new chat** for a new task.

### Projects (company gateways)

If a company gateway bills its usage per project, a **Project** button sits next to the model with the same kind of menu. The project in use is sent with every request of the chat (as `X-Project` by default), so the spend is counted against it. The first choice is the gateway's own default. Pick another, and that choice is remembered for this repository alone, in its `.parth/settings.json`. A provider that lists no projects shows **Default** and sends nothing. See [Company providers](../guides/company-providers.md#projects).

**Where the projects come from.** They're set on the company provider. In its form (**⚙ → Providers → ›** on the provider's row), the **Projects** card has three fields:

| Field | What to enter |
|---|---|
| **Projects** | One project per line. The usage of a chat is counted against the project picked next to the model |
| **Default project** (optional) | Used until someone picks another for their own repository. Empty: no project header is sent until someone picks one |
| **Header** (optional) | The header the project is sent in. Empty: `X-Project` |

{% include screenshot.html src="settings-custom-provider-04.png" width="320" alt="The form's Models card, the Projects card with Parth entered as the only project and empty Default project and Header fields, the Backup card with an Export settings button, and the Delete, Test connection and Save buttons at the bottom" %}

The other cards of the form, with a screenshot and the value for every field, are in [Add one in the panel](../guides/company-providers.md#add-one-in-the-panel).

#### Try it: import an example gateway with projects

The easiest way to see the **Project** button is to import a company provider that lists projects. This example has two (`Parth` and `2 - Second`), and `Parth` is the default. Copy it into a file, or [download it]({{ '/assets/examples/amey-ai-gateway.json' | relative_url }}):

```json
{
    "providers": {
        "amey-ai-gateway": {
            "name": "Amey AI Gateway",
            "description": "Amey AI Gateway",
            "api": "anthropic",
            "baseUrl": "https://ameyllc.com",
            "credential": {
                "type": "file",
                "path": "Path to your custom '~/config.json' file which contains the actual key",
                "field": "api_key"
            },
            "headers": {
                "CUSTOM_HEADER_KEY": "CUSTOM_HEADER_VALUE"
            },
            "allowedProjects": [
                "Parth",
                "2 - Second"
            ],
            "defaultProject": "Parth"
        }
    }
}
```

**Change these to match your gateway before you import it:**

| Field | What to put |
|---|---|
| `baseUrl` | Your gateway's address. For `"api": "anthropic"`, leave out `/v1` |
| `credential` | This one reads the value of `api_key` from a JSON file. **Replace the text in `path` with the real path of that file**, for example `~/config.json`, and make sure the file exists and holds your key: `{ "api_key": "your-key" }`. Or point `path` at the file your company's sign-in tool writes, or use another [credential type](../guides/company-providers.md#credentials) |
| `headers` | The headers your gateway wants on every request. Replace `CUSTOM_HEADER_KEY` and `CUSTOM_HEADER_VALUE` with the real name and value, or delete the whole `headers` block if there are none |
| `allowedProjects` and `defaultProject` | The projects your usage can be billed to, and the one used until someone picks another. `defaultProject` must be one of them |

**Import it:**

1. Save the JSON above as a file, for example `amey-ai-gateway.json`.
2. In the Parth panel, click **⚙ → Providers**.
3. In the **Custom Providers** card, click **Import settings…**, and choose the file. The result lists what was imported, and any entry that was skipped and why.
4. Click **Connect** on **Amey AI Gateway**. Company providers are listed first.
5. Open the model menu and pick one of its models. A **Project** button now sits next to the model, showing `Parth`. Pick `2 - Second` to bill that repository's usage to the other project: your choice is saved in that repository's `.parth/settings.json`.

{% include screenshot.html src="settings-custom-provider-01.png" width="320" alt="Settings, Providers tab: the Custom Providers card with an Amey AI row marked Not connected, a Connect button, and the buttons Add custom provider, Open providers file and Import settings" %}

This is the card from step 3: **Import settings…** is the bottom button, and a provider you've imported appears as a row above the buttons, with its **Connect** button (step 4).

Importing adds the provider without touching your other providers. If you already have a provider with the same ID (`amey-ai-gateway`), the import replaces it.

**Without the button:** put the file at `~/.parth/providers.json`. If you already have that file, add the `amey-ai-gateway` entry inside its existing `providers` object instead of replacing the file. Parth checks the file every couple of seconds, so it appears under **⚙ → Providers** by itself.

**Prefer to fill in a form instead?** Click **Add custom provider** in the same card. [Add one in the panel](../guides/company-providers.md#add-one-in-the-panel) shows every card of the form with a screenshot and the value for each field.

More about the file, every field, and the other ways to get a credential: [Company providers](../guides/company-providers.md).

## Choose a mode

Click the mode pill (**∞ Agent ⌄**), or type `/agent`, `/plan` or `/ask` in the chat.

| Mode | What the agent can do |
|---|---|
| **∞ Agent** | Read, edit and create files, update the files that depend on a change, check diagnostics, run commands. What it may do without asking depends on the [permissions](permissions.md) |
| **☰ Plan** | **Read-only.** It investigates and answers with a numbered plan. A **Build this plan** button under the answer switches to Agent and carries it out |
| **? Ask** | **Read-only.** It answers questions about your code |

Plan and Ask get only the read-only tools, so they can't change files even if asked to. In Agent mode, a **Permissions** pill (Manual, Auto Edit or Auto) sits in the composer toolbar.

{% include screenshot.html src="mode-menu.png" width="300" alt="The mode menu: Agent, Plan and Ask" %}

## Commands you can type

Type **`/`** at the start of a message for the list.

{% include screenshot.html src="slash-commands.png" width="300" alt="Typing / shows the list of commands" %}

| Command | Does |
|---|---|
| `/agent`, `/plan`, `/ask` | Switch mode |
| `/new` | New chat (stops the current one; it stays in the history) |
| `/attach` | Attach files |
| `/clear` | Remove attached context |
| `/keep`, `/undo` | Keep or undo all changes |
| `/models`, `/providers` | Open Settings |
| `/permissions` | Open the permissions and allowed commands (⚙ → Agent) |
| `/logs` | Open the log |

## Next

[Attach files](attach-context.md)
