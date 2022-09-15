# (P)React + Vite + TypeScript のセットアップ

## プロジェクト作成

`npm create vite`

`index.html` の lang などを設定する

Preact を利用する場合は以下のエイリアスを tsconfig に設定する

```json
"compilerOptions": {
"baseUrl": "./",
  "paths": {
    "react": ["./node_modules/preact/compat/"],
    "react-dom": ["./node_modules/preact/compat/"]
  }
}
```

## xo

eslint のラッパー

`npm i -D xo`

## eslint, prettier

`npm create @eslint/config`

好みに応じて TypeScript の型も使ったリントを設定する: https://typescript-eslint.io/docs/linting/typed-linting

hooks のリントを追加

`npm i -D eslint-plugin-react-hooks`

Preact を使用する場合

`npm i -D eslint-config-preact`

prettier を追加

`npm i -D prettier eslint-config-prettier`

prettier のインポート順プラグイン追加

`npm i -D @trivago/prettier-plugin-sort-imports`

追加した eslint のプラグインを設定に.eslintrc に追加

```json
{
  "extends": [
    "eslint:recommended",
    "plugin:react/recommended",
    "plugin:react-hooks/recommended",
    "preact", // Preactを利用する場合
    "plugin:@typescript-eslint/recommended",
    "prettier"
  ],
  "rules": {
    "react/jsx-uses-react": "off",
    "react/react-in-jsx-scope": "off"
  }
}
```

.prettierrc に設定を追加

```json
{
  "singleQuote": true,
  "importOrder": ["^[./]"],
  "importOrderSeparation": true,
  "importOrderSortSpecifiers": true
}
```

## TypeScript

そのままでは Vite で型チェックが行われないのでツールをインストールする。

`npm i vite-plugin-checker -D`

`vite.config.ts` に追記する

```ts
import { defineConfig } from "vite";
import checker from "vite-plugin-checker";

export default defineConfig({
  plugins: [
    checker({
      typescript: true,
      eslint: {
        lintCommand: 'eslint "./src/**/*.{ts,tsx}"', // for example, lint .ts & .tsx
      },
    }),
    preact(),
  ],
});
```

## storybook

`npx storybook init --builder @storybook/builder-vite`
