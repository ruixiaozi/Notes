## PostgreSQL学习笔记 查找操作

---

### 1. 基本语法

```
SELECT 
	column1, column2,...columnN 
FROM table_name，table2, ...table2
    [WHERE <表达式>]
    [GROUP BY <group by definition>]
    [HAVING <表达式>[{操作符 表达式}...]]
    [ORDER BY 字段名 [desc [nulls last/first]],...字段名3 [desc [nulls last/first]]]	//前面的具有更高的优先级
    [LIMIT 数量 [offset 偏移量]];
```

### 2. 链接查询

1. 内连接

```
//隐式内连接
select a_col1, a_col2, b_col1, b_col2 
    from table1, table2 
    where a_pid = b_id;

//显示内连接
select a_col1, a_col2, b_col1, b_col2 
    from table1, table2 
    inner join a on a_pid = b_id;
```

2. 





---

#### [返回目录](./)

