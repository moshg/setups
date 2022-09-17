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

React 対応

`npm install --save-dev eslint-config-xo-react eslint-plugin-react eslint-plugin-react-hooks`

package.json に設定を加える

```json
{
  "xo": {
    "space": true,
    "prettier": true,
    "extends": "xo-react/space"
  }
}
```

VSCode を使用する場合、`xo`の拡張機能導入後に以下の設定を追加する。

```json
{
  "editor.formatOnSave": true,
  "xo.enable": true,
  "xo.format.enable": true,
  "[javascript]": {
    "editor.defaultFormatter": "samverschueren.linter-xo"
  },
  "[typescript]": {
    "editor.defaultFormatter": "samverschueren.linter-xo"
  }
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
        lintCommand: 'xo "./src/**/*.{ts,tsx}"',
      },
    }),
    preact(),
  ],
});
```

## storybook

`npx storybook init --builder @storybook/builder-vite`
