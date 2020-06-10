### DDL

数据定义语言

`show databases`  显示所有数据库名称

`use 数据库名` 切换数据库

`create database 数据库名字`  创建数据库

`drop databse 数据库名字` 删除数据库

### 表

`create table 表名<列名 列类型， 列名 列类型>` 创建表

```mysql
CREATE TABLE classes (
    id BIGINT NOT NULL AUTO_INCREMENT,
    name VARCHAR(100) NOT NULL,
    PRIMARY KEY (id)
) ENGINE=InnoDB DEFAULT CHARSET=utf8;
```



### 添加数据

添加单条数据

```mysql
INSERT INTO students (id, class_id, name, gender, score) VALUES (1, 1, '小明', 'M', 90);
```

添加多条数据

```mysql
INSERT INTO students (id, class_id, name, gender, score) VALUES 
(1, 1, '小明', 'M', 90),
(2, 1, '小红', 'F', 95),
(3, 1, '小军', 'M', 88),
(4, 1, '小米', 'F', 73);
```

查询字段

SELECT 字段名（多个字段用,相隔, *代表所有字段） FROM 表名

```mysql
select * from students;
```

添加过滤条件

WHERE

单个过滤条件时 直接写

过滤id为1

```mysql
select * from students where id = 1;
```

多个过滤条件时使用AND 或者 OR

```mysql
SELECT * FROM students WHERE score >= 80 OR gender = 'M';
```

```mysql
SELECT * FROM students WHERE score >= 80 AND gender = 'M';
```

除了 = 还可以使用`> < >= <=`

还有个特殊的LIKE `name LIKE 'ab%'` %表示任意字符



### 排序 order by

按score从低到高

```mysql
select * from students order by score;
```

添加DESC表示倒序

```mysql
select * from students order by score desc;
```

如果有`WHERE`子句，那么`ORDER BY`子句要放到`WHERE`子句后面

### 分页

LIMIT <M> OFFSET <N>

```mysql
SELECT id, name, gender, score
FROM students
ORDER BY score DESC
LIMIT 3 OFFSET 0;
```

通过COUNT函数可以查询一个表一共有多少条数据

```mysql
select COUNT(*) from students;
```



### 更新

```mysql
UPDATE students SET score=score+10 WHERE score<80;
```





### 事物

把多条语句作为一个整体进行操作的功能，被称为数据库*事务*。数据库事务可以确保该事务范围内的所有操作都可以全部成功或者全部失败。如果事务失败，那么效果就和没有执行这些SQL一样，不会对数据库数据有任何改动

要手动把多条SQL语句作为一个事务执行，使用`BEGIN`开启一个事务，使用`COMMIT`提交一个事务，这种事务被称为*显式事务*，例如，把上述的转账操作作为一个显式事务：

```mysql
BEGIN;
UPDATE accounts SET balance = balance - 100 WHERE id = 1;
UPDATE accounts SET balance = balance + 100 WHERE id = 2;
COMMIT;
```

