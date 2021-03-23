## JavaScript学习笔记 基本概念
---
### 1. JavaScript实现

&emsp;&emsp;一个完整的JavaScript实现由三部分组成:  
+ 核心(ECMAScript)  
    ECMAScript 与Web浏览器没有依赖关系，只定义来这门语言的基础。
    
+ 文档对象模型(DOM)  
    DOM是针对XML但经过扩展用于HTML的API。DOM把整个页面映射为一个
    
+ 浏览器对象模型(BOM)  
    开发人员使用BOM可以控制浏览器显示的页面以外的部分
    
    ![](./img/图片11.png)

---
### 2. HTML的文档模式

&emsp;&emsp;HTML的文档模式分为：混杂模式和标准模式。其中混杂模式会让浏览器的css、js特性与标准不尽相同，而标准模式则尽可能与标准相同。我们主要使用标准模式，后来还衍生了准标准模式。

&emsp;&emsp;声明文档模式，需要使用<!DOCTYPE>，<!DOCTYPE> 声明不是 HTML 标签；它是指示 web 浏览器关于页面使用哪个 HTML 版本进行编写的指令。  
&emsp;&emsp;在 HTML 4.01 中，<!DOCTYPE> 声明引用 DTD，因为 HTML 4.01 基于 SGML。DTD 规定了标记语言的规则，这样浏览器才能正确地呈现内容。  
&emsp;&emsp;HTML5 不基于 SGML，所以不需要引用 DTD。

1. 标准模式  
    可以使用下面的方式开启：
    + HTML 4.01 严格型
        ```
        <!DOCTYPE HTML PUBLIC "-//W3C//DTD HTML 4.01//EN" 
        "http://www.w3.org/TR/html4/strict.dtd">
        ```
        包含所有 HTML 元素和属性，但不包括展示性的和弃用的元素（比如 font）。不允许框架集（Framesets）。
    + HTML 5
        ```
        <!DOCTYPE html>
        ```
2. 准标准模式
    可以使用下面的方式开启：  
    + HTML 4.01 过度型
        ```
        <!DOCTYPE HTML PUBLIC "-//W3C//DTD HTML 4.01 Transitional//EN" 
        "http://www.w3.org/TR/html4/loose.dtd">
        ```
        包含所有 HTML 元素和属性，包括展示性的和弃用的元素（比如 font）。不允许框架集（Framesets）。
    + HTML 4.01 框架集型
        ```
        <!DOCTYPE HTML PUBLIC "-//W3C//DTD HTML 4.01 Frameset//EN" 
        "http://www.w3.org/TR/html4/frameset.dtd">
        ```
        等同于 HTML 4.01 过度型，但允许框架集内容

---
### 3. 在HTML中使用JavaScript

&emsp;&emsp;可以使用 `<script>` 标签来向HTML页面中插入JavaScript，需要注意的是该标签应该被放在 `<body>` 元素中页面内容的后面，这样在下载和解析JavaScript代码之前，可以将页面的内容完全呈现出来。各个JavaScript脚本按照在从上到下的顺序依次执行，除非使用 `async` 或者 `deger` 属性。

&emsp;&emsp;该标签有以下6个属性：
1. async  
    可选。只适用于外部脚本，立即下载该文件。其目的是不让页面等待脚本下载，异步加载页面，**脚本的先后执行顺序无法确定**。
2. charset  
    可选。也是适用于外部脚本，指定代码的字符集。大部分浏览器忽略它，所以不重要。
3. defer  
    可选。也是适用于外部脚本，表示可以先下载，但是需要文档完全被解析和显示出来以后再执行。
4. language  
    已废弃。
5. src  
    可选。指定外部脚本的地址。
6. type  
    可选。表示代码使用的脚本语言类型（MIME类型）。这个值也同样不是必须的，可以不填，默认就是指JavaScript。

---
### 4. 不支持JavaScript时的备选策略

&emsp;&emsp;当浏览器不支持JavaScript或者被禁用了JavaScript时，可以使用 `<noscript>` 标签来显示一段内容，这段内容仅在JavaScript不被使用时显示。

---

#### [返回目录](./)