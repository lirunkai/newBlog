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



## URL

包含若干静态方法的对象，用来创建 URLs



+++

涉及到的其他知识

### 三次握手（three-way handshake）

在TCP/IP协议中，TCP协议提供可靠的连接服务，采用三次握手建立一个连接。

在连接创建过程中，很多参数要被初始化，例如序号被初始化以保证按序传输和连接的强壮性

第一次握手: 建立连接时, 客户端发送syn(syn=j)包到服务器, 进入SYN_SEND状态, 等待服务器确认

第二次握手: 服务器收到syn包, 必须确认客户端的syn(ack=j+1),同时自己也发送一个syn(syn=k)包,即SYN+ACK包, 此时服务器进入SYN_RECEIVED状态

第三次握手: 客户端收到SYN+ACK包, 向服务端发送ACK(ack=k+1)包, 此包发送完毕, 服务端和客户端进入ESTABLISHED状态， 完成三次握手

> SYN(同步序列编号)是TCP/IP建立连接时使用的握手信号
>
> ACK(确认字符) ，在数据通信中，接收站发给发送站的一种传输类控制字符。表示发来的数据已确认接收无误。

SYN-ACK 重传次数: 服务器发送完SYN-ACK包之后,如果未收到客户确认包，服务器将进行首次重传,等待一段时间仍未收到客户确认包，进行第二次重传，如果重传次数超过系统规定的最大重传次数，系统将该连接信息从半连接队列中删除。注意，每次重传等待的时间不一定相同。

半连接存活时间: 是指半连接队列的条目存活的最长时间，也即服务从收到SYN包到确认这个报文无效的最长时间，该时间值是所有重传请求包的最长等待时间总和。有时我们也称半连接存活时间为Timeout时间

半连接队列: 服务器第一次收到客户端的 SYN 之后，就会处于 SYN_RCVD 状态，此时双方还没有完全建立其连接，服务器会把此种状态下请求连接放在一个队列里，我们把这种队列称之为**半连接队列**。

三次握手的作用: 

1. 确认双方的接受能力,发送能力是否正常
2. 指定自己的初始化序列号, 为后面的可靠传送做准备
3. 如果是 https 协议的话，三次握手这个过程，还会进行数字证书的验证以及加密密钥的生成到。

### 四次挥手

一开始双方处于establised状态. 

假如客户端先发起关闭请求,则:

第一次挥手:  客户端发送一个FIN报文,报文中会指定一个序列号, 此时客户端处于CLOSE_WAIT1状态

第二次挥手: 服务端收到FIN报文, 会发送 ACK 报文且把客户端的序列号值 + 1 作为 ACK 报文的序列号值，表明已经收到客户端的报文了, 此时服务端处于CLOSE_WAIT2状态

第三次挥手: 如果服务端也想断开连接了，和客户端的第一次挥手一样，发给 FIN 报文，且指定一个序列号。此时服务端处于 **LAST_ACK** 的状态

第四次挥手: 客户端收到 FIN 之后，一样发送一个 ACK 报文作为应答，且把服务端的序列号值 + 1 作为自己 ACK 报文的序列号值，此时客户端处于 **TIME_WAIT** 状态。需要过一阵子以确保服务端收到自己的 ACK 报文之后才会进入 CLOSED 状态

服务端收到 ACK 报文之后，就处于关闭连接了，处于 CLOSED 状态

> TIME_WAIT 
>
> 为什么客户端发送 ACK 之后不直接关闭，而是要等一阵子才关闭。这其中的原因就是，要确保服务器是否已经收到了我们的 ACK 报文，如果没有收到的话，服务器会重新发 FIN 报文给客户端，客户端再次收到 ACK 报文之后，就知道之前的 ACK 报文丢失了，然后再次发送 ACK 报文。
>
> IME_WAIT 持续的时间至少是一个报文的来回时间。一般会设置一个计时，如果过了这个计时没有再次收到 FIN 报文，则代表对方成功就是 ACK 报文，此时处于 CLOSED 状态。

> **FIN** （finish）结束



