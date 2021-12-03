型表現に使われる演算子
---
`typeof`演算子
渡された値の``型の名前``を文字列に返す   
型のコンテキストで用いると変数から型を抽出してくれる       

  ```
  console.log(typeof100); //'number'
const arr = [1, 2, 3];
 console.log(typeofarr); //'object'
type NumArr = typeof arr;
 const val: NumArr = [4, 5, 6];
constval2:NumArr=['foo','bar','baz']; //compileerror!
```
NumArrは`number[]`であるため`string[]`はエラーになる。これは型推論   

`in`演算子    
指定した値がオブジェクトのキーとして存在するか どうかの真偽値を返したりする。   
`for...in` 文ではオブジェクトからインクリメンタルにキーを抽出する のに使われる。   
型コンテキストでは、列挙された型の中から各要素の型の値を抜き出して マップ型(Mapped Types)   

```
const obj={a:1,b:2,c:3};
console.log('a' in obj); // true
for(const key in obj){console.log(key);} //abc

type Fig = 'one' | 'two' | 'three'; 
type FigMap = { [k in Fig]?: number };
const figMap: FigMap = {
one: 1,
two: 2,
three: 3, 
};
figMap.four=4; //compileerror!
```