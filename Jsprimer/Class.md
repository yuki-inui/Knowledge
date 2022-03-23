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

```
class Counter = {
	constructor() {
		this.count = 0;
	}
	// increment メソッドをクラスに定義する
	increment() {
		this.count++;
	}
}
const counterA = new Counter();
const counterB = new Counter();
// `counterA.increment()`のベースオブジェクトは`counterA`インスタンス
counterA.increment();
// 各インスタンスの持つプロパティ(状態)は異なる
console.log(counterA.count); // => 1
console.log(counterB.count); // => 0
```

プロトタイプメソッドは各インスタンスで共有される。  
```
class Counter {
    constructor() {
        this.count = 0;
    }
    increment() {
        this.count++;
    }
}
const counterA = new Counter();
const counterB = new Counter();
// 各インスタンスオブジェクトのメソッドは共有されている(同じ関数を参照している)
console.log(counterA.increment === counterB.increment); // => true
```

## classのインスタンスに対してメソッドを定義する
``class``構文のメソッド定義はインスタンス間で共有される。  
一方、クラスのインスタンスに対して、直接メソッドを定義する方法もあります。  

```
class Counter = {
	constructor() {
		this.count = 0;
		this.increment = () => {
			 // `this`は`constructor`メソッドにおける`this`（インスタンスオブジェクト）を参照する
			this.count++;
		};
	}
}
const counterA = new Counter();
const counterB = new Counter();
// `counterA.increment()`のベースオブジェクトは`counterA`インスタンス
counterA.increment();
// 各インスタンスの持つプロパティ(状態)は異なる
console.log(counterA.count); // => 1
console.log(counterB.count); // => 0
```

Arrow Function には静的に``this``が決まるため。メソッドにおけ``るthis``の参照先をインスタンスに固定できます。  
なぜならArrow Functionで定義したincrementメソッドはどのような呼び出し方をしても、必ずconstructorにおけるthisとなるためです。  
```
"use strict";
class ArrowClass {
    constructor() {
        // コンストラクタでの`this`は常にインスタンス
        this.method = () => {
            // Arrow Functionにおける`this`は静的に決まる
            // そのため`this`は常にインスタンスを参照する
            return this;
        };
    }
}
const instance = new ArrowClass();
const method = instance.method;
// 呼び出し方法（ベースオブジェクト）に依存しないため、`this`がインスタンスを参照する
console.log(method()); // => instance
```

## classのアクセッサプロパティの定義
クラスに対してメソッドを定義できますが、メソッドは``メソッド()``のように呼び出せる。  
プロパティの参照(getter),プロパティの代入(setter)時に呼び出さされる特殊なメソッドを定義できる。  
getter（get）には仮引数はありませんが、必ず値を返す必要がある。setter(set)はプロパティへ代入する値が入りますが、値を返す必要ない。  

次のコードでは、NumberWrapperクラスのvalueプロパティをアクセッサプロパティとして定義しています。  
 valueプロパティへアクセスした際にそれぞれ定義したgetterとsetterが呼ばれているのがわかります。  
 このアクセッサプロパティで実際に読み書きされているのは、NumberWrapperインスタンスの_valueプロパティとなります。  
```
const ClassWrapper = {
	constructor() {
		this._value = value;
	}
	//'_value' のプロパティを返すgetter
	get value() {
		console.log("getter");
		return this._value;
	}
	//'_value'プロパティに値を代入するsetter
	set value(newValue) {
		console.log("setter");
		this._value = newValue;
	}
}

const numberWrapper = new NumberWrapper(1);
// "getter"とコンソールに表示される
console.log(numberWrapper.value); // => 1
// "setter"とコンソールに表示される
numberWrapper.value = 42;
// "getter"とコンソールに表示される
console.log(numberWrapper.value); // => 42
```

[コラム]  
``value``のアクセッサプロパティで実際読み書きしてるのは、``_value``プロパティである。  
このように外から直接読み取って欲しくない場合は、''_''(アンダーバー)を使う。構文的意味はない。  

##  ``array.length``でアクセッサプロパティを再現
``array.length``をするとそれ以降の要素は削除される。以降に要素をいれても空が表示される。 

```
const array = [1, 2, 3, 4, 5];
// 要素数を減らすと、インデックス以降の要素が削除される
array.length = 2;
console.log(array.join(", ")); // => "1, 2"
// 要素数だけを増やしても、配列の中身は空要素が増えるだけ
array.length = 5;
console.log(array.join(", ")); // => "1, 2, , , "
```
この``length``プロパティを再現するため、``ArrayLike``が存在する。  
1. 現在要素数より小さな要素数が指定された場合、その要素数を変更し、配列の末尾の要素を削除する　　
2. 現在要素数より大きな要素数が指定された場合、その要素数だけを変更し、配列の実際の要素はそのままにする  

