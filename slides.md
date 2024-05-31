---
theme: apple-basic
background: https://cover.sli.dev
title: LLM AI 应用的简单实现方法
info: |
  ## EMQ 培训内容
  本教程旨在介绍如何使用大语言模型 API 构建简单的 AI 应用。
class: text-left
highlighter: shiki
drawings:
  persist: false
transition: slide-left
mdc: true
lineNumbers: true
---

<div class="absolute inset-0 flex flex-col justify-center items-center">
  <h1 class="relative inline-flex items-center">
    <span class="text-black mr-2">🚀</span>
    <span class="bg-clip-text text-transparent" style="background-image: linear-gradient(123deg, #5e4eff 13.15%, #f14eff 88.72%);">
      LLM AI 应用的简单实现方法
    </span>
  </h1>
  <p class="pt-6">如何使用大语言模型 API 构建简单的 AI 应用</p>
</div>

---

<h1 class="relative inline-flex items-center">
  <span class="text-black mr-2">📱</span>
  <span class="bg-clip-text text-transparent" style="background-image: linear-gradient(123deg, #5e4eff 13.15%, #f14eff 88.72%);">
    大语言模型应用
  </span>
</h1>

> 大语言模型（LLM）是一种利用机器学习技术来理解和生成人类语言的人工智能模型。而大语言模型的 AI 应用则是基于这种模型构建的各种应用程序。

<ul class="py-4">
  <li>ChatGPT</li>
  <li>GitHub Copilot</li>
  <li>Notion AI</li>
  <li>...</li>
</ul>

为什么需要基于大语言模型的 AI 应用？

<ul class="pt-4">
  <li>提升生产力</li>
  <li>增强创作</li>
  <li>智能交互</li>
  <li>...</li>
</ul>

---

<h1 class="relative inline-flex items-center">
  <span class="text-black mr-2">🌐</span>
  <span class="bg-clip-text text-transparent" style="background-image: linear-gradient(123deg, #5e4eff 13.15%, #f14eff 88.72%);">
    大语言模型 API
  </span>
</h1>

<p class="pt-6">构建大语言模型 AI 最简单和快速的方式就是直接使用 AI 厂商提供的 API 服务。</p>

<p class="pt-6">常见的 LLM 服务 API 平台：</p>

<ul>
  <li><a href="https://platform.openai.com/docs/api-reference/introduction">OpenAI Platform</a></li>
  <li><a href="https://azure.microsoft.com/en-us/products/ai-services/openai-service">Azure OpenAI</a></li>
  <li><a href="https://ai.google.dev/gemini-api">Google Gemini</a></li>
  <li><a href="https://docs.anthropic.com/en/api/getting-started">Anthropic - Claude</a></li>
  <li><a href="https://platform.moonshot.cn/docs/api/chat#%E5%9F%BA%E6%9C%AC%E4%BF%A1%E6%81%AF">Kimi</a></li>
  <li>通义千问，文言一心</li>
  <li>...</li>
</ul>

---

<h1 class="relative inline-flex items-center">
  <span class="bg-clip-text text-transparent" style="background-image: linear-gradient(123deg, #5e4eff 13.15%, #f14eff 88.72%);">
    使用 OpenAI API
  </span>
</h1>

<p class="pt-6">我们可以通过使用任何语言的 HTTP 请求，或者利用其官方的 Python 包和 Node.js 库，甚至社区维护的库，与 Open AI 的大语言模型通过 API 来进行交互。</p>

OpenAI API 提供了多种功能：

- 文本生成 (Text Generation)
  - Chat Completions API
  - JSON Mode
- 函数调用 (Function Calling)
- 嵌入 (Embeddings)
- 微调 (Fine-tuning)
- 图像生成 (Image Generation)
- 视觉处理 (Vision)
- ...

---

