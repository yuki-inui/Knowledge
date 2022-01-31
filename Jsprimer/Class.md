## クラス

### クラスの定義
クラスを定義するには**Class**構文を使います。宣言の方式には２つある。  
クラス宣言文とクラス式である。  

class クラス名{} 構造  
クラスには必ずconstructorメソッドである。

```
class MyClass {
    constructor() {
        // コンストラクタ関数の処理
        // インスタンス化されるときに自動的に呼び出される
    }
}
```
もう一つの宣言方式はクラス式として定義する。  
```
const MyClass = class MyClass {
    constructor() {}
};

const AnonymousClass = class {
    constructor() {}
};
```

### クラスのインスタンス化
クラスはnew演算子でインスタンスであるオブジェクトを作成できます。  
class構文で定義したクラスからインスタンスを作成することをインスタンス化と呼ぶ。  
あるインスタンスが指定したクラスから作成されたものかを判定するにはinstanceof演算子が利用できます。  

```
class MyClass {
}
// `MyClass`をインスタンス化する
const myclass = new Myclass();
//　毎回新しいインスタンス（オブジェクト）を作成
const myClassAnother = new MyClass();
// それぞれのインスタンスは異なるオブジェクト
console.log(myClass === myClassAnother); // => false
// クラスのインスタンスかどうかは`instanceof`演算子で判定できる
console.log(myClass instanceof MyClass); // => true
console.log(myClassAnother instanceof MyClass); // => true
```

クラスではインスタンスの初期化処理をコンストラクタ関数で行います。  
new演算子でインスタンス化する際に自動的に呼び出されます。  
```
class Point {
    // コンストラクタ関数の仮引数として`x`と`y`を定義
    constructor(x, y) {
        // コンストラクタ関数における`this`はインスタンスを示すオブジェクト
        // インスタンスの`x`と`y`プロパティにそれぞれ値を設定する
        this.x = x;
        this.y = y;
    }
}
```

```
class Point {
	// 2. コンストラクタ関数の仮引数として`x`には`3`、`y`には`4`が渡る
	constructor(x, y) {
		//3. インスタンス(`this`)の`x`と`y`プロパティにそれぞれ値を設定する
        this.x = x;
	this.y = y;
	// コンストラクタではreturn文は書かない
    }
}

// 1. コンストラクタを`new`演算子で引数とともに呼び出す
const point = new Point(3, 4);
// 4. `Point`のインスタンスである`point`の`x`と`y`プロパティには初期化された値が入る
console.log(point.x); // => 3
console.log(point.y); // => 4
```

一方、クラスは通常の関数として呼ぶことができません。 これは、クラスのコンストラクタはインスタンス（this）を初期化する場所であり、通常の関数とは役割が異なるためです。   

## クラスのプロトタイプメソッドの定義

