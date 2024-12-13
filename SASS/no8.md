## SASS/SCSS学习笔记 sass:color 颜色模块

---

## 1. 颜色模块（sass:color）

### 1.1 color.adjust()/adjust-color()，修改某个颜色值

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

### 1.2 adjust-hue()增加、减少颜色的色相

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

### 1.3 color.alpha()/opacity()获取透明度

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

### 1.4 color.blue()返回蓝色通道

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

### 1.5 color.change()/change-color()修改某个颜色值

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

### 1.6  color.complement()获取互补色

- **包含函数：**

  - `color.complement($color)`
  - `complement($color)`

- **返回值：**color

- **用法：**

  返回颜色的RGB互补色

  与`color.adjust($color, $hue: 180deg)`是完全相同的。

### 1.7 darken()灰度值减少

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

### 1.8 desaturate() 饱和度减少

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

### 1.9 color.grayscale() 返回同亮度灰色

- **包含函数：**

  - `color.grayscale($color)`
  - `grayscale($color)`

- **返回值：**color

- **用法：**

  返回与`$color`亮度相同的灰色。

  这与color.change($color, $saturation: 0%)是等效的。

### 1.10 color.green() 返回绿色通道

- **包含函数：**

  - `color.green($color)`
  - `green($color)`

- **返回值：**number

- **用法：**

  返回绿色通道的值，是一个介于0-255之间的数字。

### 1.11 color.hue() 返回色相值

- **包含函数：**

  - `color.hue($color)`
  - `hue($color)`

- **返回值：**number

- **用法：**

  返回`$color`的色相的值，是一个介于`0deg - 255deg`之间的值。

  ```
  @debug color.hue(#e1d7d2); // 20deg
  @debug color.hue(#f2ece4); // 34.2857142857deg
  @debug color.hue(#dadbdf); // 228deg
  ```

### 1.12 color.ie-hex-str() Internet Explorer所期望的`#AARRGGBB`格式

- **包含函数：**

  - `color.ie-hex-str($color)`
  - `ie-hex-str($color)`

- **返回值：**unquoted string

- **用法：**

  返回一个不带引号的字符串，该字符串表示Internet Explorer的-ms-filter属性所期望的`#AARRGGBB`格式的`$color`。

### 1.13 color.invert() 相反或者互补的颜色

- **包含函数：**

  - `color.invert($color, $weight: 100%)`
  - `invert($color, $weight: 100%)`

- **返回值：**color

- **用法：**

  返回与`$color`相反或者互补的颜色。

  `$weight`必须是0%到100%的数字（包括0%、100%）。值越大越接近负数；值越低越接近`$color`。`$weight = 50%`时，`$color = #808080`。

  ```
  @debug color.invert(#b37399); // #4c8c66
  @debug color.invert(black); // white
  @debug color.invert(#550e0c, 20%); // #663b3a
  ```

### 1.14 lighten() 使颜色变浅，亮度减少

- **包含函数：**

  - `lighten($color, $amount)`

- **返回值：**color

- **用法：** 使颜色变浅。

  `$amount`是0%-100%的数字（包括0%，100%），表示颜色HSL亮度的减少量。

  `lighten()`相当于是亮度的减法，这通常不是我们想要的效果。要使颜色比以前浅一定百分比，可以使用color.scale()

  ```
  // #036 has lightness 20%, so when darken() subtracts 30% it just returns black.
  @debug darken(#036, 30%); // black
  
  // scale() instead makes it 30% darker than it was originally.
  @debug color.scale(#036, $lightness: -30%); // #002447
  ```

### 1.15 color.lightness() 获取亮度值

- **包含函数：**

  - `color.lightness($color)`
  - `lightness($color)`

- **返回值：**number

- **用法：**

  返回`$color`的亮度值，是一个介于`0% - 100%`之间的值。

  ```
  @debug color.lightness(#e1d7d2); // 85.2941176471%
  @debug color.lightness(#f2ece4); // 92.1568627451%
  @debug color.lightness(#dadbdf); // 86.4705882353%
  ```

### 1.16 color.mix() 混合颜色

- **包含函数：**

  - `color.mix($color1, $color2, $weight: 50%)`
  - `mix($color1, $color2, $weight: 50%)`

- **返回值：**color

