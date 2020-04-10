## Widget

描述一个UI元素的配置数据，Widget其实并不是表示最终绘制在设备屏幕上的显示元素，而它只是描述显示元素的一个配置数据， 真正代表屏幕上显示元素的类是`Element`。

Key

Flutter根据是否有key来决定更新的机制，如果没有key, 只对runtimeType进行对比, 如果有key,则对runtimeType和Key进行联合对比.

Key分为LocalKey 和 GlobalKey

###### LocalKey的子类

+ `ValueKey`  如果您有一个 Todo List 应用程序，它将会记录你需要完成的事情。我们假设每个 Todo 事情都各不相同，而你想要对每个 Todo 进行滑动删除操作
+ `ObjectKey`  如果你有一个生日应用，它可以记录某个人的生日，并用列表显示出来，同样的还是需要有一个滑动删除操作。
+ `UniqueKey` 如果组合的 Object 都无法满足唯一性的时候，你想要确保每一个 Key 都具有唯一性。那么，你可以使用 UniqueKey。它将会通过该对象生成一个具有唯一性的 hash 码。

###### GlobalKey

GlobalKey 能够跨 Widget 访问状态

### StatelessWidget

不需要维护状态的场景

### StatefulWidget

需要维护状态, 内部创建State

`createState`用来多次创建和Stateful Widget相关的状态, 在Stateful Widget生命周期中可能会多次调用

### State

一个StatefulWidget类会对应一个State类，State表示与其对应的StatefulWidget要维护的状态，State中的保存的状态信息可以：

1. 在widget 构建时可以被同步读取。
2. 在widget生命周期中可以被改变，当State被改变时，可以手动调用其`setState()`方法通知Flutter framework状态发生改变，Flutter framework在收到消息后，会重新调用其`build`方法重新构建widget树，从而达到更新UI的目的。

```dart
State()
```

方法

`initState()`  Widget第一次插入到Widget树时会被调用。

`didChangeDependecies()`  依赖发生变化时会调用

`setState(VoidCallback fn)`

`dispose()` 当State对象从树中被永久移除时调用

属性

+ widget 该State实例关联的widget实例
+ context StatefulWidget对应的BuildContext

#### VoidCallback

无参数，无返回

##### GlobalKey`<T extend State<StatefulWidget>>`

在app中的唯一key

实例属性

`currentContext`  

`currentState` 当前的

`currentWidget`



Widget的分类

单个元素类的 `Text` `Img` `Icon`

单个子元素(has child) `RaisedButton` `FloatButton` `OutlineButton`

多个子元素(has children) `TextSpan` `Row`   `Column`



