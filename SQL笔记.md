# SQL基础知识

在关系型数据库管理系统（RDBMS）中，数据库是一个包含多个表（tables）的数据集合。表是数据库中的基本组织单位，用于存储特定类型的数据。每个表包含若干行和列，每一行代表表中的一个记录，而每一列代表记录中的一个属性或字段。

1. **表（Tables）：**
   - 表是数据库中的基本结构，用于存储数据。每个表包含多个列，每一列代表一个属性或字段，每一行代表一个记录。
   - 表是关系型数据库中的核心概念，它们用于组织和存储数据。
2. **视图（Views）：**
   - 视图是基于一个或多个表的查询结果，它不是实际存储数据的结构，而是一个虚拟表。
   - 视图允许用户以一定的角度和条件看待数据库中的数据，它简化了复杂查询的操作，并且可以提供更高层次的安全性，因为你可以限制用户只能访问特定的数据集。
3. **存储过程（Stored Procedures）：**
   - 存储过程是一组预编译的SQL语句集合，它们可以被存储在数据库中，并且可以像函数一样被调用。
   - 存储过程通常用于实现特定的业务逻辑，可以接受参数、执行SQL语句、进行流程控制等。存储过程的使用可以提高数据库的性能和安全性，因为它们减少了重复的SQL语句的执行次数，同时也可以控制用户对数据库的操作权限。
4. **函数（Functions）：**
   - 函数是一组预定义的逻辑操作，用于返回单一值或表达式的计算结果。
   - 在数据库中，函数可以用于各种目的，例如数学计算、字符串操作、日期操作等。数据库管理系统通常提供了很多内置函数，同时也允许用户创建自定义函数以满足特定需求。

**总结：表是数据库中存储数据的基本结构，视图提供了数据的逻辑展示，存储过程是一组预定义的操作集合，函数用于计算和数据处理。这些结构和功能共同构成了关系型数据库管理系统中的基本元素，用于组织、存储和操作数据。**

## 一.选择语句

### 1.USE语句

`USE`语句是SQL语言中的一种用法，它用于在关系型数据库管理系统中选择要操作的数据库。具体地说，`USE`语句用于切换当前会话到指定的数据库，之后所有的SQL操作都将在该数据库上执行。

例如，如果你有一个数据库叫做`sql_store`，你可以使用`USE`语句切换到这个数据库：

```
USE sql_store;
```

在执行这个语句后，所有的后续SQL查询和操作都将在`sql_store`数据库上执行。这样，你不再需要每次在SQL语句中指定数据库的名称，系统会默认在`sql_store`数据库上执行操作。

请注意，使用`USE`语句切换数据库之后，除非你再次使用`USE`语句切换到其他数据库，否则当前会话将一直在指定的数据库上操作，即使你关闭了连接再重新连接数据库服务器，也是如此。

需要注意的是，在执行`USE`语句时，确保指定的数据库名称是存在的，否则会出现错误。

### 2.SELECT语句

`SELECT`语句是SQL中用于从数据库中检索数据的基本语句。它允许你指定要返回的列、表、以及一些可选的条件和排序规则。以下是`SELECT`语句的详细语法：

```
SELECT 列名1, 列名2, ...
FROM 表名
WHERE 条件表达式
ORDER BY 列名 [ASC|DESC];
```

- `列名1, 列名2, ...`：要从数据库中检索的列的名称。可以是一个或多个列名，用逗号分隔，或者使用通配符 `*` 表示选择所有列。
- `表名`：要从中检索数据的表的名称。
- `WHERE`（可选）：用于指定过滤条件，只有满足条件的行才会被检索出来。可以使用比较运算符（例如 `=`, `<`, `>`, `<=`, `>=`）和逻辑运算符（例如 `AND`, `OR`, `NOT`）来构建条件表达式。
- `ORDER BY`（可选）：用于对结果集进行排序。你可以指定一个或多个列的名称，以及可选的排序顺序。默认情况下，排序是升序的（ASC），如果需要降序排序，可以使用 `DESC` 关键字。

以下是一些具体的示例：

1. **选择所有列的数据：**

   ```
   SELECT * FROM 表名;
   ```

2. **选择特定列的数据：**

   ```
   SELECT 列名1, 列名2 FROM 表名;
   ```

3. **带有条件的查询：**

   ```
   SELECT 列名 FROM 表名 WHERE 列名 = 值;
   ```

4. **排序查询结果：**

   ```
   SELECT 列名 FROM 表名 ORDER BY 列名 ASC; -- 升序排序
   SELECT 列名 FROM 表名 ORDER BY 列名 DESC; -- 降序排序
   ```

5. **使用逻辑运算符的条件查询：**

   ```
   SELECT 列名 FROM 表名 WHERE 列名 > 值1 AND 列名 < 值2;
   ```

6. **使用通配符进行模糊查询：**

   ```
   SELECT 列名 FROM 表名 WHERE 列名 LIKE '部分字符串%';
   ```

以上是`SELECT`语句的基本用法，你可以根据实际需求和条件，组合使用不同的操作符和关键字来编写更复杂的查询语句。



#### 例一

```
SELECT 
    last_name,
    first_name,
    points,
    (points + 10) *100 AS 'discount factor'
FROM customers
```

解释一下每个部分：

- `last_name`：选择`customers`表中的`last_name`列。
- `first_name`：选择`customers`表中的`first_name`列。
- `points`：选择`customers`表中的`points`列。
- `(points + 10) * 100`：这是一个计算表达式，对`points`列的值加上10，然后乘以100。
- `AS 'discount factor'`：用于给计算得到的新列指定一个别名，即`discount factor`，在结果集中会显示这个别名作为新列的标题。



#### 例二

```
SELECT DISTINCT state  
FROM customers
```

如果有一个名为`customers`的表，其中包含一个列名为`state`的列，执行上述SELECT语句后，将会返回`state`列中的不同州名称，且每个州名称只会出现一次，去重后的结果。即去除了重复的值。执行这个查询将返回`customers`表中不同的州（state）列表。



### 3.WHERE字句

```
SELECT *
FROM Customers
WHERE birth_date > '1990-1-1'
```

`WHERE`：用于指定条件表达式。只有满足条件的行才会被返回。可以使用比较运算符（例如 `=`, `<`, `>`, `<=`, `>=`）和逻辑运算符（例如 `AND`, `OR`, `NOT`）来构建条件表达式。

1. **等值比较：**

   ```
   SELECT 列名 FROM 表名 WHERE 列名 = 值;
   ```

2. **不等值比较：**

   ```
   SELECT 列名 FROM 表名 WHERE 列名 <> 值;
   ```

3. **范围比较：**

   ```
   SELECT 列名 FROM 表名 WHERE 列名 BETWEEN 值1 AND 值2;
   ```

4. **空值检查：**

   ```
   SELECT 列名 FROM 表名 WHERE 列名 IS NULL;
   ```

5. **逻辑操作符：**

   ```
   SELECT 列名 FROM 表名 WHERE 列名 > 值1 AND 列名 < 值2;
   ```

6. **模糊查询：**

   ```
   SELECT 列名 FROM 表名 WHERE 列名 LIKE '部分字符串%';
   ```



#### and的优先级

```
SELECT * 
FROM customers 
WHERE birth_date > '1990-1-1' OR points > 1000 AND state = 'VA';
```

根据这个查询，结果集将包括满足以下条件之一的行：

- 出生日期在 '1990-1-1' 之后的行
- 积分大于 1000 并且州名等于 'VA' 的行

如果某行同时满足两个条件，它也会出现在结果中。这个查询将返回符合这些条件的行的所有列。

**AND 操作符的优先级高于 OR 操作符。因此，查询会先挑选出满足 `points > 1000 AND state = 'VA'` 条件的行，然后再从这个结果集中挑选出满足 `birth_date > '1990-1-1'` 条件的行。**



#### not

```
SELECT * 
FROM customers 
WHERE NOT (birth_date > '1990-1-1' OR points > 1000 ) 
```

在这里面的 NOT 可以这么表示     **WHRER  birth_date <= '1990-1-1' AND point <= 1000**

注意:  使用NOT时直接把 **OR **该成了 **AND**



#### in 和 not in

在SQL中，`IN`和`NOT IN`是用于筛选某列值是否在指定值列表中或不在指定值列表中的条件表达式。在你提供的两个查询中，使用了`IN`和`NOT IN`来筛选`state`列是否在指定的州（"VA", "GA", "FL"）列表中或不在该列表中。

1. **使用`IN`：**

```
SELECT * FROM customers
WHERE state IN ("VA", "GA", "FL");
```

上述查询会选择`state`列的值在("VA", "GA", "FL")列表中的行，返回满足条件的所有列。

1. **使用`NOT IN`：**

```
SELECT * FROM customers
WHERE state NOT IN ("VA", "GA", "FL");
```

上述查询会选择`state`列的值不在("VA", "GA", "FL")列表中的行，返回满足条件的所有列。

这两个查询可以帮助你过滤出在指定州列表中或不在指定州列表中的客户数据。`IN`和`NOT IN`是非常方便的操作符，用于简化包含多个等值条件的查询。



#### between ...and...

```
SELECT *
FROM customers 
WHERE points BETWEEN 1000 AND 3000
```

这里的 **WHERE points BETWEEN 1000 AND 3000**  类似于 **WHERE points >=1000 AND point <=3000**



#### like

```
SELECT *
FROM customers
WHERE last_name LIKE "b%"
WHERE last_name LIKE "%b%"
WHERE last_name LIKE "%y"
WHERE last_name LIKE "b____y"
```

在SQL中，`LIKE`操作符用于进行模糊查询，其中`%`代表零个或多个字符，`_`代表一个字符。你的查询尝试使用了不同的模式匹配来选择`last_name`列的值。

请注意，这些查询使用的模式是区分大小写的，这意味着它们会区分大写和小写字母。如果你希望不区分大小写，你可以在查询中使用`LOWER()`或`UPPER()`函数来规范化比较，或者在数据库的配置中设置不区分大小写的规则。



#### 在 SQL 中，逻辑操作符需要两个完整的条件表达式进行比较。

```
SELECT *
FROM customers
WHERE address LIKE "%trail%" OR 
      address LIKE "%avenue%" 
```



#### 正则表达式 REGEXP	

在SQL中，正则表达式（Regular Expression）是一种用于在文本数据中进行模式匹配的强大工具。MySQL支持使用`REGEXP`关键字进行正则表达式匹配。以下是一些基本的用法和示例：

**基本正则表达式匹配**

```
SELECT * FROM table_name WHERE column_name REGEXP 'pattern';
```

在这个查询中，`column_name` 是你希望匹配的列的名称，`pattern` 是一个正则表达式模式。

当在正则表达式中使用特定的字符和语法时，它们具有特定的含义和功能。以下是一些常用的正则表达式元字符和语法的解释：

1. `^`（脱字符）：匹配字符串的开始。例如，`^A`会匹配以字母 "A" 开头的字符串。
2. `$`（美元符号）：匹配字符串的结束。例如，`ing$`会匹配以 "ing" 结尾的字符串。
3. `|`（竖线或管道符号）：逻辑或操作符。用于匹配多个模式中的任何一个。例如，`apple|orange`会匹配包含 "apple" 或 "orange" 的字符串。
4. `[]`（字符类）：匹配括号内的任意一个字符。例如，`[ad]`会匹配 "a" 或 "d"。
5. `[a-f]`：字符范围。匹配指定范围内的任意一个字符，例如，`[a-f]`会匹配小写字母 "a" 到 "f" 之间的任意一个字符。

**例子**

```
SELECT *
FROM customers
WHERE first_name REGEXP 'elka|ambur'
WHERE first_name REGEXP 'ey$|on$'
WHERE first_name REGEXP '^my$|se'
WHERE first_name REGEXP 'e[ru]'
```



#### null运算符

在SQL中，`NULL` 是一个特殊的值，表示缺失或未知的数据。`NULL` 值通常用于表示某一列的数据在插入时未提供值，或者在查询时无法确定具体的值。在处理 `NULL` 值时，可以使用 `IS NULL` 和 `IS NOT NULL` 运算符来检查列中是否包含 `NULL` 值。

1. **`IS NULL` 运算符：**

`IS NULL` 运算符用于检查某一列的值是否为 `NULL`。

```
SELECT * FROM table_name WHERE column_name IS NULL;
```

上述查询会返回表 `table_name` 中列 `column_name` 包含 `NULL` 值的所有行。

1. **`IS NOT NULL` 运算符：**

`IS NOT NULL` 运算符用于检查某一列的值是否不为 `NULL`。

```
SELECT * FROM table_name WHERE column_name IS NOT NULL;
```

上述查询会返回表 `table_name` 中列 `column_name` 不包含 `NULL` 值的所有行。

这些运算符用于处理数据库中可能存在的 `NULL` 值，使得你可以根据列中的数据是否为 `NULL` 来筛选出符合条件的行。



#### order by 运算符

`ORDER BY` 子句用于对查询结果进行排序。通过 `ORDER BY` 子句，你可以指定一个或多个列来作为排序的依据，以及指定排序的顺序（升序或降序）。

基本语法如下：

```
SELECT 列1, 列2, ...
FROM 表名
ORDER BY 列1 [ASC|DESC], 列2 [ASC|DESC], ...;
```

- `列1, 列2, ...`：要选择的列的名称，可以是一个或多个列，用逗号分隔，或者使用通配符 `*` 表示选择所有列。
- `表名`：要从中选择数据的表的名称。
- `ORDER BY`：用于指定排序的列和排序顺序。默认情况下，排序是升序（从小到大）的，如果你希望降序排序（从大到小），可以使用 `DESC` 关键字。如果不指定排序顺序，默认为升序。

以下是一些示例：

1. **按单列排序：**

```
SELECT * FROM employees
ORDER BY last_name ASC;
```

上述查询将返回 `employees` 表中的所有行，按照 `last_name` 列的升序顺序进行排序。

1. **按多列排序：**

```
SELECT * FROM products
ORDER BY category_id ASC, price DESC;
```

上述查询将返回 `products` 表中的所有行，首先按照 `category_id` 列的升序顺序排序，然后在同一 `category_id` 下，按照 `price` 列的降序顺序排序。

`ORDER BY` 子句非常有用，它可以帮助你将查询结果按照特定的顺序呈现，使数据更容易阅读和分析

**例子**

```
SELECT *, quantity * unit_price AS total_price
FROM order_items
WHERE order_id = 2
ORDER BY total_price DESC
```



#### limit字句

`LIMIT` 子句用于限制查询结果的行数。你可以使用 `LIMIT` 子句来指定返回的记录数，从而控制查询结果集的大小。基本语法如下：

```
SELECT 列1, 列2, ...
FROM 表名
LIMIT 行数;
```

或者，你还可以指定从哪一行开始返回，以及返回的行数：

```
SELECT 列1, 列2, ...
FROM 表名
LIMIT 偏移量, 行数;
```

- `列1, 列2, ...`：要选择的列的名称，可以是一个或多个列，用逗号分隔，或者使用通配符 `*` 表示选择所有列。
- `表名`：要从中选择数据的表的名称。
- `LIMIT`：用于指定返回的行数。如果只指定一个值，则表示返回的行数不超过这个值。如果指定两个值（偏移量和行数），则表示从偏移量位置开始返回指定数量的行。

以下是一些示例：

1. **只返回前 N 行：**

```
SELECT * FROM products
LIMIT 10;
```

上述查询将返回 `products` 表中的前 10 行记录。

1. **从偏移量开始返回 N 行：**

```
SELECT * FROM products
LIMIT 5, 10;
```

上述查询将从 `products` 表的第 6 行（偏移量为 5）开始返回 10 行记录。偏移量是从 0 开始计数的。

`LIMIT` 子句非常有用，它可以用于分页查询，或者在大数据集上限制查询结果的大小，提高查询性能。

## 二.连接

### 1.内连接

内连接（Inner Join）是 SQL 中最常用的连接类型之一，它用于从多个表中检索数据，只返回两个表中具有匹配关系的行。内连接基于两个表之间的共同列进行匹配，如果这两个表中的列有相同的值，那么这些行将被返回。

内连接的基本语法如下：

```
SELECT 列1, 列2, ...
FROM 表1
INNER JOIN 表2
ON 表1.共同列 = 表2.共同列;
```

在这个语法中，`表1` 和 `表2` 是要连接的两个表的名称，`共同列` 是两个表中用来匹配的共同列的名称。查询将返回两个表中所有匹配的行，即那些在 `表1` 和 `表2` 中具有相同值的行。

#### 示例：

假设有两个表 `orders` 和 `customers`，它们分别包含订单信息和客户信息，两个表中都有一个名为 `customer_id` 的列，用于匹配订单和客户。

```
SELECT orders.order_id, orders.order_date, customers.customer_name
FROM orders
INNER JOIN customers
ON orders.customer_id = customers.customer_id;
```

上述查询将返回订单表 `orders` 和客户表 `customers` 中匹配的订单信息和客户名。`INNER JOIN` 语句基于 `customer_id` 列的值匹配两个表，并且只返回那些在两个表中都有匹配的 `customer_id` 的行。

内连接通常用于在多个表之间建立关系，它可以帮助你从相关联的表中获取有用的信息。

**注意: 这里的SELECT 后面查询的列如果有重复的，需要指定是那个表格的重复列**

例子

```
SELECT oi.product_id , name ,quantity,p.unit_price
FROM order_items oi
JOIN products p
   ON oi.product_id = p.product_id
```



### 2.跨数据库连接

在MySQL中，通常情况下，一个数据库连接只能连接到一个特定的数据库。但是，有时候我们可能需要在不同的数据库之间进行操作，这时可以使用以下两种方法来实现跨数据库连接：

#### 使用全限定表名（Fully Qualified Table Names）

在一个SQL查询中，你可以使用全限定表名来指定不同数据库中的表。全限定表名的格式为：`database_name.table_name`。例如，如果你想在数据库`db1`中的`table1`表和数据库`db2`中的`table2`表之间进行连接，可以这样写SQL查询：

```
SELECT db1.table1.column_name, db2.table2.column_name
FROM db1.table1
JOIN db2.table2 ON db1.table1.common_column = db2.table2.common_column;
```

在这个例子中，我们使用了全限定表名来指定在不同数据库中的表，然后通过`JOIN`语句将它们连接起来。

​	

### 3.自连接

自连接（Self Join）是指在同一个表中进行连接操作，即将表中的两行数据进行比较和匹配。自连接通常用于处理具有层次结构的数据，例如，一个员工表中包含员工和他们的经理的信息。在这种情况下，你可以使用自连接来查找员工和他们的经理的关系。

以下是一个自连接的基本示例：

假设有一个名为`employees`的表，包含以下列：`employee_id`（员工ID），`employee_name`（员工姓名），`manager_id`（经理ID，指向同一表中的另一个员工ID）。

表结构如下：

```
+-------------+---------------+-------------+
| employee_id | employee_name | manager_id  |
+-------------+---------------+-------------+
| 1           | Alice         | 3           |
| 2           | Bob           | 3           |
| 3           | Charlie       | NULL        |
| 4           | David         | 2           |
+-------------+---------------+-------------+
```

现在，如果你想获取每个员工及其经理的姓名，可以使用自连接的方式：

```
SELECT e1.employee_name AS employee, e2.employee_name AS manager
FROM employees e1
LEFT JOIN employees e2 ON e1.manager_id = e2.employee_id;
```

在这个查询中，`e1`和`e2`是同一个表`employees`的别名，通过`LEFT JOIN`将表与自身连接，比较`e1`的`manager_id`与`e2`的`employee_id`。通过这种方式，你可以获取每个员工及其对应经理的信息。

请注意，如果一个员工没有经理（`manager_id`为`NULL`），那么在使用`LEFT JOIN`时，相关列的值将为`NULL`。

**例子**

```
USE sql_hr;

SELECT 
     e.employee_id,
     e.first_name AS 'employee',
     m.first_name AS 'manager'
FROM employees e
JOIN employees m
    ON e.reports_to = m.employee_id
```





### 4.多表连接

当你需要连接三个或更多表时，你可以使用多个连接操作符来连接这些表。以下是一个连接三张表的基本示例：

假设有三个表：`employees`、`departments`和`projects`，分别包含员工信息、部门信息和项目信息。

**employees表结构：**

```
+-------------+---------------+-------------+
| employee_id | employee_name | department_id|
+-------------+---------------+-------------+
| 1           | Alice         | 1           |
| 2           | Bob           | 2           |
| 3           | Charlie       | 1           |
| 4           | David         | 3           |
+-------------+---------------+-------------+
```

**departments表结构：**

```
+-------------+---------------+
| department_id| department_name|
+-------------+---------------+
| 1           | IT            |
| 2           | Sales         |
| 3           | Marketing     |
+-------------+---------------+
```

**projects表结构：**

```
+-------------+---------------+
| project_id  | project_name  |
+-------------+---------------+
| 1           | Project A     |
| 2           | Project B     |
| 3           | Project C     |
+-------------+---------------+
```

如果你想获取每个员工的姓名、所在部门的名称以及参与的项目名称，你可以使用多个连接操作符：

```
SELECT employees.employee_name, departments.department_name, projects.project_name
FROM employees
JOIN departments ON employees.department_id = departments.department_id
JOIN projects ON employees.employee_id = projects.employee_id;
```

在这个查询中，`employees`表与`departments`表通过`department_id`连接，`employees`表与`projects`表通过`employee_id`连接。这样，你可以获取每个员工的姓名、所在部门的名称以及参与的项目名称。

请注意，确保连接条件在各个表之间能够唯一地确定关联关系，以避免产生不正确的结果。在实际使用中，根据你的数据模型和需求，连接操作符的顺序和连接条件可能会有所不同。



**例子**

```
USE sql_store;

SELECT 
    o.order_id,
    o.order_date,
    c.first_name,
    c.last_name,
    os.name AS 'status'
FROM orders o
JOIN customers c ON o.customer_id = c.customer_id
JOIN order_statuses os ON o.status = os.order_status_id 
```

```
USE invoicing;

SELECT 
    c.client_id AS '客户ID',
    c.name AS '姓名',
    p.date AS '支付时间',
    pm.name AS '支付方式',
    p.amount AS '总计'
FROM payments p 
JOIN clients c 
    ON c.client_id = p.client_id
JOIN payment_methods pm
    ON pm.payment_method_id = p.payment_id
```



### 5.复合连接条件

复合连接条件指的是在多表连接中，使用多个列来建立连接关系，而不仅仅是单个列。这种连接条件通常用于确保连接的唯一性，避免出现不准确或混乱的查询结果。

例如，假设有两个表：`table1` 和 `table2`，它们的结构如下：

**`table1` 表结构：**

```
+---------+---------+
| column1 | column2 |
+---------+---------+
|   A     |   1     |
|   B     |   2     |
|   C     |   3     |
+---------+---------+
```

**`table2` 表结构：**

```
+---------+---------+
| column1 | column3 |
+---------+---------+
|   A     |   X     |
|   B     |   Y     |
|   C     |   Z     |
+---------+---------+
```

如果你想要连接这两个表，并且希望连接条件不仅仅是 `column1` 列的匹配，还希望 `column2` 列和 `column3` 列也匹配，那么你可以使用复合连接条件。例如，你可以这样写查询：

```
SELECT t1.column1, t2.column3
FROM table1 t1
JOIN table2 t2 
ON t1.column1 = t2.column1 AND t1.column2 = t2.column3;
```

在这个查询中，使用了两个连接条件：`t1.column1 = t2.column1` 和 `t1.column2 = t2.column3`。这样确保了只有在 `table1` 和 `table2` 中的这两组列同时匹配的情况下，两个表的行才会连接起来。

复合连接条件的使用可以根据具体的业务需求，结合表的结构和数据关系，选择合适的列组合来确保连接的准确性和唯一性。

**例子**

```
USE sql_store;

SELECT *
FROM order_items oi
JOIN order_item_notes oin
    ON oi.order_id = oin.order_id
    AND oi.product_id = oin.product_id
```

