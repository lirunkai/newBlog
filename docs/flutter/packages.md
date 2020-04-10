auto_size 自动适配屏幕

```dart
import 'package:auto_size/auto_size.dart';
void main() => runAutoSizeApp(MyApp());

void main() => runAutoSizeApp(MyApp(), width: designWidth, height: designeight);
```

### fluro

路由package

定义页面的handler

定义页面的路由

### dio

请求库

引入 

`import 'package:dio/dio.dart`

`Dio dio = Dio()`

发送get请求 `res = await dio.get('/user', queryParameters: {a: '1'})`

发送post请求 `res = await dio.post('/user/list', data: {pageSize: 10})`

多个并发 `res = await Future.wait([dio.post('/user/list'), dio.get('/user')])`

下载文件 `res = await dio.download('/url', '.xxxx.pdf')`

发送formData 

```dart
FormData formData = FormData.from({
	"name": "name",
	"age": "age"
})
res = await dio.post('/formdata', data: formData)
  
  // 上传多个文件
  FormData.fromMap({
    "name": "wendux",
    "age": 25,
    "file": await MultipartFile.fromFile("./text.txt",filename: "upload.txt"),
    "files": [
      await MultipartFile.fromFile("./text1.txt", filename: "text1.txt"),
      await MultipartFile.fromFile("./text2.txt", filename: "text2.txt"),
    ]
  });
response = await dio.post("/info", data: formData);
```

### provider

