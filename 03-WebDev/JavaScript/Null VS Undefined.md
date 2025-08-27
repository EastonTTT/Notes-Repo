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
## 判空运算符 & 兜底操作：

### ?? 操作符：
用法：`a ?? b`  -> `a` 为 **`null 或 undefined`** 时为 `b`，否则为`a`
- ==只判断 null 和 undefined，而不是判断**值的真假**==
***
### || 操作符：
用法：`a || b` 若 `a` 是“真值”就取 `a`，否则取 `b`。
- 与`??`不同，`||`操作符扩大了兜底值`b`的使用范围。
----
### ?. 操作符：
用法：在链路任何一步是 `null`/`undefined` 时**短路并返回 `undefined`**，而不是报错。
- 因为当被访问属性值为`null`/`undefined`的时候会报出`TypeError: Cannot read property of null/undefined`，导致程序崩溃。
***
### 短路求值：
用法：`boolean && other operation`
- 当判断值为`true`的时候执行右侧的操作并返回右侧操作的结果值
- 否则返回`false`
- 可以当作简介版本的`if`操作