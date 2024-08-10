---
sidebar_position: 6
title: 環境変数の追加
---

ソースによると、LangChainでLLMアプリケーションを構築する際には、使用する言語モデルに応じて**環境変数の追加**が必要になります。環境変数は、APIキーなどの機密情報をコードに直接書き込むことなく、アプリケーションに渡すために使用されます。

**手順**

1. **使用する言語モデルを選択:** ソースでは、OpenAI、Anthropic、FireworksAI、MistralAI、Groq、VertexAIといった主要な言語モデルが紹介されており、それぞれのモデルで必要な環境変数が異なります。

2. **環境変数を設定:** 選択した言語モデルに応じて、必要な環境変数を設定します。設定方法は、オペレーティングシステムやシェル環境によって異なりますが、一般的には以下のいずれかの方法が使用されます。

   - **直接設定:** `export`コマンドを使用して、現在のセッションの環境変数を設定します。
     ```bash
     export OPENAI_API_KEY="your-api-key"
     ```

   - **.envファイル:** プロジェクトのルートディレクトリに`.env`ファイルを作成し、環境変数を記述します。
     ```
     OPENAI_API_KEY="your-api-key"
     ```

3. **環境変数をコードから参照:**  JavaScriptでは、`process.env`オブジェクトを使用して環境変数を参照できます。
     ```javascript
     const apiKey = process.env.OPENAI_API_KEY;
     ```

**各言語モデルで必要な環境変数:**

* **OpenAI:** `OPENAI_API_KEY`
* **Anthropic:** `ANTHROPIC_API_KEY`
* **FireworksAI:** `FIREWORKS_API_KEY`
* **MistralAI:** `MISTRAL_API_KEY`
* **Groq:** `GROQ_API_KEY`
* **VertexAI:** `GOOGLE_APPLICATION_CREDENTIALS` (認証情報を含むJSONファイルのパス)

**重要なポイント**

* 環境変数名は、各言語モデルのAPIドキュメントで確認してください。
* APIキーなどの機密情報は、コードに直接書き込まず、環境変数として設定してください。
* ソースはJavaScriptでの利用を想定していますが、他の言語でも同様の方法で環境変数を設定できます。

**追加情報**

* ソースでは、LangSmithというツールを使用して、LangChainアプリケーションのデバッグとトレースを行う方法についても解説されています。LangSmithを使用する場合、`LANGCHAIN_TRACING_V2`と`LANGCHAIN_API_KEY`の環境変数を設定する必要があります。

**注記:** この解説は提供されたソースに基づいており、LangChainのバージョンや利用環境によって手順や情報が異なる可能性があります。最新の情報については、LangChainの公式ドキュメントを参照してください。 
