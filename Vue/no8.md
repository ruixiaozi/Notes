## Vue全家桶学习笔记  事件处理
 ### 1. 监听事件（v-on）

#### 1.1 直接执行简单js代码

```
 <button v-on:click="counter += 1">Add 1</button>
```

#### 1.2 绑定方法

```
<div id="example-2">
  <!-- `greet` 是在下面定义的方法名 -->
  <button v-on:click="greet">Greet</button>
</div>

var example2 = new Vue({
  el: '#example-2',
  data: {
    name: 'Vue.js'
  },
  // 在 `methods` 对象中定义方法
  methods: {
    greet: function (event) {
      // `this` 在方法里指向当前 Vue 实例
      alert('Hello ' + this.name + '!')
      // `event` 是原生 DOM 事件
      if (event) {
        alert(event.target.tagName)
      }
    }
  }
})
```

#### 1.3 调用内链方法

可以传入$event来设置event值

```
<button v-on:click="warn('Form cannot be submitted yet.', $event)">
  Submit
</button>

methods: {
  warn: function (message, event) {
    // 现在我们可以访问原生事件对象
    if (event) {
      event.preventDefault()
    }
    alert(message)
  }
}
```

#### 1.4 绑定一个对象

对象的属性名为事件名，属性值为回调函数

```
<input v-on="inputListeners" />

Vue.component('base-input', {
  computed: {
    inputListeners: function () {
      return {
                input: function (event) {
                	vm.$emit('input', event.target.value)
                }
             }
    }
  },
```



---

### 2. 修饰符

#### 2.1 事件修饰符

在事件处理程序中调用 `event.preventDefault()` 或 `event.stopPropagation()` 是非常常见的需求。尽管我们可以在方法中轻松实现这点，但更好的方式是：方法只有纯粹的数据逻辑，而不是去处理 DOM 事件细节。

为了解决这个问题，Vue.js 为 `v-on` 提供了**事件修饰符**。之前提过，修饰符是由点开头的指令后缀来表示的。

- `.stop` 阻止单击事件继续传播
- `.prevent` 阻止默认行为
- `.capture` 捕获的方式，先调用这个捕获处理，再调用其他事件处理（内部）
- `.self`  只有当前元素
- `.once` 触发一次
- `.passive` 默认行为 将会立即触发

```
<!-- 阻止单击事件继续传播 -->
<a v-on:click.stop="doThis"></a>

<!-- 提交事件不再重载页面 -->
<form v-on:submit.prevent="onSubmit"></form>

<!-- 修饰符可以串联 -->
<a v-on:click.stop.prevent="doThat"></a>

<!-- 只有修饰符 -->
<form v-on:submit.prevent></form>

<!-- 添加事件监听器时使用事件捕获模式 -->
<!-- 即内部元素触发的事件先在此处理，然后才交由内部元素进行处理 -->
<div v-on:click.capture="doThis">...</div>

<!-- 只当在 event.target 是当前元素自身时触发处理函数 -->
<!-- 即事件不是从内部元素触发的 -->
<div v-on:click.self="doThat">...</div>

<!-- 点击事件将只会触发一次 -->
<a v-on:click.once="doThis"></a>

<!-- 滚动事件的默认行为 (即滚动行为) 将会立即触发 -->
<!-- 而不会等待 `onScroll` 完成  -->
<!-- 这其中包含 `event.preventDefault()` 的情况 -->
<div v-on:scroll.passive="onScroll">...</div>
```

使用修饰符时，顺序很重要；相应的代码会以同样的顺序产生。因此，用 `v-on:click.prevent.self` 会阻止**所有的点击**，而 `v-on:click.self.prevent` 只会阻止对元素自身的点击。

不要把 `.passive` 和 `.prevent` 一起使用，因为 `.prevent` 将会被忽略，同时浏览器可能会向你展示一个警告。请记住，`.passive` 会告诉浏览器你*不*想阻止事件的默认行为。

#### 2.2 按键修饰符

在监听键盘事件时，我们经常需要检查详细的按键。Vue 允许为 `v-on` 在监听键盘事件时添加按键修饰符：

```
<!-- 只有在 `key` 是 `Enter` 时调用 `vm.submit()` -->
<input v-on:keyup.enter="submit">
```

你可以直接将 `KeyboardEvent.key` 暴露的任意有效按键名转换为 kebab-case 来作为修饰符。

```
<input v-on:keyup.page-down="onPageDown">
```

在上述示例中，处理函数只会在 `$event.key` 等于 `PageDown` 时被调用。

+ 系统按键修饰符

  + `.ctrl`

  + `.alt`

  + `.shift`

  + `.meta`

  + `.exact` 修饰符允许你控制由精确的系统修饰符组合触发的事件。(只能是当前的这些按键，多或者少都不行)

  + `.left` 鼠标左键

  + `.right` 鼠标右键

  + `.middle` 鼠标中键

    ```
    <!-- 即使 Alt 或 Shift 被一同按下时也会触发 -->
    <button v-on:click.ctrl="onClick">A</button>
    
    <!-- 有且只有 Ctrl 被按下的时候才触发 -->
    <button v-on:click.ctrl.exact="onCtrlClick">A</button>
    
    <!-- 没有任何系统修饰符被按下的时候才触发 -->
    <button v-on:click.exact="onClick">A</button>
    ```

  > 注意：在 Mac 系统键盘上，meta 对应 command 键 (⌘)。在 Windows 系统键盘 meta 对应 Windows 徽标键 (⊞)。在 Sun 操作系统键盘上，meta 对应实心宝石键 (◆)。在其他特定键盘上，尤其在 MIT 和 Lisp 机器的键盘、以及其后继产品，比如 Knight 键盘、space-cadet 键盘，meta 被标记为“META”。在 Symbolics 键盘上，meta 被标记为“META”或者“Meta”。

  ```
  <!-- Alt + C -->
  <input v-on:keyup.alt.67="clear">
  
  <!-- Ctrl + Click -->
  <div v-on:click.ctrl="doSomething">Do something</div>
  ```


#### 2.3 原生事件修饰符

你可能有很多次想要在一个组件的根元素上直接监听一个原生事件。这时，你可以使用 `v-on` 的 `.native` 修饰符：

```
<base-input v-on:focus.native="onFocus"></base-input>
```





---

#### [返回目录](./)
