## Vue全家桶学习笔记 VueCLI
---
### 1. 安装

```
npm install -g @vue/cli
```

---
### 2. 初始化和项目结构

```
vue create 项目页名称
```

项目结构如下：
```
  项目页名称
  |- /public （存放静态文件）
  |- /src
    |- /assets （小型静态文件，转换为base64）
    |- /components （vue组件）
    |- App.vue
    |- main.js
  |- .browserslistrc (浏览器适配）
  |- .gitignore
  |- babel.config.js （ES语法转换）
  |- postcss.config.js （css相关转换）
  |- package.json
  |- package-lock.json
  |- README.md
```

---
### 3. 配置

1. 通过ui界面

    ```
    vue ui
    ```
2. 添加项目配置  
    在项目目录中创建`vue.config.js`，导出对象中包含`configureWebpack`属性：

    ```
    // vue.config.js
    module.exports = {
        configureWebpack: {
            plugins: [
            new MyAwesomeWebpackPlugin()
            ]
        }
    }
    ```


---

#### [返回目录](./)
