#vue #响应式原理
- Vue2：`Object.defineProperty
- Vue3：`Proxy`

知识目录：
- `effect`
- `proxy`
- `track`
- `trigger`
- `scheduler`
- `cleanup`
- `lazy`
# Vue3:

```txt
大致流程：
读取属性 -> 触发proxy.get -> 触发track -> 依赖收集
设置属性 -> 触发proxy.set -> 触发trigger -> 依赖函数重新执行
```

## computed：
```js
function computed(getter) { 
	let value 
	let dirty = true
	const effectFn = effect(getter, {
		lazy: true,
		scheduler() {
			if (!dirty) { 
			 // 当计算属性依赖的响应式数据变化时，手动调用 trigger 函数触发响应
			 dirty = true  
			 trigger(obj, 'value')
			}
		}
	})  
	const obj = {
	  get value() {
	    if (dirty) {
	      value = effectFn()
	      dirty = false
	    }  // 当读取 value 时，手动调用 track 函数进行追踪 
		track(obj, 'value') 
		return value
		}
	}
	return obj
}
```
全流程：创建一个computed，并传入一个副作用函数，然后当副作用函数依赖的值变化的时候会触发trigger，随即触发scheduler，将dirty修改为true，由于lazy默认是true，所以此时值并不会变化，等到我需要用到computed的值的时候，get钩子触发，判断到dirty为true，随即触发我传入的副作用函数，重新计算并返回新的值，我的理解准确吗