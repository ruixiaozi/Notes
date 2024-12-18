## Git学习笔记 标签
---
### 1.显示已有标签

&emsp;&emsp;使用如下命令可以显示已有的标签列表：
```
git tag
```
---
### 2.创建标签

&emsp;&emsp;标签有两种形式，一种是含附注的标签，一种轻量级的标签，含附注的标签使用如下格式的命令：
```
git tag -a [版本号] -m [说明]
```
&emsp;&emsp;轻量级的标签使用如下格式的命令：
```
git tag [版本号]
```

---
### 3.后期加标签

&emsp;&emsp;使用如下命令可以给制定的提交记录打上标记：
```
git tag -a [标签号] [提交记录的校验值]
```
&emsp;&emsp;其中校验值可以只取前几位。

---
### 4.分享标签

&emsp;&emsp;使用git push的时候一般不会把标签推上去，需要使用--tags参数才行。如下命令：
```
git push origin --tags
```

---
### 5.删除标签

&emsp;&emsp;使用如下命令可以删除本地标签：
```
git tag -d [标签号]
```
&emsp;&emsp;然后使用下面的命令把更改推送到远程：
```
git push origin --delete [标签号]
```

---

#### [返回目录](./)
