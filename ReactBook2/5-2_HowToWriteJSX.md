# JSXの書き方

JSXにはその中に別の式を埋め込むことができる。   

式の埋め込みには`{}`を使う。   

しかし`{}`の中には式しか書き込めない。 ifやfor文などは組み込めない。   

nullやundefinedやbooleanのtrueやfalseなどは出力されない。   


```
const name = 'Patty';
const greet = (name: string) => <p>Hello, {name || 'Guest'}!</p>;

return <div>{greet(name)}</div>;
```

JSX に埋め込めるのは式だけだから if文などの制御文を中に書くことはできない。   

任意の条件によってレンダリングするものを分けたいことがある。その場合はこの boolean 値が何もレンダリングされない性質を利用する。   
```
const n = Math.floor(Math.random() * 10); //0~9までの整数を作成
const threshold = 5;

return (
  <div>
    {n > threshold && <p>'n' is larger than {threshold}</p>}
    <p>`n` is {n % 2 === 0 ? 'even' : 'odd'}</p>
  </div>
);
```
`<div>`の下には if文を代用するJSXでの式表現で、&&論理演算子によるショートサーキット評価を用いる。  
その下にはif else文の代わりの三項演算子を用いている。

`n > threshold`と`n % 2 === 0`はtrue falseを表すので、JSXの中では影響されない   
JSXは文は書けず、常に値を返す式を作らなくてはいけない関数型のプログラミングである。   

繰り返し表現はこのように表される
```
const list = ['Patty', 'Rolley', 'Bobby'];

return (
  <ul>
    {list.map((name) => (
      <li>Hello, {name}!</li>
    ))}
  </ul>
);
```

コメントの書き方はこれではなく
```
const elems = ( 
  <div>foo</div> 
  <div>bar</div> 
  <div>baz</div>
);
```
```
const elems = ( 
  <div>
    <div>foo</div> 
    <div>bar</div> 
    <div>baz</div>
  </div> 
);
```
この方がいい   

しかし、HTMLにレンダリングされた時、意味のないノード階層が余分にできる。   

そこで`Fragments(フラグメンツ)`を使うことで防ぐ。   
```
const elems = ( 
  <>
    <div>foo</div> 
    <div>bar</div> 
    <div>baz</div>
  </> 
);
```
空のタグ<>は `<React.Fragment>`の省略記法で使われている。


# JSXとコンポーネントの関係

# Reactの組み込みのコンポーネント
JSXのユーザー定義コンポーネントは、必ず大文字から始める   

小文字だと、組み込みコンポーネントになる。   
