## python

内置全局函数

`ord()` 获取字符的整数表示

`chr()` 把编码转换为对应的字符

`encode()`  编码为指定的bytes

`decode()`  解析bytes为str

`len()` 查看有多少个字符

`format()` 格式化字符串 `'hello, {0}, 成绩提升了{1}%'.format('猪猪', 12)`

`input()` 读取用户输入, 返回输入的str

`range()` 生成整数序列

`isinstance()` 数据类型检查

`enumerate()` 将list变成索引-元素对

### 数学算法

`abs()` 获取绝对值

`max()` 返回最大的输入

`hex()` 转换成十六进制表示的字符串

#### 数据类型转换

`int()` 将字符串转换成整数

`list()` 转换为list类型

`float()` 转换为浮点数

`str()`  转换为字符串

将字符串str转成bytes `b''`

#### 类型判断

`type(test) == str` 判断是不是字符串

`type(test) == int` 判断是不是整数

`type(test) == types.FunctionType`

`type(test) == types.BuiltinFunctionType`

`type(test) == types.LambdaType`

`isinstance(test, Type)` 判断test是不是Type类型

### 替换字符

`%s`  替换字符串

`%d`  替换整数

`%f`  替换浮点数

```python
'我说%s, 你有%d元' % ('kk', 1000)
```

#### 类型

**字符串**     `''`

**Boolean**       `True False`

**list**   `[]`

**tuple** `()`元组 ，声明了就不能修改

**dict**  `key-value` 字典

**set**  不重复  `s = set([1,2,3])`

### Str

`replace()`  替换 `'a'.replace('a', 'A')` 

## list

`list.append` 插入list最后

`list.pop(i)` 没有传入i删除最后的元素, 如果传入i，删除指定位置i的数据

`list.insert(index)` 在index的位置插入数据

`list.sort()`  排序

`list.count(x)` 返回x在list中出现了几次

`list.index(item)` 查看item在list中的index

`list.count(item)` item在list中出现了几次

`list.remove(x)` 移除list中第一个值为x的元素

`list.index(x, start, end)`  获取第一个值为x的索引

`list.clear()` 清空list

`list.reverse()` 翻转list

`list.copy()`  浅拷贝

切片 `L[0:3]` 取

### dict属性和方法

`in`  判断key是否存在 `key in dict`

`get()`  判断key是否存在 `dict.get(key, -1)`

`pop(key)` 删除key `dict.pop(key)`

循环

`for key in dict` 迭代key

`for value in dict.values()` 迭代value

`for k, v in dict.items()`  同时迭代key和value

### set

`add（key）`  添加一个key到set

`remove(key)` 删除一个key

### 条件判断

`if else `

`if elif else `

```python
if x > 10:
		print('x>10')
elif x > 5:
		print('x>5')
else:
		print('x > 0')
```



### 循环

`for in`

```python
names = ['Michael', 'Bob', 'Tracy']
for name in names:
    print(name)
```

`while`

```python
sum = 0
n = 99
while n > 0:
		sum = sum + n
		n = n - 2
print(sum)
```

`break` 退出结束循环

`continue` 调过本次循环

### 函数

声明 ： `def 函数名(参数):` 

函数内通过`return`返回计算后的数据, 如果没有写return, 默认返回`None`

```python
def printHello(str):
		return 'hello,%s' %str
```

**默认参数** 

默认参数必须指向不变对象

```python
def printLog(str='world'):
		return 'hello, %s' %str
```

**可变参数** 接收的是一个tuple

`*参数`

```python
def printLog(*logs):
		return logs
```

**关键字参数** 接收的是一个dict

`def defName(arg1, arg2, **arg)`

命名关键字参数

`def name(arg1, arg2, *, nameArg1, nameArg2)`

### 函数

`lambda x: x*x` 表示声明匿名函数    `:`前面的是参数  后面的是表达式,返回结果  lambda只能有一个表达式

`__name__` 函数的名字

**装饰器**

代码运行期间动态增加功能的方式, 称为装饰器(Decorator)

decorator就是一个返回函数的高阶函数

`@property` 把一个方法变成属性调用

### 作用域

`_` private变量, 不应该直接引用

### 类 class

`__init__(self)` 

+ 第一个参数必须是self表示创建的实例本身
+ 创建实例时需要传入和`__init__`相同的参数, self不用传

