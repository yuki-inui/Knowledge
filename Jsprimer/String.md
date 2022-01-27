## 文字列の分解と結合
```
const string = "赤・青・緑".split("・");
console.log(string); // ["赤", "青", "緑"]
```

```
const str = "赤・青・緑".split("・").join("、");
console.log(str); // => "赤、青、緑"
```
splitで文字列にして  
joinで"、"を入れる  

```

