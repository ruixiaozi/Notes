## HTML+CSS学习笔记 HTML简介

---

### 1. 介绍

HTML 指的是超文本标记语言 (**H**yper **T**ext **M**arkup **L**anguage)是用来描述网页的一种语言。

**所谓超文本，有2层含义：** 

1. 因为它可以加入图片、声音、动画、多媒体等内容（**超越文本限制 **）
2. 不仅如此，它还可以从一个文件跳转到另一个文件，与世界各地主机的文件连接（**超级链接文本 **）。



---

### 2. HTML骨架

```html
<!DOCTYPE html>
<html lang="zh-CN">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Document</title>
</head>
<body>
  
</body>
</html>
```

可以使用Emmet快速生成，生成语法 `! tab` 或者 `html:5 tab` ;

更多的Emmet语法参考：[VsCode中使用Emmet神器快速编写HTML代码](https://www.cnblogs.com/summit7ca/p/6944215.html) 

**说明**：

1. **文档类型**

   ```html
   <!-- 指定html5 -->
   <!DOCTYPE html> 
   ```

   声明位于文档中的最前面的位置，处于  标签之前。此标签可告知浏览器文档使用哪种 HTML 或 XHTML 规范。

2. **页面语言lang**

   ~~~html
   <!-- 指定html 语言种类:影响浏览器判断网页使用的语言，比如翻译插件会根据这个判断源语言 -->
   <html lang="en">
   ~~~

   最常见的2个：

   1. `en`定义语言为英语
   2. `zh-CN`定义语言为中文

3. **字符集**

   ```html
   <meta charset="UTF-8" />
   ```

   设置网页内文本使用字符集编码，以保证浏览器使用对应的字符集编码进行正确解析。

   UTF-8是目前最常用的字符集编码方式，常用的字符集编码方式还有GBK和GB2312。

   * GB2312 简单中文 
   * BIG5   繁体中文 港澳台等用
   * GBK包含全部中文字符    是GB2312的扩展，加入对繁体字的支持，兼容GB2312
   * UTF-8则基本包含全世界所有国家需要用到的字符



---

### 3. HTML标签分类

1. 常规元素（双标签）

```html
<标签名> 内容 </标签名>   
比如：
<body>  我是文字  </body>
```

2. 空元素（单标签）

```html
<标签名 />  
比如  
<br />
```



---

### 4. HTML标签关系

1. 嵌套关系

```html
<head>  
	<title> </title> 
</head>
```

2.并列关系

```html
<head></head>
<body></body>
```



---

#### [返回目录](./)