## JavaScript学习笔记 基本语法
---
### 1. 总述

&emsp;&emsp;主要介绍ECMAScript基本语法，因为其语法大量借鉴了C和其他类C语言的语法，本部分只记录一些特殊之处。

---
### 2. 变量

&emsp;&emsp;ECMAScript的变量是松散类型的，可以保存任何类型的数据。每一个变量仅仅只是一个用于保存值的占位符。定义变量时使用 `var` 操作符，后面跟一个变量名。未初始化的变量会保存一个特殊值 `undefined` 。

&emsp;&emsp;注意：可以省略 `var` 标示符，但是**在定义局部变量的时候，如果不使用 `var` 操作符，就会创建或更改一个全局变量**，所以**建议一直使用 `var` 操作符**。

---
### 3. 数据类型

&emsp;&emsp;ECMAScript有5种基本数据类型：`Undefined` , `Null` , `Boolean` , `Number` , `String` 。还有1种复杂数据类型：`Object`。所有值都是这6种数据类型其中之一。

&emsp;&emsp;可以使用 `typeof` 操作符来检测变量的数据类型。对一个值使用 `typeof` 操作符可以返回以下字符串之一（操作符后可用括号，但不是必须，返回的字符串和上述数据类型不一定一样）：
+ "undefined"：未定义
+ "boolean"：布尔值
+ "string"：字符串
+ "number"：数值
+ "object": 对象或者**null**
+ "function"：函数

&emsp;&emsp;以下对各个类型进行说明：
1. Undefined 类型  
    Undefined类型只有一个值就是：`undefined`，未初始化的变量默认值为它。主要用于比较一个变量是不是该值。**最好使用 `typeof` 操作符**。
2. Null 类型  
    Null类型也只有一个值就是：`null`，但是在使用 `typeof` 操作符的时候会返回 "object" 字符串。需要注意，所以在一个变量将来要用做保存对象的时候，可以先给这个变量初始化为 `null` 值，这样检测的时候就知道是对象变量了。**`undefined` 值派生自 `null`，但是用途不同**。
3. Boolean 类型  
    Boolean类型只有两个值：`true` 和 `false`。需要注意的是：这两个值与数字 `1` 和 `0` 不相等，但是可以使用转型函数 `Boolean()`将其他类型转换到对应的布尔值。

---

#### [返回目录](./)