---
sidebar_position: 6
title: OpenAIモデルをインスタンス化
---

```js
import { ChatOpenAI } from "@langchain/openai";
const model = new ChatOpenAI({ model: "gpt-4" });
```

- 最初に`@langchain/openai`から`ChatOpenAI`をインポートします。
- `new ChatOpenAI()` で`ChatOpenAI`クラスのインスタンスを作成します。
- この例では、`model`パラ<!--  -->メータで"gpt-4"を指定することで、GPT-4モデルを使用することを明示しています。
