---
sidebar_position: 8
title: モデルの使用
---

ソースによると、言語モデルを直接使用するには、まず、言語モデルのインスタンスを生成します。生成されたインスタンスは、"Runnables"と呼ばれる標準インターフェースを公開しており、対話するための共通の手法を提供します。モデルを呼び出すには、`.invoke`メソッドにメッセージのリストを渡します。

例えば、以下のようにして、モデルにメッセージのリストを渡し、その応答を受け取ることができます。

```javascript
import { HumanMessage, SystemMessage } from "@langchain/core/messages";
const messages = [
  new SystemMessage("Translate the following from English into Italian"),
  new HumanMessage("hi!"),
];
await model.invoke(messages);
```

このコードでは、`HumanMessage`と`SystemMessage`を用いて、ユーザーとシステムのメッセージをそれぞれ定義し、それらを`messages`というリストに格納しています。そして、`model.invoke(messages)`のように、定義したメッセージのリストを`invoke`メソッドに渡すことで、モデルに対して翻訳の指示と翻訳対象のテキストを送信しています。

この`model.invoke`メソッドの戻り値は、`AIMessage`オブジェクトとなり、これには、文字列の応答と応答に関するその他のメタデータが含まれます。 多くの場合、文字列の応答のみを使用したい場合があります。その場合は、単純な出力パーサーを使用して、文字列の応答のみを抽出することができます。

出力パーサーを使用するには、まず、`StringOutputParser`をインポートします。

```javascript
import { StringOutputParser } from "@langchain/core/output_parsers";
const parser = new StringOutputParser();
```

そして、言語モデル呼び出しの結果を保存し、それをパーサーに渡すことで、文字列の応答のみを抽出できます。

```javascript
const result = await model.invoke(messages);
await parser.invoke(result); 
```

このコードでは、`parser.invoke(result)`を呼び出すことで、`result`（`AIMessage`オブジェクト）から文字列の応答("ciao!")のみが抽出されます。

また、`.pipe()`メソッドを使用して、モデルと出力パーサーを"チェーン"することもできます。これは、モデルの出力が自動的に出力パーサーに渡されることを意味します。

```javascript
const chain = model.pipe(parser);
await chain.invoke(messages);
```

このコードでは、`model.pipe(parser)`によって、モデルと出力パーサーがチェーン化され、`chain.invoke(messages)`のように、`chain`に対して`invoke`メソッドを呼び出すだけで、モデルの呼び出しと応答の解析が連続して実行されます。その結果、"Ciao!"という文字列が出力されます。

これは、LangChain Expression Language (LCEL)を使用してLangChainモジュールをチェーンする簡単な例です。このアプローチには、最適化されたストリーミングやトレースのサポートなど、いくつかの利点があります。