<h1 class="relative inline-flex items-center">
  <span class="bg-clip-text text-transparent" style="background-image: linear-gradient(123deg, #5e4eff 13.15%, #f14eff 88.72%);">
    Chat Completions API
  </span>
</h1>

```shell {all|1|3|5|7-10|11-14} twoslash
curl https://api.openai.com/v1/chat/completions \
  -H "Content-Type: application/json" \
  -H "Authorization: Bearer $OPENAI_API_KEY" \
  -d '{
    "model": "gpt-3.5-turbo-16k",
    "messages": [
      {
        "role": "system",
        "content": "You are a helpful assistant."
      },
      {
        "role": "user",
        "content": "Hello!"
      }
    ]
  }'
```

<ExplainAPI :content="[
  '请求的 API 端点',
  '认证信息，API Key 配置在这里',
  '选择一个支持的大语言模型',
  '发送一条系统消息',
  '用户输入一条消息'
]" />

---

<h1 class="relative inline-flex items-center">
  <span class="bg-clip-text text-transparent" style="background-image: linear-gradient(123deg, #5e4eff 13.15%, #f14eff 88.72%);">
    Streaming
  </span>
</h1>

````md magic-move
```shell
curl https://api.openai.com/v1/chat/completions \
  -H "Content-Type: application/json" \
  -H "Authorization: Bearer $OPENAI_API_KEY" \
  -d '{
    "model": "gpt-3.5-turbo-16k",
    "messages": [
      {
        "role": "system",
        "content": "You are a helpful assistant."
      },
      {
        "role": "user",
        "content": "Hello!"
      }
    ]
  }'
```
```shell {all|16} twoslash
curl https://api.openai.com/v1/chat/completions \
  -H "Content-Type: application/json" \
  -H "Authorization: Bearer $OPENAI_API_KEY" \
  -d '{
    "model": "gpt-3.5-turbo-16k",
    "messages": [
      {
        "role": "system",
        "content": "You are a helpful assistant."
      },
      {
        "role": "user",
        "content": "Hello!"
      }
    ],
    "stream": true
  }'
```
````

<p v-click="[2]" class="pt-4">启用流模式后，消息将以增量方式发送，就像在 ChatGPT 中一样。数据会作为 <a href="https://developer.mozilla.org/en-US/docs/Web/API/Server-sent_events/Using_server-sent_events#Event_stream_format">Server-Sent Events(SSE)</a> 实时传送，每当有新的数据可用时就会发送。传输过程会以一个 <code>data: [DONE]</code> 消息结束。</p>

---
layout: two-cols
---

## Default Response

```json
{
  "id": "chatcmpl-123",
  "object": "chat.completion",
  "created": 1677652288,
  "model": "gpt-3.5-turbo-0125",
  "system_fingerprint": "fp_44709d6fcb",
  "choices": [{
    "index": 0,
    "message": {
      "role": "assistant",
      "content": "\n\nHello there, how may I assist you today?",
    },
    "logprobs": null,
    "finish_reason": "stop"
  }],
  "usage": {
    "prompt_tokens": 9,
    "completion_tokens": 12,
    "total_tokens": 21
  }
}
```

::right::

## Streaming Response

```json
{"id":"chatcmpl-123","object":"chat.completion.chunk","created":1694268190,"model":"gpt-3.5-turbo-0125", "system_fingerprint": "fp_44709d6fcb", "choices":[{"index":0,"delta":{"role":"assistant","content":""},"logprobs":null,"finish_reason":null}]}

{"id":"chatcmpl-123","object":"chat.completion.chunk","created":1694268190,"model":"gpt-3.5-turbo-0125", "system_fingerprint": "fp_44709d6fcb", "choices":[{"index":0,"delta":{"content":"Hello"},"logprobs":null,"finish_reason":null}]}

{"id":"chatcmpl-123","object":"chat.completion.chunk","created":1694268190,"model":"gpt-3.5-turbo-0125", "system_fingerprint": "fp_44709d6fcb", "choices":[{"index":0,"delta":{"content":"How are"},"logprobs":null,"finish_reason":null}]}

....

{"id":"chatcmpl-123","object":"chat.completion.chunk","created":1694268190,"model":"gpt-3.5-turbo-0125", "system_fingerprint": "fp_44709d6fcb", "choices":[{"index":0,"delta":{},"logprobs":null,"finish_reason":"stop"}]}
```

