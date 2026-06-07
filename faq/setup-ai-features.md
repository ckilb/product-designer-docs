---
nav_order: 250
parent: FAQ
---

# How do I set up AI features?

The product designer includes two AI-powered features your customers can use:

- **AI Design Generation** — the customer describes a design in plain words (e.g. *"a birthday card with a balloon in the top-right corner and 'Happy Birthday' at the bottom"*) and the AI creates a complete design with text, images and QR code elements positioned on the canvas.
- **AI Image Generation** — the customer types a prompt and the AI generates an image directly onto the canvas.

Both features are powered by **OpenRouter**. Setting them up requires three steps:

1. [Get and configure an OpenRouter API key](#1-openrouter-api-key)
2. [Set a privacy disclaimer](#2-privacy-disclaimer)
3. [Enable the features and pick models](#3-enable-the-features)

---

## 1. OpenRouter API key

### What is OpenRouter?

[OpenRouter](https://openrouter.ai) is an API gateway that gives you access to dozens of AI models — Google Gemini, OpenAI GPT, Anthropic Claude and many more — through a **single API key**. Instead of creating accounts with every AI provider and managing separate billing, you only pay OpenRouter and they route your requests to the model you choose. You pay per request based on the model's pricing.

> ⚠️ **Costs apply.** Every AI request sent through OpenRouter costs a small amount depending on the model. The rate limiter (see below) helps keep these costs under control.

### How to get an API key

1. Create an account at [openrouter.ai](https://openrouter.ai)
2. Go to the [API Keys page](https://openrouter.ai/settings/keys) and create a new key
3. Copy the key — it starts with `sk-or-v1-`

### Where to enter the key

In your **Shopware Administration**, navigate to:

**Extensions → My Extensions → Kilb Product Designer → Configure**

Find the **OpenRouter** card and paste your key into the input field.

> Without an API key, **all AI features are disabled for every configuration** in your shop. The AI tab won't even show up in the product designer configuration until a valid key is set.

---

## 2. Rate limiting

Right below the API key in the same **OpenRouter** card you'll find the rate limiting setting (default: **10**).

### Why rate limiting matters

Every AI request costs money. Without a rate limit, a single visitor — or a malicious script — could fire hundreds of requests in a short time, running up your OpenRouter bill. The rate limiter protects you against this.

### How it works

The rate limiter uses a **leaky bucket** that tracks requests per visitor (by IP address) and per action (design generation and image generation are counted separately). Requests above the limit are **not rejected** — they are simply **delayed** (slowed down) so the average rate stays within the configured limit.

For example, with the default of 10 requests per minute, a visitor can trigger one AI request roughly every 6 seconds without waiting. If they trigger requests faster, subsequent requests will be queued and slowed down automatically.

> Set this value as low as your use case allows. A lower number means better cost protection.

---

## 3. Privacy disclaimer

Before AI features can be enabled for a configuration, you must provide a **privacy disclaimer**. This is a short text shown to your customers before they can use any AI feature, informing them that their prompt will be sent to an external AI provider.

Open any product designer configuration in your shop backend, switch to the **AI** tab, and fill in the field.

> If the privacy disclaimer is empty, the **enable toggles for both AI features are locked** and cannot be turned on. This is intentional — your customers should always know where their data goes.

---

## 4. Enable the features

Still in the **AI** tab of your product designer configuration:

| Setting | Description |
| --- | --- |
| **AI design generation enabled** | Turn on to let customers generate complete designs from a text description |
| **AI image generation enabled** | Turn on to let customers generate individual images from a text prompt |

Both toggles become available as soon as you have filled in the privacy disclaimer.

### Choosing a model

When a feature is enabled, a model dropdown appears:

**Design generation models** (text-to-design):

| Model | Description |
| --- | --- |
| Auto (OpenRouter) | Let OpenRouter pick the best available model |
| Google Gemini 2.5 Flash | Fast and affordable |
| Google Gemini 2.5 Pro | Higher quality, slightly slower |
| OpenAI GPT-4.1 | Good general-purpose model |
| OpenAI GPT-4o | Fast multimodal model |
| Anthropic Claude Sonnet 4 | Strong at following complex instructions |

**Image generation models** (text-to-image):

| Model | Description |
| --- | --- |
| Auto (OpenRouter) | Let OpenRouter pick the best available model |
| Google Gemini 2.5 Flash Image | Fast image generation |
| OpenAI GPT-5 Image Mini | High-quality images |

If you're unsure, start with **Auto (OpenRouter)** — it automatically routes to a capable model with good availability.
