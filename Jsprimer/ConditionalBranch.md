## 条件分岐

条件分岐の表現
	最も楽な方法
```
function ECMAScriptNama(version) {
	switch (version) {
		case "ES5":
			return "ECMAScript5";
		case "ES6":
			return "ECMAScript2015;
		case "ES7":
			return "ECMASrtipt2016;
		default:
			return "知らないバージョンだ";
		}
	}
return ECMAScript("ES5");  //ECMAScript5
```

複数の条件に対応するものを作る（？）時
```
const Height = 165;
      Weigh  = 55;

function getBMI(Height, Weigh) {
	switch (Height, Weigh) {
		case Heigh > 165 && Weigh > 55:
			return "ほどほどやな";
		case Heigh <= 165 && Weigh <= 55:
			return "痩せすぎよ";
		}
	}
```

論理演算子で条件を絞れる。
長ったらしい文にならないようにしよう。

