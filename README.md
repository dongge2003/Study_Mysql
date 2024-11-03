
# <center>Mysql
---
## SQL分类
| 分类 | 全称                       | 说明                                                 |
| ---- | -------------------------- | ---------------------------------------------------- |
| DDL  | Data Definition Language   | 数据定义语言,用来定义数据库对象(数据库,表,字段)      |
| DML  | Data Manipulation Language | 数据操作语言,用来对数据库表中的数据进行增删改查      |
| DQL  | Data Query Language        | 数据查询语言,用来查询数据库中表的记录                |
| DCL  | Data Control Language      | 数据控制语言,用来创建数据库用户,控制数据库的访问权限 |
---
## 注释
```sql
-- 单行注释
# 单行注释(Mysql特有)

/*
 多行
 注释
 */
```
---
## 数据类型
#### <center>数值类型
| 类型          | 描述         | 范围或大小                                                        |
| ------------- | ------------ | ----------------------------------------------------------------- |
| INT           | 整数类型     | -2,147,483,648 到 2,147,483,647                                   |
| TINYINT       | 小整数类型   | -128 到 127（有符号）                                             |
| SMALLINT      | 小整型       | -32,768 到 32,767（有符号）                                       |
| MEDIUMINT     | 中整型       | -8,388,608 到 8,388,607（有符号）                                 |
| BIGINT        | 大整型       | -9,223,372,036,854,775,808 到 9,223,372,036,854,775,807（有符号） |
| FLOAT         | 单精度浮点数 | 大约 -3.402823466E+38 到 3.402823466E+38                          |
| DOUBLE        | 双精度浮点数 | 大约 -1.7976931348623157E+308 到 1.7976931348623157E+308          |
| DECIMAL(p, s) | 精确数值类型 | 根据定义的精度 p 和小数位数 s 决定                                |


#### <center>字符串类型
| 类型         | 描述             | 最大长度                           |
| ------------ | ---------------- | ---------------------------------- |
| CHAR(n)      | 定长字符串类型   | n（1 到 255）                      |
| VARCHAR(n)   | 变长字符串类型   | n（1 到 65,535，具体取决于字符集） |
| TEXT         | 长文本类型       | 65,535 字符                        |
| TINYTEXT     | 小文本类型       | 255 字符                           |
| MEDIUMTEXT   | 中文本类型       | 16,777,215 字符                    |
| LONGTEXT     | 大文本类型       | 4,294,967,295 字符                 |
| BINARY(n)    | 定长二进制字符串 | n（1 到 255）                      |
| VARBINARY(n) | 变长二进制字符串 | n（1 到 65,535）                   |
| BLOB         | 二进制大对象     | 65,535 字节                        |
| TINYBLOB     | 小二进制大对象   | 255 字节                           |
| MEDIUMBLOB   | 中二进制大对象   | 16,777,215 字节                    |
| LONGBLOB     | 大二进制大对象   | 4,294,967,295 字节                 |

- 对象
  - 存储图像文件、音频文件、视频文件等。
用于需要存储大文件的应用，如文档管理系统、内容管理系统等。
  - BLOB 数据在数据库中以二进制格式存储，通常需要特殊的函数或方法来读取和写入。
在一些数据库中，处理 BLOB 数据时可能需要使用流（stream）或二进制读取器。

#### <center>日期类型
| 类型      | 描述           | 范围或格式                                             |
| --------- | -------------- | ------------------------------------------------------ |
| DATE      | 日期类型       | '1000-01-01' 到 '9999-12-31'                           |
| TIME      | 时间类型       | '-838:59:59' 到 '838:59:59'                            |
| DATETIME  | 日期和时间类型 | '1000-01-01 00:00:00' 到 '9999-12-31 23:59:59'         |
| TIMESTAMP | 时间戳类型     | '1970-01-01 00:00:01' UTC 到 '2038-01-19 03:14:07' UTC |
| YEAR      | 年类型         | 1901 到 2155                                           |

---
## DDL
### <center>数据库操作
```sql
-- 查询所有数据库
show databases;

-- 查询当前数据库
select database();

-- 创建数据库
create database [if not exists] 数据库名 [default charset 字符集] [collate 排序规则];
-- if not exists 如果没有就这个数据库就创建

-- 删除数据库
drop database if exists 数据库名;

-- 使用数据库
use 数据库名;
```

### <center>表操作
#### <center>查询
```sql
-- 查询当前数据库所有表
show tables;

-- 查询表结构
desc 表名;

-- 查询指定表的建表语句
show create table 表名;
```

