---
sidebar_position: 10
title: チェーンの作成
---

LangChain Expression Language (LCEL) を使用して、LangChainモジュールをチェーン接続できます。
`.pipe()` メソッドは、LangChainで2つの要素を組み合わせるために使用されます。
これは、最適化されたストリーミングやトレースのサポートなど、いくつかの利点があります。

**チェーンの例**

この例では、プロンプトテンプレート、言語モデル、出力パーサーの3つのコンポーネントをチェーン接続します。

```javascript
const chain = promptTemplate.pipe(model).pipe(parser);
```

このチェーンは、最初にプロンプトテンプレートを呼び出し、次にその結果を言語モデルに渡し、最後に言語モデルの出力を出力パーサーに渡します。
