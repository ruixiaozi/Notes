## MySQL高级学习笔记 索引
---
### 1. 介绍

&emsp;&emsp;Index（索引）是帮助Mysql高效获取数据的数据结构。像字典一样，提高效率。是排好序的快速查找数据结构（B树\hash\全文\R树）。

优点：

+ 提高检索速率，因为有序，所以检索起来可以用算法提高
+ 降低排序成本，因为索引就是有序的，建起来就有序了

缺点：

+ 占空间
+ 虽然提高检索速度，但是会降低更新速度
+ 研究如何建立优秀的索引

---
### 2. 分类

1. 单值索引：一个索引只包含一个字段，一个表可以有多个单值索引
2. 唯一索引：索引列的值必须唯一，但允许空
3. 复合索引：一个索引包含多个字段


---
### 3. 语法 

+ 创建 

    ```
    create [unique] index indexName on tableName(columName,columName2 ……);

    alter table tableName add [unique] index [indexName]  (columName,columName2 ……);
    
    alter table tableName add primary key (columName,columName2 ……);
    ```

+ 删除 

    ```
    drop index indexName on tableName;

    alter table tableName drop index indexName;

    alter table tableName drop primary key;
    ```

+ 查看

    ```
    show index from tableName;
    ```


---
### 4. 建索引的条件

适合创建的：

+ 主键
+ 频繁查找的字段
+ 外键
+ 查询中排序的字段，将大大提高排序速度
+ 查询中统计和分组的字段

不适合创建的：

+ 频繁更新的字段
+ 频繁更新的表
+ where条件用不到的
+ 表记录太少
+ 字段有大量重复值，且每种值的数量均匀

---

#### [返回目录](./)
