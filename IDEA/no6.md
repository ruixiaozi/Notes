## IDEA学习笔记 实时代码模板
---
### 1. 设置

`Editor` -> `Live Templates` 里面可以设置实时代码模板，或者在`Editor` -> `General` -> `Postfix Completion`

---
### 2. 创建自定义模板

点击 `+` 号可以创建

+ `Abbreviation` 模板调用命令名
+ `Description` 描述
+ `Template text` 代码
+ 最下面要勾选应用范围：Java -> statement

其中`Tempalate Text`中可以使用一对`$`包裹一个变量，在调用的时候光标会自动在变量位置，按tab跳转变量输入。`$END$`为特殊的变量，表示最后输入光标的位置。

---
#### [返回目录](./)
