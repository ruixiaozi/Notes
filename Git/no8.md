## Git学习笔记 变基
---
### 1.合并多次提交记录

&emsp;&emsp;对于一个功能多次提交，造成冗余。使用如下命令进入最近几次提交的编辑：
```
git rebase -i HEAD~[N]
```
&emsp;&emsp;其中[N]表示从当前提交往前找几个提交。进入编辑模式，可以根据下方的提示，修改，进行合并。如果异常退出了 vi 窗口，可以使用如下命令：
```
git rebase --edit-todo
```
&emsp;&emsp;如果修改完成，使用如下命令：
```
git rebase --continue
```

---
### 2.分支合并

&emsp;&emsp;在当前分支使用如下命令，可以合并当前和目标分支，然后当前分支指向最新节点，上一个节点为目标分支的最后一次提交：
```
git rebase [分支名]
```


---

#### [返回目录](./)
