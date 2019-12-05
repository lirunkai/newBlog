

Flutter

记录下flutter的使用方式，以及一些默认规则.

> flutter 一切皆组建
>
> dart 一切皆对象

`lib/main.dart`  **flutter**的主文件

`main` 主函数

## 布局

### 水平布局 Row

### 垂直布局 Column

### 主轴  main

使用column时, 垂直方向时主轴, 使用row时 水平方向时主轴

`mainAxisAlignment: MainAxisAlignment.center`

value

+ MainAxisAlignment.start 居左对齐
+ MainAxisAlignment.center 居中对齐
+ MainAxisAlignment.end 居右对齐

### 副轴 cross

cross 和主轴垂直的方向

`crossAxisAlignment: CrossAxisAlignment.center`

value

- CrossAxisAlignment.start 居左对齐
- CrossAxisAlignment.center 居中对齐
- CrossAxisAlignment.end 居右对齐

### SafeArea 安全布局

+ bottom 
  + false 可以使用底部
+ child

### Expanded 扩展空间

按比例扩伸子组件所占的空间

可以实现灵活布局

+ flex
+ child

### Stack 层叠布局

类似前端的绝对定位



### Flex布局









### Text

**textAlign** 文本的对齐方式

通过`TextAlign.value`  value值有

+ center 居中对齐
+ left 左对齐
+ right 右对齐
+ start 以开始位置对齐
+ end 以结束位置对齐

eg

```dart
child:Text(
	'aaaaa',
    textAlign: TextAlign.left
)
```

**maxLines** 最多显示的行数

**overflow** 设置文本溢出时，处理方式

value

+ clip 切断, 删除之后的文字
+ ellipsis 后面的用省略号表示
+ fade 溢出的部分会有一个渐变消失的效果

eg

```
child:Text(
	'aasdasdasdasdad',
	overflow: TextOverflow.ellipsis
)
```

### TextSpan

如果需要对一个Text内容的不同部分按照不同的样式展示, 需要使用TextSpan

```dart
const TextSpan({
	TextStyle style,
  String text,
  List<TextSpan> children,
  GestureRecognizer recognizer
})
```



### Container

**alignment**  针对`Container`中的`child`的对齐方式

通过`Alignment.value`来设置， value有

+ bottomCenter bottomLeft bottomRight
+ topCenter topLeft topRight
+ center centerLeft centerRight

**padding** `Container`的内边距

通过`EdgeInsets.fromLTRB()`来设置四个方向的内边距

**margin** `Container`的外边距

通过`EdgeInsets.fromLTRB()` 来设置四个方向的外边距

**color** `Container`的背景颜色

**decoration**  用来修饰`Container`,主要修改背景和边框

通过`new BoxDicoration`来设置decoration

decoration内部gradient 通过`LinearGradient`设置背景渐变

decoration内部border 通过`Border.all`来设置边框

### Image

### Navigator

`Navigator`是一个管理路由的`widget`，它通过一个栈(先进后出)来管理一个路由`widget`集合，通常当前屏幕显示的页面就是栈顶的路由。

`Navigator.push(BuildContext context, Route route)`

 将给定的路由入栈(即打开新的页面),返回一个`Future`对象,用以接受新路由出栈时的返回数据.

`Navigator.pop(BuildContext context, result)`

将栈顶路由出栈,`result`为页面关闭时返回给上一个页面的数据

### MaterialPageRoute

继承自`PageRoute`，表示占有整个屏幕空间的一个模态路由页面,定义了路由构建及切换时过度动画的相关接口及属性。

```dart
MaterialPageRoute({
    WidgetBuilder: builder,
    RouteSetting: setting,
    bool maintainState= true,
    bool fullscreenDialog=false
})
```

+ `builder` 是一个WidgetBuilder类型的回调函数，作用是构建路由页面的具体内容，返回值是一个widget。我们通常要实现此回调, 返回新路由的实例.
+ `setting`包含路由的配置信息，如路由名称，是否是初始路由
+ `maintainState` 默认情况下 当入栈一个新路由时,原来的路由仍然会保存在内存中,如果想在路由没用的时候释放所占用的资源,设置为false
+ `fullscreenDialog` 表示新的路由页面是否是一个全屏的模态对话框,在ios中 如果`fullscreenDialog`为true，新页面会从屏幕底部滑入

## 路由表

要想使用命名路由,得先注册一个路由表

```dart
return new MaterialApp(
	title: 'Flutter demo',
	theme: new Theme(
		primarySwatch: Colors.blue
	),		
  routes: {
    'name': (context) => NewRoute()
  },
  home: new MyHomePage()
)
```

通过路由名称打开新路由页

`pushNamed(BuildContext context, String routeName, {Object arguments})`

`Navigator.pushNamed(context, 'name')`

带参数

`Navigator.of(context).pushNamed('name', arguments: 123)`

获取参数

`ModalRoute.of(context).settings.arguments`

## 包管理

通过使用配置文件`pubspec.yaml`来管理第三方依赖包

```yaml
dependencies:
	flutter:
		sdk: flutter
	cupertino_icons: ^0.1.0	
dev_dependencies:
	english_words: ^3.1.3
```

本地包

```yaml
dependencies:
	pkg1: 
		path: ../../code/pkg1
	pkg2:
  	git:
  		url: git://github.com/xxx/pkg1.git
```

### 关于资源

同样是使用`pubspec.yaml`来管理

```yaml
flutter:
	assets: 
		- assets/my_icon.png
		_ assets/background.png
```

#### 加载assets

**加载文本assets** 通过`rootBundle`对象加载, `rootBundle`可以访问主资源包

```dart
import 'dart:async' show Future;
import 'package:flutter/services.dart' show rootBundle;
Future<String> loadAsset() async{
	return await rootBundle.loadString('assets/config.json');
}
```

`DefaultAssetBundle` 使用`DefaultAssetBundle`来获取当前`BuildContext`的`AssetBundle`。

#### 加载图片

`AssetImage` 可以将asset的请求逻辑映射到最接近当前设备像素比例（dpi）的asset. 为了使这种映射起作用, 必须根据特定的目录结构来保存asset

```
.../image.png
.../2.0x/image.png
.../3.0x/image.png
```

```dart
Widget build(BuildContext context) {
	return new DecoratedBox(
  	decoration: new BoxDecoration(
      	image: new DecotationImage(
        	image: new AssetImage('graphics/background.png')
        )
    )
  )
}
```



`flutter packages get`

`flutter run`

`flutter doctor`

`flutter upgrade`









