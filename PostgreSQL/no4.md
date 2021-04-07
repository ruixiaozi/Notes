## PostgreSQL学习笔记 插入操作

---

### 1. 插入单条数据

INSERT INTO 语句语法格式如下：

```
insert into TABLE_NAME (column1, column2, column3,...columnN) VALUES (value1, value2, value3,...valueN);
```

插入默认值使用 `DEFAULT`：

```
insert into COMPANY (ID,NAME,AGE,ADDRESS,SALARY,JOIN_DATE) VALUES (3, 'Teddy', 23, 'Norway', 20000.00, DEFAULT );
```

### 2. 插入多行数据

通过多行Value插入：

```
insert into TABLE_NAME (column1, column2, column3,...columnN) VALUES 
(value1, value2, value3,...valueN),
(value1, value2, value3,...valueN),
(value1, value2, value3,...valueN);
```

通过select插入：

```
insert into TABLE_NAME (column1, column2, column3,...columnN) 
select (column1, column2, column3,...columnN) from table2;
```



---

#### [返回目录](./)

