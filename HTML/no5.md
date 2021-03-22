## HTML+CSS学习笔记 CSS选择器

---

### 1. 基础选择器

1. **元素选择器**

   其基本语法格式如下：

   ```css
   html {color:black;}
   h1 {color:blue;}
   h2 {color:silver;}
   ```

2. **通配符选择器**

   其基本语法格式如下：

   ```css
   * {color:black;}
   ```

3. **类选择器**

   其基本语法格式如下：

   ```css
   .important {color:red;}
   ```

4. **ID选择器**

   其基本语法格式如下：

   ```css
   #intro {font-weight:bold;}
   ```

5. **属性选择器**

   其基本语法格式如下：

   ```css
   [href] {color: red;}
   
   /*使用target="_blank"的a元素*/
   a[target=_blank]
   {
   background-color:yellow;
   }
   
   /*标题属性包含单词"flower"的所有元素*/
   [title~=flower]
   {
   background-color:yellow;
   }
   
   /* lang 属性值以 "en" 开头的元素*/
   [lang|=en]
   { 
   background-color:yellow;
   }
   
   
   /*以下是css3新增*/
   
   /*class属性值以"test"开头的所有div元素*/
   div[class^="test"]
   {
   background:#ffff00;
   }
   
   /*class属性值以"test"结尾的所有div元素*/
   div[class$="test"]
   {
   background:#ffff00;
   }
   
   /*class属性值包含"test"的所有div元素*/
   div[class*="test"]
   {
       background:#ffff00;
   }
   ```

6. **伪类选择器**

   其基本语法格式如下：

   ```css
   :伪类 {color: red;}
   ```

   其中伪类有下列值：

   | 属性          | 描述                                     | css3? |
   | ------------- | ---------------------------------------- | ----- |
   | **:active**   | 向被激活的元素添加样式。                 |       |
   | **:focus**    | 向拥有键盘输入焦点的元素添加样式。       |       |
   | **:hover**    | 当鼠标悬浮在元素上方时，向元素添加样式。 |       |
   | **:link**     | 向未被访问的链接添加样式。               |       |
   | **:visited**  | 向已被访问的链接添加样式。               |       |
   | :lang         | 向带有指定 lang 属性的元素添加样式。     |       |
   | :target       | 活动的元素                               | yes   |
   | :enabled      | 已经启用的元素                           | yes   |
   | :disabled     | 禁用的元素                               | yes   |
   | :checked      | 选中的元素                               | yes   |
   | :selection    | 选中或者处于高亮状态的元素               | yes   |
   | :out-of-range | 值在指定区间之外的input元素              | yes   |
   | :in-range     | 值在指定区间之内的input元素              | yes   |
   | :read-write   | 可读及可写的元素                         | yes   |
   | :read-only    | 设置 "readonly"（只读） 属性的元素       | yes   |
   | :optional     | 可选的输入元素                           | yes   |
   | :required     | 设置了 "required" 属性的元素             | yes   |
   | :valid        | 输入值为合法的元素                       | yes   |
   | :invalid      | 输入值为非法的元素                       | yes   |

   - `nth-child`  选择父元素里面的第几个子元素，不管是第几个类型
   - `nt-of-type`  选择指定类型的元素

   | E**:first-child**     | 每个（在其父元素E中是第1个）                                 |      |
   | --------------------- | ------------------------------------------------------------ | ---- |
   | E:last-child          | 每个（在其父元素中E是倒数第1个）                             | yes  |
   | E:first-of-type       | 每个（第一个元素E，在其父元素中）                            | yes  |
   | E:last-of-type        | 每个（最后一个元素E，在其父元素中）                          | yes  |
   | E:only-of-type        | 每个（在其父元素E中只有一个）                                | yes  |
   | E:only-child          | 每个（在其父元素E中有且仅有它一个）                          | yes  |
   | E:nth-child(n)        | 每个（在其父元素E中是第n个）<br />注意：本质上就是选中第几个子元素<br />n 可以是数字、关键字、公式<br />n 如果是数字，就是选中第几个<br />常见的关键字有 `even` 偶数、`odd` 奇数<br />常见的公式如下(如果 n 是公式，则从 0 开始计算)<br />但是第 0 个元素或者超出了元素的个数会被忽略 | yes  |
   | E:nth-last-child(n)   | 每个（在其父元素E中是倒数第n个）<br />同上                   | yes  |
   | E:nth-of-type(n)      | 每个（第n个元素E，在其父元素中）<br />同上                   | yes  |
   | E:nth-last-of-type(n) | 每个（倒数第n个元素E，在其父元素中）<br />同上               | yes  |
   | :root                 | 文档根元素                                                   | yes  |
   | **:empty**            | 没有任何子元素(包括文本节点)的元素                           | yes  |
   | **:not(选择器)**      | 每个（并非选择器选中的元素）                                 | yes  |

   

