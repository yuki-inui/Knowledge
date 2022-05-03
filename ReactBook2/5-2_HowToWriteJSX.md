# JSXの書き方

## JSXの基本的な文法
JSXは``React.createElement``のメソッドコールに対するシンタックスシュガーである。
また、``tsconfig.json``で``jsx``オプションを``react``にすると、
JSXの記載は、``React.createElement(...)``のように変換される。  
であるため、JSXの記載においては、``React``のインポートが必要になる。  
しかし、**Typescript4.1**以降では``React17.0``以降で導入された、新たな変換方式で、  
``jsx``オプションを``react-jsx``にすることで、``React``のimportを省略できるよ。  

``JSX``はその中に``式``を埋め込むことができる。しかし、``文``は無理。  
また、``null`` ``undefined`` ``true`` ``false``は何も出力されない。  
```
const name = "patty";
const greet = (name: string) => <p> Hello! {name : `Guest`}! </p>;
return <div>{greet(name)}</div>;
```

しかし、任意のレンダリングをしたい場合、``boolean``が何も影響しないことを使う。
```
const n = Math.floor(Math.random() * 10); // 0 〜 9 の整数を生成  
const threshold = 5;  
return ( 
  <div>{n > threshold && <p>`n` is larger than {threshold}</p>} //if文の代わりになる表現。ショートサーキット評価をしている。
        <p>`n` is {n % 2 === 0 ? 'even' : 'odd'}</p> if-elseを表している。  
  </div>
);
```

次に、繰り返し処理はこのように表される。  
```
const list = [`Patty`, `Rolley`, `Bobby`];

return (
  <ul>
    {list.map((name) => (
      <li>Hello, {name}!</li>
    ))}
  </ul>
);
```
以上に付け加えて``.filter(...)``や``.map(...)``などのメソッドチェーンや演算子を用いて表せる。  

``JSX``のコメントの書き方は
```
<div> {
3 > 1 && 'foo' // インラインコメント }
{/* 複数行に
渡るコメント */}
</div>
```
あくまで``JSX``はjavascriptなので、HTML形式では表されない。  


``JSX``を記載する上で注意すべき点、複数の要素で表される場合はトップレベルが一つの要素にならんといけない。  
```
const elems = (
  <div>foo</div>
  <div>bar</div>
  <div>baz</div>
);
```
これを修正したものが  
```
const elems = (
  <div>
    <div>foo</div>
    <div>bar</div>
    <div>baz</div>
  </div>
);
```

しかし、これでは**ノード階層**が多くなるため不適。ここで**フラグメント**を使用する。  
```
const elems = (
  <>
    <div>foo</div>
    <div>bar</div>
    <div>baz</div>
  </>
);
// <> は元は<React.Fragment>というコンポーネント。それの省略技法。
```

## JSXとコンポーネントの関係
JSX構文は``React.createElement()``のメソッドコールに変換され、最終的に``ReactElement``を生成する。  
ここで``ReactElement``は実行リンクのような働きをする。  

実行リンクがコンポーネント関数をコールする際に渡す引数は、``ReactElement``の``prop``プロパティである。

## Reactの組み込みコンポーネント
Reactのコンポーネントは、``ユーザー定義コンポーネント``と``組み込みコンポーネント``の２種類がある。  
ユーザーが自前に定義する場合、命名規則がある。必ず大文字から始めなければいけない。  
もし小文字で始めると、組み込みコンポーネントとして解釈される。  
