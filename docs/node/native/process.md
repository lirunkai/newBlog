# process

`process` 提供**当前Node进程**的相关信息, 也就是Node启动之后, 可以通过`process`这个全局对象来获取一些信息. 当然`process`能做的还有控制当前的进程,比如杀死当前的进程等等, 来详细了解下

**process作为全局对象, 不需要使用require引入**

**process是EventEmitter的一个实例, 所以注定拥有许多事件**

## 获取信息

`process.cwd()` 获取当前执行文件的目录, 通过`process.env.PWD`也可以访问

`process.cpuUsage()` 包含当前进程的用户CPU时间和系统CPU时间的对象 `{user: int, system: int}`

`process.memoryUsage()` 返回进程的内存使用情况

`process.version` 通常用来对node版本进行检查, 有一些属性在低版本node下是不支持的, 可以通过这个api来进行判断

### 画重点 经常使用的

`process.argv` 返回一个数组, 包含了启动进程时的命令行参数, 第一个参数是node的执行路径(也可以通过`process.execPath`获取), 第二个参数是当前执行文件的执行路径 之后的参数是命令行参数

```
node index.js a b=b c d

console.log(process.argv)  // [nodejs路径， 文件路径， a, b=b, c, d]

```

`process.execArgv`  返回不包含在`process.argv`中的命令行选项

`process.env` 返回一个包含用户环境信息的对象, 可以对这个对象进行添加和删除, 注意添加后的属性会自动转成字符串

`process.env.PWD` 返回package.json所在的项目根目录


```
process.env.Lb = 333 //添加

delete process.env.Lb  // 删除

```

`process.pid` 进程的pid, 在发送信号时需要使用`process.kill(pid, [signal])`

`process.ppid` 当前父进程的进程id




## 可以做什么

**对当前进程进行监控**

### warning事件

任何时候nodejs发出进程告警, 都会触发warning事件，回调函数只有一个`Error`对象, `name`(告警名称), `message`(告警信息), `stack`(告警堆栈)

### beforeExit事件

对当前进程进行控制： 如果事件循环为空, 正常情况下会退出当前进程, 如果beforeExit中存在异步函数, 当前进程会继续运行, 在exit事件之前被触发

### exit事件

当前进程结束后触发, 主动触发:`process.exit(code)`， 被动触发:Nodejs事件循环中没有事件之后, 自动触发exit事件

exit的回调函数中只可以编写同步代码，异步代码不会运行, 回调函数的入参`code`(退出码)

### 信号事件

在进程接受到信号时, 触发信号事件。

`SIGINT` `ctrl+c`时触发



```

setTimeout(() => {
   console.log('查看process的监控触发情况')
  }, 3000)

process.on('beforeExit', () => {
  console.log('beforeExit在exit之前触发')
  })

process.on('exit', () => {
  console.log('exit 触发有两种情况, 1 process.exit()直接触发 2 事件循环里没有事件之后触发')
  })  

```

**对当前进程进行控制**

**杀死进程**
1. `process.abort()`使node进程立即结束
2. `process.kill(pid, [signal])` 将signal信号发送给pid标示的进程
3. `process.exit([code])` 以code结束码命令nodejs同步终止进程, 注意在nodejs所有的`exit`事件监听器处理后，才会终止进程。


**进程报警**

`process.emitWarning(warning, [options])` 可用于发出定制的或应用特定的进程警告

*warning* 发出的警告

*options:Object* `{code(警告的唯一标示): String, detail(error附加的信息): String}`





## IPC相关

`IPC` 进程间通信 `Inter-Process Communication`指至少两个进程或线程间发送数据或者信号的技术或者方法

### message事件

进程由IPC通道创建, 当子进程收到父进程发送的消息时, 会触发message事件

### disconnect事件

进程是由IPC通道建立的, 通道关闭时会触发disconnect事件

**process.send(message, cb)** 给父进程传递信息

**process.connected** 如果IPC channel保持连接, `process.connected`返回true. `process.disconnect()`被调用后, `process.connected`返回false. 若为false, 则不能通过`process.send()`发送信息

**process.disconnect()** 关闭到父进程的IPC通道
