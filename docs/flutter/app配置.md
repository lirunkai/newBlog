MaterialApp

配置当前App

比如配置router，home页的展示.

```dart
MaterialApp({
   Key key,
   GlobalKey<NavigatorState> navigatorKey,
   Widget home, //主页
   Map<String, WidgetBuilder> routes: const {}, // 路由的定义
   String initialRoute, //初始时路由 默认为 '/'
   RouteFactory onGenerateRoute, // routes中没有注册的会调用工厂函数来创建路由
   RouteFactory onUnknownRoute, // 不知道的路由生成函数
   List<NavigatorObserver> navigatorObservers: const [], // 监听所有路由跳转动作
   TransitionBuilder builder,
   String title,
   GenerateAppTitle onGenerateTitle,
   Color color,
   ThemeData theme,
   ThemeData darkTheme,
   ThemeMode themeMode: ThemeMode.system
})
```

##### TransitionBuilder



##### ThemeData

##### NavigatorObserver   class

监听Navigator的操作

`NavigatorObserver()`

方法

+ `didPop(Route route, Route previousRoute)` Navigator.pop之后触发
+ `didPush(Route route, Route previousRoute)`  Navigator.push之后触发
+ `didRemove(Route route, Route previousRoute)`  Navigator.remove之后触发
+ `didReplace(Route route, Route previousRoute)` 替换之后触发

##### RouteFactory

通过给定的setting来创建路由

`**typedef** RouteFactory = Route<**dynamic**> Function(RouteSettings settings);`

