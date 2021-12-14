# JSXの本質を理解する
    
JSXはJavascriptとXMLの組み合わせでできている。   
ECMAScript2015の構造拡張である。　　　

```
<button type="submit" autoFocus> 
  Click Here
</button>
```
変換前のJSXコード。    

```
React.createElement(
  'button',
  { type: 'submit', autoFocus: true },
  'Click Here' 
);
```
変換後のJavacsriptのコード    

JSXは`React.ceateElement`を前提にXMLのノードツリーを、Javacsript内で楽にかけるためのもの。   

```
{
type: 'button', 
props: {
  type: 'submit', 
  autoFocus: true, 
  children: 'Click Here',
  },
  key: null, 
  ref: null,
};
```

これによりJSXはJavascript　においては単なるオブジェクトを表現する式に還元するものである。   
特別な存在ではない。`*変数に代入* *狭義のオブジェクトのプロパティ* *引数の戻り値*にでもできる`   


# なぜReactは見た目とロジックが混在するのか