#### <center>创建
```sql
-- 创建表
create table 表名(
    字段1 字段1类型 [comment 字段1注释],
    字段2 字段2类型 [comment 字段2注释],
    ...
    字段n 字段n类型 [comment 字段n注释]
)[comment 表注释];
```

#### <center>修改
```sql
-- 添加字段
ALTER Table 表名 ADD 字段名 字段类型 [COMMENT '注释'];

-- 修改数据类型
ALTER Table 表名 MODIFY 字段名 新字段类型(长度);

-- 修改字段名和字段类型
ALTER TABLE 表名 CHANGE 旧字段名 新字段名 类型(长度) [COMMENT '注释'] [约束];

-- 删除字段
ALTER Table 表名 DROP 字段名;

-- 修改表名
ALTER Table 表名 RENAME TO 新表名;

-- 刪除表
DROP TABLE IF EXISTS 表名;
```
---
## DML
#### <center>添加数据
```sql

-- 给指定字段插入数据
INSERT INTO 表名 (字段1,字段2,...) VALUES (值1,值2,...);

-- 给全部字段插入数据
INSERT INTO 表名 VALUES (值1,值2,...);

-- 批量添加数据
INSERT INTO 表名 (字段1,字段2,...) VALUES (值1,值2,...),(值1,值2,...);
INSERT INTO 表名 VALUES (值1,值2,...),(值1,值2,...);

# 字符串和日期类型的数据应该包含在引号范围内
# 插入数据时,指定字段的顺序与值的顺序一一对应
```

#### <center>修改数据
```sql
-- 修改数据
UPDATE test_table SET 字段名1 = 值1, 字段名2 = 值2,... [WHERE 条件];

# 如果没有条件则会修改整张表的数据
```

#### <center>删除数据
```sql
-- 删除数据
DELETE FROM 表名 [WHERE 条件];

# 如果没有条件则会删除整张表的数据
# delete语句不能删除某一字段的值时(可以使用update)
```
---
## DQL
```sql
-- ---------DQL语法-------------
SELECT 字段列表
FROM 表名列表
WHERE 条件列表
GROUP BY 分组字段列表
HAVING 分组后条件列表
ORDER BY 排序字段列表
LIMIT 分页参数
```
- 基本查询
- 条件查询(where)
- 聚合函数(cont, max, min, avg, sum)
- 分组查询(group by)
- 排序查询(order by)
- 分页查询(limit)

#### <center>基本查询
```sql
-- 查询多个字段
SELECT 字段1,字段2,... FROM 表名;
SELECT * FROM 表名

-- 设置别名
SELECT 字段1[AS 别名1], 字段2[AS 别名2],.... FROM 表名;

-- 去除重复字段
SELECT DISTINCT 字段列表 FROM 表名
```

#### <center>条件查询
```sql
-- 语法
SELECT 字段列表 FROM 表名 WHERE 条件;
```

| 运算符        | 功能描述          | 示例                                                 |
| ------------- | ----------------- | ---------------------------------------------------- |
| `=`           | 等于              | `SELECT * FROM emp WHERE age = 30;`                  |
| `!=`          | 不等于            | `SELECT * FROM emp WHERE age != 30;`                 |
| `<`           | 小于              | `SELECT * FROM emp WHERE age < 30;`                  |
| `<=`          | 小于或等于        | `SELECT * FROM emp WHERE age <= 30;`                 |
| `>`           | 大于              | `SELECT * FROM emp WHERE age > 30;`                  |
| `>=`          | 大于或等于        | `SELECT * FROM emp WHERE age >= 30;`                 |
| `BETWEEN AND` | 在两个值之间      | `SELECT * FROM emp WHERE age BETWEEN 18 AND 30;`     |
| `IN`          | 在指定的集合中    | `SELECT * FROM emp WHERE workno IN ('1', '2', '3');` |
| `LIKE`        | 模糊匹配          | `SELECT * FROM emp WHERE name LIKE '张%';`           |
| `IS NULL`     | 检查是否为 NULL   | `SELECT * FROM emp WHERE idcard IS NULL;`            |
| `IS NOT NULL` | 检查是否不为 NULL | `SELECT * FROM emp WHERE idcard IS NOT NULL;`        |
- 模糊匹配规则:
  -  %：表示零个或多个字符。
  - _：表示一个字符。

