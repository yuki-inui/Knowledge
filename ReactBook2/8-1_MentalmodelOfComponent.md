Reactは`Component`という独立したパーツを使うことで、アプリケーションを作る。   

Reactは仮想DOMをリアルなDOMにレンダリングすることで、アプリケーションとして動作する。   

仮想DOMを構成するのが`ReactElements`   
 `ReactElements`は`Component`を任意のpropでコールするための実行リンクである。  

`Component`はJavascriptで例えるといい   
　`props`を引数として受け取り、戻り値として`ReactElements`を返す関数   
　`ReactElements`がその`Components`のレンダリングの結果になる。 
　関数と違うところは、個々を「状態」として保つことができる。   

この状態は、仮想DOMの差分検出処理エンジンによって`ReactElements`ごとに状態を保持する空間が生成される。この空間を`state`と呼ぶ。   

`state`と`prop`が同じである限り`ReactElements`は変わることのない。   
しかし、片方もしくは両方変更されると、`ReactElements`も変更される。   
よって、レンダリングに変更がされるかをみるには、`prop`と`state`を見ればいい。  

差分検出処理エンジンは仮想DOMの`ReactElements`を監視しているため`state``prop`  
の差分を検出すると、再度レンダリングを行なってくれる。   

親が変わると、子が代わり、また孫も変わる。  

