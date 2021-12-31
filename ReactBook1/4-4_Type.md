# Type
## 共用体型と交差型
---
共用体(AまたはB)
```
let id: number | string = 208239;
>id
>208239
id = 'a6ba7fb9-8435-4226-804e-387f3d2e53a7'; >id
>'a6ba7fb9-8435-4226-804e-387f3d2e53a7'
```

```
typeA={
foo: number; bar?: string;
};
type B = { foo: string };
type C = { bar: string };
type D = { baz: boolean };

typeAorB= A | B; //{foo:number | string; bar?:string}
typeAorC= A | C; //{foo:number;bar?:string} or {bar:string}
typeAorD= A | D; //{foo:number;bar?:string} or {baz:boolean}
```

交差型(AかつB)
---
```
type A = { foo: number };
type B = { bar: string }; 
typeC={
foo?: number;
baz: boolean; 
};
type AnB = A & B; //{ foo: number, bar: string } 
type AnC = A & C; //{ foo: number, baz: boolean} 
type CnAorB = C & (A | B);
// { foo: number, baz: boolean } or { foo?: number, bar: string, baz: boolean }
```
省略と必須が交差していれば、必須が選択される。   


