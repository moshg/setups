# Tanstack Router + Vite + TypeScript のセットアップ

## プロジェクト作成

以下のコマンドを実行する

```sh
pnpm create @tanstack/router
```

## TypeScript

以下のコマンドを実行する

```sh
pnpm add -D typescript
```

tsconfig.json を編集する

```diff json
{
  "compilerOptions": {
+   "skipLibCheck": true
  }
}
```

Vite ではデフォルトで型チェックが行われないのでプラグインをインストールする。

```sh
pnpm add -D vite-plugin-checker
```

`vite.config.ts` に追記する

```diff ts
import { defineConfig } from "vite";
import checker from "vite-plugin-checker";

export default defineConfig({
  plugins: [
+   checker({
+     typescript: true,
+   }),
  ],
});
```

## ESLint

以下のコマンドを実行する

```sh
pnpm create @eslint/config
√ Which framework does your project use? · react
√ Does your project use TypeScript? · typescript
√ Where does your code run? · browser                                                            
The config that you've selected requires the following dependencies:

eslint, globals, @eslint/js, typescript-eslint, eslint-plugin-react
√ Would you like to install them now? · No / Yes
√ Which package manager do you want to use? · pnpm
```

hooks のリントを追加

```sh
pnpm add -D eslint-plugin-react-hooks
```

```diff js
export default [
  {
    files: ["**/*.{js,mjs,cjs,ts,jsx,tsx}"],
+   plugins: {
+     "react-hooks": pluginReactHooks,
+   },
+   rules: {
+     ...pluginReactHooks.configs.recommended.rules,
+   }
  }
];
```

好みに応じて TypeScript の型も使ったリントを設定する: [Linting with Type Information](https://typescript-eslint.io/getting-started/typed-linting/)

## Biome

以下のコマンドを実行する

```sh
pnpm add -D @biomejs/biome
```

設定ファイルを作成する

```sh
pnpm biome init
```

biome.json を編集する

```diff json
{
  "files": {
+   "ignore": ["**/routeTree.gen.ts"]
  },
  "linter": {
-   "enabled": true,
+   "enabled": false,
  }
}
```
