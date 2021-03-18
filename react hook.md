## React Hook

### 1. 每次 render 之后都会执行 useEffect 吗？
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

### 4. 
