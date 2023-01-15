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