| 运算符        | 功能描述          | 示例                                                  |
| ------------- | ----------------- | ----------------------------------------------------- |
| `AND`         | 同时满足多个条件  | `SELECT * FROM emp WHERE age > 20 AND gender = '男';` |
| `OR`          | 满足任意一个条件  | `SELECT * FROM emp WHERE age < 18 OR gender = '女';`  |
| `NOT`         | 取反条件          | `SELECT * FROM emp WHERE NOT gender = '男';`          |
| `BETWEEN`     | 在两个值之间      | `SELECT * FROM emp WHERE age BETWEEN 18 AND 30;`      |
| `IN`          | 在指定的集合中    | `SELECT * FROM emp WHERE workno IN ('1', '2', '3');`  |
| `LIKE`        | 模糊匹配          | `SELECT * FROM emp WHERE name LIKE '张%';`            |
| `IS NULL`     | 检查是否为 NULL   | `SELECT * FROM emp WHERE idcard IS NULL;`             |
| `IS NOT NULL` | 检查是否不为 NULL | `SELECT * FROM emp WHERE idcard IS NOT NULL;`         |


#### <center>聚合函数
- 将一列数据作为整体,进行纵向计算

| 函数  | 功能     |
| ----- | -------- |
| count | 统计数量 |
| max   | 最大值   |
| min   | 最小值   |
| avg   | 平均值   |
| sum   | 求和     |

```sql
-- 语法
SELECT 聚合函数(字段列表) FROM 表名;

# 所有的NULL值不参与运算
```

#### <center>分组查询
```sql
-- 语法
SELECT 字段列表 FROM 表名 [WHERE 条件] GROUP BY 分组字段名 [HAVING 分组后过滤条件]
```
| 区别      | where                                               | having                         |
| --------- | --------------------------------------------------- | ------------------------------ |
| 执行时机: | where 是分组之前进行过滤,不满足where条件,不参与分组 | having是分组之后对结果进行过滤 |
| 判断条件: | where 不能对聚合函数进行判断                        | having可以                     |

*注意:
执行顺序: where > 聚合函数 > having
分组之后,查询的字段一般为聚合函数和分组字段,查询其他字段无任何意义*


#### <center>排序查询
```sql
-- 语法
SELECT 字段列表 FROM 表名 ORDER BY 字段1 排序方式1, 字段2 排序方式2, ....; 
```
| 排序方式 | 描述       |
| -------- | ---------- |
| ASC      | 升序(默认) |
| DESC     | 降序       |

*注意: 如果多字段排序,当第一个字段值相同时,才会根据第二个字段进行排序.*


#### <center>分页查询
```sql
-- 语法
SELECT 字段名 FROM 表名 LIMIT 起始索引,查询记录数;
```
- 注意:
  - 起始索引从0开始,起始索引 = (查询页码 - 1) * 每页显示记录数
  - 分页查询是数据库的方言,不同的数据库有不同的实现,Mysql是limit
  - 如果查询的第一页是数据,起始索引可以省略,直接简写为limit 10.  

#### <center>执行顺序
| 序号 | 编写顺序 | 执行顺序 |
| ---- | -------- | -------- |
| 1    | select   | from     |
| 2    | from     | where    |
| 3    | where    | group by |
| 4    | group by | having   |
| 5    | having   | select   |
| 6    | order by | order by |
| 7    | limit    | limit    |
---

