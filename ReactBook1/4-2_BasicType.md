型アノテーション(Type Annotation)
---
``value: Type``で表されるもの。
型アノテーションによって静的に型つけられたものは、コンパイルチェックに用いられる。
不整合があればコンパイルエラーになる。   

データ配列の表し方は２種類ある。   
```
const numArr: number[] = [1, 2, 3];
const strArr: Array<string> = ['one', 'two', 'three'];
```
前者の表し方が推奨される。   

リテラル型
---
```
> let Mary: 'Cat' | 'Dog' | 'Rabbit' = 'Cat'; 
> Mary = 'Rabbit';
> Mary = 'Parrot';
[eval].ts:5:1 - error TS2322: Type '"Parrot"' is not assignable to type '"Cat" | "Dog" | "Rabbit"'.
```
