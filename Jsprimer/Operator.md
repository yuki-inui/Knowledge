# 演算子

## 二項演算
### プラス演算子(+)
```
console.log(1 + 1); => 2
```

### 文字列結合
```
const value = "文字列" + "結合";
console.log(value); // "文字列結合"
```

### マイナス演算子(-)
```
console.log(10 - 0.2); => 9.8
```

### 乗算演算子
```
console.log(2 * 3); => 6
```

### 除算演算子
```
console.log(8 / 2); => 4
```

### 剰余演算子
```
console.log(9 % 2);  => 1
console.log(8 % 2); => 0

### べき上演算子
```
console.log(2 ** 4) => 16
console.log(Math.pow(2, 4));  => 16
```

## 単項演算子（算術)

### インクリメント演算子(++)
```
let n = 1;
num++;
console.log(num); // 2
// num = num + 1 が計算されている
```

## 代入演算子(=)
```
let x = 1;
x =42;
console.log(x); // 42
```

## 分割代入
```
const obj = {
	"key": "value"
};
// プロパティ名`key`を変数`key`として変換 //
const { key } = obj;
console.log(key); => "value"
```
これは以下の内容と一緒である。   
```
const obj = {
	"key": "value"
};
const key = obj.key;
```

## 論理演算子

### AND演算子
```
//左辺がtrueなら右辺の結果返す
console.log(true && "右辺の値"); => "右辺の値"
//左辺がfalseなら右辺は実行されん
console.log(false && "右辺の値"); => "false"
```
AND演算子はif文と組み合わせできる   
```
const value = "str";
if (typeof value === "string" && value === "str"); {
	console.log(`${value} is string value');
```


