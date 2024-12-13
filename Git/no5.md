## Git学习笔记 使用远程仓库
---
### 1.查看远程仓库

&emsp;&emsp;可以使用如下命令参看当前仓库的远程仓库列表：
```
git remote -v
```

---
### 2.添加远程仓库

&emsp;&emsp;使用如下命令可以添加一个远程仓库：
```
git remote add [shortname] [url]
```

---
### 3.从远程仓库抓取数据

&emsp;&emsp;使用如下命令可以从远程仓库抓取本地没有的数据到本地：
```
git fetch [remote-name]
```
&emsp;&emsp;fetch 命令只是将远端的数据拉到本地仓库，并不自动合并到当前工作分支，只有当你确实准备好了，才能手工合并。如果设置了某个分支用于跟踪某个远端仓库的分支，可以使用 `git pull `命令自动抓取数据下来，然后将远端分支自动合并到本地仓库中当前分支。

---
### 4.推送数据到远程仓库

&emsp;&emsp;使用如下命令可以推送数据到远程仓库：
```
git push [remote-name] [branch-name]
```

---
### 5.查看远程仓库信息

&emsp;&emsp;我们可以使用如下命令查看某个远程仓库的详细信息：
```
git remote show [remote-name]
```

---
### 6.重命名远程仓库

&emsp;&emsp;可以使用如下命令更改远程仓库的名字：
```
git remote rename [old_name] [new_name]
```

---
### 7.删除远程仓库

&emsp;&emsp;可以使用如下命令删除一个远程仓库：
```
git remote rm [remote-name]
```

---

#### [返回目录](./)
