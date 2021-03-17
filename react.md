### 1. 生命周期

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

#### 三、兄弟传值
* 兄弟之间的传值就是：首先 子组件1 向 父组件 传值，然后 父组件 传值给 子组件2

### 3. state 和 props 区别是什么？
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
* 建议，在开发组件时，保持稳定的 DOM 结构会有助于性能的提升；在开发过程中，尽量减少类似将最后一个节点移动到列表首部的操作，当节点数量过大或更新操作过于频繁时，在一定程度上会影响 React 的渲染性能。

### 9. ref属性
* ref就是用来获取**真实dom元素**或者是**组件实例**的属性。
* ref 的值根据节点的类型而有所不同：
  * 当 ref 属性用于 HTML 元素时，构造函数中使用 `React.createRef()` 创建的 ref 接收底层 DOM 元素作为其 current 属性。
  * 当 ref 属性用于自定义 class 组件时，ref 对象接收组件的挂载实例作为其 current 属性。
  * 不能在函数组件上使用 ref 属性，因为他们没有实例。若是想用需要借助 `React.forwardRef()`
* Refs 使用场景
  * 处理焦点、文本选择或者媒体的控制
  * 触发必要的动画
  * 集成第三方 DOM 库
  
### 10. setState只在合成事件和钩子函数中是异步的，在原生事件和setTimeout中是同步的
* 合成事件：就是react在组件中的onClick等都是属于它自定义的合成事件。
* 原生事件：比如通过addEventListener添加的，dom的原生事件。
* 原因：在React的setState函数实现中，会根据一个变量 `isBatchingUpdates` 判断是直接更新 `this.state` 还是放到队列中回头再说，而isBatchingUpdates默认是false，也就表示setState会同步更新this.
  state，但是，有一个函数batchedUpdates，这个函数会把isBatchingUpdates修改为true，而当React在调用事件处理函数之前就会调用这个batchedUpdates，造成的后果就是由React控制的事件处理过程setState不会同步更新this.state。

### 11. 高阶组件HOC
* 高阶组件是参数为组件，返回值为新组件的函数。
* 组件是将 props 转换为 UI，而高阶组件是将组件转换为另一个组件。(例如 Redux 的 connect)

### 12. 
