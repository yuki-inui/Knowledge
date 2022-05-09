コンポーネントにおけるライフサイクルとは  
 - マウントして初期化され、次にレンダリングされた後、何らかの理由で再レンダリングされ、アンマウントするまで。  

**ライフサイクルメソッド**  
- `Mounting`フェーズ      :コンポーネントが初期化され、仮想DOMにマウントされるまでのフェーズ。
- `Updating`フェーズ      :差分検出処理エンジンが変更を検知して、コンポーネントが再レンダリングされるフェーズ。
- `Unmounting`フェーズ    :コンポーネントが仮想DOMから削除されるフェーズ。
- `Error Handling`フェーズ:子孫コンポーネントの`Error`を検知補足するフェーズ。   

- Mountingフェーズ    

| メソッド | 戻り値 | 説明 |
| -- | -- | -- |
| constructor(props) | void | クラスのコンストラクタ |
| static<br>getDerivedStateFromProps(prop,state) | State or null | renderメソッド実行の直前に呼ばれ<br>戻り値で新しいstateが設定 |
| render() | ReactElement | レンダリングの内容を返す |
| componentDidMount() | void | コンポーネントがマウントされた直後に呼ばれる |

- Updatingフェーズ

| メソッド | 戻り値 | 説明 |
| -- | -- | -- |
| static<br>getDerivedStateFromProps(prop,state) | State or null | renderメソッ>ド実行の直前に呼ばれ<br>戻り値で新しいstateが設定 |
| shouldComponentUpdates<br>(nextProps,nextState) | boolean | 変更を検知してから再レンダリングの前に呼ばれ<br>falseを返すことでさいレンダリングを中止する。
| render() | ReactElement | レンダリングの内容を返す |
| getSnapShotBeforeUpdate<br>(nextProps,nextState) | SnapShot or null | 再レンダリング内容がDOMに反映される直前に呼ばれ、<br>戻り値でスナップショットをとっておき、<br>それを、componentDidUpdateに渡すことができる。 |
| componentDidUpdate<br>(prevProps, prevState, snapshot?) | void | 再レンダリングの完了直後に呼ばれる |

- Unmountingフェーズ

| メソッド | 戻り値 | 説明 |
| -- | -- | -- |
| componentWillUnmount() | void | コンポーネントがアンマウントされて破棄される<br>直前に呼ばれる。 |

- Error Handlingフェーズ

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
    super(props);                     //super(props)は親クラスのコンストラクタを呼び出す役割
    this.state = { timeLeft: LIMIT };   //super(props)がないとthis.stateが使えない
  };

  componentDidMount = (): void => {
    this.timerID = setInterval(this.tick, 1000);   //tickを1000ミリ秒(1秒)ごとに実行される
  };

  componentDidUpdate = (): void => {
    const { timeLeft } = this.state;     //?
    if (timeLeft === 0) this.reset();　　//timeLeftが0になればリセット
  };

  componentWillUnmount = (): void => {
    if (this.timerId) clearInterval(this.timerId);   //this.timerIdを止める
  };

  tick = (): void =>
    this.setState((prevState) => ({ timeLeft: prevState.timeLeft -1 }));　　　//timeleft-1　をする関数

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
