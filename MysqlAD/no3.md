## MySQL高级学习笔记 性能分析
---
### 1. 背景 

&emsp;&emsp;Mysql的查询优化器会对我们的查询进行优化，可以通过 `查询执行计划 Explain` 来分析Mysql的查询过程，进而达到性能分析的目的。

---
### 2. 分析内容

+ 表的读取顺序
+ 数据读取操作的操作类型
+ 哪些索引可以使用
+ 哪些索引被实际使用
+ 表之间的引用
+ 每张表有多少行被优化器查询

---
### 3. 语法

```
explain select语句
```

结果中各个字段含义：

+ id：表的读取顺序（数字大的优先，数字相同的按从上往下的顺序）
+ selet_type：查询的类型，有：
    1. SIMPLE   简单查询
    2. PRIMARY  主查询，包含子查询的最外层查询
    3. SUBQUERY 子查询
    4. DERIVED 衍生表查询
    5. UNION 联合查询
    6. UNION RESULT 联合后的结果查询
+ table：这一行数据是属于哪个表的
+ type：访问类型：
    1. ALL 全表访问
    2. index 遍历索引
    3. range 通过索引查询，匹配某个范围（范围条件）
    4. ref 通过索引查询，匹配某个值（等于条件），但匹配了多条记录
    5. eq_ref 通过索引查询，匹配某个值（等于条件），但匹配的只有一条
    6. const 通过索引一次就找到，查询主键或者unique索引，只匹配一行数据
    7. system 查询的表中只有一行记录的，等于系统表
    8. NULL

    从好到坏（如果是记录比较大，能够优化到range或者ref就可以了）：
    ```
    system > const > eq_ref > ref > range > index > ALL
    ```
+ possible_keys：可能应用在这张表中的索引列表。查询涉及到的字段上存在索引，就会列出。但不一定被实际查询使用。
+ key：
    1. 实际使用的索引。如果有覆盖索引，则出现在此列表中。
    2. NULL：没有使用索引
+ key_len：索引中使用的字节数，计算出查询中使用的索引长度。在能够查询到同样精确的结果情况下，这个值越短越好！是可能长度，不是实际长度。
+ ref：索引的哪些列被使用，可能是一个const表示常量。
+ rows：估算出找到所需记录需要读取的行数。
+ Extra：包含不适合在其他列中显示，但很重要的额外信息：
    1. Using Filesort（不好）：mysql无法使用索引进行的排序，需要使用外部的排序，称为文件排序。
    2. Using temporary（最坏）：使用了临时表保存中间结果，且对查询结果排序时使用了临时表。比如order by和group by。
    3. Using index（好的）：表示select中使用了覆盖索引，避免访问了表的数据行。 覆盖索引：需要的查询结果字段，被索引包含了，不必读取所有字段。
        + 同时using where：表示用了索引进行匹配查找。
        + 没有using where：表示只用索引来读数据，没有进行匹配查找。
    4. Using where：使用了where。
    5. Using join buffer：使用了链接缓存。
    6. impossible where：不可能成功的where，就是where的值总是false。
    7. select table optimized away：在没有Group by子句的情况下，基于索引优化MIN/MAX操作。
    8. distinct：优化distinct操作，在找到第一匹配的元组后停止找同样值的动作。



---

#### [返回目录](./)
