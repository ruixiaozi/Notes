## Linux学习笔记 搭建FTP服务器
---
### 1. 介绍

&emsp;&emsp;本次专题使用vsftp在linux上搭建ftp服务器，测试机为ubuntu，不同发行版理论上通用（安装软件命令需要更改，本次测试默认使用root用户进行操作），把主要存在的问题已经找出。

---
### 2. FTP传输模式

&emsp;&emsp;FTP客户端与服务器端有两种传输模式，分别是**FTP主动模式**、**FTP被动模式**。主被动模式均是以FTP服务器端为参照。
+ **FTP主动模式**：客户端从一个任意的端口N（N>1024）连接到FTP服务器的port 21命令端口，客户端开始监听端口N+1，并发送FTP命令“port N+1”到FTP服务器，FTP服务器以数据端口（20）连接到客户端指定的数据端口（N+1）。
+ **FTP被动模式**：客户端从一个任意的端口N（N>1024）连接到FTP服务器的port 21命令端口，客户端开始监听端口N+1，客户端提交 PASV命令，服务器会开启一个任意的端口（P >1024），并发送PORT P命令给客户端。客户端发起从本地端口N+1到服务器的端口P的连接用来传送数据。

&emsp;&emsp;主动模式，只需要开放服务器的20,21端口；被动模式，需要开放21端口，和1024以上的一个范围端口。

---
### 3. 安装vsftpd

&emsp;&emsp;在ubuntu中使用下面的命令安装：
```
# apt-get install vsftpd
```
&emsp;&emsp;启动|停止|重启|状态 使用一下命令：
```
# systemctl start|stop|restart|status vsftpd
```

---
### 4. 配置【重点】

&emsp;&emsp;配置有3大类：①**匿名访问配置** ②**本地用户访问配置** ③**虚拟用户访问配置**。匿名和本地用户都具有一定的安全风险，且不常用、配置较为简单。**本次测试仅仅使用虚拟用户访问配置**。

&emsp;&emsp;vsftpd的全局配置文件是`/etc/vsftpd.conf`，先备份源文件：
```
# mv /etc/vsftpd.conf /etc/vsftpd.conf.bak
```
然后创建一个新的`/etc/vsftpd.conf`，并开始编辑：
```
# vim /etc/vsftpd.conf
```
提示：以下的配置，按需求逐条（顺序不用一致）是写入`/etc/vsftpd.conf`
1. 配置监听模式：
```
#以下两个监听配置，选择一个，就必须注释掉另一个 
#如果设置为YES，监听IPv4端口的连接请求
listen=YES
#如果设置为YES，同时监听IPv4和IPv6端口
#listen_ipv6=YES
```
2. 配置传输模式：
```
#以下两种方式只选一种，注释掉另一种
#
#被动方式：
#设置让数据从20端口发送（主动模式专属）
#connect_from_port_20=NO
#设置是否允许被动模式
#pasv_enable=YES
#使用的端口范围
#pasv_min_port=50000
#pasv_max_port=60000
#
#主动方式：
connect_from_port_20=YES
pasv_enable=NO
```

3. 配置通用控制参数：
```
#设定不允许匿名访问
anonymous_enable=NO
#设定可以进行写操作。
write_enable=YES
#设定上传后文件的权限掩码。
local_umask=022
#禁止匿名用户上传。
anon_upload_enable=NO
#禁止匿名用户建立目录。
anon_mkdir_write_enable=NO
#设定开启目录标语功能。
dirmessage_enable=YES
#设定开启日志记录功能。
xferlog_enable=YES
#设定日志使用标准的记录格式。
xferlog_std_format=YES
#设定Vsftpd的服务日志保存路径
xferlog_file=/var/log/vsftpd.log
#设定禁止上传文件更改宿主。
chown_uploads=NO
#设定空闲连接超时时间，单位为秒，默认600。
idle_session_timeout=3000
#设定空闲连接超时时间，单位为秒，默认120.
data_connection_timeout=120
#设定支持异步传输功能。
async_abor_enable=YES
#设定支持ASCII模式的上传和下载功能。
ascii_upload_enable=YES
ascii_download_enable=YES
#设定Vsftpd的登陆标语。
ftpd_banner=Welcome to Ruixiaozi FTP service.
#禁止用户登陆FTP后使用"ls -R"的命令。该命令会对服务器性能造成巨大开销。
ls_recurse_enable=NO
#设定支持TCP Wrappers
tcp_wrappers=YES
```
4. 配置虚拟用户参数：
```
#设定本地用户可以访问。注意：主要是为虚拟宿主用户，如果该项目设定为NO那么所有虚拟用户将无法访问。
local_enable=YES
#是否将所有用户限制在自己的root目录
chroot_local_user=YES
#新版vsftpd安全检查如果限制用户在自己的root目录，则不允许用户的root目录具有写权限，设置这个表示，可以允许有写权限
allow_writeable_chroot=YES
#设定启用虚拟用户功能。
guest_enable=YES
#指定虚拟用户的宿主用户(需要新建一个用户vsftpd，具体请看下文)。
guest_username=vsftpd
#设定虚拟用户的权限符合他们的宿主用户。
virtual_use_local_privs=YES
#设定PAM服务下的验证配置文件名。因此，PAM验证将参考/etc/pam.d/下的此文件。
pam_service_name=vsftpd
#设定虚拟用户个人 配置文件（内容与/etc/vsftpd.conf格式一样） 存放目录，用于设置不同用户不同限制参数。注意：配置文件名必须和虚拟用户名相同。
user_config_dir=/etc/vsftpd/virtualconf
```