##### <center>案例
```sql
-- Active: 1730470824717@@127.0.0.1@3306@test_database

CREATE DATABASE test_database;

USE test_database;

CREATE TABLE emp (
    id INT COMMENT '编号',
    workno VARCHAR(10) COMMENT '工号',
    name VARCHAR(10) COMMENT '姓名',
    gender CHAR(1) COMMENT '性别',
    age TINYINT UNSIGNED COMMENT '年龄',
    idcard CHAR(18) COMMENT '身份证号',
    workaddress VARCHAR(50) COMMENT '工作地址',
    entrydate DATE COMMENT '入职时间'
) COMMENT '员工表';


INSERT INTO emp (id, workno, name, gender, age, idcard, workaddress, entrydate) VALUES
(1, '1', '柳岩', '女', 20, '123456789012345678', '北京', '2000-01-01'),
(2, '2', '张无忌', '男', 18, '123456789012345670', '北京', '2005-09-01'),
(3, '3', '韦一笑', '男', 38, '123456789712345670', '上海', '2005-08-01'),
(4, '4', '赵敏', '女', 18, '123456757123845670', '北京', '1989-12-31'), -- 日期格式修正
(5, '5', '小昭', '女', 16, '123456769012345678', '上海', '2007-07-01'),
(6, '6', '杨逍', '男', 28, '12345678931234567X', '北京', '2006-01-01'),
(7, '7', '范瑶', '男', 40, '123456789212345670', '北京', '2005-05-01'),
(8, '8', '黛绮丝', '女', 38, '123456157123645670', '天津', '2015-05-01'),
(9, '9', '范凉凉', '女', 45, '123156789012345678', '北京', '2018-04-01'), -- 日期格式修正
(10, '10', '陈友谅', '男', 53, '123456789012345670', '上海', '2011-01-01'),
(11, '11', '张士诚', '男', 55, '123567897123465670', '江苏', '1985-12-31'), -- 日期格式修正
(12, '12', '常遇春', '男', 32, '12346757152345670', '北京', '2004-02-01'), -- 修正引号
(13, '13', '张三丰', '男', 88, '123656789012345678', '江苏', '2020-11-01'),
(14, '14', '灭绝', '女', 65, '123456719012345670', '西安', '2019-05-01'),
(15, '15', '胡青牛', '男', 70, '12345674971234567X', '西安', '2018-04-01'),
(16, '16', '周芷若', '女', 18, NULL, '北京', '2012-06-01'); -- 使用 NULL 而不是空值




--------------------基础查询---------------------------

-- 查询指定字段name , workno,age返回
SELECT name AS sname,workno as sworkno, age as sage FROM emp;

--  查询所有字段
SELECT * FROM emp;

-- 查询所有员工地址
SELECT workaddress FROM emp;

-- 查询所有员工工作地址,起别名
SELECT workaddress as address FROM emp;

-- 查询公司员工上班地址(不重复)
SELECT workaddress FROM emp WHERE ;




-----------------------条件查询--------------------------

-- 查询年龄等于88的员工
SELECT * FROM emp WHERE age = 88;

-- 查询年龄小于 20 的员工
SELECT * FROM emp WHERE age < 20;

-- 查询年龄小于等于20的员工信息
SELECT * FROM emp WHERE age <= 20;

-- 查询没有省份证的员工信息
SELECT * FROM emp WHERE idcard IS NULL;


-- 查询有省份证号的员工信息
SELECT * FROM emp WHERE idcard IS NOT NULL;

-- 查询年龄不等于88 的员工信息
SELECT * FROM emp WHERE age != 20 AND age != 88;

-- 查询年龄在15(包含) 到 20(包含) 的信息
SELECT * FROM emp WHERE age >= 15 AND age <= 20;

-- 查询性别为女 且年龄小于 25的信息
SELECT * FROM emp WHERE age >= 15 AND age <= 20 AND gender = '女';

-- 查询年龄等于18 或20 或 40 的信息
SELECT * FROM emp WHERE age = 18 OR age = 20 OR age = 40;

-- 查询姓名为两个字的信息
SELECT * FROM emp WHERE name like '__';

-- 查询身份证号最后一位为X的信息
SELECT * FROM emp WHERE idcard LIKE '%X';




---------------------------聚合函数---------------------


-- 统计企业员工数量
SELECT count (id) as '员工数量' FROM emp;
SELECT count (*) as '员工数量' FROM emp;

-- 统计员工平均年龄
SELECT AVG (age) as '平均年龄' FROM emp;

-- 统计员工最大年龄
SELECT max (age) as '最大年龄' FROM emp;

-- 统计员工最小年龄
SELECT min (age) 'minAge' FROM emp;

-- 统计西安地区年龄之和
SELECT sum(age) FROM emp WHERE workaddress = '西安';




-----------------------分组查询------------------------

SELECT 字段列表 FROM 表名 [WHERE 条件] GROUP BY 分组字段名 [HAVING 分组后过滤条件]

-- 根据性别分组,统计男性和女性员工的数量
SELECT gender, count(*) FROM emp GROUP BY gender;

SELECT 
    COUNT(CASE WHEN gender = '男' THEN 1 END) AS '分组后男',
    COUNT(CASE WHEN gender = '女' THEN 1 END) AS '分组后女'
FROM emp;


-- 根据性别分组,统计 男性 和 女性 员工的平均年龄
SELECT gender, avg(age) FROM emp GROUP BY gender;


--  查询小于45岁的员工, 并根据工作地址分组,获取员工数量大于等于3的工作地址
SELECT workaddress, count(*) FROM emp WHERE age < 45 GROUP BY workaddress HAVING count(*) >= 3;




---------------------排序查询--------------------
SELECT 字段列表 FROM 表名 GROUP BY 字段1 排序方式1, 字段2 排序方式2; 

-- 根据年龄对公司员工进行升序排序
SELECT * FROM emp ORDER BY age;
SELECT * FROM emp ORDER BY age ASC;

-- 根据入职时间,对员工进行降序排序
SELECT * FROM emp ORDER BY entrydate DESC;

-- 根据年龄对员工进行升序排序,年龄相同,再按照入职时间进行降序排序
SELECT * FROM emp ORDER BY age ASC, entrydate DESC;




--------------------------分页查询--------------------------
SELECT 字段名 FROM 表名 LIMIT 起始索引,查询记录数;

-- 查询第一页员工数据,每页展示10条记录
SELECT * FROM emp LIMIT 1 ,10;

-- 查询第二页员工数据,每页展示10条记录
SELECT * FROM emp LIMIT 10,10;




---------------------案例--------------------

-- 查询年龄为20,21,22,23岁员工信息
SELECT * FROM emp WHERE age = 20 OR age = 21 OR age = 22 OR age = 23;

-- 查询性别为 男,并且年龄在20~40以内的姓名为三个字的员工
SELECT * FROM emp WHERE gender = '男' AND age BETWEEN 20 AND 40;

-- 统计员工表中,年龄小于60,男性员工和女性员工的人数
SELECT gender, count(*) FROM emp WHERE age < 60 GROUP BY gender;

-- 查询所有年龄小于等于35岁员工的姓名和年龄,并对查询的结果按年龄升序,如果年龄相同按入职时间降序排序
SELECT * FROM emp WHERE age <= 35 ORDER BY age ASC, entrydate DESC;

-- 查询性别为男,且年龄在20~40以内的前5个员工信息,并对查询的结果按年龄升序,如果年龄相同按入职时间降序排序
SELECT * FROM emp WHERE age BETWEEN 20 AND 40 AND gender = '男' ORDER BY age ASC, entrydate DESC LIMIT 0,5;

```
---
## DCL
#### <center>管理用户
```sql
-- 查询用户
USE mysql;
SELECT * FROM user;

-- 创建用户
CREATE USER '用户名'@'主机名' IDENTIFIED BY '密码';

-- 修改用户密码
ALTER USER '用户名'@'主机名' IDENTIFIED WITH mysql_native_password BY '新密码';

-- 删除用户
DROP USER '用户名'@'主机名';

# 主机名可以使用%通配符
# 这类sql开发人员操作较少,主要是dba(数据库管理员)人员使用
```