### 6.隐式连接语法


隐式连接是指在 SQL 查询中，不使用显式的 `JOIN` 关键字，而是通过列名进行连接的一种连接方式。隐式连接将两个或多个表中的列名用在 `WHERE` 子句中，以指定连接条件，而不是使用 `JOIN` 关键字明确指明连接关系。

以下是一个使用隐式连接的例子，假设有两个表 `employees` 和 `departments`：

**`employees` 表结构：**

```
+-------------+---------------+-------------+
| employee_id | employee_name | department_id |
+-------------+---------------+-------------+
| 1           | Alice         | 1           |
| 2           | Bob           | 2           |
| 3           | Charlie       | 1           |
+-------------+---------------+-------------+
```

**`departments` 表结构：**

```
+-------------+---------------+
| department_id| department_name |
+-------------+---------------+
| 1           | IT            |
| 2           | Sales         |
+-------------+---------------+
```

你可以使用隐式连接来获取每个员工的姓名和所在部门的名称，查询可以这样写：

```
SELECT employees.employee_name, departments.department_name
FROM employees, departments
WHERE employees.department_id = departments.department_id;
```

在这个查询中，没有使用 `JOIN` 关键字，而是将两个表的列名用在 `WHERE` 子句中，指定了连接条件 `employees.department_id = departments.department_id`。这样的查询方式称为隐式连接。然而，需要注意的是，**隐式连接在可读性上可能没有显式连接清晰，容易引起歧义**，**所以在实际开发中，推荐使用显式连接方式（使用 `JOIN` 关键字）以提高查询的可读性和维护性。**

### 7.外连接

外连接（Outer Join）是一种在两个或多个表之间建立连接关系的方法，它允许你检索左表（左外连接）或右表（右外连接）中的所有行，即使在另一个表中没有相匹配的行。外连接使用 `LEFT JOIN`、`RIGHT JOIN` 或 `FULL OUTER JOIN` 关键字来实现。

1. **左外连接（LEFT JOIN）：** 左外连接返回左表中的所有行，以及右表中与左表中行匹配的行。如果右表中没有匹配的行，结果集中将会包含 NULL 值。

示例：假设有两个表 `employees` 和 `departments`，你想获取所有员工以及他们所在的部门（如果有的话），可以使用左外连接：

```
SELECT employees.employee_name, departments.department_name
FROM employees
LEFT JOIN departments ON employees.department_id = departments.department_id;
```

在这个查询中，`LEFT JOIN` 关键字表示左外连接，它返回所有员工的信息，同时如果有的话，返回他们所在的部门名称。如果员工没有分配到任何部门，`departments.department_name` 列将包含 NULL 值。

1. **右外连接（RIGHT JOIN）：** 右外连接与左外连接相反，它返回右表中的所有行，以及左表中与右表中行匹配的行。如果左表中没有匹配的行，结果集中将会包含 NULL 值。

示例：如果你想获取所有部门以及在这些部门工作的员工（如果有的话），可以使用右外连接：

```
SELECT employees.employee_name, departments.department_name
FROM employees
RIGHT JOIN departments ON employees.department_id = departments.department_id;
```

在这个查询中，`RIGHT JOIN` 关键字表示右外连接，它返回所有部门的信息，同时如果有的话，返回在这些部门工作的员工的姓名。如果没有员工分配到某个部门，`employees.employee_name` 列将包含 NULL 值。

1. **全外连接（FULL OUTER JOIN）：** 全外连接返回左表和右表中的所有行，如果某一边没有匹配的行，结果集中将会包含 NULL 值。

示例：如果你想获取所有员工和所有部门的信息，包括不匹配的部分，可以使用全外连接：

```
SELECT employees.employee_name, departments.department_name
FROM employees
FULL OUTER JOIN departments ON employees.department_id = departments.department_id;
```

在这个查询中，`FULL OUTER JOIN` 关键字表示全外连接，它返回所有员工和部门的信息，如果没有匹配的部分，相应的列将包含 NULL 值。需要注意的是，不是所有的数据库系统都支持 `FULL OUTER JOIN`，因此在使用时需要查阅相应数据库系统的文档。



 **注意:**

- **内连接只返回匹配的行，不包含不匹配的行。**
- 左外连接返回左表的所有行，包括右表中的匹配行，如果没有匹配，右表中的列将包含 NULL 值。
- 右外连接返回右表的所有行，包括左表中的匹配行，如果没有匹配，左表中的列将包含 NULL 值。
- 全外连接返回左表和右表的所有行，不匹配的列将包含 NULL 值。
- **尽量避免使用用右连接，使用左连接**

选择何种连接类型取决于你的查询需求，以及你是否需要包含不匹配的行。



### 8.多表外连接

多表外连接指的是在一个查询中连接三个或更多的表，并且使用外连接（左外连接、右外连接或全外连接）来获取这些表之间的关联数据。在多表外连接中，可以通过使用 `LEFT JOIN`、`RIGHT JOIN`、或 `FULL OUTER JOIN` 关键字来实现外连接操作。

以下是一个使用三个表的左外连接的例子，假设有三个表 `employees`、`departments` 和 `projects`：

**`employees` 表结构：**

```
+-------------+---------------+-------------+
| employee_id | employee_name | department_id |
+-------------+---------------+-------------+
| 1           | Alice         | 1           |
| 2           | Bob           | 2           |
| 3           | Charlie       | 1           |
+-------------+---------------+-------------+
```

**`departments` 表结构：**

```
+-------------+---------------+
| department_id| department_name |
+-------------+---------------+
| 1           | IT            |
| 2           | Sales         |
+-------------+---------------+
```

**`projects` 表结构：**

```
+-------------+-------------+
| project_id  | project_name|
+-------------+-------------+
| 101         | Project A   |
| 102         | Project B   |
+-------------+-------------+
```

如果你希望获取所有员工、所在部门以及参与的项目（如果有的话），你可以使用左外连接：

```
SELECT e.employee_name, d.department_name, p.project_name
FROM employees e
LEFT JOIN departments d ON e.department_id = d.department_id
LEFT JOIN projects p ON e.employee_id = p.employee_id;
```

在这个查询中，使用了两个左外连接，第一个连接将 `employees` 表与 `departments` 表关联，第二个连接将 `employees` 表与 `projects` 表关联。这样可以获取所有员工的信息，包括他们所在的部门和参与的项目（如果有的话），如果没有参与项目，`project_name` 列将包含 NULL 值。

### 9.自外连接 

自外连接（Self Join）是指在同一个表内进行连接操作，即使用表的别名将同一表的两个实例连接在一起。自外连接常用于处理包含自引用关系的数据，例如，一个表中的某一列包含对表中另一行的引用。

以下是一个使用自外连接的简单示例。假设有一个表 `employees` 包含员工信息，其中有两列：`employee_id` 是员工的唯一标识，`manager_id` 是员工的直接上级的 `employee_id`。

**`employees` 表结构：**

```
+-------------+---------------+-------------+
| employee_id | employee_name | manager_id  |
+-------------+---------------+-------------+
| 1           | Alice         | NULL        |
| 2           | Bob           | 1           |
| 3           | Charlie       | 1           |
| 4           | David         | 2           |
+-------------+---------------+-------------+
```

在这个例子中，`manager_id` 列表示员工的上级经理。如果你想要获取每个员工及其直接上级经理的信息，你可以使用自外连接：

```
SELECT e.employee_name AS employee, m.employee_name AS manager
FROM employees e
LEFT JOIN employees m ON e.manager_id = m.employee_id;
```

在这个查询中，`employees` 表被自身连接了两次，使用了两个不同的别名 `e` 和 `m`，分别表示员工和经理。`LEFT JOIN` 关键字表示左外连接，确保所有员工都被包含在结果中，即使他们没有上级经理。结果集将显示每个员工及其直接上级经理的信息，如果没有上级经理，`manager` 列将包含 NULL 值。

这个查询返回的结果可能类似于以下内容：

```
+-----------+-----------+
| employee  | manager   |
+-----------+-----------+
| Alice     | NULL      |
| Bob       | Alice     |
| Charlie   | Alice     |
| David     | Bob       |
+-----------+-----------+
```

在这个结果中，`employee` 列包含员工的名字，`manager` 列包含他们的直接上级经理的名字，如果没有上级经理，则为 NULL。

### 10.USING子句 

在 SQL 中，`USING` 子句是用于指定连接条件的一种方法。它在连接多个表时，可以用来简化连接条件的书写。`USING` 子句指定了两个表之间用于连接的列，这些列在连接的两个表中具有相同的名称。

通常，`USING` 子句用在 `JOIN` 操作中，比如 `INNER JOIN`、`LEFT JOIN`、`RIGHT JOIN` 等。**使用 `USING` 子句可以避免在连接条件中重复列出相同的列名，提高了查询的可读性。**

以下是一个使用 `USING` 子句的示例，假设有两个表 `employees` 和 `departments`，它们都有一个共同的列 `department_id` 用于连接：

**`employees` 表结构：**

```
+-------------+---------------+-------------+
| employee_id | employee_name | department_id|
+-------------+---------------+-------------+
| 1           | Alice         | 1           |
| 2           | Bob           | 2           |
| 3           | Charlie       | 1           |
+-------------+---------------+-------------+
```

**`departments` 表结构：**

```
+-------------+---------------+
| department_id| department_name |
+-------------+---------------+
| 1           | IT            |
| 2           | Sales         |
+-------------+---------------+
```

如果你想要获取每个员工的姓名以及他们所在的部门名称，你可以使用 `USING` 子句进行连接：

```
SELECT employees.employee_name, departments.department_name
FROM employees
INNER JOIN departments USING (department_id);
```

在这个查询中，`USING (department_id)` 指定了连接条件，它告诉数据库系统在连接时使用 `employees` 表和 `departments` 表中共同的 `department_id` 列。这样，数据库会自动根据这个共同的列来进行连接，而不需要在 `ON` 子句中再次指定连接条件。

这个查询将返回每个员工的姓名以及他们所在的部门名称，而不用明确指定连接条件的列。

**例子**

```
USE sql_invoicing;

SELECT 
    date,
    c.name AS clinet,
    amount,
    pm.name AS payment_method
FROM payments p
JOIN clients c
    USING (client_id)
JOIN payment_methods pm
    ON p.payment_method = pm.payment_method_id
```



### 11.自然连接

**不太建议使用**

自然连接是 SQL 中一种特殊的连接操作，它不需要明确指定连接条件，而是根据两个表中具有相同列名的列自动进行连接。自然连接使用 `NATURAL JOIN` 关键字来实现。

在自然连接中，数据库系统会查找两个表中具有相同列名的列，并将这些列用作连接条件，然后返回满足连接条件的行。需要注意的是，自然连接会连接所有具有相同列名的列，而不是只连接一个特定的列。

以下是一个使用自然连接的示例，假设有两个表 `employees` 和 `departments`，它们都有一个共同的列 `department_id` 用于连接：

**`employees` 表结构：**

```
+-------------+---------------+-------------+
| employee_id | employee_name | department_id|
+-------------+---------------+-------------+
| 1           | Alice         | 1           |
| 2           | Bob           | 2           |
| 3           | Charlie       | 1           |
+-------------+---------------+-------------+
```

**`departments` 表结构：**

```
+-------------+---------------+
| department_id| department_name |
+-------------+---------------+
| 1           | IT            |
| 2           | Sales         |
+-------------+---------------+
```

你可以使用自然连接来获取这两个表中具有相同 `department_id` 列名的行：

```
SELECT * FROM employees
NATURAL JOIN departments;
```

在这个查询中，`NATURAL JOIN` 关键字自动根据两个表中相同列名的列 `department_id` 进行连接，返回了满足连接条件的行。查询结果将包含两个表中所有其他列的数据，因为 `department_id` 是连接条件，而不需要再次列出。

需要注意的是，**自然连接可能会带来一些潜在的问题。如果表的结构发生变化，例如增加了新的列，可能会影响到自然连接的结果。**因此，在实际使用中，推荐使用显式指定连接条件的方式（使用 `ON` 子句或 `USING` 子句），以提高查询的可读性和稳定性。

### 12.交叉连接

交叉连接（Cross Join）是 SQL 中一种简单的连接方式，也叫做笛卡尔积。它会返回两个或多个表的所有可能的组合。在交叉连接中，第一个表的每一行都会与第二个表的每一行进行组合，形成新的结果集。

交叉连接并不需要指定连接条件，因此它会返回两个表中的所有行组合。这在某些特殊情况下可能会用到，但是在大多数实际应用中，交叉连接的结果集往往非常庞大，所以使用时需要小心，确保了解它的影响。

以下是一个简单的交叉连接的示例，假设有两个表 `employees` 和 `departments`：

**`employees` 表结构：**

```
+-------------+---------------+
| employee_id | employee_name |
+-------------+---------------+
| 1           | Alice         |
| 2           | Bob           |
+-------------+---------------+
```

**`departments` 表结构：**

```
+-------------+---------------+
| department_id| department_name |
+-------------+---------------+
| 1           | IT            |
| 2           | Sales         |
+-------------+---------------+
```

你可以使用交叉连接获取这两个表的所有可能的组合：

```
SELECT * FROM employees
CROSS JOIN departments;
```

在这个查询中，`CROSS JOIN` 关键字表示交叉连接，它返回了 `employees` 表中每一行与 `departments` 表中每一行的所有可能组合。查询结果将包含所有可能的组合，即笛卡尔积，共有 4 行。

查询结果可能类似于以下内容：

```
+-------------+---------------+-------------+---------------+
| employee_id | employee_name | department_id| department_name |
+-------------+---------------+-------------+---------------+
| 1           | Alice         | 1           | IT            |
| 1           | Alice         | 2           | Sales         |
| 2           | Bob           | 1           | IT            |
| 2           | Bob           | 2           | Sales         |
+-------------+---------------+-------------+---------------+
```

请注意，交叉连接的结果集大小是第一个表的行数乘以第二个表的行数。在实际应用中，如果你需要执行交叉连接，请确保你了解它会生成大量的结果，而且通常情况下不会被广泛使用。

### 13.联合

在SQL中，`UNION`操作用于合并两个或多个`SELECT`语句的结果集。`UNION`操作返回的结果集会去除重复的行，即如果两个或多个`SELECT`语句返回了相同的行，`UNION`操作会保留其中的一行。

`UNION`操作的基本语法如下：

```
SELECT column1, column2, ...
FROM table1
UNION
SELECT column1, column2, ...
FROM table2;
```

在这个语法中，`UNION`操作会合并两个`SELECT`语句的结果集，并返回去重后的结果。

如果你希望保留所有的行，包括重复的行，可以使用`UNION ALL`操作。`UNION ALL`操作不会去除重复的行，它会简单地合并所有的结果。

```
SELECT column1, column2, ...
FROM table1
UNION ALL
SELECT column1, column2, ...
FROM table2;
```

**需要注意的是，`UNION`和`UNION ALL`的两个`SELECT`语句必须具有相同的列数和相似的数据类型。如果两个`SELECT`语句的列数不同，或者列的数据类型不匹配，数据库系统会返回错误。**

以下是一个简单的示例，假设有两个表`employees`和`customers`：

**`employees`表结构：**

```
+-------------+---------------+
| employee_id | employee_name |
+-------------+---------------+
| 1           | Alice         |
| 2           | Bob           |
+-------------+---------------+
```

**`customers`表结构：**

```
+-------------+---------------+
| customer_id | customer_name |
+-------------+---------------+
| 1           | Customer A    |
| 2           | Customer B    |
+-------------+---------------+
```

如果你想要获取`employees`表中的员工名字以及`customers`表中的客户名字，可以使用`UNION`操作：

```
SELECT employee_name FROM employees
UNION
SELECT customer_name FROM customers;
```

这个查询会返回去除重复的员工名字和客户名字的结果集。如果希望保留所有的行，包括重复的行，可以使用`UNION ALL`操作：

```
SELECT employee_name FROM employees
UNION ALL
SELECT customer_name FROM customers;
```

**例子**

```
USE sql_store;

SELECT 
    customer_id,
    first_name,
    points,
    "Bronze" AS type
FROM customers
WHERE points<1000
UNION 
SELECT 
    customer_id,
    first_name,
    points,
    "Sliver" AS type
FROM customers
WHERE points BETWEEN 1000 AND 2000
UNION 
SELECT 
    customer_id,
    first_name,
    points,
    "Gold" AS type
FROM customers
WHERE points>3000
ORDER BY customer_id
```



## 三,列属性

在数据库中，每一列都有一些属性（也称为特性或约束），这些属性定义了列的行为、数据类型、和规则。以下是常见的列属性：

1. **数据类型（Data Type）：** 指定列可以存储的数据类型，例如整数（INT）、字符串（VARCHAR）、日期（DATE）等。数据类型定义了列可以包含的数据种类和范围。
2. **长度（Length）：** 对于字符串类型的列，长度表示该列可以存储的字符数量。例如，VARCHAR(50) 表示该列可以存储最多 50 个字符的字符串。
3. **约束（Constraints）：** 约束定义了列的规则和限制。常见的约束包括：
   - **主键约束（Primary Key Constraint）：** 保证列中的值是唯一的，并且不为空。主键是用来唯一标识表中的每一行数据的列。
   - **外键约束（Foreign Key Constraint）：** 用于在两个表之间建立关系。外键列的值必须在另一个表的主键列中存在。
   - **唯一约束（Unique Constraint）：** 确保列中的所有值都是唯一的，但允许空值。
   - **检查约束（Check Constraint）：** 定义了该列中的值必须满足的条件。
   - **非空约束（NOT NULL Constraint）：** 确保该列中的值不为空。
4. **默认值（Default Value）：** 指定当插入新行时，如果没有提供该列的值，将会使用的默认值。
5. **自动增量（Auto Increment）：** 对于整数列，可以设置为自动增量（例如MySQL中的AUTO_INCREMENT），这样数据库系统会自动为每个新行生成一个唯一的、递增的值，通常用作主键。

这些列属性可以根据具体的数据库系统和表的设计需求来定义，它们确保了数据的一致性、完整性和准确性。在设计数据库表时，合理定义列属性是至关重要的，因为它们决定了数据的有效性和可靠性。

### 1.插入单行

在 SQL 中，要插入单行数据到数据库表中，你可以使用 `INSERT INTO` 语句。以下是插入单行数据的基本语法：

```
INSERT INTO table_name (column1, column2, column3, ...)
VALUES (value1, value2, value3, ...);
```

在这个语法中：

- `table_name` 是你要插入数据的表的名称。
- `column1, column2, column3, ...` 是表中的列名，你要插入数据的列。
- `value1, value2, value3, ...` 是对应列名的实际值。

例如，如果有一个表 `employees` 包含 `employee_id`、`first_name` 和 `last_name` 列，你可以插入一行数据如下：

```
INSERT INTO employees (employee_id, first_name, last_name)
VALUES (1, 'Alice', 'Smith');
```

这个语句会将一行数据插入到 `employees` 表中，`employee_id` 列的值是 1，`first_name` 列的值是 'Alice'，`last_name` 列的值是 'Smith'。

请确保提供的列名和值的数量和顺序是一致的，遵循表的定义。如果表有自增列（例如 MySQL 中的 AUTO_INCREMENT 列），你可以不提供该列的值，数据库会自动生成一个唯一的值。

如果你不提供列名，可以直接插入所有列的数据。例如：

```
INSERT INTO employees
VALUES (1, 'Alice', 'Smith');
```

这种情况下，必须确保提供的值的顺序与表的列的顺序一致。

### 2.插入多行

要插入多行数据到数据库表中，你可以使用 `INSERT INTO` 语句的扩展语法，一次性插入多组数据。以下是插入多行数据的基本语法：

```
INSERT INTO table_name (column1, column2, column3, ...)
VALUES (value1, value2, value3, ...),
       (value1, value2, value3, ...),
       (value1, value2, value3, ...),
       ...;
```

在这个语法中，你可以指定多个值组，每个值组都用括号括起来，并用逗号分隔。每个值组代表一行数据。例如，如果你有一个表 `employees` 包含 `employee_id`、`first_name` 和 `last_name` 列，你可以插入多行数据如下：

```
INSERT INTO employees (employee_id, first_name, last_name)
VALUES (1, 'Alice', 'Smith'),
       (2, 'Bob', 'Johnson'),
       (3, 'Charlie', 'Brown');
```

这个语句会一次性插入三行数据到 `employees` 表中。

请确保每个值组中的列值和顺序与表的定义相匹配。如果表有自增列（例如 MySQL 中的 AUTO_INCREMENT 列），不需要为该列提供值，数据库会自动生成唯一的值。

插入多行数据的语法可以简化大量单行插入语句，提高数据插入效率。

**例子**

```
USE sql_store;

INSERT INTO products( name , quantity_in_stock , unit_price )

VALUES ("王旭",68,1.2),
      ('王迪宇',59,4.7),
      ("欧阳泽强",47,3.6)
```





### 3.插入分层行

如果你想要插入带有层次结构的数据，可以使用递归插入或者使用多个INSERT语句，逐层插入数据。假设你有一个分层的表`categories`，它包含`category_id`和`parent_category_id`列，表示每个类别的唯一标识和其父类别的标识。下面是一个递归插入数据的示例：

```
INSERT INTO categories (category_id, parent_category_id, category_name)
VALUES (1, NULL, 'Root Category'), -- 插入根类别

-- 插入第一层子类别
(2, 1, 'Subcategory 1.1'),
(3, 1, 'Subcategory 1.2'),

-- 插入第二层子类别
(4, 2, 'Sub-subcategory 1.1.1'),
(5, 2, 'Sub-subcategory 1.1.2'),

(6, 3, 'Sub-subcategory 1.2.1'),
(7, 3, 'Sub-subcategory 1.2.2');
```

在这个示例中，我们首先插入了一个根类别，然后插入了两个一级子类别，接着插入了这两个子类别的二级子类别。`parent_category_id`列用于指示每个类别的父类别。

请注意，插入数据时，你需要确保每个子类别的`parent_category_id`对应于其父类别的`category_id`，以建立正确的层次关系。在具体的应用中，你需要根据你的数据结构和需求，逐层插入数据。

 

**例子**

```
USE sql_store;

INSERT INTO orders (customer_id, order_date, status)
VALUES (1, '2019-01-02', 1);

INSERT INTO order_items
VALUES 
    (LAST_INSERT_ID(), 1, 1, 2.95),
    (LAST_INSERT_ID(), 2, 1, 3.95)
```

这两个 SQL 语句用于在数据库中插入订单相关的数据。

**第一个 SQL 语句：**

```
INSERT INTO orders (customer_id, order_date, status)
VALUES (1, '2019-01-02', 1);
```

这个语句插入了一条新的订单记录到 `orders` 表中。具体解释如下：

- `INSERT INTO orders`: 指定了要插入数据的目标表是 `orders`。
- `(customer_id, order_date, status)`: 指定了要插入的列，这三列分别是 `customer_id`、`order_date` 和 `status`。
- `VALUES (1, '2019-01-02', 1)`: 插入的具体数值，分别对应了 `customer_id` 为 1、`order_date` 为 '2019-01-02'、`status` 为 1。

这样，这条语句在 `orders` 表中插入了一个新的订单。

**第二个 SQL 语句：**

```
INSERT INTO order_items
VALUES 
    (LAST_INSERT_ID(), 1, 1, 2.95),
    (LAST_INSERT_ID(), 2, 1, 3.95);
```

这个语句插入了相关的订单项到 `order_items` 表中。具体解释如下：

