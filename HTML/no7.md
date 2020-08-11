## HTML+CSS学习笔记 CSS样式

---

### 1. 字体

| 属性             | 说明                                                         | CSS3？ |
| ---------------- | ------------------------------------------------------------ | ------ |
| **font**         | 在一个声明中设置所有字体属性<br />顺序为："font-style font-variant font-weight font-size/line-height font-family。<br />font-size和font-family的值是必需的 |        |
| **font-family**  | 规定文本的字体系列，每个值用逗号分开。                       |        |
| **font-size**    | 规定文本的字体尺寸                                           |        |
| **font-style**   | 规定文本的字体样式。<br />normal：默认，标准的字体样式<br />italic：斜体的字体样式<br />oblique：倾斜的字体样式 |        |
| font-variant     | 规定文本的字体样式。<br />normal：默认，标准的字体<br />small-caps：显示小型大写字母的字体 |        |
| **font-weight**  | 规定字体的粗细。<br />normal：默认，标准的字体<br />bold：粗体字符<br />bolder：更粗的字符<br />lighter：更细的字符<br />数字：400 等同于 normal，而 700 等同于 bold |        |
| @font-face       | 一个规则，允许网站下载并使用其他超过"Web- safe"字体的字体    | yes    |
| font-size-adjust | 为元素规定 aspect 值                                         | yes    |
| font-stretch     | 收缩或拉伸当前的字体系列                                     | yes    |

---

### 2. 文本

| 属性                | 说明                                                         | CSS3？ |
| ------------------- | ------------------------------------------------------------ | ------ |
| **color**           | 设置文本的颜色                                               |        |
| direction           | 规定文本的方向 / 书写方向<br />ltr：默认，左到右<br />rtl：右到左 |        |
| **letter-spacing**  | 设置字符间距                                                 |        |
| **line-height**     | 设置行高<br />在应用到一个块级元素时，它定义了该元素中基线之间的**最小距离**而不是最大距离。<br />line-height 与 font-size 的计算值之差（在 CSS 中称为“行间距”）分为两半，分别加到一个文本行内容的顶部和底部。可以包含这些内容的最小框就是行框。<br />line-height与height的关系：<br />1. line-height = height：文字垂直居中<br />2. line-height > height：文字偏下<br />3. line-height < height：文字偏上 |        |
| **text-align**      | 规定文本的水平对齐方式<br />left：默认值<br />right<br />center<br />justify：两端对齐 |        |
| **text-decoration** | 规定添加到文本的装饰效果<br />none：默认<br />underline：下划线<br />overline：上划线<br />line-through：删除线<br />blink：闪烁 |        |
| **text-indent**     | 规定文本块首行的缩进                                         |        |
| **text-transform**  | 控制文本的大小写<br />none：默认<br />capitalize：每个单词以大写字母开头<br />uppercase：全大写<br />lowercase：全小写 |        |
| **vertical-align**  | 设置行内（内链）元素的垂直对齐方式<br />baseline：默认，父元素的基线上<br />sub：对齐文本的下标<br />super：对齐文本的上标<br />top：元素的顶端与行中最高元素的顶端对齐<br />text-top：元素的顶端与父元素字体的顶端对齐<br />middle：放置在父元素的中部<br />bottom：元素及其后代元素的底部与整行的底部对齐<br />text-bottom：元素的底端与父元素字体的底端对齐 |        |
| **white-space**     | 设置元素内的空白怎样处理<br />normal：默认，空白会被浏览器忽略<br />pre：空白会被浏览器保留<br />nowrap：文本不会换行，文本会在在同一行上继续，直到遇到 `<br/>` 标签为止<br />pre-wrap：保留空白符序列，但是正常地进行换行<br />pre-line：合并空白符序列，但是保留换行符 |        |
| **word-spacing**    | 设置单词间距                                                 |        |
| **text-overflow**   | 指定当文本溢出包含的元素，应该发生什么<br />clip：默认，修剪文本<br />ellipsis：显示省略符号来代表被修剪的文本<br />“自定义字符串”：使用给定的字符串来代表被修剪的文本 | yes    |
| **text-shadow**     | 为文本添加阴影<br />格式："*h-shadow v-shadow blur color*"<br />*h-shadow*：必需，水平阴影位置<br />*v-shadow*：必需，垂直阴影的位置<br />*blur*：模糊的距离<br />*color*：阴影的颜色 | yes    |
| **word-break**      | 指定非CJK（"中日韩"）文字的断行规则<br />normal：默认，浏览器默认的换行规则<br />break-all：允许在单词内换行。<br />keep-all：只能在半角空格或连字符处换行 | yes    |
| **word-wrap**       | 设置浏览器是否对过长的单词进行换行。<br />normal：默认，只在允许的断字点换行<br />break-word：在长单词或 URL 地址内部进行换行 | yes    |

---

### 3. 定位

