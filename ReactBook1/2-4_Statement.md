# 関数宣言(statements)と関数式(expression)

関数宣言文   
```
function double (n) {  
  return n * 2;  
  }  
```  
  
関数式  
```
const double = function (n) {  
  return n * 2;  
  };  
```  
  最終的には関数式では代入を行なっているため、末尾にセミコロンがある
  

# アロー関数
```
const addOne = (n) => {   　
  return n + 1;　
  };
```  
省略して書いたら
```  
const addOne = n => n + 1;
```
引数が一つだけの場合は省略可能

# デフォルト引数
```
const raise = (n, m = 2) => n *** m;  
console.log(raise(2, 3));   //8   
console.log(raise(3));  
```
`n ** m` は nをm乗する関数である
また、(n, m = 2)で2乗は設定されているため、raise(3)では3^2が出力される

# Rest Parametors
最後の引数の名前に...をつけることで残りの引数を配列として受け取ることができる。

```
const showname = (a, b, ...rest) => {
  console.log(a);
  console.log(b);
  console.log(rest);
};

showname('jon', 'jony', 'json', 'julia');
```
第二引数以降しか使えないわけではない。第一引数としてReat Parametorsを使えば中身全てを配列として返す。  
```
const showallargs = (...args) => {
  console.log(args);
};
console.log(showallargs('A', 'B', 'C', 'D')); // ['A', 'B', 'C', 'D']
```

またRest Parametorsを名前をつけて取得したい場合は以下のように記述する。  
```
const sum = (i, ...[j, k, l]) => i + j + k + l;
console.log(sum(1, 2, 3, 4)); //10
console.log(sum(1, 1, 1, 1, 1)); //4　超過分は消される。
```
