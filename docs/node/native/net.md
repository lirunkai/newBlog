# net

## net.Server

用于创建TCP或者IPC server的一个类

### 创建net.Server实例

`let server = net.createServer()`

### 拥有的事件

`close` 当server被关闭时触发

`error` 出现错误的时候触发 handler(err)

`listening` 监听端口的时候触发

**获取地址** `server.address()`

**关闭连接** `server.close()` 停止 server接受建立新的connections, 返回server

**服务开始监听** `server.listen({port, host, })` 可以调用多次, 每次调用都会重新打开服务器, 返回server

**断开连接** `server.unref()`

**恢复链接** `server.ref()`

## net.Socket

用于创建Socket类

### 创建Socket

`let socket = net.createConnection({port})`

## 事件

`close`  socket关闭后触发 handler(had_error)

`connect` 当一个 socket 连接成功建立的时候触发该事件

`data` 接受到数据触发 handler(buffer)

`drain`  当写入缓冲区变为空时触发

`end`  当 socket 的另一端发送一个 FIN 包的时候触发，从而结束 socket 的可读端

`error` 当错误发生时触发

`timeout`  超时触发

**获取地址** `socket.address()`

**总字节** `socket.bufferSize`

**已读字节** `socket.bytesRead`

**发送的字节** `socket.bytesWritten`

**销毁Socket** `socket.destroy()` 确保socket上没有连接后

**是否销毁** `socket.destroyed` 是否销毁了

**发送数据** `socket.write()` 在 socket 上发送数据

**半关闭数据** `socket.end(data)` 返回socket本身

**暂停数据流** `socket.pause()` 暂停读写数据

**恢复数据流**  `socket.resume()` 恢复数据流

**设置超时** `socket.setTimeout(time)`  返回socket本身


### net判断

`net.isIP(input)` 测试input是否是IP地址, 无效是0， IPv4返回4, IPv6返回6

`net.isIPv4(input)` 测试input是否是IPv4

`net.isIPv6(input)` 测试input是否是IPv6
