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
