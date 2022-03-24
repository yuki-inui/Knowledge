# 例外処理

## try...catch構文
``try...catch```構文の``try``で例外が発生すると、以降の処理がなされず、``catch``節が実行される。  
``try``節はエラーオブジェクトと共に実行される。  
``finally``は``try``でエラーが発生したかしなかったか関係なく、なされる。  

``catch``節と``finally``節のうち片方があれば、もう片方は省略されます。  
``finally``のみでできていれば、例外がキャッチされないため、``finally``節実行ごにエラー発生。  

```
// catch節のみ
try {
    undefinedFunction();
} catch (error) {
    console.error(error);
}
// finally節のみ
try {
    undefinedFunction();
} finally {
    console.log("この行は実行されます");
}
// finally節のみでは例外がキャッチされないため、この行は実行されません
```

## throw文

``throw``を使うと、ユーザーが例外を投げることができる。投げられた例外はcatch節のように引数のようにできる。

```
try {
    // 例外を投げる
    throw new Error("例外が投げられました");
} catch (error) {
    // catch節のスコープでerrorにアクセスできる
    console.log(error.message); // => "例外が投げられました"
}
```

## Error
``Error``オブジェクトのインスタンス``Error``を``new``して作成します。コンストラクタの第一引数には、エラーメッセージの文字列が入る。  
渡したエラーメッセージは``message``プロパティで参照できる。  

```
// 渡された数値が0以上ではない場合に例外を投げる関数
function assertPositiveNumber(num) {
    if (num < 0) {
        throw new Error(`${num} is not positive.`);
    }
}

try {
    // 0未満の値を渡しているので、関数が例外を投げる
    assertPositiveNumber(-1);
} catch (error) {
    console.log(error instanceof Error); // => true
    console.log(error.message); // => "-1 is not positive."
}
```


