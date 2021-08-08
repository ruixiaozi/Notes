## SASS/SCSS学习笔记 CSS功能扩展

---

### 1. 嵌套

Sass 允许将一套 CSS 样式嵌套进另一套样式中，**内层的样式将它外层的选择器作为父选择器**：

```
#main p {
  color: #00ff00;
  width: 97%;

  .redbox {
    background-color: #ff0000;
    color: #000000;
  }
}
```

### 2. 父亲选择器

有时也**需要 直接 使用嵌套外层的父选择器**，用 `&` 代表嵌套规则外层的父选择器

```
a {
  &:hover { text-decoration: underline; }
}

a{
	div &{ text-decoration: underline; }
}
```

**`&` 必须作为选择器的第一个字符，其后可以跟随后缀生成复合的选择器**

```
#main {
  color: black;
  &-sidebar { border: 1px solid; }
}
```

### 3. 属性嵌套

CSS 属性遵循相同的命名空间 (namespace)，比如 `font-family, font-size, font-weight` 都以 `font` 作为属性的命名空间，Sass 允许将属性嵌套在命名空间中：

```
.funky {
  font: {
    family: fantasy;
    size: 30em;
    weight: bold;
  }
}
```

命名空间也可以包含自己的属性值:

```
.funky {
  font: 20px/24px { //自己的属性值
    family: fantasy;
    weight: bold;
  }
}
```

### 4. 占位符选择器

用 `%名称` 来定义个占位选择器，通过 `@extend` 指令使用这个占位选择器。占位选择器定义的样式只用于sass中，不会实际编译到css中。





---

#### [返回目录](./)