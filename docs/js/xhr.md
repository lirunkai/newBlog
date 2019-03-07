XHR

在Web上我们通过XHR来和服务端进行交互, 我们可以通过URL来获取数据, 而无需刷新页面。

### XHR（XMLHttpRequest）

```javascript
let ajax = new XMLHttpRequest()
```

#### 事件

`onreadystatechange`  readystate发生变化时触发

`onopen`

`onerror`

`onmessage`

`ontimeout`

#### 属性

`readyState `   当前xhr的请求状态码

  		1.  `ajax.readyState == 0` 代理被创建, 没有调用open方法 
  		2.  `ajax.readyState == 1` open方法被调用
  		3.   `ajax.readyState == 2` send方法被调用
  		4.  `ajax.readyState == 3` 下载数据中
  		5.  `ajax.readyState == 4` 下载操作完成

`timeout` 请求被自动终止的毫秒数, 默认是0, 意味着没有超时.

`status` 返回xhr的响应中的数字状态码 `eg: 200 400 300`

`withCredentials`  跨域时是否传递cookie

#### 方法

`abort()`  终止请求

`open()` 初始化一个请求

`send()` 发送请求

`upload()` 返回一个`XMLHttpRequestUpload`对象, 用来表示上传的进度. 

​	可以在被绑定的upload对象上添加事件监听器去获取上传进度

​	 `onloadstart` 获取开始 `onprogress` 数据传输中 `onabort` 获取操作终止 `onerror` `onload`获取成功

​	`onloadend` 获取完成 `ontimeout` 获取操作在用户规定的时间内未完成

`getAllResponseHeaders()` 以字符串的形式返回响应头

`getResponseHeader(name)`  返回响应头中的name的值

`setResponseHeader(name)` 设置Http请求头的值

