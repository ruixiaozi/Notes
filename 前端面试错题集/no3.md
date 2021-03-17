## 前端面试错题集 介绍一下你对浏览器内核的理解？常见的浏览器内核有哪些

---

浏览器内核又可以分成两部分：渲染引擎(layout engineer 或者 Rendering Engine)和 JS 引擎。它负责取得网页的内容（HTML、XML、图像等等）、整理讯息（例如加入 CSS 等），以及计算网页的显示方式，然后会输出至显示器或打印机。浏览器的内核的不同对于网页的语法解释会有不同，所以渲染的效果也不相同。所有网页浏览器、电子邮件客户端以及其它需要编辑、显示网络内容的应用程序都需要内核。JS 引擎则是解析 Javascript 语言，执行 javascript 语言来实现网页的动态效果。**最开始渲染引擎和 JS 引擎并没有区分的很明确，后来 JS 引擎越来越独立，内核就倾向于只指渲染引擎**。有一个网页标准计划小组制作了一个 ACID 来测试引擎的兼容性和性能。内核的种类很多，如加上没什么人使用的非商业的免费内核，可能会有 10 多种，但是常见的浏览器内核可以分这四种：Trident、Gecko、Blink、Webkit。

IE：Trident 
firefox：Gecko 
safari：webkit 
chrom、Opera：blink 
Microsoft Edge：EdgeHTML

---

#### [返回目录](./)



