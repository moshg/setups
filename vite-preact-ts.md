1. pnpm init vite
1. index.html の lang などを設定する
1. pnpm i -D eslint eslint-config-preact
1. pnpm init @eslint/config
1. 好みに応じて TypeScript の型も使った Lint: https://typescript-eslint.io/docs/linting/type-linting
1. pnpm i -D prettier eslint-config-prettier
1. eslint.config を以下のように弄る

```json
{
  "extends": [
    "eslint:recommended",
    "preact",
    "plugin:@typescript-eslint/recommended",
    "prettier"
  ]
}
```
