## PostgreSQL学习笔记 函数

### 1. 常用数值函数

| 函数名称 |     函数作用     |
| :------: | :--------------: |
|  AVG()   | 返回某列的平均值 |
| COUNT()  |  返回某列的行数  |
|  MAX()   | 返回某列的最大值 |
|  MIN()   | 返回某列的最小值 |
|  SUM()   | 返回某列的值之和 |

### 2. 常用字符串函数

|         函数名称          |      函数作用      |
| :-----------------------: | :----------------: |
|         LENGTH(s)         |   计算字符串长度   |
|    CONCAT(s1, s2, ...)    |   字符串合并函数   |
| LTRIM(s)/RTRIM(s)/TRIM(s) | 删除字符串空格函数 |
|    REPLACE(s, s1, s2)     |   字符串替换函数   |
|   SUMSTRING(s, n, len)    |    获取子串函数    |

### 3. 常用日期时间函数

|       函数名称       |       函数作用       |
| :------------------: | :------------------: |
| EXTRACT(type FROM d) |  获取日期指定值函数  |
|     CURRENT_DATE     |   获取当前日期函数   |
|     CURRENT_TIME     |   获取当前时间函数   |
|        NOW()         | 获取当前日期时间函数 |

### 4. 自定义函数语法

```
create function				//声明创建函数
	add(integer, integer)	//定义函数名称, 参数类型
returns integer				//定义函数返回值
	as 'select $1 + $2;'	//定义函数体
language SQL				//用以实现函数的语言的名称
returns null on null input;	//参数为NULL时，返回null
```





---

#### [返回目录](./)