>>> 类中定义的函数, 第一个参数必须是self, 但是在调用时不需要传递self

`__变量` 私有变量 外部无法读取私有变量, 需要通过定义类方法来读取

`hasattr(obj, key)` obj有属性key么？ 返回True或False

`getattr(obj, key)`  获取某个属性

`setattr(obj, key, value)` 设置某个属性

`__slots__` 属性 限制class实例能添加的属性

`__str__`  函数, 定义输出

## 元类

`metaclass`  允许你创建类或者修改类



## sys

`argv` 存储了命令行的所有参数

+ 第一个参数永远是.py文件的名称
+ 使用list存储



## os

`os.name`  操作系统类型 

+ `posix`  linux
+ `nt`   windows

`os.environ` 在操作系统中定义的环境变量

`os.environ.get(key)` 获取某个key的environ

`os.path.abspath('.')`  查看当前目录的绝对路径

`os.path.join(basePath, joinPath)` 返回组装好的完整路径

`os.path.split(path)`  拆分一个路径，后一部分总是最后级别的目录或文件名

`os.path.splitext(path)` 拆分路径, 最后一部分是文件扩展名

`os.rename(oldName, nowName)` 重命名文件

`os.remove(path)` 删除文件

`os.path.isdir(path)` 当前路径是不是文件夹

`os.path.isfile(path)` 当前路径是不是文件

`os.listdir(path)` 当前路径下的所有文件夹

`os.mkdir(path)` 创建目录

`os.rmdir(path)` 删掉一个目录

`os.fork()` 创建一个子进程

`os.getpid()` 获取主进程pid

## multiprocessing

**Process** 进程对象

`Process(执行函数, 执行函数的参数)` 创建了子进程

`Process().start()` 启动子进程

`Process().join()` 等待子进程结束

**Pool** 进程池

**subprocess** 子进程

## threading 线程

`threading.Thread(target=函数, name=名称)`  创建一个线程

`threading.Thread().start()`  启动一个线程

`threading.Thread().join()`  等待线程执行完毕

`threading.current_thread()` 返回当前进程的实例

`threading.Lock()` 创建一个锁

`lock.acquire()`  获取锁

`loack.release()` 释放锁

## re正则 

`re.match(regexp, str)` 判断是否匹配，如果匹配成功，返回一个`Match`对象，否则返回`None`

`re.split(regexp, str)`  分割字符串

`r()`  在正则中使用`()` 标识需要提取的字串, 可以在match返回的group中通过索引获取， `group(0)` 永远返回的是初始字符串, 匹配的字串从索引1开始

## shutil

## JSON

`json.dumps(dict)` 将一个dict对象变成JSON， 返回str

`json.loads(dict)` 反序列化, 将JSON字符串转为python的数据类型


## logging

### 文件

`flag`

+ r 读
+ w 写
+ b 二进制

`open(path, flag)` 打开文件

`read(size)` 读取文件内容， 读取size

`readline()` 每次读取一行内容, 按行返回list

`close()` 关闭文件

## datetime 处理日期和时间

**datatetime**

`dt = datetime.now()`

`datetime.now()` 获取当前日期和时间

`dt.timestamp()`  将时间转换为timestamp

`datetime.fromtimestamp(timestamp)` 将timestamp转换为时间

`datatime.strptime(dateStr, format)` 将datestr转换为时间

**timedelta** 对时间进行加减

`timedelta(days=1, hours=3)`

## collections

**namedtuple** 定义一种数据类型，它具备tuple的不变性，又可以根据属性来引用

```python
Point = namedtuple('Point', ['x', 'y'])
p = Point(1, 2)
p.x //1
p.y //2
```

### deque 高效插入和删除list元素

```python
del = deque([1,2,3])
del.append(4)
del.appendleft(0)
del.pop()
del.popleft()
```

### defaultdict dict拥有默认值

`defaultdict(lambda)` dict没有默认值时， 返回默认值

**OrderedDict**  可以保持dict的key的顺序

## Socket

`s = socket.socket(socket.AF_INEF, socket.STREAM)` 创建一个socket

`s.connect((host, port))` 建立连接



## 模块

模块是一个包含Python定义和语句的文件. 

`__name__` 获取当前模块的文件名，通过`python` 命令行运行时`__name__`被设置为`__main__`

---

`pass` 语句, 占位语句, 使程序可以正常运行