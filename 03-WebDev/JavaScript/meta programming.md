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
- `get`
- `set`
- `has`
- `apply`
- 