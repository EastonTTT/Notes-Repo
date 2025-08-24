#js-object对象  
## entries & fromentries ：
### entries
方法：`Object.entries(obj)`
**作用**：`对象 -> 数组` 把对象的**可枚举属性**转成一个二维数组，每个元素是 `[key, value]` 形式。
- **参数**：`obj`（要转换的对象）
- **返回值**：`Array`，数组元素形如 `[key, value]`
---
### fromentries
方法：`Object.fromentries(iterable)
**作用**：`数组 -> 对象` 把一个形如 `[key, value]` 的二维数组（或任何可迭代对象）转换回对象。==是`Object.entries()`函数的逆操作。==
- **参数**：`iterable`（必须是可迭代对象，且每个元素都是 `[key, value]` 的形式）
- **返回值**：`Object`
***
### assign
`Object.assign()`是用于对象合并、属性复制的方法。
用法：`Object.assign(target,source1,source2...)
- 会把所有`source`对象的**可枚举属性**都复制到`target`对象上。
- `target`对象上的**同名属性会被覆盖**
- 会在`target`对象本身上进行修改。**返回target对象**
- 复制是**浅拷贝**，他不会递归的拷贝嵌套的对象，只是**复制引用**
- 目标为`null,undefined`的时候会报错
---
