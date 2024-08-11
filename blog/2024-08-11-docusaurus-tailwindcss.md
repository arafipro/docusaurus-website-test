---
slug: docusaurus-tailwindcss
title: DocusaurusにTailwind CSSを導入
tags: [tailwindcss, docusaurus]
draft: true
---

DocusaurusにTailwind CSSを導入する方法を紹介します。  

:::info
Docusaurusのプロジェクトは用意している前提で進めます。  
また、TypeScriptを使用しています。  
:::

{/* truncate */}

## 1. Tailwind CSSをインストール

まずは、Tailwind CSSをインストールします。  
以下のコマンドを実行してください。

```sh
npm add -D tailwindcss postcss autoprefixer
```

## 2. `tailwind.config.js`を作成

以下のコマンドを実行して、`tailwind.config.js`を作成します。

```sh
npx tailwindcss init
```

作成すると、以下のような、コードが用意されています。

```js title="tailwind.config.js"
/** @type {import('tailwindcss').Config} */
module.exports = {
    content: [],
  theme: {
    extend: {},
  },
  plugins: [],
}
```

ファイル名を`tailwind.config.js`から`tailwind.config.ts`に拡張子を変更します。  
次に、コードを以下のように変更します。

```ts title="tailwind.config.ts"
import type { Config } from "tailwindcss";
import { fontFamily } from "tailwindcss/defaultTheme";

const config = {
  corePlugins: {
    preflight: false,
    container: false,
  },
  darkMode: ["class", '[data-theme="dark"]'],
  content: ["./src/**/*.{jsx,tsx,html}"],
  theme: {
    extend: {
      fontFamily: {
        sans: ['"Inter"', ...fontFamily.sans],
        jakarta: ['"Plus Jakarta Sans"', ...fontFamily.sans],
        mono: ['"Fira Code"', ...fontFamily.mono],
      },
      borderRadius: {
        sm: "4px",
      },
      screens: {
        sm: "0px",
        lg: "997px",
      },
      colors: {},
    },
  },
  plugins: [],
} satisfies Config;

export default config;
```

## 3. `docusaurus.config.ts`に設定を追加

`docusaurus.config.ts`を開いて、`plugins`プロパティを追加します。

```ts title="docusaurus.config.ts"
const config = {
  // highlight-next-line
  plugins: [], // 追加
```

## 4. `tailwind-plugin.ts`を作成

`plugins`ディレクトリを作成して、その中に`tailwind-plugin.ts`を作成します。  
`tailwind-plugin.ts`には、以下のコードを貼り付けます。

```js title="plugins/tailwind-plugin.ts"
export default function tailwindPlugin() {
  return {
    name: "tailwind-plugin",
    configurePostCss(postcssOptions) {
      postcssOptions.plugins = [
        require("postcss-import"),
        require("tailwindcss"),
        require("autoprefixer"),
      ];
      return postcssOptions;
    },
  };
}
```

`tailwindPlugin`をインポートします。
また、`docusaurus.config.ts`の`plugins`プロパティに`tailwindPlugin`を追加します。  

```ts title="docusaurus.config.ts"
// highlight-next-line
import tailwindPlugin from "./plugins/tailwind-config.ts"; // 追加

const config = {
  // highlight-next-line
  plugins: [tailwindPlugin], // tailwindPluginを追加
```

## 5. `custom.css`に設定を追加

`custom.css`に各@tailwindディレクティブを追加します。

```css title="src/css/custom.css"
@tailwind base;
@tailwind components;
@tailwind utilities;
```

## 6. Tailwind CSSの動作確認

src/pages/index.tsxに以下のコードを追加します。

```ts title="src/pages/index.tsx"
export default function Home(): JSX.Element {
  const { siteConfig } = useDocusaurusContext();
  return (
    <Layout
      title={`${siteConfig.title}`}
      description="Description will go into a meta tag in <head />"
    >
      <HomepageHeader />
      <main>
        // highlight-start
        <p className="flex justify-center text-7xl text-red-500">
          Tailwind CSS test
        </p>
        // highlight-end
        <HomepageFeatures />
      </main>
    </Layout>
  );
}
```

以下のコマンドを実行して、Tailwind CSSの動作確認をします。

```sh
npm start
```