```
class ArrayLike {
	constructor(items = []) {
		this._items = items;
	}
	
	get items() {
		return this._items;
	}

	get length() {
		returnn this._items.length;
	}

	set length(newLength) {
		const currentItemLength = this.items.length;
		// 現在要素数より小さな`newLength`が指定された場合、指定した要素数となるように末尾を削除する
		if (newLength < currentItemLength) {
			this._items = this.items.slice(0, newLength);
		} else if (newLength > currentItemLength) {
			// 現在要素数より大きな`newLength`が指定された場合、指定した要素数となるように末尾に空要素を追加する
			this._items = this.items.concat(new Array(newLength - currentItemLength));
		}
	}
}

const arrayLike = new ArrayLike([1, 2, 3, 4, 5]);
// 要素数を減らすとインデックス以降の要素が削除される
arrayLike.length = 2;
console.log(arrayLike.items.join(", ")); // => "1, 2"
// 要素数を増やすと末尾に空要素が追加される
arrayLike.length = 5;
console.log(arrayLike.items.join(", ")); // => "1, 2, , , "
```

## 静的メソッド
インスタンスメソッドは、クラスをインスタンス化して利用する。 一方、クラスをインスタンス化せずに利用できる静的メソッド（クラスメソッド）staticだけ

```
class ArrayWrapper {
	constructor(array = []) {
		this.array = array;
	}
	
	// rest parametorとして要素をつける
	static of(...items) {
		return new ArrayWrapper(items);
	}

	get length() {
		return this.array.length;
	}
	
}

// 配列を引数として渡している
const arrayWrapperA = new ArrayWrapper([1, 2, 3]);
// 要素を引数として渡している
const arrayWrapperB = ArrayWrapper.of(1, 2, 3);
console.log(arrayWrapperA.length); // => 3
console.log(arrayWrapperB.length); // => 3
```

クラスの静的メソッドにおけるthisは、そのクラス自身を参照します。 そのため、先ほどのコードはnew ArrayWrapperの代わりにnew thisと書くこともできます。  
```
class ArrayWrapper {
    constructor(array = []) {
        this.array = array;
    }

    static of(...items) {
        // `this`は`ArrayWrapper`を参照する
        return new this(items);
    }

    get length() {
        return this.array.length;
    }
}

const arrayWrapper = ArrayWrapper.of(1, 2, 3);
console.log(arrayWrapper.length); // => 3
```

## 2つのインスタンスメソッドの定義
インスタンスメソッドには２つの定義がある。``class``を使ったプロトタイプのメソッド。インスタンスメソッドに対する定義が存在する。  
これらの2つの方法を同時に使い、1つのクラスに同じ名前でメソッドを2つ定義した場合はどうなるでしょうか？  

```
class ConflictClass {
    constructor() {
        // インスタンスオブジェクトに`method`を定義
        this.method = () => {
            console.log("インスタンスオブジェクトのメソッド");
        };
    }


	// クラスのプロトタイプメソッドとして`method`を定義
    method() {
        console.log("プロトタイプのメソッド");
    }
}

const conflict = new ConflictClass();
conflict.method(); // どちらの`method`が呼び出される？
```

この場合はインスタンスオブジェクトで定義したものが出される。  
削除するとプロトタイプが呼び出される。  

```
class ConflictClass {
    constructor() {
        this.method = () => {
            console.log("インスタンスオブジェクトのメソッド");
        };
    }

    method() {
        console.log("プロトタイプメソッド");
    }
}

const conflict = new ConflictClass();
conflict.method(); // "インスタンスオブジェクトのメソッド"
// インスタンスの`method`プロパティを削除
delete conflict.method;
conflict.method(); // "プロトタイプメソッド"
```

・ プロトタイプメソッドとインスタンスオブジェクトのメソッドは上書きされずにどちらも定義されている  
・ インスタンスオブジェクトのメソッドがプロトタイプオブジェクトのメソッドよりも優先して呼ばれている  

## 継承
```
class Child extend Parent [
	}
```

## super
``extend``で参照した子クラスは親クラスを``super``を用いて参照する。  

```
//　親クラス
class Parent {
	constructor(...args) {
		console.log("Parentコンストラクタの処理", ...args);
	}
}

class Child extend Parent {
	constructor(...args) {
		//Parentコンストラくたを呼び出す
		super(...args);
		console.log("Childコンストラクタの処理", ...args);
	}
}

const child = new Child("引数1", "引数2");
// "Parentコンストラクタの処理", "引数1", "引数2"
// "Childコンストラクタの処理", "引数1", "引数2"
```


