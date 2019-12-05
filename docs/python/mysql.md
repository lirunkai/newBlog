## Mysql

### 库

`CREATE DATABASE 库`  创建一个库

`DELETE DATABASE 库` 删除一个库

`use 库` 使用某个库

### 表

查询

`SELECT`

+ `*` 返回所有列

+ `FROM`  指定要查询的表或视图
+ `JOIN` 根据连接条件从其他表获取数据
+ `WHERE` 过滤结果集中的行
  + `AND` 多个条件
  + `BETWEEN` 选择在给定范围内的值
  + `LIKE` 匹配基于模式匹配的值
  + `IS NULL` 检查值是否是NULL
  + `IN`  匹配列表中的任何值
  + 运算符
    + `= > < != >= <=`
+ `ORDER BY ` 指定用于排序的列的列表
+ `LIMIT` 限制返回行的数量

`CREATE` 创建

```mysql
CREATE TABLE IF NOT EXISTS tasks (
    task_id INT(11) AUTO_INCREMENT,
    subject VARCHAR(45) DEFAULT NULL,
    start_date DATE DEFAULT NULL,
    end_date DATE DEFAULT NULL,
    description VARCHAR(200) DEFAULT NULL,
    PRIMARY KEY (task_id)
)ENGINE=InnoDB DEFAULT CHARSET=utf8;
```



`INSERT` 插入

`INSERT INTO tasks(subject,start_date,end_date,description)`

`VALUES('Learn MySQL INSERT','2017-07-21','2017-07-22','Start learning..');`

`UPDATE` 更新

```mysql
UPDATE employees 
SET 
    lastname = 'Hill',
    email = 'mary.hill@yiibai.com'
WHERE
    employeeNumber = 1056;
```

`DELETE`

```mysql
DELETE FROM 表名
WHERE 条件
LIMIE 3;
```

`ALTER` 修改当前表结构

`ALTERTABLEtable_name action1[,action2,…]`

+ `ADD COLUMN columnname` 添加列
+ `CHANGE COLUMN  columnname` 修改列
+ `DROP COLUMN columnname` 删除列