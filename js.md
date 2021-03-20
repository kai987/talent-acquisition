## JavaScript

### 1. Array
* 不会改变原数据(map，filter，concat，forEach 等)
* 改变数据(pop(从一个数组中删除并返回最后一个元素)，push，shift(从数组中删除第一个元素，并返回该元素的值)，unshift(将一个或多个元素添加到数组的开头)，splice 等)。

* reduce
    * Accumulator (累计器) 累计器累计回调的返回值; 它是上一次调用回调时返回的累积值。
    * CurrentValue (当前值) 数组中正在处理的元素。
    * CurrentIndex (当前索引) 数组中正在处理的当前元素的索引。如果提供了initialValue，则起始索引号为0，否则从索引1起始。
    * SourceArray (源数组) 调用reduce()的数组
    * initialValue 作为第一次调用callback函数时的第一个参数的值。如果没有提供初始值，则将使用数组中的第一个元素。

      ```
        [0, 1, 2, 3, 4].reduce((accumulator, currentValue, currentIndex, array) => {
          return accumulator + currentValue
        }, 10)
      ```
    
      | callback | accumulator | currentValue | currentIndex | array | return value |
      | :--:|:--:|:--:|:--:|:--:|:--:|
      | first call | 10 | 0 | 0 | [0, 1, 2, 3, 4] | 10 |
      | second call | 10 | 1 | 1 | [0, 1, 2, 3, 4] | 11 |
      | third call | 11 | 2 | 2 | [0, 1, 2, 3, 4] | 13 |
      | fourth call | 13 | 3 | 3 | [0, 1, 2, 3, 4] | 16 |
      | fifth call | 16 | 4 | 4 | [0, 1, 2, 3, 4] | 20 |
  
    * accumulator 和currentValue的取值有两种情况：
      * 如果调用 reduce() 时提供了initialValue，accumulator取值为initialValue，currentValue取数组中的第一个值； 
      * 如果没有提供 initialValue，那么accumulator取数组中的第一个值，currentValue取数组中的第二个值。
    * 用途
      * 数组里所有值的和
      `var sum = [0, 1, 2, 3].reduce((acc, cur) => acc + cur, 0)`
      * 将二维数组转化为一维数组
      `var flattened = [[0, 1], [2, 3], [4, 5]].reduce((acc, cur) => acc.concat(cur), [])`
  
* Set
  * 类似于数组， 但是成员的值都是唯一的，没有重复的值。(对象)
  * api: `Set.size`, `new Set.add(val)`, `Set.delete(val)`, `Set.has(val)`, `Set.clear()`
  * 字符串去重
    * `[...new Set('ababbc')].join('')  //'abc'`
  * 数组去重
    * `Array.from(new Set(array))`
    
* Map
  * 本质上是键值对的集合(Hash结构)，只能用字符串当作键。
  ```
    const map = new Map()
    map.set('foo', true)
    map.set('bar', false)
    map.size  // 2
  ```
  * api: `new Map.set(key, value)`, `Map.get(key)`, `Map.has(key)`, `Map.delete(key)`, `Map.clear()`

### 2. 深拷贝和浅拷贝
* 浅拷贝是创建一个新对象，这个对象有着原始对象属性值的一份精确拷贝。**如果其中一个对象改变了这个地址，就会影响到另一个对象。**
* 深拷贝是将一个对象从内存中完整的拷贝一份出来，从堆内存中开辟一个新的区域存放新对象，且**修改新对象不会影响原对象**。
* 浅拷贝实现方式
  * Object.assign()
  * 函数库lodash的_.clone方法
  * 展开运算符...
  * Array.prototype.concat()
  * Array.prototype.slice()
* 深拷贝的实现方式
  * JSON.parse(JSON.stringify())
  * 函数库lodash的_.cloneDeep方法
  * 手写递归方法

### 3. this
* this表示函数上下文，即与函数调用相关联的对象。函数的定义方式和调用方式决定了this的取值。
* 函数的调用方式有4种
  * 作为函数调用：`b()`
  * 作为方法调用：`a.b()` 关联在一个对象上。
  * 作为构造函数调用：`new A()`  实例化一个新的对象。
  * 通过apply与call方法调用：`b.apply(a)` 或 `b.call(a)`

* 函数的调用方式影响this的取值
  * 如果作为函数调用，在非严格模式下，this指向全局window对象；在严格模式下，this指向undefined。
  * 作为方法调用，this通常指向调用的对象。
  * 作为构造函数调用，this指向新创建的对象。
  * 通过call或apply调用，this指向call或apply的第一个参数。
  
* 箭头函数没有单独的this值，this在箭头函数创建时确定，从定义时的所在函数继承上下文。
* 所有函数均可使用bind方法，创建新函数，并绑定到bind方法传入的参数上。被绑定的函数与原始函数具有一致的行为。

### 4. 闭包
* 闭包允许函数访问并操作函数外部的变量。只要变量或函数存在于声明函数时的作用域内，闭包即可使函数能够访问这些变量或函数。

### 5. 扩展运算符(...)内部使用for...of循环

### 6. JavaScript语言的数据类型(7种)
* undefined、null、布尔值(Boolean)、字符串(String)、数值(Number)、对象(Object)、Symbol

### 7. Symbol
* 保证属性名属于Symbol类型都是独一无二的，不会与其他属性产生冲突。
* 对象的属性名现在有两种类型，1. 字符串   2. Symbol类型

### 8. var 与 let、const的区别
* var 声明变量存在提升，let 和 const不存在变量提升（要先声明再使用）
* let、const都是块级局部变量（只在当前代码块起作用）
* 同一作用域下 let 和 const 不能声明同名变量，而 var 可以

### 9. === 与 == 的区别
* == 会发生隐式转换，可能导致类型转换错误，=== 全等则可避免

### 10. bind、call、apply区别
* 都是为了解决改变 this 的指向。三者第一个参数都是 this 要指向的对象，若第一个参数没有或是 null，则默认指向全局 window。
* 传参上除了第一个参数外，call可以接受一个参数列表，apply只接受一个参数数组。
* bind 方法返回值是函数，并且需要稍后调用才会执行，而 apply 和 call 是立即调用。

### 11. 回流和重绘
* 当render tree中的一部分(或全部)因为元素的规模尺寸，布局，隐藏等改变而需要重新构建。这就称为回流(reflow)。
* 当render tree中的一些元素需要更新属性，而这些属性只是影响元素的外观，风格，而不会影响布局的，比如background-color。则就叫称为重绘。
* 回流必将引起重绘，而重绘不一定会引起回流。比如：只有颜色改变的时候就只会发生重绘而不会引起回流，当页面布局和几何属性改变时就需要回流，比如：添加或者删除可见的DOM元素，元素位置改变，元素尺寸改变——边距、填充、边框、宽度和高度，内容改变

### 12. 防抖和节流
* 防抖（debounce）
  * 所谓防抖，就是指触发事件后在 n 秒内函数只能执行一次，如果在 n 秒内又触发了事件，则会重新计算函数执行时间。
* 节流（throttle）
  * 所谓节流，就是指连续触发事件但是在 n 秒中只执行一次函数。
  
### 13. 跨域
![avatar](https://raw.githubusercontent.com/kai987/talent-acquisition/main/img/cors.png)

* 同源策略是**协议** + **域名** + **端口**三者相同
* script 标签不受这个限制
