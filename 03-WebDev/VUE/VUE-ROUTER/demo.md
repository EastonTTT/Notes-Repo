这里对一个功能全面的路由模块应该有的部分做一个整体的说明。
```bash
src/
├── router/
│   ├── index.ts             # 路由主入口
│   ├── routes.ts            # 所有路由配置
│   └── guards.ts            # 全局守卫定义
├── views/
│   ├── Home.vue
```
- 在`routes.ts`里集中定义路由（如果路由数量多，可以再进行细分，然后统一导入到`routes.ts`里面
- 在`guards.ts`里定义全局守卫（登录、权限控制、页面标题设置等）
-  