# Voice AI Agent

This repository contains a Power Platform solution that enables a Voice AI Agent in Microsoft Teams using Power Automate and Azure OpenAI. With this solution, end‑users can send voice messages in Teams and receive automated, AI‑driven summaries, action items, and contextual replies.

---

## 📦 Solution Contents

* **Power Automate Flows**
  * (`CollabDays Madrid - Summary agent - Receive a voice message`) – orchestrates message trigger, audio extraction, transcription, AI processing, and reply.
  * (`CollabDays Madrid - Get AI endpoints`) – provide Azure OpenAI endpoint and keys.
* **Connection references** – Microsoft Teams connector
* **Environment Variables** – for Azure AD application credentials and Azure OpenAI settings.

---

## 🛠 Prerequisites

1. **Power Platform** environment with appropriate permissions to import solutions and create flows.
2. **Azure Subscription** with:

   * Azure AD App Registration
   * Azure OpenAI resource
3. **Microsoft Teams** tenant where the "bot" will operate (bot = the user/account to receive the message).

---

## 🔑 Azure AD App Registration & Permissions

1. In the Azure Portal, navigate to **Azure Active Directory > App registrations > New registration**.

2. Give it a name, e.g., `VoiceAIAgentApp`, and register.

3. Under **Certificates & secrets**, create a new **Client secret** and copy its value.

4. Under **API permissions**, add the following **Microsoft Graph** application permissions and click **Grant admin consent**:

   | Permission              | Type        | Purpose                                        | Admin Consent |
   | ----------------------- | ----------- | ---------------------------------------------- | ------------- |
   | Chat.Read.All           | Application | Read all chat messages                         | ✔️ Granted    |
   | Chat.ReadWrite.All      | Application | Read/write all chat messages                   | ✔️ Granted    |
   | ChatMessage.Send        | Delegated   | Send chat messages on behalf of a user         | (optional)    |
   | Directory.Read.All      | Application | Read directory data                            | ✔️ Granted    |
   | Directory.ReadWrite.All | Application | Read/write directory data                      | ✔️ Granted    |
   | Teamwork.Migrate.All    | Application | Create chat/channel messages with any identity | ✔️ Granted    |
   | User.Read               | Delegated   | Sign in and read user profile                  | (optional)    |
   | User.Read.All           | Application | Read all users’ full profiles                  | ✔️ Granted    |
   | User.ReadBasic.All      | Application | Read all users’ basic profiles                 | ✔️ Granted    |
   | User.ReadWrite.All      | Application | Read/write all users’ profiles                 | ✔️ Granted    |

5. Copy the **Application (client) ID** and **Tenant ID** for later.

---

## 🔧 Azure OpenAI Setup

1. In the Azure Portal, create an **Azure OpenAI** resource.
2. Under **Keys and Endpoint**, note down the **Endpoint URL** and one of the **Keys**.
3. Under **Model deployments**, create two deployments:

   * **Whisper** (speech-to-text): deploy model `whisper` with a name like `whisper-stt`.
   * **ChatCompletion**: deploy a chat model such as `gpt-35-turbo` or `gpt-4` with a name like `chat-agent`.

---

## 🚀 Installation Steps

1. **Import Solution**

   * In Power Apps/Power Automate, go to **Solutions > Import** and select the provided `.zip` solution file.
2. **Configure Environment Variables**

   * After import, navigate to **Solutions > \[Your Solution] > Environment variables**.
   * Enter the values for `ClientId`, `ClientSecret`, `TenantId`, `...`.
3. **Publish**

   * Save and publish all customizations.
4. **Test the Flow**

   * In Teams, send a voice message to the bot/account.
   * Observe the Power Automate run history for successful transcription and AI reply.

---

## 🛠️ Troubleshooting

* **401 Unauthorized**: Check that `ClientId/ClientSecret/TenantId` are correct and that the app has the necessary permissions.
* **OpenAI Errors**: Verify your OpenAI Endpoint, OpenAI Key, and deployment names.
* **Flow Failures**: Use the Power Automate run history to inspect each step’s inputs and outputs.

---

## 🙏 Contributors & License

Developed by Renato Romao [(@renatoromao)](https://www.linkedin.com/in/renatoromao/). Feel free to raise issues or contribute!
