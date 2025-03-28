---
title: "API Keys"
linkTitle: "API Keys"
weight: 20
date: 2025-03-28
description: >
  了解如何在 Cursor 中为 OpenAI、Anthropic、Google 和 Azure LLM 提供商使用您自己的 API key
---

Cursor 允许您为各种 LLM 提供商输入自己的 API 密钥，以便以自己的成本发送尽可能多的 AI 消息。当使用客户 API key 时，我们将在调用 LLM 提供程序时使用该密钥。

若要使用您自己的 API 密钥，请前往 Cursor Settings > Models，然后输入您的 API 密钥。然后，点击“验证”按钮。一旦您的密钥通过验证，您的 API 密钥将被启用。


## FAQ

### 我的 API 密钥会被存储还是会离开我的设备？

您的 API 密钥将不会被存储，但它将与每个请求一起发送到我们的服务器。所有的请求都通过我们的后端路由，我们在那里做最后的提示建设。

### 支持哪些自定义LLM提供程序？

Cursor 仅支持与 OpenAI API 格式（如 OpenRouter）兼容的 API 提供程序。我们不提供对自定义本地 LLM 设置或其他 API 格式的支持。如果您遇到的自定义 API 设置问题不是来自我们支持的提供商，我们很遗憾无法提供技术支持。