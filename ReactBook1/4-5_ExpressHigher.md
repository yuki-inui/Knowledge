型表現に使われる演算子
---
## `typeof`演算子
渡された値の``型の名前``を文字列に返す   
型のコンテキストで用いると変数から型を抽出してくれる       

  ```
console.log(typeof　100); //'number'
const arr = [1, 2, 3];
console.log(typeof　arr); //'object'
type NumArr = typeof arr;
const val: NumArr = [4, 5, 6];
constval2:NumArr=['foo','bar','baz']; //compileerror!
```
NumArrは`number[]`であるため`string[]`はエラーになる。これは型推論   

## `in`演算子    
指定した値がオブジェクトのキーとして存在するか どうかの真偽値を返したりする。   
`for...in` 文ではオブジェクトからインクリメンタルにキーを抽出する のに使われる。   
型コンテキストでは、列挙された型の中から各要素の型の値を抜き出して マップ型(Mapped Types)   

```
const obj={　a:　1,　b:　2,　c:　3};
console.log('a' in obj); // true
for(const key in obj){console.log(key);} //abc

type Fig = 'one' | 'two' | 'three'; 
type FigMap = { [k in Fig]?: number };
const figMap: FigMap = {
 one: 1,
 two: 2,
 three: 3, 
};
figMap.four=4; //compileerror!
```
## `keyof`演算子
型コンテキストでしか使われてない。型からキーをぬきだす。   

```
const permissions = {
 r: 0b100,
 w: 0b010,
 x: 0b001,
};
typePermsChar=keyoftypeofpermissions; //'r'|'w'|'x' 
const readable: PermsChar = 'r';
const writable: PermsChar = 'z'; // compile error!
```
typeofと合わせると、既存の型かたキーを抽出できる    




条件付き型とテンプレートリテラル型
---

## `extend`
```
const override = <T, U extends T>(obj1: T, obj2: U): T & U => ({ 
...obj1,
...obj2,
});

override({a: 1},{a: 24,b: 8}); //{a: 24,b: 8}
override({ a: 2 }, { x: 73 }); // compile error!
```
`extend`は関数`object()`は第二引数である`obj2`の型を定義をしている`U`  
は第一引数`obj1`の型`T`と同じか拡張したものでないといけない、というものを示すもの。

## 条件付き型
```
type User = { id: unknown };
type NewUser = User & { id: string }; 
type OldUser = User & { id: number }; 
type Book = { isbn: string };
type IdOf<T> = T extends User ? T['id'] : never;
type NewUserId = IdOf<NewUser>; //string typeOldUserId=IdOf<OldUser>; //number
type BookId = IdOf<Book>; // never
```

## `infer`
そのマッチング中に取得した型を出力にも利用できるよ。そ れには infer というキーワードを使う   
```
type Flatten<T> = T extends Array<infer U> ? U : T;
const num = 5;
const arr = [3, 6, 9]; 
typeA = Flatten<typeofarr>; //number
typeN = Flatten<typeofnum>; //number   
```
この例では型 T が何らかの型の配列だった場合、その配列の中身の型を infer U で型 U として 取得し、出力の型として使ってる。配列じゃなかった場合はそのままその型が出力される   

## `Template Literal Type`
```
type DateFormat = `${number}-${number}-${number}`; 
const date1: DateFormat = '2020-12-05';
const date2: DateFormat = 'Dec. 5, 2020'; //compileerror!
```

```
const tables = ['users', 'posts', 'comments'] as const; 
type Table = typeof tables[number];
type AllSelect = `SELECT * FROM ${Table}`;
type LimitSelect = `${AllSelect} LIMIT ${number}`;
const createQuery = (table: Table, limit?: number): AllSelect | LimitSelect => 
  limit ? `SELECT * FROM ${table} LIMIT ${limit}` as const
  : `SELECT * FROM ${table}` as const;

const query = createQuery('users', 20);
console.log(query);
```

## Pick<T,K> Omit<T,K>
Pick<T,K> ...... T から K が指定するキーのプロパティだけを抽出する   
Omit<T,K> ...... T から K が指定するキーのプロパティを省く   

```
type Todo = {
title: string; 
description: string; 
isDone: boolean;
};
type PickedTodo = Pick<Todo, 'title' | 'isDone'>; //{ title: string; isDone: boolean }
type OmittedTodo = Omit<Todo, 'description'>;  //{ title: string; isDone: boolean }
```

## Extract<T,K> Exclude<T,K>
Extract<T,U> ...... T から U の要素だけを抽出する   
Exclude<T,U> ...... T から U の要素を省く   

```
type Permission = 'r' | 'w' | 'x';
type RW1 = Extract<Permission, 'r' | 'w'>;
type RW2 = Exclude<Permission, 'x'>;
```

## NonNullable
NonNullable<T> ...... T から null と undefined を省く  
```
type T1 = NonNullable<string | number | undefined>; 
type T2 = NonNullable<number[] | null | undefined>;
const str: T1 = undefined; //compileerror!
const arr: T2 = null; // compile error!
```

## Record<K.T>
Record<K,T> ...... K の要素をキーとしプロパティ値の型を T としたオブジェクトの型を作成す
る   

```
type Animal = 'cat' | 'dog' | 'rabbit'; 
type AnimalNote = Record<Animal, string>;
const animalKanji: AnimalNote = { 
  cat: '猫',
  dog: '犬',
  rabbit: '兎',
};
```

関数のオーバーロード
---
```
public class Main {
public static void main(String args[]) {
greet();
    greet("Usagi");
  }

  static void greet() { 
    System.out.println("Hello!");
  }
  static void greet(String name) { 
   System.out.println("Hi, " + name + "!");
  } 
}
```

