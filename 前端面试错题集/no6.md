## 前端面试错题集 CSS的BFC

---

## 一、常见定位方案
在讲 BFC 之前，我们先来了解一下常见的定位方案，定位方案是控制元素的布局，有三种常见方案:

#### 普通流 (normal flow)
在普通流中，元素按照其在 HTML 中的先后位置**至上而下**，在这个过程中，**行内元素水平排列，直到当行被占满然后换行**，**块级元素则会被渲染为完整的一个新行**，除非另外指定，否则所有元素默认都是普通流定位，也可以说，普通流中元素的位置由该元素在 HTML 文档中的位置决定。

#### 浮动 (float)
在浮动布局中，元素首先按照**普通流的位置**出现，然后根据浮动的方向**尽可能的向左边或右边偏移**，其效果与印刷排版中的文本环绕相似。

#### 绝对定位 (absolute positioning)
在绝对定位布局中，元素会整体脱离普通流，因此绝对定位元素不会对其兄弟元素造成影响，而元素具体的位置由绝对定位的坐标决定。

## 二、BFC 概念
Formatting context(格式化上下文) 是 W3C CSS2.1 规范中的一个概念。它是页面中的一块渲染区域，并且有一套渲染规则，它决定了其子元素将如何定位，以及和其他元素的关系和相互作用。

那么 BFC 是什么呢？

BFC 即 Block Formatting Contexts (块级格式化上下文)，它属于上述定位方案的**普通流**。【所有BFC元素也是按照从上到下，从左到右的方式排列】

**具有 BFC 特性的元素可以看作是隔离了的独立容器，【容器里面的元素不会在布局上影响到外面的元素】，并且 BFC 具有普通容器所没有的一些特性**。

通俗一点来讲，可以把 BFC 理解为一个封闭的大箱子，箱子内部的元素无论如何翻江倒海，都不会影响到外部。

## 三、触发 BFC
只要元素满足下面任一条件即可触发 BFC 特性：

根元素（html）
浮动元素（元素的 float 不是 none）
绝对定位元素（元素的 position 为 absolute 或 fixed）
行内块元素（元素的 display 为 inline-block）
表格单元格（元素的 display 为 table-cell，HTML表格单元格默认为该值）
表格标题（元素的 display 为 table-caption，HTML表格标题默认为该值）
匿名表格单元格元素（元素的 display 为 table、table-row、 table-row-group、 table-header-group、table-footer-group（分别是HTML table、row、tbody、thead、tfoot 的默认属性）或 inline-table）
overflow 值不为 visible 的块元素
display 值为 flow-root 的元素
contain 值为 layout、content 或 paint 的元素(这个属性Firefox不支持)
弹性元素（display 为 flex 或 inline-flex 元素的直接子元素）
网格元素（display 为 grid 或 inline-grid 元素的直接子元素）
多列容器（元素的 column-count 或 column-width 不为 auto，包括 column-count 为 1）
column-span 为 all 的元素始终会创建一个新的BFC，即使该元素没有包裹在一个多列容器中（标准变更，Chrome bug）。



## 四、解决问题

1. 浮动元素的父元素高度坍塌（触发父元素的BFC就可以了）
2. 两栏或者更多宽度自适应布局，当右侧内容高度大于左侧内容高度时，内部的内容会环绕到左侧下方。可以给右侧一个BFC
3. 外边距垂直方向重合

---

#### [返回目录](./)



