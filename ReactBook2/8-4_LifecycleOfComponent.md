　ライフサイクルとは、まずマウントして初期化され、次にレンダリングされた後、 何らかのきっかけで再レンダリングされ、最後にアンマウントされるまでの過程。  

ライフサイクルメソッド  
	1 Mountingフェーズ: コンポーネントが初期化され、仮想DOMにマウントされる	　        までのフェーズ。ここで初めてレンダリングされる。   
	2 Updatingフェーズ: 差分検出処理エンジンが変更を検知してコンポーネント
	  が再レンダリングされる。  
	3 Unmountingフェーズ: コンポーネントが仮想DOMから削除される。  
	4 ErrorHandlingフェーズ: 子孫コンポーネントのエラーを検知補足する。   

2の「変更を検知して再レンダリング」は基本的に２つある。propsもしくはstateの変更  
1 Mountingフェーズ    
| メソッド | 戻り値 | 説明 |
| -- | -- | -- |
| constructor(props) | void | クラスのコンストラクタ |
| static<br>getDerivedStateFromProps(prop,state) | State or null | renderメソッド実行の直前に呼ばれ<br>戻り値で新しいstateが設定 |
| render() | ReactElement | レンダリングの内容を返す |
| componentDidMount() | void | コンポーネントがマウントされた直後に呼ばれる |

2 Updatingフェーズ

| メソッド | 戻り値 | 説明 |
| -- | -- | -- |
| static<br>getDerivedStateFromProps(prop,state) | State or null | renderメソッ>ド実行の直前に呼ばれ<br>戻り値で新しいstateが設定 |
| shouldComponentUpdates<br>(nextProps,nextState) | boolean | 変更を検知してから再レンダリングの前に呼ばれ<br>falseを返すことでさいレンダリングを中止する。
| render() | ReactElement | レンダリングの内容を返す |
| getSnapShotBeforeUpdate<br>(nextProps,nextState) | SnapShot or null | 再レンダリング内容がDOMに反映される直前に呼ばれ、<br>戻り値でスナップショットをとっておき、<br>それを、componentDidUpdateに渡すことができる。 |
| componentDidUpdate<br>(prevProps, prevState, snapshot?) | void | 再レンダリングの完了直後に呼ばれる |

3 Unmountingフェーズ

| メソッド | 戻り値 | 説明 |
| -- | -- | -- |
| componentWillUnmount() | void | コンポーネントがアンマウントされて破棄される<br>直前に呼ばれる。 |

4 Error Handlingフェーズ

| メソッド | 戻り値 | 説明 |
| -- | -- | -- |
| componentDidCatch(error,info) | void | 子孫コンポーネントで例外が起きた時に呼ばれる |
| static<br>getDerivedStateFromError(error) | State or null | 子孫コンポーネントで例外が起きた時に呼ばれ、戻り値で新しいstateが設定できる |

タイマー
```
import { Component, ReactElement } from 'react';
import { Button, Card, Icon, Statistic } from 'semantic-ui-react';
import './App.css';

const LIMIT = 60;
type State = { timeLeft: number };

class App extends Component<unknown, State> {
  timerId: NodeJS.Timer | null = null;

  constructor(props: unknown){
    super(props);
    this.state = { timeLeft: LIMIT };
  };

  componentDidMount = (): void => {
    this.timerID = setInterval(this.tick, 1000);
  };

  componentDidUpdate = (): void => {
    const { timeLeft } = this.state;
    if (timeLeft === 0) this.reset();
  };

  componentWillUnmount = (): void => {
    if (this.timerId) clearInterval(this.timerId);
  };

  tick = (): void =>
    this.setState((prevState) => ({ timeLeft: prevState.timeLeft -1 }));

  reset = (): void => this.setState({ timeLeft: LIMIT });

  render = (): ReactElement => {
    const { timeLeft } = this.state;


    return (
      <div className="container">
        <header>
          <h1>タイマー</h1>
        </header>
        <Card>
          <Statistic className="number-board">
            <Statistic.Label>time</Statistic.Label> 
            <Statistic.Value>{timeLeft}</Statistic.Value>
          </Statistic>
          <Card.Content>
            <Button color="red" fluid onClick={this.reset}>
              <Icon name="redo" />
              Reset
            </Button>
          </Card.Content>
        </Card>
      </div>
);
}; 
}

export default App;
```
