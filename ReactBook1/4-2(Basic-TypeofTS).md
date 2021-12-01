型アノテーション
---
value:Type で表される   
example...  let n: number =3;   

リテラル型
---
```
> let Mary: 'Cat' | 'Dog' | 'Rabbit' = 'Cat'; > Mary = 'Rabbit';
> Mary = 'Parrot';
[eval].ts:5:1 - error TS2322: Type '"Parrot"' is not assignable to type '"Cat" | "Dog" | "Rabbit"'.
```