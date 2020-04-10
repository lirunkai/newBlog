

Flutter

记录下flutter的使用方式，以及一些默认规则.

> flutter 一切皆组建
>
> dart 一切皆对象

`lib/main.dart`  **flutter**的主文件

`main` 主函数

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









