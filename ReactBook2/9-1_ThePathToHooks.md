## 手軽ながら壊れやすかったHooks
```
import React from 'react';

const CountMixin = {
  getInitialState: () => ({ count: 0 });
  reset: () => {
    this.setState({ count: 0 });
  };
  increment: () => {
    this.setState((state) => ({ count: state.count + 1 }));
  };
  componentDidUpdate: () => {
    if (this.state.count > this.props.max) this.reset(); 
  },
};

const CounterComponent = React.createClass({
  propTypes: {
    max: React.PropTypes.number.isRequired,
  },
  mixins: [CounterMixin],


  
  render: () => {
    const { count } = this.state;

  return ( 
    <div>
      <div>
        {count} / {max}
      </div>
      <button onClick={reset} type="button">
        Reset
      </button>
      <button onClick={increment} type="button">
        +1 
      </button>
    </div> 
   );
  } 
});

export default CounterComponent;
```

### mixinの危険性
 mixinはコンポーネントとの間に依存関係ができやすい。また、ミックス先のコンポーネントには特定の名前のstate,propなどがある前提の記述になるため、ロジックの再利用が難しい。   

 次にmixinは名前の衝突が起きやすい。state,propなどが意図せず重複してしまいバグの原因になってしまう。   
また、複数のオブジェクトをフラットに配列するインターフェイスのため、きを使わないといけない。    

 mixinは他のmixinに依存するようになり、どれか一つ壊れるとmixinが崩壊することがある。  
これは、mixinはコンポーネントとは違い階層構造ではないため、データの依存関係をみるのが難しい。  


## Render Props
  

