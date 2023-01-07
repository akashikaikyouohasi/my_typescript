## 概要
Reactについて簡単にまとめる

### 始め方
Facebookが公開しているReact向け環境構築ツールを利用して、プロジェクト作成
```
npx create-react-app@latest [プロジェクト名] --template typescript
```

開発サーバを起動して、接続確認
```
cd [プロジェクト名]
npm run start

●ListenするIPアドレスを別のものに変える場合
HOST=192.168.56.50 npm run start
```

### ディレクトリ
#### src
ソースコード
#### public

### JSX
JavaScript/TypeScript中にHTMLタグを直接書き込める機能。

`tsx`拡張子となる。

