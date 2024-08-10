---
sidebar_position: 7
title: OpenAIモデルの使用
---

インスタンス化したOpenAIモデル`model`を使用して、`.invoke`メソッドにメッセージのリストを渡します。
たとえば、以下のようにして、モデルにメッセージのリストを渡し、その応答を受け取ることができます。

```js
import { HumanMessage, SystemMessage } from "@langchain/core/messages";
const messages = [
  new SystemMessage("Translate the following from English into Italian"),
  new HumanMessage("hi!"),
];
await model.invoke(messages);
```

このコードでは、`HumanMessage`と`SystemMessage`を用いて、ユーザーとシステムのメッセージをそれぞれ定義し、それらを`messages`というリストに格納しています。
そして、`model.invoke(messages)`のように、定義したメッセージのリストを`invoke`メソッドに渡すことで、モデルに対して翻訳の指示と翻訳対象のテキストを送信しています。

この`model.invoke`メソッドの戻り値は、`AIMessage`オブジェクトとなり、これには、文字列の応答と応答に関するその他のメタデータが含まれます。
多くの場合、文字列の応答のみを使用したい場合があります。その場合は、単純な出力パーサーを使用して、文字列の応答のみを抽出できます。
