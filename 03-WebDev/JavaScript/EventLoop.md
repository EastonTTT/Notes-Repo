#js事件循环
运行模型如下：
```text
[ 主线程运行 script（宏任务） ]
	↓ 
[ 执行所有的微任务队列 ]
	↓
[ 渲染阶段（如果有渲染任务触发）]
	 ↓
[ 执行下一个宏任务 ]
```
### 渲染阶段：
渲染阶段触发条件：==**一轮宏任务完成 + 微任务队列清空 + 触发了DOM、样式、布局变更**==
常见api：`requestAnimationFrame(callback)`
执行阶段：==**宏任务执行完毕+清空微任务队列之后**==
***
### 常见宏任务(**macro-task**)：
- script(整体代码)
- setTimeout
- setInterval
- setImmediate(Node 环境)
- I/O，事件队列 （如fs、http等Node.js模块的回调函数）
- postMessage（web worker）
---
### 常见微任务(**micro-task**)
- `Promise.then/catch/finally`  回调
- Async 中 Await 的回调(实际就是 promise 的回调)
- `queueMicrotask()`：是一个 **浏览器/Node 提供的原生 API**，用于**向微任务队列中添加一个任务（callback）**。会在当前执行栈清空之后、**所有同步代码之后、下一个宏任务之前**执行。