&emsp;&emsp;到此为止，`/etc/vsftpd.conf`的配置完成了。接下来需要做一些后续操作：
1. 创建宿主用户（所有虚拟用户实际操作，在后台使用该用户进行）：
```
# useradd -d /home/vsftpd -s /usr/sbin/nologin vsftpd
```

2. 创建虚拟用户列表：

&emsp;&emsp;首先创建虚拟用户配置的目录`/etc/vsftpd/`：
```
# mkdir /etc/vsftpd
```
&emsp;&emsp;然后在该目录下创建**虚拟用户信息**文件`/etc/vsftpd/users`：
```
# vim /etc/vsftpd/users
```
&emsp;&emsp;输入内容（可多行，奇数行为用户名，偶数行为密码）:
```
user1
123456
```
3. 生成虚拟用户数据库：

&emsp;&emsp;安装数据库生成工具dbx.x-util（x.x是版本号，可以用tab建查看当前系统软件库里带的是多少）：
```
# apt-get install db5.3-util
```
&emsp;&emsp;把**虚拟用户信息文件**生成为db数据库，并删除原文件：
```
# db5.3_load -T -t hash -f /etc/vsftpd/users /etc/vsftpd/users.db
# rm /etc/vsftpd/users
```
4. 配置pam认证服务（登陆验证）：

&emsp;&emsp;安装pam认证服务：
```
# apt-get install pam
```
&emsp;&emsp;先备份pam默认的vsftpd认证配置文件`/etc/pam.d/vsftpd`：
```
# cp /etc/pam.d/vsftpd /etc/pam.d/vsftpd.bak
```
&emsp;&emsp;vim编辑`/etc/pam.d/vsftpd`：
```
# vim /etc/pam.d/vsftpd
```
&emsp;&emsp;在文件开头，添加以下内容：
```
#%PAM
auth    sufficient      pam_userdb.so     db=/etc/vsftpd/users
account sufficient      pam_userdb.so     db=/etc/vsftpd/users
```
&emsp;&emsp;以上内容的意义：
```
这里的 auth 是指对用户的用户名口令进行验证。
这里的 accout 是指对用户的帐户有哪些权限哪些限制进行验证。
其后的 sufficient 表示充分条件，也就是说，一旦在这里通过了验证，那么也就不用经过下面剩下的验证步骤了。相反，如果没有通过的话，也不会被系统立即挡之门外，因为sufficient的失败不决定整个验证的失败，意味着用户还必须将经历剩下来的验证审核。
再后面的 pam_userdb.so 表示该条审核将调用pam_userdb.so这个库函数进行。
最后的 db=/etc/vsftpd/users 则指定了验证库函数将到这个指定的数据库中调用数据进行验证。
```

5. 配置虚拟用户的个人配置

&emsp;&emsp;在`/etc/vsftpd/`目录下创建`virtualconf`目录：
```
# mkdir /etc/vsftpd/virtualconf
```
&emsp;&emsp;在`/etc/vsftpd/virtualconf`目录下按照之前创建的虚拟用户，创建对应的配置文件，文件名与用户名相同。例如：
```
# vim /etc/vsftpd/virtualconf/user1
```
&emsp;&emsp;在文件中填写个人配置：
```
#指定用户登陆FTP后的root路径（必填）。
local_root=/home/user1
#设定空闲连接超时时间。
#idle_session_timeout=600
#设定单次连续传输最大时间。
#data_connection_timeout=120
#设定并发客户端访问个数。
#max_clients=10
#设定单个客户端的最大线程数，这个配置主要来照顾Flashget、迅雷等多线程下载软件。
#max_per_ip=5
#设定该用户的最大传输速率，单位b/s。
#local_max_rate=50000
```
&emsp;&emsp;把root路径设置成宿主用户（vsftpd）所有，否则可能出现权限问题：
```
# chown vsftpd:vsftpd /home/user1
```

---
### 5. 重启服务，测试

&emsp;&emsp;重启vsftpd服务：
```
# systemctl restart vsftpd
```
&emsp;&emsp;接下来打开ftp客户端连接测试即可！确保服务器防火墙打开了20和21端口。

---

#### [返回目录](./)
