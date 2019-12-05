## Sqlalchemy

`pip install PyMySQL`

`pip install flask-MysqlAlchemy`

新建一个db

```python
from flask import Flask
from flask.ext.sqlalchemy import SQLAlchemy

db = SQLAlchemy()

def create_app():
		app = Flask(__name__)
    app.config['SQLALCHEMY_DATABASE_URI'] = 'mysql://root:password@localhost:3306/throne'
		db.init_app(app)
		return app
```

表

`db.Model`

列

`db.Column(columnType, primary_key)`

- columnType
  - `db.Integer` 整数
  - `db.String(size)` 字符串
  - `db.Text` 一些较长的 unicode 文本
  - `db.DateTime` 表示为 Python `datetime` 对象的 时间和日期
  - `db.Float` 浮点值
  - `db.Boolean` 浮点值
  - `db.PickleType` 存储为一个持久化的Python对象
  - `db.LargeBinary` 存储一个任意大的二进制数据
- `primary_key`  是否是主键, 默认是False

外键

`db.ForeignKey(外键的值)` 



`db.relationship(ModelName, backref, lazy)`

- ModelName 声明关联的表的名字
- `backref` 在ModelName类上声明新属性的方法
  - `db.backref(Column, lazy)` 为新属性设置`lazy`
- `lazy` 决定了什么时候从数据库加载数据
  - `select`  SQLAlchemy 会使用一个标准的 select 语句必要时一次加载数据。
  - `joined` SQLAlchemy 使用 JOIN 语句作为父级在同一查询中来加载关系
  - `subquery` 
  - `dynamic` SQLAlchemy 会返回一个查询对象，在加载数据前您可以过滤（提取）它们

一对多



多对多



`from flask_sqlalchemy import SQLAlchemy`

`db = SQLAlchemy(app)`

### 数据库模型 db.Model

```python
class User(db.Model):
		id = db.Column(db.Integer, primary_key=True)
		name = db.Column(db.String(20), unique=True)
    
    def __init__(self, name):
      self.name = name
```

### 增

```python
user1 = User("bo")
user2 = User('user2')
db.session.add(user1)
db.session.add(user2)
db.session.commit()
```



### 删

```

```



### 改

### 查

`Model.query`

+ `filter()`    过滤
+ `filter_by()`  过滤
+ `order_by()`  排序
+ `limit()`  限制返回数量
+ `all()` 返回所有
+ `get()`
+ `first()`

### 根据模型创建数据库表

`db.create_all()`

废弃表 重新创建

`db.drop_all() `  之后 `db.create_all()`