- `INSERT INTO order_items`: 指定了要插入数据的目标表是 `order_items`。
- `VALUES`: 指定了要插入的具体数值。
- `(LAST_INSERT_ID(), 1, 1, 2.95)`: 插入了一行数据，其中 **`LAST_INSERT_ID()` 用于获取刚刚插入到 `orders` 表中的订单的主键值（通常是自增的），这个主键值将作为外键关联到 `order_items` 表中，**然后后面的数据 `1, 1, 2.95` 分别对应了 `order_id`、`product_id`、`quantity` 和 `price`。
- `(LAST_INSERT_ID(), 2, 1, 3.95)`: 插入了另一行数据，使用了同样的 `LAST_INSERT_ID()` 函数获取刚刚插入到 `orders` 表中的订单的主键值，然后后面的数据 `2, 1, 3.95` 分别对应了 `order_id`、`product_id`、`quantity` 和 `price`。

这样，第二条语句在 `order_items` 表中插入了两个订单项，这两个订单项都与刚刚插入的订单相关联。



#### LAST_INSERT_ID()方法

在关系型数据库中，`LAST_INSERT_ID()` 是一个函数，用于获取最后插入的行的自增主键值。通常，在执行一个插入操作后，可以使用**这个函数来获取刚刚插入的行的主键值。**

具体来说，当你在一个表中插入一条新记录时，如果该表的主键列（通常是自增列）被设置成了自动增长，数据库会为新插入的行分配一个唯一的主键值。`LAST_INSERT_ID()` 函数用于返回刚刚插入的行的主键值。

这个函数通常在以下场景中使用：

1. 插入一条新的记录，并且你需要获取刚刚插入的行的主键值。
2. 插入多条记录，但是你只关心最后一条记录的主键值。

例如，在MySQL数据库中，当你插入一条新的记录时，可以这样使用 `LAST_INSERT_ID()` 函数：

```
INSERT INTO table_name (column1, column2) VALUES (value1, value2);
SELECT LAST_INSERT_ID();
```

这个例子中，`table_name` 是你要插入数据的表的名称，`column1` 和 `column2` 是表中的列名，`value1` 和 `value2` 是对应列名的实际值。`LAST_INSERT_ID()` 函数会返回刚刚插入的行的主键值。

### 4.创建表复制

在MySQL中，你可以使用`CREATE TABLE`语句来复制现有表的结构，并在新表中插入现有表中的数据。以下是在MySQL中进行表复制的基本方法：

```
CREATE TABLE new_table AS
SELECT * FROM existing_table;
```

在这个语句中，`new_table` 是你想要创建的新表的名称，`existing_table` 是现有表的名称。这个语句会创建一个新表 `new_table`，它的结构（列名、数据类型等）与 `existing_table` 相同，并且会复制 `existing_table` 中的所有数据。

如果你只想复制表的结构而不包括数据，你可以使用以下语句：

```
CREATE TABLE new_table LIKE existing_table;
```

这个语句会创建一个空的 `new_table`，它的结构与 `existing_table` 相同，但是不包含任何数据。

如果你想要在新表中复制部分数据，你可以在 `SELECT` 语句中添加适当的条件，例如：

```
CREATE TABLE new_table AS
SELECT * FROM existing_table WHERE column_name = 'some_value';
```

这将会在 `new_table` 中复制 `existing_table` 中 `column_name` 列值为 `'some_value'` 的所有行。

### 5.更新单行

要更新数据库表中的单行数据，你可以使用 `UPDATE` 语句。以下是基本的 `UPDATE` 语法：

```
UPDATE table_name
SET column1 = value1, column2 = value2, ...
WHERE condition;
```

在这个语法中，`table_name` 	是你要更新数据的表的名称，`column1`、`column2` 等是你要更新的列名，`value1`、`value2` 等是你要更新的新值，`condition` 是用于指定要更新哪些行的条件。

例如，如果你有一个表 `employees` 包含 `employee_id`、`first_name` 和 `last_name` 列，你可以使用以下语句更新表中 `employee_id` 为 1 的员工的 `first_name` 列的值：

```
UPDATE employees
SET first_name = 'John'
WHERE employee_id = 1;
```

这个语句会将 `employee_id` 为 1 的员工的 `first_name` 更新为 'John'。

请注意，**`WHERE` 子句是非常重要的，它指定了哪些行将会被更新。如果你省略了 `WHERE` 子句，所有行都会被更新**。因此，请确保在 `UPDATE` 语句中使用 `WHERE` 子句来指定更新的具体行。

### 6.更新多行

在MySQL中，更新多行数据的方法与更新单行类似，你可以使用 `UPDATE` 语句，并通过 `WHERE` 子句指定更新的条件。以下是更新多行数据的基本语法：

```
UPDATE table_name
SET column1 = value1, column2 = value2, ...
WHERE condition;
```

在这个语法中，`table_name` 是你要更新数据的表的名称，`column1`、`column2` 等是你要更新的列名，`value1`、`value2` 等是你要更新的新值，`condition` 是用于指定要更新哪些行的条件。

例如，假设有一个表 `employees` 包含 `employee_id`、`first_name` 和 `last_name` 列，你可以使用以下语句将所有姓氏（`last_name`）为 'Smith' 的员工的名字（`first_name`）更新为 'John'：

```
UPDATE employees
SET first_name = 'John'
WHERE last_name = 'Smith';
```

这个语句会将表中所有姓氏为 'Smith' 的员工的名字更新为 'John'。

如果你希望更新所有行而没有特定的条件，可以省略 `WHERE` 子句。但请小心使用，因为没有 `WHERE` 子句的 `UPDATE` 语句会将表中所有行的数据都更新为指定的值，可能导致不可逆的数据变更。在没有特定条件的情况下，建议先做好备份，并仔细确认更新的操作。

**例子**

```
USE sql_store;

UPDATE orders
SET comments = 'Gold customer'
WHERE customer_id IN
        (SELECT customer_id
        FROM customers
        WHERE points >3000)
```

### 7.删除行

在 MySQL 中，要删除表中的行，你可以使用 `DELETE` 语句。以下是基本的 `DELETE` 语法：

```
DELETE FROM table_name WHERE condition;
```

在这个语法中，`table_name` 是你要删除数据的表的名称，`condition` 是一个可选的条件，用于指定哪些行将被删除。

例如，如果你有一个名为 `invoices` 的表，想要删除那些 `client_id` 为 3 的发票，你可以使用以下 `DELETE` 语句：

```
DELETE FROM invoices WHERE client_id = 3;
```

如果你希望删除表中的所有行，可以省略 `WHERE` 子句，但请小心使用这种情况，因为它会删除整个表中的所有数据：

```
DELETE FROM invoices;
```

在执行 `DELETE` 语句时，请确保你理解它的影响，并谨慎使用带有 `WHERE` 子句的条件，以免删除过多的数据。在执行删除操作之前，最好做好数据备份。

**例子**

```
DELETE FROM invoices
WHERE client_id =(
    SELECT *
    FROM clients
    WHERE name = 'Myworks'
)
```

## 四.聚合函数

MySQL中有许多聚合函数，它们用于对一组值执行计算并返回单个值。以下是一些常见的MySQL聚合函数：

1. **COUNT()：** 计算行的数量。

   ```
   SELECT COUNT(*) FROM table_name;
   ```

2. **SUM()：** 计算数值列的总和。

   ```
   SELECT SUM(column_name) FROM table_name;
   ```

3. **AVG()：** 计算数值列的平均值。

   ```
   SELECT AVG(column_name) FROM table_name;
   ```

4. **MIN()：** 返回数值列的最小值。

   ```
   SELECT MIN(column_name) FROM table_name;
   ```

5. **MAX()：** 返回数值列的最大值。

   ```
   SELECT MAX(column_name) FROM table_name;
   ```

6. **GROUP_CONCAT()：** 将结果集中的值连接为一个字符串，通常与 GROUP BY 一起使用。

   ```
   SELECT column_name, GROUP_CONCAT(other_column) FROM table_name GROUP BY column_name;
   ```

7. **GROUP BY：** 将结果集按照指定列的值分组，并对每个组应用聚合函数。

   ```
   SELECT column_name, COUNT(*) FROM table_name GROUP BY column_name;
   ```

8. **HAVING：** 在 GROUP BY 中使用，对分组后的结果进行条件过滤。

   ```
   SELECT column_name, COUNT(*) FROM table_name GROUP BY column_name HAVING COUNT(*) > 1;
   ```

这些聚合函数可以用于在查询中执行各种计算和统计操作。请注意，聚合函数通常与 GROUP BY 子句一起使用，以便按照特定列的值对数据进行分组。

**例子**

```
SELECT
    MAX(invoice_total) AS highest,
    MIN(invoice_total) AS lowest,
    AVG(invoice_total) AS average,
    SUM(invoice_total * 1.1) AS total,
    COUNT(DISTINCT client_id) AS total_records
FROM invoices
WHERE invoice_date > '2019-07-01'    
```

**例子**

```
SELECT
    'first' AS date_range, 
    SUM(invoice_total) AS total_sales,
    SUM(payment_total) AS total_payment,
    SUM(invoice_total - payment_total) AS what_we_expect
FROM invoices
WHERE invoice_date
    BETWEEN '2019-01-01' AND '2019-06-30'
UNION
SELECT
    'last' AS date_range, 
    SUM(invoice_total) AS total_sales,
    SUM(payment_total) AS total_payment,
    SUM(invoice_total - payment_total) AS what_we_expect
FROM invoices
WHERE invoice_date
    BETWEEN '2019-07-01' AND '2019-12-31'
UNION
SELECT
    'total' AS date_range, 
    SUM(invoice_total) AS total_sales,
    SUM(payment_total) AS total_payment,
    SUM(invoice_total - payment_total) AS what_we_expect
FROM invoices
WHERE invoice_date
    BETWEEN '2019-01-01' AND '2019-12-31'

```



### 1.count()

`COUNT()` 是MySQL中的聚合函数之一，用于计算指定列或符合特定条件的行数。它可以用来获取表中的记录数量，也可以结合其他列或条件来进行更复杂的计数操作。

基本语法如下：

```
SELECT COUNT(column_name) FROM table_name WHERE condition;
```

- `column_name` 是要计数的列的名称，如果你想计算整个表的行数，可以使用 `COUNT(*)`。
- `table_name` 是要从中进行计数的表的名称。
- `condition` 是一个可选的条件，用于过滤计数的行。如果省略条件，则将计算整个表的行数。

例如，如果有一个名为 `users` 的表，你可以使用 `COUNT(*)` 来获取表中的总行数：

```
SELECT COUNT(*) FROM users;
```

如果你只想计算一个特定条件下的行数，可以添加 `WHERE` 子句：

```
SELECT COUNT(*) FROM users WHERE age > 18;
```

这将返回满足条件 `age > 18` 的行数。

此外，`COUNT()` 还可以与 `GROUP BY` 结合使用，用于按照某列的值进行分组计数。例如，计算每个城市的用户数量：

```
SELECT city, COUNT(*) FROM users GROUP BY city;
```

这将返回每个城市的用户数量，并按城市进行分组。

总之，`COUNT()` 是一个非常有用的聚合函数，用于获取行数或满足特定条件的行数，可以在简单的统计查询和复杂的分组查询中发挥作用。

### 2.group by子句

`GROUP BY` 字句是用于对查询结果进行分组的 SQL 语句。它通常与聚合函数一起使用，以便在每个分组上执行计算。以下是 `GROUP BY` 字句的基本语法：

```
SELECT column1, aggregate_function(column2)
FROM table_name
GROUP BY column1;
```

其中：

- `column1` 是你希望按其分组的列。
- `aggregate_function(column2)` 是在每个分组上执行的聚合函数，可以是 `COUNT()`、`SUM()`、`AVG()`、`MIN()`、`MAX()` 等。

以下是一个简单的示例，假设有一个名为 `sales` 的表，包含了销售人员、销售额和销售日期：

```
SELECT salesman, SUM(sales_amount)
FROM sales
GROUP BY salesman;
```

在这个例子中，查询将按 `salesman` 列进行分组，并计算每个销售人员的销售总额。

在使用 `GROUP BY` 时，需要注意以下几点：

1. **选择列和聚合函数：** `SELECT` 子句中的列必须是 `GROUP BY` 子句中列的一部分，或者是聚合函数的参数。除非它们是 `GROUP BY` 子句中列的一部分，否则选择的列必须是聚合函数的参数。

2. **聚合函数：** 通常与 `GROUP BY` 一起使用的是聚合函数，以对每个分组执行计算。

3. **多列分组：** 你可以指定多个列，以便按多个列的组合进行分组。例如：

   ```
   SELECT department, city, AVG(salary)
   FROM employees
   GROUP BY department, city;
   ```

   在这个例子中，结果将按照 `department` 和 `city` 列的组合进行分组，并计算每个组的平均工资。

4. **HAVING 子句：** 如果你想对分组后的结果应用条件过滤，可以使用 `HAVING` 子句。它的用法类似于 `WHERE` 子句，但是它是在分组后应用的。

   ```
   SELECT department, AVG(salary)
   FROM employees
   GROUP BY department
   HAVING AVG(salary) > 50000;
   ```

   在这个例子中，只返回平均工资超过 50000 的部门。

`GROUP BY` 字句是进行数据聚合和分组分析时非常有用的工具，可以帮助你更好地理解和汇总数据。

**例子**

```
SELECT 
    date,
    pm.name,
    SUM(amount) AS 'total_payments'
FROM payments p
JOIN payment_methods pm 
    ON p.payment_method = pm.payment_method_id
GROUP BY date, pm.name
ORDER BY date
```

### 3.having子句

`HAVING` 子句通常与 `GROUP BY` 子句一起使用，用于对分组后的结果进行过滤。它允许你筛选出满足特定条件的分组，类似于 `WHERE` 子句用于筛选行。

基本语法如下：

```
SELECT column1, aggregate_function(column2)
FROM table_name
GROUP BY column1
HAVING condition;
```

其中：

- `column1` 是你希望按其分组的列。
- `aggregate_function(column2)` 是在每个分组上执行的聚合函数。
- `condition` 是对分组后的结果进行过滤的条件。

以下是一个简单的例子，假设有一个名为 `sales` 的表，包含了销售人员、销售额和销售日期。我们想找到销售总额大于 1000 的销售人员：

```
SELECT salesman, SUM(sales_amount) AS total_sales
FROM sales
GROUP BY salesman
HAVING total_sales > 1000;
```

在这个例子中，`HAVING total_sales > 1000` 用于筛选出总销售额大于 1000 的销售人员的分组。

`HAVING` 子句可以包含与聚合函数相关的条件，例如 `SUM(column) > value`，也可以包含其他列的条件。在使用 `HAVING` 子句时，要确保条件是与聚合函数或分组列相关的，因为它是在已经进行分组的结果上进行过滤的。

请注意，`HAVING` 子句在 `GROUP BY` 子句之后执行，并且在 `SELECT` 列表中的列名可以使用别名。

### 4.rollup 子句

**在用rollup运算符的时候，我们不能在group by 子句中使用别名**

`ROLLUP` 是一种用于在 `GROUP BY` 子句中生成汇总行的扩展。它允许在结果集中包含汇总值，而不仅仅是按照给定列进行分组的行。 `ROLLUP` 生成的行对应于按照给定列的不同层次进行的汇总。

基本语法如下：

```
SELECT column1, column2, aggregate_function(column3)
FROM table_name
GROUP BY column1, column2 WITH ROLLUP;
```

其中：

- `column1`, `column2` 是你希望按其分组的列。
- `aggregate_function(column3)` 是在每个分组上执行的聚合函数。
- `WITH ROLLUP` 表示启用 `ROLLUP` 功能。

以下是一个简单的例子，假设有一个名为 `sales` 的表，包含了销售人员、产品类型、销售额和销售日期。我们想找到每个销售人员、产品类型的销售总额，并在每个销售人员和产品类型的组上生成总销售额：

```
SELECT salesman, product_type, SUM(sales_amount) AS total_sales
FROM sales
GROUP BY salesman, product_type WITH ROLLUP;
```

在这个例子中，`WITH ROLLUP` 会生成一个包含每个销售人员、产品类型以及总销售额的行。例如，如果有两个销售人员（A、B）和三个产品类型（X、Y、Z），则结果中将包含 2 * 3 + 1 = 7 行，其中 6 行是每个销售人员和产品类型的组合，还有一个总计行。

`ROLLUP` 会生成多个层次的总计行，每个层次都会提供当前层次上的小计。在结果集中，可以通过检查某些列的值是否为 `NULL` 来确定哪个层次上的总计。

请注意，`ROLLUP` 是在 SQL 标准中定义的一部分，但并非所有数据库管理系统都支持该功能。在使用时，请查阅你使用的数据库管理系统的文档，以确保其支持和语法的正确性。

## 五.编写复杂查询

### 1.子查询

子查询是在 SQL 查询中嵌套在其他查询内部的查询。子查询可以嵌套在 `SELECT`、`FROM`、`WHERE` 或 `HAVING` 子句中，用于执行额外的查询并将结果用作外部查询的一部分。

以下是一些常见的子查询用法：

1. **在 `SELECT` 子句中使用子查询：**

   ```
   SELECT column1, (SELECT column2 FROM table2 WHERE condition) AS subquery_result
   FROM table1;
   ```

   在这个例子中，子查询 `(SELECT column2 FROM table2 WHERE condition)` 在 `SELECT` 子句中返回一个值，该值将作为新列 `subquery_result` 的值出现在结果中。

2. **在 `FROM` 子句中使用子查询：**

   ```
   SELECT column1, column2
   FROM (SELECT column1, column2 FROM table1 WHERE condition) AS subquery_result;
   ```

   在这个例子中，子查询 `(SELECT column1, column2 FROM table1 WHERE condition)` 在 `FROM` 子句中创建一个虚拟表，然后外部查询从这个虚拟表中选择数据。

3. **在 `WHERE` 子句中使用子查询：**

   ```
   SELECT column1, column2
   FROM table1
   WHERE column1 = (SELECT column1 FROM table2 WHERE condition);
   ```

   在这个例子中，子查询 `(SELECT column1 FROM table2 WHERE condition)` 在 `WHERE` 子句中返回一个值，该值用于过滤外部查询的结果。

4. **在 `HAVING` 子句中使用子查询：**

   ```
   SELECT column1, COUNT(column2) AS count_column2
   FROM table1
   GROUP BY column1
   HAVING COUNT(column2) > (SELECT AVG(column2) FROM table1);
   ```

   在这个例子中，子查询 `(SELECT AVG(column2) FROM table1)` 在 `HAVING` 子句中返回一个值，用于过滤分组后的结果。

子查询可以是标量子查询（返回单个值），也可以是行子查询（返回多个列和行）或表子查询（返回整个表）。子查询通常用于解决复杂的查询问题，它可以帮助你在一个查询中使用另一个查询的结果。

**例子**

```
USE sql_hr;

SELECT *
FROM employees
WHERE salary > (
    SELECT AVG(salary)
    FROM employees
)
```

### 2.子查询中的IN

这个查询的目的是从 `products` 表中选择那些在 `order_items` 表中没有出现的产品。让我解释一下：

```
USE sql_store;

SELECT *
FROM products
WHERE product_id NOT IN (
    SELECT DISTINCT product_id
    FROM order_items
);
```

1. **外部查询 (`SELECT \* FROM products WHERE product_id NOT IN (...);`):**
   - 这个部分从 `products` 表中选择所有列。
   - `WHERE` 子句使用 `NOT IN` 运算符，后面跟着一个子查询。
2. **子查询 (`SELECT DISTINCT product_id FROM order_items;`):**
   - 这个子查询从 `order_items` 表中选择唯一的 `product_id` 列值。`DISTINCT` 用于确保子查询中没有重复的产品 ID。
   - 这个子查询的结果是一个包含 `order_items` 表中所有不同的 `product_id` 的列表。
3. **`NOT IN` 运算符:**
   - 外部查询使用 `NOT IN`，表示它要选择在 `products` 表中，但不在上述子查询结果列表中的产品。

因此，最终结果是选择那些在 `products` 表中，但在 `order_items` 表中没有出现的产品。这可能用于找出尚未被订购的产品。



### 3.子查询中加join

这个查询的目的是从 `customers` 表中选择那些在 `order_items` 表中购买了产品ID为3的产品的客户。让我解释一下：

```
USE sql_store;

SELECT *
FROM customers
WHERE customer_id IN (
    SELECT o.customer_id
    FROM order_items os
    JOIN orders o USING (order_id)
    WHERE product_id = 3
);
```

1. **外部查询 (`SELECT \* FROM customers WHERE customer_id IN (...);`):**
   - 这个部分从 `customers` 表中选择所有列。
   - `WHERE` 子句使用 `IN` 运算符，后面跟着一个子查询。
2. **子查询 (`SELECT o.customer_id FROM order_items os JOIN orders o USING (order_id) WHERE product_id = 3;`):**
   - 这个子查询从 `order_items` 表中选择那些购买了产品ID为3的产品的订单。它通过联接 `order_items` 表和 `orders` 表，并根据 `order_id` 进行联接。
   - `WHERE product_id = 3` 用于过滤掉那些购买了产品ID不为3的订单。
   - 最终，这个子查询返回一个包含购买了产品ID为3的产品的订单的 `customer_id` 列值的列表。
3. **`IN` 运算符:**
   - 外部查询使用 `IN`，表示它要选择在 `customers` 表中，但在上述子查询结果列表中的客户。

因此，最终结果是选择那些在 `customers` 表中，而且购买了产品ID为3的产品的客户。这可以用于查找购买了特定产品的客户。

### 4.ALL关键字

`ALL` 关键字通常与比较运算符一起使用，用于比较一个值与子查询中的所有值。下面是一些关于 `ALL` 关键字的详细解释：

1. **基本语法：**

   ```
   value comparison_operator ALL (subquery)
   ```

   - `value` 是一个标量值，可以是常量或来自外部查询的列值。
   - `comparison_operator` 是比较运算符，指定如何比较左侧的值和子查询的结果。
   - `subquery` 是返回一列值的子查询，它提供了与左侧值进行比较的参考值。

2. **比较过程：**

   - 如果 `comparison_operator` 是 `=`，则左侧的值必须等于子查询中的所有值，否则条件不满足。
   - 如果 `comparison_operator` 是 `<`, `>`, `<=`, `>=`，则左侧的值必须在与子查询中的所有值进行比较时都满足条件，否则条件不满足。
   - 如果 `comparison_operator` 是 `<>`，则左侧的值不能等于子查询中的任何值，否则条件不满足。

3. **示例：**

   假设我们有一个 `employees` 表，想找到所有工资高于所有销售代表平均工资的员工：

   ```
   SELECT employee_id, salary
   FROM employees
   WHERE salary > ALL (
       SELECT AVG(salary)
       FROM employees
       WHERE job_title = 'Sales Representative'
   );
   ```

   在这个例子中，外部查询选择了员工ID和工资，但是只有当员工的工资高于所有销售代表的平均工资时，才会包括在结果中。`ALL` 关键字确保员工的工资高于销售代表的平均工资，而不仅仅是其中的一位销售代表。

总体而言，**`ALL` 提供了一种在比较运算中处理多个值的方式，它要求左侧的值在与子查询中的所有值进行比较时都满足指定的条件。**

**例子**

```
USE sql_invoicing;

SELECT *
FROM invoices
WHERE invoice_total >ALL(
    SELECT invoice_total
    FROM invoices
    WHERE client_id = 3
)
```

### 5.any关键字

`ANY` 关键字是 SQL 中用于与比较运算符一起使用的关键字，通常用于子查询中。它用于比较一个值与子查询的结果中的任何值。

以下是 `ANY` 关键字的一般用法：

```
value comparison_operator ANY (subquery)
```

- `value` 是与子查询中的任何值进行比较的标量值。
- `comparison_operator` 是比较运算符，如 `=`, `>`, `<`, `>=`, `<=`, `<>` 等。
- `subquery` 是返回一列值的子查询。

`ANY` 的工作方式如下：

- 如果 `comparison_operator` 是 `=`，则要求左侧的值等于子查询中的任何一个值。
- 如果 `comparison_operator` 是 `<`, `>`, `<=`, `>=`，则要求左侧的值在与子查询中的任何一个值进行比较时满足条件。
- 如果 `comparison_operator` 是 `<>`，则要求左侧的值不等于子查询中的所有值。

