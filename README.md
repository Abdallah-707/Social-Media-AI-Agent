[![Support Palestine](https://raw.githubusercontent.com/Ademking/Support-Palestine/main/Support-Palestine.svg)](https://www.map.org.uk)

# 🤖 AI Posts Content Machine (n8n Automation)
![AI Posts Content Machine](https://www.orangewebsite.com/articles/wp-content/uploads/2017/10/Social-Media-History.jpg)

This is a fully automated content generation and posting system using [n8n](https://n8n.io/). It uses **AI agents**, **Google Sheets**, **OpenAI**, **Anthropic Claude**, **Perplexity AI**, **Google Drive**, and **LinkedIn API** to generate, style, store, and post high-quality LinkedIn content every day — without manual effort.

---

## 🧠 What It Does

- ✅ Collects previous content ideas from Google Sheets
- ✅ Uses an AI agent to generate a **new post** (idea, title, body, image description)
- ✅ Selects the **least-used content category** to diversify posts
- ✅ Sends image prompt to **OpenAI Image Edit API**
- ✅ Applies consistent style from a **reference image** stored in Google Drive
- ✅ Saves the new image back to Drive
- ✅ Logs the post (idea, text, image) into Google Sheets for review
- ✅ Posts to LinkedIn automatically when marked as `"ready"`
- ✅ Optional: Post to Instagram or Twitter (disabled by default)

---

## 🗂️ Workflow Components

- **AI Agent**: Claude 3.7 Sonnet (via Anthropic) generates post idea, title, text, and image description
- **Web Research Tool**: Perplexity AI enhances the relevance of ideas
- **Image Generator**: OpenAI’s image API replicates a minimal branded style
- **Google Sheets**: Central hub for post logging, status tracking, and control
- **Google Drive**: Hosts the style reference and final generated images
- **LinkedIn API**: Publishes final post directly
- **n8n Scheduler**: Triggers post generation and publishing daily

---

## 🔄 Daily Workflow

1. At 5:00 AM:
   - Collects all previously used ideas
   - Joins them to avoid repetition
   - Prompts Claude to generate a **new post idea** with all required materials
   - Requests **a styled image** from OpenAI using a template from Google Drive
   - Uploads the final image back to Google Drive
   - Logs the new post in a Google Sheet (`status = review`)

2. At 4:00 PM:
   - Checks for posts with `status = ready`
   - Selects one
   - Downloads the image
   - Publishes it to LinkedIn
   - Updates its status to `posted`

---

## 📒 Google Sheet Setup

Create a spreadsheet with the following columns:

| name | idea | text | image | status |
|------|------|------|-------|--------|
| Post title | Post category + summary | Full post | Google Drive share link | review / ready / posted |

> [📄 Template Sheet](https://docs.google.com/spreadsheets/d/1-F3ZioIs3oWOKMyDPMuquaH-qiuaZs6qdZXP-yNeRbs)

---

## 🔌 Required Integrations

Set up these credentials in n8n:

- ✅ **Google Sheets OAuth**
- ✅ **Google Drive OAuth**
- ✅ **OpenAI API (Image API)**
- ✅ **Anthropic API Key**
- ✅ **Perplexity API Key**
- ✅ **LinkedIn OAuth** (for posting)

Optional:

- 🐦 Twitter API (X node, disabled)
- 📸 Instagram via Facebook Graph API (disabled)

---
## 🛠 Setup Guide

## ✅ Step 1: Set Up Google Sheets Credential
1. In the n8n Google Sheets node create a new credential using your Google account

---

## ✅ Step 2: Set Up Google Drive Credential
1. Go to the [Google Cloud Console](https://console.cloud.google.com) and create or select a project
2. Enable the Google Drive API under APIs & Services > Library
3. Still in APIs & Services, select Credentials from the left menu
4. Click + CREATE CREDENTIALS > OAuth client ID
5. For Application type, choose Web application
6. Under Authorized redirect URIs, paste the OAuth Redirect URL: https://oauth.n8n.cloud/oauth2/callback
7. Click Create, then copy the Client ID and Client Secret shown in the modal
8. In the n8n Google Drive node click Create Credential
9. Paste in the Client ID and Client Secret from Google Cloud
10. Click Sign in with Google, complete the OAuth consent flow, then Save your credential

---

## ✅ Step 3: Set Up Anthropic Credential
1. Navigate to the [Anthropic Console](https://console.anthropic.com/) and sign in or sign up
2. Generate an API key
3. In the n8n "Anthropic Chat Model" node click Create Credential, past the API key and save

---

## ✅ Step 4: Configure OpenAI via HTTP Request Node
1. Visit the [OpenAI API Keys](https://platform.openai.com/account/api-keys) page and create a new secret key
2. In the n8n OpenAI Image node in the Authentication select Generic Credential Type
3. In Generic Auth Type select Header Auth
4. Create a new Header Auth, Name = Authorization, Value = Bearer YOUR_TOKEN

---

## ✅ Step 5: Configure Perplexity AI via HTTP Request Node
1. Go to the [Perplexity API Portal](https://www.perplexity.ai/account/api/keys) and click Create Key
2. Copy the generated API key
3. Inside n8n, in the sub-workflow, open the Perplexity Research node
4. In the Authentication select Generic Credential Type
5. In Generic Auth Type select Header Auth
6. Create a new Header Auth, Name = Authorization, Value = Bearer YOUR_TOKEN

---

## ✅ Step 6: Set Up LinkedIn Credential
1. In the n8n LinkedIn node create a new credential using your LinkedIn account

---

## ✅ Step 7: Customize The System For Your Use Case
1. In the Idea Generator node adjust the prompts to reflect your content style and your topics
2. Create a folder in your Google Drive where you will store all the images
3. Put in that folder the image with the style of your brand, that you want to replicate every time
4. Paste the shared link to this image in the "Image Style" node
5. In the OpenAI Image node adjust the prompt to reflect your image style
6. Copy my [Google Sheet](https://docs.google.com/spreadsheets/d/1-F3ZioIs3oWOKMyDPMuquaH-qiuaZs6qdZXP-yNeRbs/edit?usp=sharing)
7. Select your Google Sheet in the Google Sheets nodes
8. Activate the system, now every day a new post will be created inside the Google Sheet, and once you've reviewed it (might edit it as well), set the status to "ready" and it will be posted; the posting mechanism is set to work every day, one post at a time

---

Now you're ready to run your workflow. Happy automating!

---

## 💡 Customization Tips

- Modify prompt inside `Idea Generator` node to change tone/format
- Change post frequency by updating `Schedule` trigger
- Tweak OpenAI image prompt for different aesthetic results
- Enable Instagram/Twitter by activating the corresponding nodes

---

## 📸 Example Output

Each LinkedIn post consists of:

- **Hooking title**
- **Practical and well-structured content**
- **Stylish, minimalistic image**
- **Automatically posted at peak hours**

---

## 📄 License

MIT License — free to use, remix, and modify.

---

Happy automating your content! 🚀
