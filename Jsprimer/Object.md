## オブジェクト

```
const Object = {
	"key": "value"
};
```

```
const Object = {
	key: "value"
};
```
オブジェクトリテラルのプロパティキーは省略可能

```
const Object = {
	my-loop: "value"
}; // NG
```

```
const Object = {
	"my-loop": "value"
};
```
識別子としてできないものは省略できない

複数のプロパティを持つオブジェクトを作成できる
```
const color = {
	red: "red",
	green: "green",
	blue: "blue",
};
```

```
const name = "名前";

const obj = {
	name: name
};

console.log(obj); => { name: "名前" }
```
プロパティ名と変数が一緒なら省略可能
```
const name = "名前";
const obj = {
	name
};

console.log(obj); => { name: "名前”}
```


## プロパティへのアクセス
```
const obj = {
	key: "value"
};

//ドット記法//
console.log(obj.key);

//ブラケット記法//
console.log(obj["key"]);
```

ドット記法ではプロパティ名が識別子と同じく、命名規則を満たす必要あり
```
console.log(obj.key); // OK
console.log(obj.123); // NG	数字は入れてはいけない
console.log(obj.my-loop); // NG	ハイフンは入れない
```

ブラケット記法はプロパティ名に変数を利用できる
```
const languages = {
	ja: "日本語",
	eng: "英語"
};

const mylang = "ja";
console.log(languages[mylang]);
```

## オブジェクトと分割代入
```
const languages = {
	ja: "日本語",
	eng: "英語"
};

const ja = languages.ja;
const eng = languages.eng;

console.log(ja);
console.log(eng);
```
オブジェクトのプロパティを何度もアクセスするとき、面倒になるため省略するため  

## プロパティの追加
オブジェクトは一度作成したものを変更できる。のちにプロパティ値を設定できる
```
const obj = {};
// `key`プロパティを追加する
obj.key = "value";

console.log(obj.key); // value
```

## オブジェクトの削除
```
const obj = {
	key1: "value1",
	key2: "value2"
};
// key1プロパティを削除
delete obj.key1;
// 出力
console.log(obj);
```

## プロパティの存在確認(in演算子)
存在していたらtrueが出力される
```
const obj = {
	key: undefined
};
//　もし`key`プロパティ持ってるならtrue

if ("key" in obj) {
	console.log("`key`オブジェクトは存在する");
```

## プロパティの存在確認(hasOwnProperty)
```
const obj = {
	key: undefined
};

if (obj.hasOwnProperty("key")) {
	console.log("`obj`は`key`プロパティを持っている)
```

##  Optional Chaining演算子(?.)
```
const book = undefined;
const title = book === null || book === undefined ? undefined : book.title;
console.log(title);  //nullやundefinedを入れてエラーを起こさないため
 
const book = { title: "サバイバルTypeScript" };
const title = book === null || book === undefined ? undefined : book.title;
console.log(title);
```
上記の方法では冗長になる。ここでOptionalChaining演算子(?.)を使う  
```
const book = undefined;
const title = book?.title;  //?.がOptionalChaining
//                ^^オプショナルチェーン
console.log(title);
 
const book = { title: "サバイバルTypeScript" };
const title = book?.title;
console.log(title);
```
つまり、空にアクセスした際にundefinedを出力させるようにした。  

## toStringメソッド
toStringメソッドは、オブジェクトを文字列化させるものである。Stringコントラクタ関数とどう言う関係？  
``String()``では``toString``を呼び出しているため、同じ結果になる。
```
const obj = { key: "value" };
console.log(obj.toString()); // => "[object Object]"
// `String`コンストラクタ関数は`toString`メソッドを呼んでいる
console.log(String(obj)); // => "[object Object]"
```

## Objectのプロパティは文字列になる
```
const obj = {};
const keyObject1 = { a: 1 };
const keyObject2 = { b: 2 };
// どちらも同じプロパティ名（"[object Object]"）に代入している
obj[keyObject1] = "1";
obj[keyObject2] = "2";
console.log(obj); //  { "[object Object]": "2" }
```

## オブジェクトの列挙
Object.keys: オブジェクトのプロパティ名の配列にして返す  
Object.values: オブジェクトの値に配列にして返す  
Object.entries: プロパティ名と値を配列する  

```
const obj = {
	"one": 1,
	"two": 2,
	"three": 3
};

console.log(Object.keys(obj)); // => ["one", "two", "three"]
console.log(Object.values(obj)); // => [1, 2, 3]
console.log(Object.entries(obj)); // => [["one": 1], ["two": 2], ["three": 3]]
```

forEach文を使うことで列挙できる
```
const obj = {
	"one": 1,
	"two": 2,
	"three": 3
};
const keys = Object.keys(obj);
keys.forEach(key => {
	console.log(key)
});
```

## Objectのmergeと複製
```
const obj = Object.assign(target, ...sources);
```

空オブジェクト{}に``objectA``と``objectB``をmergeする
```
const objectA = { a: "a" };
const objectB = { b: "b" };
const merge = Object.assign({}, objectA, objectB);
console.log(merge); // { a: "a", b: "b" }
```

##  Objectのspread構文
```
const ObjectA = { a: "a" };
const ObjectB = { b: "b" };
const merge = {
	...ObjectA,
	...ObjectB 
};

console.log(merge); // { a: "a", b: "b" }
```

