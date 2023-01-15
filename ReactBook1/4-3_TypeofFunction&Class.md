関数の型定義
---
Typescriptでは戻り値は型推論が有効であれば省略できるが、``引数の型は必ず指定しなければいけない。``
```
//statement
function add(n: number, m: number){
  return n + m;
}
console.log(add(3, 4));   // 7

//expression
const add = function(n: number, m: number): number {
  return n + m;
};
console.log(add(5, 9));  // 14

//arrow function
const add = (n: number, m: number): number => n + m;
const Hello = (): void => {
  console.log('Hello');
};

console.log(add(4, 6)); // 10
Hello(); //Hello
```
何も返さない関数の戻り値は``void``になる。   
以上が引数と戻り値を別に定義する手法である。   

```
//collable object
interface NumOp {
  (n: number, m: number): number;
}

const add: NumOp = function(n, m){
  return n + m;
};

const substruct :NumOp = (n, m) => n - m;
console.log(add(4, 5));
console.log(substruct(5, 3));

//in-line
const add: (n: number, m: number)  => number = function(n, m){
  return n + m;
};

const subtract: (n: number, m: number) => number = (n, m) => n - m;
```
