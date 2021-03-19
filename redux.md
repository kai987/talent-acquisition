## Redux

### 1. 

![avatar](https://raw.githubusercontent.com/kai987/talent-acquisition/main/img/redux.png)

### 2. Redux是JavaScript状态容器，提供可预测化的状态管理。
* Action: action是把数据从应用传到store的有效载荷。它是store数据的唯一来源。一般来说通过 `store.dispatch()` 将action传到store。
* Reducer: reducer指定了应用状态的变化如何响应actions并发送到store，action只是描述了有事情发生了，并没有描述应用如何更新state。
* Store: 维持应用的state
    * 提供 `getState()` 方法取得state
    * 提供 `dispatch(action)` 方法更新state
    * 通过subscribe(listener)注册监听器，`store.subscribe(() => {})`
    * 通过subscribe(listener)返回的函数注销监听器

### 3. 如何在 reducer 之间共享 state?
* 可能需要自定义方法去处理这些 action，用自定义的顶层 reducer 方法替换 combineReducers。可以使用类似于 `reduce-reducers` 的工具运行 combineReducers 去处理尽可能多的 action，同时还要为存在 state 交叉部分的若干 action 执行更专用的 reducer。
* 类似于 redux-thunk 的 异步 action 创建函数能通过 getState() 方法获取所有的 state。 action 创建函数能从 state 中检索到额外的数据并传入 action，所以 reducer 有足够的信息去更新所维护的 state 层。

### 4. action
* 异步 Action
    * 当调用异步 API 时，发起请求的时刻，和接收到响应的时刻都需要 dispatch 至少三种 action
    * 一种通知 reducer **请求开始的** action
    * 一种通知 reducer **请求成功的** action。
    * 一种通知 reducer **请求失败的** action。
    * Redux Thunk middleware / redux-saga
    ```
    const store = createStore(
      rootReducer,
      applyMiddleware(
        thunkMiddleware, // 允许我们 dispatch() 函数
        loggerMiddleware // 一个很便捷的 middleware，用来打印 action 日志
      )
    )
    ```
  
### 5. reducer
* 可以使用 Redux 提供的 `combineReducers()` 方法将多个小的 reducer 组合成一个 rootReducer

### 6. store
* Store 就是用来维持应用所有的 state 树的一个对象。改变 store 内 state 的惟一途径是对它 dispatch 一个 action。

### 7. Immutable.JS
* 封装在 Immutable.JS 对象中的数据永远不会发生变换（mutate）。总是会返回一个新的拷贝对象。
