## Java学习笔记 代理
---
### 1. 概念  

&emsp;&emsp;动态代理提供了在运行时创建一个实现了一组给定接口的新类。

---
### 2. 调用处理器  

&emsp;&emsp;调用处理器用来进行对代理对象的方法拦截和处理。需要实现`InvocationHandler`接口，并实现`invoke`方法：
```
Object invoke(Object proxy,Method method,Object[] args)
//代理对象，方法，参数列表，返回值为方法返回值
```

---
### 3. 创建代理对象

&emsp;&emsp;通过类加载器、一组接口、调用处理器来创建一个代理对象，这个代理对象就是这一组接口的实例，并且所有方法都被调用处理器`invoke`方法拦截处理。使用`Proxy.newProxyInstance`创建：
```
static Object Proxy.newProxyInstance(ClassLoader loader,Class[] interfaces,InvocationHandler handler)
```



---
#### [返回目录](./)