<style>
.grid {
  gap: 12px;
}
</style>

---

<h1 class="relative inline-flex items-center">
  <span class="bg-clip-text text-transparent" style="background-image: linear-gradient(123deg, #5e4eff 13.15%, #f14eff 88.72%);">
    常用配置
  </span>
</h1>

```json {all|2|3|4|5|6|7|8-21|all} twoslash
{
  "model": "gpt-4o",
  "temperature": 0.7,
  "max_tokens": 1500,
  "top_p": 1,
  "stream": true,
  "stop": ["\n\n"],
  "messages": [
    {
      "role": "system",
      "content": "你是一个帮助用户进行编程任务的 AI 助手。"
    },
    {
      "role": "user",
      "content": "我正在使用 JavaScript，请问如何定义一个箭头函数？"
    },
    {
      "role": "assistant",
      "content": "你可以使用以下语法定义一个箭头函数：\n\n```javascript\nconst myFunction = () => {\n  // 你的代码\n};\n```"
    }
  ]
}
```

<ExplainAPI :content="[
  '使用的模型，如 gpt-4o, gpt-4-turbo 等',
  '生成文本的随机性，较高的值使输出更随机，较低的值使输出更确定',
  '生成文本的最大令牌数',
  '核心采样，多样性控制',
  '启用流式输出',
  '停止生成的标志',
  '对话的消息列表。包含角色和内容，确保对话连贯性',
]" />

<style>
.explain-api {
  position: absolute;
  top: 7rem;
  right: 6rem;
}
</style>

---
layout: two-cols
---

## Python

```shell
pip install openai
```

```python
from openai import OpenAI

client = OpenAI()

stream = client.chat.completions.create(
    model="gpt-3.5-turbo",
    messages=[{"role": "user", "content": "Say this is a test"}],
    stream=True,
)
for chunk in stream:
    if chunk.choices[0].delta.content is not None:
        print(chunk.choices[0].delta.content, end="")
```

::right::

## Node.js / Typescript

```shell
npm install openai@^4.0.0
```

```javascript
import OpenAI from "openai";

const openai = new OpenAI();

async function main() {
    const stream = await openai.chat.completions.create({
        model: "gpt-3.5-turbo",
        messages: [{ role: "user", content: "Say this is a test" }],
        stream: true,
    });
    for await (const chunk of stream) {
        process.stdout.write(chunk.choices[0]?.delta?.content || "");
    }
}

main();
```

<style>
.grid {
  gap: 24px;
}
</style>
---

<h1 class="relative inline-flex items-center">
  <span class="bg-clip-text text-transparent" style="background-image: linear-gradient(123deg, #5e4eff 13.15%, #f14eff 88.72%);">
    使用本地 AI 服务
  </span>
</h1>

使用 Ollama 一键运行 Llama 3，并且内置提供了 API 服务。

```shell
# 使用 Ollama 运行 Llama 3 模型默认为 8B 参数版本
ollama run llama3

# 运行 Open WebUI，一个开源的 AI 聊天 UI 服务器
docker run -d -p 3000:8080 --add-host=host.docker.internal:host-gateway -v open-webui:/app/backend/data --name open-webui --restart always ghcr.io/open-webui/open-webui:main

# 使用本地的大语言模型 API
curl -X POST http://localhost:11434/api/generate -d '{
  "model": "llama3",
  "prompt":"Why is the sky blue?"
 }'
