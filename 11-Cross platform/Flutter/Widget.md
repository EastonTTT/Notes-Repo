## Flutter的渲染过程：
1. 根据`widget`树，生成对应的`element`树，树中的每个节点都继承自`Element`类
2. 根据`element`树，生成对应的`render`树，树中的每个节点都继承自`RenderObject`类
3. 根据渲染树生成 `Layer` 树，然后上屏显示，树中的节点都继承自 `Layer` 类。
==真正的布局和渲染逻辑在 **Render 树**中，Element 是 Widget 和 RenderObject 的粘合剂，可以理解为一个中间代理。==
举个例子：
![[Pasted image 20251215201350.png]]
