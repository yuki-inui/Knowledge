## 文字列へのアクセス
```
const str = "文字列";
console.log(str[0]); // "文"
console.log(str[1]); //"字"
console.log(str[2]); //"列"
```

## 文字列の分解と結合
```
const string = "赤・青・緑".split("・");
console.log(string); // ["赤", "青", "緑"]
```

```
const str = "赤・青・緑".split("・").join("、");
console.log(str); // => "赤、青、緑"
```
splitで文字列にして  
joinで"、"を入れる  



## 文字列の取得
```
const str = "ABCDE";
console.log(str.slice(1)); // => "BCDE"
console.log(str.slice(1, 5)); // => "BCDE"
// マイナスを指定すると後ろからの位置となる
console.log(str.slice(-1)); // => "E"
// インデックスが1から4の範囲を取り出す
console.log(str.slice(1, 4)); // => "BCD"
// 第一引数 > 第二引数の場合、常に空文字列を返す
console.log(str.slice(4, 1)); // => ""
```

## 文字列の検索
-1 ``文字列.indexof("検索文字列")``: 先頭から検索し、指定された文字列が最初に現れたインデックスを返す  
-2 ``文字列.lastIndexof("検索文字列")``: 末尾から検索し、指定された文字列が最初に現れたインデックスを返す  
検索文字列に"未知の文字"があれば−１を返す  

```
// 検索対象となる文字列
const str = "にわにはにわにわとりがいる";
// indexOfは先頭から検索しインデックスを返す - "**にわ**にはにわにわとりがいる"
// "にわ"の先頭のインデックスを返すため 0 となる
console.log(str.indexOf("にわ")); // => 0
// lastIndexOfは末尾から検索しインデックスを返す- "にわにはにわ**にわ**とりがいる"
console.log(str.lastIndexOf("にわ")); // => 6
// 指定した文字列が見つからない場合は -1 を返す
console.log(str.indexOf("未知のキーワード")); // => -1
```

### 文字列にマッチした文字列の取得
```
const str = "Javascript";
const search = "script";
const index = str.indexOf(search);
if ( index !== -1) {
	console.log('${search}は見つかりました');
}else {
	console.log('${search}はみつかりません');
}
```

### 真偽値の取得
-1 ``string.startsWith("moji");`` // mojiの最初についているか
-2 ``string.endsWith("moji");`` //　mojiのエンドにあるか
-3 ``string.includes("moji");`` // 含んでいるか

```
// 検索対象となる文字列
const str = "にわにはにわにわとりがいる";
// startsWith - 検索文字列が先頭ならtrue
console.log(str.startsWith("にわ")); // => true
console.log(str.startsWith("いる")); // => false
// endsWith - 検索文字列が末尾ならtrue
console.log(str.endsWith("にわ")); // => false
console.log(str.endsWith("いる")); // => true
// includes - 検索文字列が含まれるならtrue
console.log(str.includes("にわ")); // => true
console.log(str.includes("いる")); // => true
```

## 正規表現オブジェクト
正規表現は柔軟性のある検索に特化しているもの。  
正規表現には２つの表現方法がある。

1. 正規表現リテラル  
2. "RegExp"コンストラクタ  

```
// 正規表現リテラルで正規表現オブジェクトを作成
const patternA = /パターン/フラグ;
// `RegExp`コンストラクタで正規表現オブジェクトを作成
const patternB = new RegExp("パターン文字列", "フラグ");
```

### 正規表現リテラルと"RegExp"コンストラクタの違い

| -- | -- |
| 正規表現 | ソースコードのロード時に判定をする。|  
| "RegExp"コンストラクタ| RegExpコンストラクタを呼び出す時に判定をする。 |  




