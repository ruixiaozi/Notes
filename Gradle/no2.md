## Gradle学习笔记 构建脚本
---
### 1. 构建块

&emsp;&emsp;Gradle构建脚本分为3个基本构建块：project、task和property。每个脚本至少包含一个project，包含一个或多个task。

1. 项目 Project

    项目代表一个正在构建的组件或者最终交付的产品。`Project`和`build.gradle`文件之间存在一对一的关系，自动实例化`org.gradle.api.Project`，使用隐式变量`project`访问。
    
    一个project可以创建新的task，添加依赖关系和配置，并应用插件和其他的构建脚本。**当访问属性和方法时，不需要使用project变量，隐式为该对象的属性和方法**
2. 任务 Task



---

#### [返回目录](./)