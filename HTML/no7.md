## HTML+CSS学习笔记 CSS样式

---

### 1. 字体

| 属性             | 说明                                                         | CSS3？ |
| ---------------- | ------------------------------------------------------------ | ------ |
| font             | 在一个声明中设置所有字体属性<br />顺序为："font-style font-variant font-weight font-size/line-height font-family。<br />font-size和font-family的值是必需的 |        |
| font-family      | 规定文本的字体系列，每个值用逗号分开。                       |        |
| font-size        | 规定文本的字体尺寸                                           |        |
| font-style       | 规定文本的字体样式。<br />normal：默认，标准的字体样式<br />italic：斜体的字体样式<br />oblique：倾斜的字体样式 |        |
| font-variant     | 规定文本的字体样式。<br />normal：默认，标准的字体<br />small-caps：显示小型大写字母的字体 |        |
| font-weight      | 规定字体的粗细。<br />normal：默认，标准的字体<br />bold：粗体字符<br />bolder：更粗的字符<br />lighter：更细的字符<br />数字：400 等同于 normal，而 700 等同于 bold |        |
| @font-face       | 一个规则，允许网站下载并使用其他超过"Web- safe"字体的字体    | yes    |
| font-size-adjust | 为元素规定 aspect 值                                         | yes    |
| font-stretch     | 收缩或拉伸当前的字体系列                                     | yes    |

---

### 2. 文本

| 属性            | 说明                                                         | CSS3？ |
| --------------- | ------------------------------------------------------------ | ------ |
| color           | 设置文本的颜色                                               |        |
| direction       | 规定文本的方向 / 书写方向<br />ltr：默认，左到右<br />rtl：右到左 |        |
| letter-spacing  | 设置字符间距                                                 |        |
| line-height     | 设置行高                                                     |        |
| text-align      | 规定文本的水平对齐方式<br />left：默认值<br />right<br />center<br />justify：两端对齐 |        |
| text-decoration | 规定添加到文本的装饰效果<br />none：默认<br />underline：下划线<br />overline：上划线<br />line-through：删除线<br />blink：闪烁 |        |
| text-indent     | 规定文本块首行的缩进                                         |        |
| text-transform  | 控制文本的大小写<br />none：默认<br />capitalize：每个单词以大写字母开头<br />uppercase：全大写<br />lowercase：全小写 |        |
| vertical-align  | 设置行内（内链）元素的垂直对齐方式<br />baseline：默认，父元素的基线上<br />sub：对齐文本的下标<br />super：对齐文本的上标<br />top：元素的顶端与行中最高元素的顶端对齐<br />text-top：元素的顶端与父元素字体的顶端对齐<br />middle：放置在父元素的中部<br />bottom：元素及其后代元素的底部与整行的底部对齐<br />text-bottom：元素的底端与父元素字体的底端对齐 |        |
| white-space     | 设置元素内的空白怎样处理<br />normal：默认，空白会被浏览器忽略<br />pre：空白会被浏览器保留<br />nowrap：文本不会换行，文本会在在同一行上继续，直到遇到 `<br/>` 标签为止<br />pre-wrap：保留空白符序列，但是正常地进行换行<br />pre-line：合并空白符序列，但是保留换行符 |        |
| word-spacing    | 设置单词间距                                                 |        |
| text-overflow   | 指定当文本溢出包含的元素，应该发生什么<br />clip：默认，修剪文本<br />ellipsis：显示省略符号来代表被修剪的文本<br />“自定义字符串”：使用给定的字符串来代表被修剪的文本 | yes    |
| text-shadow     | 为文本添加阴影<br />格式："*h-shadow v-shadow blur color*"<br />*h-shadow*：必需，水平阴影位置<br />*v-shadow*：必需，垂直阴影的位置<br />*blur*：模糊的距离<br />*color*：阴影的颜色 | yes    |
| word-break      | 指定非CJK（"中日韩"）文字的断行规则<br />normal：默认，浏览器默认的换行规则<br />break-all：允许在单词内换行。<br />keep-all：只能在半角空格或连字符处换行 | yes    |
| word-wrap       | 设置浏览器是否对过长的单词进行换行。<br />normal：默认，只在允许的断字点换行<br />break-word：在长单词或 URL 地址内部进行换行 | yes    |



---

#### [返回目录](./)

