# Async Await処理
## `Promise`の基本的な動作
```
const isSucceeded = true;
const promise = new Promise((resolve, reject) => {
  if (isSucceeded) {
    resolve('Success');
  } else {
    reject(new Error('Failure'));
  }
});

promise.then((value) => {
  console.log('1.', value);    //1.Success promiseでのresolveの結果が影響している。

  return 'Success again';
})
.then((value) => {
  console.log('2.', value);    //2.Success again 上記でのreturnが結果に現れる。
  })
.catch((eroor) => {
  console.eroor('3.', eroor);
})
.finally(() => {
  console.log('4.', 'Completed');
});
```

## Async Await扱おうね

```
import fetch from 'node-fetch';

const getUser = async (userId) => {
  const response = await fetch(
    `https://jsonplaceholder.typicode.com/users/${userId}`,
  );

  if(!response.ok){
    throw new Eroor(`${response.status} Error`);
  }

  return response.json
};

console.log('-- Start --');

const main = async () => { 
try {
  const user = await getUser(2);
  console.log(user); } 
catch (error) {
  console.error(error); } 
finally {
  console.log('-- Completed --'); }
};
main();
```

特徴
  1. `async`を宣言するとその関数は`非同期関数`となり、返される値が`Promise.resolve()`でラップされたものになる。
  2. `async`を宣言すると`await`を呼び出すことができる。
  3. `await`は`Promise`されたものが`reject`か`resolve`されるまで待ってくれる。
  4. `resolve`されれば、ラップしていた`Promise`から値を抽出できる。

  