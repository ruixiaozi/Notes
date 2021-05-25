## Chrome插件学习笔记 manifest.json

---

### 1. 格式

```json
{
  // 必须的字段
  "name": "My Extension",
  "version": "versionString",
  "manifest_version": 2,
  // 建议提供的字段
  "description": "A plain text description",
  "icons": { ... },
  "default_locale": "en",
  // 多选一，或者都不提供
  "browser_action": {...},
  "page_action": {...},
  "theme": {...},
  "app": {...},
  // 根据需要提供
  "background": {...},
  "chrome_url_overrides": {...},
  "content_scripts": [...],
  "content_security_policy": "policyString",
  "file_browser_handlers": [...],
  "homepage_url": "http://path/to/homepage",
  "incognito": "spanning" or "split",
  "intents": {...}
  "key": "publicKey",
  "minimum_chrome_version": "versionString",
  "nacl_modules": [...],
  "offline_enabled": true,
  "omnibox": { "keyword": "aString" },
  "options_page": "aFile.html",
  "permissions": [...],
  "plugins": [...],
  "requirements": {...},
  "update_url": "http://path/to/updateInfo.xml",
  "web_accessible_resources": [...]
}  
```

### app

可安装的webapp，包括打包过的app，需要这个字段来指定app需要使用的url。最重要的是app的启动页面------当用户在点击app的图标后，浏览器将导航到的地方。

### default_locale

指定这个扩展保的缺省字符串的子目录：_lcoales。如果扩展有_locales目录，这个字段是必须的。如果没有_locales目录，这个字段是必须不存在的。

### description

