## route VS router
`router` 是**路由控制器**，而`route` **是状态展示器**
### router：
`this.$router` 是==**路由器对象**==，是**Vue Router 的实例对象(==全局作用域==)**，对整个应用的路由有**控制权力**
### route：
`this.$route` 是一个==**普通对象**==，代表**当前**路由状态，一般用于获取当前的路由信息，包含 `path、query、params、meta `等参数。
***
## 路由参数相关
### params：
**动态路径参数**中的值被获取并保存在 `this.$route.params` 对象中。
==动态路径参数需要在**路由文件**中进行定义：==
```js
const route = [
	{
		path: '/user/:id/:info?',
		name: 'user',
		component: () => import('')
	}
]
```
路径参数可以被定义在路径的任意层级中，都可以在 `parms` 对象中获取到。
路径参数是**可选的**，定义时需要在后面加上**问号**。
当出现嵌套路由的时候，父子路由中的路径参数会被一并获取并合并到params对象中。
#### 参数的传入：
```js
this.$router.push({
	name: '',
	params: {id: },
	query: {},
})
```
#### 路由参数变化响应：
当用户以==不同路径参数访问同一个组件==时，Vue 会对这个组件进行复用以提高效率，需要注意的是：==复用组件的过程中不会触发 Vue生命周期的钩子函数。==
#### 将 params 传递给 props：
```js
const routes = [
  { path: '/user/:id', component: () => import(), props: true }
]
```
当 `props` 设置为 `true` 时，`route.params` 将被设置为组件的 props
***
### query：
查询参数**不需要在路由定义中声明，直接在 URL 中拼接**即可（参考[[Basic#参数的传入：|参数的传入]]）
查询参数会在url的最后拼接上：`/myurl?query1=xxx&query2=xxx`
**查询参数不会影响路由的匹配。**
### 通配符参数：
**用于捕获一系列符合要求的路径。**
#### 用法：
`/baseUrl/:pathMatch(.*)*`
以上路由会匹配到以`/baseUrl/`开头的所有路径。
`/:pathMatch(.*)*`
以上路由会匹配到所有路径，一般用在路由的最后用于兜底，捕获404not found的页面。
**解释：`(.*)*`:** 括号内可以填写任意正则表达式，括号外的\*表示匹配任意多层符合正则规则的路径。
***
## 嵌套路由相关
有几个注意事项：
1. 尽量避免使用默认子路由（即子路由的`path:''`)显式规定好路径，避免默认加载。
2. 给每个路由都规定好`name`属性。支持独立访问，便于跳转控制和参数传递。
---
## 跳转、替换与历史
使用`this.$router.push()`跳转会向 history 添加新纪录。
使用`this.$router.replace()`跳转==不会==向 history 添加新纪录。
### 历史：
使用`this.$router.go()`表示在历史堆栈中移动指定步数，正数表示向前，负数表示向后
***
## 历史模式
Vue Router 提供了三种路由模式，它们决定了 URL 是如何变化的，以及浏览器是如何响应这些变化的
- **Hash 模式**（默认）
- **History 模式**（HTML5 History API）
- **Memory 模式**（主要用于非浏览器环境，如 SSR、测试）
---
## 路由守卫：
路由守卫就是：**在页面跳转的过程中执行的钩子函数。**（类似于请求/响应拦截器）
### 参数：
每个守卫接受两个参数： `to` 和 `from`
- `to`：标识即将前往的路由地址
- `from`：标识当前正要离开的路由地址
### 返回值：
每个守卫可以返回以下类型的值：
- `undefined` 或者 `true`：表示导航有效，继续向前执行
- `false`：表示取消当前导航，url停留在`from`表示的路由上
- `一个新的路由地址`，表示重定向到一个新的路由地址，相当于调用了`router.push()`
### 完整的导航解析流程：
1. 导航被触发。
2. 在失活的组件里调用 `beforeRouteLeave` 守卫。
3. 调用全局的 `beforeEach` 守卫。
4. 在重用的组件里调用 `beforeRouteUpdate` 守卫。
5. 在路由配置里调用 `beforeEnter`。
6. 解析异步路由组件。
7. 在被激活的组件里调用 `beforeRouteEnter`。
8. 调用全局的 `beforeResolve` 守卫。
9. 导航被确认。
10. 调用全局的 `afterEach` 钩子（这个不是守卫，是钩子，不能干预导航）。
11. 触发 DOM 更新。
12. 调用 `beforeRouteEnter` 守卫中传给 `next` 的回调函数，创建好的组件实例会作为回调函数的参数传入。
### 各种类型的守卫：
#### 全局守卫：
==在路由实例上调用==
- `beforeEach(to, from, next)`                          导航开始前调用
- `beforeResolve(to, from, next)`                    所有守卫和异步组件解析完之后调用
- `afterEach(to, from)`                                        导航完成后调用
#### 路由独享守卫：
直接在路由配置中（某个具体 route 上），只作用于该路由，不影响其他页面，==**适用于页面独立权限**==
- `beforeEnter(to, from, next)`
#### 组件内守卫：
写在页面组件（`.vue` 文件）内部，更贴近组件本身的生命周期，适合控制**组件的进入、更新、离开行为**
- `beforeRouteEnter(to, from, next)`
- `beforeRouteUpdate(to, from, next)`
- `beforeRouteLeave(to, from, next)`
***
## 元信息(meta)
`meta` 是 Vue Router 中定义在**每个路由记录**上的一个字段（每个路由**独有的**信息存储仓库），它**不会影响路由本身的匹配或跳转逻辑**。它就是路由对象里的一个自由的数据结构字段，开发者可以**存放任意信息**，并在守卫、组件等地方访问使用。
### 使用：
#### 在守卫中使用：
```js
router.beforeEach((to, from, next) => {
  to.meta.myData... //通过 to.meta 来访问
  next()
})
```
#### 在组件中使用：
```js
const myData = this.$route.meta.data //通过 route 对象来访问
```
### 常见用法：
- 权限控制（访问当前页面是否需要登录、定义允许访问的用户类型）
- 页面展示控制（存放title、icon、是否展示导航栏/其他组件...）
- 缓存控制、标签页控制（`keepAlive`字段，`multiTab`字段）
- 面包屑（存放当前页面的面包屑数据）
- 动画控制（存放动画类型）
- 任何自定义数据结构（只要满足需求即可）




