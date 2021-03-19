## JavaScript

### 1. Array
* 不会改变原数据（map，filter，concat，forEach 等），改变数据（pop，push，splice 等）。

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
  * 如果调用 reduce() 时提供了initialValue，accumulator取值为initialValue，currentValue取数组中的第一个值；如果没有提供 
  initialValue，那么accumulator取数组中的第一个值，currentValue取数组中的第二个值。
