-  action用于提交mutation，并非直接对state进行修改
- action 可以包含异步操作（可以用async/await）
- action函数接受一个与store对象有相同属性和方法的context对象作为参数，可以调用context 的 commit 方法来触发 mutation（一般会把commit方法解构出来）
## 定义：
```js
action: {
	myAction({commit,state}，payload){
		commit('myMutation')
		...
	}
}
```
## 触发：
- 直接使用 `this.$store.dispatch('module/actionName')`
- 或者通过mapActions辅助函数进行映射。