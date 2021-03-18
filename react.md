## React

### 1. 生命周期*

![avatar](https://raw.githubusercontent.com/kai987/talent-acquisition/main/img/lifeCycle.png)

### 2. React的组件传值有哪些

#### 一、父传子

1. 在 `state` 中准备要传递给子组件的数据
2. 以属性的方法将值传递给子组件使用的标签位置
3. 在子组件内部使用 `this.props` 接收父组件传递过来的数据

#### 二、子传父

1. 在父组件中声明一个回调函数
2. 将父组件中声明的函数当成 props 属性值传递给子组件
3. 子组件通过 props 调用回调函数
4. 将子组件的数据作为参数传递给回调函数

#### 三、跨层级通信
* 1、使用 react 自带的 Context 进行通信，createContext 创建上下文， useContext 使用上下文。
* 2、使用 Redux 或者 Mobx 等状态管理库
* 3、使用订阅发布模式

### 3. state 和 props 区别是什么？*
* state主要用于组件保存、控制、修改自己的可变状态。
* props主要是让使用该组件的父组件可以传入参数来配置该组件。

### 4. 有状态组件和无状态组件(Stateless Components)
* 有状态组件和无状态组件的本质区别就是：有无 `state` 属性和生命周期函数！
* Class Component，有自己的私有数据 `this.state` 和生命周期函数；
* Functional Component ，只有 `props` ，没有自己的 `state` 和生命周期函数；
* React官方说：无状态组件，由于没有自己的 `state` 和生命周期函数，所以运行效率高。

### 5. 受控组件(Controlled Components)和非受控组件
* 受控组件：
    * 在HTML表单元素中，将React里的 `state` 属性和表单元素的值建立依赖关系，再通过onChange事件与setState()
      结合更新state属性，就能达到控制用户输入过程中表单发生的操作。以这种由React控制的输入表单元素而改变其值的方式，称为受控组件。
* 非受控组件：
    * 仅仅想要获取某个表单元素的值，而不关心它是如何改变的。使用ref获取DOM属性信息，通过defaultValue属性来指定表单元素默认值。
* 受控组件表单数据由React组件负责处理；非受控组件表单表单数据由DOM本身处理。

### 6. Virtual DOM 
* 是一种自定义对象树，它包含构造DOM所需的所有细节，可以更快的操作、创建和更改它。

### 7. React中key的作用
* 在开发过程中，我们需要保证某个元素的key在其同级元素中具有唯一性。在React Diff算法中React会借助元素的key值来判断该元素是新创建的还是被移动而来的元素，从而减少不必要的元素渲染。此外，React还需要借助key值来判断元素与本地状态的关联关系。

### 8. Diff算法
* 传统diff算法的复杂度为 $O(n^3)$ ，显然这是无法满足性能要求的。React通过制定大胆的策略，将 $O(n^3)$ 复杂度的问题转换成 $O(n)$ 复杂度的问题。
* diff策略
  * Web UI 中 DOM 节点跨层级的移动操作特别少，可以忽略不计。
  * 拥有相同类的两个组件将会生成相似的树形结构，拥有不同类的两个组件将会生成不同的树形结构。
  * 对于同一层级的一组子节点，它们可以通过唯一 id 进行区分。
  * 基于以上三个前提策略，React 分别对 tree diff、component diff 以及 element diff 进行算法优化，事实也证明这三个前提策略是合理且准确的，它保证了整体界面构建的性能。

* React 通过分层求异的策略，对 tree diff 进行算法优化；
* React 通过相同类生成相似树形结构，不同类生成不同树形结构的策略，对 component diff 进行算法优化；
* React 通过设置唯一 key的策略，对 element diff 进行算法优化；
* 在开发组件时，保持稳定的 DOM 结构会有助于性能的提升；在开发过程中，尽量减少类似将最后一个节点移动到列表首部的操作，当节点数量过大或更新操作过于频繁时，在一定程度上会影响 React 的渲染性能。

### 9. ref属性*
* ref就是用来获取**真实dom元素**或者是**组件实例**的属性。
* ref 的值根据节点的类型而有所不同：
  * 当 ref 属性用于 HTML 元素时，构造函数中使用 `React.createRef()` 创建的 ref 接收底层 DOM 元素作为其 current 属性。
  * 当 ref 属性用于自定义 class 组件时，ref 对象接收组件的挂载实例作为其 current 属性。
  * 不能在函数组件上使用 ref 属性，因为他们没有实例。若是想用需要借助 `React.forwardRef((props, ref) => ...)`
* Refs 使用场景
  * 处理焦点、文本选择或者媒体的控制
  * 触发必要的动画
  * 集成第三方 DOM 库
  
### 10. setState只在*合成事件*和钩子函数中是异步的，在*原生事件*和setTimeout中是同步的
* 合成事件：就是react在组件中的onClick等都是属于它自定义的合成事件。
* 原生事件：比如通过addEventListener添加的，dom的原生事件。
* 原因：在React的setState函数实现中，会根据一个变量 `isBatchingUpdates` 判断是直接更新 `this.state` 还是放到队列中回头再说，而isBatchingUpdates默认是false，也就表示setState会同步更新this.
  state，但是，有一个函数batchedUpdates，这个函数会把isBatchingUpdates修改为true，而当React在调用事件处理函数之前就会调用这个batchedUpdates，造成的后果就是由React控制的事件处理过程setState不会同步更新this.state。

### 11. 高阶组件HOC*
* 高阶组件是参数为组件，返回值为新组件的函数。
* 组件是将 props 转换为 UI，而高阶组件是将组件转换为另一个组件。(例如 Redux 的 connect)
* HOC 不会修改传入的组件，也不会使用继承来复制其行为。相反，HOC 通过将组件包装在容器组件中来组成新组件。HOC 是纯函数，没有副作用。

### 12. 纯函数(PureComponent)
* PureComponent 和 Component 的区别是 PureComponent 以**浅比较** `prop` 和 `state` 的方式来实现了 `shouldComponentUpdate()` 。
* 浅比较也称引用相等，例如 === 是做浅比较，只检查左右两边是否是同一个对象的引用。
* 深比较也称原值相等，深比较是指以递归的方式遍历检查两个对象的所有属性是否相等。

### 13. react-router
* BrowserRouter或HashRouter
  * Router中包含了对路径改变的监听，并且会将相应的路径传递给子组件；
  * BrowserRouter使用history模式；
  * HashRouter使用hash模式；
* Link和NavLink
  * 通常路径的跳转是使用Link组件，最终会被渲染成a元素；
  * NavLink是在Link基础上增加了一些样式属性；(activeClassName(string), activeStyle(object))
  * to属性：Link中最重要的属性，用于设置跳转到的路径；
* Route
  * Route用于路径的匹配；
  * path属性：用于设置匹配到的路径；
  * component属性：设置匹配到路径后，渲染的组件；
  * exact：精准匹配，只有精准匹配到完全一致的路径，才会渲染对应的组件；
  
* hash模式和history模式的区别
  * 在hash模式下，前端路由修改的是 # 中的信息，而浏览器请求时不会将 # 后面的数据发送到后台，所以没有问题。但是在history模式下，你可以自由的修改path，当刷新时，如果服务器中没有相应的响应或者资源，则会刷新出来404页面。

* withRouter
  * 这是一个高阶组件（函数），withRouter 可以包装任何自定义组件，将 react-router 的 history, location, match 三个对象传入组件的props。


### 14. 404页面
```
<Route path="*">
  <NotFound />
</Route>
```
* 放置到最后一个Route

### 15. react原理
* Virtual Dom模型
* 生命周期管理
* setState机制
* diff算法
* React patch、事件系统

### 16. 错误边界(Error Boundaries)
* 如果一个 class 组件中定义了 `static getDerivedStateFromError()` 或 `componentDidCatch()` 这两个生命周期方法中的任意一个（或两个）时，那么它就变成一个错误边界。当抛出错误后，请使用 `static getDerivedStateFromError()` 渲染备用 UI ，使用 `componentDidCatch()` 打印错误信息。
* 错误边界的工作方式类似于 JavaScript 的 catch {}，不同的地方在于错误边界只针对 React 组件。只有 class 组件才可以成为错误边界组件。
* 注意错误边界仅可以捕获其子组件的错误，它无法捕获其自身的错误。
* 错误边界无法捕获以下场景中产生的错误：
  * 事件处理
  * 异步代码（例如 setTimeout 或 requestAnimationFrame 回调函数）
  * 服务端渲染
  * 它自身抛出来的错误（并非它的子组件）

### 17. 状态提升
* 多个组件需要反映相同的变化数据，这时我们建议将共享状态提升到最近的共同父组件中去。

### 18. Context 
* Context 提供了一个无需为每层组件手动添加 props，就能在组件树间进行数据传递的方法。
  * API
    * createContext
    * Context.Provider
    * Class.contextType
    * Context.Consumer
    * Context.displayName
  
### 19. React Fiber
* React Fiber 的目标是提升其对于动画、布局、手势等场景的适用性。它的核心功能就是增量渲染：一种将渲染工作分解为多个区块并将其分散到每一帧里面。
* fiber是在virtual dom的前提下，为每一个节点附加的任务机制对象；
