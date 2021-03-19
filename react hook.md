## React Hook

### 1. 每次 render 之后都会执行 useEffect里面的内容吗？
* 这是默认行为，在第一次 render 之后和每次 update 之后都会运行。
* 有一个函数组件，把log写在3个地方，打印顺序是：
    * (1) useEffect外  (2) render  (3) useEffect里面

### 2. useEffect对应的生命周期是怎样的？
* (1) componentDidMount ==> `useEffect(() => {}, [])`
    * 最主要的是第二个参数是空数组[]，只会在组件挂载后运行一次
* (2) componentDidUpdate ==> `useEffect(() => {})` 或 `useEffect(() => {}, [n])`
    * 所有的state任意一个更新触发函数 / 只有n值变化，触发函数
* (3) componentWillUnMount ==> `useEffect(() => {log('渲染时执行'); return () => log('组件要死了')})`
  ```
  useEffect(()=>{
    // 需要在 componentDidMount 执行的内容
    return function cleanup() {
      // 需要在 componentWillUnmount 执行的内容      
    }
  }, [])
  ```

### 3. AB父子组件生命周期log顺序
* A(1)、A(2)、B(1)、B(2)、B(3)、A(3)

### 4. useEffect和useMemo区别
* useMemo是在DOM更新前触发的，类比生命周期`shouldComponentUpdate`，useEffect只能在DOM更新后再触发。
* 和useMemo相近的还有一个useCallback，`useCallback(fn, deps)` 相当于 `useMemo(() => fn, deps)`

### 5. useReducer
* `const [state, dispatch] = useReducer(reducer, initialArg, init)`
* 是useState的替代方案。它接受一个形如 `(state, action) => newState` 的reducer，并返回当前的state以及与其配套的dispatch方法。
* 组件只需要发出action，而无需知道如何更新状态。也就是将What to do与How to do解耦。彻底解耦的标志就是：useReducer总是返回相同的dispatch函数（发出action的渠道），不管reducer（状态更新的逻辑）如何变化。
  ```
  function init(initialCount) {
    return {count: initialCount};
  }
  
  function reducer(state, action) {
    switch (action.type) {
      case 'increment':
        return {count: state.count + 1};
      case 'decrement':
        return {count: state.count - 1};
      case 'reset':
        return init(action.payload);
      default:
        throw new Error();
    }
  }
  
  function Counter({initialCount}) {
    const [state, dispatch] = useReducer(reducer, initialCount, init);
    return (
      <>
        Count: {state.count}
        <button
          onClick={() => dispatch({type: 'reset', payload: initialCount})}>
          Reset
        </button>
        <button onClick={() => dispatch({type: 'decrement'})}>-</button>
        <button onClick={() => dispatch({type: 'increment'})}>+</button>
      </>
    );
  }
  ```
### 6. useContext
* 接收一个 context 对象（React.createContext 的返回值）并返回该 context 的当前值。当前的 context 值由上层组件中距离当前组件最近的 <MyContext.Provider> 的 value prop 决定。
  ```
  export const BookContext = createContext();
  
  <BookContext.Provider value={{books, addBook, removeBook}}>
    { props.children }
  </BookContext.Provider>
  
  const { books, addBook, removeBook } = useContext(BookContext);
  ```

### 7. useRef
* useRef 不仅仅是用来管理 DOM ref 的，它还相当于 this ，可以存放任何变量。
* 当 useRef 的内容发生变化时，它不会通知您。更改.current属性不会导致重新呈现。因为他一直是一个引用。
* createRef 每次渲染都会返回一个新的引用，而 useRef 每次都会返回相同的引用。


### 8. Hook的使用规则

* 1. 只在最顶层使用 Hook，不要在循环，条件或嵌套函数中调用 Hook
* 2. 只在 React 函数中调用 Hook，不要在普通的 JavaScript 函数中调用 Hook。
