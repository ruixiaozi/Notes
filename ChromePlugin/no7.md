## Chrome插件学习笔记 替代页面

---

### 1. 介绍

替代页面是一种使用来自您的扩展程序的 HTML 文件替换 Google Chrome 默认提供页面的方式。除了 HTML，替代页面通常还包含 CSS 和 JavaScript 代码。

扩展程序可以替换以下任一页面：

- **书签管理器：**当用户选择 Chrome 菜单中（或 Mac 系统上的书签菜单中）的书签管理器菜单项时出现的页面。您也可以输入 URL **chrome://bookmarks** 进入该页面。
- **历史记录：**当用户选择 Chrome 菜单中的历史记录（或者 Mac 系统上历史记录菜单中的显示所有历史记录）时出现的页面。您也可以输入 URL **chrome://history** 进入该页面。
- **“打开新的标签页”页面：**当用户创建新标签页或新窗口时出现的页面。您也可以输入 URL **chrome://newtab** 进入该页面。

**注意：**一个扩展程序**只能替换一个页面**。例如，一个扩展程序不能既替换书签管理页面，又替换历史记录页面。

隐身窗口是特殊对待的，“打开新的标签页”页面不能在隐身窗口中替换。只要清单文件中的 **incognito** 属性设置为 "spanning"（也是默认值），其他替代页面将在隐身窗口中工作。有关您应该如何对待隐身窗口的更多细节，请参见概述中的**保存数据和隐身模式**。

---

### 2. 清单配置

```
{
  "name": "我的扩展程序",
  ...

  "chrome_url_overrides" : {
    "pageToOverride": "myPage.html"
  },
  ...
}
```

将 `pageToOverride` 替换为以下值之一：

- `bookmarks`
- `history`
- `newtab`





---

#### [返回目录](./)