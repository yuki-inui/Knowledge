# JSXの書き方

## JSXの基本的な文法
JSXは``React.createElement``のメソッドコールに対するシンタックスシュガーである。
また、``tsconfig.json``で``jsx``オプションを``react``にすると、  
JSXの記載は、``React.createElement(...)``のように変換される。  
であるため、JSXの記載においては、``React``のインポートが必要になる。  

しかし、**Typescript4.1**以降では``React17.0``以降で導入された、新たな変換方式で、  
``jsx``オプションを``react-jsx``にすることで、``React``のimportを省略できるよ。  


