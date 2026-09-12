```
Schema（规则/蓝图）
	       ↓ 编译
Model（操作数据库的类）
        ↓ 创建或查询
Document（具体的一条数据）
        ↓ 保存
MongoDB Collection（集合）
```

## Schema：
用于定义表结构。
提供以下能力：
- 数据类型定义
- 数据校验能力
- 静态方法（对应的Model调用）
- 实例方法（对应的Document调用）
- 虚拟字段（运行时动态计算，类似computed）
- 钩子函数（数据操作前后触发）
- 对查询结果进行处理
## Model：
表的类，用于操作表。
提供以下能力：
- CRUD
- 支持链式查询：`.find().sort().limit()`
## Document：
表的一条数据。