以下是一个示例，假设我们想找到所有工资高于销售代表中的任何一个人的平均工资的员工：

```
SELECT employee_id, salary
FROM employees
WHERE salary > ANY (
    SELECT AVG(salary)
    FROM employees
    WHERE job_title = 'Sales Representative'
);
```

在这个例子中，外部查询选择了员工ID和工资，但是只有当员工的工资高于销售代表中的任何一个人的平均工资时，才会包括在结果中。`ANY` 关键字确保员工的工资高于销售代表中的至少一个人的平均工资。

总体而言，`ANY` 提供了一种在比较运算中处理多个值的方式，它要求左侧的值在与子查询中的任何一个值进行比较时满足指定的条件。

#### ALL关键字和ANY关键字可以用其他去代替 



### 6.相关子查询

相关子查询是指子查询中的结果依赖于外部查询的值。换句话说，子查询中的执行取决于外部查询的每一行。相关子查询通常使用在 `WHERE` 子句或 `FROM` 子句中，以便根据外部查询的条件动态地影响子查询的结果。

以下是一个例子，假设我们有两个表格：`orders` 包含订单信息，`order_items` 包含订单项信息。我们想找到那些订单中至少有一个产品的数量超过 10 的订单：

```
SELECT order_id, customer_id
FROM orders o
WHERE EXISTS (
    SELECT 1
    FROM order_items oi
    WHERE oi.order_id = o.order_id
      AND oi.quantity > 10
);
```

在这个例子中，外部查询是从 `orders` 表中选择订单ID和顾客ID。子查询是在 `order_items` 表中检查相同订单中是否有任何订单项的数量超过 10。`EXISTS` 关键字用于检查子查询是否返回至少一行，如果是，则外部查询的相应行就会包括在结果中。

这是一个相关子查询的例子，因为子查询中的 `oi.order_id = o.order_id` 部分将子查询的执行与外部查询的每一行关联起来。

相关子查询可以帮助你根据外部查询的条件动态地过滤子查询的结果。

#### 例子

这个查询的目的是选择工资高于其办公室（office_id）内所有员工平均工资的员工。让我对这个查询进行详细解释：

```
USE sql_hr;

SELECT *
FROM employees e
WHERE salary > (
    SELECT AVG(salary)
    FROM employees
    WHERE office_id = e.office_id
);
```

1. **外部查询 (`SELECT \* FROM employees e WHERE salary > (...);`):**
   - 这个部分从 `employees` 表中选择所有员工的所有列。
   - `WHERE` 子句包含一个子查询，用于比较员工的工资是否高于其办公室内所有员工的平均工资。
2. **子查询 (`SELECT AVG(salary) FROM employees WHERE office_id = e.office_id;`):**
   - 这个子查询计算了特定办公室（`office_id`）内所有员工的平均工资。
   - `AVG(salary)` 返回具有相同办公室ID的所有员工的工资平均值，`WHERE office_id = e.office_id` 用于确保只计算同一办公室的员工工资。
3. **比较 (`salary > (...)`):**
   - 外部查询中的 `salary` 用于与子查询的结果进行比较。
   - 如果外部查询中的员工工资高于其办公室内所有员工的平均工资，那么相应的员工将包括在结果中。

总体而言，这个查询选择了那些工资高于其办公室内所有员工平均工资的员工。这种查询结构允许你动态地基于子查询的条件过滤外部查询的结果，**确保比较的是同一办公室的员工。**





### 7.EXISTS运算符

`EXISTS` 是一个 SQL 中的条件谓词，用于检查子查询是否返回至少一行结果。它的一般形式如下：

```
EXISTS (subquery)
```

- `subquery` 是一个子查询，返回结果集不需要包含实际的列，因为 `EXISTS` 只关心子查询是否返回了至少一行。

`EXISTS` 的工作方式如下：

- 如果子查询返回至少一行，则 `EXISTS` 返回 `TRUE`，否则返回 `FALSE`。
- `EXISTS` 通常用于在主查询中检查子查询的结果，以便决定是否包括主查询的相应行。

以下是一个简单的例子，假设我们有一个表格 `employees`，我们想找到那些至少有一项项目分配给他们的员工：

```
SELECT employee_id, employee_name
FROM employees e
WHERE EXISTS (
    SELECT 1
    FROM assignments a
    WHERE a.employee_id = e.employee_id
);
```

在这个例子中，`EXISTS` 用于检查是否存在至少一个项目分配给每个员工。如果是，那么相应的员工将包括在结果中。

`EXISTS` 是一种非常有用的条件谓词，它使你能够根据子查询的结果动态地影响主查询的结果。

**例子**

```
USE sql_store;


SELECT *
FROM products p
WHERE NOT EXISTS (
    SELECT product_id
    FROM order_items
    WHERE product_id = p.product_id
)
```

### 8.SELECT子句中的子查询

在SQL中，可以在`SELECT`子句中嵌套子查询，以从内部查询中获取数据并将其作为列的一部分包括在外部查询的结果中。这种嵌套的子查询称为“标量子查询”或“行子查询”。

以下是一个简单的例子，说明如何在`SELECT`子句中使用子查询：

```mysql
SELECT 
    employee_id,
    employee_name,
    (SELECT AVG(salary) FROM employees) AS average_salary
FROM employees;
```

在这个例子中，子查询 `(SELECT AVG(salary) FROM employees)` 被嵌套在`SELECT`子句中，计算了所有员工的平均工资。结果中的`average_salary`列将包含每个员工行的相同平均工资值。

这是一个简单的示例，但你可以根据需要在`SELECT`子句中使用更复杂的子查询，以满足特定的查询要求。

### 9.FROM子句中的子查询

在 SQL 中，你也可以在 `FROM` 子句中使用子查询。这样的子查询返回一个虚拟的表，你可以在主查询中引用它。这种类型的子查询通常称为“派生表”或“内联视图”。

以下是一个示例，说明如何在 `FROM` 子句中使用子查询：

```mysql
SELECT 
    department_name,
    total_salary
FROM (
    SELECT 
        department_id,
        AVG(salary) AS total_salary
    FROM employees
    GROUP BY department_id
) AS department_totals;
```

在这个例子中，`FROM` 子句中的子查询计算了每个部门的平均工资，并为每个部门生成一个虚拟表（内联视图）。然后，外部查询选择了 `department_name` 和 `total_salary` 列，其中 `total_salary` 包括了每个部门的平均工资。

这种结构允许你在主查询中引用一个经过计算或聚合的子查询结果，而不必将这个查询的逻辑直接放在主查询的 `SELECT` 子句中。这有助于使查询更加清晰和模块化。

## 六.MySQL的基本函数

### 1.数值函数

数值函数是 SQL 中用于处理数值数据的函数。它们执行各种数学和统计操作，以及对数值进行格式化和转换。以下是一些常见的数值函数：

1. **`ABS(x)`：** 返回 x 的绝对值。

   ```mysql
   SELECT ABS(-10); -- 返回 10
   ```

2. **`ROUND(x, d)`：** 将 x 四舍五入到小数点后 d 位。

   ```mysql
   SELECT ROUND(3.14159, 2); -- 返回 3.14
   ```

3. **`CEIL(x)` 或 `CEILING(x)`：** 返回大于或等于 x 的最小整数。

   ```mysql
   SELECT CEIL(4.25); -- 返回 5 
   ```

4. **`FLOOR(x)`：** 返回小于或等于 x 的最大整数。

   ```mysql
   SELECT FLOOR(4.75); -- 返回 4
   ```

5. **`POWER(x, y)` 或 `POW(x, y)`：** 返回 x 的 y 次幂。

   ```mysql
   SELECT POWER(2, 3); -- 返回 8
   ```

6. **`SQRT(x)`：** 返回 x 的平方根。

   ```mysql
   SELECT SQRT(16); -- 返回 4
   ```

7. **`EXP(x)`：** 返回 e 的 x 次幂，其中 e 是自然对数的底。

   ```mysql
   SELECT EXP(1); -- 返回 e 的近似值（约为 2.71828）
   ```

8. **`LOG(x)`：** 返回 x 的自然对数。

   ```mysql
   SELECT LOG(10); -- 返回 ln(10)
   ```

9. **`LOG10(x)`：** 返回 x 的以 10 为底的对数。

   ```mysql
   SELECT LOG10(100); -- 返回 2
   ```

10. **`RAND()`：** 返回一个 0 到 1 之间的随机浮点数。

    ```mysql
    SELECT RAND(); -- 返回 [0, 1) 之间的随机数
    ```

这些函数允许你在 SQL 查询中对数值进行各种计算和操作。请注意，不同数据库系统的函数名称和支持的功能可能会有所不同，因此你应该查阅相应数据库系统的文档以获取准确的信息。

### 2.字符串函数

字符串函数是 SQL 中用于处理字符串数据的函数。它们执行各种字符串操作，如连接、截取、转换大小写等。以下是一些常见的字符串函数：

1. **`CONCAT(str1, str2, ...)` 或 `||`（具体取决于数据库系统）：** 连接两个或多个字符串。

   ```mysql
   SELECT CONCAT('Hello', ' ', 'World'); -- 返回 'Hello World'
   ```

2. **`UPPER(str)` 或 `UCASE(str)`：** 将字符串转换为大写。

   ```mysql
   SELECT UPPER('hello'); -- 返回 'HELLO'
   ```

3. **`LOWER(str)` 或 `LCASE(str)`：** 将字符串转换为小写。

   ```mysql
   SELECT LOWER('WORLD'); -- 返回 'world'
   ```

4. **`LENGTH(str)` 或 `LEN(str)`（具体取决于数据库系统）：** 返回字符串的长度。

   ```mysql
   SELECT LENGTH('abc'); -- 返回 3
   ```

5. **`SUBSTRING(str, start, length)` 或 `SUBSTR(str, start, length)`：** 返回从字符串中的指定位置开始的指定长度的子字符串。

   ```mysql
   SELECT SUBSTRING('Hello World', 1, 5); -- 返回 'Hello'
   ```

6. **`TRIM([leading | trailing | both] characters FROM str)`：** 移除字符串两端或指定位置的空格或指定字符。

   ```mysql
   SELECT TRIM('   Hello   '); -- 返回 'Hello'
   ```

7. **`REPLACE(str, old, new)`：** 替换字符串中的指定子字符串。

   ```mysql
   SELECT REPLACE('Hello World', 'World', 'Universe'); -- 返回 'Hello Universe'
   ```

8. **`CHAR_LENGTH(str)` 或 `CHARACTER_LENGTH(str)`：** 返回字符串中的字符数（不同于字节数）。

   ```mysql
   SELECT CHAR_LENGTH('café'); -- 返回 4
   ```

9. **`LEFT(str, length)` 或 `RIGHT(str, length)`：** 返回字符串的左侧或右侧指定长度的子字符串。

   ```mysql
   SELECT LEFT('abcdef', 3); -- 返回 'abc'
   ```

10. **`INSTR(str, substr)` 或 `CHARINDEX(substr, str)`（具体取决于数据库系统）：** 返回子字符串在字符串中的位置。

    ```mysql
    SELECT INSTR('Hello World', 'World'); -- 返回 7
    ```

这些函数允许你在 SQL 查询中对字符串进行各种计算和操作。记得要查阅相应数据库系统的文档以获取准确的信息，因为不同的数据库系统可能有不同的函数实现和名称。

### 3.日期函数

MySQL 提供了许多用于处理日期和时间的内置函数。以下是一些常见的 MySQL 日期函数：

1. **`NOW()`：** 返回当前日期和时间。

   ```mysql
   SELECT NOW();
   ```

2. **`CURDATE()` 或 `CURRENT_DATE()`：** 返回当前日期。

   ```mysql
   SELECT CURDATE();
   ```

3. **`CURTIME()` 或 `CURRENT_TIME()`：** 返回当前时间。

   ```mysql
   SELECT CURTIME();
   ```

4. **`DATE(expr)`：** 从日期时间表达式中提取日期部分。

   ```mysql
   SELECT DATE(NOW());
   ```

5. **`TIME(expr)`：** 从日期时间表达式中提取时间部分。

   ```mysql
   SELECT TIME(NOW());
   ```

6. **`DAY(date)`：** 返回日期的天数部分。

   ```mysql
   SELECT DAY(NOW());
   ```

7. **`MONTH(date)`：** 返回日期的月份部分。

   ```mysql
   SELECT MONTH(NOW());
   ```

8. **`YEAR(date)`：** 返回日期的年份部分。

   ```mysql
   SELECT YEAR(NOW());
   ```

9. **`HOUR(time)`：** 返回时间的小时部分。

   ```mysql
   SELECT HOUR(NOW());
   ```

10. **`MINUTE(time)`：** 返回时间的分钟部分。

```mysql
SELECT MINUTE(NOW());
```

1. **`SECOND(time)`：** 返回时间的秒部分。

```mysql
SELECT SECOND(NOW());
```

1. **`DATEDIFF(date1, date2)`：** 返回两个日期之间的天数差。

   ```mysql
   SELECT DATEDIFF('2023-01-01', '2023-01-10');
   ```

2. **`DATE_ADD(date, INTERVAL expr unit)`：** 将时间间隔添加到日期。

   ```mysql
   SELECT DATE_ADD(NOW(), INTERVAL 7 DAY);
   ```

3. **`DATE_SUB(date, INTERVAL expr unit)`：** 从日期中减去时间间隔。

   ```mysql
   SELECT DATE_SUB(NOW(), INTERVAL 1 MONTH);
   ```

4. **`DATE_FORMAT(date, format)`：** 格式化日期。

   ```mysql
   SELECT DATE_FORMAT(NOW(), '%Y-%m-%d %H:%i:%s');
   ```

这些函数可以用于从日期和时间中提取信息、执行日期计算以及格式化日期和时间。在使用这些函数时，请注意 MySQL 版本可能会影响某些函数的可用性或语法。

### 4.格式化日期时间


在 MySQL 中，你可以使用 `DATE_FORMAT()` 函数来格式化日期时间。该函数接受两个参数：日期时间表达式和格式化字符串。以下是一些常见的日期时间格式化字符串：

- `%Y`：四位年份
- `%y`：两位年份
- `%m`：月份（01-12）
- `%c`：月份（1-12）
- `%d`：月中的天数（01-31）
- `%e`：月中的天数（1-31）
- `%H`：小时（00-23）
- `%h`：小时（01-12）
- `%i`：分钟（00-59）
- `%s`：秒（00-59）
- `%p`：AM 或 PM

以下是一些示例：

1. **年-月-日 时:分:秒**

   ```mysql
   SELECT DATE_FORMAT(NOW(), '%Y-%m-%d %H:%i:%s');
   ```

2. **月/日/年**

   ```mysql
   SELECT DATE_FORMAT(NOW(), '%m/%d/%Y');
   ```

3. **小时:分钟 AM/PM**

   ```mysql
   SELECT DATE_FORMAT(NOW(), '%h:%i %p');
   ```

4. **自定义格式**

   ```mysql
   SELECT DATE_FORMAT(NOW(), 'Today is %W, %M %e, %Y. The time is %h:%i %p');
   ```

在格式化字符串中，除了日期和时间格式占位符之外，你还可以包含其他文本，如空格、逗号、冒号等，以增加格式的可读性。可以根据需要自定义格式，将其应用于 `DATE_FORMAT()` 函数中。

### 5.计算日期和时间

在 MySQL 中，你可以使用一系列内置函数来进行日期和时间的计算。以下是一些常见的日期和时间计算的示例：

1. **计算两个日期之间的天数差：**
   
   ```sql
   SELECT DATEDIFF('2023-01-10', '2023-01-01');
   ```
   
2. **在日期上加上一定的天数：**
   
   ```sql
   SELECT DATE_ADD('2023-01-01', INTERVAL 7 DAY);
   ```
   
3. **在日期上减去一定的天数：**
   ```sql
   SELECT DATE_SUB('2023-01-10', INTERVAL 3 DAY);
   ```

4. **获取当前日期：**
   ```sql
   SELECT CURDATE();
   ```

5. **获取当前时间：**
   ```sql
   SELECT CURTIME();
   ```

6. **获取当前日期时间：**
   ```sql
   SELECT NOW();
   ```

7. **计算未来日期：**
   ```sql
   SELECT DATE_ADD(NOW(), INTERVAL 1 MONTH);
   ```

8. **计算过去日期：**
   ```sql
   SELECT DATE_SUB(NOW(), INTERVAL 2 WEEK);
   ```

9. **获取某一天是星期几：**
   ```sql
   SELECT DAYNAME('2023-01-10');
   ```

10. **获取某一天是月份中的第几天：**
    ```sql
    SELECT DAYOFMONTH('2023-01-10');
    ```

11. **获取某一天是一年中的第几天：**
    ```sql
    SELECT DAYOFYEAR('2023-01-10');
    ```

12. **获取某一天的月份：**
    ```sql
    SELECT MONTH('2023-01-10');
    ```

13. **获取某一天的年份：**
    ```sql
    SELECT YEAR('2023-01-10');
    ```

这些函数可以帮助你进行各种日期和时间的计算，使你能够在 SQL 查询中处理和操作日期时间数据。在使用这些函数时，请注意 MySQL 版本可能会影响某些函数的可用性或语法。

### 6.IFNULL和coalesce函数

`IFNULL` 和 `COALESCE` 都是 MySQL 中用于处理 NULL 值的函数，它们有一些相似之处，但也有一些细微的区别。

1. **`IFNULL(expr1, expr2)`：** 如果 `expr1` 不为 NULL，则返回 `expr1`；否则返回 `expr2`。
    ```sql
    SELECT IFNULL(column_name, 'N/A') FROM table_name;
    ```

2. **`COALESCE(expr1, expr2, ...)`：** 返回参数列表中第一个非 NULL 表达式的值。可以有多个参数，函数将按顺序检查，返回第一个非 NULL 的值。
   
    ```sql
    SELECT COALESCE(column_name1, column_name2, 'N/A') FROM table_name;
    ```

在使用上，这两个函数在大多数情况下是等效的，都用于提供一个默认值，以防止 NULL 值引起的问题。然而，有一些细微的区别：

- **参数个数：** `IFNULL` 只接受两个参数，而 `COALESCE` 可以接受多个参数。

- **性能：** 在某些情况下，`IFNULL` 可能比 `COALESCE` 稍微更高效，因为 `IFNULL` 只有两个参数，而 `COALESCE` 可以有多个。

- **标准兼容性：** `COALESCE` 是 SQL 标准定义的函数，而 `IFNULL` 是 MySQL 特有的。如果你的代码需要与其他数据库系统兼容，使用 `COALESCE` 更具可移植性。

在实际应用中，选择使用哪个函数通常取决于具体的需求和代码的上下文。如果只需要处理两个值，而且不考虑与其他数据库的兼容性，那么 `IFNULL` 可能更简洁。如果你的代码需要处理多个值，并且你更关心标准兼容性，那么 `COALESCE` 可能更适合。

### 7.IF函数

在 MySQL 中，`IF` 函数用于条件判断。它的语法如下：

```sql
IF(expr, true_value, false_value)
```

- `expr` 是一个条件表达式，如果为真（非零），则返回 `true_value`；如果为假（零或 NULL），则返回 `false_value`。
- `true_value` 和 `false_value` 是两个可能的返回值，取决于条件表达式的结果。

以下是一个简单的例子：

```sql
SELECT IF(5 > 3, 'true', 'false'); -- 返回 'true'
```

在这个例子中，条件表达式 `5 > 3` 为真，因此返回值为 `'true'`。

你还可以嵌套使用 `IF` 函数来处理更复杂的条件。例如：

```sql
SELECT IF(score >= 60, 'Pass', IF(score >= 40, 'Conditional Pass', 'Fail')) AS result
FROM exam_results;
```

在这个例子中，根据考试成绩，如果成绩大于等于 60，则返回 `'Pass'`，如果成绩大于等于 40 但小于 60，则返回 `'Conditional Pass'`，否则返回 `'Fail'`。

### 8.CASE运算符

`CASE` 表达式是在 SQL 中进行条件逻辑的一种方法。它类似于编程语言中的 `switch` 或 `if-else` 语句，允许你基于条件执行不同的操作。`CASE` 可以用于 `SELECT` 语句、`UPDATE` 语句和 `DELETE` 语句。

以下是 `CASE` 表达式的一般语法：

```sql
CASE
    WHEN condition1 THEN result1
    WHEN condition2 THEN result2
    ...
    ELSE default_result
END
```

- `condition1`, `condition2`, ... 是条件，用于测试输入值。
- `result1`, `result2`, ... 是在满足相应条件时返回的结果。
- `ELSE` 子句是可选的，用于指定当没有条件匹配时返回的默认结果。

以下是一个简单的例子，使用 `CASE` 在 `SELECT` 语句中：

```sql
SELECT
    student_name,
    grade,
    CASE
        WHEN grade >= 90 THEN 'A'
        WHEN grade >= 80 THEN 'B'
        WHEN grade >= 70 THEN 'C'
        WHEN grade >= 60 THEN 'D'
        ELSE 'F'
    END AS letter_grade
FROM
    student_grades;
```

在这个例子中，`CASE` 表达式根据学生成绩将其映射到字母等级。这是一个简单的条件逻辑，但你可以根据需要使用更复杂的条件。`CASE` 表达式在查询和更新时非常有用，因为它允许你动态地根据条件生成结果。

## 七.视图

### 1.创建视图

在 SQL 中，视图是一种虚拟的表，它基于一个或多个表的查询结果。视图不存储实际的数据，而是提供一种方便的方式来组织和重用查询。创建视图的语法如下：

```sql
CREATE VIEW view_name AS
SELECT column1, column2, ...
FROM table1
WHERE condition;
```

其中：

- `view_name` 是视图的名称。
- `column1, column2, ...` 是视图的列，它们可以来自一个或多个表。
- `table1` 是从中选择数据的表。
- `condition` 是可选的，用于指定选择数据的条件。

以下是一个简单的例子，创建一个名为 `employee_view` 的视图，该视图包含了 `employees` 表中满足条件的员工：

```sql
CREATE VIEW employee_view AS
SELECT employee_id, first_name, last_name, salary
FROM employees
WHERE department_id = 1;
```

一旦视图被创建，你可以像使用表一样查询它：

```sql
SELECT * FROM employee_view;
```

**视图提供了一个抽象层，使你可以隐藏底层表的细节，并根据需要组织和简化查询。**需要注意的是，**视图只是一个虚拟表，不存储实际的数据，而是根据定义的查询在运行时生成结果。**

#### 例子

```
USE sql_invoicing;

CREATE VIEW client_for_balance AS
SELECT 
    i.client_id,
    name,
    SUM(invoice_total - payment_total) AS balance
FROM invoices i
JOIN clients c USING(client_id)
GROUP BY i.client_id,name
```



### 2.更改或删除视图

在 SQL 中，你可以使用 `ALTER VIEW` 语句更改视图的定义，使用 `DROP VIEW` 语句删除视图。

#### 更改视图

要更改视图的定义，使用 `ALTER VIEW` 语句，并提供新的视图定义。例如：

```sql
ALTER VIEW employee_view AS
SELECT employee_id, first_name, last_name, salary
FROM employees
WHERE department_id = 2;
```

上述语句将 `employee_view` 视图的定义更改为选择 `department_id` 等于 2 的员工。

#### 删除视图

要删除视图，使用 `DROP VIEW` 语句，后跟视图的名称。例如：

```sql
DROP VIEW employee_view;
```

上述语句将删除名为 `employee_view` 的视图。请注意，这不会影响底层的表，只是删除了视图本身。

如果你希望在删除视图时检查是否存在视图，可以使用 `IF EXISTS`：

```sql
DROP VIEW IF EXISTS employee_view;
```

这样，如果视图存在，就会被删除，否则不会发生任何事情。

