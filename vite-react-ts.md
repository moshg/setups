# (P)React + Vite + TypeScript のセットアップ

## プロジェクト作成

以下のコマンドを実行する

```sh
pnpm create vite
√ Select a framework: » React
√ Select a variant: » TypeScript + SWC
```

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

## eslint, prettier

以下のコマンドを実行する

```sh
pnpm create @eslint/config
```

好みに応じて TypeScript の型も使ったリントを設定する: https://typescript-eslint.io/docs/linting/typed-linting

hooks のリントを追加

```sh
pnpm i -D eslint-plugin-react-hooks
```

Preact を使用する場合

```sh
pnpm i -D eslint-config-preact
```

prettier を追加

```sh
pnpm i -D prettier eslint-config-prettier
```

prettier のインポート順プラグイン追加

```sh
pnpm i -D @trivago/prettier-plugin-sort-imports
```

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

```sh
pnpm i vite-plugin-checker -D
```

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
