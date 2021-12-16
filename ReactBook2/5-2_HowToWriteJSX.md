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