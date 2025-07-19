Getter 就像计算属性`computed`，可以根据 state 派生出一些值，**用于封装计算逻辑、避免模板中出现复杂表达式**
## 定义：
Getter接受一个state作为参数。
```js
const store = new Vuex.Store({
  state: {
    todos: [
      { id: 1, text: '...', done: true },
      { id: 2, text: '...', done: false }
    ]
  },
  getters: {
    doneTodos: state => {
      return state.todos.filter(todo => todo.done)
    }
    // getter也可以返回一个函数
	getTodoById: (state) => (id) => {
	    return state.todos.find(todo => todo.id === id)
	}
  }
})
```
## 访问：
-  通过store对象属性的形式访问：`store.getter.myGetter`
