## Flutter 基本元素 Text

### Text

单个样式时，可直接使用Text

```dart
Text(
	String data, 
  {
		TextStyle style, 
    StrutStyle strutStyle, 
		TextAlign textAlign, 
		TextDirection textDirection, 
		TextOverflow overflow, 
		int  maxLines,
    double textScaleFactor,
    Locale locale,
    bool softWrap,
    String semanticsLabel,
    TextWidthBasis textWidthBasis
  }
)
```

### RichText

展示多个不同的文本样式，必须明确指明使用什么样式

```dart
RichText({
	@required InlineSpan text, // 多样式文本
  TextAlign textAlign: TextAlign.start, // 水平文本对齐方式
  TextDirection textDirection, 
  bool softWrap: true, // 是否可换行
  TextOverflow overflow: TextOverflow.clip, //超出空间时如何展示
  double textScaleFactor: 1.0,
  int maxLines, // 最大行数
  Locale locale, 
  StrutStyle strutStyle,
  TextWidthBasis textWidthBasis: TextWidthBasis.parent
})
```

### TextSpan

可以内联的Text

```dart
TextSpan({
  	String text,
	  List<InlineSpan> children,
   	TextStyle style,
		GestureRecognizer 	recognizer,
  	String semanticsLabel
})
```

#### 文本的修饰类

##### TextAlign enum

控制文本位置的展示

+ `TextAlign.center ` 居中
+ `TextAlign.left`
+ `TextAlign.right`
+ `TextAlign.justify`
+ `TextAlign.end`
+ `TextAlign.start`

##### TextDirection enum

文本的书写方式, 从右到左 或者其他

+ `TextDirection.ltr`  从左到右
+ `TextDirection.rtl` 从右到左

##### TextOverflow

超出text边界时如何展示

+ `TextOverflow.clip`       切割,  不显示
+ `TextOverfow.ellipsis`      点点点展示
+ `TextOverflow.fade`       渐隐
+ `TextOverflow.visible`  不显示

##### TextWidthBasis

文本长度

+ `TextWidthBasis.longesLine`  字符串长度
+ `TextWidthBasis.parent`  父级宽度, 如果单行文本, 最大为文本的长度

##### TextStyle

```dart
TextStyle({
  bool inherit:true,
  Color color,
  Color backgroundColor,
  double fontSize,
  FontWeight fontWeight,
  double letterSpacing,
  double wordSpacing,
  TextBaseline textBaseline,
  double height,
  Locale locale,
  Paint foreground,
  Paint background,
  List<Shadow> shadow,
  List<FontFeature> fontFeatures,
  TextDecoration decoration,
  Color decorationColor,
  TextDecorationStyle decorationStyle,
  double decorationThickness,
  String debugLabel,
  String fontFamily,
  List<String> fontFamilyFallback,
  String package
})
```

##### FontStyle   enum

字体的显示

+ `FontStyle.italic` 斜体
+  `FontStyle.nomal` 正常

##### FontWeight  class

字体粗细

+ `FontWeight.w100`
+  `FontWeight.w200`    ....    `FontWeight.w900`
+  `FontWeight.bold`  === `FontWeight.w700`
+  `FontWeight.normal` === `FontWeight.w400`

##### TextBaseline enum

垂直方向上字体的对齐方式

+ `TextBaseline.alphabetic`
+  `TextBaseline.ideographic`

##### TextDecoration class

文本的装饰

+ `TextDecoration.lineThrough`  横穿文本的装饰
+  `TextDecoration.overline`  文本上方添加装饰
+  `TextDecoration.underline`  文本下方添加装饰

##### TextDecorationStyle enum

文本的装饰样式

+ `TextDecorationStyle.dashed`
+  `TextDecorationStyle.dotted`
+  `TextDecorationStyle.double`
+  `TextDecorationStyle.solid`
+  `TextDecorationStyle.wavy`

##### Shadow  class

文本的阴影设置

##### DefaultTextStyle

默认的text继承的样式类

