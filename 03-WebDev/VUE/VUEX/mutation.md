==提交mutation是修改store中状态的**唯一方式！** mutation是同步执行的(mutation不能包含异步操作！)==
## 定义：
mutation接受一个 **state** 作为参数：
```js
const store = new Vuex.Store({
	state: {
	},
	mutations:{
		change(state){
		}
	}
})
```
## 触发：
- 使用 `this.$store.commit('模块名/函数名',载荷)` 
	e.g. this.$store.commit(module/func, payload) payload建议是对象，也可以是值
- 使用`mapMutations`方法进行映射，之后像普通函数一样使用mutation即可。