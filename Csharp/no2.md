## C#学习笔记 程序结构

---

### 1. Hello World

一个 C# 程序主要包括以下部分：

1. 引入需要使用的命名空间
2. 声明本文件的命名空间（Namespace declaration）
3. 定义一个入口类(class)
4. 定义其他 Class 成员方法
5. Class 属性
6. 定义入口 Main 方法
7. 语句（Statements）& 表达式（Expressions）
8. 程序注释

```
using System;
namespace HelloWorldApplication
{
   class HelloWorld
   {
      static void Main(string[] args)
      {
         /* 我的第一个 C# 程序*/
         Console.WriteLine("Hello 简单教程");
         Console.ReadKey();
      }
   }
}
```





---

#### [返回目录](./)