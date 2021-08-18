## Vue全家桶学习笔记  双向绑定与表单
---
### 1. 基本使用 

+ 它的背后本质上是包含两个操作：
    1. v-bind绑定一个value属性
    2. v-on指令给当前元素绑定input事件
+ 下面两个代码的意义相同：
    ```
    <input type="text" v-model="message">
    ```
    与
    ``` 
    <input type="text" v-bind:value="message" v-on:input="message = $event.target.value">
    ```

### 2. 与radio/checkbox/select结合

+ radio结合  
    在每个radio中加入`v-model="变量名"`
+ checkbox结合  
    1. 单选：`v-model`绑定一个boolean变量
    2. 多选：`v-model`绑定一个数组，checkbox的value值作为数组元素。
+ select结合  
    1. 单选：`v-model`绑定一个变量，值为选中的value
    2. 多选：`v-model`绑定一个数组

3. 修饰符

    + lazy：lazy修饰符可以让数据在***失去焦点***或者***回车***时才会更新。
    + number：number修饰符可以让在输入框中输入的内容***自动转成数字类型***。
    + trim：trim修饰符可以过滤内容左右两边的空格。

---



---

#### [返回目录](./)
