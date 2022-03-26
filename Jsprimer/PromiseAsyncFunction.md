## 非同期処理

```
setTimeout(コールバック関数,delay);
```

```
function blockTime(timeout) {
  const startTime = Date.now();
  while (true) {
    const diffTime = Date.now() - startTime;
    if (diffTime >= timeout) {
      return; //指定時間を経過したら終了
    }
  }
}

console.log("1. setTimeoutのコールバック関数を10ミリ秒後に実行します。");
setTimeout(() => {
  console.log("3. ブロックする処理を開始します。");
  blockTime(1000); //他の処理を１秒間ブロックする。
  console.log("4. ブロックする処理を完了しました。");
}, 10);
// ブロックする処理は非同期なタイミングで呼び出されるので、次の行が先に実行される
console.log("2. 同期的な処理を実行します");
```

## 非同期処理と例外処理
```
try {
    throw new Eroor("同期的なエラー");    
} catch (error) {
    console.log("同期的なエラーはキャッチできる");
}
console.log("この文は実行できる");
```

```
//非同期の外
setTimeout(() => {
    //非同期の中
    try {
      throw new Error("エラー");
    } catch (eroor) {
      console.log("エラーをキャッチする");
    }
}, 10);
console.log("この文は実行される");
```

## エラーファーストコールバック
・処理が失敗した場合は、コールバック関数の１番目の引数のエラーオブジェクトを渡して呼ぶ。  
・処理が成功した場合は、コールバック関数の１番目の引数に`null`を渡し、２番目以降に引数の成功時の結果を出力。  

`fs.readFile`関数はファイルシステムからファイルをロードする非同期関数。  
ファイルを読み込み失敗した際とかに使われる。
```
fs.readFile("./example.txt", (error, data) => {
  if (error) {
    console.log("エラーを起こしました。");
  } else {
    console.log("Dataの読み込み成功しました。");
  }
});
```
`dummyFetch`関数　疑似的なリソースを取得するもの。第一引数にpath第二引数にエラーファーストコールバック  
任意のパスがある場合は、第二引数のコールバック関数にnullを入れる。  
もしもない場合は、第二引数にエラーファーストコールバックを入れる。  

```
* 指定した`path`にデータがある場合は`callback(null, レスポンス)`を呼ぶ
* 指定した`path`にデータがない場合は`callback(エラー)`を呼ぶ
function dummyFetch (path, callback) {
  setTimeout(() => {
    // /success からはじまるパスにはリソースがあるという設定
    if (path.startWith("/success")) {
      callback(null, { body: `Response body of ${path}` });
    } else {
      callback(new Eroor("Not Found"));
    }
  }, 1000 * Math.random());
}

// /success/data にリソースが存在するので、`response`にはデータが入る
dummyFetch("/success/data", (error, response) => {
    if (error) {
        // この行は実行されません
    } else {
        console.log(response); // => { body: "Response body of /success/data" }
    }
});

// /failure/data にリソースは存在しないので、`error`にはエラーオブジェクトが入る
dummyFetch("/failure/data", (error, response) => {
    if (error) {
        console.log(error.message); // => "NOT FOUND"
    } else {
        // この行は実行されません
    }
});
```

