## Chrome插件学习笔记 browserAction浏览器按钮

---

### 1. 介绍

可以在 Google Chrome 浏览器主窗口中地址栏右侧的工具栏中添加图标。除了**图标**，浏览器按钮还可以有**工具提示**、**徽章**和**弹出内容**。

---

### 2. 清单配置


```
{
  "name": "我的扩展程序",
  ...
  "browser_action": {
    "default_icon": {                    // 可选
      "19": "images/icon19.png",           // 可选
      "38": "images/icon38.png"            // 可选
    },
    "default_title": "Google Mail",      // 可选，在工具提示中显示
    "default_popup": "popup.html"        // 可选
  },
  ...
}
```

如果您只提供 19px 或 38px 图标大小中的一个，扩展程序系统将会缩放您提供的图标，以适应用户显示器的像素密度，这有可能会丢失细节或使它看上去很模糊。注册默认图标的旧语法仍然支持：

```
{
  "name": "我的扩展程序",
  ...
  "browser_action": {
    ...
    "default_icon": "images/icon19.png"  // 可选
    // 等价于 "default_icon": { "19": "images/icon19.png" }
  },
  ...
}
```

---

### 3. 具体配置

#### 图标

浏览器按钮图标的宽度和高度最大可以为 19 dip（设备无关像素），更大的图标会被缩小。为了最佳结果，请使用 19 dip 大小的正方形图标。

您可以通过两种方式设置图标：使用静态图像或者使用 HTML5 canvas 元素。对于简单的应用来说，使用静态图像更方便，但是您可以使用 canvas 元素创建动态的用户界面，例如平滑的动画。

静态图像可以是 WebKit 能够显示的任何格式，包括 BMP、GIF、ICO、JPEG 或 PNG。对于未打包的扩展程序来说，图片必须是 PNG 格式。

要设置图标，请使用**清单文件**中 **browser_action** 部分的 **default_icon** 属性，或者调用 **setIcon** 方法。

要在屏幕像素密度（比值 `size_in_pixel / size_in_dip`）不为 1 的时候正确显示图标，图标可以定义为一组不同大小的图片。实际显示的图片将从这一组图标中选取，以便最佳匹配 19 dip 图标的像素大小。目前一组图标可以包含像素大小为 19 和 38 的图片。

#### 工具提示

要设置工具提示，使用**清单文件**中 **browser_action** 部分的 **default_title** 属性，或者调用**setTitle**方法。对于 **default_title** 属性，您可以指定区域相关的字符串。

浏览器按钮可以选择在图标上显示徽章，即一小段文字。徽章使得更新浏览器按钮更容易，来显示有关扩展程序状态的一点点信息。

因为徽章所拥有的空间有限，它不应超过四个字符。

分别调用**setBadgeText**和 **setBadgeBackgroundColor**设置徽章的内容和颜色。

#### 弹出内容

如果浏览器按钮有弹出内容，当用户单击图标时会出现弹出内容。弹出内容可以包含任何您需要的 HTML 内容，并且会自动调整大小以适应内容。

要向您的浏览器按钮添加弹出内容，请创建一个 HTML 文件存放弹出内容，并在**清单文件**中 **browser_action** 部分的 **default_popup** 属性指定该 HTML 文件或者调用 **setPopup**方法。

---

### 4. API

#### chrome.browserAction 参考

#### 类型

---

##### ColorArray

array of integer

##### ImageDataType

图片的像素数据，必须为 ImageData 对象（例如来自 `canvas` 元素）。



#### 方法

---

##### setTitle

```
chrome.browserAction.setTitle(object details)
```

设置浏览器按钮的标题，显示在工具提示中。

###### 参数

1. details ( object )
   属性
   + title ( string )
     当鼠标移到浏览器按钮上时应显示的字符串。
   + tabId ( optional integer )
     将更改限制在当某一特定标签页选中时应用，当该标签页关闭时，更改的内容自动恢复。



##### getTitle

```
chrome.browserAction.getTitle(object details, function callback)
```

获取浏览器按钮的标题。

###### 参数

1. details ( object )
   属性
   + tabId ( optional integer )
     指定要获取标题的标签页。如果没有指定标签页，则返回用于所有标签页的标题。

2. callback ( function )

   *callback* 参数应该指定一个如下形式的函数：

   ```
   function(string result) {...};
   ```



##### setIcon

```
chrome.browserAction.setIcon(object details, function callback)
```

设置浏览器按钮的图标。图标既可以指定为图片文件的路径，也可以指定来自 canvas 元素的像素数据，或者这两者中任意一个的词典。**path** 或 **imageData** 属性中有且只有一个必须指定。

###### 参数

