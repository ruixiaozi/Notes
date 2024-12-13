## SASS/SCSS学习笔记 变量、类型与运算

---

## 1. 变量

变量以美元符号开头，赋值方法与 CSS 属性的写法一样：

```
$width: 5em;
//直接使用即调用变量：

#main {
  width: $width;
}
```

变量支持块级作用域，嵌套规则内定义的变量只能在嵌套规则内使用（局部变量），不在嵌套规则内定义的变量则可在任何地方使用（全局变量）。将局部变量转换为全局变量可以添加 `!global`

```
#main {
  $width: 5em !global;
  width: $width;
}

#sidebar {
  width: $width;
}
```

特殊变量：`&` ，&可以作为值进行操作，他表示父选择器的名称

## 2. 数据类型

SassScript 支持 6 种主要的数据类型：

- 数字，`1, 2, 13, 10px`
- 字符串，有引号字符串与无引号字符串，`"foo", 'bar', baz`
- 颜色，`blue, #04a3f9, rgba(255,0,0,0.5)`
- 布尔型，`true, false`
- 空值，`null`
- 数组 (list)，用空格或逗号作分隔符，`1.5em 1em 0 2em, Helvetica, Arial, sans-serif`
- maps, 相当于 JavaScript 的 object，`(key1: value1, key2: value2)`

SassScript 也支持其他 CSS 属性值，比如 Unicode 字符集，或 `!important` 声明。然而Sass 不会特殊对待这些属性值，一律视为无引号字符串

**其中数组：**

数组本身没有太多功能，但Sass方法 赋予了数组更多新功能：`nth` 函数可以直接访问数组中的某一项；`join` 函数可以将多个数组连接在一起；`append` 函数可以在数组中添加新值；而 `@each` 指令能够遍历数组中的每一项。

数组中可以包含子数组，比如 `1px 2px, 5px 6px` 是包含 `1px 2px` 与 `5px 6px` 两个数组的数组。如果内外两层数组使用相同的分隔方式，**需要用圆括号包裹内层**，所以也可以写成 `(1px 2px) (5px 6px)`。变化是，之前的 `1px 2px, 5px 6px` 使用逗号分割了两个子数组 (comma-separated)，而 `(1px 2px) (5px 6px)` 则使用空格分割(space-separated)。

当数组被编译为 CSS 时，Sass 不会添加任何圆括号（CSS 中没有这种写法），所以 `(1px 2px) (5px 6px)` 与 `1px 2px, 5px 6px` 在编译后的 CSS 文件中是完全一样的，但是它们在 Sass 文件中却有不同的意义，前者是包含两个数组的数组，而后者是包含四个值的数组。

用 `()` 表示不包含任何值的空数组（在 Sass 3.3 版之后也视为空的 map）。空数组不可以直接编译成 CSS，比如编译 `font-family: ()` Sass 将会报错。如果数组中包含空数组或空值，编译时将被清除，比如 `1px 2px () 3px` 或 `1px 2px null 3px`。

基于逗号分隔的数组允许保留结尾的逗号，这样做的意义是强调数组的结构关系，尤其是需要声明只包含单个值的数组时。例如 `(1,)` 表示只包含 `1` 的数组，而 `(1 2 3,)` 表示包含 `1 2 3` 这个以空格分隔的数组的数组。

## 3. 运算

### 3.1 数字运算

SassScript 支持数字的加减乘除、取整等运算 (`+, -, *, /, %`)，如果必要会在不同单位间转换值。

```
p {
  width: 1in + 8pt;
}
```

关系运算 `<, >, <=, >=` 也可用于数字运算，相等运算 `==, !=` 可用于所有数据类型。

### 3.2 颜色值运算

颜色值的运算是分段计算进行的，也就是分别计算红色，绿色，以及蓝色的值：

```scss
p {
  color: #010203 + #040506;
}
// color: #050709; 
//使用 color functions 比计算颜色值更方便一些。

//需要注意的是，如果颜色值包含 alpha channel（rgba 或 hsla 两种颜色值），必须拥有相等的 alpha 值才能进行运算，因为算术运算不会作用于 alpha 值。
p {
  color: rgba(255, 0, 0, 0.75) + rgba(0, 255, 0, 0.75);
}
```

### 3.3 字符串运算 

`+` 可用于连接字符串

```
p {
  cursor: e + -resize;
}
//如果有引号字符串（位于 + 左侧）连接无引号字符串，运算结果是有引号的，相反，无引号字符串（位于 + 左侧）连接有引号字符串，运算结果则没有引号
p:before {
  content: "Foo " + Bar;
  font-family: sans- + "serif";
}
// content: "Foo Bar";
// font-family: sans-serif;
```

### 3.4 布尔运算

SassScript 支持布尔型的 `and` `or` 以及 `not` 运算。

### 3.5 圆括号

圆括号可以用来影响运算的顺序：

```
p {
  width: 1em + (2em * 3);
}
```

### 3.6 函数调用

SassScript 定义了多种函数，有些甚至可以通过普通的 CSS 语句调用

```
p {
  color: hsl(0, 100%, 50%);
}
//Sass 函数允许使用关键词参数 (keyword arguments)，上面的例子也可以写成：
//关键词参数可以打乱顺序使用，如果使用默认值也可以省缺，另外，参数名被视为变量名
p {
  color: hsl($hue: 0, $saturation: 100%, $lightness: 50%);
}
```

### 3.7 插值语句

通过 `#{}` 插值语句可以在选择器或属性名中使用变量：

```
$name: foo;
$attr: border;
p.#{$name} {
  #{$attr}-color: blue;
}
```

`#{}` 插值语句也可以在属性值中插入 SassScript，大多数情况下，这样可能还不如使用变量方便，但是使用 `#{}` 可以避免 Sass 运行运算表达式，直接编译 CSS。

```
p {
  $font-size: 12px;
  $line-height: 30px;
  font: #{$font-size}/#{$line-height};
}
```

### 3.8 !defulat 运算符

在变量的结尾添加 `!default` 可以给没有赋值的变量定义初始值，如果变量已经被赋值，不会再被重新赋值，但是如果变量还没有被赋值，则会被赋予新的值。

```
$content: "First content";
$content: "Second content?" !default;
$new_content: "First time reference" !default;

#main {
  content: $content;
  new-content: $new_content;
}

=>

#main {
  content: "First content";
  new-content: "First time reference"; }
```





---

#### [返回目录](./)