请谨慎使用 `DROP VIEW`，因为它会永久删除视图。如果你只是想暂时禁用视图，可以使用 `ALTER VIEW` 更改其定义为一个不返回任何行的查询。

### 3.可更新视图

在 SQL 中，不是所有的视图都是可更新的。可更新视图是指可以通过对视图的操作来更改底层表的数据。可更新视图必须符合一些规则，例如：

1. 视图必须是从单个表或多个表的连接中派生的。
2. 视图的 SELECT 语句不能包含以下元素：
   - 聚合函数（如 COUNT、SUM）
   - DISTINCT
   - GROUP BY 或 HAVING
   - UNION 或 UNION ALL
   - 子查询
   - FROM 子句中有多个表

如果一个视图满足这些条件，那么它就是可更新的。在进行视图上的更新操作时，数据库系统将相应的更新操作转换为基础表上的相应操作。

以下是一个创建可更新视图的简单示例：

```sql
CREATE VIEW employee_view AS
SELECT employee_id, first_name, last_name, salary
FROM employees
WHERE department_id = 1;
```

然后，你可以对 `employee_view` 视图执行更新操作：

```sql
UPDATE employee_view SET salary = salary * 1.1 WHERE employee_id = 1001;
```

这个更新操作将反映在底层的 `employees` 表中，因为 `employee_view` 是可更新的。

请注意，**可更新视图的条件相当严格，因此并非所有的视图都能够进行更新**。在设计和使用可更新视图时，请确保满足相关的规则和条件。

### 4.WITH CKECK OPTION子句

在 SQL 中，`WITH CHECK OPTION` 子句通常与创建可更新视图一起使用，以确保通过视图进行的更新操作满足视图的定义条件。

当你创建可更新视图时，可能希望确保用户通过视图插入或更新的数据仍然符合视图的定义条件。这时，你可以在创建视图的 `CREATE VIEW` 语句中添加 `WITH CHECK OPTION` 子句。

以下是一个简单的示例，创建了一个可更新的视图，并使用 `WITH CHECK OPTION`：

```sql
CREATE VIEW high_salary_employees AS
SELECT employee_id, first_name, last_name, salary
FROM employees
WHERE salary > 50000
WITH CHECK OPTION;
```

在这个例子中，`high_salary_employees` 视图只包含工资大于 50000 的员工。添加 `WITH CHECK OPTION` 子句确保任何通过视图进行的更新操作都会检查新插入或更新的行是否仍然满足 `salary > 50000` 的条件。如果不满足条件，更新操作将被拒绝。

这可以防止用户通过视图插入或更新不符合视图定义条件的数据。需要注意的是，`WITH CHECK OPTION` 仅在插入和更新操作时进行检查，而不在删除操作时进行检查，因为删除操作不涉及视图定义的条件。

这个特性有助于确保视图一直保持在用户期望的状态，并且插入或更新的数据符合定义的过滤条件。

### 5.视图的其他优点

视图在数据库中有许多优点，除了提供数据的虚拟表示外，它们还为数据库管理和应用程序开发提供了一些重要的优势：

1. **简化复杂的查询：** 视图允许将复杂的查询逻辑封装到一个单独的对象中。这使得数据库管理更加简单，应用程序代码更加清晰，而且有助于减少错误。

2. **增强安全性：** 通过视图，你可以限制用户或应用程序对底层表的访问。只提供对特定列或行的访问权限，有助于确保敏感信息的安全性。

3. **提高性能：** 在某些情况下，数据库系统可以使用视图来优化查询执行计划。通过使用视图，数据库系统可以更有效地处理查询，提高性能。

4. **简化权限管理：** 视图允许数据库管理员根据用户的角色和权限要求，创建具有适当访问级别的数据视图。这使得权限管理更加灵活。

5. **重用查询逻辑：** 如果某个查询逻辑在多个地方使用，将其封装在一个视图中可以减少代码的重复，提高代码的可维护性。

6. **隐藏数据结构变化：** 当底层表的结构发生变化时，视图可以充当一个抽象层，隐藏这些变化对应用程序的影响。这使得应用程序更加灵活和容错。

7. **支持多层架构：** 视图支持数据库设计的多层架构，使得逻辑数据模型和物理数据模型之间存在一定的隔离，提高了系统的可维护性和可扩展性。

8. **简化复杂计算：** 视图允许在查询中执行计算，将复杂的计算逻辑隐藏在视图中。这对于报表生成和业务分析非常有用。

总的来说，视图是数据库设计和应用程序开发中非常有用的工具，能够提高数据管理的灵活性、安全性和性能。

## 八.储存过程

存储过程（Stored Procedure）是在数据库中保存和执行的一组预编译的 SQL 语句。它是一种存储在数据库内部的可重复使用的程序单元，通常由 SQL 语句和流程控制语句组成。存储过程能够接受参数、执行一系列 SQL 语句，返回结果，也可以包含逻辑控制结构。

存储过程通常具有以下特点：

1. **封装性（Encapsulation）：** 存储过程将一系列 SQL 语句封装在一个单独的单元中，用户可以通过调用存储过程来执行这些语句，而无需了解其内部实现细节。

2. **参数传递：** 存储过程可以接受输入参数，允许用户在调用时传递参数值。这样可以提高存储过程的灵活性和通用性。

3. **可重用性：** 存储过程是可重复使用的，可以在多个地方被调用，而不必重新编写其代码。这有助于减少代码冗余，提高代码维护性。

4. **性能优化：** 存储过程的 SQL 语句在第一次执行时通常会被编译，并生成执行计划。这使得存储过程的执行速度相对较快，因为编译开销只发生一次。

5. **安全性：** 存储过程可以设置权限，控制对数据库的访问。用户可以通过存储过程进行数据库操作，而无需直接访问底层表，从而提高数据库的安全性。

在创建存储过程时，可以使用类似编程语言的结构，包括条件判断、循环、异常处理等，从而实现更复杂的逻辑。

示例存储过程的基本结构如下：

```sql
CREATE PROCEDURE procedure_name (parameter1 datatype, parameter2 datatype, ...)
BEGIN
    -- SQL statements
END;
```

在实际使用中，存储过程常用于完成特定的业务逻辑、数据处理和维护任务，提高数据库的整体性能和可维护性。

### 1.创建一个储存过程

创建存储过程需要使用 `CREATE PROCEDURE` 语句，并在 `BEGIN` 和 `END` 之间编写存储过程的主体部分。以下是一个简单的创建存储过程的示例，该存储过程接受两个参数，计算它们的和，并将结果返回：

```sql
DELIMITER //

CREATE PROCEDURE CalculateSum(IN a INT, IN b INT, OUT result INT)
BEGIN 
    SET result = a + b;
END //

DELIMITER ;
```

在这个例子中：

- `DELIMITER //` 用于更改语句分隔符，以允许在存储过程中使用分号。
- `CREATE PROCEDURE CalculateSum` 定义了存储过程的名称和参数。
- `IN a INT, IN b INT, OUT result INT` 定义了两个输入参数（`a` 和 `b`）和一个输出参数（`result`）。
- `BEGIN` 和 `END` 之间是存储过程的主体部分，这里简单地将 `result` 设置为 `a + b`。
- `DELIMITER ;` 恢复语句分隔符为分号。

要调用这个存储过程并获取结果，可以使用 `CALL` 语句：

```sql
CALL CalculateSum(5, 7, @sum);
SELECT @sum AS SumResult;
```

在这个例子中，`@sum` 是一个用户变量，用于存储存储过程的输出结果。存储过程计算完成后，你可以通过查询该变量来获取结果。

请注意，具体的存储过程语法和特性可能会因数据库管理系统而异。上述示例是基于 MySQL 语法的。如果你使用的是不同的数据库系统，可能需要调整语法。

#### DELIMITER 

在 SQL 中，分号 (`;`) 通常用作语句的结束符。当你在创建存储过程或触发器等包含多个 SQL 语句的结构时，SQL 解释器会将每个语句的分号视为语句的结束。然而，**如果你在存储过程或触发器等结构中使用了分号，那么解释器可能会误认为分号是语句的结束，从而导致语法错误。**

**为了解决这个问题，可以使用 `DELIMITER` 命令来更改语句分隔符，以允许在结构体中使用分号。**`DELIMITER` 是 MySQL 等一些数据库系统支持的命令。

下面是使用 `DELIMITER` 的基本步骤：

1. **更改语句分隔符：** 使用 `DELIMITER` 命令将语句分隔符更改为其他字符，例如 `//`。这使得解释器将 `//` 视为语句的结束，而不是单独的分号。

   ```sql
   DELIMITER //
   ```

2. **编写存储过程：** 在 `BEGIN` 和 `END` 之间编写存储过程的主体，可以自由使用分号。

   ```sql
   CREATE PROCEDURE SampleProcedure()
   BEGIN
       -- SQL statements;
   END //
   ```

3. **恢复语句分隔符：** 在结构体的末尾，使用 `DELIMITER ;` 恢复原始的语句分隔符。

   ```sql
   DELIMITER ;
   ```

这样，当你创建存储过程时，解释器会将 `//` 视为语句的结束，而不是分号。这允许你在存储过程中使用分号而不会导致语法错误。在执行实际的 SQL 查询时，还是使用分号作为语句的结束符。

请注意，使用 `DELIMITER` 是特定于数据库系统的，不是 SQL 标准的一部分。因此，具体的数据库系统可能有不同的方式处理这个问题。



**`DELIMITER`的使用主要是为了处理存储过程、触发器、函数等数据库对象中包含多个SQL语句的情况。当你在创建这些对象时，它们的主体可能包含多条SQL语句，而默认的SQL语句结束符是分号(`;`)。然而，MySQL解释器会在遇到分号时认为语句结束，这就导致了一个问题：当你在这些对象中使用分号时，MySQL会误以为是语句结束，从而导致语法错误。**

**通过使用`DELIMITER`，你可以改变语句结束符，将其设置为其他字符（通常是`$$`），这样在对象体中就可以自由使用分号而不引起混淆。在对象体的结束时，你可以使用`DELIMITER ;`将结束符改回分号，以确保后续SQL语句在正常的分号结束符下执行。**

**这个机制主要是为了解决语法歧义的问题，使得在对象中可以使用常见的分号，同时确保解释器能够正确地识别对象体的结束。这种技术在创建复杂的数据库对象时特别有用，因为这些对象可能需要包含多个SQL语句来完成特定的逻辑**。



#### 例子

```
DELIMITER //
CREATE PROCEDURE get_invoices_with_balance()
BEGIN
    SELECT*
    FROM invoices
    WHERE  invoice_total - payment_total > 0 ;
END //

DELIMITER ;
```

### 2.删除储存过程

要删除存储过程，可以使用 `DROP PROCEDURE` 语句。以下是删除存储过程的基本语法：

```sql
DROP PROCEDURE [IF EXISTS] procedure_name;
```

其中：

- `procedure_name` 是要删除的存储过程的名称。
- `IF EXISTS` 是一个可选的子句，如果指定了它，并且存储过程不存在，系统将不会报错。

示例：

```sql
DROP PROCEDURE IF EXISTS SampleProcedure;
```

在这个例子中，如果名为 `SampleProcedure` 的存储过程存在，它将被删除。如果不存在，不会发生错误。

请注意，删除存储过程的操作是不可逆的。确保你真的希望删除该存储过程，因为删除后将无法恢复。在实际应用中，通常在修改或删除存储过程之前，先进行备份或者仔细确认，以避免不必要的数据丢失。

### 3.带默认值的参数

在存储过程中，你可以为参数设置默认值，这样在调用存储过程时，如果不提供相应参数的值，将会使用默认值。以下是带有默认值的参数的基本语法：

```sql
CREATE PROCEDURE procedure_name(
    parameter1 datatype DEFAULT default_value,
    parameter2 datatype DEFAULT default_value,
    ...
)
BEGIN
    -- SQL statements using parameters
END;
```

其中：

- `DEFAULT` 关键字用于为参数指定默认值。
- `default_value` 是参数的默认值。

以下是一个带有默认值参数的存储过程的示例：

```sql
CREATE PROCEDURE GreetUser(
    IN user_name VARCHAR(50) DEFAULT 'Guest'
)
BEGIN
    SELECT CONCAT('Hello, ', user_name) AS greeting;
END;
```

在这个例子中，`GreetUser` 存储过程接受一个输入参数 `user_name`，并为其设置了默认值 `'Guest'`。如果调用过程时不提供 `user_name` 参数的值，将使用默认值 `'Guest'`。

调用这个存储过程的方式如下：

```sql
CALL GreetUser('John'); -- 输出：Hello, John
CALL GreetUser();        -- 输出：Hello, Guest
```

在实际应用中，带有默认值的参数使得存储过程更加灵活，调用者可以选择性地提供参数值，而不必为每个参数都提供值。

### 4.参数验证

在存储过程中，参数的验证是确保传递给存储过程的数据符合期望格式和条件的一种方式。这有助于提高存储过程的健壮性和安全性。以下是一些常见的参数验证方法：

1. **空值检查：** 确保输入参数不为空，特别是对于不允许为空的参数。

   ```sql
   CREATE PROCEDURE ExampleProcedure(
       IN input_parameter VARCHAR(255)
   )
   BEGIN
       -- 空值检查
       IF input_parameter IS NULL THEN
           SIGNAL SQLSTATE '45000'
           SET MESSAGE_TEXT = 'Input parameter cannot be null';
       END IF;

       -- 存储过程的其他逻辑
   END;
   ```

2. **数据类型检查：** 针对输入参数，确保其数据类型符合预期。

   ```sql
   CREATE PROCEDURE ExampleProcedure(
       IN input_parameter INT
   )
   BEGIN
       -- 数据类型检查
       IF input_parameter IS NOT NULL AND NOT input_parameter BETWEEN 1 AND 100 THEN
           SIGNAL SQLSTATE '45000'
           SET MESSAGE_TEXT = 'Input parameter must be an integer between 1 and 100';
       END IF;

       -- 存储过程的其他逻辑
   END;
   ```

3. **范围检查：** 针对数字类型的输入参数，确保其值在有效范围内。

   ```sql
   CREATE PROCEDURE ExampleProcedure(
       IN age INT
   )
   BEGIN
       -- 范围检查
       IF age IS NOT NULL AND NOT age BETWEEN 0 AND 120 THEN
           SIGNAL SQLSTATE '45000'
           SET MESSAGE_TEXT = 'Age must be between 0 and 120';
       END IF;

       -- 存储过程的其他逻辑
   END;
   ```

4. **长度检查：** 针对字符串类型的输入参数，确保其长度在有效范围内。

   ```sql
   CREATE PROCEDURE ExampleProcedure(
       IN name VARCHAR(50)
   )
   BEGIN
       -- 长度检查
       IF name IS NOT NULL AND LENGTH(name) > 50 THEN
           SIGNAL SQLSTATE '45000'
           SET MESSAGE_TEXT = 'Name must be up to 50 characters';
       END IF;
   
       -- 存储过程的其他逻辑
   END;
   ```

这些验证方法可以根据存储过程的具体需求进行调整。在存储过程中，使用条件语句和 `SIGNAL` 语句可以生成自定义的错误消息，以便更好地说明验证失败的原因。这样可以确保存储过程只接受符合条件的输入参数。

### 5.输出参数

输出参数允许存储过程将计算的结果返回给调用者。在存储过程中，你可以使用 `OUT` 关键字来定义输出参数。以下是一个带有输出参数的简单存储过程的示例：

```sql
CREATE PROCEDURE CalculateSumAndProduct(
    IN a INT,
    IN b INT,
    OUT sum_result INT,
    OUT product_result INT
)
BEGIN
    SET sum_result = a + b;
    SET product_result = a * b;
END;
```

在这个例子中，存储过程 `CalculateSumAndProduct` 接受两个输入参数 `a` 和 `b`，并定义了两个输出参数 `sum_result` 和 `product_result`。在存储过程的主体内，计算了输入参数的和和积，并将结果分别赋值给输出参数。

调用这个存储过程的方式如下：

```sql
CALL CalculateSumAndProduct(5, 7, @sum, @product);
SELECT @sum AS SumResult, @product AS ProductResult;
```

在这个例子中，`@sum` 和 `@product` 是用于接收存储过程计算结果的用户变量。在调用过程结束后，你可以查询这些变量以获取存储过程的输出值。

需要注意的是，在调用存储过程时，需要为输出参数提供变量来接收结果。这些变量可以是用户变量（使用 `@` 符号），也可以是存储过程的参数。



#### INTO

在MySQL存储过程中，`INTO`是一个关键字，通常与`SELECT`语句结合使用，用于将`SELECT`语句的结果存储到一个或多个变量中。这主要用于将查询的结果集中的某些值赋给存储过程中定义的变量。

以下是一个基本的例子，演示了`INTO`的使用：

```sql
CREATE PROCEDURE example_procedure()
BEGIN
    DECLARE var1 INT;
    DECLARE var2 VARCHAR(255);

    -- 使用 SELECT INTO 将查询结果存储到变量中
    SELECT column1, column2 INTO var1, var2
    FROM my_table
    WHERE some_condition;

    -- 在后续逻辑中使用变量
    INSERT INTO another_table (columnA, columnB) VALUES (var1, var2);
END;
```

在这个例子中，`SELECT column1, column2 INTO var1, var2`语句执行了一个查询，将`my_table`中符合`some_condition`条件的一行的`column1`和`column2`的值分别存储到`var1`和`var2`变量中。然后，可以在存储过程的后续逻辑中使用这些变量，例如将它们插入到另一个表中。

注意几点：

1. **变量声明：** 在存储过程开始部分，你需要先声明变量。在上面的例子中，使用`DECLARE var1 INT;`和`DECLARE var2 VARCHAR(255);`声明了两个变量。

2. **SELECT INTO 语法：** `SELECT column1, column2 INTO var1, var2`的语法表示将查询结果中的列值赋给相应的变量。

3. **查询条件：** `WHERE some_condition`是一个查询条件，用于过滤出符合条件的行。

总的来说，`INTO`关键字在存储过程中的使用是为了从查询结果中选择特定列的值，并将这些值存储到事先声明的变量中，以便在存储过程的后续逻辑中使用。



### 6.变量

在存储过程中，你可以使用变量来存储和操作数据。变量是一种命名的存储位置，用于存储和处理数据值。以下是在存储过程中使用变量的基本语法：

```sql
DECLARE variable_name datatype [DEFAULT default_value];
```

其中：

- `variable_name` 是变量的名称。
- `datatype` 是变量的数据类型。
- `DEFAULT default_value` 是可选的，用于指定变量的默认值。

以下是一个简单的存储过程，演示如何声明和使用变量：

```sql
CREATE PROCEDURE ExampleProcedure()
BEGIN
    -- 声明变量
    DECLARE user_name VARCHAR(50) DEFAULT 'Guest';
    DECLARE age INT;

    -- 设置变量值
    SET age = 25;

    -- 使用变量
    SELECT CONCAT('Hello, ', user_name, '! You are ', age, ' years old.') AS greeting;
END;
```

在这个例子中：

- `DECLARE user_name VARCHAR(50) DEFAULT 'Guest';` 声明了一个名为 `user_name` 的字符串类型变量，初始值为 `'Guest'`。
- `DECLARE age INT;` 声明了一个名为 `age` 的整数类型变量。
- `SET age = 25;` 设置了变量 `age` 的值为 `25`。
- 在 `SELECT` 语句中使用了这两个变量。

变量在存储过程中用于临时存储数据，可以在存储过程的执行过程中进行读取和修改。它们对于执行复杂的计算、存储临时结果以及简化代码逻辑非常有用。需要注意，变量的作用域通常限于声明它们的存储过程，无法在其他存储过程中直接访问。

### 7.函数

用户自定义函数（User-Defined Functions，简称UDF）是在MySQL数据库中由用户创建的、可重用的自定义函数。这些函数允许用户将一系列SQL语句封装到一个函数中，从而提高代码的可维护性和可重用性。用户可以根据自己的需求创建自定义函数，并在存储过程、触发器、查询等中使用它们。

以下是创建和使用用户自定义函数的基本步骤：

#### 创建用户自定义函数：

```sql
CREATE FUNCTION function_name (parameter1 datatype, parameter2 datatype, ...)
RETURNS return_datatype
BEGIN
    -- 函数体，包含一系列SQL语句
    -- 可以包括条件、循环、变量等逻辑
    DECLARE variable_name datatype;
    -- 一些操作，可能包括返回值的计算
    RETURN calculated_value;
END;
```

- `function_name` 是函数的名称。
- `(parameter1 datatype, parameter2 datatype, ...)` 是函数的输入参数列表，可以有零个或多个参数。
- `RETURNS return_datatype` 指定函数的返回类型。
- `BEGIN` 和 `END` 之间是函数体，包含一系列SQL语句，变量声明，逻辑等。
- `DECLARE variable_name datatype;` 用于声明函数中使用的变量。
- `RETURN calculated_value;` 用于返回函数的计算结果。

#### 示例：

以下是一个简单的用户自定义函数，用于计算两个整数的和：

```sql
CREATE FUNCTION add_numbers(x INT, y INT)
RETURNS INT
BEGIN
    DECLARE result INT;
    SET result = x + y;
    RETURN result;
END;
```

#### 使用用户自定义函数：

```sql
-- 调用用户自定义函数
SELECT add_numbers(5, 7) AS sum_result;
```

在这个例子中，`add_numbers` 函数接受两个整数参数，并返回它们的和。在实际使用中，你可以在查询语句中调用这个函数，得到计算的结果。

总体而言，用户自定义函数是MySQL中强大的工具，可以帮助提高代码的模块化程度、可读性和可维护性。用户可以根据业务逻辑需求创建不同类型的自定义函数，从而更有效地利用数据库功能。

## 九.触发器和事件

### 1.触发器

触发器是与表相关联的一种特殊类型的存储过程，它在表上执行特定的动作（触发事件）时自动触发。这些动作可以包括插入、更新或删除记录。触发器是在数据库中实现数据完整性和业务规则的强大工具。

以下是一些关于触发器的基本概念和使用方法：

#### 触发器的创建语法：

触发器的创建使用 `CREATE TRIGGER` 语句：

```sql
CREATE TRIGGER trigger_name
BEFORE/AFTER INSERT/UPDATE/DELETE
ON table_name
FOR EACH ROW
BEGIN
    -- 触发器的逻辑
END;
```

- `trigger_name` 是触发器的名称。
- `BEFORE` 或 `AFTER` 指定触发器在触发事件之前或之后执行。
- `INSERT`、`UPDATE`、`DELETE` 指定触发器在执行相应的操作之前或之后触发。
- `ON table_name` 指定触发器与哪个表关联。
- `FOR EACH ROW` 表示触发器对表的每一行记录执行一次。

#### 触发器的事件：

1. **BEFORE INSERT：** 在插入新记录之前触发。
2. **AFTER INSERT：** 在插入新记录之后触发。
3. **BEFORE UPDATE：** 在更新记录之前触发。
4. **AFTER UPDATE：** 在更新记录之后触发。
5. **BEFORE DELETE：** 在删除记录之前触发。
6. **AFTER DELETE：** 在删除记录之后触发。

#### 触发器中的OLD和NEW：

在数据库中，当你插入、更新或删除一行数据时，触发器可以捕捉这些事件，并在事件发生前（BEFORE）或发生后（AFTER）执行一些操作。在这个过程中，你可能需要引用被改变的行的旧值（发生前）或新值（发生后）。

- `NEW` 关键字：用于引用触发器事件后的新值。比如，在 `AFTER INSERT` 和 `AFTER UPDATE` 事件中，你可以使用 `NEW` 来引用已经插入或已经更新的新行的值。

- `OLD` 关键字：用于引用触发器事件前的旧值。在 `BEFORE UPDATE` 和 `BEFORE DELETE` 事件中，你可以使用 `OLD` 来引用即将更新或即将删除的旧行的值。

让我们看一个简单的例子：

