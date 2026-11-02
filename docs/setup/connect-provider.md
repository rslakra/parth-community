---
title: Connect a provider
parent: Set up Parth
nav_order: 1
---

# Connect an AI provider
{: .no_toc }

Parth doesn't come with a model. You connect **your own** account with an AI provider, once per provider. Your key is stored in the IDE's secure storage (your OS keychain), never in the chat.

{: .note }
**Open a project folder first.** Parth's agent only starts once a folder is open. If the chat box says **Open a folder or workspace to use Parth.**, the provider list below will be empty too. Open a folder with **File → Open Folder…** and it appears. See [the FAQ](../faq.md#open-a-folder).

1. TOC
{:toc}

## Open the Providers screen

The first time, the chat shows **Connect an AI provider**. Click **Connect a provider**. Or click **⚙ → Providers** at any time.

Providers are listed under *Connected* and *Available Providers*. Click **›** on a row for its details and settings.

{% include screenshot.html src="connect-provider.png" src2="settings-providers.png" width="300" alt="First run: the chat asks you to connect an AI provider" alt2="Settings, Providers tab: Anthropic connected with an API key, other providers with Sign in and API key buttons, AWS Bedrock's details open" %}

## How to connect each provider

| Provider | What to click | What happens |
|---|---|---|
| **Anthropic (Claude)**, **OpenAI**, **Google Gemini API** | **API key**, or **Sign in**, which first opens the provider's page where you create a key | The IDE's **password box** opens (not the chat). Paste the key. It's checked, then stored in the IDE's secure storage |
| **OpenRouter** | **Sign in** (or **API key**) | Your browser opens OpenRouter. Approve, and the row moves to *Connected* |
| **Azure OpenAI / Microsoft Foundry** | **›** → fill in Endpoint and Deployment names → **Save**, then **API key** or **Sign in** | Sign-in shows a code to enter at microsoft.com/devicelogin. It needs your Entra app's client ID, in the same form |
| **AWS Bedrock** | **Sign in** (region and profile are under **›**), or **API key** for a Bedrock API key | Sign-in uses your AWS login. Run `aws sso login` first if you use SSO |
| **Google Vertex AI** | **Sign in** (it asks for the Project ID first), or **API key** (express mode) | Sign-in uses `gcloud auth application-default login` |
| **Ollama** or **LM Studio** (runs on your computer) | **›** → check the Base URL → **Connect** | Start the server first (`ollama serve`). Full setup: [Local models](../guides/local-models.md) |
| **Any OpenAI-compatible server** | **›** → Base URL → **Save**, then **API key** | |
| **GitHub Copilot** (VS Code only) | nothing | Listed automatically, with the models your Copilot plan includes. VS Code asks permission on first use |

A **Sign in** button that's greyed out means that provider's sign-in needs an app ID. Hover it, or open the row with **›**, for the reason. Or use **API key** instead.

## Connect from the Command Palette (VS Code)

In VS Code and the editors built on it, **Parth: Set Provider API Key** opens the same password prompt for a provider's key, and **Parth: Sign Out of a Provider** signs out.

## Disconnect a provider

Use **Remove** (for an API key), **Sign out**, or **Disconnect**, on the provider's row.

## Your organization's AI gateway

If your company runs its own AI gateway or proxy, add it under **⚙ → Providers → Custom Providers → Add custom provider**: it's saved in one file you can share with a whole team. See [Company providers](../guides/company-providers.md).

**Quickest way to set one up:** import a providers file with **⚙ → Providers → Custom Providers → Import settings…**, then click **Connect**. There's a ready-made example you can copy and change, with its steps, in [Try it: import an example gateway with projects](models-and-modes.md#try-it-import-an-example-gateway-with-projects).

### The Custom Providers card

Scroll to the bottom of the **Providers** tab. The **Custom Providers** card lists the company providers you've added, each with a **Connect** button and **›**, and has three buttons under them: **Add custom provider**, **Open providers file** and **Import settings…**.

{% include screenshot.html src="settings-custom-provider-01.png" width="320" alt="Settings, Providers tab: the Custom Providers card with an Amey AI row marked Not connected, a Connect button, and the buttons Add custom provider, Open providers file and Import settings" %}

### The form

**Add custom provider** opens a form with a card for each part: **Provider** (name), **Endpoint** (the API and the base URL), **Credential**, **Headers**, **Fields people fill in**, **Models** and **Projects**. The first two cards:

{% include screenshot.html src="settings-custom-provider-02.png" width="320" alt="The form's Provider card with the Name field set to Amey AI, and the Endpoint card with the API switch on Anthropic Messages and the Base URL field set to https://ai.ameyllc.com" %}

Then the credential, where it says where the key comes from (**Command**, **File**, **Variable**, **API key** or **None**), and how it's sent:

{% include screenshot.html src="settings-custom-provider-03.png" width="320" alt="The form's Credential card with the File tab selected, a file path, a JSON field and the Send it as drop-down, then the Headers card with one header and the Fields people fill in card" %}

Fill in the form, click **Test connection** to check it, **Save**, then **Connect** on its row. Every field, with the value to enter in it, is explained in [Add one in the panel](../guides/company-providers.md#add-one-in-the-panel).

## If it doesn't work

| You see | Fix |
|---|---|
| "… rejected the credentials (401)" | Wrong or expired API key. Use **Providers → Change key** |
| No models in the model menu for a provider | Click ⟳ in the model menu. Check **⚙ → Models** (the switches) and **⚙ → Providers** (the row shows the error) |
| "Can't reach Ollama (local)" or LM Studio | The local server isn't running. See [Local models](../guides/local-models.md) |

More in [Troubleshooting](../troubleshooting.md).

## Next

[Models and modes](models-and-modes.md)