#### <center>权限控制
| 权限 (加粗为常用)       | 说明                                             |
| ----------------------- | ------------------------------------------------ |
| **SELECT**              | **允许用户从表中选择数据。**                     |
| **INSERT**              | **允许用户向表中插入数据。**                     |
| **UPDATE**              | **允许用户更新表中的现有数据。**                 |
| **DELETE**              | **允许用户从表中删除数据。**                     |
| **CREATE**              | **允许用户创建新数据库或表。**                   |
| DROP                    | 允许用户删除数据库或表。                         |
| INDEX                   | 允许用户创建和删除索引。                         |
| ALTER                   | 允许用户修改数据库或表的结构。                   |
| GRANT OPTION            | 允许用户将其权限授予其他用户。                   |
| EXECUTE                 | 允许用户执行存储过程或函数。                     |
| FILE                    | 允许用户读写文件系统上的文件。                   |
| SHOW DATABASES          | 允许用户查看他们有权限访问的数据库列表。         |
| RELOAD                  | 允许用户执行重载操作，如刷新权限。               |
| SHUTDOWN                | 允许用户关闭MySQL服务器。                        |
| PROCESS                 | 允许用户查看其他用户的执行过程。                 |
| SUPER                   | 允许用户执行高级操作，如停止线程和设置全局变量。 |
| CREATE TEMPORARY TABLES | 允许用户创建临时表。                             |
| LOCK TABLES             | 允许用户锁定表以便独占访问。                     |


```sql
-- 查询权限
SHOW GRANTS FOR '用户名'@'主机名';

-- 授予权限
GRANT 权限列表 ON 数据库名.表名 TO '用户名'@'主机名';

-- 撤销权限
REVOKE 权限列表 ON 数据库名.表名 FROM '用户名'@'主机名';

# 多个权限之间用','逗号分隔
# 授权时,数据库名和表名可以使用 * 进行通配,代表所有
```
---
##### <center>案例
```sql
--------------用户管理--------------------------------

-- 创建用户test 只能在Localhost主机访问,密码123456
CREATE USER 'test'@'localhost' IDENTIFIED BY '123456';

-- 创建用户dong可在任意主机访问,密码123456
CREATE USER 'dong'@'%' IDENTIFIED BY '123456';

-- 修改用户test 密码为1234
ALTER USER 'test'@'localhost' IDENTIFIED WITH mysql_native_password BY '1234';

-- 删除test用户
DROP USER 'test'@'localhost';



-------------------------权限控制------------------
SELECT * FROM user;

-- 查询权限
SHOW GRANTS FOR 'root'@'localhost';
SHOW GRANTS FOR 'test'@'localhost';

-- 授予权限
GRANT all  ON test_database.* TO 'test'@'localhost';

-- 撤销权限
REVOKE all ON test_database.* TO 'test'@'localhost';

```

