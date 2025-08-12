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
