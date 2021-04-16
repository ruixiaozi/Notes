## C#学习笔记 关键字与数据类型

---

### 1. 关键字

### 保留关键字和上下文关键字

C# 总共有 79 个保留关键字和 18 个上下文关键字

这两张表列出了 C# 中的保留关键字（Reserved Keywords）和上下文关键字（Contextual Keywords）：

| *保留关键字* |           |          |            |                        |                       |         |
| ------------ | --------- | -------- | ---------- | ---------------------- | --------------------- | ------- |
| abstract     | as        | base     | bool       | break                  | byte                  | case    |
| catch        | char      | checked  | class      | const                  | continue              | decimal |
| default      | delegate  | do       | double     | else                   | enum                  | event   |
| explicit     | extern    | false    | finally    | fixed                  | float                 | for     |
| foreach      | goto      | if       | implicit   | in                     | in (generic modifier) | int     |
| interface    | internal  | is       | lock       | long                   | namespace             | new     |
| null         | object    | operator | out        | out (generic modifier) | override              | params  |
| private      | protected | public   | readonly   | ref                    | return                | sbyte   |
| sealed       | short     | sizeof   | stackalloc | static                 | string                | struct  |
| switch       | this      | throw    | true       | try                    | typeof                | uint    |
| ulong        | unchecked | unsafe   | ushort     | using                  | virtual               | void    |
| volatile     | while     |          |            |                        |                       |         |

| *上下文关键字* |                |                  |            |         |      |
| -------------- | -------------- | ---------------- | ---------- | ------- | ---- |
| add            | alias          | ascending        | descending | dynamic | from |
| get            | global         | group            | into       | join    | let  |
| orderby        | partial (type) | partial (method) | remove     | select  | set  |



### 2. 数据类型

在 C# 中，变量分为以下几种类型：

- 值类型（Value types）
- 引用类型（Reference types）
- 指针类型（Pointer types）

1. **值类型**

   值类型变量可以直接分配给一个值。 它们是从类 **System.ValueType** 中派生的。

   C# 2010 中可用的值类型：

   | 类型    | 描述                                 | 范围                                                  | 默认值 |
   | ------- | ------------------------------------ | ----------------------------------------------------- | ------ |
   | bool    | 布尔值                               | True 或 False                                         | False  |
   | byte    | 8 位无符号整数                       | 0 到 255                                              | 0      |
   | char    | 16 位 Unicode 字符                   | U +0000 到 U +ffff                                    | '\0'   |
   | decimal | 128 位精确的十进制值，28-29 有效位数 | (-7.9 x 1028 到 7.9 x 1028)/ 100 到 28                | 0.0M   |
   | double  | 64 位双精度浮点型                    | (+/-)5.0 x 10-324 到 (+/-)1.7 x 10308                 | 0.0D   |
   | float   | 32 位单精度浮点型                    | -3.4 x 1038 到 + 3.4 x 1038                           | 0.0F   |
   | int     | 32 位有符号整数类型                  | -2,147,483,648 到 2,147,483,647                       | 0      |
   | long    | 64 位有符号整数类型                  | -923,372,036,854,775,808 到 9,223,372,036,854,775,807 | 0L     |
   | sbyte   | 8 位有符号整数类型                   | -128 到 127                                           | 0      |
   | short   | 16 位有符号整数类型                  | -32,768 到 32,767                                     | 0      |
   | uint    | 32 位无符号整数类型                  | 0 到 4,294,967,295                                    | 0      |
   | ulong   | 64 位无符号整数类型                  | 0 到 18,446,744,073,709,551,615                       | 0      |
   | ushort  | 16 位无符号整数类型                  | 0 到 65,535                                           | 0      |

   如需得到一个类型或一个变量在特定平台上的准确尺寸，可以使用 **sizeof** 方法。 表达式 *sizeof(type)* 产生以字节为单位存储对象或类型的存储尺寸。

2. **引用类型**

   引用类型的值不是存储在变量中的实际数据，他们存储的是实际数据的内存地址。

   **内置的** 引用类型有： **Object**、 **Dynamic** 和 **String**。

   + Object类型

     所有数据类型的终极基类。

     自动装箱和拆箱：

     ```
     int val = 8;
     Object obj = val;//先装箱
     int nval = （int）obj;//再拆箱
     ```

   + Dynamic类型

     动态类型与对象类型相似，但是对象类型变量的类型检查是在编译时发生的，而动态类型变量的类型检查是在运行时发生的。

   + String类型

     允许您给变量分配任何字符串值。字符串（String）类型的值可以通过两种形式进行分配：引号和 @引号。

     ```
     String str = "简单教程";
     ```

     C# string 字符串的前面可以加 @（称作"逐字字符串"）将转义字符（\）当作普通字符对待，比如(两行代码等价):

     ```
     string str = @"C:\Windows";
     string str = "C:\\Windows";
     ```

     @ 字符串中可以任意换行，换行符及缩进空格都计算在字符串长度之内。

     ```
     string str = @"<script type=""text/javascript"">
         <!--
         -->;
     </script>";
     ```

3. **指针类型**

   C# 中的指针与 C 或 C++ 中的指针有相同的功能。 声明指针类型的语法：

   ```
   type* identifier;
   ```





---

#### [返回目录](./)