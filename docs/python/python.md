python 是动态类型语言

也就是说以下是成立的， 不会报错

```python
a = "123"
a = 123
```

这里记录下 python 和 js 语法的不一致的地方

1. 声明 python 不需要`let const`等标记进行变量声明 直接写就行
2. python 的布尔值是 True 和 False.
3. 多行字符串使用`'''...'''`
4. 与 and 或 or 非 not
5. if 语句使用`:` `if age >= 18:` if elif else
6. for 语句同样适用`:` `for name in names:`
7. while 语句同样使用`:` `while m > 0:`

### 语句

```python
while m > 0:
	pass

if age>= 18:
	pass

for name in names:
	pass

for x in len(names):
	pass

for x in range(1, len(names)):
	pass
```

### 关键字

`in` 测试一个序列是否包含某个值

`is` 判断

### 自带函数

`range(num)` 生成一个整数序列

`list()` 转换为 list

`abs(num)` 返回一个数字的绝对值

`int()` 转换为整数

`float()` 转换为浮点数

`str()` 转换为字符串

`bool()` 转换为布尔值

`map(fn, list)` 列表的每一项都执行 fn, 返回一个新列表. fn 的第一项是列表的元素

`all(iterable)` 判断给定的可迭代参数 iterable 中的所有元素是否都为 TRUE，如果是返回 True，否则返回 False。

`filter(fn, list)` 过滤序列

`sorted(list, key=fn)` 排列

`type()` 判断对象类型

`ord()` 返回传入的字符串对应的ASCII码

### string

`ord()` 获取字符的整数表示 `ord('A') #65`

`chr()` 把编码转换为对应的字符 `chr(65) #A`

`str.lower()` 返回小写的字符串

`str.upper()` 返回大写的字符串

`str.isalpha()` 返回是否只由字母组成

`str.join(list)` 返回一个由 iterable 中的字符串拼接而成的字符串, 如果有非字符串报错

格式化

`%s` 替换字符串

`%d` 替换数字

`%f` 替换浮点数

```python
'hi, %s, you have $%d' % ('michael', 100)
```

### list

一种有序的集合 `classmates = ['michael', 'bob', 'tracy']`

`len(list)` 表示 list 的长度

`list.append(item)` 插入元素到 list 末尾

`list.insert(index, item)` 插入元素到 list 的 index 位置

`list.extend(iterable)` 类似`a[len(a):]=iterable`

`list.remove(x)` 移除列表中第一个值为 x 的元素

`list.pop()` 删除队尾元素

`list.pop(index)` 删除索引位置的元素

`list.clear()` 清空列表

`list.index(x, [start, end])` 返回 list 列表中第一个元素为 x 的索引

`list.count(x)` 返回 list 列表中 x 出现的次数

`list.reverse()`

`list.sort()`

`list.copy()` 返回列表的浅拷贝

切片

`list[start:end:step]`

取出 start 到 end 的元素, 不包含 end（前开后闭原则）

start, end, step 都可以为负数

step 相隔多少取一次

```python
a = [1,3,2,4]
a[::-1]
// [4,2,3,1]
```

### tuple 元组

通过`,`相隔，创建一个元祖， 一般需要使用`()`包裹

初始化之后不可修改 `classmates=('michael', 'bob', 'tra')`

元组只能通过下标访问

### set

一组没有重复 key 的集合

通过`set([key1, key2])` 或者`{key1, key2}` 来创建一个 set

`s = set([1,2,3])`

`s.add(key)` 添加元素到 set 中

`s.remove(key)` 从 set 中删除 key

### dict

字典 也就是 js 中的 object，使用(key-value)存储

通过`{key: value}`直接声明 或者通过`dict([(key, value), (key, value)])` `dict(key=value, key=value)`来声明

1. 查询某个 key 时, 需要使用`d[key]`，不能使用`.`查询
2. 通过`in`判断 key 是否存在`key in dict`
3. 通过`d.get(key, [value])` 如果 key 不存在返回 None， 或者指定的 value

`d.values()` 返回 value 的 list

`d.items()` 返回 key-value 的 list

### 函数

定义: 通过`def`定义一个函数 函数的返回值需用 return 语句返回

1. 函数是为了复用
2. pass 占位符可以声明一个空函数
3. 返回多个值时， 实际返回的是一个 tuple
4. 通过`__name__`可以拿到函数名

参数

参数定义的顺序: 必选参数, 默认参数, 可变参数（\*args）, 命名关键字参数, 关键字参数(\*\*dict)

- 位置参数
- 默认参数 默认参数必须指向不可变对象`def perseon(name, age=20)`
- 可变参数 给参数前面添加`*`来声明一个可变参数 `def person(*info)`
- 关键字参数 给参数前面添加`**`来定一个关键字参数 `def person(name, age, **other)`
  - 命名关键字参数, 通过`*`号进行分割, `*`号后的是命名关键字`def perseon(name, age, *, city, job)`

**匿名函数: lambda 表达式`lambda x:x\*x**`

- 冒号之前的为参数
- 冒号之后的为返回

### 装饰器

在代码运行期间动态增加功能的方式, 称之为装饰器

### 列表生成式

`[x * x for x in range(1, 11)]`

`[x * x for x in range(1, 11) if x % 2 == 0]` 仅筛选出偶数的平方

`[m + n for m in 'ABC' for n in 'XYZ']` 双排列

`[x if x % 2 == 0 else -x for x in range(1, 11)]`

### 生成器

在循环的过程中不断推算出后续的元素

将列表生成式的`[]`改成`()`就创建好了一个生成器 generator

generator 的值需要使用 next()来调用，通过 for 循环来取 generator 的值不需要写 next

### 类

通过 class 关键字定义一个类

通过`__init__`方法 可以在创建实例的时候, 绑定一些属性

```python
class Student(object): # 默认从object继承 也可以写其他类
	def __init__(self, name, score):
		self.name = name
		self.score = score
```

私有变量 给变量添加`__`前缀

实例方法 第一个参数永远是 self

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

由于 python 是动态语言, 实例之后可以动态添加属性。那怎么能限制住 class 只能添加某些属性？ 通过`__slots__`来限制该 class 实例能添加的属性 **限制的属性只队当前类实例起作用**

```python
class Student(object):
	__slots__ = ('name', 'age') #元组 tuple来定义
```

类方法装饰器

`@property` 把一个 getter 方法变成属性

`@keyFnName.setter` 由`@property`创建, 负责把一个 setter 方法变成属性赋值

多重继承

```python
class Dog(Mammal, RunnableMixin):
	pass
```

### Enum 类

### 模块

模块搜索路径

1. 包含输入脚本的目录
2. 一个包含目录名称的列表
3. 取决于安装的默认设置

`sys.path`变量是一个字符串列表，用于确定解释器的模块搜索路径

添加模块路径

`sys.path.append()`

```python
import pb

from pb import fn1, fn2

```

---

注意

1. 多重赋值

```python
a, b = 0, 1
while a < 10:
	print(a)
	a, b = b, a+b
```

在任何赋值发生之前就被求值了。右手边的表达式是从左到右被求值的。

2.