描述扩种的一段字符串（不能是html或者其他格式，不能超过132个字符）。这个描述必须对浏览器扩展的管理界面和[Chrome Web Store](https://chrome.google.com/webstore)都合适。你可以指定本地相关的字符串

### homepage_url

这个扩展的主页 url。扩展的管理界面里面将有一个链接指向这个url。[如果你将扩展放在自己的网站上](http://chrome.cenchy.com/hosting.html)，这个url就很有用了。如果你通过了[Extensions Gallery](https://chrome.google.com/extensions)和[Chrome Web Store](https://chrome.google.com/webstore)来分发扩展，主页 缺省就是扩展的页面。

### icons

一个或者多个图标来表示扩展，app，和皮肤。你通常可以提供一个128x128的图标，这个图标将在webstore安装时候使用。扩展需要一个48x48的图标，扩展管理页面需要这个图标。同时，你还可以提供给一个16x16的图标作为扩页面的fa网页图标 。这个16x16的图标，还将显示在实验性的扩展[infobar](http://code.google.com/chrome/extensions/experimental.infobars.html)特性上。

图标要求是png格式，因为png格式是对透明支持最好的。你也可以用其他webkit支持的格式，如BMP,GIF,ICON和JPEG。下面有个例子：

```
"icons": 
  { 
    "16": "icon16.png",             
    "48": "icon48.png",            
    "128": "icon128.png" 
  },  
```

### incognito

可选值："spanning"和"split"，指定当扩展在允许隐身模式下运行时如何响应。

扩展的缺省值是Spanning，这意味着扩展将在一个共享的进程里面运行。隐身标签页的事件和消息都会发送到这个共享进程，来源通过incognito标志来区分。

可安装的webapp的缺省值是split，这个意思是隐身模式下的webapp都将运行在他们自己的隐身进程中。如果app或扩展有背景页面，也将运行在隐身进程中。隐身进程和普通进程一样，只是cookie保存在内存中而已。每个进程只可看到和自己相关的事件和消息（比如，隐身进程只能看到隐身标签也更新）。这些进程之间不能互相通信。

根据经验，如果你的扩展或app需要在隐身浏览器里面开一个标签页，使用split；如果你的扩展或app需要登记录到远程服务器或者本地永久配置，用spanning。

### intents

一个字典，用于描述扩展或app所提供的全部intent handler。字典里的每个键指定了一个action verb。下面这个例子为"http://webintents.org/share"这个action verb指定了2个的intent handler。

```
{
    "name": "test",
    "version": "1",
    "intents": {
      "http://webintents.org/share": [
        { 
          "type": ["text/uri-list"],
          "href": "/services/sharelink.html",
          "title" : "Sample Link Sharing Intent",
          "disposition" : "inline"
        },
        {
          "type": ["image/*"],
          "href": "/services/shareimage.html",
          "title" : "Sample Image Sharing Intent",
          "disposition" : "window"
        }
      ]
    }  
}
  
```

“type”指定handler所支持的一组MIME。

“href”指定了处理intent的页面URL。对于托管的apps，这个URL必须在属于允许URL集。对于扩展，这个页面必须是扩展自带的，其URL是相对扩展根目录的相对路径。

当用户触发handler对应的动作时，“title”会显示在intent选择界面中。

“disposition”可以是“inline”或“window”。当intent被触发时，“window”表示将在一个新标签中打开，而“inline”表示直接在当前标签页打开。

### key

开发时为扩展指定的唯一标识值。

注意：通常您并不需要直接使用这个值，而是在您的代码中使用相对路径或者[chrome.extension.getURL()](http://chrome.cenchy.com/extension.html#method-getURL)得到的绝对路径。

这个值并不是开发时显式指定的，而是Chrome在安装`.crx`时辅助生成的。（开发时可以通过[谷歌浏览器应用开放平台](http://chrome.cenchy.com/open/index.html)或[上传扩展](https://chrome.google.com/webstore/developer/dashboard)，也可以自行[打包](http://chrome.cenchy.com/packaging.html)生成`.crx`文件。） 安装完`.crx`，在Chrome的[用户数据目录](http://www.chromium.org/user-experience/user-data-directory)下的`Default/Extensions/*<extensionId>*/*<versionString>*/manifest.json`文件中，您可以看到这个扩展的key。

### minimum_chrome_version

扩展，app或皮肤需要的chrome的最小版本，如果有这个需要的话。这个字符串的格式和 [version](http://chrome.cenchy.com/manifest.html#version)字段一样。

### name

用来标识扩展的简短纯文本。这个文字将出现在安装对话框，扩展管理界面，和[store](https://chrome.google.com/webstore)里面。你可以指定一个本地相关的字符串为这个字段，具体参考：[Internationalization](http://chrome.cenchy.com/i18n.html)。

### nacl_modules

一个或多个从MIME到处理这个MIME的本地客户端模块之间的映射。 例如，下段代码中加粗部分将一个本地客户端模块注册为处理OpenOffice电子表格MIME。

```
{
    "name": "Native Client OpenOffice Spreadsheet Viewer",
    "version": "0.1",
    "description": "Open OpenOffice spreadsheets, right in your browser.",
    "nacl_modules": [{
      "path": "OpenOfficeViewer.nmf",
      "mime_type": "application/vnd.oasis.opendocument.spreadsheet"
    }]
  }
  
```

"path" 指定一个NaCl 的manifest（就像扩展有各自的manifest一样，NaCl 也有自己的manifest文件，不同的是NaCl 的以`.nmf`作为后缀）。 这个路径是相对于扩展根目录的。 更多NaCl 信息和`.nmf` 文件格式请参考[NaCl 技术概述](http://code.google.com/chrome/nativeclient/docs/technical_overview.html)。

一个MIME只能与一个“.nmf”文件关联，但一个“.nmf”文件可处理多个MIME。下面例子的扩展有2个“.nmf”文件，但处理了3个MIME。

```
{
    "name": "Spreadsheet Viewer",
    "version": "0.1",
    "description": "Open OpenOffice and Excel spreadsheets, right in your browser.",
    "nacl_modules": [{
      "path": "OpenOfficeViewer.nmf",
      "mime_type": "application/vnd.oasis.opendocument.spreadsheet"
    },
    {
      "path": "OpenOfficeViewer.nmf",
      "mime_type": "application/vnd.oasis.opendocument.spreadsheet-template"
    },
    {
      "path": "ExcelViewer.nmf",
      "mime_type": "application/excel"
    }]
  }
  
```

**注意：**扩展不在manifest中指定“nacl_modules”也可以使用NaCl。仅在扩展希望自己的NaCl 被浏览器知道并用于显示关联的MIME内容时才需要指定。

### offline_enabled

指定本扩展或app是否支持脱机运行。当Chrome检测到处于脱机状态，此项设置为“是”的app将会在新标签页中高亮显示。



### permissions

扩展或app将使用的一组权限。每个权限是一列已知字符串列表中的一个，如geolocatioin或者一个匹配模式，来指定可以访问的一个或者多个主机。权限可以帮助限定危险，如果你的扩展或者app被攻击。一些权限在安装之前，会告知用户，具体参考：[权限提醒](http://chrome.cenchy.com/permission_warnings.html)。

如果一个扩展api需要你的声明一个权限在manifest文件，一般的，api的文档将告诉怎么做。例如，[Tabs](http://chrome.cenchy.com/tabs.html)页面告诉你这么声明一个tabs权限。

这是一个扩展的manifest文件的权限设置的一部分。

```
"permissions": 
[    
	"tabs",    
	"bookmarks",    
	"http://www.blogger.com/",    
	"http://*.google.com/",    
	"unlimitedStorage"  
],  
```

### requirements

指定本app或扩展所需的特殊技术功能。安装扩展时，扩展商店根据这个清单，必要时劝阻用户在不支持所需功能的电脑上安装这些扩展。

目前只支持指定“3D”，也就是GPU加速。您可以指定所需的3D相关功能，比如：

```
"requirements": {
    "3D": {
      "features": ["css3d", "webgl"]
    }
  }
  
```

"css3d"的详细信息请参考[CSS 3D Transforms 规范](http://www.w3.org/TR/css3-3d-transforms/)，"webgl"请参考[WebGL API](http://www.khronos.org/webgl/)。 Chrome 3D功能的支持情况请参考[WebGL and 3D graphics](http://www.google.com/support/chrome/bin/answer.py?answer=1220892)。 未来可能会增加更多技术功能的检测指定。

### version

扩展的版本用一个到4个数字来表示，中间用点隔开。这些数字有些规则：必须在0到65535之间，非零数字不能0开头，比如，99999和032是不合法的。

下面是一些版本字符串例子：

- "version": "1"
- "version": "1.0"
- "version": "2.10.2"
- "version": "3.1.2.4567"

自动升级系统将比较版本来确定一个已经安装的扩展是否需要升级。如果一个发布的扩展有一个更新的版本字符串，比一个安装的扩展，这个扩展将自动升级。

版本字符串从比较从左边开始。如果这些数字相等，这个数字的右边的数字将被比较，这样持续下去。比如：1.2.0就比1.1.9.9999更新。

缺少的数字将用0来代替。例子，1.1.9.9999就比1.1.更新。

具体信息请参考[Autoupdating](http://chrome.cenchy.com/autoupdate.html)。

### manifest_version

用整数表示manifest文件自身格式的版本号。从Chrome 18开始，开发者应该（不是必须，但是2012年底左右就必须了）指定版本号为2（没有引号），如下所示：

```
"manifest_version": 2
```

manifest版本1从Chrome 18才开始逐步被弃用，版本2目前并不是必须的，但预计我们将在2012年底强制只支持版本2。还没有准备好支持manifest版本2的扩展、应用和主题，可以明确指定版本1，或者索性不提供本字段。

版本1到2之间的变化细节可以参考[`manifest_version`文档。](http://code.google.com/chrome/extensions/manifestVersion.html)

在Chrome17（极速5.2）或之前的指定版本2将会发生不可预料的事情。

### web_accessible_resources

一组字符串，指定本扩展在注入的目标页面上所需使用的资源的路径（相对于扩展的安装根目录）。例如，扩展在example.com上注入脚本以构建制界面，将其间所需的资源（图片、图标、样式、脚本等）加入白名单，如下所示：

```
{
    ...
    "web_accessible_resources": [
      "images/my-awesome-image1.png",
      "images/my-amazing-icon1.png",
      "style/double-rainbow.css",
      "script/double-rainbow.js"
    ],
    ...
  }
```

这些资源的访问URL是 `chrome-extension://[PACKAGE ID]/[PATH]`，可通过调用`chrome.extension.getURL`构造出。 这些白名单资源是通过[CORS](http://www.w3.org/TR/cors/)头提供的，因此可被类似XHR这样的机制使用。

扩展的content scripts自身不需要加入白名单

#### 资源的缺省可用性

manifest_version为2的扩展，缺省将不能使用除web_accessible_resources中指定外的任何其它任何扩展包内资源。

manifest_version为1的扩展，缺省仍可访问任何扩展包内资源。*但是*，一旦指定web_accessible_resources，将也只能访问其中指定的资源。

---

#### [返回目录](./)