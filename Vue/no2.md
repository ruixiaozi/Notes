## Vue全家桶学习笔记 基础语法
---
### 1. 插值语法

1. mustache（`{{要显示的值}}`）
2. v-once
3. v-html
4. v-text
5. v-pre
6. v-cloak

---
### 2. 属性绑定（v-bind:XXX 或 :XXX）

1. 普通属性
2. class与style

---
### 3. 计算属性

1. 用法(getter和setter)
2. 缓存机制


---
### 4. 事件监听（v-on:XXX 或 @XXX）

1. 普通用法
2. 带参数用法（传入$event）
3. 修饰符用法（在@XXX后面加.修饰符）
    + .stop - 调用 event.stopPropagation()。
    + .prevent - 调用 event.preventDefault()。
    + .{keyCode | keyAlias} - 只当事件是从特定键触发时才触发回调。
    + .native - 监听组件根元素的原生事件。
    + .once - 只触发一次回调。


---
### 5. 条件与循环  

1. 条件  
    + v-if、v-else-if、v-else  
        例如：`v-if="score >= 90"`

        v-if后面的条件为false时，对应的元素以及其子元素不会渲染。也就是根本没有不会有对应的标签出现在DOM中。

        注意：***应该使用`key`来标识if、else的相同html元素，保证重新渲染html***，这是因为Vue在进行DOM渲染时，出于性能考虑，会尽可能的复用已经存在的元素，而不是重新创建新的元素。
    + v-show  
        例如：`v-show="true"`  

        v-show当条件为false时，仅仅是将元素的display属性设置为none而已。

2. 循环(v-for)  

    + 基本用法(`v-for="(item, index) in items
"`)
    + 遍历对象用法(`v-for="(value, key, index) in object
"`)

        注意：***尽量给v-for的每一项加上一个唯一的`:key`属性，能够提升在列表中插入和删除一个元素的效率***

        能触发界面更新的数组操作：

        + push()
        + pop()
        + shift()
        + unshift()
        + splice()
        + sort()
        + reverse()
        + Vue.set()

---
### 6. 过滤器

1. 基本用法

    过滤器可以用在两个地方：***双花括号插值***和 ***v-bind 表达式*** (后者从 2.1.0+ 开始支持)。过滤器应该被添加在 JavaScript 表达式的尾部，由“管道”符号指示：

    ```
    <!-- 在双花括号中 -->
    {{ message | capitalize }}

    <!-- 在 `v-bind` 中 -->
    <div v-bind:id="rawId | formatId"></div>
    ```

    过滤器函数总接收表达式的值 (之前的操作链的结果) 作为第一个参数。过滤器可以串联：
    ```
    {{ message | filterA | filterB }}
    ```
    过滤器是 JavaScript 函数，因此可以接收参数：
    ```
    {{ message | filterA('arg1', arg2) }}
    ```
    filterA 被定义为接收三个参数的过滤器函数。其中 message 的值作为第一个参数，普通字符串 'arg1' 作为第二个参数，表达式 arg2 的值作为第三个参数。


---
### 6. 双向绑定（v-model）

1. 基本使用 
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

2. 与radio/checkbox/select结合
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
### 7. 生命周期

***红色框***表示可以可以作为钩子绑定方法进行自定义操作。

![生命周期](./image/lifecycle.png)




---

#### [返回目录](./)
