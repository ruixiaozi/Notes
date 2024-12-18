## Java学习笔记 类
---
### 1. 访问修饰符  

| 修饰符 | 说明 |
| :-----| :---- | 
| 默认 | 本包可见 | 
| private | 本类可见 | 
| protected | 本包和所有子类可见 | 
| public | 所有类可见 | 

---
### 2. 静态域 静态方法

+ 公共静态常量  
    静态域通常声明成`公共静态常量`，标示符使用全大写。  
    `public static final ……`

+ 静态方法  
    1. 静态方法只可以访问静态域
    2. 静态方法可以直接从类调用

---
### 3. 隐式参数 显式参数  

+ 隐式参数  
    `this`代表隐式参数，指向当前对象

+ 显式参数  
    方法实际参入的参数

---
### 4. 重载  

+ 方法签名：方法名 与 参数类型
+ 重载：相同方法名，不同参数就产生了重载
+ 重载解析：匹配方法名与最适合的参数类型

---
### 5. 对象初始化

1. 域被初始化为默认值
2. 按顺序，执行域初始化语句和初始化块
3. 如果调用了其他构造器(使用this作为方法名，出现在构造器首行)，则执行其他构造器
4. 执行本构造器


---
### 6. 类加载

1. 静态域被初始化为默认值
2. 按顺序执行静态域初始化语句
3. 静态初始化块

---
### 7. 析构 

&emsp;&emsp;添加`finalize`方法，实现析构

---
### 8. 继承  

+ 子类继承父类所有域和方法
+ super关键字：
    1. 使用`super`关键字，可以访问指向父类，调用父类的公共属性和方法。
    2. 构造器中，第一行使用`super`作为方法名，可以调用父类构造方法。（默认会调用父类无参构造方法）
+ 重写：子类可以覆盖父类的方法，不能低于超类方法的可见性，不能覆盖static或者private修饰的类
+ 阻止继承：final类和final方法
+ 内链方法：简短、频繁调用、没有被重写

---
### 9. 多态

+ 多态：对象变量可以指向多种实际类型
+ 动态绑定：运行时，自动选择调用哪个方法（经过重写的方法）
+ 方法调用过程：
    1. 检查对象声明类型、方法名
    2. 参数类型
    3. 静态绑定
    4. 动态绑定

---
### 10. 抽象类  

+ 抽象方法：使用`abstract`关键字声明方法，且没有方法定义
+ 抽象类：包含一个或多个抽象方法的类本身也必须声明为抽象的，没有抽象方法也可以声明为抽象的。无法实例化，但可以定义抽象类变量。
+ 继承抽象类：
    1. 没有定义全部抽象方法，也声明为抽象类
    2. 定义全部抽象方法，声明为普通类

---
### 11. 枚举类

+ 定义：把`class`换成`enum`就可以定义枚举类，也是一种类
+ 枚举常量：在枚举类首行中直接定义的标示符，用逗号隔开
+ 可以添加普通域和构造器、方法

---
### 12. 内部类

+ 特点：
    1. 可以直接访问该类所在作用域中的数据，包括私有域
    2. 与域、方法有相同的访问修饰符
    4. 匿名内部类可以实现接口，作为回调块
    5. 尽量不使用静态方法，因为写在内部类里没有什么意义
+ 格式：
    1. 放在类块里面
    2. 与定义普通类一样，但可以为私有类

---
### 13. 局部内部类

+ 特点：
    1. 不能使用访问修饰符，作用域限制在局部块里
    2. 可以访问局部变量，但必须是final

---
### 14. 匿名内部类

+ 定义：如果创建的类马上就使用，且只用创建一个对象。就没必要命名了。这种称谓匿名内部类。
+ 格式：
    ```
    new 父类/接口(父类构造器参数)
    {
        域、方法、初始化块定义
    }
    ```
+ 用途：
    1. 可以代替lambda表达式，传递给函数式接口等
    2. 创建一个数组列表：
        ```
        //匿名内部类，ArrayList的子类
        new ArrayList<String>(){
            {   //初始化块，调用add方法
                add("a");
                add("b");
            }
        }
        ```
---
### 15. 静态内部类

+ 特点：
    1. 只有内部类可以是静态
    2. 相当于二级类，使用`.`访问
    3. 可以有静态域和方法
    4. 接口中的内部类，自动为`public static`静态内部类

---

#### [返回目录](./)
