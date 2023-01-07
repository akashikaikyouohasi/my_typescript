## 概要
開発時の設定などを残す

### tsconfig.json
コンパイルに必要なオプションなど情報を書き込む
`tsc --init`でデフォルトファイルが作成される

#### strict
`strict`をtrueにして、厳密な型チェックを行う


### Prettier
フォーマッター

以下でインストール
`npm install prettier --save-dev`

`.prettierrc`が設定ファイルで、以下のように設定する
```
{
    // コードの末尾にセミコロンを入れるか
    "semi": falsem,
    // オブジェクト定義の最後のカンマを無しにするか
    "trailingComm": "none"
    // 文字列の定義などクオートにシングルクォートを使用するか
    "singleQuote": true,
    // 行を開業する際の文字数
    "printWidth": 80
}
```
`package.json`に以下を追記する
```
{
    "scripts": {
        ...
        "prettie-format": "prettier --config .prettierrc 'src/**/*.ts' --write"
    }
}
```
`npm run prettier-format`を実行することで`src`配下がフォーマットされる

### ESLint
悪い書き方を指摘してくれ、`.eslintrc.js`で設定する

ただ、Next.jsはESLintの設定をデフォルトで持つ

### コンパイルオブション
#### noImplicitAny
暗黙的なanyをエラーにする

#### strictNullChecks
nullやundefinedを利用するには、型にunion型なので定義する必要がある

#### target
コンパイル時のECMAScriptのバージョン指定



