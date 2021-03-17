## HTML+CSS学习笔记 HTML标签

---

### 1. 不显示标签

1. 网页标题标签

   提供网页的标题，供浏览器顶部显示。

   其基本语法格式如下：

   ```html
   <title>标题内容</title>
   ```

2. 元信息标签

   提供有关页面的元信息（meta-information），比如针对搜索引擎和更新频度的描述和关键词。

   其基本语法格式如下：

   ```html
   <meta name="keywords" content="HTML,ASP,PHP,SQL">
   ```

   属性说明：

   | 属性       | 值                                                           | 描述                              | 是否必要             |
   | :--------- | :----------------------------------------------------------- | :-------------------------------- | -------------------- |
   | name       | author（作者的名字）<br />description（页面的描述）<br />keywords（逗号分隔的关键词列表）<br />revised（最后修改时间）<br />viewport（手机页面[参数](https://www.cnblogs.com/pigtail/archive/2013/03/15/2961631.html)） | 把 content 属性关联到一个名称。   | name\htt-equiv二选一 |
   | http-equiv | content-type<br/>default-style<br/>refresh（定义文档自动刷新的时间间隔） | 把 content 属性关联到 HTTP 头部。 | name\htt-equiv二选一 |
   | content    | some_text                                                    | 相关的元信息                      | 必要                 |
   | charset    | *character_set*                                              | 定义文档的字符编码。              | 单独使用             |

3. base标签

   为页面上的所有的**相对链接**规定**默认 URL **或**默认目标**。

   请把 `<base>` 标签排在` <head>` 元素中*第一个*元素的位置，这样 head 区域中其他元素就可以使用` <base>` 元素中的信息了。

   其基本语法格式如下：

   ```html
   <base href="http://example.com" target="_blank">
   ```

   属性说明：

   | 属性   | 值                                                           | 描述                                                         | 是否必要 |
   | :----- | :----------------------------------------------------------- | :----------------------------------------------------------- | -------- |
   | href   | *URL*                                                        | 规定页面中所有相对链接的基准 URL。                           | 必要     |
   | target | 用于指定链接页面的打开方式<br />`_blank` 在新窗口中打开<br />`_parent` 在父框架中打开<br />`_self` （默认）在自生框架打开<br />`_top` 在顶层框架中打开 | 规定页面中所有的超链接和表单在何处打开。<br />该属性会被每个链接中的 target 属性覆盖。 |          |

4. link标签

   定义文档与外部资源的关系，最常见的用途是链接样式表。

   其基本语法格式如下：

   ```html
   <link rel="stylesheet" href="style.css">
   ```

   属性说明：

   | 属性  | 值                                                           | 描述                                             | 是否必要 |
   | :---- | :----------------------------------------------------------- | :----------------------------------------------- | -------- |
   | href  | *URL*                                                        | 定义被链接文档的位置。                           | 必要     |
   | rel   | author（链接到该文档的作者）<br />help（链接到帮助文档）<br />icon（常用，该文档的图标）<br />license（链接到该文档的版权信息）<br />next（链接到下一个文档）<br />prefetch （应该对目标资源进行缓存）<br />prev（链接到上一个文档） <br />search（链接到针对文档的搜索工具）<br />stylesheet（常用，样式表）<br /> | 定义当前文档与被链接文档之间的关系。             | 必要     |
   | sizes | *Height* x *Width* \| any                                    | 定义了链接属性大小，只对属性 rel="icon" 起作用。 |          |
   | type  | *MIME_type*                                                  | 规定被链接文档的 MIME 类型。H5可以省略           |          |





---

### 2. 块级标签

1. 标题标签

   其基本语法格式如下：

   ```html
   <h1>   标题文本   </h1>
   <h2>   标题文本   </h2>
   <h3>   标题文本   </h3>
   <h4>   标题文本   </h4>
   <h5>   标题文本   </h5>
   <h6>   标题文本   </h6>
   ```

2. 段落标签

   其基本语法格式如下：

   ```html
   <p>  文本内容  </p>
   ```

3. 水平线标签

   其基本语法格式如下：

   ```html
   <hr />
   ```

4. 换行标签

   其基本语法格式如下：

   ```html
   <br />
   ```

5. div标签

   div 就是  division  的缩写   分割， 分区的意思。

   其基本语法格式如下：

   ```html
   <div> 这是头部 </div>
   ```


6. 预格式化的文本标签

   被包围在 `<pre>` 标签 元素中的文本通常会**保留空格和换行符**。而文本也会呈现为**等宽字体**。

   其基本语法格式如下：

   ```html
   <pre>
   
     此例演示如何使用 pre 标签
   
     对空行和 空格
   
     进行控制
   
   </pre>
   ```

7. 表格标签

   创建表格的基本语法：

   ```html
   <table>
     <caption>标题</caption>
     <thead>
     	<tr>
       	<th>单元格内的文字</th>
         ...
       </tr>
     </thead>
     <tbody>
       <tr>
         <td>单元格内的文字</td>
         ...
       </tr>
     </tbody>
     <tfoot>
       <tr>
         <td>单元格内的文字</td>
         ...
       </tr>
     </tfoot>
   </table>
   ```

   | 标签名                   | 定义           | 说明                                                         |
   | ------------------------ | :------------- | :----------------------------------------------------------- |
   | `<table></table>`        | 表格标签       | 就是一个四方的盒子                                           |
   | `<tr></tr>`              | 表格行标签     | 行标签要再table标签内部才有意义                              |
   | `<td></td>`              | 单元格标签     | 单元格标签是个容器级元素，可以放任何东西                     |
   | `<th></th>`              | 表头单元格标签 | 它还是一个单元格，但是里面的文字会居中且加粗                 |
   | `<caption></caption>`    | 表格标题标签   | 表格的标题，跟着表格一起走，和表格居中对齐                   |
   | `<thead></thead>`        | 题头           |                                                              |
   | `<tbody></tbody>`        | 主体           |                                                              |
   | `<tfoot></tfoot>`        | 脚部           |                                                              |
   | cellspacing和cellpadding | 设置单元格距离 | cellspacing单元格之间的间距<br />cellpadding单元格内与单元格边框之间的间距 |
   | clospan 和 rowspan       | 合并属性       | 用来合并单元格的                                             |

   对于比较复杂的表格，表格的结构也就相对的复杂了，所以又将表格分割成三个部分：题头、正文和脚注。而这三部分分别用:thead,tbody,tfoot来标注， 这样更好的分清表格结构。

8. 列表标签

   + 无序列表

     其基本语法格式如下：

     ```html
     <ul>
       <li>列表项1</li>
       <li>列表项2</li>
       <li>列表项3</li>
       ......
     </ul>
     ```

   + 有序列表

     其基本语法格式如下：

     ```html
     <ol>
       <li>列表项1</li>
       <li>列表项2</li>
       <li>列表项3</li>
       ......
     </ol>
     ```

   + 自定义列表（重要！**一般用于网站底部，一个标题然后再带列表的**）

     其基本语法格式如下：

     ```html
     <dl>
       <dt>名词1</dt>
       <dd>名词1解释1</dd>
       <dd>名词1解释2</dd>
       ...
       <dt>名词2</dt>
       <dd>名词2解释1</dd>
       <dd>名词2解释2</dd>
       ...
     </dl>
     ```

9. 表单域标签

   其基本语法如下：

   ```html
   <form action="url地址" method="提交方式" name="表单名称">
     各种表单控件
   </form>
   ```

   | 属性   | 属性值   | 作用                                               |
   | ------ | :------- | -------------------------------------------------- |
   | action | url地址  | 用于指定接收并处理表单数据的服务器程序的url地址。  |
   | method | get/post | 用于设置表单数据的提交方式，其取值为get或post。    |
   | name   | 名称     | 用于指定表单的名称，以区分同一个页面中的多个表单。 |

   



---

### 3. 内链标签

1. span标签

   其基本语法格式如下：

   ```html
   <span>今日价格</span>
   ```

2. 文本格式化标签

   为文字设置粗体、斜体或下划线效果，这时就需要用到HTML中的文本格式化标签。

   其基本语法格式如下：

   ```html
   <b>粗体</b> <strong>强调，粗体显示</strong>
   <i>斜体</i> <em>强调，斜体显示</em>
   <s>删除线</s> <del>删除线</del>
   <u>下划线</u> <ins>下划线</ins>
   ```

3. 链接标签

   其基本语法格式如下：

   ```html
   <a href="跳转目标" target="目标窗口的弹出方式">文本或图像</a>
   ```

   属性说明：

   | 属性   | 作用                                                         | 是否必要 |
   | ------ | :----------------------------------------------------------- | -------- |
   | href   | 用于指定链接目标的url地址。<br />当地址为 `#myid` 时，通过锚点定位到 `id` 为 `myid` 的标签处 | 必要     |
   | target | 用于指定链接页面的打开方式<br />`_blank` 在新窗口中打开<br />`_parent` 在父框架中打开<br />`_self` （默认）在自生框架打开<br />`_top` 在顶层框架中打开 |          |

   链接的默认外观如下：

   - **未被访问**的链接带有 <ins>下划线</ins> 而且是 <span style="color:blue">蓝色</span> 的
   
     a:link {color: #FF00FF} /* 未访问的链接  */
   
   - **已被访问**的链接带有 <ins>下划线</ins> 而且是 <span style="color:purple">紫色</span> 的
   
     a:visited {color: #00FF00} /* 已访问的链接 */
   
   - **活动链接**带有 <ins>下划线</ins> 而且是 <span style="color:red">红色</span> 的
   
     a:active {color: #0000FF} /* 选定的链接 */
   
4. **lable标签**

   label 标签为 input 元素定义标注。通过与input绑定，可以实现点击标签让input获取焦点的功能。

   其基本语法格式如下：

   ```html
   <label> 用户名： <input type="radio" name="usename" value="请输入用户名">   </label>
   
   <!-- for与id进行绑定 -->
   <label for="sex">男</label>
   <input type="radio" name="sex"  id="sex">
   ```
```
   
   

---

### 4. 内链块级标签

1. 图像标签

   显示图像，可以设置高宽等块级属性。

   其基本语法格式如下：

   ```html
   <img src="图像URL" alt="某某图形" />
```

   属性说明：

| 属性   | 值            | 描述                 | 是否必要 |
| :----- | :------------ | :------------------- | -------- |
| alt    | *text*        | 规定图像的替代文本。 | 必要     |
| src    | *URL*         | 规定显示图像的 URL。 | 必要     |
| title  | *text*        | 鼠标悬停显示的内容。 |          |
| height | *pixels*  *%* | 定义图像的高度。     |          |
| width  | *pixels*  *%* | 设置图像的宽度。     |          |

2. input标签

   表单输入标签，其基本语法如下：

   ```html
   <input type="属性值" value="你好">
   ```

   属性说明：

   | 属性        | 值                                                           | 描述                                        | 是否必要 |
   | :---------- | :----------------------------------------------------------- | :------------------------------------------ | -------- |
   | type        | button<br/>checkbox<br/>color<br/>date<br/>datetime<br/>datetime-local<br/>email<br/>file<br/>hidden<br/>image<br/>month<br/>number<br/>password<br/>radio<br/>range<br/>reset<br/>search<br/>submit<br/>tel<br/>text<br/>time<br/>url<br/>week | 要显示的 `<input> `元素的类型               | 必要     |
   | name        | *text*                                                       | 控件名称                                    |          |
   | value       | *text*                                                       | 控制默认值                                  |          |
   | placeholder | text                                                         | 预显示提示                                  |          |
   | checked     | checked                                                      | 在页面加载时应该被预先选定的 `<input> `元素 |          |
   | disabled    | disabled                                                     | 禁用的 `<input>` 元素                       |          |
   | readonly    | readonly                                                     | 输入字段是只读的                            |          |

3. 文本域标签

   其基本语法如下：

   ```html
   <textarea >
     默认值
   </textarea>
   ```

4. 下拉列表标签

   一般不使用，自定义下拉组件，通过 `div` + `ul` 实现。

   其基本语法如下：

   ```html
   <select name="test" id="test">
     <option value="1">1</option>
     <option value="2">2</option>
     <option value="3">3</option>
   </select>
   ```

   





---

#### [返回目录](./)