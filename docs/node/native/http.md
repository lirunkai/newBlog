# http系列

负责接受客户端的请求. 分为几大类`http.Agent` `http.ClientRequest` `http.Server` `http.ServerResponse` `http.IncomingMessage`

**http.Agent** 负责http客户端连接的持续和复用。Agent也就是类似前端的`XMLHttpRequest`

**http.ClientRequest**  表示着一个正在处理的请求，其请求头已进入队列

**http.Server**  请求实例。

**http.IncomingMessage** 用来访问请求头, 平时实例使用`request`

**http.ServerResponse** 实例作为第二个参数传入`request`事件, 表示请求的返回， 平时实例简写为`response`

## 创建一个Http Server

`let server = http.createServer(handler)` 创建一个httpServer， handler(IncomingMessage, ServerResponse)

继承自`net.Server`

### 拥有的事件

`close` 当server被关闭时触发

`error` 出现错误的时候触发 handler(err)

`listening` 监听端口的时候触发

`clientError`  客户端触发了一个`error`事件, 会被传递到这里

`request` 每次接受到一个请求时触发 handler(IncomingMessage, ServerResponse)

---

`server.listen()` 开启HTTP服务器监听连接

`server.listening` 表示服务器是否正在监听

`server.setTimeout(timeout)`

`server.timeout`

`server.keepAliveTimeout` 完成响应后需要等待的毫秒数. 如果超过这个毫秒数则销毁

## 创建一个Http ClientRequest

`let req = http.get(url, (res<IncomingMessage>))`

or

`let req = http.request(options, (IncomingMessage))`

options

  1. method
  2. path
  3. headers
  4. timeout
  5. agent

使用 http.request() 必须调用 req.end() 表明请求的结束  

### 拥有的事件

`abort`  请求被客户端终止时触发, 仅在首次调用`abort`触发

`connect` 每当服务器响应CONNECT请求时触发. handler(IncomingMessage, socket, head)

`response` 当请求的响应被接受到时触发。 该请求只触发一次 handler(IncomingMessage)

---

`request.abort()`  标记请求终止

`request.aborted` 如果请求已终止, 返回true

`request.write(chunk, encoding, cb)` 发送请求主体的一个数据块

`request.end()` 结束发送请求

`request.getHeader(name)` 读取请求头, 大小写不敏感

`request.removeHeader(name)` 移除某个请求头

`request.setHeader(name, value)` 设置请求头， 大小写不敏感

`request.maxHeadersCount` 响应头的最大数量限制, 如果设置为0,则不限制

`request.setTimeout(timeout)`  设置超时的毫秒数
---

## IncomingMessage

`IncomingMessage`对象由 `http.Server` 或 `http.ClientRequest` 创建，并作为第一个参数分别递给 `request` 和 `response` 事件

`IncomingMessage` 是一个可读流

### 拥有的事件

`aborted` 请求被终止时触发

`close` 当底层连接被关闭时触发

---

**是否被终止**  `message.aborted` 请求终止返回true

**头信息** `message.headers` 请求头或者响应头

**请求使用的方法** `message.method`

**原始头信息** `messagee.rawHeaders`

**响应状态码** `message.statusCode`

**请求的URL** `message.url`


## ServerResponse

服务器内部创建, 作为第二个参数传入`request`事件

### 拥有的事件

`close` 调用`response.end()`之后触发

`finish` 响应被发送时触发 `response.finished` 表示响应是否完成

---

`response.addTrailers(headers)`  添加HTTP尾部响应头到响应

`response.setHeader(name, value)` 为一个隐式的响应头设置值

`response.getHeader(name)` 读取一个已入队列, 但是还没有发送到客户端的响应头， 不区分大小写

`response.getHeaderNames()`   返回包含当前响应头名称的数组

`response.getHeaders()` 返回当前响应头文件的浅拷贝

`response.hasHeader(name)` 如果设置了这个name的响应头, 返回true

`response.headersSet` 响应头已被发送返回true

`response.removeHeader(name)`  移除一个响应头

`response.writeHead(statusCode, statusMessage, headers)` 发送一个响应头给请求， 必须在`response.end()`之前调用

`response.write(chunk, encoding, cb)` 发送一块响应体

`response.end(data,encoding, cb)` 通知服务器, 所有响应有和响应体都已经被发送 每次响应都必须调用`response.end()`方法

`response.statusCode` 控制响应头发送到客户端的状态码
