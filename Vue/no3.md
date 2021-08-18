## Vue全家桶学习笔记 模板语法
### 1.  插值语法

#### 1.1 **mustache**（`{{要显示的值}}`）

```
<span>Message: {{ msg }}</span>
```

#### 1.2 **v-once** 

只会执行一次性地插值，当数据改变时，插值处的内容不会更新。

```
<span v-once>这个将不会改变: {{ msg }}</span>
```

#### 1.3 **v-html** 

输出真正的 HTML

```
<p>Using v-html directive: <span v-html="rawHtml"></span></p>
```

#### 1.4 **v-text** 

更新元素的 `textContent`

```
<span v-text="msg"></span>
```

#### 1.5 **v-pre** 

跳过这个元素和它的子元素的编译过程（即：插值不需要编译）

```
<span v-pre>{{ this will not be compiled }}</span>
```

#### 1.6 **v-cloak** 

这个指令保持在元素上直到关联实例结束编译（即：如果插值编译未结束，则这个标签有v-cloak属性，可以配合css使用）

```
[v-cloak] {
  display: none;
}
<div v-cloak>
  {{ message }}
</div>
//不会显示，直到编译结束。
```

---

### 2. 属性绑定（v-bind:XXX 或 :XXX）

#### 2.1 普通属性

```
<div v-bind:id="dynamicId"></div>
```

#### 2.2 布尔类型属性

对于布尔 attribute (**它们只要存在就意味着值为 `true`**)，`v-bind` 工作起来略有不同，在这个例子中：

```
<button v-bind:disabled="isButtonDisabled">Button</button>
```

如果 `isButtonDisabled` 的值是 `null`、`undefined` 或 `false`，则 `disabled` attribute 甚至不会被包含在渲染出来的 `<button>` 元素中。

#### 2.3 class与style

操作元素的 class 列表和内联样式是数据绑定的一个常见需求。因为它们都是 attribute，所以我们可以用 `v-bind` 处理它们：只需要通过表达式计算出字符串结果即可。不过，字符串拼接麻烦且易错。因此，在将 `v-bind` 用于 `class` 和 `style` 时，Vue.js 做了专门的增强。表达式结果的类型除了字符串之外，还可以是对象或数组。

`v-bind:class`  和 `v-bind:style`指令也可以与普通的 class attribute 共存

+ **class**

  **当在一个自定义组件上使用 `class` property 时，这些 class 将被添加到该组件的根元素上面。这个元素上已经存在的 class 不会被覆盖。**

  + 对象

    对象属性的key为相应的class名称，value为boolean类型，表示是否存在该class：

    ```
    <div
      class="static"
      v-bind:class="{ active: isActive, 'text-danger': hasError }"
    ></div>
    
    data: {
      isActive: true,
      hasError: false
    }
    ```

  + 数组

    可以把一个数组传给 `v-bind:class`，以应用一个 class 列表：

    ```
    <div v-bind:class="[activeClass, errorClass]"></div>
    
    data: {
      activeClass: 'active',
      errorClass: 'text-danger'
    }
    ```

    在数组语法中也可以使用对象语法:

    ```
    <div v-bind:class="[{ active: isActive }, errorClass]"></div>
    ```

    

+ **style**

  当 `v-bind:style` 使用需要添加浏览器引擎前缀的 CSS property 时，如 `transform`，Vue.js 会自动侦测并添加相应的前缀。

  + 对象

    对象语法十分直观——看着非常像 CSS，但其实是一个 JavaScript 对象。CSS property 名可以用驼峰式 (camelCase) 或短横线分隔 (kebab-case，记得用引号括起来) 来命名：

    ```
    <div v-bind:style="{ color: activeColor, fontSize: fontSize + 'px' }"></div>
    ```

    ```
    data: {
      activeColor: 'red',
      fontSize: 30
    }
    ```

  + 数组

    数组语法可以将多个样式对象应用到同一个元素上（相当于混入样式）：

    ```
    <div v-bind:style="[baseStyles, overridingStyles]"></div>
    ```

    

---

### 3. js表达式

在模板语法中，对于所有的数据绑定，Vue.js 都提供了完全的 JavaScript 表达式支持。这些表达式会在所属 Vue 实例的数据作用域下作为 JavaScript 被解析

```
{{ number + 1 }}

{{ ok ? 'YES' : 'NO' }}

{{ message.split('').reverse().join('') }}

<div v-bind:id="'list-' + id"></div>
```



---

#### [返回目录](./)
