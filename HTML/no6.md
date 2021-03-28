## HTML+CSS学习笔记 CSS三大特性

---

### 1. 层叠性

一个标签被设置了多个重复的样式的时候，一个属性会覆盖另外一个属性。

原则：

- 样式冲突（同一元素、同优先级），遵循的原则是 **就近原则，会根据这些样式出现的先后顺序来决定，处于最后面的CSS样式将会覆盖前面的CSS样式。**。
- 样式不冲突，不会层叠



---

### 2. 继承性

子标签会**继承父标签的某些样式，如文本颜色和字号**。

可继承的属性比如有字体类属性（字体颜色、字体大小之类的）、文本类属性（行高之类的）、背景类属性（背景颜色之类的）。

不可继承的：边框、外边距、内边距、背景、定位、元素高度等**==与块级元素相关的==**属性都不具有继承性



---

### 3. 优先级

浏览器通过**优先级**来判断哪一些属性值与一个元素最为相关，从而在该元素上应用这些属性值。优先级是基于不同种类选择器组成的匹配规则。

优先级基本规则：

```
内联 > ID选择器 > 类选择器/属性选择器/伪类 > 标签选择器/伪元素 > 通配符选择器/继承 > 浏览器默认
```

优先级的规则计算如下：

优先级是由 `A` 、`B`、`C`、`D` 的值来决定的，其中它们的值计算规则如下：

1. 如果存在内联样式，那么 `A = 1`, 否则 `A = 0`;
2. `B` 的值等于 `ID选择器` 出现的次数;
3. `C` 的值等于 `类选择器` 和 `属性选择器` 和 `伪类` 出现的总次数;
4. `D` 的值等于 `标签选择器` 和 `伪元素` 出现的总次数 。

**比较规则是: 从A到D依次进行比较 ，较大者胜出，如果相等，则继续往后一位进行比较 。如果4位全部相等，则按定义顺序，后面定义的会覆盖前面的**。

关于CSS权重，我们需要一套计算公式来去计算，这个就是 CSS Specificity（特殊性）

| 标签选择器             | 计算权重公式 |
| ---------------------- | ------------ |
| 继承或者 *             | 0,0,0,0      |
| 每个元素（标签选择器） | 0,0,0,1      |
| 每个类，伪类           | 0,0,1,0      |
| 每个ID                 | 0,1,0,0      |
| 每个行内样式 style=""  | 1,0,0,0      |
| 每个!important  重要的 | ∞ 无穷大     |

- 值从左到右，左面的最大，一级大于一级，数位之间没有进制，级别之间不可超越。 
- 关于CSS权重，我们需要一套计算公式来去计算，这个就是 CSS Specificity（特殊性）



**特殊情况：**

使用了 `!important` 的，则会优先于其他所有定义。



---

#### [返回目录](./)
