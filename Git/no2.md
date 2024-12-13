## Git学习笔记 提交更新
---
### 1.查看仓库状态

&emsp;&emsp;要查看当前仓库的状态，使用如下命令：
```
git status
```
&emsp;&emsp;通过这个命令可以看到哪些文件没有被提交到缓存区。

---
### 2.添加文件到暂存区

&emsp;&emsp;如果在目录下有新文件或者以及跟踪过的文件有更新，那么需要添加该文件到暂存区，使用如下命令：
```
git add [file]
```
&emsp;&emsp;其中file可以是单个文件，也可以是带通配符的文件，也可以是一个目录，如果是目录那么则递归添加所有子文件。

---
### 3.忽略某些文件

&emsp;&emsp;如果要忽略掉一些文件的话，那么只需要在项目目录下创建一个.gitignore文件，文件 .gitignore 的格式规范如下：
> + 所有空行或者以注释符号 ＃ 开头的行都会被 Git 忽略。
+ 可以使用标准的 glob 模式匹配。
+ 匹配模式最后跟反斜杠（/）说明要忽略的是目录。
+ 要忽略指定模式以外的文件或目录，可以在模式前加上惊叹号（!）取反。

&emsp;&emsp;glob 模式是指 shell 所使用的简化了的正则表达式。星号（ * ）匹配零个或多个任意字符；[abc] 匹配任何一个列在方括号中的字符（这个例子要么匹配一个 a，要么匹配一个 b，要么匹配一个 c）；问号（?）只匹配一个任意字符；如果在方括号中使用短划线分隔两个字符，表示所有在这两个字符范围内的都可以匹配（比如 [0-9] 表示匹配所有 0 到 9 的数字）

---
### 4.提交更新到仓库

&emsp;&emsp;输入如下命令，可以把暂存区的内容提交更新到仓库：
```
git commit
```
&emsp;&emsp;执行该命令后，会出现一个文本编辑器，输入本次提交的信息，也可以使用如下格式，提交简略信息：
```
git commit -m [message]
```

---
### 5.Commit message 的格式

&emsp;&emsp;使用commit提交的时候，该信息其实有一定的格式规范，按照该格式，可以快速生成Change log。参考：[Commit message 和 Change log 编写指南](http://www.ruanyifeng.com/blog/2016/01/commit_message_change_log.html)

&emsp;&emsp;每次提交，Commit message 都包括三个部分：Header，Body 和 Footer。具体如下：
```
<type>(<scope>): <subject>
// 空一行
<body>
// 空一行
<footer>
```
&emsp;&emsp;其中，Header 是必需的，Body 和 Footer 可以省略。不管是哪一个部分，任何一行都不得超过72个字符（或100个字符）。

 &emsp;&emsp;1. Header部分只有一行，包括三个字段：type（必需）、scope（可选）和subject（必需）。  
 + type 用于说明 commit 的类别，只允许使用下面7个标识
 ```
feat：新功能（feature）
fix：修补bug
docs：文档（documentation）
style： 格式（不影响代码运行的变动）
refactor：重构（即不是新增功能，也不是修改bug的代码变动）
test：增加测试
chore：构建过程或辅助工具的变动
```
如果type为feat和fix，则该 commit 将肯定出现在 Change log 之中。其他情况（docs、chore、style、refactor、test）由你决定，要不要放入 Change log，建议是不要。

+ scope 用于说明 commit 影响的范围，比如数据层、控制层、视图层等等，视项目不同而不同。

+ subject是 commit 目的的简短描述，不超过50个字符。格式要求：
> + 以动词开头，使用第一人称现在时，比如change，而不是changed或changes
> + 第一个字母小写
> + 结尾不加句号（.）

&emsp;&emsp;2. Body 部分是对本次 commit 的详细描述，可以分成多行。应该说明代码变动的动机，以及与以前行为的对比。

&emsp;&emsp;3. Footer 部分只用于两种情况。

+ 如果当前代码与上一个版本不兼容，则 Footer 部分以BREAKING CHANGE开头，后面是对变动的描述、以及变动理由和迁移方法。

+ 如果当前 commit 针对某个issue，那么可以在 Footer 部分关闭这个 issue 。

&emsp;&emsp;4.还有一种特殊情况，如果当前 commit 用于撤销以前的 commit，则必须以revert:开头，后面跟着被撤销 Commit 的 Header。Body部分的格式是固定的，必须写成This reverts commit &lt;hash>.，其中的hash是被撤销 commit 的 SHA 标识符。

---
### 6.跳过使用暂存区

&emsp;&emsp;如果不需要使用暂存区，每次添加后都要提交更新，那么可以直接跳过暂存区，给 git commit 加上 -a 选项，Git 就会自动把所有已经跟踪过的文件暂存起来一并提交。

---
### 7.从暂存区移除

&emsp;&emsp;可以使用如下命令取消跟踪某个文件，也就是从暂存区中移除：
```
git rm --cached [file]
```
&emsp;&emsp;其中file同git add里一样。

---
### 8.移动

&emsp;&emsp;文件被重新命名或者移动位子，就需要提交旧的文件被删除和新的文件被跟踪的信息。使用如下命令可以更方便：
```
git mv file_from file_to
```
&emsp;&emsp;该命令相当于：
```
mv file_from file_to
git rm --cached file_from
git add file_to
```

---

#### [返回目录](./)
