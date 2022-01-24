# 関数と宣言

## 関数宣言
```
// 関数宣言
function 関数名　(仮引数１, 仮引数2) {
	return 返り値;
}
```

```
function Add(num) {
	return num + 3;
}

const AddFuntion = (num) => num + 3:

console.log(3) // 6
```

## 関数の引数
```
funciton echo(x) {
	return x;
}

console.log(echo(4)); // 4
console.log(echo()); // undefined
```

複数の引数をもつ場合、余ったものはundefinedする
```
function argumentToArray(x, y) {
	return [x, y];
}

console.log(argumentToArray(1, 2)); // [1, 2]
console.log(argumentTaArray(1)); // [1, undefined]
```

デフォルト引数
```
function default(x = 123) {
	return x;
}

console.log(3); // 3
console.log(); // 123
```
`123` がデフォルトの引数である。

## ReatParametor
```
function add(...arg) {
	console.log(arg);
}
add("a", "b", "c");
```

Restparametorは仮引数と一緒にできる
```
function fn(arg1, ...restArg) {
	console.log(arg1);  // "a"
	console.log(...restArg);  // ["b", "c", "d"];
};
fn("a", "b", "c", "d");
```

Spread構文  
	関数の引数に渡すもの
```
function fn(x, y, z) {
	console.log(x);
	console.log(y);
	console.log(z);
};
const array = [1, 2, 3];  
//Spread構文で表すと
fn(...array);
```

函数の引数と分割代入
```
function printUserId(user) {
	console.log(user.id);
};
const user = {
	id: 43
};
printUserId(user);
```
    
printuserIdはオジェクト{id}を引数として受け取れる
```
function printUserid({ id }) {
	console.log(id);
};
const user = {
	id: 43
};
printUserId(user);
```

分割代入は配列でも使える
```
function print([first, second]) {
	console.log(first);
	console.log(second);
};
const array = [1, 2];
print(array);
```

## 関数はオブジェクト

関数式  
```
//factorialは関数の外から呼び出すことできる
//innerFactは関数の外から呼び出しできない
const factorial = function innerfact(n) {
	if(n === 0) {
		return 1;
	}
	// innnerfactを再起的に呼び出す
	return n * innerfact(n -1);
};
console.log(factorial(5));  //20
```

```
const array = [1, 2, 3, 4];

const doublearray = array.map(value => value * 2);
console.log(doublearray); // [2, 4, 6, 8]
// 仮引数が一つのため`()`を省略可能
// 関数が一つのため return が省略可能
```




