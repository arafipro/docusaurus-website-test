---
sidebar_position: 9
title: PromptTemplateの作成
---

PromptTemplateは、生のユーザー入力を言語モデルに渡す準備ができたデータ（プロンプト）に変換するのに役立つように設計されたLangChainの概念です。
PromptTemplateは、生のユーザー入力を受け取り、言語モデルに渡す準備ができたデータ（プロンプト）を返します。
一般的な変換には、システムメッセージの追加や、ユーザー入力を使用したテンプレートのフォーマットなどがあります。

**PromptTemplateの作成**

この例では、テキストを別の言語に翻訳するPromptTemplateを作成します。
このPromptTemplateは、次の2つのユーザー変数を受け取ります。

- language：テキストの翻訳先言語
- text：翻訳するテキスト

まず、システムメッセージとしてフォーマットする文字列を作成します。

```js
const systemTemplate = "Translate the following into {language}:";
```

次に、`systemTemplate`とテキストの配置場所を指定するより単純なテンプレートを組み合わせて、PromptTemplateを作成します。

```js
import { ChatPromptTemplate } from "@langchain/core/prompts";
const promptTemplate = ChatPromptTemplate.fromMessages([
  ["system", systemTemplate],
  ["user", "{text}"],
]);
```

**PromptTemplateの使用**

このプロンプトテンプレートへの入力は辞書です。
プロンプトテンプレート単独でどのような動作をするのかを確認するために、以下のように試すことができます。

```js
const result = await promptTemplate.invoke({ language: "italian", text: "hi" });
result;
```

これにより、2つのメッセージで構成される`ChatPromptValue`が返されます。
メッセージに直接アクセスする場合は、次のようにします。

```js
result.toChatMessages();
```

このPromptTemplateを、上記のモデルと言語パーサーと組み合わせることができます。
これにより、3つのコンポーネントすべてが連鎖します。

```js
const chain = promptTemplate.pipe(model).pipe(parser);
await chain.invoke({ language: "italian", text: "hi" });
```

これにより、"ciao"が出力されます。 
