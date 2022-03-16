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
| 正規表現の仕方 | 説明 |
| -- | -- |
| 正規表現 | ソースコードのロード時に判定をする。|  
| "RegExp"コンストラクタ| RegExpコンストラクタを呼び出す時に判定をする。 |  

```
// ３つの連続するスペースなどにマッチするやつ
const pattern = /\s{3}/;
```
正規表現リテラルは動的に連続する回数を変更できない。  

```
const spaceCount = 3;
// `/\s{3}/`の正規表現を文字列から作成する
// "\"がエスケープ文字であるため、"\"自身を文字列として書くには、"\\"のように2つ書く
const pattern = new RegExp(`\\s{${spaceCount}}`);
```
RegExpでは特殊文字のエスケープが必要になるため面倒。  


## 正規表現の検索
正規表現による検索は、正規表現オブジェクトと対応したStringオブジェクトまたはRegExpオブジェクトのメソッドを利用します。  

## 正規表現いよるインデックスの取得
Stringの``indexOf``メソッドの正規表現であるStringの``search``がある。  
searchメソッドは、マッチした正規表現のインデックスを返す。なければ、−１を返す。  

1. String#search(/パターン/): 指定された正規表現のパターンにマッチした箇所のインデックスを返す  

```
const str = "ABC123EFG";
const searchPattern = /\d{3}/;
console.log(str.search(searchPattern)); // => 3
```
``\d``は、１文字の数字(1から9)にマッチする特殊文字である。  

## 正規表現によるマッチした文字列の取得

## マッチした文字列の取得
matchメソッドは、正規表現/パターン/が”文字列”にマッチすると返す。　ないと``null``を返す

```
"文字列".match(/パターン/);
console.log("文字列".match(/マッチしないパターン/)); // => null
```

matchメソッドに``g``フラグなし(g:マッチする文字列を全部繰り返す)の場合は最初だけを返して終わる。  
この結果には``index``プロパティと``input``プロパティを持った特殊な配列になる。  
indexプロパティにはマッチした文字列の先頭のインデックスが、inputプロパティには検索対象となった文字列全体が含まれています。　　

```
const str = "ABC あいう DE えお";
const alphabetsPattern = /[a-zA-Z]+/;
// gフラグなしでは、最初の結果のみを含んだ特殊な配列を返す
const results = str.match(alphabetsPattern);
console.log(results.length); // => 1
// マッチした文字列はインデックスでアクセスできる
console.log(results[0]); // => "ABC"
// マッチした文字列の先頭のインデックス
console.log(results.index); // => 0
// 検索対象となった文字列全体
console.log(results.input); // => "ABC あいう DE えお"    連続した文字列を１つとして見ている。
```
``/[a-zA-Z]+/``はaからZのうち１つ以上連続してるやつにマッチする。  

matchメソッドに``g``があればマッチした全ての文字列を返す。  
``/[a-zA-Z]+/g``
  
```
const str = "ABC あいう DE えお";
const alphabetsPattern = /[a-zA-Z]+/g;
// gフラグありでは、すべての検索結果を含む配列を返す
const resultsWithG = str.match(alphabetsPattern);
console.log(resultsWithG.length); // => 2
console.log(resultsWithG[0]); // => "ABC"
console.log(resultsWithG[1]); // => "DE"
// indexとinputはgフラグありの場合は追加されない
console.log(resultsWithG.index); // => undefined
console.log(resultsWithG.input); // => undefined
```
``index``と``input``はフラグ付きでは追加されない。  

matchメソッドの結果  
1. マッチしない場合は``null``を返す  
2. マッチした場合は、マッチした文字列を含んだ特殊な配列返す。  
3. 正規表現``g``がある場合は全ての結果を返す。  

ES2020では、正規表現のgフラグを使った繰り返しマッチする場合においても、それぞれマッチした文字列ごとの情報を得るためのStringのmatchAllが追加されています。 matchAllメソッドは、マッチした結果をIteratorで返します  

