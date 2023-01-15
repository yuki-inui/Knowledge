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
前者は```呼び出し可能オブジェクトを定義```して、関数式として使っている。   


Typescriptでのクラスの扱い
---

```
class Rectangle {
  readonly name = 'rectangle'; 
  sideA: number;
  sideB: number;

constructor(sideA: number, sideB: number) { 
  this.sideA = sideA;
  this.sideB = sideB;
 }
getArea = (): number => this.sideA * this.sideB;
}
```
``プロパティ初期化子(Property Initializer)``はコンストラクタに引数がないクラスは、インスタンスの初期化だけで済ます。   

- ``readonly`` : メンバー変数を変更不可にできる。  
- ``public`` : 自クラス、子クラス、インスタンスからアクセス可能。デフォルトではすべてpublicになる。
- ``protected`` : 自クラス、子クラスからアクセス可能。インスタンスからは不可。
- ``private`` : 自クラスから可能。子クラス、インスタンスからは不可。

``継承より合成``現在のオブジェクト指向においてのトレンドである。  

```
class Square extends  Rectangle {
  readonly name = 'square';
  side: number;

  constructor(side: number){
    super(side, side);
  }
}

class Square {
  readonly name = 'square'; 
  side: number;

  constructor(side: number) {
     this.side = side;
}
getArea = (): number => new Rectangle(this.side, this.side).getArea();
 }
 ```

継承では、暗黙の内にReactangleのクラス、sideAとsideBを継承しているため、バグになりかねない。  
また、getArea()は親クラスに大きく依存しているため、不用意に変更ができない。  

合成においてはReactangleクラスをただの独立した部品として扱っている。そのため内部について知る必要がない。  

