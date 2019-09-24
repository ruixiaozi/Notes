## Linux学习笔记 几个基础命令
---
### 1. 日期时间命令：data  
```
# date [-u] [-d datestr] [-s datestr] [--utc] [--universal] [--date=datestr] [--set=datestr] [--help] [--version] [+FORMAT] [MMDDhhmm[[CC]YY][.ss]]
```
&emsp;&emsp;其中的部分参数说明：
+ -d 'datestr' : 显示 datestr字符串 中表示的时间 (非系统时间)
+ -s 'datestr' : 将系统时间设为 datestr字符串 中所表示的时间
+ -u : 显示目前的格林威治时间(GMT)
+ -I[TIMESPEC] : 使用ISO 8601标准格式显示时间字符串，其中TIMESPEC可以是"hours"、"minutes"、"date"、"seconds"、 "ns"。默认为"date"
+ -R : 使用RFC-2822标准格式显示时间字符串
+ '+FORMAT' : 通常会加上一个引号括起来(可以不用引号，当有空格的时候最好使用)，表示格式化输出时间
+ '[MMDDhhmm[[CC]YY][.ss]' : 如果带上这种格式的字符串，就是设置当前系统时间，和-s的功能一样。其中 MM 为月份，DD 为日，hh 为小时，mm 为分钟，CC 为年份前两位数字，YY 为年份后两位数字，ss 为秒数

&emsp;&emsp;FORMAT格式如下：
>时间方面：  
>  
>% : 印出 %  
>%n : 下一行  
>%t : 跳格  
>%H : 小时(00..23)  
>%I : 小时(01..12)  
>%k : 小时(0..23)  
>%l : 小时(1..12)  
>%M : 分钟(00..59)  
>%p : 显示本地 AM 或 PM  
>%r : 直接显示时间 (12 小时制，格式为 hh:mm:ss [AP]M)  
>%s : 从 1970 年 1 月 1 日 00:00:00 UTC 到目前为止的秒数  
>%S : 秒(00..61)  
>%T : 直接显示时间 (24 小时制)  
>%X : 相当于 %H:%M:%S  
>%Z : 显示时区  
>  
>日期方面：  
>  
>%a : 星期几 (Sun..Sat)  
>%A : 星期几 (Sunday..Saturday)  
>%b : 月份 (Jan..Dec)  
>%B : 月份 (January..December)  
>%c : 直接显示日期与时间  
>%d : 日 (01..31)  
>%D : 直接显示日期 (mm/dd/yy)  
>%h : 同 %b  
>%j : 一年中的第几天 (001..366)  
>%m : 月份 (01..12)  
>%U : 一年中的第几周 (00..53) (以 Sunday 为一周的第一天的情形)  
>%w : 一周中的第几天 (0..6)  
>%W : 一年中的第几周 (00..53) (以 Monday 为一周的第一天的情形)  
>%x : 直接显示日期 (mm/dd/yy)  
>%y : 年份的最后两位数字 (00.99)  
>%Y : 完整年份 (0000..9999)  

&emsp;&emsp;当您以 root 身分更改了系统时间之后，请记得以 `clock -w` 来将系统时间写入 CMOS 中，这样下次重新开机时系统时间才会持续抱持最新的正确值。另外可以使用 `ntpdate ntp地址` 命令通过网络更新系统时间。常用ntp地址：
```
time.windows.com
cn.pool.ntp.org
cn.ntp.org.cn
```

&emsp;&emsp;时间字符串标准参考一下： 其他标准学习笔记->时间字符串标准

---
### 2. 日历命令：cal
```
# cal [options] [[[day] month] year]
```
&emsp;&emsp;其中options有如下几个：  
+ -1 显示一个月的月历
+ -3 显示系统前一个月，当前月，下一个月的月历
+ -s  显示星期天为一个星期的第一天(在ubuntu中不支持)，默认的格式
+ -m 显示星期一为一个星期的第一天(在ubuntu中不支持)
+ -j  显示在当年中的第几天（一年日期按天算，从1月1号算起，默认显示当前月在一年中的天数）
+ -y  显示当前年份的日历

---
### 3. 计算器命令：bc
```
# bc [ options ] [long-options] [  file ... ]
```
&emsp;&emsp;options如下：
+ -i：强制进入交互式模式
+ -l：使用标准数学库
+ -w：对POSIX bc的扩展给出警告信息
+ -s: 使用 POSIX 标准来处理
+ -q：不显示欢迎信息

&emsp;&emsp;file是指定包含计算任务的文件。

&emsp;&emsp;计算器可以进行基本的算术运算，使用quit退出，详细的使用方法参考`man bc`。

---
#### [返回目录](./)