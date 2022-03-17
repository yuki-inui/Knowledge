## 関数とスコープ

### スコープ
```
function fn() {
	const x = 1;
	//fn関数の中での参照であるため
	console.log(x); // =>1
};
fn();
//関数の外にあるためエラー
console.log(x); // Error
```

// 関数のスコープ
```
異なる関数のスコープには同じ"x"を定義できる
function fnA() {
	let x;
}
function fnB() {
	let x;
}
```

## スコープチェーン
```
{
	//Outerスコープ
	const x = "x";
	{
		//InnerスコープからOuterスコープを参照できる
		console.log(x); // => "x"
	}
}
```

```
{
	//Outerスコープ
	const x = Outer;
	{
		//Innerスコープ
		const x = Inner;
		//現在のInnerスコープ"x”参照できる
		console.log(x); // => Inner
	}
	console.log(x); // => Onter
}
```

## グローバルスコープ
Innerスコープには参照するものがない場合、グローバルが参照される。  
```
//グローバルはどこからでも参照できる
const x = "グローバル";
{
	//参照するものないから外のスコープへ
	console.log(x); // => ”グローバル"
}

//関数スコープ
function fn() {
	//参照するものない。外のスコープへ
	console.log(x);
}
```

## 参照の範囲を狭める
コードを書くにつれ、どの変数がピックされるかわからない。その対処法は関数にする

```
const doHeavyTask() {
//　書きたいなよう
};

const startTime = Date.now();
doHeavyTask();
const endTime = Date.now();
console.log(`実行時間は${startTime - endTime}ミリ秒`);
```
このコードでは``startTime``と``endTime``関数がグローバルスコープになっている。  
```
// 実行時間を計測したい関数をコールバック関数として引数に渡す
const measureTask = (taskFn) => {
    const startTime = Date.now();
    taskFn();
    const endTime = Date.now();
    console.log(`実行時間は${endTime - startTime}ミリ秒`);
};
function doHeavyTask() {
    // 計測したい処理
}
measureTask(doHeavyTask);
```

## 関数スコープとvarの巻き上げ
初期値を持たない変数を宣言すると、undefinedになる。
```
let let_x;
var var_x;
//宣言後に参照するとundefinedになる
console.log(let_x); // => undefined
console.log(var_x); // => undefined
// 宣言後に値を代入できる
let_x = "letのx";
var_x = "varのx";
```

letでは、変数を**宣言する前**に変数を参照すると、ReferenceErrorが発生する。
```
console.log(x); // => ReferenceError: can't access lexical declaration `x' before initialization
let x = "letのx";
```

一方varでは、変数を宣言する前にその変数を参照してもundefinedとなります。
```
// var宣言より前に参照してもエラーにならない
console.log(x); // => undefined
var x = "varのx";
```

```
// 解釈されたコード
// スコープの先頭に宣言部分が巻き上げられる
var x;
console.log(x); // => undefined
// 変数への代入はそのままの位置に残る
x = "varのx";
console.log(x); // => "varのx"
```

## 関数宣言と巻き上げ
functionキーワードを使った関数宣言もvarと同様に、もっとも近い関数またはグローバルスコープの先頭に巻き上げられます。 次のコードでは、実際にhello関数を宣言した行より前に関数を呼び出せます。　　

```
// `hello`関数の宣言より前に呼び出せる
hello(); // => "Hello"

function hello(){
    return "Hello";
}
```
以上のコードは以下のものと同じである
```
// 解釈されたコード
// `hello`関数の宣言が巻き上げられる
function hello(){
    return "Hello";
}

hello(); // => "Hello"
```

varと関数宣言はvarが優先して巻き上げられるため、undefinendが表示される。   

## 即時実行関数
即時実行関数(IIFE(Immediately-Invoked Function Expression))は、グローバルスコープの汚染を避けるために生まれたものである。  
次のように、匿名関数を宣言した直後に呼び出すことで、任意の処理を関数のスコープに閉じて実行できます。 関数スコープを作ることでfoo変数は匿名関数の外側からはアクセスできません。  

```
// 匿名関数を宣言 + 実行を同時に行っている
(function() {
    // 関数のスコープ内でfoo変数を宣言している
    var foo = "foo";
    console.log(foo); // => "foo"
})();
// foo変数のスコープ外
console.log(typeof foo === "undefined"); // => true
```

## クロージャー
```
// `increment`関数を定義して返す関数
function createCounter() {
	let count = 0;
	// `increment`関数は`count`変数を参照
	function increment() {
		count = count + 1;
		return count;
	}
	return increment;
}

// `myCounter`は`createCounter`が返した関数を参照
const myCounter = createCounter();
myCounter(); // => 1
myCounter(); // => 2
// 新しく`newCounter`を定義する
// 新しく`newCounter`を定義する
const newCounter = createCounter();
newCounter(); // => 1
newCounter(); // => 2
// `myCounter`と`newCounter`は別々の状態持っている
myCounter(); // => 3
newCounter(); // => 3
```