```
const str = "ABC あいう DE えお";
const alphabetsPattern = /[a-zA-Z]+/g;
// matchAllはIteratorを返す
const matchesIterator = str.matchAll(alphabetsPattern);
for (const match of matchesIterator) {
    // マッチした要素ごとの情報を含んでいる
    console.log(`match: "${match[0]}", index: ${match.index}, input: "${match.input}"`);
}
// 次の順番でコンソールに出力される
// match: "ABC", index: 0, input: "ABC あいう DE えお"
// match: "DE", index: 8, input: "ABC あいう DE えお"
```

### マッチした文字列の一部を取得
``match``と``matchAll``はどちらもキャプチャリングに対応してる。   
キャプチャリングは``/パターン１(パターン2)/``で表現される。  

```
const [マッチした全体の文字列, キャプチャ1, キャプチャ2] = 文字列.match(/パターン(キャプチャ1)と(キャプチャ2)/);
```

```
// "ECMAScript (数字+)"にマッチするが、欲しい文字列は数字の部分のみ
const pattern = /ECMAScript (\d+)/;
// 返り値は0番目がマッチした全体、1番目がキャプチャの1番目というように対応している
// [マッチした全部の文字列, キャプチャの1番目, キャプチャの2番目 ....]
const [all, capture1] = "ECMAScript 6".match(pattern);
console.log(all); // => "ECMAScript 6"
console.log(capture1); // => "6"
```

正規表現　``g``を使いマッチしたやつを個別でピックする方法  
```
// "ES(数字+)"にマッチするが、欲しい文字列は数字の部分のみ
const pattern = /ES(\d+)/g;
// iterator
const matchesIterator = "ES2015,ES2016,ES2017".matchAll(pattern);
for(const match of matchIterator) {
	// マッチした要素ごとの情報を含んでいる
    // 0番目はマッチした文字列全体、1番目がキャプチャの1番目である数字
    console.log(`match: "${match[0]}", capture1: ${match[1]}, index: ${match.index}, input: "${match.input}"`);
}
// 次の順番でコンソールに出力される
// match: "ES2015", capture1: 2015, index: 0, input: "ES2015、ES2016、ES2017"
// match: "ES2016", capture1: 2016, index: 7, input: "ES2015、ES2016、ES2017"
// match: "ES2017", capture1: 2017, index: 14, input: "ES2015、ES2016、ES2017"
```

## 文字列の置換/削除

Stringの``replace``メソッドで文字列を削除したり置換したりできる
```
文字列.replace("検索文字列", "置換文字列");
文字列.replace(/パターン/, "置換文字列");
```

```
const str = "文字列";
//"文字"を空文字に置き換える
const newstr = replace("文字", "");
console.log(newstr); // "列"
```

``reduce``メソッドは正規表現にも対応している
```
const str = "にわにはにわにわとりがいる";
//文字列を指定した場合は、最初に一致したものが変換される
console.log(str.reduce("にわ", "niwa")); // => "niwaにはにわにわとりがいる"
//`g`フラグなしに正規表現で表したら最初に一致したものだけ置換される
console.log(str.reduce(/にわ/, "niwa")); // => "niwaにはにわにわとりがいる"
// `g`フラグありなら全て起きかわる
console.log(str.reduce(/にわ/g, "niwa")); // "niwaにはniwaniwaとりがいる"
```
reduce("文字列", ●) は最初だけ入れ替わる  
reduce(/文字列/, ●)　は最初だけ入れ替わる  
reduce(/文字列/g, ●)　は全て  

文字列から検索文字列全て置換するものは``replaceAll``  
| 置換方法 | 説明 |
| -- | -- |
| ``replaceAll`` | 文字列全てを置換する("?"などの特殊文字も可) |
| ``replace+`g`付き | "?"などの特殊文字不可 |


