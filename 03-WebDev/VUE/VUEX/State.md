**state 用于存储全局共享数据（数据是响应式的，可读的）**
## 在组件中获取Vuex状态：

从 store 实例中读取状态最简单的方法就是在==计算属性==中返回某个状态：
==一般都会把store全局注册在Vue根实例中，子组件可以通过 **this.$store** 访问到==
```vue
computed: {
    count () {
      return this.$store.state.count
    }
  }
```

