## Vue全家桶学习笔记  双向绑定与表单
---
### 1. 基本使用 

#### 1.1 基本原理（v-model）

它的背后本质上是包含两个操作：

1. v-bind绑定一个属性
2. v-on指令给当前元素绑定事件

- text 和 textarea 元素使用 `value` property 和 `input` 事件；
- checkbox 和 radio 使用 `checked` property 和 `change` 事件；
- select 字段将 `value` 作为 prop 并将 `change` 作为事件

下面两个代码的意义相同：

```
<input type="text" v-model="message">
```
与

``` 
<input type="text" v-bind:value="message" v-on:input="message = $event.target.value">
```

#### 1.2 表单用法

+ 文本

  ```
  <input v-model="message" placeholder="edit me">
  <p>Message is: {{ message }}</p>
  ```

+ 多行文本

  ```
  <span>Multiline message is:</span>
  <p style="white-space: pre-line;">{{ message }}</p>
  <br>
  <textarea v-model="message" placeholder="add multiple lines"></textarea>
  ```

+ 复选框（两种形式）

  ```
  //单个复选框，对应一个布尔值（或者使用对应的字符串）
  <input type="checkbox" id="checkbox" v-model="checked">
  <label for="checkbox">{{ checked }}</label>
  
  <input
    type="checkbox"
    v-model="toggle"
    true-value="yes"
    false-value="no"
  >
  // 当选中时
  vm.toggle === 'yes'
  // 当没有选中时
  vm.toggle === 'no'
  
  //多个复选框，对应一个数组
  <input type="checkbox" id="jack" value="Jack" v-model="checkedNames">
  <label for="jack">Jack</label>
  <input type="checkbox" id="john" value="John" v-model="checkedNames">
  <label for="john">John</label>
  <input type="checkbox" id="mike" value="Mike" v-model="checkedNames">
  <label for="mike">Mike</label>
  <br>
  <span>Checked names: {{ checkedNames }}</span>
  
  new Vue({
    el: '...',
    data: {
      checkedNames: []
    }
  })
  ```

+ 单选按钮

  ```
  <div id="example-4">
    <input type="radio" id="one" value="One" v-model="picked">
    <label for="one">One</label>
    <br>
    <input type="radio" id="two" value="Two" v-model="picked">
    <label for="two">Two</label>
    <br>
    <span>Picked: {{ picked }}</span>
  </div>
  
  new Vue({
    el: '#example-4',
    data: {
      picked: ''
    }
  })
  ```

+ 下拉选择框

  ```
  <div id="example-5">
    <select v-model="selected">
      <option disabled value="">请选择</option>
      <option>A</option>
      <option>B</option>
      <option>C</option>
    </select>
    <span>Selected: {{ selected }}</span>
  </div>
  ```

  如果 `v-model` 表达式的初始值未能匹配任何选项，`<select>` 元素将被渲染为“未选中”状态。在 iOS 中，这会使用户无法选择第一个选项。因为这样的情况下，iOS 不会触发 change 事件。因此，更推荐像上面这样提供一个值为空的禁用选项。

  多选(绑定数组)：

  ```
  <div id="example-6">
    <select v-model="selected" multiple style="width: 50px;">
      <option>A</option>
      <option>B</option>
      <option>C</option>
    </select>
    <br>
    <span>Selected: {{ selected }}</span>
  </div>
  
  new Vue({
    el: '#example-6',
    data: {
      selected: []
    }
  })
  ```

### 2. 修饰符

#### 2.1 `.lazy`

在默认情况下，`v-model` 在每次 `input` 事件触发后将输入框的值与数据进行同步 (除了上述输入法组合文字时)。你可以添加 `lazy` 修饰符，从而转为在 `change` 事件_之后_进行同步：

```
<!-- 在“change”时而非“input”时更新 -->
<input v-model.lazy="msg">
```

#### 2.2 `.number`

如果想自动将用户的输入值转为数值类型，可以给 `v-model` 添加 `number` 修饰符：

```
<input v-model.number="age" type="number">
```

这通常很有用，因为即使在 `type="number"` 时，HTML 输入元素的值也总会返回字符串。如果这个值无法被 `parseFloat()` 解析，则会返回原始的值。

#### 2.3 `.trim`

如果要自动过滤用户输入的首尾空白字符，可以给 `v-model` 添加 `trim` 修饰符：

```
<input v-model.trim="msg">
```

---



---

#### [返回目录](./)