```sql
CREATE TRIGGER example_trigger
BEFORE UPDATE ON my_table
FOR EACH ROW
BEGIN
    -- 使用 OLD 和 NEW 进行比较和操作
    IF OLD.column1 <> NEW.column1 THEN
        -- 在这里执行逻辑，例如记录日志或修改其他字段
    END IF;
END;
```

在这个例子中，触发器在更新 `my_table` 表的操作之前执行。在触发器内部，通过比较 `OLD.column1` 和 `NEW.column1` 的值，你可以执行一些逻辑。这个逻辑可以是记录日志、修改其他字段等。这就是 `OLD` 和 `NEW` 关键字在触发器中的基本用法。

#### 触发器的应用场景：

1. **数据完整性：** 通过触发器，可以在插入、更新或删除记录时执行额外的检查，以确保数据的完整性。
  
2. **自动记录变更：** 可以使用触发器记录表的变更历史，例如，创建一个触发器在记录被更新时将变更写入日志表。

3. **复杂业务规则：** 触发器可以用于实施复杂的业务规则，如计算字段值、数据转换等。

4. **防止非法操作：** 可以使用触发器阻止执行某些非法的操作，以维护业务规则。

#### 示例：

下面是一个简单的触发器示例，用于在插入记录之前更新一个时间戳字段：

```sql
CREATE TRIGGER before_insert_trigger
BEFORE INSERT
ON my_table
FOR EACH ROW
SET NEW.create_time = NOW();
```

在这个例子中，`before_insert_trigger` 触发器在每次插入新记录之前将 `create_time` 字段设置为当前时间。

触发器是数据库中强大的工具，但应慎重使用，确保合理并考虑其对性能的影响。

#### 示例:

```mysql
USE sql_invoicing;


DELIMITER $$

CREATE TRIGGER payments_after_insert
    AFTER INSERT ON payments
    FOR EACH ROW
BEGIN
    UPDATE invoices
    SET payment_total = payment_total + NEW.amount
    WHERE invoice_id = NEW.invoice_id;
END $$

DELIMITER ;

```

你提供的 SQL 代码是一个触发器，它在 `payments` 表中的插入操作之后触发。具体来说，这个触发器用于在 `invoices` 表中更新 `payment_total` 列，将其增加新插入的 `payments` 表中的 `amount` 列的值，这是一种在两个表之间保持关联数据的常见做法。

让我解释一下你的触发器代码：

1. **触发器定义：**
   - `CREATE TRIGGER payments_after_insert`：定义了触发器的名称为 `payments_after_insert`。
   - `AFTER INSERT ON payments`：指定了触发器在 `payments` 表中发生插入操作之后触发。
   - `FOR EACH ROW`：表示触发器对每一行执行一次。

2. **触发器逻辑：**
   - `BEGIN` 和 `END` 之间的部分是触发器的逻辑。
   - `UPDATE invoices ...`：这是触发器执行的 SQL 语句。它更新了 `invoices` 表中的 `payment_total` 列。
   - `SET payment_total = payment_total + NEW.amount`：这一行的作用是将 `payment_total` 列的值增加新插入的 `payments` 表中的 `amount` 列的值。
   - `WHERE invoice_id = NEW.invoice_id`：这个条件确保只有与新插入的 `payments` 行相关联的 `invoices` 行被更新。这是通过 `invoice_id` 列的匹配来实现的。

3. **DELIMITER 的使用：**
   - `DELIMITER $$` 和 `DELIMITER ;` 之间的代码是用于改变语句分隔符，因为触发器中包含了多个语句，而默认的语句分隔符是分号 (`;`)。在这个例子中，将分隔符改为 `$$`，并在触发器代码结束后将其还原为分号。

这个触发器的作用是在插入到 `payments` 表后，自动更新关联的 `invoices` 表中的 `payment_total` 列，以反映最新的支付总额。这是一个常见的数据库设计实践，确保数据的一致性。

#### 示例:

```mysql
USE sql_invoicing;

DELIMITER $$

CREATE TRIGGER payment_after__delete
    AFTER DELETE ON payments
    FOR EACH ROW 
BEGIN
    UPDATE invoices
    SET payment_total = payment_total - OLD.amount
    WHERE invoice_id = OLD.invoice_id;
END $$

DELIMITER ;
```

### 2.查看触发器

在 MySQL 中，你可以使用 `SHOW TRIGGERS` 或 `SHOW CREATE TRIGGER` 语句来查看触发器的信息。

#### 1. 使用 `SHOW TRIGGERS`：

这个语句可以显示数据库中所有表的触发器信息。语法如下：

```sql
SHOW TRIGGERS [FROM database_name] [LIKE 'pattern'];
```

- `database_name`：可选，用于指定数据库的名称。
- `pattern`：可选，用于指定触发器名称的匹配模式。

示例：

```sql
SHOW TRIGGERS FROM my_database;
```

#### 2. 使用 `SHOW CREATE TRIGGER`：

这个语句可以显示指定触发器的创建语句，包括触发器的详细定义。语法如下：

```sql
SHOW CREATE TRIGGER trigger_name;
```

- `trigger_name`：指定要查看的触发器的名称。

示例：

```sql
SHOW CREATE TRIGGER my_trigger;
```

这将返回一个包含触发器详细信息的结果集，其中包括触发器的名称、事件、表名、触发时机、触发器的创建语句等。

注意：你需要有足够的权限才能查看触发器信息。如果你无法查看触发器，可能是由于权限不足。在这种情况下，你需要联系数据库管理员获取相应的权限。

### 3.删除触发器

在 MySQL 中，你可以使用 `DROP TRIGGER` 语句来删除触发器。以下是删除触发器的基本语法：

```sql
DROP TRIGGER [IF EXISTS] [schema_name.]trigger_name;
```

- `IF EXISTS`：可选项，如果触发器存在，则执行删除；如果不存在，不报错。
- `schema_name`：可选项，用于指定触发器所属的数据库模式（数据库名称）。
- `trigger_name`：指定要删除的触发器的名称。

示例：

```sql
-- 删除触发器，如果存在的话
DROP TRIGGER IF EXISTS my_trigger;

-- 删除指定数据库中的触发器
DROP TRIGGER my_database.my_trigger;
```

请谨慎使用 `DROP TRIGGER` 命令，因为删除触发器会导致相关触发器的逻辑不再执行。确保你真的希望删除触发器，并理解删除后可能的影响。

在执行 `DROP TRIGGER` 命令之前，最好先使用 `SHOW CREATE TRIGGER` 来查看触发器的定义，以确保你删除的是正确的触发器。

### 4.审计

审计是记录数据库操作以便后续分析和追踪的一种常见数据库管理实践。通过使用触发器，你可以实现对数据库表的审计，记录哪些数据发生了变化，以及变化的细节。以下是一个简单的示例，演示如何使用触发器进行审计：

假设有一个表 `employees`：

```sql
CREATE TABLE employees (
    id INT PRIMARY KEY,
    name VARCHAR(255),
    salary DECIMAL(10, 2)
);
```

现在，我们希望创建一个触发器，以记录所有对 `employees` 表的插入、更新和删除操作。

```sql
-- 创建用于审计的表
CREATE TABLE audit_log (
    id INT AUTO_INCREMENT PRIMARY KEY,
    action VARCHAR(50),
    table_name VARCHAR(50),
    record_id INT,
    field_name VARCHAR(50),
    old_value VARCHAR(255),
    new_value VARCHAR(255),
    audit_timestamp TIMESTAMP DEFAULT CURRENT_TIMESTAMP
);

-- 创建触发器，用于记录插入操作
CREATE TRIGGER employees_after_insert
AFTER INSERT ON employees
FOR EACH ROW
INSERT INTO audit_log (action, table_name, record_id, new_value)
VALUES ('INSERT', 'employees', NEW.id, CONCAT('Name: ', NEW.name, ', Salary: ', NEW.salary));

-- 创建触发器，用于记录更新操作
CREATE TRIGGER employees_after_update
AFTER UPDATE ON employees
FOR EACH ROW
INSERT INTO audit_log (action, table_name, record_id, field_name, old_value, new_value)
VALUES ('UPDATE', 'employees', NEW.id, 'Salary', OLD.salary, NEW.salary);

-- 创建触发器，用于记录删除操作
CREATE TRIGGER employees_after_delete
AFTER DELETE ON employees
FOR EACH ROW
INSERT INTO audit_log (action, table_name, record_id, old_value)
VALUES ('DELETE', 'employees', OLD.id, CONCAT('Name: ', OLD.name, ', Salary: ', OLD.salary));
```

在这个示例中：

- 我们创建了一个名为 `audit_log` 的表，用于存储审计日志。
- 然后，我们创建了三个触发器，分别在插入、更新和删除操作之后执行。
- 这些触发器将相应的审计信息插入到 `audit_log` 表中，包括操作类型（INSERT、UPDATE、DELETE）、表名、记录ID、字段名、旧值、新值和审计时间戳。

请注意，这只是一个简单的例子，实际的审计需求可能更加复杂，根据具体情况可能需要记录更多的信息。此外，审计日志表的设计和存储方式可能会因实际需求而有所不同。

### 5.事件

在MySQL中，事件（Events）是一种**用于在预定时间执行某些操作的机制。**MySQL事件允许你在数据库中调度和执行一系列的SQL语句或存储过程。这对于执行周期性任务或自动化某些数据库操作非常有用。

让我们详细解释MySQL事件中涉及的关键字，并提供一些具体的例子：

1. **`CREATE EVENT`：** 用于创建事件的关键字。

   ```sql
   CREATE EVENT event_name
   ON SCHEDULE schedule
   DO
   BEGIN
       -- SQL statements to be executed
   END;
   ```

   - `event_name`：事件的名称，唯一标识一个事件。
   - `ON SCHEDULE`：定义事件何时执行的部分。
   - `BEGIN ... END`：在这个部分中放置要在事件触发时执行的SQL语句。

   **例子：** 创建一个每天执行一次的事件。

   ```sql
   CREATE EVENT daily_cleanup
   ON SCHEDULE
       EVERY 1 DAY
   DO
   BEGIN
       -- SQL statements for daily cleanup
   END;
   ```

2. **`ON SCHEDULE`：** 用于定义事件执行时间表的子句。

   ```sql
   ON SCHEDULE
   EVERY interval
   STARTS timestamp
   ENDS timestamp
   ```

   - `EVERY interval`：定义事件执行的间隔，可以是`1 DAY`、`1 HOUR`等。
   - `STARTS timestamp`：定义事件的开始时间。
   - `ENDS timestamp`：定义事件的结束时间。

   **例子：** 创建一个每周一次的事件。

   ```sql
   ON SCHEDULE
       EVERY 1 WEEK
   STARTS '2023-01-01 00:00:00'
   ENDS '2023-12-31 23:59:59'
   ```

#### 示例:

```mysql
DELIMITER $$

CREATE EVENT yearly_delete_stale_audit_rows
ON SCHEDULE
    -- AT '2019-05-01'
    EVERY 1 YEAR STARTS '2019-01-01' ENDS '2029-01-01'
DO BEGIN
    DELETE FROM payments_audit
    WHERE action_date < NOW() - INTERVAL 1 YEAR ;
END $$

DELIMITER ;
```

在 MySQL 中，查看、删除和更改事件的操作可以通过使用以下命令完成：

#### 1. 查看事件：

使用 `SHOW EVENTS` 命令来查看数据库中所有的事件。

```sql
SHOW EVENTS;
```

#### 2. 删除事件：

使用 `DROP EVENT` 命令来删除指定的事件。

```sql
DROP EVENT [IF EXISTS] event_name;
```

- `IF EXISTS`：可选，如果事件存在则执行删除，如果不存在则不报错。
- `event_name`：指定要删除的事件的名称。

示例：

```sql
DROP EVENT IF EXISTS yearly_delete_stale_audit_rows;
```

#### 3. 更改事件：

更改事件通常意味着修改事件的定义。你需要先删除旧的事件，然后重新创建一个新的事件。

例如，如果你想更改 `yearly_delete_stale_audit_rows` 事件的调度规则，你可以这样做：

```sql
-- 删除旧的事件
DROP EVENT IF EXISTS yearly_delete_stale_audit_rows;

-- 创建新的事件
CREATE EVENT yearly_delete_stale_audit_rows
ON SCHEDULE
    EVERY 1 YEAR STARTS '2020-01-01' ENDS '2030-01-01'
DO BEGIN
    DELETE FROM payments_audit
    WHERE action_date < NOW() - INTERVAL 1 YEAR;
END;
```

在这个例子中，删除了旧的事件并创建了一个新的事件，更新了事件的调度规则。

请注意，更改事件时需要小心，确保你了解事件的定义以及修改可能带来的影响。

## 十.事务与并发

### 1.事务

在数据库管理中，"事务"（Transaction）是一组数据库操作，这些操作要么全部执行成功，要么全部执行失败。事务通常用于确保数据库的一致性和完整性。

事务具有四个基本特性，通常被称为 ACID 特性：

1. **原子性（Atomicity）：** 事务是一个原子操作单元，要么全部执行成功，要么全部回滚到事务开始前的状态，没有中间状态。

2. **一致性（Consistency）：** 事务在执行前后，数据库的状态应保持一致。如果事务执行成功，数据库从一个一致的状态转移到另一个一致的状态。

3. **隔离性（Isolation）：** 多个事务并发执行时，每个事务的执行应该相互隔离，互不干扰。即使多个事务同时执行，每个事务都应该认为它是唯一在执行的事务。

4. **持久性（Durability）：** 一旦事务提交，它对数据库的改变应该是永久性的，即使系统崩溃也不会丢失。

在关系型数据库中，通过使用 `BEGIN TRANSACTION`（或简写的 `BEGIN`）开始事务，`COMMIT` 提交事务，`ROLLBACK` 回滚事务。以下是一个简单的示例：

```sql
-- 开始事务
BEGIN;

-- 执行一系列数据库操作
INSERT INTO users (id, name) VALUES (1, 'John');
UPDATE accounts SET balance = balance - 100 WHERE user_id = 1;

-- 提交事务
COMMIT;
```

如果在事务中的任何地方发生错误或者执行 `ROLLBACK`，那么整个事务将回滚到事务开始前的状态。这确保了事务的一致性和完整性。

事务的使用可以确保数据库操作的可靠性，特别是在涉及多个操作的复杂业务逻辑中。

### 2.创建事务

在关系型数据库中，创建事务通常涉及使用事务的开始、提交和回滚语句。以下是一个简单的示例，演示如何在 MySQL 中创建和使用事务：

```sql
-- 开始事务
START TRANSACTION;

-- 执行一系列数据库操作
INSERT INTO users (id, name) VALUES (1, 'John');
UPDATE accounts SET balance = balance - 100 WHERE user_id = 1;

-- 提交事务
COMMIT;
```

在上面的示例中，`START TRANSACTION;` 表示事务的开始。在事务中，可以执行多个 SQL 语句，这些语句将作为一个原子操作单元进行处理。在这个例子中，包括了插入用户记录和更新账户余额两个数据库操作。

如果在事务执行期间出现错误，或者你想要取消事务并回滚到事务开始前的状态，可以使用 `ROLLBACK;` 语句：

```sql
-- 回滚事务
ROLLBACK;
```

这将取消在事务开始后的所有数据库更改，并将数据库恢复到事务开始前的状态。

请注意，事务的使用通常涉及到错误处理，以确保在发生错误时能够正确地回滚事务。在实际应用中，你可能会将事务结合使用在存储过程、触发器、应用程序代码等不同的上下文中。

### 3.并发与锁定

并发和锁定是数据库系统中两个重要且密切相关的概念，涉及到多个用户或进程同时访问数据库的情况。

#### 并发（Concurrency）：

并发是指在同一时间间隔内处理多个事务或操作的能力。数据库系统通常支持多个用户或进程并发地执行数据库操作，这有助于提高系统的性能和响应速度。并发能够同时服务多个用户，提高系统资源利用率。

但并发也带来了一些问题，主要是由于多个事务同时对数据库进行读写可能导致数据的不一致性。因此，需要使用锁定机制来确保在某一时刻只有一个事务能够修改某一数据。

#### 锁定（Locking）：

锁定是一种用于管理并发访问的机制。它通过在数据上设置锁，阻止其他事务对相同数据的并发访问，从而确保事务的隔离性和一致性。锁定分为共享锁和排他锁：

- **共享锁（Shared Lock）：** 允许多个事务同时获取读取访问权限，但不允许任何事务获取写入访问权限。

- **排他锁（Exclusive Lock）：** 仅允许一个事务获取写入访问权限，其他事务无法同时获取读取或写入访问权限。

锁定的粒度可以是整个表、行、页面或其他更小的数据单元，具体取决于数据库系统和应用的设计。

#### 并发控制（Concurrency Control）：

为了保证并发执行的正确性，数据库系统通常使用并发控制机制。其中一个重要的并发控制技术是事务隔离级别，它定义了事务之间的隔离程度，包括读未提交、读提交、可重复读和串行化等级别。

在实践中，合理的并发控制和锁定策略是确保数据库系统能够同时提供高性能和数据一致性的关键。选择适当的隔离级别和锁定策略是数据库设计和性能调优的一个重要方面。

### 4.并发问题

并发问题是在多用户或多进程同时访问数据库时可能出现的一系列挑战。这些问题可能导致数据的不一致性、丢失更新、死锁等情况。以下是一些常见的并发问题：

1. **丢失更新（Lost Update）：** 当两个事务同时读取相同的数据并尝试更新时，最后提交的事务的更改可能会覆盖先前提交的事务的更改，导致其中一个事务的更新被丢失。

2. **脏读（Dirty Read）：** 一个事务读取了另一个事务尚未提交的未提交数据。如果另一个事务后来回滚，读取的数据就是无效的。

3. **不可重复读（Non-repeatable Read）：** 一个事务在读取某个数据后，另一个事务修改了该数据并进行了提交，导致第一个事务再次读取相同数据时得到了不同的值。

4. **幻读（Phantom Read）：** 一个事务在读取一组数据后，另一个事务插入了新的数据行或删除了已存在的数据行，导致第一个事务再次读取相同数据时发现数据集不同。

5. **死锁（Deadlock）：** 两个或多个事务相互等待对方释放锁资源，导致系统无法继续执行。这是一种致命的并发问题，需要通过死锁检测和解决机制来解决。

### 处理并发问题的方法：

1. **锁定机制：** 使用锁定来控制对共享资源的访问。根据需要选择共享锁和排他锁，以确保数据的一致性和隔离性。

2. **事务隔离级别：** 通过设置适当的事务隔离级别来控制事务之间的可见性，如读未提交、读提交、可重复读和串行化。

3. **乐观并发控制：** 使用版本控制或时间戳机制，允许事务并发执行，但在提交时检查是否有冲突。

4. **死锁检测和解决：** 实现死锁检测机制，并在检测到死锁时进行解锁或回滚操作。

5. **并发控制算法：** 使用先进的并发控制算法，如多版本并发控制（MVCC），以提高性能并减少锁的争夺。

处理并发问题需要综合考虑系统的性能需求和数据的一致性要求，并选择适当的并发控制策略。

### 5.事务隔离级别

事务隔离级别是数据库系统中用于控制事务之间可见性的一种机制。SQL 标准定义了四个事务隔离级别，每个级别提供了不同程度的隔离。这些隔离级别分别是：

1. **读未提交（Read Uncommitted）：**
   - 允许一个事务读取另一个事务尚未提交的数据。
   - 最低的隔离级别，存在脏读、不可重复读和幻读的风险。

2. **读提交（Read Committed）：**
   - 一个事务只能读取已提交的其他事务的数据。
   - 防止脏读，但仍可能出现不可重复读和幻读。

3. **可重复读（Repeatable Read）：**
   - 事务在整个过程中能看到一个快照，确保在事务执行期间同一查询的结果是一致的。
   - 防止脏读和不可重复读，但仍可能出现幻读。

4. **串行化（Serializable）：**
   - 最高的隔离级别，确保事务串行执行，彻底防止脏读、不可重复读和幻读。
   - 通常通过锁定数据来实现，可能会导致性能下降。

这些隔离级别提供了不同的权衡，更高的隔离级别通常会导致更多的锁定和性能开销。选择适当的隔离级别取决于应用程序的需求，需要在数据一致性和性能之间进行权衡。

在 SQL 中，可以使用以下语句设置事务隔离级别：

```sql
SET TRANSACTION ISOLATION LEVEL isolation_level;
```

其中 `isolation_level` 可以是 `READ UNCOMMITTED`、`READ COMMITTED`、`REPEATABLE READ` 或 `SERIALIZABLE`。例如：

```sql
-- 设置事务隔离级别为可重复读
SET TRANSACTION ISOLATION LEVEL REPEATABLE READ;
```

需要注意的是，不同的数据库系统对事务隔离级别的实现可能存在差异，因此在具体的数据库系统中查阅相关文档是推荐的。



当使用不同的事务隔离级别时，会影响并发问题的发生和解决方式。以下是重新调整位置的表格，展示了各种并发问题在不同事务隔离级别下的表现和解决方式：

| 事务隔离级别                 | 脏读（Dirty Read） | 不可重复读（Non-repeatable Read） | 幻读（Phantom Read） | 死锁（Deadlock） |
| ---------------------------- | ------------------ | --------------------------------- | -------------------- | ---------------- |
| 读未提交（Read Uncommitted） | 防不住             | 防不住                            | 防不住               | 可能             |
| 读提交（Read Committed）     | 防止               | 可能                              | 可能                 | 可能             |
| 可重复读（Repeatable Read）  | 防止               | 防止                              | 可能                 | 可能             |
| 串行化（Serializable）       | 防止               | 防止                              | 防止                 | 最小化可能性     |

- **脏读（Dirty Read）：** 允许一个事务读取另一个事务尚未提交的数据。

- **不可重复读（Non-repeatable Read）：** 一个事务在读取某个数据后，另一个事务修改了该数据并进行了提交，导致第一个事务再次读取相同数据时得到了不同的值。

- **幻读（Phantom Read）：** 一个事务在读取一组数据后，另一个事务插入了新的数据行或删除了已存在的数据行，导致第一个事务再次读取相同数据时发现数据集不同。

- **死锁（Deadlock）：** 两个或多个事务相互等待对方释放锁资源，导致系统无法继续执行。死锁的可能性在各隔离级别下是最小化的，但在 Serializable 级别下，可能性最小。

### 6.死锁

死锁是数据库中一个常见的并发问题，它发生在两个或多个事务相互等待对方释放资源的情况下，导致系统无法继续执行。每个事务都持有对方需要的资源，并且同时等待对方释放资源，从而形成了一个闭环，无法继续进行。

死锁的情境可以通过以下步骤来理解：

1. **事务 A 持有资源 X，请求资源 Y。**
2. **事务 B 持有资源 Y，请求资源 X。**

在这种情况下，如果事务 A 和事务 B 同时尝试获取对方持有的资源，就可能发生死锁。当这种互相等待的情况发生时，系统就陷入了死锁状态，不再有可用的资源，无法继续进行事务的执行。

为了解决死锁，数据库管理系统通常采用以下策略：

1. **超时机制（Timeouts）：** 允许事务在一定时间内等待对方释放资源，如果等待时间超过预定的阈值，则中断事务，放弃获取资源。

2. **死锁检测和回滚（Deadlock Detection and Rollback）：** 系统周期性地检测是否存在死锁，一旦检测到死锁，系统会选择回滚其中的某个事务，以解除死锁。

3. **事务优先级（Transaction Priority）：** 给事务分配不同的优先级，当死锁发生时，系统选择回滚优先级较低的事务，以最小化对业务的影响。

4. **等待图解锁（Wait-for Graph）：** 系统维护一个等待图，根据图的结构来判断是否存在死锁，以及如何解除死锁。

5. **避免死锁（Deadlock Avoidance）：** 在事务进行资源请求之前，系统会评估是否有可能引发死锁，如果可能，则拒绝或推迟其中一个事务的请求。

