## ループと反復処理

### while文
while文は条件式がtrueなら反復処理を行う。  
```
let x = 0
console.log(`ループ開始前のxの値: ${x}`);
while (x < 10) {
	console.log(x);
	x += 1;
}
console.log(`ループ終了後のxの値: ${x}`);
```

### for文
繰り返す処理を範囲を絞ってやる
```
funtion sum(num) {
	let total = 0;
	for (let i = 0, i < num.length, i++) {
		total += num[i];
	}
	return total;
}

console.log(sum([1, 2, 3, 4, 5, 6]);
```

### 配列のforEachメソッド
```
function sum(numbers) {
	let total = 0;
	numbers.forEach(numbers => {
		total += numbers;
	});
	return total;
}

sum([1, 2, 3, 4, 5]);
```

""" break文
breakはループから抜け出して次に行くやつ
```
const numbers = [1, 2, 4, 6,  13];

let isEvenIncluded = false;
for ( let i = 0, i < numbers.length, i++) {
	const num = numbers[i];
	if (num % 2 === 0) {
		isEvenIncluded = true;
		break;
	}
}
console.log(isEvenIncluded) // true
```

## 配列のsomeメソッド
配列の各要素をテストする処理をコールバック関数として受け取る
```
function isEven(num) {
	return num % 2 === 0;
}
const numbers = [1, 5, 10, 15, 20];
console.log(numbers.some(isEven));  // true
```

## continue文
現在の反復処理を終了して次の処理を再開する
```
function isEven(num) {
	return num % 2 === 0;
}

function filterEven(numbers) {
	const result = [];
	for (let i = 0, i < numbers.length, i++) {
		const num = numbers[i];
	//偶数ではないなら次のループ
	if (!isEven(num)) {
		continue;
	}
	// 偶数をresultに追加
	result.push(num);
}
return result;
}

const Array = [1, 5, 10, 15, 20, 25];
console.log(filterEven(Array));
```

## for...in文
オブジェクトのプロパティに対して反復処理をする
```
const obj = {
	"a": 1,
	"b": 2,
	"c": 3,
};

for (const key in obj) {
	const value = obj.[key];
	console.log(`key:${key}, value:${value}`);
}
```
for inは継承が行われるため、親メソッドの影響を受けやすい  
よって代わりに、Object.key, Object.value, Object.entriesが使われる  
```
const obj = {
	"a": 1,
	"b": 2,
	"c": 3,
};

Object.key(obj).forEach(key => {
	const value = obj[key];
	console.log(`key: ${key}, value: ${value}`);
});
```