```dart
DefaultTextStyle({
  @required TextStyle style,
  TextAlign textAlign,
  bool softWrap: true,
  TextOverflow overflow: TextOverflow.clip,
  int maxLines,
  TextWidthBasis textWidthBasis: TextWidthBasis.parent,
  @required Widget child
})
```

`DefaultTextStyle.of(context)` 从context上继承textStyle

#### DefaultTextStyleTransition

**来个🌰**

先看图
![text](https://aidoudou.top/_media/text_flutter.png)

```dart
import 'package:flutter/material.dart';

class TextDemo extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return Scaffold(
      appBar: new AppBar(
        title: Text('TextDemo'),
      ),
      body: new TextDetail(),
    );
  }
}

class TextDetail extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return Column(
      crossAxisAlignment: CrossAxisAlignment.start,
      children: <Widget>[
        Container(
          child: new Text(
            '单个样式文本的时候使用Text, align为left',
            style: TextStyle(
              fontSize: 16,
              color: Colors.red,
            ),
            textWidthBasis: TextWidthBasis.parent,
            textAlign: TextAlign.right,
          ),
        ),
        Container(
          child: new Text(
            '单个样式文本的时候使用Text, align为start, 单个样式文本的时候使用Text, align为left, 单个样式文本的时候使用Text, align为left',
            maxLines: 2,
            style: TextStyle(
              fontSize: 16,
              color: Colors.red
            ),
            textAlign: TextAlign.end,
          ),
        ),
        Container(
          child: new Text(
            '多行文本时, overflow为clip, align为start, 单个样式文本的时候使用Text, align为left, 单个样式文本的时候使用Text, align为left',
            maxLines: 1,
            overflow: TextOverflow.clip,
            style: TextStyle(
              fontSize: 16,
              color: Colors.red
            ),
          ),
        ),
        Container(
          child: new Text(
            '多行文本时, overflow为ellipsis, align为start, 单个样式文本的时候使用Text, align为left, 单个样式文本的时候使用Text, align为left',
            maxLines: 1,
            overflow: TextOverflow.ellipsis,
            style: TextStyle(
              fontSize: 16,
              color: Colors.red
            ),
          ),
        ),
        Container(
          child: new Text(
            '多行文本时, overflow为fade, align为start, 单个样式文本的时候使用Text, align为left, 单个样式文本的时候使用Text, align为left',
            maxLines: 1,
            overflow: TextOverflow.fade,
            style: TextStyle(
              fontSize: 16,
              color: Colors.red
            ),
          ),
        ),
        Container(
          child: new Text(
            '多行文本时, overflow为visible, align为start, 单个样式文本的时候使用Text, align为left, 单个样式文本的时候使用Text, align为left',
            maxLines: 1,
            overflow: TextOverflow.visible,
            style: TextStyle(
              fontSize: 16,
              color: Colors.red
            ),
          ),
        ),
        Container(
          child: RichText(
            textAlign: TextAlign.start,
            text: TextSpan(
              text: 'xxxx',
              style: TextStyle(
                fontSize: 14,
                color: Colors.red
              ),
              children: <TextSpan>[
                TextSpan(
                  text: '多',
                  style: TextStyle(
                    fontSize: 14,
                    color: Colors.green
                  )
                ),
                TextSpan(
                  text: '个',
                  style: TextStyle(
                    fontSize: 14,
                    color: Colors.red
                  )
                ),
                TextSpan(
                  text: '内',
                  style: TextStyle(
                    fontSize: 14,
                    color: Colors.blue
                  )
                ),
                TextSpan(
                  text: '联',
                  style: TextStyle(
                    fontSize: 14,
                    color: Colors.orange
                  )
                ),
                TextSpan(
                  text: '文',
                  style: TextStyle(
                    fontSize: 14,
                    color: Colors.green
                  )
                ),
                TextSpan(
                  text: '本',
                  style: TextStyle(
                    fontSize: 14,
                    color: Colors.orange
                  )
                )
              ]
            )
          ),
        )
      ],
    );
  }
}
```

