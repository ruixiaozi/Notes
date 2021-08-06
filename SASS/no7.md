## SASS/SCSS学习笔记 函数与特殊函数

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

## 2. 颜色模块（sass:color）

### 2.1 color.adjust()/adjust-color()，修改某个颜色值

- **包含函数：**

  - `color.adjust($color,$red: null, $green: null, $blue: null,$hue: null, $saturation: null, $lightness: null,$alpha: null)`
  - `adjust-color(...)`

- **返回值：**color

- **用法：**

  增加或减少`$color`的一个或多个属性，返回调整后的颜色。

  不能同时设置RGB（`$red,$green,$blue`）和HSL（`$hue,$saturation,$lightness`）属性的的值。

  所有可选参数必须是数字。`$red,$green,$blue`参数必须是-255到255之间的无单位数字单位)（包括-255、255）。`$hue`参数必须包含单位`deg`或没有单位。`$saturation`和`$lightness`参数必须介于-100%和100%之间（包括-100%、100%），并且可能是无单位的。`$alpha`参数必须-1和1之间的无单位数字（包括-1，1）。

  类似功能的函数：

  - color.scale()，缩放、扩大颜色的属性。
  - color.change()，设置颜色的属性值。

  ```
  @debug color.adjust(#6b717f, $red: 15); // #7a717f
  @debug color.adjust(#d2e1dd, $red: -10, $blue: 10); // #c8e1e7
  @debug color.adjust(#998099, $lightness: -30%, $alpha: -0.4); // rgba(71, 57, 71, 0.6)
  ```

### 2.2 adjust-hue()

- **包含函数：**

  - `adjust-hue($color, $degrees)`

- **返回值：**color

- **用法：**

  增大或减少颜色的色相。

  `$hue`必须是-360deg到360deg的一个无单位数字单位)（包括-360deg、360deg）。

  类似功能的函数color.adjust()，可以修改颜色的任意属性。

  因为`adjust-hue()`与adjust()是冗余的，所以它没有直接包含在新的模块系统中。您可以用`color.adjust($color, $hue: $amount)`，代替`adjust-hue($color, $amount)`。

  ```
  // Hue 222deg becomes 282deg.
  @debug adjust-hue(#6b717f, 60deg); // #796b7f
  
  // Hue 164deg becomes 104deg.
  @debug adjust-hue(#d2e1dd, -60deg); // #d6e1d2
  
  // Hue 210deg becomes 255deg.
  @debug adjust-hue(#036, 45); // #1a0066
  ```

### 2.3 color.alpha()/opacity()

- **包含函数：**

  - `color.alpha($color)`
  - `alpha($color)`
  - `opacity($color)`

- **返回值：**number

- **用法：**

  返回颜色alpha通道的值，是一个介于0-1之间的数字。

  作为一个特例，它支持Internet Explorer语法`alpha(opacity=20)`，返回一个不带引号的字符串。

  ```
  @debug color.alpha(#e1d7d2); // 1
  @debug color.opacity(rgb(210, 225, 221, 0.4)); // 0.4
  @debug alpha(opacity=20); // alpha(opacity=20)
  ```

### 2.4 color.blue()

- **包含函数：**

  - `color.blue($color)`
  - `blue($color)`

- **返回值：**number

- **用法：**

  返回蓝色通道的值，是一个介于0-255之间的数字。

  ```
  @debug color.blue(#e1d7d2); // 210
  @debug color.blue(white); // 255
  @debug color.blue(black); // 0
  ```

### 2.5 color.change()/change-color()

- **包含函数：**

  - `color.change($color,$red: null, $green: null, $blue: null,$hue: null, $saturation: null, $lightness: null,$alpha: null)`
  - `change-color(...)`

- **返回值：**color

- **用法：**

  改变`$color`的一个或多个属性，返回调整后的颜色。

  不能同时设置RGB（`$red,$green,$blue`）和HSL（`$hue,$saturation,$lightness`）属性的的值。

  所有可选参数必须是数字。`$red,$green,$blue`参数必须是-255到255之间的无单位数字（包括-255、255）。`$hue`参数必须包含单位`deg`或没有单位。`$saturation`和`$lightness`参数必须介于-100%和100%之间（包括-100%、100%），并且可能是无单位的。`$alpha`参数必须-1和1之间的无单位数字（包括-1，1）。

  ```
  @debug color.change(#6b717f, $red: 100); // #64717f
  @debug color.change(#d2e1dd, $red: 100, $blue: 50); // #64e132
  @debug color.change(#998099, $lightness: 30%, $alpha: 0.5); // rgba(85, 68, 85, 0.5)
  ```

### 2.6  color.complement()

- **包含函数：**

  - `color.complement($color)`
  - `complement($color)`

- **返回值：**color

- **用法：**

  返回颜色的RGB互补色

  与`color.adjust($color, $hue: 180deg)`是完全相同的。

### 2.7 darken()

- **包含函数：**

  - `darken($color, $amount)`

- **返回值：**color

- **用法：** 使颜色变深。

  `$amount`是0%-100%的数字（包括0%，100%），表示颜色HSL灰度值的减少量。

  ```
  // Lightness 92% becomes 72%(92-20=72).
  @debug darken(#b37399, 20%); // #7c4465
  
  // Lightness 85% becomes 45%(85-40=45).
  @debug darken(#f2ece4, 40%); // #b08b5a
  
  // Lightness 20% becomes 0%.
  @debug darken(#036, 30%); // black
  ```

  `darken()`相当于是灰度的减法，这通常不是我们想要的效果。要使颜色比以前暗一定百分比，可以使用color.scale()

### 2.8 desaturate()

- **包含函数：**

  - `darken($color, $amount)`

- **返回值：**color

- **用法：** 降低颜色饱和度的值。

  `$amount`是0%-100%的数字（包括0%，100%），表示颜色HSL饱和度的减少量。

  ```
  // Saturation 100% becomes 80%.
  @debug desaturate(#036, 20%); // #0a335c
  
  // Saturation 35% becomes 15%.
  @debug desaturate(#f2ece4, 20%); // #eeebe8
  
  // Saturation 20% becomes 0%.
  @debug desaturate(#d2e1dd, 30%); // #dadada
  ```

  `desaturate()`相当于是饱和度的减法，这通常不是我们想要的效果。要使颜色饱和度比之前降低一定百分比，可以使用color.scale()









---

#### [返回目录](./)