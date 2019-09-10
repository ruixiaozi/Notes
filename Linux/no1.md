## Linux学习笔记 历史
---
### 1.Unix的发展历史

+ Multics系统  
为了强化大型主机的功能，以便让主机的资源可以提供给更多用户来使用。在1965年前后，三大巨头：Bell，MIT和GE发起了Multics计划：让大型主机可以实现提供300个以上的终端用于联机使用。
+ Unics系统  
参与过Multics计划的Ken Thompson通过汇编语言编写了一组内核程序，包括内核工具与小型的文件系统。因为简化了Multics的功能，于是便被朋友称为Unics。  
涉及了重要的概念：所有程序或系统设备都是文件。  
+ Unix系统  
因为Unics使用汇编语言编写而成，移植性不好，Thompson和Ritchie打算使用高级语言来编写，Ritchie将B语言重新改编成C语言，再用C语言重写改写了Unics，命名为Unix。
+ BSD系统  
伯克利大学的Bill Joy取得Unix源码，修改成适合自己机器的版本，并且添加了很多工具软件和编译器，将他命名为BSD (如今的FreeBSD是BSD改版而来的)。  
+ System V系统  
AT&T自家的Unix系统叫做System V，还有各大公司的Unix操作系统，都与自己的硬件设备配合使用。纯种的Unix可以说只有System V和BSD。System V第七版可以支持X86架构，但开始收回Unix的版权。  
+ Minix系统  
自Unix被AT&T收回版权后，Tanenbaum教授便自己动手写了一个Unix-like的内核，完全不参照Unix内核代码，而且必须和Unix兼容。

---
### 2.GNU计划、自由软件、GPL、开源软件与闭源软件

+ GNU计划是由理查德·斯托曼(Richard Stallman)在1983年发起的，它的主要目标是创建一套完全自由的Unix-like操作系统。其中一个理由就是要“重现当年软件界合作互助的团结精神”。但写操作系统过于复杂，于是便先以写可以在Unix上运行的程序作为目标。在此期间他改写了之前的Emacs，成立FSF自由软件基金会，请来工程师和志愿者一起完善了GCC(GNU C Complier)。GNU计划和FSF开发出来的软件被统称为自由软件(Free Software)。GNU计划里还编写了Bash Shell。  
+ 1985年，为了避免GNU所开发的自由软件被用做专利软件，斯托曼与律师草拟了GPL(General Public License)通用公共许可证来保护自由软件。并称作copyleft。GPL强调的自由软件：用户可以自由地执行、复制、再发行、学习、修改与强化自由软件。但不可以修改授权和单纯售卖。
+ 开源软件：是一种源代码可以任意获取的计算机软件，这种软件的版权持有人在软件协议的规定之下保留一部分权利并允许用户学习、修改、增进提高这款软件的质量。GPL规定的自由软件算开源软件的一种，且为较严格的一种。开源软件目前拥有许多开源软件授权，如同GPL。
+ 闭源软件：不公布源代码，被称为copyright。一般有两种方式：免费软件和共享软件。

---
### 3.Linux发展历史

+ Linux起源  
Linus Torvalds在386机器上使用Minix系统后，觉得很不错，但是Minix并没有进一步开发，功能不够。于是Torvalds决定自己写一个想要的系统，同时当时有了GNU计划的一些自由软件比如：GCC和bash。开发出来以后，他放到网络上，因为FTP网站将这个目录取名为Linux(Linus 的 Unix)，所以后面便称作Linux了，且这第一个放到网上的版本是0.02。

+ 兼容性  
由于Linux不同于Unix，许多软件还是不能在Linux运行，值得修改软件进行移植。于是Torvalds开始修改Linux，让Linux支持POSIX(Portable Operating System Interface 可移植操作系统接口)规范，这样Linux就可以很容易地兼容Unix的软件了。

+ 后续发展  
后来Linux使用的人不断增加，Torvalds一个人没有足够的精力来维护了，于是发展成模块化，将一些功能独立于内核外，慢慢的越来越多人加入到维护行列来，后来便成立了Linux的内核网站：`https://www.kernel.org`，也正是Linux内核的到来，让GNU计划中的大量软件得到广泛应用，如今Linux基本上就是搭载Linux内核 + GNU软件，所以也被托斯曼认为是GNU/Linux。

---
### 4.Linux内核版本

&emsp;&emsp;Linux的内核版本编号如下：
```
3.7.5-201.fc18.x86_64
主版本.次版本.发布版本-修改版本
```
&emsp;&emsp;从3.0版本后，内核主要根据主线版本(MainLine)开发，开发完成后，就开发下一个主线版本。每个版本都有新功能的加入。当新的主线版本出现以后，对于旧的主线版本，一般分为两种方式：1.结束开发(EOF End of Live)。2.长期维护(Longterm)。

---
#### [返回目录](./)