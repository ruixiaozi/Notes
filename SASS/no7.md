## SASS/SCSS学习笔记 函数与全局函数

---

Sass 支持自定义函数，并能在任何属性值或 Sass script 中使用：

```
$grid-width: 40px;
$gutter-width: 10px;

@function grid-width($n) {
  @return $n * $grid-width + ($n - 1) * $gutter-width;
}

#sidebar { width: grid-width(5); }
```

**特殊函数**：

- sass:math 模块，提供对数字进行操作的函数。
- sass:string 模块，使组合、搜索或拆分字符串变得很容易。
- sass:color 模块，根据现有的颜色生成新的颜色，使得构建颜色主题变得很容易。
- sass:list 模块，允许您访问和修改列表中的值。
- sass:map 模块，使查找与映射中的键关联的值成为可能，并且还有更多功能。
- sass:selector 模块，提供对强大的Sass选择器引擎的访问方法。
- sass:meta 模块，暴露了sass内部工作的细节

## 1. 全局函数

### 1.1 hsl()

- **包含函数：**

  - `hsl($hue $saturation $lightness)`
  - `hsl($hue $saturation $lightness / $alpha)`
  - `hsl($hue, $saturation, $lightness, $alpha: 1)`
  - `hsla($hue $saturation $lightness)`
  - `hsla($hue $saturation $lightness / $alpha)`
  - `hsla($hue, $saturation, $lightness, $alpha: 1)`

- **返回值：**color

- **用法：**

  返回具有给定[色相、饱和度和亮度](https://en.wikipedia.org/wiki/HSL_and_HSV)和alpha通道的颜色。

  色调是`0deg <= num <= 360deg`的一个数字。饱和度和亮度是`0% <= num <= 100%`的一个数字。所有这些数可能都是**无单位**的。alpha通道可以指定为`0 <= num <= 1`的一个无单元数，也可以指定为`0% <= num <= 100%`之间的百分比。

  您可以将诸如`calc()`或`var()`这样的特殊函数传递给`hsl()`来代替任何参数。您甚至可以使用`var()`来代替多个参数，因为它可能被多个值替换！当以这种方式调用颜色函数时，它将使用与调用时相同的方法返回未引用的字符串。

  ```
  @debug hsl(210deg 100% 20%); // #036
  @debug hsl(34, 35%, 92%); // #f2ece4
  @debug hsl(210deg 100% 20% / 50%); // rgba(0, 51, 102, 0.5)
  @debug hsla(34, 35%, 92%, 0.2); // rgba(242, 236, 228, 0.2)
  ```

### 1.2 if()

- **包含函数：**

  - `if($condition, $if-true, $if-false)`

- **返回值：**boolean

- **用法：**

  这个函数的特殊之处在于，它甚至不计算未返回的参数的值，所以即使未使用的参数会抛出错误，调用它也是安全的。

  ```
  @debug if(true, 10px, 15px); // 10px
  @debug if(false, 10px, 15px); // 15px
  @debug if(variable-defined($var), $var, null); // null
  ```

### 1.3 rgb()

- **包含函数：**

  - `rgb($red $green $blue)`
  - `rgb($red $green $blue / $alpha)`
  - `rgb($red, $green, $blue, $alpha: 1)`
  - `rgb($color, $alpha)`
  - `rgba($red $green $blue)`
  - `rgba($red $green $blue / $alpha)`
  - `rgba($red, $green, $blue, $alpha: 1)`
  - `rgba($color, $alpha)`

- **返回值：**color

- **用法：**

  如果传递了`$red、$green、$blue`和可选的`$alpha`，则返回具有给定的红色、绿色、蓝色和alpha通道的颜色。

  每个颜色通道可以指定为0到255之间的无单位数字单位)（包括0、255），或`0%`到`100%`之间的百分比（包括0%、100%）。alpha通道可以指定为0到1之间的无单位数字（包括0、1），也可以指定为`0%`到`100%`之间的百分比（包括0%、100%）。
  
  ```
  @debug rgb(0 51 102); // #036
  @debug rgb(95%, 92.5%, 89.5%); // #f2ece4
  @debug rgb(0 51 102 / 50%); // rgba(0, 51, 102, 0.5)
  @debug rgba(95%, 92.5%, 89.5%, 0.2); // rgba(242, 236, 228, 0.2)
  ```





---

#### [返回目录](./)