```

---

<img src="/ollama.png" class="h-120" />

---

<h1 class="relative inline-flex items-center">
  <span class="bg-clip-text text-transparent" style="background-image: linear-gradient(123deg, #5e4eff 13.15%, #f14eff 88.72%);">
    Prompt 提示工程
  </span>
</h1>

<img src="/prompt.png" class="h-100" />

此提示演示了如何有效使用每个构建块，从而产生高质量的输出。

---

<h1 class="relative inline-flex items-center mb-5">
  <span class="bg-clip-text text-transparent" style="background-image: linear-gradient(123deg, #5e4eff 13.15%, #f14eff 88.72%);">
    Demo: MQTTX Copilot
  </span>
</h1>

```javascript
const response = await fetch('https://api.openai.com/v1/chat/completions', fetchOptions)
if (response && response.status === 200 && response.ok) {
  const throttledScroll = throttle(() => {
    this.scrollToBottom()
  }, 500)
  const done = await processStream(response, (chunkStr) => {
    this.responseStreamText += chunkStr
    this.$nextTick(() => {
      Prism.highlightAllUnder(this.$refs.chatBody as HTMLElement)
      throttledScroll()
    })
  })
  if (done) {
    responseMessage.content = this.responseStreamText
    await copilotService.create(responseMessage)
    this.messages.push(responseMessage)
    this.$nextTick(() => {
      Prism.highlightAllUnder(this.$refs.chatBody as HTMLElement)
    })
  }
}
```

https://github.com/emqx/MQTTX/blob/main/src/components/Copilot.vue

---

<img src="/copilot-code-quick-actions.png" class="h-100"/>

https://mqttx.app/docs/copilot

---

<h1 class="relative inline-flex items-center mb-5">
  <span class="bg-clip-text text-transparent" style="background-image: linear-gradient(123deg, #5e4eff 13.15%, #f14eff 88.72%);">
    Demo: 使用 OpenAI Node.js SDK 构建一个 AI Agent
  </span>
</h1>

<br/>

本教程展示了如何使用 OpenAI 函数和 Open AI 的 Node.js SDK 构建一个智能代理应用。

- 应用功能：帮助用户找到本地活动。
- 使用的两个函数：`getLocation()` 和 `getCurrentWeather()`。
- OpenAI 只提供函数调用建议，实际执行由应用完成。

---

获取位置：
```javascript
async function getLocation() {
  const response = await fetch("https://ipapi.co/json/");
  const locationData = await response.json();
  return locationData;
}
```
获取天气：
```javascript
async function getCurrentWeather(latitude, longitude) {
  const url = `https://api.open-meteo.com/v1/forecast?latitude=${latitude}&longitude=${longitude}&hourly=apparent_temperature`;
  const response = await fetch(url);
  const weatherData = await response.json();
  return weatherData;
}
```

---

描述函数：

```javascript
const tools = [
  {
    type: "function",
    function: {
      name: "getCurrentWeather",
      description: "Get the current weather in a given location",
      parameters: {
        type: "object",
        properties: {
          latitude: { type: "string" },
          longitude: { type: "string" },
        },
        required: ["longitude", "latitude"],
      },
    }
  },
  {
    type: "function",
    function: {
      name: "getLocation",
      description: "Get the user's location based on their IP address",
      parameters: {
        type: "object",
        properties: {},
      },
    }
  },
];
```

---

设置消息数组：

```javascript
const messages = [
  {
    role: "system",
    content: "You are a helpful assistant. Only use the functions you have been provided with.",
  },
];
```

- 定义消息数组

- 设置系统角色和初始内容

---

创建代理函数：

```javascript
async function agent(userInput) {
  messages.push({ role: "user", content: userInput });
  const response = await openai.chat.completions.create({
    model: "gpt-4",
    messages,
    tools,
  });
  console.log(response);
}
```

- 代理函数处理用户输入

- 调用 OpenAI API 获取响应

---

```javascript
for (let i = 0; i < 5; i++) {
  const response = await openai.chat.completions.create({
    model: "gpt-4",
    messages: messages,
    tools: tools,
  });
  const availableTools = { getCurrentWeather, getLocation };
  const { finish_reason, message } = response.choices[0];
  if (finish_reason === "tool_calls" && message.tool_calls) {
    const functionName = message.tool_calls[0].function.name;
    const functionToCall = availableTools[functionName];
    const functionArgs = JSON.parse(message.tool_calls[0].function.arguments);
    const functionArgsArr = Object.values(functionArgs);
    const functionResponse = await functionToCall.apply(null, functionArgsArr);
    messages.push({
      role: "function",
      name: functionName,
      content: `The result of the last function was this: ${JSON.stringify(functionResponse)}`
    });
  }
}
```

- 从 OpenAI API 的响应中获取函数名称和参数。
- 动态调用相应的函数并处理结果。
- 使用循环处理多次迭代，直到获得最终答案。

---

运行应用：

```javascript
const response = await agent("Please suggest some activities based on my location and the current weather.");
console.log(response);
```

- 运行代理函数并输出结果。

- 示例输出：根据用户位置和天气推荐活动。

---

<h1 class="relative inline-flex items-center mb-5">
  <span class="bg-clip-text text-transparent" style="background-image: linear-gradient(123deg, #5e4eff 13.15%, #f14eff 88.72%);">
    使用限制
  </span>
</h1>

<br/>

直接使用 AI 服务的 API 会有一些限制：

- 一定的费用
- 网络依赖
- 数据隐私
- 请求速率限制
- 响应延迟

使用本地 LLM API 的话：

- 对机器配置的限制比较高
- 维护成本
- 存储需求
- 能耗问题
- 部署复杂性

---

<h1 class="relative inline-flex items-center mb-5">
  <span class="bg-clip-text text-transparent" style="background-image: linear-gradient(123deg, #5e4eff 13.15%, #f14eff 88.72%);">
    扩展
  </span>
</h1>

- [AI Agent](https://aws.amazon.com/what-is/ai-agents/)
- [RAG (Retrieval-Augmented Generation) 模型](https://aws.amazon.com/what-is/retrieval-augmented-generation/)
- [🦜🔗 LangChain](https://www.langchain.com/)
- [Dify.AI](https://dify.ai/)
- [Lobe UI](https://ui.lobehub.com/), [open-webui](https://docs.openwebui.com/)
- Apps
    - ChatGPT Web | Desktop (Chat APP)
    - [v0](https://v0.dev/)
    - [Perplexity AI](https://www.perplexity.ai/)

---

<h1 class="relative inline-flex items-center mb-5">
  <span class="text-black mr-2">🤔</span>
  <span class="bg-clip-text text-transparent" style="background-image: linear-gradient(123deg, #5e4eff 13.15%, #f14eff 88.72%);">
    Thinking
  </span>
</h1>

<div class="grid grid-cols-2 gap-4">
  <div>
    <ul>
      <li>MQTT + AI -> Agent?</li>
      <li>带来便利的同时也有安全问题
        <ul>
          <li><span v-mark.circle.red="1">隐私和安全</span></li>
          <li>准确性和偏见</li>
        </ul>
      </li>
      <li>Local-first</li>
      <li>大模型的闭源与开源</li>
    </ul>
  </div>
  <div>
    <Tweet id="1793252867454685232" />
  </div>
</div>

---

<div class="absolute inset-0 flex flex-col justify-center items-center">
  <h1 class="relative inline-flex items-center">
    <span class="text-black mr-2">🙏</span>
    <span class="bg-clip-text text-transparent" style="background-image: linear-gradient(123deg, #5e4eff 13.15%, #f14eff 88.72%);">
      Thanks
    </span>
  </h1>
  <p class="pt-6">Shifan Yu 2024-5-31</p>
</div>

---
