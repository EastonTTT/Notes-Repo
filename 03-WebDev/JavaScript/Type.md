JavaScript 是一种**动态类型语言**，变量在运行时可以保存任何类型的值。
类型分为：
- 原始类型
- 引用类型
---
## 原始类型：
原始类型的值是不可变的，是按值存储的。
- `undefined`：已声明但还未赋值，或者变量不存在
- `null`：已赋空值
- `boolean`：布尔值
- `number`：包括整数、浮点数、`NaN`、`Infinity`。
- `string`：文本数据，==注意：string是**不可变的**==
- `symbol`：创建唯一标识符，用于对象属性的私有键。
- `bigInt`：表示任意大整数，后缀 `n`
---
### boolean：
==**所有非假值外的值全都为`true`**==
#### 假值：
- `false`：布尔值
- `0`：数字0
- `NaN`：非法数字（注意：`NaN === NaN -> false!!）
- `''`：空字符串
- `null`：空值
- `undefined`：未定义
---
### symbol：

***
## 引用类型：
引用类型的值是**对象(Object)**，存储的是地址。
- `Object`
- `Array`
- `Function`
- `Date`
- `RegExp`
- `Error`
---
## 类型的判断：
### typeof：
用法：`const type = typeof val`
`typeof`操作符，返回一个字符串来表示变量的类型。
#### 局限性：
`typeof`操作符没有办法区分某些对象的子类型：`Array,Map,Set,Date,RegExp`，他们返回的结果全部都是`Object`，`typeof null`的结果也是`Object`。这是历史包袱。
能够被`typeof`正确返回的类型：
`"undefined"、"object"、"boolean"、"number"、"string"、"symbol"、"bigint"、  "function"`
***
### instance of
用法：`val instanceof Type` 
**注意：`instanceof`==只能用于对象（array,date,map,set,自定义对象...）==**
返回一个布尔值来表示判断的结果。
返回`true`表示构造函数 `Constructor` 的`prototype` 在对象 `obj` 的原型链上。
原理：`instanceof` 是基于**原型链**（`[[Prototype]]`，也就是 `__proto__`）来判断的。
***
### Object.prototype.toString
方法名：`Object.prototype.toString`，这里的`.call`是为了绑定this对象。
用法：`const typeString = Object.prototype.toString.call(val)`
返回值：形如`[object TypeName]`的字符串。其中TypeName就是变量的类型名称。
**是最通用和全面的方法，可以精准判定所有数据类型。**
这是**每个对象的底层默认方法**，它通过内部 `[[Class]]` 值来识别对象类型。
每个JavaScript 的对象都有一个内部属性 `[[Class]]`，`Object.prototype.toString` 就是用来读取 `[[Class]]` 的。
**原始类型在调用Object方法的时候会被自动“装箱”，即用包装类封装成对象。**
***
### 指定类型判断：
- `Array.isArray(val)`：判断数组
- `Number.isNaN(val)`：判断是否为`NaN`
- `val === null`：判断是否为空值。
***
## Set：
集合，**Set对象允许存储任何类型的唯一值**
### 属性：
- `.size`：返回成员总数
### 方法：
- `.add(val)`：添加一个值
- `.delete(val)`：删除一个值
- `.has(val)`：返回一个布尔值，表示Set中是否有该值
- `.clear()`：清空Set，无返回值
- `.values()`：返回一个可迭代对象，包含Set内的所有值
- `.foreach()`：遍历所有成员
---
## Map：
字典，**Map对象是键值对的集合**
### 属性：
- `.size`：返回成员总数
### 方法：
- `.set(key,value)`：设置键名和对应值，返回值为当前Map对象
- `.has(key)`：返回一个布尔值，判断某个键是否在Map中
- `.get(key)`：返回该键对应的值，如果不存在则返回`undefined`
- `.delete(key)`：删除对应的键值对，删除成功返回`true`，失败则返回`false`
- `.clear()`：清空Map，无返回值
- `.keys()`：返回键名的遍历器
- `.values()`返回键值的遍历器
- `.entries()`：返回所有成员的遍历器
- `.foreach()`：遍历所有成员
### 特性：
- Map 的键实际上是跟内存地址绑定的，只要内存地址不一样，就视为两个键
- Map 的键若是一个简单类型的值（数字、字符串、布尔值），则只要两个值严格相等，就会被视为同一个值
- Map 的 set 方法返回的是当前的 Map 对象，因此可以采用链式写法。
- Map 结构转数组结构，可用扩展运算符（...）
---
## WeakMap & WeakSet：
### 特性：
- 成员只能是对象，而不能是其他类型的值
- 没有 size 静态属性
- 没有 clear 方法
- 没有遍历方法，不能遍历
- WeakMap/WeakSet中的对象都是弱引用，引用不计入垃圾回收机制，所以不会引发内存泄漏
- 它们可以用于存储DOM对象，在DOM被清除的时候无需担心内存泄漏问题