6. **锁超时（Lock Timeout）：** 设置锁的超时时间，如果在规定时间内未能获取锁，则放弃事务。

避免死锁是数据库系统设计和管理中的一个重要方面，不同的数据库系统可能采用不同的策略来处理和避免死锁。

## 十一.数据类型

### 1.字符串类型

在数据库中，字符串是一种常见的数据类型，用于存储文本数据。不同的数据库管理系统可能支持不同的字符串类型，但其中一些常见的字符串类型包括：

1. **CHAR(n)：**
   - 固定长度的字符串类型，存储指定长度的字符。
   - 例如，`CHAR(10)` 表示存储长度为 10 的字符。

2. **VARCHAR(n)：**
   - 可变长度的字符串类型，存储可变长度的字符。
   - 例如，`VARCHAR(255)` 表示存储最大长度为 255 的字符，但实际存储的长度可以根据数据内容而变化。

3. **TEXT：**
   - 用于存储大量文本数据的字符串类型，通常不限定长度。
   - 适用于存储较长的字符串，比如文章、博客内容等。

4. **BINARY(n)：**
   - 固定长度的二进制字符串类型，存储指定长度的二进制数据。
   - 例如，`BINARY(16)` 表示存储长度为 16 的二进制数据。

5. **VARBINARY(n)：**
   - 可变长度的二进制字符串类型，存储可变长度的二进制数据。
   - 例如，`VARBINARY(255)` 表示存储最大长度为 255 的二进制数据，但实际存储的长度可以根据数据内容而变化。

6. **BLOB：**
   - 用于存储大量二进制数据的字符串类型，通常不限定长度。
   - 适用于存储较大的二进制数据，比如图片、音频等。

这只是一些常见的字符串类型，实际上，不同的数据库系统可能还支持其他字符串类型，具体取决于数据库的实现和版本。在使用字符串类型时，需要根据实际需求选择合适的类型，并考虑存储空间、性能和查询需求等因素。

### 2.整数类型

在数据库中，整数类型用于存储整数数据。不同的数据库管理系统支持不同的整数类型，以下是一些常见的整数类型：

1. **TINYINT：**
   - 范围：-128 到 127（有符号）或 0 到 255（无符号）
   - 存储大小：1 字节

2. **SMALLINT：**
   - 范围：-32,768 到 32,767（有符号）或 0 到 65,535（无符号）
   - 存储大小：2 字节

3. **MEDIUMINT：**
   - 范围：-8,388,608 到 8,388,607（有符号）或 0 到 16,777,215（无符号）
   - 存储大小：3 字节

4. **INT（INTEGER）：**
   - 范围：-2^31 到 2^31-1（有符号）或 0 到 2^32-1（无符号）
   - 存储大小：4 字节

5. **BIGINT：**
   - 范围：-2^63 到 2^63-1（有符号）或 0 到 2^64-1（无符号）
   - 存储大小：8 字节

这些整数类型可以存储不同范围的整数值，有些还可以选择是否使用有符号或无符号表示。选择合适的整数类型取决于你的数据范围和存储需求。例如，如果你知道数据范围较小，可以选择较小的整数类型以节省存储空间。如果数据范围较大，可以选择较大的整数类型。

### 3.定点数类型和浮点数类型

在数据库中，定点数类型和浮点数类型都用于存储数值，但它们有一些关键的区别。

#### 定点数类型：

1. **DECIMAL（或 NUMERIC）：**
   - 用于存储精确的十进制数值，**通常用于表示货币或其他要求精确计算的数据。**
   - 定义时需要指定精度和小数位数。
   - 不会有浮点数的精度损失问题。

```sql
-- 例子：DECIMAL 类型
CREATE TABLE example_table (
    id INT,
    price DECIMAL(10, 2)
);
```

#### 浮点数类型：

1. **FLOAT：**
   - 用于存储近似值的二进制浮点数。
   - 存储大小较小，适合大范围的数值，但可能存在精度损失问题。
   - 适用于科学计算等场景。

2. **DOUBLE：**
   - 双精度浮点数，提供更大的范围和更高的精度，但仍然可能存在精度损失。

```sql
-- 例子：FLOAT 和 DOUBLE 类型
CREATE TABLE example_table (
    id INT,
    measurement FLOAT,
    distance DOUBLE
);
```

#### 关键区别：

1. **精度：**
   - 定点数类型（DECIMAL）提供精确的表示，不会有浮点数的精度损失问题。
   - 浮点数类型（FLOAT 和 DOUBLE）是近似值的表示，可能存在精度损失。

2. **存储方式：**
   - 定点数使用固定的小数位数，以十进制方式存储。
   - 浮点数使用二进制表示，具有指数部分，适合表示很大或很小的数值范围。

3. **用途：**
   - 定点数通常用于要求精确计算的场景，如货币。
   - 浮点数通常用于科学计算等场景，对于绝对精度要求较低但需要处理大范围数值的情况。

在选择使用定点数类型还是浮点数类型时，需要根据具体的业务需求和对数值精度的要求进行权衡。

### 4.枚举和集合类型

在数据库中，枚举（ENUM）和集合（SET）是两种用于存储一组离散值的特殊数据类型。

#### 枚举（ENUM）：

1. **ENUM：**
   - 用于存储单个值，该值必须是在定义枚举时列举的值之一。
   - 枚举类型可以包含零个或多个元素，每个元素都有一个相关的索引（从1开始）。
   - 枚举类型适用于存储有限且已知的可能取值的字段。

```sql
-- 例子：ENUM 类型
CREATE TABLE example_table (
    id INT,
    status ENUM('Active', 'Inactive', 'Pending')
);
```

#### 集合（SET）：

1. **SET：**
   - 用于存储多个值，这些值必须是在定义集合时列举的值之一。
   - 集合类型可以包含零个或多个元素，每个元素都有一个相关的位位置。
   - 集合类型适用于存储一组可能取值的字段，可以选择一个或多个值。

```sql
-- 例子：SET 类型
CREATE TABLE example_table (
    id INT,
    permissions SET('Read', 'Write', 'Execute')
);
```

#### 区别：

1. **唯一值：**
   - 枚举类型只能存储单个值，该值必须是事先定义好的枚举元素之一。
   - 集合类型可以存储多个值，每个值必须是事先定义好的集合元素之一。

2. **存储方式：**
   - 枚举类型的存储通常是整数，表示枚举元素的索引。
   - 集合类型的存储是一个二进制位集，表示选定的集合元素。

3. **用途：**
   - 枚举类型适用于存储有限的且已知的可能取值的字段，如状态字段。
   - 集合类型适用于存储一组可能取值的字段，用户可以选择一个或多个值，如权限字段。

在使用枚举和集合类型时，需要考虑数据的特性和业务需求，选择最适合场景的类型。注意，使用过多的枚举或集合元素可能导致查询复杂性增加，因此需要权衡选择。

### 5.时间和日期类型

在数据库中，日期和时间类型用于存储日期和时间信息。不同的数据库管理系统支持不同的日期和时间类型，以下是一些常见的类型：

#### 日期类型：

1. **DATE：**
   - 用于存储日期，不包含时间部分。
   - 例如，'2023-11-17'。

#### 时间类型：

2. **TIME：**
   - 用于存储时间，不包含日期部分。
   - 例如，'12:30:00'。

3. **DATETIME：**
   - 用于存储日期和时间。
   - 例如，'2023-11-17 12:30:00'。

4. **TIMESTAMP：**
   - 类似于 DATETIME，但通常表示相对于某个特定时区或相对于协调世界时（UTC）的时间戳。
   - 通常用于记录修改或插入记录的时间。
   - 例如，'2023-11-17 12:30:00'。

#### 日期和时间类型：

5. **DATETIME 和 TIME 的组合：**
   - 有些数据库支持将 DATE 和 TIME 组合在一起，形成 DATETIME。
   - 例如，'2023-11-17 12:30:00'。

6. **TIMESTAMP WITH TIME ZONE：**
   - 存储带有时区信息的时间戳。
   - 例如，'2023-11-17 12:30:00 +03:00'。

#### 时间间隔类型：

7. **INTERVAL：**
   - 用于表示时间间隔或持续时间。
   - 例如，'3 days'，'2 hours'。

在使用日期和时间类型时，需要根据具体的业务需求选择最适合的类型。时区的处理也是一个重要考虑因素，特别是在分布式系统中。不同的数据库系统可能对日期和时间类型的实现细节有所不同，因此在具体使用时需要参考相应的数据库文档。

### 6.Blob类型

在关系型数据库中，不要储存这种类型数据，（**关系型数据库重点储存的是关系型数据**）

### 7.JSON类型

JSON（JavaScript Object Notation）是一种用于数据交换的轻量级文本格式，常用于前后端之间的数据传输。MySQL引入了JSON数据类型，使得可以在数据库中存储和查询JSON格式的数据。

以下是一些JSON类型的特性和用法：

#### 1. JSON数据类型的创建

在MySQL中，可以使用`JSON`来定义JSON类型的列。例如：

```sql
CREATE TABLE my_table (
    id INT PRIMARY KEY,
    json_data JSON
);
```

这将创建一个表`my_table`，其中包含一个`json_data`列，其数据类型为JSON。

#### 2. 存储JSON数据

可以使用INSERT语句向JSON类型的列中插入JSON数据：

```sql
INSERT INTO my_table (id, json_data) VALUES (1, '{"name": "John", "age": 30, "city": "New York"}');
```

#### 3. 查询JSON数据

可以使用内置的JSON函数来查询和操作JSON数据。例如，使用`->`运算符来访问JSON对象的属性：

```sql
SELECT json_data->'$.name' AS name FROM my_table WHERE id = 1;
```

这将返回`my_table`表中ID为1的行的JSON数据中的"name"属性的值。

#### 4. JSON函数

MySQL提供了一系列用于处理JSON数据的内置函数，例如：

- `JSON_EXTRACT()`: 从JSON数据中提取特定的值。
- `JSON_UNQUOTE()`: 去除JSON字符串外围的引号。
- `JSON_SEARCH()`: 在JSON数据中查找特定的路径。
- `JSON_ARRAY()`: 创建JSON数组。
- `JSON_OBJECT()`: 创建JSON对象。

#### 5. JSON索引

从MySQL 8.0.13版本开始，支持在JSON列上创建函数索引，以提高JSON数据的查询性能。这允许你在JSON对象的某个属性上创建索引，以加速按该属性搜索的查询。

#### 注意事项：

- JSON类型适合存储半结构化数据，但对于大规模结构化数据，可能更适合使用传统的关系型数据库设计。
  
- 在进行复杂的JSON查询时，要注意性能问题，因为JSON数据的深度嵌套和大小可能影响查询性能。

总的来说，JSON类型为MySQL提供了更好的支持半结构化数据的能力，使得处理和查询JSON数据更为灵活。

# 设计数据库

## 一.数据建模

在学习 MySQL 时，理解数据建模是非常重要的，因为它涉及到如何组织和设计数据库中的数据结构。数据建模的目标是创建一个能够有效存储和检索数据的数据库，同时保持数据的一致性和完整性。

**设计数据库**通常包括以下几个关键步骤：

1. **需求分析**：
   - 确定数据库的目标和需求。了解将要存储的数据类型、数据量、使用模式等信息，以便为数据库设计提供基础。

2. **概念设计**：
   - 使用概念模型（如实体-关系图）来捕捉系统中的主要实体、关系和属性。这一阶段主要关注业务需求和概念层面，而不考虑具体的数据库表结构。

3. **逻辑设计**：
   - 将概念设计转化为逻辑模型，确定数据库中的表、列、关系、主键和外键等。这一阶段关注如何将概念模型映射到数据库管理系统（DBMS）支持的结构。

4. **规范化**：
   - 应用范式规则，通过规范化来消除冗余、提高数据一致性和减少插入、更新和删除操作的异常。通常包括将数据组织成符合第一范式（1NF）、第二范式（2NF）、第三范式（3NF）等规范形式的过程。

5. **物理设计**：
   - 考虑数据库的物理存储结构，包括索引、分区、存储过程等。这一步骤通常与具体的数据库管理系统相关，需要根据系统的性能和存储需求做出相应的选择。

6. **实施**：
   - 根据逻辑和物理设计创建数据库和表，定义约束、触发器等数据库对象。这一步骤实际上将设计转化为数据库系统中的实体。

7. **数据导入**：
   - 如果有现有的数据，将其导入数据库中。这可能涉及从其他数据源中导入数据，确保导入的数据符合数据库设计的结构。

8. **测试和优化**：
   - 进行测试，确保数据库的功能和性能符合预期。优化数据库结构、查询和索引以提高性能。

9. **备份和恢复策略**：
   - 制定数据库的备份和恢复策略，确保在发生故障或数据丢失时能够快速恢复数据。

10. **文档化**：
    - 记录数据库设计和实现的细节，包括表结构、索引、关系图、存储过程等。文档化有助于团队成员了解数据库结构和操作。

这些步骤通常构成了数据库设计的主要流程。在整个设计过程中，与利益相关者（包括业务用户和开发团队）的沟通和反馈都是非常重要的，以确保最终的数据库能够满足实际需求。



### 1.实体

当我们谈论数据库或数据建模时，实体通常可以想象成现实生活中的一个事物、对象或概念。你可以把实体看作是你想要在数据库中记录的某个东西，它有一些特征和属性。

举个例子，如果我们设计一个学生管理系统的数据库，那么"学生"就是一个实体。每个学生都有一些特定的属性，比如姓名、学号、出生日期等。这些属性就是描述这个实体的特征。

再举一个例子，如果我们设计一个图书馆系统的数据库，那么"图书"就是一个实体。每本图书有一些属性，比如书名、作者、出版日期等。这些属性描述了图书这个实体的特征。

在数据库中，我们用表（Table）来表示实体。每个表的行（Row）代表数据库中的一个实体实例，而表的列（Column）代表实体的属性。通过这样的方式，我们可以很方便地组织和存储大量不同类型的实体及其属性。这种结构化的方式使得我们能够高效地检索和管理数据。

所以，实体就是我们在数据库中想要记录的具体事物或概念，每个实体都有一些与之相关的属性，这些属性用来描述实体的特征。



### 2.概念模型和逻辑模型

设计数据库时，概念模型和逻辑模型是两个重要的阶段，分别用于捕捉系统概念层面的需求和转化为数据库系统能够理解的结构。

#### **概念模型：**

**通俗易懂解释**：概念模型就像是你脑海中对系统的一个简单图画，关注的是系统中的主要概念、实体以及它们之间的关系。

**比喻**：想象你要设计一个社交媒体平台的数据库。在概念模型阶段，你可能会画出用户、帖子、评论等各种元素之间的关系图。这个图只是一个简单的表示，不涉及到具体的数据库表和字段。

**关键特点**：

- 强调业务需求和系统的高层概念。
- 用实体-关系图等工具表示系统中的实体、关系和属性。
- 不考虑数据库管理系统（DBMS）的具体技术实现。

#### 逻辑模型：

**通俗易懂解释**：逻辑模型是将概念模型转化为数据库系统理解的语言，即将业务概念转换为数据库表、列、关系等结构的过程。

**比喻**：回到社交媒体平台的例子，逻辑模型阶段会涉及确定实际的数据库表，比如用户表、帖子表、评论表，以及它们之间的关系，比如用户和帖子之间可能有一对多的关系。

**关键特点**：
- 将概念模型转化为数据库管理系统能够理解的结构。
- 包括具体的数据库表、列、主键、外键等定义。
- 强调如何在数据库中组织和存储数据。

在整个设计流程中，概念模型通常是设计的起点，帮助捕捉业务需求。而逻辑模型则是将这些需求具体实现的阶段，考虑数据库系统的细节。这两个阶段相辅相成，共同构建出一个能够满足业务需求且在数据库系统中有效运行的结构。



### 3.实体模型

实体模型是数据库设计中的一种模型，主要用于描述系统中的实体、实体之间的关系以及实体的属性。在通俗易懂的解释中，你可以把实体模型看作是一个系统的“大纲图”，它展示了系统中有哪些关键的事物（实体）、这些事物之间如何相互关联，以及它们具有哪些特征（属性）。

#### 实体模型的关键要素：

1. **实体（Entity）**：
   - 实体是系统中可以独立辨识和描述的一个事物、对象或概念。比如，在学生管理系统中，学生就是一个实体。

2. **属性（Attributes）**：
   - 属性是与实体相关联的特征或性质，描述了实体的各个方面。例如，一个学生实体可能有姓名、学号、出生日期等属性。

3. **关系（Relationships）**：
   - 关系描述了不同实体之间的联系。在实体模型中，你可以表示实体之间的关系，比如学生和课程之间可能存在一个“选修”关系。

#### 通俗比喻：

想象你正在设计一个在线商城的数据库。在实体模型阶段，你会考虑哪些实体是关键的，比如“商品”、“用户”、“订单”等。每个实体都有一些特定的属性，比如商品实体可能有名称、价格、库存等属性。然后，你会思考这些实体之间的关系，比如一个订单实体与用户和商品之间是如何关联的。

#### 关键特点：

- 强调系统中的实体、它们的属性和关系。
- 使用图形工具（如实体-关系图）表示不同实体及其关系。
- 帮助设计者和利益相关者理解系统中的重要元素和它们之间的相互作用。

实体模型是数据库设计的一个重要步骤，它提供了一个高层次的视图，帮助设计者在开始具体的数据库设计之前捕捉和理解系统中的关键概念。

### 概念模型,逻辑模型,实体模型之间的区别

概念模型、逻辑模型和实体模型是数据库设计中的三个不同层次的模型，它们在设计过程中扮演不同的角色。以下是它们之间的主要区别：

1. **概念模型（Conceptual Model）**：

   - **角色**：用于捕捉系统的高层次概念和业务需求。
   - **关注点**：主要关注业务层面的实体、关系和属性，不涉及具体的数据库表结构。
   - **工具**：通常使用实体-关系图等工具表示。
   - **示例**：在社交媒体平台的概念模型中，你可能会定义用户、帖子、评论等概念。

2. **逻辑模型（Logical Model）**：

   - **角色**：用于将概念模型转化为数据库系统能够理解的结构。
   - **关注点**：主要关注数据库表、列、关系、主键、外键等逻辑结构，以及如何组织和存储数据。
   - **工具**：使用数据库管理系统支持的建模工具或 SQL 语句。
   - **示例**：在社交媒体平台的逻辑模型中，你可能会定义用户表、帖子表、评论表，并指定它们之间的关系。

3. **实体模型（Entity Model）**：

   - **角色**：实际上，实体模型通常是概念模型的一部分，用于描述系统中的实体、实体之间的关系以及实体的属性。
   - **关注点**：强调系统中的实体、它们的属性和关系。
   - **工具**：使用实体-关系图等工具表示。
   - **示例**：在在线商城的实体模型中，你可能会定义商品、用户、订单等实体，以及它们之间的关系。

在设计流程中，概念模型通常是起点，帮助设计者理解业务需求。逻辑模型是将这些需求转化为数据库系统能够理解的结构的中间步骤。而实体模型是在概念模型中特别强调实体、属性和关系的一部分。这三个模型相互关联，协同工作，帮助设计者从不同层次审视和构建数据库。



### 4.主键,外键,外键约束

#### 主键（Primary Key）：

- **定义**：主键是一列或一组列，其值能够唯一标识表中的每一行数据。
- **作用**：用于确保表中的每一行都有一个唯一标识，便于快速查找和关联数据。
- **特点**：主键值不能有重复，而且不能是空值（NULL）。
- **示例**：在用户表中，用户的唯一标识可以是用户ID，这个ID就是主键。

#### 外键（Foreign Key）：

- **定义**：外键是一列或一组列，它建立了到另一个表中主键的关系。
- **作用**：通过外键，我们可以在两个表之间建立关系，通常是用来连接相关的数据。
- **特点**：外键的值必须是另一个表中的主键值，或者是 NULL（如果允许的话）。
- **示例**：在订单表中，用户ID可以是一个外键，连接到用户表的主键，表示订单是哪个用户下的。

#### 外键约束（Foreign Key Constraint）：

- **定义**：外键约束是一种规则，它确保外键的值在表中存在，并且与另一表的主键值匹配。
- **作用**：保证了数据的完整性，防止存在无法关联的外键值。
- **特点**：当尝试插入或更新数据时，外键约束会检查外键的值是否存在于关联表的主键中。
- **示例**：如果订单表的外键约束与用户表的主键相连，试图在订单表中插入一个不存在的用户ID时，外键约束将阻止这个操作。

#### 简记：

- **主键**：唯一标识表中每一行的标识符，不能重复，不能为NULL。
- **外键**：建立表与表之间关系的桥梁，连接到另一个表的主键。
- **外键约束**：确保外键的值在关联表中存在，保持数据的完整性。

通过使用主键和外键，我们能够建立起表与表之间的关系，使得数据库中的数据更为关联和一致。外键约束则是保障这种关系的有效性和完整性的一种机制。



### 5.复合主键

当我们讨论数据库设计时，复合主键是指表中使用多个列的组合来唯一标识每一行数据。为了更好地理解，让我们用一个简单的例子来说明：

#### 通俗易懂的例子：

想象你有一个班级花名册的数据库，需要记录每个学生在每门课上的成绩。在这个情况下，单一的主键（比如学生ID或课程ID）可能无法满足我们的需求，因为一个学生可能在不同课程中有相同的成绩，而相同的课程也可能有不同学生有相同的成绩。

为了解决这个问题，我们可以使用复合主键。在这个例子中，我们的复合主键可以由两个部分组成：学生ID和课程ID的组合。这样，每一对学生和课程都形成了一个唯一的标识。

#### 花名册数据库示例：

```plaintext
| 学生ID | 课程ID | 成绩 |
|--------|--------|------|
|   1    |   A    |  85  |
|   1    |   B    |  92  |
|   2    |   A    |  78  |
|   2    |   B    |  88  |
```

在这个示例中，（学生ID，课程ID）的组合就构成了复合主键。这意味着每一行都有一个独特的标识，我们可以准确地知道每个学生在每门课上的成绩。

#### 简要总结：

- **复合主键**：由两个或更多列组成的主键，用于确保表中每一行的唯一性。

- **适用场景**：当单一的标识符无法满足唯一性要求时，比如处理多对多关系或需要多个维度来标识数据时。

- **示例**：在学生成绩表中，学生ID和课程ID的组合可以形成复合主键，确保每个学生在每门课上的成绩都有唯一的标识。

通过使用复合主键，我们可以更灵活地处理多方面的数据关系，确保数据库中的每一行都能够被准确地标识。

## 二.标准化

当我们谈论数据库范式时，我们实际上在讨论如何组织数据以确保数据的一致性和避免数据冗余。让我们用通俗易懂的方式来理解第一范式、第二范式和第三范式：

### 1.第一范式（1NF）：

- **目标**：确保每一列的原子性，即每个单元格中的数据不可再分。

- **通俗解释**：每一列中的数据都应该是不可再分的最小单元，不包含集合、数组或其他结构。

- **示例**：如果有一列是“电话号码”，那么这一列的每个单元格中都只能包含一个完整的电话号码，而不是一个电话号码集合。

### 2.第二范式（2NF）：

- **目标**：确保表中的每一行都有唯一标识，消除部分依赖。

- **通俗解释**：每一行都应该被唯一的东西标识，而不是依赖于表中的一部分数据。

- **示例**：如果有一个表记录学生的成绩，学生ID和课程ID是联合主键，而不是仅仅以学生ID为主键。这样，每一行就可以被唯一地标识。

### 3.第三范式（3NF）：

- **目标**：确保表中的每一列都与主键直接相关，消除传递依赖。

- **通俗解释**：每一列都应该直接和主键相关，而不是间接依赖于其他列。

- **示例**：如果有一个表包含学生的地址和城市，而城市依赖于邮政编码，那么最好将城市和邮政编码分成另一个表，以确保每一列都直接与主键相关。

#### 简记：

