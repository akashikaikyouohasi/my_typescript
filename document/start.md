## 前提条件
node.jsのバージョンは`v18.12.1`です

## npm,npx,yarnの違い
### npm
Node.jsのパッケージ管理ツール

### npx
npmでインストールしていないパッケージも利用可能
一次的にインストールして、使用後に削除してくれる

### yarn
npmと同じでパッケージ管理ツール
npmと互換があり、npmと比較して高速でセキュリティ高いらしい
パッケージがより厳密
参考URL：[npmとはyarnとは](https://qiita.com/Hai-dozo/items/90b852ac29b79a7ea02b)

## 変数
`var`は使わない！
`let`は変数、`const`は定数

### 型
`const num1: number`のようにコロン(`:`)でつなげること！

### 配列
配列`[]`に型をつけると、指定した型以外は入らなくなる

以下のように複数型の定義も可能
```
const mixedArrayU: (string|number) = ['foo', 1]
const mixedArrayT: [string, number] = ['foo', 1]
```

### オブジェクト型
`let 変数: { キー名1: 型1; ...} = オブジェクト`

`?`でオプショナル（省略可能）になる

### any
全てを受け入れる型で、型チェック機能が効かなくなるので使用しないこと！

JavaScriptから移行するときに一次的に使えるらしい。

## 関数
変数定義
```
function 関数名(引数: 型,...): 戻り値型{
    //...
}
```
引数や戻り値はの関数を指定することも可能

オプショナルやデフォルト値も可能

### アロー関数
定義
```
let 変数名: (引数名: 引数の型): 戻り値の型 => TypeScriptの式
```

### 関数の型
```
(引数名: 引数の型) => 戻り値の型
例： (x: string) => string[]
```


## 型推論
推論していい感じにしてくれる

### 型アサーション
戻り値の型がわからない時などに使用し、型を指定できる
```
変数 = 値 as 型
```

### 型エイリアス
型に別名を付ける
```
●例1
type Point = {
    x: number;
    y: number;
}
●例2
type Formatter = (a: string) => string
```

#### インデックス型
キー名とキー数が可変
```
●型
type Label = {
    [key: string]: string
}
●変数定義
const labels: Label = {
    top: 'トップ',
    bottom: 'ボトム'
}
```

## インタフェース
```
interface 型名 {
    プロパティ1: 型1;
    プロパティ2: 型2;
}
```
typeと違い、拡張可能

また、`implements`でクラスに実装を与えることができ‘、`extends`で継承可能

## クラス
```
class クラス名{
    フィールド1: 型1;
    フィールド2: 型2;
    //...
}
```
readonlyを付けると変更不可になる

### アクセス修飾子
public, private, publicがあり、デフォルトpublic


## 役立つ型
### Enum(列挙型)
TypeScriptの拡張機能
```
enum Direction = {
    'Up': 0,
    'Down': 1,
    'Left': 2,
    'Right': 3
}
```
列挙した値以外は代入不可

値を入れないと0から順番に割り当てられる。
文字列も可能

### ジェネリック型
型を外側から指定してふるまうクラスを記述するのに便利

Reactのコンポーネントもこれで、propsの型を外から定義できる

```
●型定義
class Queu<T> {
    private array: T[] = []
    push(item: T) {
        this.array.push(item)
    }
    pop(): T | undefined {
        return this.array.shift()
    }
}
●使用
const queue = new Queue<number>()
```

### Union型とIntersection型
和集合(`|`)のUnion型と、積集合(`&`)のIntersection型

```
type Id: number | string ⇒number or stringとなる
```
Unionでは、型エイリアスどうしも可能

```
type Employee = Identity & Contact ⇒２つを１つにまとめる
```

### リテラル型
決まった文字列や数値しか入らない型
```
変数: 許可データ1 | 許可データ2 | ...

●例
let status: 'OK' | 'NG' | 'Pending'
〇　status = 'OK'
×　status = 'Error'
```

### never型
決して値が返されることのない戻り値の型を定義できます
```
function error(message: string): never {
    throw new Error(message)
}
```
ifやswitch分で型の条件分岐に漏れがないことを保証することが可能

```
switch (type) {
    case Type.test:
        return "OK"
    case Type.test2:
        ...
    default:
        //起きてはいけないことをコンパイラに伝えるためにnever型に代入
        const wrongType: never = type
        throw new Error('not in Type')
}
```

### unknown
anyと同じでどのような値も代入可能だが、利用するにはtypeofで型安全な状況を創らないといけない

### 型定義ファイル
`@types/[ライブラリ名]`で公開されている型定義ファイルを導入するか、型定義ファイルを自作する

```
●jqueryの型定義ファイルの導入例
npm install --save-dev @types/jquery
```

自作する場合は`.d.ts`拡張子で定義する