- **用法：**

  返回一个混合了`$color1`和`$color2`的颜色。

  `$weight`和每种颜色的相对不透明度都决定了每种颜色在结果中的比例。`$weight`必须是0%到100%之间的数字（包括0%，100%）。`$weight`值越大表示应该使用更多的`$color1`，`$weight`值越小表示应该使用更多的`$color2`。

  ```
  @debug color.mix(#036, #d2e1dd); // #698aa2
  @debug color.mix(#036, #d2e1dd, 75%); // #355f84
  @debug color.mix(#036, #d2e1dd, 25%); // #9eb6bf
  @debug color.mix(rgba(242, 236, 228, 0.5), #6b717f); // rgba(141, 144, 152, 0.75)
  ```

### 1.17 opacify() /fade-in()变得更不透明，透明度值增加

- **包含函数：**

  - `opacify($color, $amount)`
  - `fade-in($color, $amount)`

- **返回值：**color

- **用法：**

  使`$color`的变得更不透明。

  `$amount`须是0-1之间的数字（包含0、1），表示`$color`alpha通道的增加量。

  ```
  @debug opacify(rgba(#6b717f, 0.5), 0.2); // rgba(107, 113, 127, 0.7)
  @debug fade-in(rgba(#e1d7d2, 0.5), 0.4); // rgba(225, 215, 210, 0.9)
  @debug opacify(rgba(#036, 0.7), 0.3); // #036
  ```

  `opacify()`将alpha通道增加了一个固定的量，这通常不是期望的效果。要使颜色比以前更加不透明，可以使用scale()

### 1.18 color.red() 返回红色通道

- **包含函数：**

  - `color.red($color)`
  - `red($color)`

- **返回值：**number

- **用法：**

  返回`$color`红色通道的值，是一个介于0-255之间的数字。

### 1.19 saturate() 增加饱和度

- **包含函数：**

  - `saturate($color, $amount)`

- **返回值：**color

- **用法：**

  增加`$color`的饱和度。

  `$amount`须是0%-100%之间的数字（包含0%、100%），表示`$color`HSL饱和度的增加量 。

  saturate()将饱和度增加了一个固定的量，这通常不是期望的效果。要增加颜色的饱和度，可以使用scale()。

  ```
  // #0e4982 has saturation 80%, so when saturate() adds 30% it just becomes
  // fully saturated.
  @debug saturate(#0e4982, 30%); // #004990
  
  // scale() instead makes it 30% more saturated than it was originally.
  @debug color.scale(#0e4982, $saturation: 30%); // #0a4986
  ```

### 1.20 color.saturation() 获取饱和度

- **包含函数：**

  - `color.saturation($color)`
  - `saturation($color)`

- **返回值：**number

- **用法：**

  返回`$color`的饱和度，是一个介于`0% - 100%`之间的值。

  ```
  @debug color.saturation(#e1d7d2); // 20%
  @debug color.saturation(#f2ece4); // 30%
  @debug color.saturation(#dadbdf); // 7.2463768116%
  ```

### 1.21 color.scale()/scale-color() 缩放一个或多个属性

- **包含函数：**

  - `color.scale($color,$red: null, $green: null, $blue: null,$saturation: null, $lightness: null,$alpha: null)`
  - `scale-color(...)`

- **返回值：**color

- **用法：**

  缩放`$color`的一个或多个属性。

  每个关键字参数必须是一个介于-100%和100%之间的数字（包括-100%、100%）。这表示相应的属性应该从其原始位置移动到最大值（如果参数是正的）或最小值（如果参数是负的）的距离。这意味着，例如，`$lightness:50%`表示亮度值增加`(最大亮度-当前亮度)*50%`，而不使它们完全白色。

  不能同时调整RGB（`$red,$green,$blue`）和HSL（`$hue,$saturation,$lightness`）属性的的值。

  ```
  @debug color.scale(#6b717f, $red: 15%); // #81717f
  @debug color.scale(#d2e1dd, $lightness: -10%, $saturation: 10%); // #b3d4cb
  @debug color.scale(#998099, $alpha: -40%); // rgba(153, 128, 153, 0.6)
  ```

### 1.22 color.transparentize()/fade-out() 变得更透明

- **包含函数：**

  - `transparentize($color, $amount)`
  - `fade-out($color, $amount)`

- **返回值：**color

- **用法：**

  使`$color`变得更透明。

  `$amount`须是0-1之间的数字（包含0、1），表示`$color`alpha通道的减少量





---

#### [返回目录](./)