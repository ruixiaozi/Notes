## 数据结构学习笔记 基础概念
---
### 1. 数据结构

+ 数据（data）：对客观事物的符号表示，在计算机科学中是指所有能够输入到计算机中并被计算机程序处理的符号的总称。
+ 数据元素（data element）：数据的基本单位，在计算机程序中通常作为一个整体进行考虑好处理。
+ 数据对象（data object）：性质相同的数据元素的集合，是数据的一个子集。
+ 数据结构（data structure）：相互之间存在一种或多种特定关系的数据元素的集合。数据元素之间的关系称为结构（structure）。常用的4个基本结构：
    > 1. 集合
    > 2. 线性结构
    > 3. 树形结构
    > 4. 图形结构
+ 逻辑结构：结构中的逻辑关系。
+ 物理结构：数据结构在计算机中的表示，又称存储结构。一般分为顺序存储结构和链式存储结构。
+ 数据类型（data type）：用以刻画操作对象的特性。
+ 抽象数据类型（abstract data type，ADT）：数据模型以及定义在该模型上的一组操作。仅取决于逻辑特性，与其在计算机内部如何表示无关。ADT定义格式：
    ```
    ADT 抽象数据类型名{
        数据对象：<数据对象的定义>
        数据关系：<数据关系的定义>
        基本操作：
            操作方法名(参数列表)
                初始条件：<描述>
                操作结果：<描述>
            ……
    }ADT抽象数据类型名
    ```

---
### 2. 算法

&emsp;&emsp;算法是对特定问题求解步骤的一种描述（数据结构中的操作方法中涉及到算法的实现），它是指令的有限序列，具有5个特征：
1. 有穷性：总在执行有穷的步骤后结束，且每个步骤都在有穷时间内完成。
2. 确定性：每一条指令必须有确切的含义，且对于相同的输入只能得出相同的结果。
3. 可行性：一个算法是能使用的，可行的。
4. 输入：有零个或多个输入
5. 输出：有一个或多个输出

&emsp;&emsp;算法设计的要求（好算法）：
1. 正确性
2. 可读性
3. 健壮性 ：输入非法数据时，能够适当地做出反应何处理。
4. 效率和低存储量需求：时间和空间问题。

&emsp;&emsp;算法效率的度量（时间复杂度）：使用大O记法，表示随问题规模n的增大，算法执行时间的增长率何f(n)的增长率相同。

&emsp;&emsp;算法的存储空间度量（空间复杂度）：同样使用大O记法。

---
### 3. 总结

&emsp;&emsp;这个笔记主要学习的是数据结构的表示和实现，给出一个ADT，如何使用一种语言去表示何实现它，同时学习一定的基础算法。

---

#### [返回目录](./)

