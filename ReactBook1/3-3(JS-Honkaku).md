# 本格関数型プログラミング
カリー化のと関数の部分適用
---

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

Curriedは nを引数とした上で「mを引数にとり n との積を返す関数」を返す関数　　

省略形で表すと   
const withMultiple = (n) => (m) => n * m;   
console.log(withMultiple(3)(5)); //15   

const triple = withMultiple(3);   
console.log(triple(5));   





