#元编程
“元编程”（meta programming），即对编程语言进行编程。
***
## Proxy：
#Proxy 
`Proxy` 可以理解为**对象的“拦截器”**，它允许你**在访问、修改、删除对象属性时加一层自定义逻辑**。
```js
let proxy = new Proxy(target, handler);
```

- target：要被代理的对象（可以是对象、数组、函数等）。
- handler：一个对象，定义了一系列 “陷阱（traps）”，用来拦截对象的操作。
### 常见的handler：
- `get(target, propKey, receiver)
- `set(target, propKey, value, receiver)`
- `has(target, propKey)`
- `deleteProperty(target, propKey)`
- `apply(target, object, args)`
- 还有好多。。。
### 注意点：
- 要使得`Proxy`起作用，==**必须针对`Proxy`实例（上例是`proxy`对象）进行操作，而不是针对目标对象（上例是空对象）进行操作。**==
- **==`proxy`是 Vue3 实现响应式对象的基础！==**
- **Proxy 本身只会代理你传进去的对象这一层**。如果对象里面还有嵌套对象（子对象），**默认不会自动代理**。（所以Vue3会对嵌套对象递归调用`reactive()`）
***
## Object.defineProperty()
该方法可以在一个对象上定义一个新属性，或者修改一个对象的现有属性，并**返回这个对象。**
`Object.defineProperty(obj, key, descriptor)`
- `obj`：操作的对象
- `key`：要定义/修改的属性名称
- `descriptor`：属性描述符，是一个对象 
	- 属性描述符分为两类，他们是**互斥的**：
		- **数据描述符（Data Descriptor）**
			- `value`：属性的值
			- `writable`：是否允许修改
		- **存取描述符（Accessor Descriptor）**
		    - `get`：一个函数，在读取属性的时候调用 -> **必须要返回一个值**（变量名随便取）
		    - `set`：一个函数，在写入属性的时候调用
	- 通用属性：
		- `enumerable`：是否可枚举(`for...in...`)
		- `configurable`：布尔值，控制能否删除该属性、能否修改其属性描述符，默认为`false`
---
### defineProperty VS proxy：
- `defineProperty()`**只能重新定义对象属性的读取和设置，**`proxy`可以拦截到更多的操作。
- `defineProperty()`**只能拦截已有的属性**，后续添加的属性是不会被捕获到的。如果有新增的话要使用`Vue.set()`
- `defineProperty()`可以直接操作对象实例来触发拦截，`proxy`不能直接操作原有实例，需要操作`proxy`实例才能触发
---