- **第一范式**：确保每一列的数据原子性，不可再分。

- **第二范式**：确保每一行都有唯一标识，消除部分依赖。

- **第三范式**：确保每一列都直接与主键相关，消除传递依赖。

这些范式有助于设计出更加结构化、一致性和易于维护的数据库，减少数据冗余和提高查询效率。

### 4.链接表

在数据库设计中，"链接表" 通常指的是用来处理多对多关系的表，也被称为关联表或中间表。它的作用是解决多对多关系的复杂性，将两个实体之间的关系转化为多个一对多关系，从而更好地组织和管理数据。让我用通俗易懂的方式来解释：

#### 通俗解释：

假设你有一个数据库，其中包含学生和课程。一个学生可以选择多门课程，而一门课程也可以被多个学生选择。这就是一个典型的多对多关系。为了解决这个问题，我们引入了一个链接表。

#### 示例：

#### 学生表：

| 学生ID | 姓名 |
| ------ | ---- |
| 1      | 小明 |
| 2      | 小红 |
| 3      | 小李 |

#### 课程表：

| 课程ID | 课程名 |
| ------ | ------ |
| A      | 数学   |
| B      | 英语   |
| C      | 物理   |

#### 链接表（选课表）：

| 学生ID | 课程ID |
| ------ | ------ |
| 1      | A      |
| 1      | B      |
| 2      | A      |
| 3      | C      |
| 3      | B      |

在这个例子中，选课表是链接表。它的每一行表示一个学生选了一门课程的关系。通过这种方式，我们避免了在学生表或课程表中重复信息，而是将关联关系放到链接表中。

#### 使用链接表的好处：

1. **解决多对多关系**：通过链接表，我们能够清晰地表示多对多关系，避免在原始表中出现冗余信息。

2. **灵活性**：可以轻松地添加新的关联，而无需修改原始表结构。

3. **查询效率**：通过链接表，我们可以方便地进行多表查询，获取想要的信息。

#### 简记：

- **链接表**：解决多对多关系的表，用于存储两个实体之间的关联关系。

- **示例**：在学生和课程的例子中，选课表就是一个链接表，记录了学生和课程之间的关系。

使用链接表是数据库设计中常见的一种技巧，特别适用于处理多对多的关系。通过它，我们能够更好地组织和管理复杂的数据结构。

### 5.模型的正向工程、数据库同步模型、模型的逆向工程

#### 1. 正向工程（Forward Engineering）：

- **定义**：正向工程是数据库设计过程中的一部分，用于将数据库模型或设计规范转化为实际的数据库结构。

- **步骤**：
  1. **设计模型**：使用数据库设计工具创建数据库模型，定义表、列、关系等。
  2. **生成脚本**：根据设计模型生成数据库脚本。
  3. **执行脚本**：在目标数据库上执行生成的脚本，创建数据库结构。

- **应用场景**：适用于从零开始设计数据库时，通过设计模型生成实际数据库结构。

#### 2. 数据库同步模型：

- **定义**：数据库同步模型用于将一个数据库的变更同步到另一个数据库，以保持数据的一致性。常见的同步模型包括主从复制、主主复制等。

- **应用场景**：适用于分布式系统或多个数据库实例需要保持一致性的情况，确保数据同步更新。

#### 3. 逆向工程（Reverse Engineering）：

- **定义**：逆向工程是通过已存在的数据库结构提取信息，生成数据库模型或设计规范的过程。

- **步骤**：
  1. **提取信息**：分析已有数据库的结构，提取表、列、关系等信息。
  2. **生成模型**：使用逆向工程工具或脚本生成数据库模型。
  3. **优化设计**：根据生成的模型进行设计优化，如添加注释、调整关系。

- **应用场景**：适用于对已存在的数据库进行分析和文档化，或者在没有明确模型的情况下重新建模。

#### 简记：

- **正向工程**：设计模型 → 生成脚本 → 执行脚本，将设计模型转化为实际数据库结构。

- **数据库同步模型**：保持多个数据库之间的一致性，通过同步模型实现数据更新的同步。

- **逆向工程**：提取信息 → 生成模型 → 优化设计，通过已有数据库结构生成数据库模型或设计规范。

# 索引

索引是数据库中一种用于提高查询性能的数据结构。它类似于书籍的目录，通过提供一种快速访问数据的方式，加速查询操作。在数据库中，索引通常基于表的一个或多个列。

以下是一些关于数据库索引的关键概念：

#### 1. **索引的作用**：

- **提高查询速度**：通过预先排好序并存储索引，数据库引擎可以更快地定位和检索数据，特别是对于大型表。
  
- **加速排序和过滤操作**：在排序和过滤操作中，索引可以显著减少需要扫描的数据量。

- **唯一性约束**：在数据库中，索引可以用于强制唯一性约束，确保某列或某组列中的值是唯一的。

#### 2. **常见类型的索引**：

- **单列索引**：基于单个列的索引。
  
- **复合索引**：基于多个列的索引，可以加速涉及这些列的查询。

- **唯一索引**：确保索引列的值是唯一的。

- **全文索引**：适用于文本字段，支持全文搜索。

#### 3. **创建索引的注意事项**：

- **权衡空间和性能**：虽然索引提高了查询性能，但它也会占用额外的存储空间。在创建索引时需要权衡空间和性能。

- **避免过多索引**：过多的索引可能会导致写操作变慢，因为每次写入都需要更新索引。在创建索引时要谨慎，只创建必要的索引。

- **定期维护索引**：对于高度动态的数据库，定期维护索引是重要的。这包括重新构建索引、优化查询等操作。

#### 4. **索引的工作原理**：

- **B-树索引**：大多数数据库使用 B-树（或其变种，如B+树）来实现索引。B-树是一种自平衡的树结构，能够快速查找、插入和删除数据。

- **哈希索引**：某些数据库支持哈希索引，适用于等值查询。然而，哈希索引不适用于范围查询和排序。

- **全文索引**：全文索引使用特殊算法来支持文本的搜索，允许用户执行全文搜索而不是简单的精确匹配。

#### 5. **什么时候使用索引**：

- 当你经常执行查询操作时，特别是涉及到 WHERE 子句的查询。
  
- 当你需要通过排序和过滤操作来优化查询性能。

- 当你需要确保某列或某组列的唯一性时。

总体而言，索引是数据库性能优化的重要手段之一，但需要在合适的时机、合适的列上使用，避免不必要的索引以及定期进行维护。

## 1.创建索引

在 MySQL 中，你可以使用 `CREATE INDEX` 语句来创建索引。索引可以在单个列上创建，也可以在多个列上创建，以满足不同的查询需求。以下是一些常见的 MySQL 创建索引的示例：

### 创建单列索引：

```sql
CREATE INDEX index_name ON table_name (column_name);
```

例如，如果你有一个名为 `users` 的表，想要在 `username` 列上创建索引，可以执行以下命令：

```sql
CREATE INDEX idx_username ON users (username);
```

### 创建复合索引：

```sql
CREATE INDEX index_name ON table_name (column1, column2);
```

例如，在一个名为 `orders` 的表中，你可能想在 `customer_id` 和 `order_date` 列上创建一个复合索引：

```sql
CREATE INDEX idx_customer_order_date ON orders (customer_id, order_date);
```

### 创建唯一索引：

唯一索引确保索引列中的值是唯一的。在创建时，如果表中已存在重复的值，创建索引操作将失败。

```sql
CREATE UNIQUE INDEX index_name ON table_name (column_name);
```

例如，你可以在 `email` 列上创建一个唯一索引，确保每个用户的电子邮件地址是唯一的：

```sql
CREATE UNIQUE INDEX idx_email ON users (email);
```

### 注意事项：

1. **索引的命名**：为索引选择一个有意义的名称，以便更容易理解其目的。

2. **避免过度索引**：不要为每个列都创建索引，只创建对查询性能有实际影响的索引。

3. **选择适当的索引类型**：MySQL 支持多种索引类型，例如 B-Tree、Hash 等，根据查询的特性选择合适的索引类型。

4. **定期维护**：对于高度动态的表，定期维护索引是重要的，包括重新构建索引、优化查询等。

5. **查看已存在的索引**：可以使用 `SHOW INDEX FROM table_name;` 来查看表的索引信息。

请在进行任何涉及生产数据库的索引更改之前，确保你已经对索引的创建和影响有充分的了解，并在低峰期进行操作。

## 2.查看索引

在 MySQL 中，你可以使用 `SHOW INDEX` 语句或查询 `INFORMATION_SCHEMA` 数据库中的相关表来查看已存在的索引。以下是两种方法的示例：

### 1. 使用 `SHOW INDEX` 语句：

```sql
SHOW INDEX FROM table_name;
```

替换 `table_name` 为你要查看索引的表名。这将显示表的索引信息，包括索引名称、列名、索引类型等。

例如，查看名为 `users` 的表的索引信息：

```sql
SHOW INDEX FROM users;	
```

## 3.前缀索引

前缀索引是一种优化技术，它允许你只对列值的前缀部分创建索引，而不是整个列值。这可以减少索引的大小，提高查询性能，尤其在对大量数据的列进行索引时。

在 MySQL 中，你可以使用前缀索引来创建只对列值的前几个字符的索引。以下是使用前缀索引的一些示例：

### 创建前缀索引：

```sql
CREATE INDEX index_name ON table_name (column_name(length));
```

在这里，`length` 是你希望包含在索引中的字符的数量。例如，如果你希望对 `name` 列的前五个字符创建索引，可以执行以下命令：

```sql
CREATE INDEX idx_name_prefix ON your_table (name(5));
```

### 查询时使用前缀索引：

在查询时，MySQL 会使用前缀索引来加速匹配。例如：

```sql
SELECT * FROM your_table WHERE name LIKE 'abc%';
```

在这个查询中，如果有一个前缀索引 `idx_name_prefix`，MySQL 将使用该索引来查找以 'abc' 开头的所有行。

### 注意事项：

1. **选择合适的前缀长度：** 前缀长度的选择需要根据实际的数据分布和查询需求来决定。太短的前缀可能导致索引选择性降低，太长的前缀可能会增加索引的大小。

2. **考虑存储需求：** 前缀索引可以减少索引的存储需求，但也可能导致索引的选择性降低。在创建前缀索引时，需要权衡存储和性能。

3. **只对需要的列使用前缀索引：** 不是所有的列都适合使用前缀索引，只对需要在查询中用到的列使用前缀索引。

4. **定期维护索引：** 对于高度动态的表，定期维护索引是重要的，包括重新构建索引、优化查询等。

在实际应用中，前缀索引通常用于文本列，例如 VARCHAR 类型的列，以提高在前缀条件下的查询性能。

## 4.全文索引

全文索引是一种用于在文本数据中进行全文本搜索的索引类型。它允许在文本列中进行高效的模糊搜索、自然语言搜索以及关键词搜索。在 MySQL 中，`FULLTEXT` 是用于实现全文索引的关键字。

以下是在 MySQL 中使用全文索引的基本步骤：

### 创建全文索引：

在创建表时，你可以指定某个列需要使用全文索引。例如：

```sql
CREATE TABLE your_table (
    id INT PRIMARY KEY,
    content TEXT,
    FULLTEXT(content)
);
```

上述例子中，`content` 列被添加了全文索引。

### 查询时使用全文索引：

```sql
SELECT * FROM your_table WHERE MATCH(content) AGAINST('your_keyword');
```

1. **`WHERE MATCH(content)`：** 这是使用全文索引的关键部分。`MATCH()` 是 MySQL 中用于进行全文索引搜索的函数，括号内是要进行搜索的列名，这里是 `content` 列。全文索引通常用于针对文本数据进行高效的搜索。
2. **`AGAINST('your_keyword')`：** 指定要搜索的关键词。`AGAINST()` 是用于与全文索引匹配的关键字的函数。替换 `'your_keyword'` 为你希望搜索的实际关键词。

### 注意事项：

1. **仅适用于特定存储引擎：** MySQL 的全文索引功能通常在使用 InnoDB 存储引擎时生效。在 MyISAM 存储引擎下，所有的 `CHAR`、`VARCHAR` 和 `TEXT` 列都会自动获得全文索引。

2. **停用和启用全文索引：** 在创建表时启用全文索引，如果需要停用或删除全文索引，可以使用 `ALTER TABLE` 语句。

    ```sql
    -- 停用全文索引
    ALTER TABLE your_table DROP INDEX content;

    -- 重新启用全文索引
    ALTER TABLE your_table ADD FULLTEXT(content);
    ```

3. **定期维护索引：** 对于高度动态的表，定期维护全文索引是重要的，包括重新构建索引、优化查询等。

4. **了解全文索引的限制：** 全文索引的查询语法和性能会受到一些限制，例如最小关键词长度、停用词等。在使用全文索引之前，请了解这些限制以及你的具体需求。

全文索引是一个强大的工具，适用于需要进行文本搜索的场景，但在使用时需要注意其特定的语法和限制。

## 5.复合索引

复合索引是在多个列上创建的索引，而不仅仅是单个列。它的目的是提高多列条件下的查询性能，使得在涉及这些列的查询中能够更有效地过滤和检索数据。

### 创建复合索引：

在 MySQL 中，你可以通过以下方式创建复合索引：

```sql
CREATE INDEX index_name ON your_table (column1, column2, ...);
```

其中，`index_name` 是你为索引选择的名称，而 `column1, column2, ...` 是你想要在其上创建索引的列名列表。

例如，如果你有一个名为 `employees` 的表，你可能想要在 `department_id` 和 `hire_date` 列上创建一个复合索引：

```sql
CREATE INDEX idx_department_hiredate ON employees (department_id, hire_date);
```

### 查询时使用复合索引：

复合索引在查询时可以加速涉及索引列的等值匹配、范围查询、排序和组合条件的操作。例如：

```sql
SELECT * FROM your_table
WHERE column1 = 'value1' AND column2 = 'value2';
```

在这个查询中，如果有一个名为 `idx_column1_column2` 的复合索引，数据库系统可以利用这个索引来快速定位匹配条件的行。

### 注意事项：

1. **选择合适的列顺序：** 复合索引的列顺序很重要。通常，将最常用于查询条件的列放在索引的前面。

2. **适度使用：** 避免创建过多的复合索引，因为每个索引都会占用额外的存储空间，并影响插入、更新和删除的性能。

3. **覆盖索引：** 如果查询的列都包含在复合索引中，这称为覆盖索引，可以加速查询，因为不需要回到数据表中检索额外的信息。

4. **了解查询优化器：** 数据库查询优化器会尝试选择最优的索引。在一些情况下，可能会选择合并多个单列索引而不是使用复合索引，因此在实践中要进行测试和性能分析。

复合索引是数据库中一个重要的性能优化工具，但在设计和使用时需要根据具体的查询需求和数据分布做出明智的选择。

## 6.复合索引中的列顺序

在设计复合索引时，列的顺序非常重要，因为它会影响到索引的效率和性能。以下是一些关于复合索引列顺序的一般准则：

1. **最常用于查询条件的列放在前面：** 将最常用于 WHERE 子句的条件列放在复合索引的前面。这样可以确保索引在最频繁的查询中发挥最大的作用。

2. **等值查询的列优先：** 如果有等值查询（例如 `=`）的条件，将这些列放在复合索引的前面。等值查询的效率通常比范围查询更高。

3. **范围查询的列次之：** 如果有范围查询（例如 `<`, `>`, `BETWEEN`）的条件，将这些列放在等值查询列之后。这样可以充分利用索引进行范围扫描。

4. **排序和分组的列放在最后：** 如果有 ORDER BY 或 GROUP BY 子句，将这些列放在复合索引的最后。这有助于满足排序和分组的需求。

5. **覆盖索引的考虑：** 如果能够设计一个覆盖索引，即索引包含了查询所需的所有列，就可以避免访问实际的数据行，提高性能。在这种情况下，索引中的列顺序应该优化以覆盖查询的需要。

### 示例：

考虑一个订单表，有 `customer_id`、`order_date`、`product_id` 三个列。如果经常有查询按照客户、日期和产品进行筛选的情况，可以考虑以下两种复合索引：

1. 查询经常按照客户、日期、产品筛选：

   ```sql
   CREATE INDEX idx_customer_date_product ON orders (customer_id, order_date, product_id);
   ```

2. 查询经常按照日期、产品、客户筛选：

   ```sql
   CREATE INDEX idx_date_product_customer ON orders (order_date, product_id, customer_id);
   ```

在选择上述索引时，取决于你的实际查询模式，选择最符合常见查询条件的顺序。

## 7.索引无效

索引可能在某些情况下没有发挥出预期的性能优势，甚至可能导致性能下降。以下是一些常见情况，导致索引看起来“无效”的原因：

1. **低选择性的索引：** 如果索引列中的值重复度非常高，即索引的选择性很低，数据库优化器可能选择不使用索引而进行全表扫描。在这种情况下，索引的帮助有限，甚至可能变得不划算。

2. **小表：** 对于非常小的表，使用索引可能不如直接扫描整个表更有效率。索引的维护和使用也有开销，对小表可能不划算。

3. **范围查询和排序：** 如果查询涉及范围查询（`BETWEEN`、`<`, `>`) 或排序操作，索引的效果可能较差。在这种情况下，优化器可能会选择使用全表扫描而不是索引。

4. **表结构变更：** 当表结构发生变更，如增加、删除或修改索引列时，可能导致原有的索引不再适用。优化器可能需要重新评估并重新选择索引。

5. **隐式数据类型转换：** 如果查询条件中的列与索引列的数据类型不匹配，可能会导致隐式的数据类型转换，使得索引无法有效使用。

6. **并发问题：** 在高并发环境下，当多个事务同时竞争对同一行进行更新时，索引可能会引起锁的问题，导致性能下降。

7. **复杂的查询条件：** 当查询条件非常复杂，涉及多个连接、子查询等情况时，索引可能无法充分发挥作用，甚至会降低性能。

8. **随机分布的查询条件：** 如果查询的条件是随机分布的，而不是按照索引的顺序进行访问，那么索引的性能优势可能较小。

在面对这些情况时，进行性能调优时可以考虑重新评估索引的设计、查询语句的结构以及表的使用情况，以找到更有效的解决方案。

## 8.使用索引排序

在一些情况下，索引可以帮助加速排序操作。当查询中包含了 ORDER BY 子句，并且 ORDER BY 的列与某个索引的列相匹配时，数据库系统可以利用这个索引来执行排序，避免对整个结果集进行排序操作。

### 如何使用索引进行排序：

1. **创建适当的索引：** 确保在 ORDER BY 子句中使用的列上存在合适的索引。

2. **查询语句：** 编写查询语句时，确保 ORDER BY 子句中的列与索引的列相匹配。

3. **查看执行计划：** 使用 `EXPLAIN` 命令或查看数据库的执行计划，确认数据库是否选择使用了索引来执行排序。

### 示例：

假设有一个表 `employees` 包含列 `employee_id`、`employee_name` 和 `salary`。如果你想按照薪水从高到低排序，可以创建一个索引：

```sql
CREATE INDEX idx_salary ON employees (salary DESC);
```

然后，查询语句可以是这样：

```sql
SELECT * FROM employees
ORDER BY salary DESC;
```

在这种情况下，如果数据库选择使用 `idx_salary` 索引，它可以直接从索引中读取数据，避免了对整个表的排序操作。

### 注意事项：

1. **索引排序的方向：** 索引可以是升序（ASC）或降序（DESC）的。确保 ORDER BY 子句中的排序方向与索引的排序方向相匹配，以便数据库优化器能够充分利用索引。

2. **组合索引：** 如果 ORDER BY 子句中涉及多个列，可以考虑创建一个包含这些列的复合索引，以提高排序的效率。

3. **定期维护索引：** 索引的性能可能受到表数据变化的影响，因此需要定期进行索引维护，例如重新构建索引或进行优化操作。

请注意，虽然索引可以加速排序操作，但并非在所有情况下都是最佳选择。具体的性能优化需要根据具体的数据库引擎、表结构、查询模式等来综合考虑。

## 9.覆盖索引

覆盖索引（Covering Index）是指一个索引包含了所有查询所需的列，而不需要回表（即不需要再去实际的数据表中检索数据）。这样的索引能够完全满足查询的需求，从而避免了额外的表查找操作，提高了查询性能。

### 覆盖索引的优势：

1. **减少 I/O 操作：** 由于所有需要的数据都包含在索引中，不再需要额外的表查找操作，从而减少了 I/O 操作，提高了查询速度。

2. **降低存储成本：** 由于不需要存储重复的数据，覆盖索引可以节省存储空间。

### 创建覆盖索引的注意事项：

1. **包含所有查询列：** 确保索引包含了所有查询中涉及的列。如果查询中的列没有包含在索引中，数据库可能会选择回表，降低了覆盖索引的效果。

2. **避免创建过多索引：** 不要为每个可能的查询都创建覆盖索引。索引的数量也会影响到写入性能，因此需要在性能优化和维护的成本之间进行权衡。

### 每当创建一个二级索引，MySQL会自动将主键包含在第二索引中

这句话的意思是，当你在 MySQL 数据库中创建一个二级索引（非主键索引）时，MySQL 在该二级索引中会自动包含主键列的值。这被称为“覆盖索引”（Covering Index）。

让我们通过一个例子来解释：

假设有一个表 `users`，包含以下列：

- `user_id` (主键)
- `username`
- `email`
- 其他列...

现在，你想在 `username` 列上创建一个索引，以提高查询速度。当你创建这个索引时，MySQL 会自动在这个索引中包含主键列 `user_id` 的值。这就是说，`username` 索引中的每个条目都包含了对应行的 `username` 值和 `user_id` 值。

为什么会这样做呢？这是因为在执行查询时，如果可以仅通过索引就能获取所需的数据，而不需要回到原始的数据表中查找，那么查询的效率将更高。这也是覆盖索引的概念。

所以，当你执行一个查询，例如：

```sql
SELECT user_id, username FROM users WHERE username = 'example';
```

如果有一个覆盖了 `username` 的索引，MySQL 可以直接从索引中获取 `user_id` 和 `username` 的值，而不必回到原始的数据表中查找。这种做法减少了 I/O 操作，提高了查询性能。

## 10.维护索引

索引的维护是数据库管理中一个重要的任务，它确保索引的有效性和性能。以下是一些常见的索引维护任务：

1. **重建索引：** 通过定期重建索引，可以消除索引中的碎片，提高索引的性能。索引重建的频率取决于数据库的使用情况，通常在数据库经历大量数据变动或删除操作后执行。

2. **优化索引选择性：** 确保索引列的选择性足够高。选择性是指索引中不同值的数量与表中总行数的比率。如果选择性过低，可能导致数据库优化器不选择使用索引，影响查询性能。

3. **删除不需要的索引：** 定期检查并删除不再需要的索引。过多的索引不仅会增加存储空间占用，还可能影响写操作的性能。

4. **避免过度索引：** 不要为每个列都创建索引。过多的索引不仅浪费存储空间，还会增加更新和插入操作的开销。仅在经常用于查询条件或排序的列上创建索引。

5. **使用覆盖索引：** 在一些查询中，可以使用覆盖索引，避免回表操作，提高查询性能。

6. **监控索引的使用情况：** 使用数据库的性能监控工具，监控索引的使用情况，及时发现可能存在的性能问题。

7. **定期收集统计信息：** 统计信息对于数据库优化器选择正确的执行计划至关重要。定期收集表和索引的统计信息，帮助优化器更好地进行决策。

8. **避免频繁的索引创建和删除：** 过于频繁的创建和删除索引会增加数据库的维护成本。在设计时，应该慎重选择索引并避免不必要的变动。

9. **理解不同存储引擎的索引特性：** 不同的数据库存储引擎对索引的处理方式可能不同，了解并根据使用的存储引擎选择适当的索引维护策略。

索引的维护工作需要根据具体的数据库使用情况和业务需求来制定。定期的性能分析和监控可以帮助发现潜在的问题，进而采取相应的索引维护措施。
