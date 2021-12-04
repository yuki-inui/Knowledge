# 関数宣言(statements)と関数式(expression)

関数宣言文<br>
function double (n) {  
  return n * 2;  
  }  
  
  
関数式  
const double = function (n) {  
  return n * 2;  
  };  
  
  最終的には関数式では代入を行なっているため、末尾にセミコロンがある
  

# アロー関数

const addOne = (n) => {<br>　
  return n + 1;　<br>
  };
  
省略して書いたら  
const addOne = n => n + 1;

引数が一つだけの場合は省略可能

# デフォルト引数
const raise = (n, m = 2) => n *** m;  
console.log(raise(2, 3));   //8<br>
console.log(raise(3));  

`n ** m` は nをm乗する関数である
また、(n, m = 2)で2乗は設定されているため、raise(3)では3^2が出力される

