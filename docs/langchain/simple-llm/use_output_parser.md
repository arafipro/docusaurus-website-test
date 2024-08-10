---
sidebar_position: 8
title: OutputParserの使用
---

OutputParserは、言語モデルからの応答から文字列型の応答のみを抽出するために使用されます。

まず、`StringOutputParser` をインポートします。


```js
import { StringOutputParser } from "@langchain/core/output_parsers";
const parser = new StringOutputParser();
```

次に、言語モデル呼び出しの結果を保存し、それをパーサーに渡すことで、文字列の応答のみを抽出できます。

```js
const result = await model.invoke(messages);
await parser.invoke(result); 
```

このコードでは、`parser.invoke(result)` を呼び出すことで、`result`（`AIMessage` オブジェクト）から文字列の応答 ("ciao!") のみが抽出されます。

また、`.pipe()`メソッドを使用して、モデルと出力パーサーを"チェーン"することもできます。
これは、モデルの出力が自動的に出力パーサーに渡されることを意味します。

```js
const chain = model.pipe(parser);
await chain.invoke(messages);
```

このコードでは、`model.pipe(parser)`によって、モデルと出力パーサーがチェーン化されます。
そして、`chain.invoke(messages)`のように、`chain`に対して`invoke`メソッドを呼び出すだけで、モデルの呼び出しと応答の解析が連続して実行されます。
その結果、 "Ciao!"という文字列が出力されます。 

これは、LangChain Expression Language (LCEL) を使用してLangChainモジュールをチェーンする簡単な例です。
このアプローチには、最適化されたストリーミングやトレースのサポートなど、いくつかの利点があります。 
