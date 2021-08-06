## SASS/SCSS学习笔记 @规则

## 1. @import

Sass 拓展了 `@import` 的功能，允许其导入 SCSS 或 Sass 文件。被导入的文件将合并编译到同一个 CSS 文件中，另外，被导入的文件中所包含的变量或者混合指令 (mixin) 都可以在导入的文件中使用。

在以下情况下，`@import` 仅作为普通的 CSS 语句，不会导入任何 Sass 文件。

- 文件拓展名是 `.css`；
- 文件名以 `http://` 开头；
- 文件名是 `url()`；
- `@import` 包含 media queries。

文件的拓展名是 `.scss` 或 `.sass`，则导入成功。没有指定拓展名，Sass 将会试着寻找文件名相同，拓展名为 `.scss` 或 `.sass` 的文件并将其导入；支持同时导入多个文件:

```
@import "foo.scss";
@import "foo";
@import "rounded-corners", "text-shadow";
```

可以将 `@import` 嵌套进 CSS 样式或者 `@media` 中，与平时的用法效果相同，只是这样导入的样式只能出现在嵌套的层中。

```
// example.scss 
.example {
  color: red;
}

//main.scss
#main {
  @import "example";
}
```

## 2. @media

Sass 中 `@media` 指令与 CSS 中用法一样，只是增加了一点额外的功能：允许其在 CSS 规则中嵌套。如果 `@media` 嵌套在 CSS 规则内，编译时，`@media` 将被编译到文件的最外层，包含嵌套的父选择器。这个功能让 `@media` 用起来更方便，不需要重复使用选择器，也不会打乱 CSS 的书写流程。

```scss
.sidebar {
  width: 300px;
  @media screen and (orientation: landscape) {
    width: 500px;
  }
}

=>

.sidebar {
  width: 300px; }
  @media screen and (orientation: landscape) {
    .sidebar {
      width: 500px; } }
```

@media 的 queries 允许互相嵌套使用，编译时，Sass 自动添加 and

```scss
@media screen {
  .sidebar {
    @media (orientation: landscape) {
      width: 500px;
    }
  }
}

=>

@media screen and (orientation: landscape) {
  .sidebar {
    width: 500px; } }
```

`@media` 甚至可以使用 SassScript（比如变量，函数，以及运算符）代替条件的名称或者值：

```
$media: screen;
$feature: -webkit-min-device-pixel-ratio;
$value: 1.5;

@media #{$media} and ($feature: $value) {
  .sidebar {
    width: 500px;
  }
}

=>

@media screen and (-webkit-min-device-pixel-ratio: 1.5) {
  .sidebar {
    width: 500px; } }
```

## 3. @extend

用于：**一个元素使用的样式与另一个元素完全相同，但又添加了额外的样式**，相当于是**继承**另一个元素的样式。

```
//@extend 的作用是将重复使用的样式 (.error) 延伸 (extend) 给需要包含这个样式的特殊样式（.seriousError）
.error {
  border: 1px #f00;
  background-color: #fdd;
}
.error.intrusion {
  background-image: url("/image/hacked.png");
}
.seriousError {
  @extend .error;
  border-width: 3px;
}

=>

.error, .seriousError {
  border: 1px #f00;
  background-color: #fdd; }

.error.intrusion, .seriousError.intrusion {
  background-image: url("/image/hacked.png"); }

.seriousError {
  border-width: 3px; }
```

 延伸复杂的选择器 (Extending Complex Selectors):

```
//所有 a:hover 的样式将继承给 .hoverlink，包括其他使用到 a:hover 的样式，例如
.hoverlink {
  @extend a:hover;
}
.comment a.user:hover {
  font-weight: bold;
}
=>
.comment a.user:hover, .comment .user.hoverlink {
  font-weight: bold; }
```

多重延伸：

```
.error {
  border: 1px #f00;
  background-color: #fdd;
}
.attention {
  font-size: 3em;
  background-color: #ff0;
}
.seriousError {
  @extend .error, .attention;
  border-width: 3px;
}
```

重要：配合占位符使用

```
//占位符选择器，没有其他任何意义，仅仅由@extend时，标识作用
#context a%extreme {
  color: blue;
  font-weight: bold;
  font-size: 2em;
}

//所有notice都会扩展%extreme占位了的选择器
.notice {
  @extend %extreme;
}
```

## 4. @at-root

使一个或多个规则被限定输出在文档的根层级上，而不是被嵌套在其父选择器下。

```
.parent{
  color:red;
  @at-root .child {
    width:200px;
    height:50px;
  }
}
=>
.parent {
  color: red;
}
.child {
  width: 200px;
  height: 50px; 
}
```

默认 @at-root 只会跳出选择器嵌套，而不能跳出 @media 或 @support，如果要跳出这两种，则需使用 @at-root(without: media)，@at-root(without: support)。这个语法的关键词有

四个：all（表示所有）, rule（表示常规）,  media（表示 media），support（表示 support ）。我们默认的 @at-root 其实就是 @at-root( without: rule )。

## 5. @debug

@debug 指令将 SassScript 表达式的值打印到标准错误输出流.

```
@debug 10em + 12em;
```

## 6. @warn

@warn 指令将 SassScript 表达式的值打印到标准错误输出流。

@warn 和 @debug 之间有两个主要区别：

1. 您可以使用 --quiet 命令行选项或 :quiet Sass 选项关闭警告。
2. 样式表跟踪将与消息一起打印出来，以便被警告的用户可以看到他们的样式导致警告的位置

## 7. @error

@error 指令将 SassScript 表达式的值作为致命错误抛出，包括一个很好的堆栈跟踪。

## 8. @use

该`@use`规则从其他 Sass 样式表加载，并将来自多个样式表的 CSS 组合在一起。加载的样式表`@use`称为“模块”

与@import类似，不过@use需要带上命名空间，访问的变量，函数和混入`<namespace>.<variable>`，`<namespace>.<function>()`或`@include <namespace>.<mixin>()`。默认情况下，命名空间只是模块URL的最后一个组件 。

```
// style.scss
@use "src/corners";

.button {
  @include corners.rounded;
  padding: 5px + corners.$radius;
}
```

也可以自定义命名空间：

```
// style.scss
@use "src/corners" as c;

.button {
  @include c.rounded;
  padding: 5px + c.$radius;
}
```







---

#### [返回目录](./)