1. details ( object )
   属性
   + imageData ( optional ImageDataType or object )
     ImageData 对象或一个词典（大小 -> ImageData），表示要设置的图标。如果图标以词典的形式指定，实际使用的图标取决于屏幕的像素密度。如果单位屏幕空间容纳的图片的像素数等于 scale，则会选择大小为 scale * 19的图片。目前只支持缩放比例 1 和 2。至少要指定一个图片。注意“details.imageData = foo”等价于“details.imageData = {'19': foo}”。
   + path ( optional string or object )
     图片的相对路径或一个词典（大小 -> 图片的相对路径），指向要设置的图标。如果图标以词典的形式指定，实际使用的图标取决于屏幕的像素密度。如果单位屏幕空间容纳的图片的像素数等于 scale，则会选择大小为 scale * 19的图片。目前只支持缩放比例 1 和 2。至少要指定一个图片。注意“details.path = foo”等价于“details.path = {'19': foo}”。
   + tabId ( optional integer )
     将更改限制在当某一特定标签页选中时应用，当该标签页关闭时，更改的内容自动恢复。

2. callback ( optional function )

   如果您指定了 *callback* 参数，它应该指定一个如下形式的函数：

   ```
   function() {...};
   ```




##### setPopup

```
chrome.browserAction.setPopup(object details)
```

设置当用户单击浏览器按钮时显示为弹出内容的 HTML 文档。

###### 参数

1. details ( object )
   属性
   + tabId ( optional integer )
     将更改限制在当某一特定标签页选中时应用，当该标签页关闭时，更改的内容自动恢复。
   + popup ( string )
     显示在弹出内容中的 HTML 文件，如果设置为空字符串（""）则不显示弹出内容。



##### getPopup

```
chrome.browserAction.getPopup(object details, function callback)
```

获取设置为浏览器按钮弹出内容的 HTML 文档。

###### 参数

1. details ( object )
   属性
   + tabId ( optional integer )
     指定要获取弹出内容的标签页。如果没有指定标签页，则返回用于所有标签页的弹出内容。

2. callback ( function )

   *callback* 参数应该指定一个如下形式的函数：

   ```
   function(string result) {...};
   ```

   

##### setBadgeText

```
chrome.browserAction.setBadgeText(object details)
```

设置浏览器按钮上的徽章，显示在图标上。

###### 参数

1. details ( object )
   属性
   + text ( string )
     可以传入任意数目的字符，但是只有大约四个字符能显示得下。
   + tabId ( optional integer )
     将更改限制在当某一特定标签页选中时应用，当该标签页关闭时，更改的内容自动恢复。



##### getBadgeText

```
chrome.browserAction.getBadgeText(object details, function callback)
```

获取浏览器按钮上的徽章，如果没有指定标签页，则返回用于所有标签页的徽章。

###### 参数

1. details ( object )
   属性
   + tabId ( optional integer )
     指定要获取徽章的标签页。如果没有指定标签页，则返回用于所有标签页的徽章。

2. callback ( function )

   *callback* 参数应该指定一个如下形式的函数：

   ```
   function(string result) {...};
   ```

   

##### setBadgeBackgroundColor

```
chrome.browserAction.setBadgeBackgroundColor(object details)
```

设置徽章的背景颜色。

###### 参数

1. details ( object )
   属性
   + color ( string or ColorArray )
     含有四个在 [0,255] 范围内的整数的数组，组成徽章的 RGBA 颜色。例如，不透明的红色是 [255, 0, 0, 255]。也可以为 CSS 形式的字符串，例如不透明的红色为 #FF0000 或 #F00。
   + tabId ( optional integer )
     将更改限制在当某一特定标签页选中时应用，当该标签页关闭时，更改的内容自动恢复。



##### getBadgeBackgroundColor

```
chrome.browserAction.getBadgeBackgroundColor(object details, function callback)
```

获取浏览器按钮上的徽章，如果没有指定标签页，则返回用于所有标签页的徽章。

###### 参数 

1. details ( object )
   属性
   + tabId ( optional integer )
     指定要获取徽章背景颜色的标签页。如果没有指定标签页，则返回用于所有标签页的徽章背景颜色。

2. callback ( function )

   *callback* 参数应该指定一个如下形式的函数：

   ```
   function(ColorArray result) {...};
   ```

   

##### enable

```
chrome.browserAction.enable(integer tabId)
```

为某一标签页启用浏览器按钮。默认情况下，浏览器按钮是启用的。

###### 参数

1. tabId ( optional integer )
   您希望修改浏览器按钮的标签页标识符。



##### disable

```
chrome.browserAction.disable(integer tabId)
```

为某一标签页禁用浏览器按钮。

###### 参数

1. tabId ( optional integer )
   您希望修改浏览器按钮的标签页标识符。



#### 事件

---

##### onClicked

浏览器按钮的图标单击时产生，如果浏览器按钮有弹出内容则不会触发该事件。

+ addListener

  ```
  chrome.browserAction.onClicked.addListener(function callback)
  ```

  ###### 参数

  1. callback ( function )

     *callback* 参数应该指定一个如下形式的函数：

     ```
     function(tabs.Tab tab) {...};
     ```

     

  

---

#### [返回目录](./)