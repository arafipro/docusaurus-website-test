---
sidebar_position: 7
title: モデルをインスタンス化
---

ソースによると、LangChainで提供されている様々なチャットモデルをインスタンス化するコードは、使用するモデルによって異なります。以下は、ソースで示されている各チャットモデルのインスタンス化コードとその解説です。

**1. OpenAI**

```javascript
import { ChatOpenAI } from "@langchain/openai";
const model = new ChatOpenAI({ model: "gpt-4" });
```

* 最初に`@langchain/openai`から`ChatOpenAI`をインポートします。
* `new ChatOpenAI()` で`ChatOpenAI`クラスのインスタンスを作成します。
* この例では、`model`パラメータで"gpt-4"を指定することで、GPT-4モデルを使用することを明示しています。

**2. Anthropic**

```javascript
import { ChatAnthropic } from "@langchain/anthropic";
const model = new ChatAnthropic({
  model: "claude-3-5-sonnet-20240620",
  temperature: 0
});
```

* `@langchain/anthropic`から`ChatAnthropic`をインポートします。
* `new ChatAnthropic()`で`ChatAnthropic`クラスのインスタンスを作成します。
* `model`パラメータで使用するAnthropicのモデルを指定します。
* `temperature`パラメータで応答のランダム性を制御します。0は最も確定的で、値が大きいほどランダムになります。

**3. FireworksAI**

```javascript
import { ChatFireworks } from "@langchain/community/chat_models/fireworks";
const model = new ChatFireworks({
  model: "accounts/fireworks/models/llama-v3p1-70b-instruct",
  temperature: 0
});
```

* `@langchain/community/chat_models/fireworks`から`ChatFireworks`をインポートします。 
* `new ChatFireworks()`で`ChatFireworks`クラスのインスタンスを作成します。
* `model`パラメータで使用するFireworksAIのモデルを指定します。
* `temperature`パラメータで応答のランダム性を制御します。

**4. MistralAI**

```javascript
import { ChatMistralAI } from "@langchain/mistralai";
const model = new ChatMistralAI({
  model: "mistral-large-latest",
  temperature: 0
});
```

*  `@langchain/mistralai`から`ChatMistralAI`をインポートします。
* `new ChatMistralAI()`で`ChatMistralAI`クラスのインスタンスを作成します。
* `model`パラメータで使用するMistralAIのモデルを指定します。
* `temperature`パラメータで応答のランダム性を制御します。

**5. Groq**

```javascript
import { ChatGroq } from "@langchain/groq";
const model = new ChatGroq({
  model: "mixtral-8x7b-32768",
  temperature: 0
});
```

* `@langchain/groq`から`ChatGroq`をインポートします。
* `new ChatGroq()`で`ChatGroq`クラスのインスタンスを作成します。
* `model`パラメータで使用するGroqのモデルを指定します。
* `temperature`パラメータで応答のランダム性を制御します。

**6. VertexAI**

```javascript
import { ChatVertexAI } from "@langchain/google-vertexai";
const model = new ChatVertexAI({
  model: "gemini-1.5-flash",
  temperature: 0
});
```

* `@langchain/google-vertexai`から`ChatVertexAI`をインポートします。
* `new ChatVertexAI()`で`ChatVertexAI`クラスのインスタンスを作成します。
* `model`パラメータで使用するVertexAIのモデルを指定します。
* `temperature`パラメータで応答のランダム性を制御します。

これらのコードは、各言語モデルを使用するための基本的な構成を示しています。 
インスタンス化の際には、それぞれのモデルに応じて必要なパラメータを指定する必要があることに注意してください。 
詳細については、各言語モデルのAPIドキュメントを参照することをお勧めします。 