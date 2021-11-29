# 配列の反復処理

- map() 配列を任意の新しいものに出力する
- filter() 適合する配列を新しく出力する
- find() 適合するもののうち**最初**の数字を出力する
- findIndex() 適合するもののうち最初のインデックスを出力する
- every() 与えられた要素が全て適合するか真偽値で出力する
- some()  与えられた要素の中、一つでも適合すれば真を出すもの

const　arr　=　[1,2,3,4,5,6,7,8,9];<br>

console.log(arr.map((n) => n * 2));<br>
console.log(arr.filter((n)=>n%3===0));<br>
console.log(arr.find((n) => n > 4));<br>
console.log(arr.findIndex((n) => n > 4));<br>
console.log(arr.every((n) => n !== 0));<br>
console.log(arr.some((n) => n >= 10));<br>

`const arr = [1,2,3,4,5];`<br>
`console.log(arr.reduce((n, m) => n + m)); // 15`<br>
`console.log(arr.sort((n,m)=>n>m?-1:1)); //[5,4,3,2,1]`<br>

