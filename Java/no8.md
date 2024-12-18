## Java学习笔记 lambda
---
### 1. 概念

&emsp;&emsp;lambda表达式就是一个代码块，以及必须传入代码的变量规范，相当于闭包。（带参数变量的表达式）

---
### 2. 写法

+ 基本形式：`(type name,type name2……)->{语句}`
+ 没有参数：`()->{语句}`
+ 可以推导出参数类型：`(name,name2)->{语句}`
+ 只有一个参数，且可以推导类型：`name->{语句}`
注意：单语句或者不需要返回的，不用写return语句。

---
### 3. lambda组成

1. 代码块
2. 参数
3. 自由变量的值（非参数，不在代码块中定义的变量）
    + lambda表达式可以捕获外围作用域中变量的值
    + lambda表达式中，**只能引用值不会改变的自由变量**（内部外部都不能改变）
    + lambda表达式内部与外围作用域相同
    + lambda表达式中的`this`指外围作用域的`this`

---
### 4. 传递给函数式接口

&emsp;&emsp;Lambda表达式可以传递给一个函数式接口，语句块实现函数式接口里的唯一抽象方法。

---
### 5. 方法引用
 
 + 格式：
    1. `对象::方法名`
    2. `类名::静态方法名`
    3. `类名::方法名` (则方法第一个参数传入隐式参数)
    4. `this::方法名`
    5. `super::方法名`
    6. `类名::new`
+ 用法：
    1. 方法应用可以自动转换为lambda表达式
    2. 进而可以作为传递给函数式接口使用



---
#### [返回目录](./)