7. **伪元素选择器**

   其基本语法格式如下：

   在 CSS3 中，双冒号取代了伪元素的单冒号表示法。这是 W3C 试图区分*伪类*和*伪元素*的尝试。

   在 CSS2 和 CSS1 中，伪类和伪元素都使用了单冒号语法。

   为了向后兼容，CSS2 和 CSS1 伪元素可接受单冒号语法。

   ```css
   ::伪元素 {color: red;}
   ```

   其中伪元素有下列值：

   | 属性           | 描述                             | 支持的css样式                                                | css3？ |
   | -------------- | -------------------------------- | ------------------------------------------------------------ | ------ |
   | ::first-letter | 向文本的第一个字母添加特殊样式。 | font <br />color <br />background <br />word-spacing <br />letter-spacing <br />text-decoration <br />vertical-align <br />text-transform <br />line-height <br />clear |        |
   | ::first-line   | 向文本的首行添加特殊样式。       | font <br />color <br />background <br />margin <br />padding <br />border <br />text-decoration <br />vertical-align (仅当 float 为 none 时) <br />text-transform <br />line-height <br />float <br />clear |        |
   | **::before**   | 在元素之前添加内容。             | 所有常见css样式<br />content （必须）                        |        |
   | **::after**    | 在元素之后添加内容。             | 所有常见css样式<br />content （必须）                        |        |
   | ::selection    | 选中或者处于高亮状态的元素       |                                                              |        |



---

### 2. 组合选择器

1. **级联（交集）选择器**

   将选择器**拼接**到一起，表示需要**同时符合**所有选择器的元素

   ```css
   /*p标签 同时具有cls1和cls2类*/
   p.cls1.cls2 {
   	color: red;
   }
   ```

2. **分组（并集）选择器**

   将不同选择器用**逗号分隔**，表示**所有不同的选择器选择的元素都具有这个样式**。

   ```css
   /*p标签 和 h2标签都具有这个样式*/
   h2, p {color:gray;}
   ```

3. **后代选择器**

   将不同选择器用**空格分隔**，表示在**前面选择器选出的元素的后代元素中，继续匹配后面的选择器**。

   ```css
   /*作为 h1 元素后代的 em 元素的文本变为 红色*/
   h1 em {color:red;}
   ```

4. **子元素选择器**

   将不同的选择器用 `>` 分隔，表示在**前面选择器选出的元素的子元素中，继续匹配后面的选择器**。

   ```css
   /* h1 下面的 strong子元素 文本变成 红色*/
   h1 > strong {color:red;}
   ```

5. **后一个元素选择器**

   将不同的选择器用 `+` 分隔，表示在**前面选择器选出的元素的后续兄弟元素中，继续匹配第一个后面的选择器**。

   ```css
   /*选择紧接在 h1 元素后出现的p，h1 和 p 元素拥有共同的父元素*/
   h1 + p {margin-top:50px;}
   ```

6. **后续选择器**（css3）

   将不同的选择器用 `~` 分隔，表示在**前面选择器选出的元素的后续兄弟元素中，继续匹配每一个后面的选择器**。

   ```css
   /*同一父元素下的 p 元素之后的每一个 ul 元素*/
   p ~ ul
   {
   background:#ff0000;
   }
   ```



---

#### [返回目录](./)

