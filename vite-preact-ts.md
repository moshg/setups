1. pnpm create vite
1. index.html の lang などを設定する
1. `pnpm create @eslint/config # Reactを使用するとして設定する`
1. 好みに応じて TypeScript の型も使った Lint: https://typescript-eslint.io/docs/linting/typed-linting
1. pnpm i -D eslint-config-preact prettier eslint-config-prettier
1. eslint.config を以下のように弄る

```json
{
  "extends": [
    "eslint:recommended",
    "plugin:react/recommended",
    "preact",
    "plugin:@typescript-eslint/recommended",
    "prettier"
  ]
}
```

7. .prettierrc を以下のように弄る

```json
{
  "singleQuote": true
}
```