| 属性           | 说明                                                         | CSS3? |
| -------------- | ------------------------------------------------------------ | ----- |
| **bottom**     | 设置定位元素下外边距边界与其包含块下边界之间的偏移           |       |
| **clear**      | 规定元素的哪一侧不允许其他浮动元素                           |       |
| **clip**       | 剪裁绝对定位元素                                             |       |
| **cursor**     | 规定要显示的光标的类型（形状）                               |       |
| **display**    | 规定元素应该生成的框的显示类型<br />none：不显示<br />block：作为块级元素显示<br />inline：作为内链（行内）元素显示<br />inline-block：作为行内块元素显示<br />list-item：作为列表一项显示<br />table：作为块级表格显示（`<table>`）<br />inline-table：作为内链表格显示（`<table>`）<br />table-row-group：类似`<tbody>`<br />table-header-group：类似`<thead>`<br />table-footer-group：类似`<tfoot>`<br />table-row：类似`<tr>`<br />table-column-group：类似`<colgroup>`<br />table-column：类似`<col>`<br />table-cell：类似`<td>和<th>`<br />table-caption：类似`<caption>` |       |
| **float**      | 规定框是否应该浮动                                           |       |
| **left**       | 设置定位元素左外边距边界与其包含块左边界之间的偏移           |       |
| **overflow**   | 规定当内容溢出元素框时发生的事情                             |       |
| **position**   | 规定元素的定位类型                                           |       |
| **right**      | 设置定位元素右外边距边界与其包含块右边界之间的偏移           |       |
| **top**        | 设置定位元素的上外边距边界与其包含块上边界之间的偏移         |       |
| **visibility** | 规定元素是否可见                                             |       |
| **z-index**    | 设置元素的堆叠顺序                                           |       |

---

### 4. 背景

| 属性                    | 描述                                                         | CSS3？ |
| ----------------------- | ------------------------------------------------------------ | ------ |
| **background**          | 在一个声明中设置所有的背景属性。<br />格式："bg-color bg-image position/bg-size bg-repeat bg-origin bg-clip bg-attachment initial\|inherit;" (不分先后顺序。可以只有其中的某些值) |        |
| background-attachment   | 设置或检索背景图像是随对象内容滚动还是固定的。必须先指定background-image属性。<br />scroll：默认，随着页面的滚动而滚动<br />fixed：不会随着页面的滚动而滚动<br />local：会随着元素内容的滚动而滚动 |        |
| **background-color**    | 设置元素的背景颜色。<br />默认值：transparent  （透明）      |        |
| **background-image**    | 设置元素的背景图像。                                         |        |
| **background-position** | 设置背景图像的开始位置。<br />格式："x y"，x和y可以是任何表示位置的方式（方向名词/长度值） |        |
| **background-repeat**   | 设置是否及如何重复背景图像。<br />repeat：默认，向垂直和水平方向重复<br />repeat-x：只有水平位置会重复<br />repeat-y：只有垂直位置会重复<br />no-repeat：不会重复 |        |
| **background-clip**     | 指定背景图像向外裁剪的区域。<br />border-box：默认<br />padding-box<br />content-box | yes    |
| background-origin       | 设置背景图的参考原点。<br />padding-box：默认<br />border-box<br />content-box | yes    |
| **background-size**     | 背景图像的尺寸大小                                           | yes    |

---

### 5. 尺寸

| 属性       | 描述               | CSS3？ |
| ---------- | ------------------ | ------ |
| height     | 设置元素的高度     |        |
| max-height | 设置元素的最大高度 |        |
| max-width  | 设置元素的最大宽度 |        |
| min-height | 设置元素的最小高度 |        |
| min-width  | 设置元素的最小宽度 |        |
| width      | 设置元素的宽度     |        |

---

### 6. 内边距

| 属性           | 说明                         | CSS3？ |
| -------------- | ---------------------------- | ------ |
| padding        | 在一个声明中设置所有填充属性 |        |
| padding-bottom | 设置元素的底填充             |        |
| padding-left   | 设置元素的左填充             |        |
| padding-right  | 设置元素的右填充             |        |
| padding-top    | 设置元素的顶部填充           |        |

----

### 7. 外边距

| 属性          | 说明                           | CSS3？ |
| ------------- | ------------------------------ | ------ |
| margin        | 在一个声明中设置所有外边距属性 |        |
| margin-bottom | 设置元素的下外边距             |        |
| margin-left   | 设置元素的左外边距             |        |
| margin-right  | 设置元素的右外边距             |        |
| margin-top    | 设置元素的上外边距             |        |

---

### 8. 边框与轮廓

