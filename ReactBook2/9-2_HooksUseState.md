## Hooksでstateを扱う
クラスコンポーネントで使用する`state`を関数コンポーネントでも使用できるようにする。  

例  
```
const [count, setCount] = useState(0);  
setCount(100);
setCount(prevCount => prevCount + 1);
```
`useState(Initial_Value)`のように引数を渡すと、その値が`state`の初期値になる。  
Typescriptでは型推論に頼らず、型を定義する必要がある。  

以降　リスト 32: src/Counter.tsx
```
import { VFC, useState } from 'react';
import { Button, Card, Statistic } from 'semantic-ui-react'; import './Counter.css';

const counter : VFC = () => {
  const [count, setCount] = useState(0);
  const increment = () => setCount((c) => c + 1);
  const reset = () => setCount(0);
};

  return (
    <Card>  //見出しなどを表すもの
      <Statistic className = "number-board">
        <Statistic.Label>count</Statistic.Label>
        <Statistic.Value>{count}</Statistic.Value>
      </Statistic>

      <Card.content>
        <div className = "ui two buttons">
          <Button color = "red" onClick = {reset}>
            Reset
          </Button>
          <Button color = "green" onClick = {increment}>
            +1
          </Button>
        </div>
      </Card.content>
    </Card>
  );
};

export default Counter;
```

```
const increment = () => setCount((c) => c + 1); //関数として定義するOK  
const increment = () => setCount(count + 1);    //0を１にする計算を3回行う。

const plusThreeDirectly = () => [0, 1, 2].forEach((_) => setCount(count + 1));
```

これ以外で注意すべき項目は、Hooksの呼び出しは最上階層で行わないといけない。  
