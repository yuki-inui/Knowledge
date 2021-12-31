# 配列の反復処理

- map() 配列を任意の新しいものに出力する
- filter() 適合する配列を新しく出力する
- find() 適合するもののうち**最初**の数字を出力する
- findIndex() 適合するもののうち最初のインデックスを出力する
- every() 与えられた要素が全て適合するか真偽値で出力する
- some()  与えられた要素の中、一つでも適合すれば真を出すもの
```
const　arr　=　[1, 2, 3, 4, 5, 6, 7, 8, 9];

console.log(arr.map((n) => n * 2));
console.log(arr.filter((n) => n % 3 === 0));
console.log(arr.find((n) => n > 4));
console.log(arr.findIndex((n) => n > 4));
console.log(arr.every((n) => n !== 0));
console.log(arr.some((n) => n >= 10));
```
reduceの説明
---
reduce(n, m);  (n:第一引数, m:第二引数)
mは配列の順序ごとに数字が代入される。
nは前回の結果が入る

- 1回目: mは１回目の数字であるため、１が処理される。
- 2回目: nは`1`であり、mは2回目の2が計算され、　3が処理される
- 3回目: nは`3`であり、mは3回目の3が計算され、　6が処理される
- 4回目: nは`6`であり、mは4回目の4が計算され、　10が処理される
- 5回目: nは`10`であり、mは5回目の5が計算され、　15が処理される

このような処理がなされている。
ただ単に数字が合計されているわけではない

sortの説明
---
「比較関数」
- 第 1 引数が第 2 引数より優先度が高い(前に来る)場合、-1 を返す
- 第 1 引数が第 2 引数より優先度が低い(後に来る)場合、1 を返す
- 第 1 引数と第 2 引数の優先度が同じ(ソートの必要がない)場合、0 を返す(※省略可)
　
 
 参考コード<br>
`const arr = [1,2,3,4,5];`
`console.log(arr.reduce((n, m) => n + m)); // 15`
`console.log(arr.sort((n, m) => n > m? -1 : 1)); //[5,4,3,2,1]`

Sliceの説明
---
Sliceメソッドは　startとend が明記されている場合、startからendまで(endは含まない)の要素を返す。
  `-2`などマイナスではあれば配列の最後のものを列挙する。
  無名関数であれば、そのまま配列をコピーしてくれる。
  
参考コード
```
const lst = [5, 7, 1, 3];
console.log(lst.slice().sort((n, m) => n < m ? -1 : 1)); //[1,3,5,7]`
console.log(lst); //[5,7,1,3]`

objectと反復処理
---
`Object.key()`はプロパティのキーのリスト
`Object.value()`はプロパティ値のリスト
`Object.entire()`はキーと一体となった全て

参考コード
```
const user = {
 name: 'Yuki-Inui',
 username: 'Yuki',
 id: 3,
 email: Yuki@gmail.com,
 };
 
console.log(Object.keys(user));
// [ 'id', 'name', 'username', 'email' ]

console.log(Object.values(user));
// [ 3, 'Bobby Bear', 'bobby', 'bobby@maple.town' ]
```


  
  


