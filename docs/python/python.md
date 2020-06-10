python是动态类型语言

也就是说以下是成立的， 不会报错

```python
a = "123"
a = 123
```

这里记录下python和js语法的不一致的地方

1. 声明 python不需要`let const`等标记进行变量声明 直接写就行
2. python的布尔值是True 和 False.
3. 多行字符串使用`'''...'''`
4. 与and 或 or 非not
5. if 语句使用`:`  ` if age >= 18:` if elif else
6. for语句同样适用`:`   `for name in names:`
7. while语句同样使用`:`  `while m > 0:`



自带函数

`range(num)` 生成一个整数序列

`list()` 转换为list

`abs(num)`  返回一个数字的绝对值

`int()` 转换为整数

`float()` 转换为浮点数

`str()` 转换为字符串

`bool()` 转换为布尔值

`map(fn, list)` 列表的每一项都执行fn, 返回一个新列表. fn的第一项是列表的元素

`filter(fn, list)` 过滤序列

`sorted(list, key=fn)` 排列

`type()` 判断对象类型

### string

`ord()`  获取字符的整数表示 `ord('A') #65`

`chr()` 把编码转换为对应的字符 `chr(65) #A`

`str.lower()` 返回小写的字符串

格式化

`%s` 替换字符串

`%d` 替换数字

`%f` 替换浮点数

```python
'hi, %s, you have $%d' % ('michael', 100)
```



### list

一种有序的集合 `classmates = ['michael', 'bob', 'tracy']`

`len(list)` 表示list的长度

`list.append(item)` 插入元素到list末尾

`list.insert(index, item)` 插入元素到list的index位置

`list.pop()` 删除队尾元素

`list.pop(index)` 删除索引位置的元素

切片

`list[start:end]` 取出start到end的元素, 不包含end（前开后闭原则）



### tuple 元组

初始化之后不可修改 `classmates=('michael', 'bob', 'tra')`

元组只能通过下标访问



### dict

字典 也就是js中的object，使用(key-value)存储

1. 查询某个key时, 需要使用`d[key]`，不能使用`.`查询
2. 通过`in`判断key是否存在`key in dict`
3. 通过`d.get(key, [value])` 如果key不存在返回None， 或者指定的value

`d.values()` 返回value的list

`d.items()` 返回ke y-value的list



### set

一组没有重复key的集合

`s = set([1,2,3])`

`s.add(key)` 添加元素到set中

`s.remove(key)` 从set中删除key



### 函数

定义: 通过`def`定义一个函数 函数的返回值需用return语句返回

1. 函数是为了复用
2. pass占位符可以声明一个空函数
3. 返回多个值时， 实际返回的是一个tuple
4. 通过`__name__`可以拿到函数名

参数

参数定义的顺序: 必选参数, 默认参数, 可变参数（*args）, 命名关键字参数, 关键字参数(**dict)

+ 位置参数
+ 默认参数 默认参数必须指向不可变对象`def perseon(name, age=20)`
+ 可变参数 给参数前面添加`*`来声明一个可变参数 `def person(*info)`
+ 关键字参数 给参数前面添加`**`来定一个关键字参数 `def person(name, age, **other)`
  + 命名关键字参数, 通过`*`号进行分割, `*`号后的是命名关键字`def perseon(name, age, *, city, job)`

**匿名函数: lambda表达式`lambda x:x*x**`

+ 冒号之前的为参数
+ 冒号之后的为返回

### 装饰器

在代码运行期间动态增加功能的方式, 称之为装饰器



### 列表生成式

`[x * x for x in range(1, 11)]`

`[x * x for x in range(1, 11) if x % 2 == 0]` 仅筛选出偶数的平方

`[m + n for m in 'ABC' for n in 'XYZ']`  双排列

`[x if x % 2 == 0 else -x for x in range(1, 11)]`



### 生成器

在循环的过程中不断推算出后续的元素

将列表生成式的`[]`改成`()`就创建好了一个生成器generator

generator的值需要使用next()来调用，通过for循环来取generator的值不需要写next



### 类

通过class关键字定义一个类

通过`__init__`方法 可以在创建实例的时候, 绑定一些属性

```python
class Student(object): # 默认从object继承 也可以写其他类
	def __init__(self, name, score):
		self.name = name
		self.score = score
```

私有变量  给变量添加`__`前缀

实例方法 第一个参数永远是self

多态： 子集重新定义父集的方法, 每次调用时只会调用子集子集的方法

类属性

```python
class Student(object):
	name='student' # 类属性 所有实例公用
	def	__init__(self, name, score):
		self.name = name #实例属性 属于各个实例 互不干扰
		self.score = score
```

限制属性实例

由于python是动态语言, 实例之后可以动态添加属性。那怎么能限制住class只能添加某些属性？ 通过`__slots__`来限制该class实例能添加的属性 **限制的属性只队当前类实例起作用**

```python
class Student(object):
	__slots__ = ('name', 'age') #元组 tuple来定义
```

类方法装饰器

`@property`  把一个getter方法变成属性

`@keyFnName.setter`  由`@property`创建, 负责把一个setter方法变成属性赋值

多重继承

```python
class Dog(Mammal, RunnableMixin):
	pass
```



Enum类

