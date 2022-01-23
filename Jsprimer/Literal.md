```
console.log(typeof true);   //"boolean"//  
console.log(typeof 54);    //"number"//  
console.log(typeof "Js");  //"string"//  
console.log(typeof Symbol("シンボル"));  //"symbol"//  
console.log(typeof undefined); //"undefined"//  
console.log(typeof null);  //"object"//  
console.log(typeof ["配列"]);  //"object"//  
console.log(typeof { "key": "value" });  //"object"//   
```　　　

## リテラル
### 文字列のルール    
```
console.log("文字列");  //"文字列"
console.log('文字列');  //"文字列"
console.log(`文字列`);  //"文字列"
```
出力は"" で表される。   
   
### シングルクオートとバッククオート
```
`8 o\`clock`; => "8 o`clock"
```
文字列のなかに同じものがあると、バックスラッシュ(\)でくくる   

###　テンプレートリテラル
```
const str = "Javascript";
console.log(`こちらは${str}です); //"こちらはJavascriptです"   

`This is \`code\``;  //"This is `code`" 
```

### オブジェクトリテラル
```
const obj = {
	"key": "value"
};

//ドット記法
console.log(obj.key); // => "value"
//ブラケット記法
console.log(obj["key"]); // =>"value"
```

### 配列リテラル
```
const emptyArray = []; //空の配列を作成
const Array = [index1, index2]; //値を持った配列を作成
```




