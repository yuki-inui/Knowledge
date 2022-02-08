## Map/Set

## Map

### Mapの作成
newをすることで作成ができる
```
const map = new Map();
console.log(map.size); // => 0
```

```
const map = new Map([[key1, value1], [key2, value2]]);
//2つのエントリーで初期化されている
console.log(map.size); // => 2
```

### 要素の追加と取り出し
-1 map.setは追加
-2 map.getは内容を確認
-3 map.setでは同一keyで複数追加すると、上書きされる
-4 map.delete はkeyを削除すると、それのプロパティを削除する

```
const map = new Map();
map.set("key1", "value1");
console.log(map.size); // => 1
console.log(map.get("key1"); // => "value1"
map.set("key1", "value2");
console.log(map.size); // => 1
console.log(map.get("key1") // => 2
```

### Mapの反復試行
```
const map = new Map([["key1", "value1"], ["key2", "value2"]]);
const result = [];

map.forEach((value, key) => {
	result.push(`${key}: ${value}`);
});

console.log(result); // => ["key1:value1","key2:value2"] 
```

keysメソッドはマップが持つすべての要素のキーを挿入順に並べたIteratorオブジェクトを返します。   
これらの返り値はIteratorオブジェクトであって配列ではありません。  
for...of文で反復処理を行ったり  
Array.fromメソッドに渡して配列に変換して   

```
const map = new Map([["key1, value1"], ["key2", "value2"]]);
const keys = [];

//keysメソッドの返り値(Iterator)を反復処理する
for (const key of map.keys()) {
	keys.push(key);
};
console.log(keys);

//配列から作成
const keysArray = Array.from(map.keys());
console.log(keysArray); // => ["key1","key2"]
```

### マップとしてのObjectとMap