| 属性                       | 描述                                                         | CSS  |
| -------------------------- | ------------------------------------------------------------ | ---- |
| border                     | 复合属性。设置对象边框的特性。                               | 1    |
| border-bottom              | 复合属性。设置对象底部边框的特性。                           | 1    |
| border-bottom-color        | 设置或检索对象的底部边框颜色。                               | 1    |
| border-bottom-style        | 设置或检索对象的底部边框样式。                               | 1    |
| border-bottom-width        | 设置或检索对象的底部边框宽度。                               | 1    |
| border-color               | 置或检索对象的边框颜色。                                     | 1    |
| border-left                | 复合属性。设置对象左边边框的特性。                           | 1    |
| border-left-color          | 设置或检索对象的左边边框颜色。                               | 1    |
| border-left-style          | 设置或检索对象的左边边框样式。                               | 1    |
| border-left-width          | 设置或检索对象的左边边框宽度。                               | 1    |
| border-right               | 复合属性。设置对象右边边框的特性。                           | 1    |
| border-right-color         | 设置或检索对象的右边边框颜色。                               | 1    |
| border-right-style         | 设置或检索对象的右边边框样式。                               | 1    |
| border-right-width         | 设置或检索对象的右边边框宽度。                               | 1    |
| border-style               | 设置或检索对象的边框样式。                                   | 1    |
| border-top                 | 复合属性。设置对象顶部边框的特性。                           | 1    |
| border-top-color           | 设置或检索对象的顶部边框颜色                                 | 1    |
| border-top-style           | 设置或检索对象的顶部边框样式。                               | 1    |
| border-top-width           | 设置或检索对象的顶部边框宽度。                               | 1    |
| border-width               | 设置或检索对象的边框宽度。                                   | 1    |
| outline                    | 复合属性。设置或检索对象外的线条轮廓。                       | 2    |
| outline-color              | 设置或检索对象外的线条轮廓的颜色。                           | 2    |
| outline-style              | 设置或检索对象外的线条轮廓的样式。                           | 2    |
| outline-width              | 设置或检索对象外的线条轮廓的宽度。                           | 2    |
| border-bottom-left-radius  | 设置或检索对象的左下角圆角边框。提供2个参数，2个参数以空格分隔，每个参数允许设置1个参数值，第1个参数表示水平半径，第2个参数表示垂直半径，如第2个参数省略，则默认等于第1个参数 | 3    |
| border-bottom-right-radius | 设置或检索对象的右下角圆角边框。                             | 3    |
| border-image               | 设置或检索对象的边框样式使用图像来填充。                     | 3    |
| border-image-outset        | 规定边框图像超过边框的量。                                   | 3    |
| border-image-repeat        | 规定图像边框是否应该被重复（repeated）、拉伸（stretched）或铺满（rounded）。 | 3    |
| border-image-slice         | 规定图像边框的向内偏移。                                     | 3    |
| border-image-source        | 规定要使用的图像，代替 border-style 属性中设置的边框样式。   | 3    |
| border-image-width         | 规定图像边框的宽度。                                         | 3    |
| border-radius              | 设置或检索对象使用圆角边框。                                 | 3    |
| border-top-left-radius     | 定义左上角边框的形状。                                       | 3    |
| border-top-right-radius    | 定义右上角边框的形状。                                       | 3    |
| box-decoration-break       | 规定行内元素被折行                                           | 3    |
| box-shadow                 | 向方框添加一个或多个阴影。                                   | 3    |

---

### 9. 盒子属性

| 属性           | 描述                                                        | CSS  |
| -------------- | ----------------------------------------------------------- | ---- |
| overflow-x     | 如果内容溢出了元素内容区域，是否对内容的左/右边缘进行裁剪。 | 3    |
| overflow-y     | 如果内容溢出了元素内容区域，是否对内容的上/下边缘进行裁剪。 | 3    |
| overflow-style | 规定溢出元素的首选滚动方法。                                | 3    |
| rotation       | 围绕由 rotation-point 属性定义的点对元素进行旋转。          | 3    |
| rotation-point | 定义距离上左边框边缘的偏移点。                              | 3    |

---

### 10. 列表

| 属性                | 说明                           | CSS  |
| ------------------- | ------------------------------ | ---- |
| list-style          | 在一个声明中设置所有的列表属性 | 1    |
| list-style-image    | 将图象设置为列表项标记         | 1    |
| list-style-position | 设置列表项标记的放置位置       | 1    |
| list-style-type     | 设置列表项标记的类型           | 1    |

---

### 11. 用户界面

| 属性           | 说明                                     | CSS  |
| -------------- | ---------------------------------------- | ---- |
| appearance     | 定义元素的外观样式                       | 3    |
| box-sizing     | 允许您为了适应区域以某种方式定义某些元素 | 3    |
| icon           | 为元素指定图标                           | 3    |
| nav-down       | 指定用户按向下键时向下导航的位置         | 3    |
| nav-index      | 指定导航（tab）顺序。                    | 3    |
| nav-left       | 指定用户按向左键时向左导航的位置         | 3    |
| nav-right      | 指定用户按向右键时向左导航的位置         | 3    |
| nav-up         | 指定用户按向上键时向上导航的位置a        | 3    |
| outline-offset | 设置轮廓框架在 border 边缘外的偏移       | 3    |
| resize         | 定义元素是否可以改变大小                 | 3    |





---

#### [返回目录](./)

