# 本格関数型プログラミング
カリー化のと関数の部分適用
---
```
// Pre-curried     
{  
const multiply = (n, m) => n * m;  
console.log(multiply(2, 4));  

// Curried   
{   
const withMultiple = (n) => {    
  return(m)=>n*m;    
};    
console.log(withMultiple(2)(4)); //8     
}    

// Curried with double arrow     
{    
const withMultiple = (n) => (m) => n * m;      
console.log(withMultiple(2)(4)); //8     
}    
```
Curriedは nを引数とした上で「mを引数にとり n との積を返す関数」を返す関数　　

省略形で表すと   
```
const withMultiple = (n) => (m) => n * m;   
console.log(withMultiple(3)(5)); //15   

const triple = withMultiple(3);   
console.log(triple(5));   
```


# クロージャーについて
```
let count = 0;   
const increment = () => { return count += 1;   
};   
$ node    
 .load open-counter.js  
 increment(); 1  
 increment(); 2  
 count 2   
 ```
 このままではconstの値に依存することになり、グローバル変数がゆえ、にどこからでも改変が可能になる　　　
 
 ```
 $ node  
 const counter = (count = 0) => (adds = 1) => count += adds;   
 const increment = counter();`   
 increment(); 1   
 increment(2); 3
 ```
引数でもなくローカルの変数でもないものを`自由変数(Free Variable)`という   
ex)  count, adds　など   

 
``` 
 let frinedship;   
if (true) {          
const he = 'Kakeru';
const saveHim = () => {     
console.log(`${he} saved`); };      
}
```
このままではheがifを外れると、どこからも参照されなくなる。

ここで
```
const saveHim = () => {　　　　
console.log(`${he} saved`); };　　　　　　
 friendship=saveHim;　　　　　　　
}　　　　
friendship(); //Kakerusaved　
```　　

こうすることで参照をされる
