## 型アサーションと型キャスト
```
> const n = 123;
> const s1 = String(n);
> console.log(typeof s1); string

> const s2 = n as string;
[eval].ts:4:12 - error TS2352: Conversion of type 'number' to type 'string' may be a mistake because neither type sufficiently overlaps with the other. If this was intentional, convert the expression
to 'unknown' first.
```
`型キャスト`は、異なるデータ型の値を任意の型にコンバートするもの   
`型アサーション`はあくまでコンパイラによる型の解釈が変わるだけであって、実際の値 が変化するわけじゃ   
```
T as (U extends T) または (T extends U) as U
```
はTがUのサブタイプ、UがTのサブタイプである   
s2はできない。　　　
基本的に型アサーションは最終手段   

## 型ガードでスマートに
```
const foo: unknown = '1,2,3,4';
if (typeof foo === 'string') { console.log(foo.split(','));
}
console.log(foo.split(',')); //compileerror!
```
*typeof によって string 型だと判断されたブロック内*では、変数 foo に string のプロトタイプメソッdドである split() が使えてる。　　　
　このようにスコープ内を保証するチェックを行う式を*型ガード*という   




