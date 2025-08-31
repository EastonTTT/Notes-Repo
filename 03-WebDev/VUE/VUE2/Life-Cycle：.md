总共有八个钩子：
- beforeCreate
- created
- beforeMount
- mounted
- beforeUpdate
- updated
- beforeDestroy
- destroyed
---
**Vue2的生命周期分为四个阶段：**
创建阶段：
  beforeCreate  →  created
       ↓
挂载阶段：
  beforeMount   →  mounted
       ↓
运行阶段（响应式更新）：
  beforeUpdate  →  updated（会多次执行）
       ↓
销毁阶段：
  beforeDestroy →  destroyed
***
## 钩子用法：
### `created：
**含义**：实例已创建，数据已初始化，但 DOM 还未挂载。
**常见用途**：  
- 可以访问 `data`、`methods`  
- 可以发送请求、初始化数据  
- 不能操作 DOM
***
