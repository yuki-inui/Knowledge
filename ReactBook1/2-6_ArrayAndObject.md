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