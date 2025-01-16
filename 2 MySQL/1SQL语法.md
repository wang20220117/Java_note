[TOC]







# 数据库分类

关系型数据库（SQL）

* MySQL、Oracle、Sql Server
* 通过表和表之间，行和列之间的关系进行数据的存储。

非关系型数据库

* Redis
* 利用对象存储，通过对象自身的属性来决定。

DBMS

* 数据库管理系统



> MySQL 是一个实现了 SQL 标准的关系型数据库管理系统，它提供了用于操作和管理数据的功能，而 SQL 是用于描述这些操作的语言。几乎所有的关系型数据库系统，无论是开源的如 MySQL、PostgreSQL，还是商业的如 Oracle Database、Microsoft SQL Server，都支持 SQL 作为其主要的交互语言。





sqlyog：数据库管理工具



==mysql安装教程：==

[MYSQL压缩包方式的安装与卸载（一步步超详细）_mysql压缩包安装卸载教程-CSDN博客](https://blog.csdn.net/I_need_your_help/article/details/107294394)



常用命令：

```sql
net stop mysql    //关闭mysql

net start mysql   //启动mysql

mysql -u root -p  //登录mysql
```



==SQL语法：==

[CS-Notes/notes/SQL 语法.md at master · CyC2018/CS-Notes (github.com)](https://github.com/CyC2018/CS-Notes/blob/master/notes/SQL 语法.md#一基础)



数据库->数据库中的表->数据库表中的字段

# 定义数据库对象（数据库、表、字段）

## DDL 数据库定义语言

*用来定义数据库对象（数据库、表、字段）*

 ![img](D:\md_image\f33446caa8c4418bab4bce1af0ca0827.png)

* 创建表：

```sql
CREATE TABLE mytable(
	id int,
	name VARCHAR(45),
	gender VARCHAR(1),
	PRIMARY KEY (`id`)
);

```

* 删除表：

```sql
DROP TABLE mytable;
```

* 使用`DESC mytable; ` 查看表的结构：

 ![image-20240715110903414](D:\md_image\image-20240715110903414.png)

 

* `SHOW CREATE TABLE 表名;` 返回一个包含了创建指定表的SQL语句的结果集。这个语句显示了创建表时使用的所有选项，包括列的定义、索引、约束、分区等信息。

* `ALTER TABLE 表名` 是一个SQL命令，用于修改现有数据库表的结构或其他属性。通过 `ALTER TABLE` 命令，可以执行多种操作，如添加、修改或删除列，添加或删除索引，修改表的存储引擎和字符集，以及进行其他结构调整。
  * 添加列
  * 修改列
  * 删除列
  * 添加主键
  * 添加外键
  * 修改表名称
  * 修改表的存储引擎
  * 修改表的字符集



常用命令：

 ![image-20240715164625733](D:\md_image\image-20240715164625733.png)





## 数据库的列类型

 ![image-20240715160516076](D:\md_image\image-20240715160516076.png)

 ![image-20240715160735000](D:\md_image\image-20240715160735000.png)

 ![image-20240715161050614](D:\md_image\image-20240715161050614.png)

 ![image-20240715161128542](D:\md_image\image-20240715161128542.png)

## 数据库的字段属性（重点）

 ![image-20240715161750374](D:\md_image\image-20240715161750374.png)

 ![image-20240715161811307](D:\md_image\image-20240715161811307.png)

SQL 中，反引号 `` `（也称为backtick）通常用于标识数据库对象（如表名、列名）的标识符，特别是在需要区分关键字或保留字的情况下，或者在对象名包含特殊字符时使用。

主要用途包括：

1. **标识符的引用**：在 SQL 中，反引号用于引用包含特殊字符或空格的数据库对象名。例如，如果你的表名是 `user info`，那么可以用反引号括起来：``user info``。
2. **保留字或关键字的使用**：有时候*数据库对象的名称与 SQL 关键字相同或类似，使用反引号可以避免歧义*。
3. **跨数据库兼容性**：某些数据库系统（如MySQL）要求使用反引号来引用对象名，而其他数据库系统（如PostgreSQL、SQL Server）可能使用双引号或方括号。反引号的使用使得 SQL 语句在不同数据库系统中具有一定的兼容性。



在 SQL 语言中，单引号 `' '` 用来表示==字符串字面值==（String Literal）。字符串字面值是用来表示文本数据的方式，在单引号内包裹着具体的文本内容。

在 SQL 查询中，使用单引号将字符串括起来是非常重要的，因为它告诉数据库解析器如何区分文本数据和 SQL 查询语句中的关键字或标识符。



## 数据表的类型

数据库引擎：

 ![image-20240715165850284](D:\md_image\image-20240715165850284.png)



## 修改和删除数据表字段

 ![image-20240715170533215](D:\md_image\image-20240715170533215.png)



`modify` 用来修改字段的类型和约束；

`change` 用来重命名字段名



# MySQL数据管理

## 外键（了解即可）

创建外键约束：

==在定义表时创建：==

```sql
--表A
CREATE TABLE TableA (
    id INT PRIMARY KEY,
    ...
);

--表B
CREATE TABLE TableB (
    id INT PRIMARY KEY,
    tableA_id INT,
    CONSTRAINT fk_student_id FOREIGN KEY (tableA_id) REFERENCES TableA(id)
);
```

定义表时创建外键时，可以选择使用 `CONSTRAINT` 关键字为外键约束指定一个名称。这种命名可以帮助提高代码的可维护性和错误处理能力，同时使数据库结构更加清晰和易于管理。

==使用语句创建：==

1. **创建表B**：首先，确保表B已经存在，并且包含一个用于存储外键的列（例如 `tableA_id`）。

2. **添加外键约束**： 使用 `ALTER TABLE` 语句添加外键约束，如下所示：

   ```sql
   ALTER TABLE TableB
   ADD CONSTRAINT fk_tableA_id
   FOREIGN KEY (tableA_id) REFERENCES TableA(id);
   ```

   - `fk_tableA_id` 是外键约束的名称，可以根据你的命名习惯进行调整。
   - `FOREIGN KEY (tableA_id)` 指定了在表B中的外键列。
   - `REFERENCES TableA(id)` 指定了外键引用的目标表和目标列。



***在实际开发中不推荐使用外键。***



## DML（数据库操作语言）      

*用来对数据库表中的数据（**操作行**）进行增删改查*

* insert
* update
* delete

### 插入

普通插入：

```sql
INSERT INTO mytable(col1, col2) VALUES(val1, val2);
```

主键由于自增可以省略。



### 修改/更新

```sql
UPDATE mytable
SET col = val
WHERE id = 1;   --val可以是变量，不一定是具体的值
```

WHERE 用于条件过滤

条件语句，在a和b之间：

* WHERE `id` BETWEEN a AND b

* AND  多个条件并列

* OR

## 删除

```sql
DELETE FROM mytable
WHERE id = 1;
```

**TRUNCATE TABLE** 可以清空表，也就是删除所有行。表的结构和索引约束不会变。

```sql
TRUNCATE TABLE mytable;
```



> DELETE 和 TRUNCATE 清空表的区别
>
> * 相同点：都能清空表，都不会删除表的结构。
> * 不同：
>   * TRUNCATE 重新设置 自增列 计数器会归0
>   * TRUNCATE 不会影响事务
>   *  ![image-20240716111301277](D:\md_image\image-20240716111301277.png)



# DQL 查询数据（最重点）

* 关键词 Select
* 数据库中最核心的语句

 ![image-20240717155330575](D:\md_image\image-20240717155330575.png)



```sql
SELECT `字段1`,`字段2`
FROM `表名`;
```

起别名：

```sql
SELECT `字段1` AS 别名1 ,`字段2` AS 别名2
FROM `表名`;
```

**CONCAT**函数

 ![image-20240716143900879](D:\md_image\image-20240716143900879.png)



**DISTINCT** 去重

```sql
SELECT DISTINCT col1, col2
FROM mytable;
```

相同值只会出现一次。它作用于所有列，也就是说所有列的值都相同才算相同。



**LIMIT**

限制返回的行数。可以有两个参数，第一个参数为起始行，从 0 开始；第二个参数为返回的总行数。

返回前 5 行：

```sql
SELECT *
FROM mytable
LIMIT 5;
```



```sql
SELECT *
FROM mytable
LIMIT 0, 5;
```



返回第 3 ~ 5 行：

```sql
SELECT *
FROM mytable
LIMIT 2, 3;
```



## **WHERE 查询过滤**

```sql
SELECT *
FROM mytable
WHERE col IS NULL;
```

 ![image-20240716144559207](D:\md_image\image-20240716144559207.png)

应该注意到，NULL 与 0、空字符串都不同。

**AND 和 OR** 用于连接多个过滤条件。优先处理 AND，当一个过滤表达式涉及到多个 AND 和 OR 时，可以使用 () 来决定优先级，使得优先级关系更清晰。

**IN** 操作符用于匹配一组值，其后也可以接一个 SELECT 子句，从而匹配子查询得到的一组值。

**NOT** 操作符用于否定一个条件。



## 通配符模糊查询

通配符也是用在过滤语句中，但它只能用于文本字段。

- **%** 匹配 >=0 个任意字符；
- **_** 匹配 ==1 个任意字符；
- **[ ]** 可以匹配集合内的字符，例如 [ab] 将匹配字符 a 或者 b。用脱字符 ^ 可以对其进行否定，也就是不匹配集合内的字符。

使用 **Like** 来进行通配符匹配。

```sql
SELECT *
FROM mytable
WHERE col LIKE '[^AB]%'; -- 不以 A 和 B 开头的任意文本
```



模糊查询本质是 比较运算符

 ![image-20240716145424332](D:\md_image\image-20240716145424332.png)

## 联表查询 Join on

联表查询（Join）是SQL中一种重要的操作，用于在多个表之间根据指定的条件关联数据。在联表查询中，常见的一种方式是使用 `ON` 关键字来指定连接条件，这种形式被称为 `JOIN ON`。连接查询

**示例：**

假设我们有两个表 `orders` 和 `customers`，它们的结构如下：

**`orders` 表**：

| order_id | customer_id | order_date | amount |
| -------- | ----------- | ---------- | ------ |
| 1        | 101         | 2024-07-15 | 150.00 |
| 2        | 102         | 2024-07-16 | 200.00 |
| 3        | 101         | 2024-07-16 | 100.00 |

**`customers` 表**：

| customer_id | customer_name | city     |
| ----------- | ------------- | -------- |
| 101         | John Doe      | New York |
| 102         | Jane Smith    | San Jose |

现在，我们想要获取每个订单的详细信息，包括客户的名称和订单金额，可以使用联表查询：

```sql
SELECT orders.order_id, customers.customer_name, orders.amount
FROM orders
JOIN customers ON orders.customer_id = customers.customer_id;   --就是INNER JOIN
```

ON 后面跟条件。

在这个例子中：

- `orders` 和 `customers` 是要连接的两个表。
- `ON orders.customer_id = customers.customer_id` 指定了连接条件，即 `orders` 表中的 `customer_id` 列与 `customers` 表中的 `customer_id` 列相匹配。

**结果：**

| order_id | customer_name | amount |
| -------- | ------------- | ------ |
| 1        | John Doe      | 150.00 |
| 2        | Jane Smith    | 200.00 |
| 3        | John Doe      | 100.00 |

这条查询的结果是一个包含了订单编号、客户姓名和订单金额的表格，其中客户姓名来自于关联的 `customers` 表，通过 `customer_id` 来连接两个表。

 ![image-20240717153648125](D:\md_image\image-20240717153648125.png)



***连接可以替换子查询，并且比子查询的效率一般会更快。***

可以用 AS 给列名、计算字段和表名取别名，给表名取别名是为了简化 SQL 语句以及连接相同表。





## 自连接

在SQL中，自连接是指查询中使用同一张表的多个实例（或称为别名）。自连接通常用于需要将表中的数据与其自身进行比较或连接的情况。

假设有一个名为 `employees` 的表，结构如下：

```sql
sqlCopy CodeCREATE TABLE employees (
    id INT PRIMARY KEY,
    name VARCHAR(100),
    manager_id INT
);

INSERT INTO employees (id, name, manager_id) VALUES
(1, 'Alice', NULL),
(2, 'Bob', 1),
(3, 'Charlie', 2),
(4, 'David', 1),
(5, 'Eve', 2);
```

这个表存储了员工的信息，其中 `manager_id` 指向该员工的直接上级（如果有的话）。现在，如果我们想要查询每个员工及其直接上级的姓名，可以使用自连接来实现。

示例查询

```sql
SELECT 
    e.name AS employee_name,
    m.name AS manager_name
FROM 
    employees e
LEFT JOIN 
    employees m ON e.manager_id = m.id;
```

这个查询的含义是，从 `employees` 表中选择员工的姓名（使用别名 `e`）和他们的上级的姓名（使用别名 `m`）。`LEFT JOIN` 用于连接 `employees` 表的两个实例，条件是员工的 `manager_id` 等于上级的 `id`。这样，我们就可以得到每个员工及其直接上级的信息。

自连接的注意事项

- **别名使用**：为了区分同一张表中的多个实例，在自连接中必须使用表的别名。
- **性能考虑**：自连接可能会影响查询性能，特别是在处理大量数据时。因此，应该注意优化查询。
- **多级连接**：如果需要连接多层次的关系（如员工的直接上级、间接上级等），可以多次使用自连接或者考虑使用递归查询（在支持递归的数据库系统中）。

通过上述示例，你可以了解SQL中自连接的基本用法和实现方式。

## 分页和排序

**limit** 和 **order by**



limit 见上文

排序：

- **ASC** ：升序（默认）
- **DESC** ：降序

可以按多个列进行排序，并且为每个列指定不同的排序方式：

```sql
SELECT *
FROM mytable
ORDER BY col1 DESC, col2 ASC;
```



## 子查询

子查询（Subquery），又称为内查询（Inner Query）或嵌套查询（Nested Query），是指在一个查询语句中嵌套的另一个查询。子查询通常用于检索基于其他查询结果的数据。子查询可以出现在 `SELECT`、`INSERT`、`UPDATE` 或 `DELETE` 语句的 `WHERE` 子句、`FROM` 子句或 `HAVING` 子句中。



## 计算字段

在数据库服务器上完成数据的转换和格式化的工作往往比客户端上快得多，并且转换和格式化后的数据量更少的话可以减少网络通信量。

计算字段通常需要使用 **AS** 来取别名，否则输出的时候字段名为计算表达式。

```sql
SELECT col1 * col2 AS alias
FROM mytable;
```

**CONCAT()** 用于连接两个字段。许多数据库会使用空格把一个值填充为列宽，因此连接的结果会出现一些不必要的空格，使用 **TRIM()** 可以去除首尾空格。

```sql
SELECT CONCAT(TRIM(col1), '(', TRIM(col2), ')') AS concat_col
FROM mytable;
```



## 函数（聚合函数）

SQL中的聚合函数（Aggregate Functions）用于对一组值进行计算并返回一个单一的值。这些函数通常与`GROUP BY`子句一起使用，用于在进行分组操作时进行各种统计计算。常见的聚合函数包括：

以下主要是 MySQL 的函数。

 ![image-20240717161710739](D:\md_image\image-20240717161710739.png)

AVG() 会忽略 NULL 行。



==文本处理函数==



==日期和时间处理函数==

处理类型为data的列！

 ![image-20240719110529848](D:\md_image\image-20240719110529848.png)

==数值处理函数==



## 分组过滤

分组和过滤主要通过 `GROUP BY` 和 `HAVING` 子句实现。

where 过滤行，group by对过滤后的行进行分组，having再对分好的组进行过滤。

因此分组规定：

> - GROUP BY 子句出现在 WHERE 子句之后，ORDER BY 子句之前；
> - 除了汇总字段外，SELECT 语句中的每一字段都必须在 GROUP BY 子句中给出;
> - NULL 的行会单独分为一组；

示例：

 ![image-20240717163722414](D:\md_image\image-20240717163722414.png)

## select小结

 ![image-20240717155330575](D:\md_image\image-20240717155330575.png)

# 事务

- 事务（transaction）指一组 SQL 语句；
- 回退（rollback）指撤销指定 SQL 语句的过程；
- 提交（commit）指将未存储的 SQL 语句结果写入数据库表；*（持久化）*
- 保留点（savepoint）指事务处理中设置的临时占位符（placeholder），你可以对它发布回退（与回退整个事务处理不同）。



数据库事务原则：ACID原则 原子性（atom）、一致性（consistency）、隔离性（isolate）、持久性（durable）

*mysql是默认开启事务自动提交的。*

```sql
SET autocommit = 0    -- 关闭事务自动提交
SET autocommit = 1    -- 开启事务自动提交
```

设置 autocommit 为 0 可以取消自动提交；autocommit 标记是针对每个连接而不是针对服务器的。



```sql
START TRANSACTION       -- 事务开启
// ...
SAVEPOINT delete1       -- 设置保存点
// ...
ROLLBACK TO delete1     -- 回退
// ...
COMMIT                  -- 提交
```

>  如果没有设置保留点，ROLLBACK 会回退到 START TRANSACTION 语句处；如果设置了保留点，并且在 ROLLBACK 中指定该保留点，则会回退到该保留点。



MySQL 的事务提交默认是隐式提交，每执行一条语句就把这条语句当成一个事务然后进行提交。当出现 START TRANSACTION 语句时，会关闭隐式提交；当 COMMIT 或 ROLLBACK 语句执行后，事务会自动关闭，重新恢复隐式提交。

# 索引

索引的分类

* 主键索引 （primary key）
  * 唯一的标识，主键不可重复。
* 唯一索引 （unique key）
  * 避免重复的列出现，唯一索引可以重复，多个列都可以标识为唯一索引。
* 常规索引 （key / index）
  * 默认的，index，key关键字来设置
* 全文索引 （FullText）
  * 在特定的数据库引擎下才有



**普通索引可重复，唯一索引和主键一样不能重复。**

一张表里面只能有一个主键，不能为空，唯一索引可有多个。唯一索引可有一条记录为null。



增加主键索引、唯一索引、常规索引的方法。

创建主键约束：

```sql
-- 或者在已有表上添加主键
ALTER TABLE users
    ADD PRIMARY KEY (user_id);
```

```sql
-- 创建表时设置主键
CREATE TABLE mytable(
	id int,
	name VARCHAR(45),
	gender VARCHAR(1),
	PRIMARY KEY (`id`)
);
```

创建唯一索引：

```sql
CREATE UNIQUE INDEX uk_users_name ON t_users(name); 
```

***ON t_users(name)**: 指定了要在哪个表的哪一列上创建索引。具体地，`ON t_users(name)` 表示在 `t_users` 表的 `name` 列上创建索引。*



创建普通索引：

```sql
CREATE INDEX idx_last_name ON employees(last_name);
```

使用索引进行查询：

```sql
SELECT * FROM employees WHERE last_name = 'Smith';
```

查看索引：

```sql
SHOW INDEXES FROM employees;
```

删除索引：

```sql
DROP INDEX idx_last_name ON employees;
```

组合索引：

组合索引是指在多个列上创建的索引，可以加速涉及这些列的查询。例如，创建一个在 `first_name` 和 `last_name` 列上的组合索引：

````sql
CREATE INDEX idx_name ON employees(first_name, last_name);
````

组合索引查询示例：

```sql
SELECT * FROM employees WHERE first_name = 'John' AND last_name = 'Doe';
```



**索引原则：**

* 索引不是越多越好。
* 不要对进程变动数据加索引。
* 小数据量的表不需要加索引。
* 索引一般加在常用来查询的字段上



[MySQL索引背后的数据结构及算法原理](https://blog.codinglabs.org/articles/theory-of-mysql-index.html)（面试用）

# 数据库三大范式

1. 原子性：列不可再分
2. 数据库表中每一列都和主键相关，而不能只与主键的某一部分相关。
3. 确保数据表中的每一列数据都和主键直接相关，而不能间接相关。
