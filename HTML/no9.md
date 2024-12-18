## HTML+CSS学习笔记 CSS浮动

---

### 1.CSS 布局的三种机制

> 网页布局的核心——就是**用 CSS 来摆放盒子**。

CSS 提供了 **3 种机制**来设置盒子的摆放位置，分别是**普通流**（标准流）、**浮动**和**定位**，其中： 

1. **普通流**（标准流）
   - **块级元素**会独占一行，**从上向下**顺序排列；
     - 常用元素：div、hr、p、h1~h6、ul、ol、dl、form、table
   - **行内元素**会按照顺序，**从左到右**顺序排列，碰到父元素边缘则自动换行；
     - 常用元素：span、a、i、em等
2. **浮动**
   - 让盒子从普通流中**浮**起来,主要作用让多个块级盒子一行显示。
3. **定位**
   - 将盒子**定**在浏览器的某一个**位**置——CSS 离不开定位，特别是后面的 js 特效。



### 2.什么是浮动(float)

**概念**：元素的浮动是指**设置了浮动属性的元素**会

1. 脱离标准普通流的控制
2. 移动到指定位置。



### 3. 作用

1. **让多个盒子(div)水平排列成一行**，使得浮动成为布局的重要手段。
2. 可以实现盒子的左右对齐等等..
3. 浮动最早是用来**控制图片**，实现**文字环绕图片的效果**。（因为文字内容不会被浮动遮挡，所以就形成了环绕效果）



### 4. 语法

在 CSS 中，通过 `float`  中文，  浮 漏 特    属性定义浮动，语法如下：

```
选择器 { float: 属性值; }
```

| 属性值    | 描述                     |
| --------- | ------------------------ |
| **none**  | 元素不浮动（**默认值**） |
| **left**  | 元素向**左**浮动         |
| **right** | 元素向**右**浮动         |

pink老师教你学浮动口诀。通过 `float`   -----  浮 漏 特

| 特点 | 说明                                                         |
| ---- | ------------------------------------------------------------ |
| 浮   | 加了浮动的盒子**是浮起来**的，漂浮在其他标准流盒子的上面。   |
| 漏   | 加了浮动的盒子**是不占位置的**，它原来的位置**漏给了标准流的盒子**。 |
| 特   | **特别注意**：浮动元素会改变display属性， 类似转换为了行内块，但是元素之间没有空白缝隙。浮动的元素互相贴靠一起的，但是如果父级宽度装不下这些浮动的盒子， 多出的盒子会另起一行对齐 |





---

#### [返回目录](./)

