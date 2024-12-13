## 前端面试错题集 a链接css设置

---

解析：a:link,a:visited,a:hover,a:active 分别是什么意思?

1. link:连接平常的状态

2. visited:连接被访问过之后
3. hover:鼠标放到连接上的时候

4. active:连接被按下的时候



正确顺序：“爱恨原则”（LoVe/HAte），即四种伪类的首字母:LVHA。再重复一遍正确的顺序：a:link、a:visited、a:hover、a:active .

a:link、a:visited、a:focus、a:hover、a:active；推荐的顺序是：LVFHA



如果未按照这个顺序来则会出现以下问题（因为就近原则的影响）：

因为当鼠标经过未访问的链接，会同时拥有a:link、a:hover两种属性，a:link离它最近，所以它优先满足a:link，而放弃a:hover的重复定义。当鼠标经过已经访问过的链接，会同时拥有a:visited、a:hover两种属性，a:visited离它最近，所以它优先满足a:visited，而放弃a:hover的重复定义。究其原因，是css的就近原则“惹的祸”。

---

#### [返回目录](./)



