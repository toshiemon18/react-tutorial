# React Tutorial

## Overview
### Reactとは?
* Reactでは独立したUIをコンポーネントとして定義していく
* 以下は `React.Component` というコンポーネントクラスのサブクラスとして定義したもの
	* コンポーネントには何を描画するかを定義する

```js
class ShoppingList extends React.Component {
  render() {
    return (
      <div className="shopping-list">
        <h1>Shopping List for {this.props.name}</h1>
        <ul>
          <li>Instagram</li>
          <li>WhatsApp</li>
          <li>Oculus</li>
        </ul>
      </div>
    );
  }
}

// Example usage: <ShoppingList name="Mark" />
```

## Componentの各要素について
* ShoppingList について
	* React.Component型のクラス
	* コンポーネントは初期化されたときにpropsというパラメータを受け取って `render` メソッドでビューのDOMを返す
	* renderが返すのはDOMのスケルトンで、これにpropなどで渡されたパラメータや状態によって描画内容を制御する感じ
	* 中身的には `React.createElement()` が呼ばれてDOMに変換されていく

* JSXについて
	* JavaScriptのコードを埋め込めるテンプレート言語っぽいやつ
	* `<div />` やら `<li />` といったHTMLのDOMコンポーネントの他にも独自定義の Reactコンポーネントも同様にかける
		* `<ShoppingList />` みたいな感じ

## How to build components?
* props経由でデータをコンポーネントにわたす
	* `<Square value=1>` のような感じでコンポーネントに値を渡せる
	* コンポーネント側で受け取った値を参照するには、 `{this.props.value}` のように書けばよい

* state で状態を持つ
	* constructor で状態を初期化する
		```
		class Hoge extends React.Component {
			constructor(props) {
				super(props)
				this.state = {
					value: null,
				}
			}
		}
		```
	* onClickなどのフックで `this.setState()` を使って状態を更新していく
		* `setState` が呼ばれた時点でコンポーネントとその内側にあるコンポーネントは更新される

## Why immutability is important?
* 複雑な機能の実装が容易になる
	* ex) tutorial のタイムトラベル機能
	* 可変性のデータを扱わず、不変なデータを記録していくことで再利用したり
* 変更検知
	* mutableなオブジェクトは内容の変更検知が困難
	* immutableであれば、差分を見ればいいのでめちゃ簡単になる
* Reactの再レンダリングタイミングを決定できる
	* 先の変更検知の延長だが、差分を検知していつコンポーネントを再レンダリングすればよいか判断が付きやすい
	* keyword: `shouldComponentUpdate()` , pure component
	* ref: (https://ja.reactjs.org/docs/optimizing-performance.html#examples)[パフォーマンス最適化]

## Functional Component
* ステートを持たないコンポーネントの記法
* `React.Component` を継承せず、`props` を入力とする関数を定義する
```js
function Square(props) {
	return (
		<button className="square" onClick={props.onClick}>
			{ props.value }
		</button>
	);
}
```
