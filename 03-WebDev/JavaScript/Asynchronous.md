#js异步
## promise：
`Promise` 是一个对象，它代表了一个**异步操作的最终完成或者失败**
`Promise`有三种状态：
- `pending`：待定状态
- `fulfilled`：已成功
- `rejected`：已失败
	- 其中`fulfilled` 和 `rejected` 统称`settled/resolved`态 
**`Promise`的状态是不可逆的，==一旦确定就没有办法再改变。==**
---
`Promise`的缺点：
- `Promise`一旦开始执行，在没有得到结果之前是没有办法中途取消的。
- `Promise`只能有一个完成值或者拒绝原因。
- 在`pending`状态时是无法得知具体进度的。
```js
const p = new Promise(excutor)//excutor 是一个同步函数，会在promise创建的时候立即执行。
const p = new Promise((resolve,reject) => {
	//在里面执行异步操作...
})
p.then(data => {
	//对数据执行的其他操作...
}).catch(err => {
}).finally()
```
---
### 相关方法：
#### `Promise.all()`：
该方法接受一个数组作为参数，数组内的成员都是`Promise`实例，如果不是的话会先使用`promise.resolve()`将参数转化为`Promise`。返回一个`Promise`对象。该对象只有在数组内所有`Promise`都成功执行之后才会触发成功。所有`Promise`都执行成功之后会返回一个数组，存放着所有`Promise`执行的结果。
一旦有任何一个`Promise`执行失败，则返回一个失败的`Promise`。
***
#### `Promise.allSettled`:
接受一个数组为参数，等到数组内的所有`Promise`的状态都`settled`之后才返回。返回一个数组，包含所有`Promise`执行的结果。
***
#### `Promise.race()`
接受一个数组作为参数，返回状态最早`settled`的`Promise`的结果，无论成功还是失败。

