## 関数とthis

Thisの参照先は次の条件によって変化する
1. 実行コンテキストにおける**this**
2. コントラクタにおける**this**
3. 関数とメソッドにおける**this**
4. Arrow Functionにおける**this**

## 実行コンテキストにおけるthis

### スクリプトにおけるthis
```
<script>
//実行コンテキストは"script"
console.log(this) // => window
</script>
```
ブラウザでは、script要素のtype属性を指定していない場合は、実行コンテキストが"Script"として実行されます。 このscript要素の直下に書いたthisはグローバルオブジェクトであるwindowオブジェクトとなります。  

### モジュールにおけるthis
```
<script type ="module">
//　実行コンテキストは"Module"
console.log(this) // => undefined
</script>
```
ブラウザで、script要素にtype="module"属性がついた場合は、実行コンテキストが"Module"として実行されます。 このscript要素の直下に書いたthisはundefinedとなります。   

## 関数とメソッドにおけるthis

## メソッドの種類
オブジェクトのプロパティが関数である場合、それを**メソッド**と言う。  
一般的にメソッドを含んだものを**関数**という。  

```
const obj = {
    // `function`キーワードを使ったメソッド
    method1: function() {
    },
    // Arrow Functionを使ったメソッド
    method2: () => {
    }
};
```

メソッドには短縮記法がある  
```
const obj = {
    // メソッドの短縮記法で定義したメソッド
    method() {
    }
};
obj.method();
```

## Arrow Functionメソッドにおけるthis


