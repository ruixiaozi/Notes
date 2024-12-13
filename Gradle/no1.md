## Gradle学习笔记 开始使用
---
### 1. 安装配置

&emsp;&emsp;下载地址：[https://gradle.org/releases/](https://gradle.org/releases/)，选择版本下载，配置环境变量：
```
GRADLE_USER_HOME=/{gradle目录所在路径}/gradle-6.1.1
PATH=$PATH:$GRADLE_USER_HOME/bin
export GRADLE_USER_HOME
export PATH
```
&emsp;&emsp;输入命令`gradle -v`可显示以下内容(其中版本号可能不同)：
```
------------------------------------------------------------
Gradle 6.1.1
------------------------------------------------------------

Build time:   2020-01-24 22:30:24 UTC
Revision:     a8c3750babb99d1894378073499d6716a1a1fa5d

Kotlin:       1.3.61
Groovy:       2.5.8
Ant:          Apache Ant(TM) version 1.10.7 compiled on September 1 2019
JVM:          1.8.0_181 (Oracle Corporation 25.181-b13)
OS:           Mac OS X 10.14.6 x86_64

```
---
### 2. 创建Gradle项目

&emsp;&emsp;在任一目录下运行命令`gradle init --type {type}`就可以初始化一个项目，其中`{type}`可为以下值：

| type | 说明 | 
| :-----| :---- | 
| pom | 将现有的Apache Maven构建转换为Gradle | 
| basic | 一个基本的，空的，Gradle构建 | 
| java-application | Java实现的命令行应用程序 | 
| java-gradle-plugin | Java实现的Gradle插件 | 
| java-library | Java库 | 
| kotlin-application | 在Kotlin / JVM中实现的命令行应用程序 | 
| kotlin-gradle-plugin | 在Kotlin / JVM中实现的Gradle插件 | 
| kotlin-library | Kotlin / JVM库 | 
| groovy-application | Groovy中实现的命令行应用程序 | 
| groovy-gradle-plugin | Groovy中实现的Gradle插件 | 
| groovy-library | 	Groovy库 | 
| scala-library | 一个Scala库 | 
| cpp-application | 用C ++实现的命令行应用程序 | 
| cpp-library | 一个C ++库 | 


---
### 3. 执行任务

&emsp;&emsp;输入命令`gradle {taskname}`执行对应的任务。其中`{taskname}`可使用缩写驼峰方式，但是必须保证缩写的驼峰名称唯一对应一个任务。如任务`taskFirst`可以缩写成`tF`。

---

#### [返回目录](./)