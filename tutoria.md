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

* ShoppingList について
	* React.Component型のクラス
	* コンポーネントは初期化されたときにpropsというパラメータを受け取って `render` メソッドでビューのDOMを返す
	* renderが返すのはDOMのスケルトンで、これにpropなどで渡されたパラメータや状態によって描画内容を制御する感じ
	* 中身的には `React.createElement()` が呼ばれてDOMに変換されていく

* JSXについて
	* JavaScriptのコードを埋め込めるテンプレート言語っぽいやつ
	* `<div />` やら `<li />` といったHTMLのDOMコンポーネントの他にも独自定義の Reactコンポーネントも同様にかける
		* `<ShoppingList />` みたいな感じ

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