---
## 函数
函数是指一段可以直接被另一段程序调用的程序或代码
#### <center>字符串函数
| 函数                             | 功能                                                                               |
| -------------------------------- | ---------------------------------------------------------------------------------- |
| `LENGTH(str)`                    | 返回字符串 `str` 的字节长度。                                                      |
| `CHAR_LENGTH(str)`               | 返回字符串 `str` 的字符长度。                                                      |
| `LOWER(str)`                     | 将字符串 `str` 转换为小写字母。                                                    |
| `UPPER(str)`                     | 将字符串 `str` 转换为大写字母。                                                    |
| `SUBSTRING(str, pos, len)`       | 从字符串 `str` 的 `pos` 位置开始，返回长度为 `len` 的子字符串。                    |
| `TRIM(str)`                      | 删除字符串 `str` 开头和结尾的空格。                                                |
| `CONCAT(str1, str2, ...)`        | 连接多个字符串并返回结果。                                                         |
| `REPLACE(str, old, new)`         | 用新字符串 `new` 替换字符串 `str` 中的旧字符串 `old`。                             |
| `INSTR(str, substr)`             | 返回子字符串 `substr` 在字符串 `str` 中首次出现的位置（从1开始）。                 |
| `FIND_IN_SET(str, str_list)`     | 检查字符串 `str` 是否在以逗号分隔的字符串列表 `str_list` 中，返回位置（从1开始）。 |
| `LEFT(str, len)`                 | 返回字符串 `str` 的左边 `len` 个字符。                                             |
| `RIGHT(str, len)`                | 返回字符串 `str` 的右边 `len` 个字符。                                             |
| `REVERSE(str)`                   | 返回字符串 `str` 的反转字符串。                                                    |
| `SOUNDEX(str)`                   | 返回字符串 `str` 的 Soundex 字符串，用于发音相似的匹配。                           |
| `FORMAT(number, decimal_places)` | 返回格式化的数字字符串，保留 `decimal_places` 位小数。                             |
| `LPAD(str,n,pad)`                | 左填充,用字符串`pad`对`str`的左边进行填充,达到`n`个字符串                          |
| `RPAD(str,n,pad)`                | 右填充,用字符串`pad`对`str`的左边进行填充,达到`n`个字符串                          |

`select 函数(参数);` 

##### <center> 案例
```sql
--------------字符串函数------------------
SELECT LENGTH('hello mysql'); -- 11
SELECT LOWER('HELLO'); -- hello
SELECT SUBSTRING('hello world',1,7); -- hello w
SELECT TRIM('  ffjal '); -- ffjal
SELECT LPAD('01',5,'-'); -- ---01


-- 将企业员工的工号统一为5位数,不足5为数前面补0,如00001,00002
UPDATE emp SET workno = LPAD(workno,5,'0');
```

#### <center>数值函数
| 函数                          | 功能                                                       |
| ----------------------------- | ---------------------------------------------------------- |
| `ABS(x)`                      | 返回数字 `x` 的绝对值。                                    |
| `CEIL(x)`                     | 返回大于或等于 `x` 的最小整数。                            |
| `FLOOR(x)`                    | 返回小于或等于 `x` 的最大整数。                            |
| `ROUND(x, d)`                 | 将数字 `x` 四舍五入到 `d` 位小数。                         |
| `TRUNCATE(x, d)`              | 截断数字 `x` 到 `d` 位小数，不进行四舍五入。               |
| `POWER(x, y)`                 | 返回 `x` 的 `y` 次幂。                                     |
| `SQRT(x)`                     | 返回数字 `x` 的平方根。                                    |
| `MOD(x, y)`                   | 返回 `x` 除以 `y` 的余数。                                 |
| `GREATEST(x1, x2, ...)`       | 返回参数中最大的值。                                       |
| `LEAST(x1, x2, ...)`          | 返回参数中最小的值。                                       |
| `RAND()`                      | 返回 0 到 1 之间的随机浮点数。                             |
| `SIGN(x)`                     | 返回数字 `x` 的符号（1 表示正数，0 表示零，-1 表示负数）。 |
| `CONV(N, from_base, to_base)` | 将数字 `N` 从 `from_base` 进制转换为 `to_base` 进制。      |
| `FLOOR_DIV(x, y)`             | 返回 `x` 除以 `y` 的整数部分。                             |

##### <center> 案例
```sql
-----------------数字函数---------------
SELECT ABS(-87); # 87
SELECT CEIL(77.3); # 78
SELECT SQRT(9); # 3
SELECT RAND() AS '随机数';



-- 通过函数生成一个6位数的随机验证码
SELECT LPAD(CEIL(RAND() * 1000000),6,0);
```

