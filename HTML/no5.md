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
   
   
   /*以下是css新增*/
   
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
   | :active       | 向被激活的元素添加样式。                 |       |
   | :focus        | 向拥有键盘输入焦点的元素添加样式。       |       |
   | :hover        | 当鼠标悬浮在元素上方时，向元素添加样式。 |       |
   | :link         | 向未被访问的链接添加样式。               |       |
   | :visited      | 向已被访问的链接添加样式。               |       |
   | :first-child  | 向元素的第一个子元素添加样式。           |       |
   | :lang         | 向带有指定 lang 属性的元素添加样式。     |       |
   | :target       | 活动的元素                               | yes   |
   | :enabled      | 已经启用的元素                           | yes   |
   | :disabled     | 禁用的元素                               | yes   |
   | :checked      | 选中的元素                               | yes   |
   | ::selection   | 选中或者处于高亮状态的元素               | yes   |
   | :out-of-range | 值在指定区间之外的input元素              | yes   |
   | :in-range     | 值在指定区间之内的input元素              | yes   |
   | :read-write   | 可读及可写的元素                         | yes   |
   | :read-only    | 设置 "readonly"（只读） 属性的元素       | yes   |
   | :optional     | 可选的输入元素                           | yes   |
   | :required     | 设置了 "required" 属性的元素             | yes   |
   | :valid        | 输入值为合法的元素                       | yes   |
   | :invalid      | 输入值为非法的元素                       | yes   |

7. **伪元素选择器**

   其基本语法格式如下：

   ```css
   :伪元素 {color: red;}
   ```

   其中伪元素有下列值：

   | 属性                 | 描述                                       | 支持的css样式                                                | css3？ |
   | -------------------- | ------------------------------------------ | ------------------------------------------------------------ | ------ |
   | :first-letter        | 向文本的第一个字母添加特殊样式。           | font <br />color <br />background <br />word-spacing <br />letter-spacing <br />text-decoration <br />vertical-align <br />text-transform <br />line-height <br />clear |        |
   | :first-line          | 向文本的首行添加特殊样式。                 | font <br />color <br />background <br />margin <br />padding <br />border <br />text-decoration <br />vertical-align (仅当 float 为 none 时) <br />text-transform <br />line-height <br />float <br />clear |        |
   | :before              | 在元素之前添加内容。                       | 所有常见css样式<br />content （内容）                        |        |
   | :after               | 在元素之后添加内容。                       | 所有常见css样式<br />content （内容）                        |        |
   | :first-child         | 每个（该元素，在其父元素中是第1个）        |                                                              |        |
   | :last-child          | 每个（该元素，在其父元素中是倒数第1个）    |                                                              | yes    |
   | :first-of-type       | 每个（第一个该元素，在其父元素中）         |                                                              | yes    |
   | :last-of-type        | 每个（最后一个该元素，在其父元素中）       |                                                              | yes    |
   | :only-of-type        | 每个（该元素，在其父元素中只有一个）       |                                                              | yes    |
   | :only-child          | 每个（该元素，在其父元素中有且仅有它一个） |                                                              | yes    |
   | :nth-child(n)        | 每个（该元素，在其父元素中是第n个）        |                                                              | yes    |
   | :nth-last-child(n)   | 每个（该元素，在其父元素中是倒数第n个）    |                                                              | yes    |
   | :nth-of-type(n)      | 每个（第n个该元素，在其父元素中）          |                                                              | yes    |
   | :nth-last-of-type(n) | 每个（倒数第n个该元素，在其父元素中）      |                                                              | yes    |
   | :root                | 文档根元素                                 |                                                              | yes    |
   | :empty               | 没有任何子元素(包括文本节点)的元素         |                                                              | yes    |
   | :not(选择器)         | 每个（并非选择器选中的元素）               |                                                              | yes    |



---

### 2. 组合选择器

1. **级联选择器**

   将选择器**拼接**到一起，表示需要**同时符合**所有选择器的元素

   ```css
   /*p标签 同时具有cls1和cls2类*/
   p.cls1.cls2 {
   	color: red;
   }
   ```

2. **分组选择器**

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

### 3. 选择器优先级

浏览器通过**优先级**来判断哪一些属性值与一个元素最为相关，从而在该元素上应用这些属性值。优先级是基于不同种类选择器组成的匹配规则。

优先级基本规则：

```
内联 > ID选择器 > 类选择器/属性选择器/伪类 > 标签选择器/伪元素 > 通配符选择器 > 浏览器默认
```

优先级的规则计算如下：

优先级是由 `A` 、`B`、`C`、`D` 的值来决定的，其中它们的值计算规则如下：

1. 如果存在内联样式，那么 `A = 1`, 否则 `A = 0`;
2. `B` 的值等于 `ID选择器` 出现的次数;
3. `C` 的值等于 `类选择器` 和 `属性选择器` 和 `伪类` 出现的总次数;
4. `D` 的值等于 `标签选择器` 和 `伪元素` 出现的总次数 。

**比较规则是: 从A到D依次进行比较 ，较大者胜出，如果相等，则继续往后一位进行比较 。如果4位全部相等，则按定义顺序，后面定义的会覆盖前面的**。



**特殊情况：**

使用了 `!important` 的，则会优先于其他所有定义。





---

#### [返回目录](./)

