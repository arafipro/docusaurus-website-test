---
sidebar_position: 5
title: 環境変数を設定
---

LangChainでLLMアプリケーションを構築する際には、使用する言語モデルに応じて**環境変数を設定**が必要になります。
環境変数は、APIキーなどの機密情報をコードに直接書き込むことなく、アプリケーションに渡すために使用されます。

設定方法は、オペレーティングシステムやシェル環境によって異なりますが、一般的には以下のいずれかの方法が使用されます。

- **直接設定:** `export`コマンドを使用して、現在のセッションの環境変数を設定します。
  
  ```bash
  export OPENAI_API_KEY="your-api-key"
  ```

- **.envファイル:** プロジェクトのルートディレクトリに`.env`ファイルを作成し、環境変数を記述します。
  
  ```
  OPENAI_API_KEY="your-api-key"
  ```

  そして、`process.env`オブジェクトを使用して環境変数を参照できます。
  
  ```javascript
  const apiKey = process.env.OPENAI_API_KEY;
  ```
