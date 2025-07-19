
## mapState 辅助函数：
### why : 
如果每个状态都需要定义一个计算属性来获取，就显得非常的重复和冗余，于是引入了 ==mapState== 辅助函数，用于简化状态的导入。
### 作用：
把 `store.state` 中的状态映射为组件中的 `computed` 属性。
- mapState函数返回一个对象，==对象中的每一个属性都是一个computed函数==
- mapState函数必须在`computed计算属性`中调用，并且需要在前面加上**展开运算符(...)**
### 用法：
常见用法一般有2种：
传入数组形式和对象形式
```js
import { mapState } from 'vuex'
export default {
	computed: {
		...mapState(['state1', 'state2'])//传入数组形式
		...mapState({//对象形式，可以选择对状态进行重命名
			stateAlias: state => state.state1
		})
		//在命名空模块中使用，需要首先包含模块的名称
		...mapState('user', ['name', 'email']),
	    ...mapState('cart', {
		    total: state => state.items.length
	    })
	}
}
```
## mapGetters 辅助函数：
### 作用：
将 Vuex 的 `getters` 映射为组件中的 `computed` 属性。
### 用法：
与 mapState 相同
```js
computed: {
  ...mapGetters(['isLoggedIn', 'cartTotal'])
  ...mapGetters({
    loggedIn: 'isLoggedIn',
    totalPrice: 'cartTotal'
  })
  //在命名空模块中使用，需要首先包含模块的名称
  ...mapGetters('user', ['isAdmin']),
  ...mapGetters('cart', {
    price: 'totalPrice'
  })
}
```
## mapMutations 辅助函数：
### 作用：
将 Vuex 的 `mutations` 映射为组件中的 `methods` 方法。
### 用法：
```js
methods: {
  ...mapMutations(['increment', 'setUser'])
  ...mapMutations({
    add: 'increment',
    updateUser: 'setUser'
  })
  //命名空间
  ...mapMutations('cart', ['addItem']),
  ...mapMutations('user', {
    updateName: 'setName'
  })
}
```
## mapActions 辅助函数：
### 作用：
将 Vuex 的 `actions` 映射为组件中的 `methods` 方法。
### 用法：
```js
methods: {
  ...mapActions(['login', 'logout'])
  ...mapActions({
    doLogin: 'login',
    quit: 'logout'
  })
  //命名空间
  ...mapActions('user', ['login', 'register']),
  ...mapActions('cart', {
    addProduct: 'addItem'
  })
}
```
