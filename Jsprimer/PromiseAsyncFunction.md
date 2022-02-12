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