#### <center>日期函数
| 函数                                 | 功能                                               |
| ------------------------------------ | -------------------------------------------------- |
| `CURDATE()`                          | 返回当前日期（不带时间）。                         |
| `NOW()`                              | 返回当前日期和时间。                               |
| `DATE(expr)`                         | 从日期或日期时间表达式中提取日期部分。             |
| `TIME(expr)`                         | 从日期时间表达式中提取时间部分。                   |
| `YEAR(date)`                         | 返回日期 `date` 的年份部分。                       |
| `MONTH(date)`                        | 返回日期 `date` 的月份部分（1-12）。               |
| `DAY(date)`                          | 返回日期 `date` 的日部分（1-31）。                 |
| `WEEK(date)`                         | 返回日期 `date` 在一年中的周数（0-53）。           |
| `DATEDIFF(date1, date2)`             | 返回日期 `date1` 与 `date2` 之间的天数差。         |
| `DATE_ADD(date, INTERVAL expr unit)` | 返回将指定时间间隔 `expr` 加到 `date` 后的日期。   |
| `DATE_SUB(date, INTERVAL expr unit)` | 返回将指定时间间隔 `expr` 从 `date` 中减去的日期。 |
| `STR_TO_DATE(str, format)`           | 将字符串 `str` 按照指定格式 `format` 转换为日期。  |
| `DATE_FORMAT(date, format)`          | 将日期 `date` 格式化为指定的字符串格式 `format`。  |
| `LAST_DAY(date)`                     | 返回指定日期 `date` 所在月份的最后一天。           |

##### <center> 案例
```sql
-----------------日期函数--------------------
SELECT CURDATE(); #2024-11-03
SELECT now();
SELECT DATE(NOW());
SELECT TIME(NOW());
SELECT WEEK(NOW());
SELECT MONTH(NOW());
SELECT DAY(NOW());
SELECT DATE_ADD(NOW(), INTERVAL 70 DAY);
SELECT DATEDIFF(NOW(), DATE_ADD(NOW(), INTERVAL 70 DAY));

-- 查询所有员工入职天数,并根据入职天数倒叙排序
SELECT name, DATEDIFF(NOW(), entrydate) AS '入职到现在的天数' 
FROM emp 
ORDER BY entrydate DESC;
```

#### <center>流程函数
| 函数                                     | 功能                                                             |
| ---------------------------------------- | ---------------------------------------------------------------- |
| `IF(condition, true_value, false_value)` | 根据条件返回不同的值。                                           |
| `CASE WHEN THEN`                         | 提供条件判断，可以在多个条件中选择返回值。(编程语言的Switch语句) |
| `COALESCE(value1, value2, ...)`          | 返回第一个非NULL的值。                                           |
| `NULLIF(value1, value2)`                 | 如果 `value1` 等于 `value2`，则返回 NULL；否则返回 `value1`。    |
| `IFNULL(value, default_value)`           | 如果 `value` 为 NULL，则返回 `default_value`；否则返回 `value`。 |
| `LEAST(value1, value2, ...)`             | 返回参数中最小的值。                                             |
| `GREATEST(value1, value2, ...)`          | 返回参数中最大的值。                                             |
| `ELT(N, value1, value2, ...)`            | 返回第 `N` 个值（从 1 开始）。                                   |
| `FIELD(value, value1, value2, ...)`      | 返回 `value` 在参数列表中的位置（从 1 开始），如果没有则返回 0。 |

##### <center> 案例
```sql
------------流程函数-----------------------
SELECT if(true, 'ok','no'); #  ok
SELECT if(FALSE, 'ok','no'); #  no
SELECT IFNULL(NULL,'ok'); # ok
SELECT IFNULL('fjaklsf','ok'); # fjaklsf

----- case-------

--查员工的工作的地址 ,将 北京/伤害 一线城市   其他为 二线城市
SELECT 
name , 
(case workaddress
    WHEN '北京' THEN '一线城市'
    WHEN '上海' THEN '一线城市'
    else '二线城市' END) AS '工作地址'
FROM emp



-- 
CREATE TABLE scores (
    id INT PRIMARY KEY COMMENT 'ID',
    name VARCHAR(50) NOT NULL COMMENT '姓名',
    math INT COMMENT '数学成绩',
    chinese INT COMMENT '语文成绩',
    english INT COMMENT '英语成绩'
) COMMENT '学生成绩表';

INSERT INTO scores (id, name, math, chinese, english) VALUES
(1, 'Alice', 88, 92, 85),   -- 优秀
(2, 'Bob', 76, 65, 70),      -- 及格
(3, 'Charlie', 95, 90, 89),  -- 优秀
(4, 'Diana', 55, 60, 58),    -- 不及格
(5, 'Ethan', 82, 79, 64);     -- 及格


SELECT * FROM scores;

-- 根据成绩展示 >=85 为优秀  >=60 为及格 其他为不及格
SELECT 
    id,
    name,
    CASE 
        WHEN math >= 85 THEN '优秀'
        WHEN math >= 60 THEN '及格'
        ELSE '不及格'
    END AS math_grade,
    CASE 
        WHEN chinese >= 85 THEN '优秀'
        WHEN chinese >= 60 THEN '及格'
        ELSE '不及格'
    END AS chinese_grade,
    CASE 
        WHEN english >= 85 THEN '优秀'
        WHEN english >= 60 THEN '及格'
        ELSE '不及格'
    END AS english_grade
FROM 
    scores;
```

