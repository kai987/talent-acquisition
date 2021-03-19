## Redux

### 1. 

### 2. Redux是JavaScript状态容器，提供可预测化的状态管理。
A

### 3. 如何在 reducer 之间共享 state?
* 可能需要自定义方法去处理这些 action，用自定义的顶层 reducer 方法替换 combineReducers。可以使用类似于 `reduce-reducers` 的工具运行 combineReducers 去处理尽可能多的 action，同时还要为存在 state 交叉部分的若干 action 执行更专用的 reducer。
* 类似于 redux-thunk 的 异步 action 创建函数能通过 getState() 方法获取所有的 state。 action 创建函数能从 state 中检索到额外的数据并传入 action，所以 reducer 有足够的信息去更新所维护的 state 层。
