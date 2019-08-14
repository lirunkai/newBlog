Dart 语法

### 没有初始化的变量自动获取一个默认值为null

### 声明变量时, 添加具体的类型， 添加类型可以更清晰的表达你的意图

### 胖箭头语法

`=> expr` 是 `{return expr}`的缩写

### 级联调用语法

```dart
void main(){
	querySelector('#sample_text_id')
	..text= "click me"
	..onClick.listen(reverseText);
}
```

使用级联调用语法，可以在一个对象上执行多个操作0

## 声明变量

### var   不声明具体的类型

### final 不打算修改一个变量, final只能赋值一次

### const 编译时常量

## 内置的数据类型

`numbers`     `strings`    ` booleans`   `lists`   `maps`      `runes`     `symbols`

### numbers

`int` 整数值

`double` 双精度浮点数

### String

使用双引号或单引号来创建字符串, 使用`${expression}`来使用表达式，使用三个单引号或者双引号来创建多行字符串

### Booleans

字面量 `bool`

只有true和false,只有完全等于true的才为true, '1, a '这样的为false

### Map

字面量 `map`

Map是一个键值对相关的对象。键和值可以是任何类型的对象，每个键只出现1次，值可以出现多次

注意查找不存在的key时返回null

----

使用`enum`来定义枚举类型，枚举类型中的每一个值都有一个index getter函数, 该函数返回该值在枚举类型定义中的位置

```dart
enum Color {
	red,  green, blue
}
assert(Color.red.index == 0)
List<Color> colors = Color.values;
```



### 类型转换

```dart
// String -> int
var one = int.parse('1')
// string -> double
var onePointOne = double.parse('1.1')
// init -> String
String oneAsString = 1.toString()
// double -> String
String piAsString = 3.14159.toStringAsFixed(2);
```



### 类型判断

`is`  如果对象是指定的类型返回True

`is!` 如果对象是指定的类型返回False

### Functions

可选参数示例

```dart
String say (String form, String to, [String device]) {
	var result = '$from says $msg'
	if(device != null) {
		result = '$result with a $device'
	}
	return result;
}	
```

参数默认值示例

```dart
String say(String from='li', String to='bai'){}
```

### 赋值操作符

`=`  `a=value` 给a变量赋值

`??=`    `b ??=value` 如果b是null,则赋值给b； 如果b不是null, 则b值保持不变

### 条件表达式

`condition ? expr1 : expr2` 如果condition为true, 执行expr1并返回结果, 否则执行expr2并返回结果

`expr1 ?? expr2`  如果expr1是non-null, 返回其值; 否则执行expr2并返回其结果

 ### 定义Class类

```dart
class Point {
	num x;
	num y;
	num z = 0;
}
```

关于construcot的定义

定义一个和类名字一样的方法就定义了一个构造函数。

```dart
class Point {
	num x;
	num y;
	Point(num xm=, num y){
    this.x = x;
    this.y = y;
  }
}
```

关于调用超类构造函数

默认情况下，子类的构造函数会自动调用超类的 无名无参数的默认构造函数。 超类的构造函数在子类构造函数体开始执行的位置调用

 如果提供了一个 [initializer list](http://dart.goodev.org/guides/language/language-tour#initializer-list)（初始化参数列表） ，则初始化参数列表在超类构造函数执行之前执行

如果超类没有无名无参数构造函数， 则你需要手工的调用超类的其他构造函数。 在构造函数参数后使用冒号 (`:`) 可以调用 超类构造函数。

#### 常量构造函数（Constant constructor）

如果你的类提供一个状态不变的对象，你可以把这些对象 定义为编译时常量。要实现这个功能，需要定义一个 `const` 构造函数， 并且声明所有类的变量为 `final`

```dart
class ImmutablePoint {
	final num x;
	final num y;
	const ImmutablePoint(this.x, this.y);
	static final ImmutablePoint origin = const ImmutablePoint(0,0) //使用
}
```

使用常量构造函数 可以创建编译时常量，要**使用**常量构造函数只需要用 `const` 替代 `new` 即可：

两个一样的编译时常量其实是 同一个对象

#### 工厂方法构造函数

如果一个构造函数并不总是返回一个新的对象，则使用`factory`

## 注解

`@override` 表明你的函数是想覆写超类的一个函数

`@`