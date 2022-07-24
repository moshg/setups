1. pnpm create vite
1. index.html の lang などを設定する
1. pnpm create @eslint/config
1. 好みに応じて TypeScript の型も使った Lint: https://typescript-eslint.io/docs/linting/typed-linting
1. pnpm i -D prettier eslint-config-prettier
1. eslint.config を以下のように弄る

```json
{
  "extends": [
    "eslint:recommended",
    "plugin:react/recommended",
    "plugin:@typescript-eslint/recommended",
    "prettier"
  ],
  "rules": {
    "react/jsx-uses-react": "off",
    "react/react-in-jsx-scope": "off"
  }
}
```

7. .prettierrc を以下のように弄る

```json
{
  "singleQuote": true
}
```
