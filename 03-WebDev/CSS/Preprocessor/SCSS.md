#css #scss
**SCSS是一个CSS的预处理器、也是CSS的拓展语言。**
## 嵌套规则
### 样式嵌套
Sass 允许将一套 CSS 样式嵌套进另一套样式中，==内层的样式将它外层的选择器作为父选择器。==
在嵌套 CSS 规则时，有时也需要直接使用嵌套外层的父选择器，例如，当给某个元素设定 `hover` 样式时，可以用 `&` 代表嵌套规则外层的父选择器。
**注意⚠️**：当在多层嵌套的结构内部使用 `&` 时，拼接得到的不是当前层的父选择器，而是从==最外层一直拼接到当前层==得到的完整路径。
***
### 属性嵌套
有些css属性有着相同的公共前缀（比如`font-size`  `font-family` `font-weight` 以及`border-xxx`）可以把公共前缀提取出来做一层嵌套：
```css
font: {
	family: xxx;
	size: 16px;
	weight: bold;
}
```
---
## 注释规则
scss支持两种注释形式：
- 多行注释（`/*   */`）
- 单行注释（`//`）
其中多行注释会被包含在 ==*编译后*== 的文件里，而单行注释则会被忽略。
---
## 变量
### 声明与使用
变量的定义遵循格式：`$variable: value;`
变量的使用：$符号 ➕ 变量名称
作用域规则：
- 如果定义在顶部（或者不在块的内部）则为全局作用域 ==在本 scss 文件 或 当前 vue 组件内全局可用。==
- 如果定义在 `{}` 内部，则只在块内生效。
---
### 可用的数据类型
- 数字，`1, 2, 13, 10px`
- 字符串，有引号字符串与无引号字符串，`"foo", 'bar', baz`
- 颜色，`blue, #04a3f9, rgba(255,0,0,0.5)`
- 布尔型，`true, false`
- 空值，`null`
- 数组 (list)，用空格或逗号作分隔符，`1.5em 1em 0 2em`==（支持混合数据类型）==
- maps, 相当于 JavaScript 的 object，`(key1: value1, key2: value2)`
---
## 运算

---
## 继承(@extend)
==extend需要慎用，尽量使用mixin==
### 本质：
extend操作本质上是：让一个选择器“继承”另一个选择器的样式，同时**合并它出现过的所有位置（选择器合并）**。
	效果上：假设样式B继承了样式A。那么：让 `.B` 享受 `.A` 的样式，并且出现在**所有包含 `.A` 的地方**。==即所有包含`.A`的位置都会自动添加上 `.B`==（会把新类注入到所有被继承类出现过的位置，可能会带来样式的污染，破坏样式的独立性）
### 用法：
```css
.A {
  border: 1px solid white;
  background-color: gray;
}
.B {
  @extend .A;
  border-width: 2px;
}
```
***
## 混合(@mixin)
mixin指令用于定义==可重用的样式集（相当于一个模版）==，通过在其他样式集==使用 `@include`指令==来对混合样式进行引用==（把模版里的样式复制到引用区域里）==
**mixin是可以嵌套使用的。**
### 定义与使用：
```scss
@mixin my-mixin {
	background-color: white;
	font-size: 1.2em;
}

.use-mixin{
	@include my-mixin;
	display: flex;
}
//编译后得到的结果:
.use-mixin{
	background-color: white;
	font-size: 1.2em;
	display: flex;
}
```
### 添加参数：
**mixin可以给参数设置默认值。**
```scss
@mixin my-mixin($width: 200px, $height: 400px) {
	width: $width;
	height: $height;
}
//使用:
.my-size {
	@include my-mixin(100px,200px);
}
```
---
## 函数
- 使用`@function` 关键字定义，`@return`返回==一个单一值==。
- 可以包含`@if` `@else if` `@else`的逻辑操作。
- 函数可以使用定义好的全局变量。
### 定义与使用：
```scss
//用于单位转换的函数:
@function rem ($font-size, $base: 16){
	@return $font-size / $base * 1rem
}

//使用:
.use-function {
	width: rem(24) //24px -> 1.5rem
}
```
---
## 循环与条件控制
