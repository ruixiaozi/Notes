## Git学习笔记 分支
---
### 1.创建和切换分支

&emsp;&emsp;使用如下命令可以同时创建和切换分支：
```
git checkout -b [分支名]
```
&emsp;&emsp;相当于两条命令：
```
git branch [分支名]
git checkout [分支名]
```

---
### 2.分支的合并

&emsp;&emsp;在需要合并的目标分支下使用如下命令可以把某一个分支合并进来：
```
git merge [分支名]
```
&emsp;&emsp;1.如果没有冲突出现，则直接合并成功，并让确认本次提交的信息。  
&emsp;&emsp;2.如果在执行后开始合并的时候遇到冲突（即同一个文件在两个分支中产生了不同的修改），那么需要我们来解决冲突，此时会提示哪些文件产生来冲突，我们需要去修改对应的文件，手动解决好冲突，然后使用 `git add` 把文件标记为解决，最后使用 `git commit`来提交本次合并。

---
### 3.分支的删除

&emsp;&emsp;使用如下命令可以删除分支：
```
git branch -d [分支名]
```

---
### 4.查看分支

&emsp;&emsp;使用如下命令查看当前的分支列表：
```
git branch
```
&emsp;&emsp;如果想要查看更详细一点的信息，可以加上-v参数。

---
### 5.查看与当前分支合并的分支或者未合并的分支

&emsp;&emsp;可以用`git branch `加上--merged 和 --no-merged 参数来查看。

---
### 6.推送分支

&emsp;&emsp;使用如下命令，可以把一个本地分支推送到远程：
```
git push [远程名] [本地分支名]:[远程分支名]
```

---
### 7.分化一个远程分支到本地

&emsp;&emsp;可以对远程的一个分支，创建一个本地分支，使用如下命令：
```
git checkout -b [分支名] [远程名]/[分支名]
```

### 8.跟踪远程分支

&emsp;&emsp;从远程分支 checkout 出来的本地分支，称为 跟踪分支 (tracking branch)，可以直接git push默认推送到对应的分支，使用如下命令可以跟踪远程分支：
```
git checkout --track  [远程名]/[分支名]
```

---
### 9.删除本地的远程分支

&emsp;&emsp;使用如下命令可以删除本地的一个远程分支：
```
git push [远程名] :[分支名]
```
&emsp;&emsp;注意:前有空格。


---

#### [返回目录](./)
