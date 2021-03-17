## HTML+CSS学习笔记 前言

---

### 1. 常见浏览器内核 （Rendering Engine 渲染引擎）

主要是webkit（blink也是webkit的分支）

| 浏览器  |      内核      | 备注                                                         |
| :------ | :------------: | :----------------------------------------------------------- |
| IE      |    Trident     | IE、猎豹安全、360极速浏览器、百度浏览器                      |
| firefox |     Gecko      | 可惜这几年已经没落了，打开速度慢、升级频繁、猪一样的队友flash、神一样的对手chrome。 |
| Safari  |     webkit     | 现在很多人错误地把 webkit 叫做 chrome内核（即使 chrome内核已经是 blink 了）。苹果感觉像被别人抢了媳妇，都哭晕再厕所里面了。 |
| chrome  | Chromium/Blink | 在 Chromium 项目中研发 Blink 渲染引擎（即浏览器核心），内置于 Chrome 浏览器之中。Blink 其实是 WebKit 的分支。大部分国产浏览器最新版都采用Blink内核。二次开发 |
| Opera   |     blink      | 现在跟随chrome用blink内核。                                  |

```
Android手机而言，使用率最高的就是Webkit内核，大部分国产浏览器宣称的自己的内核，基本上也是属于webkit二次开发。

iOS以及WP7平台上，由于系统原因，系统大部分自带浏览器内核，一般是Safari或者IE内核Trident的
```



---

### 2. Web标准(重点)

**构成：** 主要包括结构（Structure）、表现（Presentation）和行为（Behavior）三个方面。

| 标准 | 说明                                                         |
| :--- | :----------------------------------------------------------- |
| 结构 | 结构用于对**网页元素**进行整理和分类，咱们主要学的是HTML。   |
| 表现 | 表现用于设置网页元素的版式、颜色、大小等**外观样式**，主要指的是CSS |
| 行为 | 行为是指网页模型的定义及**交互**的编写，咱们主要学的是 Javascript |



---

### 3. 相关问题



+ **介绍一下你对浏览器内核的理解？常见的浏览器内核有哪些？**

  浏览器内核又可以分成两部分：渲染引擎(layout engineer 或者 Rendering Engine)和 JS 引擎。它负责取得网页的内容（HTML、XML、图像等等）、整理讯息（例如加入 CSS 等），以及计算网页的显示方式，然后会输出至显示器或打印机。浏览器的内核的不同对于网页的语法解释会有不同，所以渲染的效果也不相同。所有网页浏览器、电子邮件客户端以及其它需要编辑、显示网络内容的应用程序都需要内核。JS 引擎则是解析 Javascript 语言，执行 javascript 语言来实现网页的动态效果。**最开始渲染引擎和 JS 引擎并没有区分的很明确，后来 JS 引擎越来越独立，内核就倾向于只指渲染引擎**。有一个网页标准计划小组制作了一个 ACID 来测试引擎的兼容性和性能。内核的种类很多，如加上没什么人使用的非商业的免费内核，可能会有 10 多种，但是常见的浏览器内核可以分这四种：Trident、Gecko、Blink、Webkit。

  IE：Trident 
  firefox：Gecko 
  chrom、safari：webkit 
  Opera：Presto 
  Microsoft Edge：EdgeHTML

  深度阅读：[五大主流浏览器内核的源起以及国内各大浏览器内核总结](http://blog.csdn.net/summer_15/article/details/71249203) 

  





---

#### [返回目录](./)

