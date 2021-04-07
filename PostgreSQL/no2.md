## PostgreSQL学习笔记 数据库操作

---

### 1. 创建数据库

`create database` 命令需要在 PostgreSQL 命令窗口来执行，语法格式如下：

```
create database dbname;
```

或者指定所有者：

```
create database dbname owner rolename;
```

### 2. 查看数据库

使用 **\l** 用于查看已经存在的数据库：

```
postgres=# \l
                             List of databases
   Name    |  Owner   | Encoding | Collate | Ctype |   Access privileges   
-----------+----------+----------+---------+-------+-----------------------
 postgres  | postgres | UTF8     | C       | C     | 
 runoobdb  | postgres | UTF8     | C       | C     | 
 template0 | postgres | UTF8     | C       | C     | =c/postgres          +
           |          |          |         |       | postgres=CTc/postgres
 template1 | postgres | UTF8     | C       | C     | =c/postgres          +
           |          |          |         |       | postgres=CTc/postgres
(4 rows)
```

### 3. 选择数据库

可以使用 **\c + 数据库名** 来进入数据库：

```
postgres=# \c runoobdb
You are now connected to database "runoobdb" as user "postgres".
runoobdb=# 
```

### 4. 删除数据库

`drop database` 会删除数据库的系统目录项并且删除包含数据的文件目录。

`drop database` 只能由超级管理员或数据库拥有者执行。

`drop database` 命令需要在 PostgreSQL 命令窗口来执行，语法格式如下：

```
drop database [ if exists ] name
```

**参数说明：**

- **if exists**：如果数据库不存在则发出提示信息，而不是错误信息。
- **name**：要删除的数据库的名称。



---

#### [返回目录](./)

