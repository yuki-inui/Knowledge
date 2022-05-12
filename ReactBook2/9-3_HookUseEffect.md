## EffectHookの使い方
副作用：データの取得・ログの記録・リアルDOM、などの外部からの取り込みに使う。  

具体的には`useEffect`という関数を使う。  
以下　リスト 33: Effect Hook の書き方  
```
const SampleComponent: VFC = () => { 
  const [data, setData] = useState(null); 
  useEffect(() => {
    doSomething();
    return () => clearSomething();
     }, [someDeps]);
};
```
