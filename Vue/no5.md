## Vue全家桶学习笔记 Webpack
---
### 1. 安装


```
npm install webpack@版本号 -g
或者
npm install webpack@版本号 --save-dev
```

---
### 2. 项目结构

```
  webpack-demo
  |- package.json
+ |- index.html
+ |- /src
+   |- index.js
```

---
### 3. 命令

1. 打包js（自动处理js依赖关系和模块化关系）

    + 简单打包 
        ```
        webpack src/index.js dist/bundle.js
        ```
    + 使用配置文件配置打包目标
        1. 创建`webpack.config.js`文件：
            ```
            const path = require('path')

            module.exports = {
                entry: './src/index.js',
                output: {
                    path: path.resolve(__dirname,'dist'),
                    filename: 'bundle.js'
                }
            }
            ```
        2. 打包命令 
            ```
            webpack
            ```

2. 运行服务

    ```
    webpack-dev-server --参数
    ```

    参数列表：
    + contentBase：为哪一个文件夹提供本地服务，默认是根文件夹，我们这里要填写./dist
    + port：端口号
    + inline：页面实时刷新
    + historyApiFallback：在SPA页面中，依赖HTML5的history模式


---
### 4. 配置 

1. 配置npm脚本  

    在`package.json`中的`scripts`对象下，创建不同的运行脚本，该脚本会优先使用本项目npm安装的组件：
    ```
    {
        ...
        "srcipts": {
            "build": "webpack"
        }
        ...
    }
    ```

---
### 5. loader

用来解析专门的文件。

1. 使用方法
    + 在webpack或者对应loader官方查找安装方法和配置方法
    + 通过npm安装对应的loader
    + 在`webpack.config.js`中的`modules`下配置。

2. 常用loader 

    + css-loader
    + style-loader
    + less-loader
    + url-loader
    + file-loader
    + vue-loader

---
### 6. babel

用于适配浏览器，转换js语法

---
### 7. 插件

1. 使用插件
    + 使用npm安装插件
    + 在`webpack.config.js`中的plugins中配置

2. 常用插件
    + 版权注释插件：BannerPlugin（自带插件）
    + 打包HTML插件：HtmlWebpackPlugin
    + js压缩插件：uglifyjs-webpack-plugin

---

#### [返回目录](./)
