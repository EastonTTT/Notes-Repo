#零碎知识点合集 #常看常新 #Vue
> [!note] ps:
> 这篇笔记用于记录一些难以归类、较为零碎的知识点。
## $event 手动传递：
#vue中event事件传递  
当触发事件时，如果绑定了函数（没有调用传参）则Vue会默认传递event参数，在绑定函数中声明后使用即可，如果使用了函数传参调用，此时需要用到event事件对象时，就需要在函数中通过 $event 的形式传递。
***
## 关于 \<template> 标签：
#template标签
### 定义：
`<template>` 是一个 **“抽象标签”** ，用于在渲染时包裹多个元素或模板内容，但本身**不会渲染为任何 DOM 节点**。只作为一种**逻辑容器**

它是 HTML 标准中的标签，Vue 利用了它的“**不渲染性**”特性，作为一种**逻辑容器**，服务于条件渲染、列表渲染、插槽等机制。
### 用法
1. 作为vue组件HTML模版部分的==根容器==（最普遍）
2. 在 `v-if` / `v-else-if` / `v-else` 中包裹多个元素
3. 在 `v-for` 中批量渲染多个元素
4. 作用域插槽（scoped slots）时必用 `<template>`
5. **其余场景中应该少用/不用 `<template>` 标签**（因为没有任何意义）
==examples: ==
<template v-if="isLoggedIn">
  <p>Welcome back!</p>
  <button @click="logout">Logout</button>
</template>
<template v-else>
  <p>Please log in</p>
</template>
<template v-if="isLoggedIn">
  <p>Welcome back!</p>
  <button @click="logout">Logout</button>
</template>
<template v-else>
  <p>Please log in</p>
</template>
<template v-if="isLoggedIn">
  <p>Welcome back!</p>
  <button @click="logout">Logout</button>
</template>
<template v-else>
  <p>Please log in</p>
</template>
<template v-if="isLoggedIn">
  <p>Welcome back!</p>
  <button @click="logout">Logout</button>
</template>
<template v-else>
  <p>Please log in</p>
</template>
<template v-if="isLoggedIn">
  <p>Welcome back!</p>
  <button @click="logout">Logout</button>
</template>
<template v-else>
  <p>Please log in</p>
</template>
<template v-if="isLoggedIn">
  <p>Welcome back!</p>
  <button @click="logout">Logout</button>
</template>
<template v-else>
  <p>Please log in</p>
</template>
<template v-if="isLoggedIn">
  <p>Welcome back!</p>
  <button @click="logout">Logout</button>
</template>
<template v-else>
  <p>Please log in</p>
</template>
<template v-if="isLoggedIn">
  <p>Welcome back!</p>
  <button @click="logout">Logout</button>
</template>
<template v-else>
  <p>Please log in</p>
</template>
<template v-if="isLoggedIn">
  <p>Welcome back!</p>
  <button @click="logout">Logout</button>
</template>
```vue
<!-- 用于v-if逻辑中 -->
<template v-if="xxx">
  <p>yes</p>
</template>
<template v-else>
  <p>no</p>
</template>
<!-- 用于v-for逻辑中 -->
<template v-for="item in items" :key="item.id">
  <div>{{ item.info }}</div>
</template>

```
---
##  watch首个参数是函数：
#watch
`watch`函数的第一个参数需要是函数形式 ，如果想监听指定变量的变化，则需要传入一个 getter 函数。
e.g. `watch (() => this.$route.params.id, callback)`
**本质原因**：Vue会在执行传入的函数的过程中==跟踪所有响应式依赖，在依赖改变时重新调用callback函数。==
因为当你传入一个变量的时候，**他只会被当作是一个值，而值是不会变化的，所以没有办法监听到变化。**
***
