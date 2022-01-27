## 配列

## 配列の作成とアクセス
```
const empty = [];
const array = [1, 2, 3];
const matrix = [
	["a", "b"],
	["c", "d"]
];
```

```
const array = ["one", "two", "three"];
console.log(array[0]); // "one"
```

```
const matrix = [
	["a", "b"],
	["c", "d"]
];

console.log(matrix[0][1]); // "d"
```

## オブジェクトが配列かどうか
Array.isArrayメソッド。
```
const obj = {};
const array = [];
console.log(Array.isArray(obj)); // => false
console.log(Array.isArray(array)); // => true
```

## 配列と分割代入
```
const array = ["one", "two", "three"];

const [first, second, third] = array;
console.log(first);
console.log(second);
console.log(third);
```

## インデックスの取得
```
const array = ["Java", "Javascript", "Ruby"];

const indexOfJs = array.indexOfJs("Java"); 
console.log(indexOfJs);
```


