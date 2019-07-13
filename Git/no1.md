## Git学习笔记 配置Git与创建仓库
---
### 1.配置Git的工具

&emsp;&emsp;Git 提供了一个叫做 `git config` 的工具，用来配置或读取相应的工作环境变量。
> + /etc/gitconfig 文件：系统中对所有用户都普遍适用的配置。若使用 git config 时用 --system 选项
> + ~/.gitconfig 文件：用户目录下的配置文件只适用于该用户。若使用 git config 时用 --global 选项，读写的就是这个文件。
> + 当前项目的 Git 目录中的配置文件（也就是工作目录中的 .git/config 文件）：这里的配置仅仅针对当前项目有效。每一个级别的配置都会覆盖上层的相同配置，所以 .git/config 里的配置会覆盖 /etc/gitconfig 中的同名变量。

>在 Windows 系统上，Git 会找寻用户主目录下的 .gitconfig 文件。主目录即 $HOME 变量指定的目录，一般都是 C:\Documents and Settings\$USER。此外，Git 还会尝试找寻 /etc/gitconfig 文件，只不过看当初 Git 装在什么目录，就以此作为根目录来定位。

---
### 2.配置用户信息

&emsp;&emsp;每次 Git 提交时都会引用用户信息，说明是谁提交了更新，所以会随更新内容一起被永久纳入历史记录。命令格式如下：
```
git config --global user.name "John Doe"
git config --global user.email johndoe@example.com
```

---
### 3.查看配置信息

&emsp;&emsp;查看目前git的配置信息，可以使用如下命令：
```
git config --list
```
&emsp;&emsp;也可以直接查阅某个环境变量的设定，只要把特定的名字跟在后面即可：
```
git config user.name
```

---
### 4.从本地创建

&emsp;&emsp;在当前工作目录，执行如下命令：
```
git init
```
&emsp;&emsp;初始化后，在当前目录下会出现一个.git的目录，git的数据都在这个目录下。

---
### 5.从远程仓库创建
&emsp;&emsp;可以使用如下代码命令，克隆一个远程仓库：
```
git clone [url] [dirname]
```
&emsp;&emsp;其中 url 是仓库的地址。dirname可以省略，代表自己定义要新建的项目目录名称。

---

#### [返回目录](./)
