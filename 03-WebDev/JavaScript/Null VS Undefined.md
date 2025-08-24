## null
`null` 是一个表示 **“刻意为空”** 的值，表示变量应当持有一个对象，但当前没有。表示一种“主动置空”（不是没有赋值）。
### 注意事项：
- `typeof null` 的结果是 `Object`. （早起语言设计的遗留bug）
- `null === null` 的结果是`true`
- `undefined == null` 的结果是 `true`
***
## undefined
`undefined` 表示一个变量 **已声明但尚未赋值**，或**访问了不存在的属性**，或某些函数没有返回值时默认的结果。
### 注意事项：
-  `typeof undefined` 的结果是 `undefined`. 
- `undefined === undefined` 的结果是`true`
- `undefined == null` 的结果是 `true`
### 值为undefined的场景：
- 声明了变量**但是没有赋值**
- 访问**对象中不存在的属性**
- 当函数没有**显式 return** 的时候访问它的返回值
- 函数**参数缺**失时
- 数组的空洞位置
- 结构失败时
---
