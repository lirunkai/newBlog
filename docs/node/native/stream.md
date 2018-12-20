# stream

stream贯穿在整个node中, 是很基础的一个node原生包, 许多node其他的包都基于strema来做. 比如`http` `fs` `process`

stream分为 `stream.Writable`可写流。 `stream.Readable`可读流。 `stream.Duplex` `stream.Transform`

数据流的特性: 数据会缓存在内部的缓冲器中等待读取。

## Writable 可写流

当调用 writable.write(chunk) 时，数据会被缓冲在可写流中。 当内部的可写缓冲的总大小小于 highWaterMark 设置的阈值时，调用 writable.write() 会返回 true。 一旦内部缓冲的大小达到或超过 highWaterMark 时，则会返回 false

### 事件

`close` 当流或其底层资源（比如文件描述符）被关闭时触发， 不是所有的可写流都会触发`close`事件（目前还不知道哪个实例不会触发）  

`drain` 写入到流失败（`writable.write(chunk)`返回false）, 可再次写入时触发

`error` 写入数据发生错误时触发

`finish` 调用`end()`后触发

`pipe` 在可读流中调用`pipe()`时触发  handler(Readable)

`unpipe` 在可读流中调用`unpiep()`时触发 handler(Readable)

---

`writable.cork()` 强制把所有写入的数据都缓冲到是内存中

`writable.uncork()` 释放`cork`的数据

`writable.destroy(error)` 销毁流,触发error并且传入error参数

`writable.end(chunk， encoding, cb)`  表明已经没有数据要写入可读流， 执行完之后触发`finish`事件

`writable.write(chunk, encoding, cb)` 写入数据到数据流

`writable.writableHighWaterMark` 返回可写流的`highWaterMark`值

## Readable 可读流

调用`stream.push(chunk)`时, 数据被缓冲在可读流中, 如果流的消费者没有调用`stream.read()` 则数据会保留在可读流中直到被消费, 如果到达可读流的`highWaterMark`, 将停止读取数据

可读流的两种模式：

  1. 流动模式, 数据自动从底层系统读取, 通过EventEmitter接口的事件
  2. 暂停模式, 必须显式调用`stream.read()`读取数据块

可读流默认都处于 **暂停模式**

切换到流动模式(readable.readableFlowing切换为true)： `stream.resume()` `stream.pipe()`    添加`data`事件

切换到暂停模式(readable.readableFlowing切换为false)：  `stream.pause()` `stream.unpipe()`

### 拥有的事件

`close` 底层流被关闭时触发

`data`  当流将数据块传递给消费者之后触发 handler(data)

`end` 当流中没有数据可供消费时触发

`error` 底层出错时触发 handler(error)

`readable` 当流中有数据可供读取时触发

---

`readable.destroy(error)` 销毁流，触发`error`和`close`事件

`readable.isPaused()` 返回可读流当前的操作状态

`readable.pause()` 使流动模式的流停止触发`data`事件， 并切换出流动模式 返回this

`readable.pipe(Writable)` 绑定可写流到可读流, 将可读流自动切换到流动模式，并将可读流的数据推送到可写流 数据流会自动管理 返回可写流

`readable.unpipe(Writable)` 返回this 解绑`stream.pipe()`绑定的可写流

`readable.read([size])` 从内部数据拉取并返回数据， 如果没有可读数据返回null

`readable.resume()` 将暂停的可读流恢复到流动模式，并消费流中的数据 返回this

`readable.setEncoding(encoding)` 设置数据的字符编码

`readable.readableHighWaterMark`  返回构造可读流时传入的highWaterMark的值



## Duplex 可写可读流

维护着两个相互独立的内部缓冲器用于读取和写入， 这使得它们在维护数据流时，读取和写入两边可以各自独立地运作

同时实现了`Readable`和`Writable`

## Transform 读写中转换流

维护着两个相互独立的内部缓冲器用于读取和写入， 这使得它们在维护数据流时，读取和写入两边可以各自独立地运作
