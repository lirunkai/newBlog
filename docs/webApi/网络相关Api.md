# 网络相关的API

## XMLHttpRequest

在Web上我们通过XHR来和服务端进行交互, 我们可以通过URL来获取数据, 而无需刷新页面。

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

1. `ajax.readyState == 0` 代理被创建, 没有调用open方法 
2. `ajax.readyState == 1` open方法被调用
3. `ajax.readyState == 2` send方法被调用
4. `ajax.readyState == 3` 下载数据中
5. `ajax.readyState == 4` 下载操作完成

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



## WebSocket

`WebSocket()` 创建一个`WebSocket`对象

`let ws = new WebSocket(wsurl, protocol)`

`wsurl` websocket服务端的路径

`protocol` 子协议

### 事件

**ws.onopen** 当`WebSocket`的readyState状态为`OPEN`时调用. 

**ws.onmessage** 当从服务器收到一条消息时触发, 监听器接受`MessageEvent`为参数

**ws.onclose**  在readyState变成`CLOSE`时调用，接受`CloseEvent`为参数

**ws.onerror** 定义一个发生错误时执行的回调函数.

### 函数

**ws.close(【code】, 【reason】)**

关闭Websocket.  

`code` `CloseEvent`允许的数字码

`reason` 字符串, 解释连接关闭的原因

**ws.send(data)**

将需要传输的数据排入队列

`data`的类型为 `USVString, ArrayBuffer, Blob, ArrayBufferView`

### 属性

**ws.readyState** 返回当前`WebSocket`的连接状态. 只读无法修改

1. `0` CONNECTING 正在连接
2. `1` OPEN 已经连接可以通讯
3. `2` CLOSING 连接正在关闭
4. `3` CLOSED 连接已关闭或者没有连接成功

**ws.url**  返回当前WebSocket的url

**ws.binaryType** 返回websocket连接所传输二进制数据的类型 `blob`或者`arrayBuffer` 

**ws.bufferedAmount** 返回已经被`send`方法放入队列但是还没发送到网络中的数据的字节数

**ws.protocol**  返回服务端选中的子协议的名字

## MessageEvent

代表一段被目标对象接收的消息

### 属性

**data**  服务端发送的数据

**origin** 发送者的来源

**lastEventId** 

**source** 发送者对象

**ports**  表示消息正通过特定渠道发送的相关端口



## CloseEvent

### 属性 

**reason** 表示服务器关闭的原因

**wasClean** 表示连接是否完全关闭

## URLSearchParams

定义了一些方法来处理URL的查询字符串

`let searchParams = new URLSearchParams(urlString)`

### 方法

**searchParams.has(key)** 是否拥有某个key

**searchParams.append(key, value)** 插入一个指定的键/值对作为新的搜索参数，添加多个不会覆盖

**searchParams.delete(key)** 从搜索参数中删除指定的搜索参数以及对应的值

**searchParams.get(key)** 获取参数中第一个与搜索参数对应的值

**searchParams.getAll(key)** 返回与搜索参数对应的所有值

**searchParmas.set(key)** 插入一个值，会删除之前的值

**searchParams.toString()** 返回适用在URL中的字符串

**searchParams.sort()**

**searchParmas.keys()**

**searchParams.values()**

**searchParams.entries()**

