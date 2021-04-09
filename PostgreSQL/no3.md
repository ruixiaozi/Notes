## PostgreSQL学习笔记 表操作

---

### 1. 创建表格

**create table** 语法格式如下：

```
create table table_name(
   column1 datatype,
   column2 datatype,
   column3 datatype,
   .....
   columnN datatype,
);
```

### 2. 约束

**一个字段可以有多个约束。只要一个接着一个写就可以了**。

1. **缺省值**

   在一个表定义里，缺省值是在字段数据类型后面列出的：

   ```
   create table products (
       product_no integer,
       name text,
       price numeric DEFAULT 9.99
   );
   ```

   缺省值可以是一个表达式，它会在插入缺省值的时候计算(**不是**在创建表的时候)：

   ```
   create table products (
       product_no integer DEFAULT nextval('products_product_no_seq'),
       ...
   );
   ```

2. **检查约束**

   检查约束是最常见的约束类型。**一个检查约束由一个关键字`CHECK`后面跟一个放在圆括弧里的表达式组成**。

   它允许你声明在某个字段里的数值必须使一个布尔表达式为真。 

   以下是一个 **字段约束** ：

   ```
   create table products (
       product_no integer,
       name text,
       price numeric CHECK (price > 0)
   );
   ```

   还可以给这个约束取一个独立的名字。这样就可以令错误消息更清晰， 并且在你需要修改它的时候引用这个名字：

   ```
   CREATE TABLE products (
       product_no integer,
       name text,
       price numeric CONSTRAINT positive_price CHECK (price > 0)
   );
   ```

   检查约束也可以引用多个字段（**表约束**），同样可以使用命名的方式：

   ```
   CREATE TABLE products (
       product_no integer,
       name text,
       price numeric,
       discounted_price numeric,
       CHECK (price > discounted_price),
       CONSTRAINT valid_discount CHECK (price > discounted_price)
   );
   ```

3. **非空约束**

   非空约束只是简单地声明一个字段必须不能是 NULL：

   ```
   CREATE TABLE products (
       product_no integer NOT NULL,
       name text NOT NULL,
       price numeric
   );
   ```

4. **唯一约束**

   唯一约束保证在一个字段或者一组字段里的数据与表中其它行的数据相比是唯一的：

   ```
   CREATE TABLE products (
       product_no integer CONSTRAINT must_be_different  UNIQUE,
       name text,
       price numeric
   );
   
   或者
   
   CREATE TABLE products (
       product_no integer,
       name text,
       price numeric,
       CONSTRAINT must_be_different UNIQUE (product_no, name)
   );
   ```

   **添加一个唯一约束通常会自动在约束中使用的列或一组列上创建一个唯一bTree索引**

5. **主键**

   从技术上讲，主键约束只是唯一约束和非空约束的组合：

   ```
   CREATE TABLE products (
       product_no integer CONSTRAINT pr_key PRIMARY KEY,
       name text,
       price numeric
   );
   
   或者
   
   CREATE TABLE example (
       a integer,
       b integer,
       c integer,
       CONSTRAINT pr_key PRIMARY KEY (a, c)
   );
   ```

   **添加一个主键将会在主键使用的列或一组列中自动创建一个唯一btree索引**

6. **外键**

   外键约束声明一个字段(或者一组字段)的数值必须匹配另外一个表中出现的数值：

   ```
   CREATE TABLE products (
       product_no integer PRIMARY KEY,
       name text,
       price numeric
   );
   CREATE TABLE orders (
       order_id integer PRIMARY KEY,
       product_no integer REFERENCES products (product_no),
       quantity integer
   );
   
   或者
   
   CREATE TABLE t1 (
     a integer PRIMARY KEY,
     b integer,
     c integer,
     FOREIGN KEY (b, c) REFERENCES other_table (c1, c2)
   );
   ```

   可以设置删除、更新级联限制：

   删除： `on delete [选项]`

   更新： `on update [选项]`

   选项：

   + NO ACTION（默认）：如果在检查约束的时候还存在任何引用行，则抛出错误
   + RESTRICT：`RESTRICT`禁止删除被引用的行
   + CASCADE：在删除一个被引用的行的时候，所有引用它的行也会被自动删除掉

   ```
   CREATE TABLE order_items (
       product_no integer REFERENCES products ON DELETE RESTRICT,
       order_id integer REFERENCES orders ON DELETE CASCADE,
       quantity integer,
       PRIMARY KEY (product_no, order_id)
   );
   ```

   在外键字段上的动作还有两个选项： `SET NULL`和`SET DEFAULT`，它们导致在被引用行删除的时候， 将引用它们的字段分别设置为 NULL 和缺省值。

   **一个外键必须要么引用一个主键，要么引用一个唯一约束**

7. **排除约束**

   排他约束保证如果将任何两行的指定列或表达式使用指定操作符进行比较，至少其中一个操作符比较将会返回否或空值。

   ```
   CREATE TABLE circles (
       c circle,
       EXCLUDE USING gist (c WITH &&)
   );
   ```



### 3. 删除表格

`drop table`  命令来删除一个表格：

```
DROP TABLE my_first_table;
```

TRUNCATE TABLE 删除，语法如下：

```
TRUNCATE TABLE  table_name;
```

### 4. 修改表格

修改一个表的定义，或者说结构，可以：

- 增加字段
- 删除字段
- 增加表约束
- 删除表约束
- 修改字段约束
- 修改字段数据类型
- 重命名字段
- 重命名表

1. **增加字段**

   要增加一个字段，使用下面这样的命令：

   ```
   alter table products add column description text;
   ```

2. **删除字段**

   要删除一个字段，使用下面这样的命令：

   ```
   alter table products drop column description;
   ```

3. **增加表约束**

   要增加一个约束，必须使用表约束语法。比如：

   ```
   alter table products add CHECK (name <> '');
   alter table products add CONSTRAINT some_name UNIQUE (product_no);
   alter table products add FOREIGN KEY (product_group_id) REFERENCES product_groups;
   ```

   要增加一个字段约束，使用下面的语法(修改字段约束语法)：

   ```
   alter table products alter column product_no SET NOT NULL;
   ```

4. **删除表约束**

   要删除一个约束，你需要知道它的名字。如果你曾经给了它取了名字， 那么事情就很简单。否则你就需要找出系统自动分配的名字。psql 的命令`\d tablename`可以帮这个忙； 其它接口可能也提供了检查表的细节的方法。然后就是这条命令：

   ```
   alter table products DROP CONSTRAINT some_name;
   ```

   除了非空约束外，所有约束类型都这么用。要删除非空约束，可以这样：

   ```
   alter table products ALTER COLUMN product_no DROP NOT NULL;
   ```

   要记得非空约束没有名字。

5. **改变字段约束**

   设置：

   ```
   alter table products ALTER COLUMN price SET DEFAULT 7.77;
   ```

   删除：

   ```
   alter table products ALTER COLUMN price DROP DEFAULT;
   ```

6. **修改字段数据类型**

   把一个字段转换成另外一种数据类型，使用下面的命令：

   ```
   alter table products ALTER COLUMN price TYPE numeric(10,2);
   ```

   只有在字段里现有的每个项都可以隐含的转换成新类型时才可能成功。 如果需要更复杂的转换，你可以增加一个`USING`子句，它声明如何从旧值里计算新值。

7. **重命名字段**

   重命名一个字段：

   ```
   alter table products RENAME COLUMN product_no TO product_number;
   ```

8. **重命名表**

   重命名一个表：

   ```
   alter table products RENAME TO items;
   ```





---

#### [返回目录](./)

