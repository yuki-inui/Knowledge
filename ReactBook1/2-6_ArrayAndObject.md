## 分割代入とスプレッド構文
```
const key = 'bar';
const baz = 65456;
const obj1 = {foo:256, [key]: 4095, baz: baz};
console.log(obj1);

const obj2 = { baz };
console.log(obj2); // {baz: 65456}
```

obj2において、変数bazの名前がプロパティのkeyに、値がそのプロパティの値になる。これを**プロパティ名のショートバンド**という。  

### 分割代入
```
const [n, m] = [1, 4];
console.log(n, m); //1 4

const obj = { name: 'kanae', age: 24 };
const {name, age} = obj;
console.log(name, age); //kanae 24
```
これが分割代入です。  

応用を効かした書き方
```
const response = {
  data: [
    {
      id: 1,
      name: 'patty rabbit',
      email: 'patty@maple.com',
    },
    {
      id: 2,
      name: 'Rolley Cocker',
      email: 'rolley@palm.town',
    },
    {
      id: 3,
      name: 'Bobby Bear',
      email: 'bobby@maple.town',
    },
  ],
};

const {data: users = [] } = response;
console.log(users);
```

## オブジェクトのマージとコピー
オブジェクト型の値は別の変数に代入しただけだと、参照渡し[^1]になり実体を共有されたままになる。  
[^1]: 渡された引数が変更されたら、呼び出し元も変更される。

スプレッド構文を使ってコピーをしていく。  
```
const original = { a: 1, b: 2, c: 3 };
const copy = {...original};
console.log(copy); //{ a: 1, b: 2, c: 3 }
console.log(original === copy); //false

const assigned = {...original, ...{ c: 10, d: 50 }, d: 100 };
console.log(assigned); // { a: 1, b: 2, c: 10, d: 100 }
console.log(original); // { a: 1, b: 2, c: 3 }
```
この記述でoriginalが汚染されずに変更がされたが、これは**シャローコピー**[^1]といってコピーされる深さが１段階までしか有効ではない。  
プロパティの値がオブジェクト・配列であった場合はそれらの値までコピーできない。  