---


## 约束

- **概念: 约束是作用在表中字段上的规则,用于限制存储在表中的数据**
- **目的: 保证数据库中数据的正确,有效和完整性**

| 约束类型 | 描述                                                | 关键字        |
| -------- | --------------------------------------------------- | ------------- |
| 主键约束 | 唯一标识表中的每一行，不能为NULL。                  | `PRIMARY KEY` |
| 外键约束 | 约束表中列的值必须在另一表的主键列中存在。          | `FOREIGN KEY` |
| 唯一约束 | 确保列中的所有值都是唯一的，允许一个NULL值。        | `UNIQUE`      |
| 非空约束 | 确保列不能有NULL值。                                | `NOT NULL`    |
| 检查约束 | 确保列中的值满足指定的条件（MySQL 8.0及以上支持）。 | `CHECK`       |
| 默认约束 | 为列设置默认值，当插入数据时未指定该列的值时使用。  | `DEFAULT`     |

##### <center> 案例
<center>通过sql创建该表结构

| 字段名 | 字段含义   | 字段类型    | 约束条件                  | 约束关键字                  |
| ------ | ---------- | ----------- | ------------------------- | --------------------------- |
| id     | ID唯一标识 | int         | 主键，并且自动增长        | PRIMARY KEY, AUTO_INCREMENT |
| name   | 姓名       | varchar(10) | 不为空，并且唯一          | NOT NULL, UNIQUE            |
| age    | 年龄       | int         | 大于0，并且小于等于120    | CHECK                       |
| status | 状态       | char(1)     | 如果没有指定该值，默认为1 | DEFAULT                     |
| gender | 性别       | char(1)     | 无                        |                             |

```sql
--------------约束------------------
CREATE Table test_table(
    id int PRIMARY KEY AUTO_INCREMENT COMMENT 'ID唯一标识符',
    name VARCHAR(10) NOT NULL UNIQUE COMMENT '姓名',
    age int CHECK(age BETWEEN 0 AND 120) COMMENT '年龄',
    status CHAR(1) DEFAULT '1' COMMENT '状态',
    gender CHAR(1) COMMENT '性别'
) COMMENT '测试表'
```

#### <center>外键约束
```sql
-- 语法
CREATE Table 表名(
    字段名 数据类型,
    ....
    [CONSTRAINT] [外键名称] FOREIGN KEY(外键字段名) REFERENCES 主表(主表列名)
);
ALTER Table 表名 ADD CONSTRAINT 外键名称 FOREIGN KEY(外键字段名) REFERENCES 主表(主表列名);

-- 删除外键语法
ALTER Table 表名 DROP FOREIGN KEY 外键名称;
```

#### <center>外键删除更新行为
| 行为类型      | 说明                                                                                        |
| ------------- | ------------------------------------------------------------------------------------------- |
| `RESTRICT`    | 禁止删除或更新父表中的记录。如果子表中存在引用的记录，则父表中对应记录不能被删除或更新。    |
| `CASCADE`     | 级联删除或更新。删除或更新父表中的记录时，子表中对应的记录会自动被删除或更新。              |
| `SET NULL`    | 设置为NULL。删除或更新父表中的记录时，子表中对应外键字段会被设置为NULL。                    |
| `NO ACTION`   | 不采取任何行动。类似于`RESTRICT`，但在检查时间上有所不同（在一些SQL模式下无效果）。         |
| `SET DEFAULT` | 设置为默认值。删除或更新父表中的记录时，子表中对应外键字段会被设置为默认值（MySQL不支持）。 |

```sql
ALTER Table 表名 ADD CONSTRAINT 外键名称 FOREIGN KEY (外键字段) REFERENCES 主表名(主表字段名) ON UPDATE CASCADE ON DELETE CASCADE;
```

### 多表查询
