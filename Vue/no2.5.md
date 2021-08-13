## Vue全家桶学习笔记 条件与循环  
---
### 1. 条件  

+ v-if、v-else-if、v-else  
    例如：`v-if="score >= 90"`

    v-if后面的条件为false时，对应的元素以及其子元素不会渲染。也就是根本没有不会有对应的标签出现在DOM中。

    注意：***应该使用`key`来标识if、else的相同html元素，保证重新渲染html***，这是因为Vue在进行DOM渲染时，出于性能考虑，会尽可能的复用已经存在的元素，而不是重新创建新的元素。
+ v-show  
    例如：`v-show="true"`  

    v-show当条件为false时，仅仅是将元素的display属性设置为none而已。

### 2. 循环(v-for)  

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

#### [返回目录](./)
