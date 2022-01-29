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

