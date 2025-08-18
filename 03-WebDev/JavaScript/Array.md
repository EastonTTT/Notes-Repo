#javascript数组操作 
这篇笔记主要包含一些`javascript`数组相关的操作函数。

##  initialize：
常见的数组初始化方法：
注意⚠️：**未初始化的数组元素是 `undefined` 直接访问会报错**
- 数组字面量：`const arr = []`
- 构造函数：`const arr = new Array<type>(len)`
### Array.from：
函数：`Array.from(arrayLike, mapFn?, thisArg?)`
- **arrayLike**：类数组（比如：`{length:5}`）或可迭代对象（如字符串、`Set`、`Map`、`arguments`、`NodeList` 等）
- **`mapFn(currentValue, index, array)`**（可选）：生成数组元素的映射函数，类似 `.map()` 的回调，可以在构造后直接操作元素
- **thisArg**（可选）：映射函数的 `this` 指向
***
## sort：
函数：`Array.prototype.sort(compareFunction)`
注意⚠️
- sort函数 **默认不是按照数值大小排序的！** 他会先把元素转化成 **字符串** ，再按照字典顺序排序。==所以不能直接用来排序数值，需要传入**比较函数**。==
- sort函数 **会原地修改数组**，而不是返回一个新数组。如果要返回新数组，请使用`toSorted`方法。
- sort函数排序是 **稳定的**，相等的值相对顺序不变。
### compareFunction：
比较函数需要返回==**负数/正数/零**，不要返回 **布尔值**。==
具体返回值的排序：
`sort((a,b) => a-b)`
- 负数：a在b前
- 零：顺序不变
- 正数：b在a前
---
## fill：
函数：`array.fill(element,startIndex,endIndex)`
往数组指定的区间内填充指定的内容 **会覆盖原数组**，如果没有指定区间则对整个数组进行操作。
***
## 数组的遍历：

### for相关：
- `for(let i = 0;i < arr.length;i++)` 最基础的循环控制。
- `for...of` 值遍历，不需要索引时可以使用。
- `for...in`键遍历，键是字符串类型的，不推荐用于数组。
---
### foreach：
`Array.prototype.forEach(callbackFn(currentValue, index, array), thisArg?)`
用于对数组的每一个元素**执行一次给定的回调函数，==不是对原数组作出修改（除非显式操作，但是不推荐使用 `foreach` 来修改数组）==**。
- `foreach`函数的返回值是`undefined`，**不会返回新数组！**
- `foreach`函数会自动跳过空值
- `foreach`函数不能中断（没有break 和 continue）
- 不主动修改原数组。（**也不推荐用来修改原数组，要修改请用`for...of`**）
#### 使用场景：
`foreach`函数更像是一个 **副作用操作** 函数，在需要使用数组原始做某些事情，但是不涉及到修改原数组时非常适用。
注意⚠：`foreach`函数不会等待异步回调，所以要**避免使用**`foreach`来执行异步操作，==异步操作应该使用 `for...of + await` 来实现==
***
### map：
函数：`Array.prototype.map`对数组的每一个元素**执行一个函数，并返回一个新数组（新数组与原数组长度相同，是原数组元素一一映射的结果）**。（这点和`foreach`不同!!）
`const newArr = arr.map(callbackFn(currentValue, index, array), thisArg?)
- 遍历之前会先固定原数组长度，超出长度的不会被遍历到
- 自动跳过空值，对应的，结果数组的相应位置也会是空值。
- 不主动修改原数组。（**也不推荐用来修改原数组，要修改请用`for...of`**）
- 不能中断（没有break 和 continue）
---
### reduce：
`reduce` 会**对数组中的每个元素依次执行回调函数，并把上一次回调返回的结果作为“累积值”传给下一次回调，最终返回一个累计结果（数、对象、数组、map...）**
`arr.reduce(callbackFn(accumulator, currentValue, index, array), initValue?)`
- `callbackFn`：必填，执行的函数
    - `accumulator` → 累积器，上一次回调的返回值
    - `currentValue` → 当前元素值
    - `index` → 当前索引 **(optional)**
    - `array` → 原数组 **(optional)**
- `initialValue`：可选，初始的 `accumulator` 值
注意⚠：
- `initialValue`是可选的，如果指定了`initialValue`，那么开始的`accumulator`的值就是`initialValue`，如果没有指定，`accumulator`的初始值会是数组的第一个值（`arr[0]`），这个时候**如果数组是空的就会报错，所以推荐每次都把`initialValue`写上**。
- `callbackFn`别忘记返回值
- 不能中断（没有break 和 continue）
- 自动跳过空值
---

