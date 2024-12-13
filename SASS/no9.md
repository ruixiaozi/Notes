## SASS/SCSS学习笔记 sass:list 列表模块

---

## 1. sass:list 列表模块

在Sass中，每个映射可看做是一个列表，映射中的每个键/值可视为的列表中的一个元素。例如，`(1: 2, 3: 4)`等同于`(1 2, 3 4)`。因此，所有列表函数也适用于映射!

单个值也算作列表。`1px`可以看做是包含值`1px`的列表，即`[1px]`

### 1.1 list.append() 末尾加上

- **包含函数：**

  - `list.append($list, $val, $separator: auto)`
  - `append($list, $val, $separator: auto)`

- **返回值：**list

- **用法：**

  在`$list`的副本末尾加上`$val`，返回这个副本。

  `$separator`表示列表分隔符，值只能是`comma,space,auto`，comma表示分号，space表示空格，auto为默认值，不允许使用其他值。`$separator = auto`时，返回的列表将使用与`$list`相同的分隔符（如果`$list`没有分隔符，则使用空格）。

  ```
  @debug list.append(10px 20px, 30px); // 10px 20px 30px
  @debug list.append((blue, red), green); // blue, red, green
  @debug list.append(10px 20px, 30px 40px); // 10px 20px (30px 40px)
  @debug list.append(10px, 20px, $separator: comma); // 10px, 20px
  @debug list.append((blue, red), green, $separator: space); // blue red green
  ```

### 1.2 list.index() 返回索引值

- **包含函数：**

  - `list.index($list, $value)`
  - `index($list, $value)`

- **返回值：**number| null

- **用法：**

  返回`$value`在`$list`中的索引值。

  如果没有找到，则返回null。如果`$list`中有多个`$value`，则返回第一次出现的索引。

  ```
  @debug list.index(1px solid red, 1px); // 1
  @debug list.index(1px solid red, solid); // 2
  @debug list.index(1px solid red, dashed); // null
  ```

### 1.3 list.is-bracketed() 判断是否有方括号

- **包含函数：**

  - `list.is-bracketed($list)`
  - `is-bracketed($list)`

- **返回值：**boolean

- **用法：**

  判断`$list`中是否有方括号。

  ```
  @debug list.is-bracketed(1px 2px 3px); // false
  @debug list.is-bracketed([1px, 2px, 3px]); // true
  ```

### 1.4  list.join() 链接列表

- **包含函数：**

  - `list.join($list1, $list2, $separator: auto, $bracketed: auto)`
  - `join($list1, $list2, $separator: auto, $bracketed: auto)`

- **返回值：**list

- **用法：**

  返回一个新列表，其中包含`$list1`和`$list2`中所有的元素。

  `$separator`表示返回新列表的分隔符，值只能是`comma,space,auto`，comma表示分号，space表示空格，auto为默认值，不允许使用其他值。`$separator = auto`时，返回的新列表使用与`$list1`相同的分隔符；否则使用`$list2`；如果`$list1,$list2`都没有分隔符，则使用空格。

  `$bracketed`用于控制返回的新列表是否有方括号，值只能是`true,false,auto`，true表示有方括号，false表示没有，auto为默认值。`$separator = auto`时，返回的新列表的方括号结果与`$list1`一致

  ```
  @debug list.join(10px 20px, 30px 40px); // 10px 20px 30px 40px
  @debug list.join((blue, red), (#abc, #def)); // blue, red, #abc, #def
  @debug list.join(10px, 20px); // 10px 20px
  @debug list.join(10px, 20px, $separator: comma); // 10px, 20px
  @debug list.join((blue, red), (#abc, #def), $separator: space); // blue red #abc #def
  @debug list.join([10px], 20px); // [10px 20px]
  @debug list.join(10px, 20px, $bracketed: true); // [10px 20px]
  ```

### 1.5 list.length() 返回长度

- **包含函数：**

  - `list.length($list)`
  - `length($list)`

- **返回值：**number

- **用法：**

  返回`$list`的长度。也可以返回映射的键值对个数。

### 1.6  list.separator() 返回分隔符

- **包含函数：**

  - `list.separator($list)`
  - `list-separator($list)`

- **返回值：**unquoted string

- **用法：**

  返回`$list`的分隔符，值为`space,comma`。如果`$list`没有分隔符，则返回`sapce`。

  ```
  @debug list.separator(1px 2px 3px); // space
  @debug list.separator(1px, 2px, 3px); // comma
  @debug list.separator('Helvetica'); // space
  @debug list.separator(()); // space
  ```

### 1.7 list.nth() 返回第n个元素

- **包含函数：**

  - `list.nth($list, $n)`
  - `nth($list, $n)`

- **返回值：** *

- **用法：**

  返回在`$list`第`$n`个元素，从1开始计数。如果`$n`是负数，则从`$list`末尾开始计数。如果找不到，则抛错。

### 1.8 list.set-nth() 替换第n个元素

- **包含函数：**

  - `list.set-nth($list, $n, $value)`
  - `set-nth($list, $n, $value)`

- **返回值：** list

- **用法：**

  返回`$list`的副本，将副本中第`$n`个值替换为`$value`。如果`$n`是负数，则从`$list`末尾开始计数。如果找不到，则抛错。

  ```
  @debug list.set-nth(10px 20px 30px, 1, 2em); // 2em 20px 30px
  @debug list.set-nth(10px 20px 30px, -1, 8em); // 10px, 20px, 8em
  @debug list.set-nth((Helvetica, Arial, sans-serif), 3, Roboto); // Helvetica, Arial, Roboto
  ```

### 1.9 list.zip() 合并为子列表

- **包含函数：**

  - `list.zip($lists...)`
  - `zip($lists...)`

- **返回值：** list

- **用法：**

  将`$lists`中的每个列表合并为子列表的单个列表。

  返回列表中的每个元素包含`$list`中该位置的所有元素。返回的列表与`$lists`中最短的列表一样长。

  返回的列表用逗号分隔，子列表用空格分隔。

  ```
  @debug list.zip(10px 50px 100px, short mid long); // 10px short, 50px mid, 100px long
  @debug list.zip(10px 50px 100px, short mid); // 10px short, 50px mid
  ```

  





---

#### [返回目录](./)