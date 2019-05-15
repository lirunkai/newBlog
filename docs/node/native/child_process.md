# 子进程

之前说了进程`process`， 现在说说和它相关的子进程`child_process`, 平时代码或者工具开发中, 在主进程启动后, 还有一些任务需要单独执行, 这时我们就需要使用`child_process`

**子进程的使用大概分为**:

1. 执行某个命令
2. 执行某个文件

**子进程的类型**
1. 异步进程
2. 同步进程


## 异步进程

异步子进程不会阻塞nodejs的事件循环. 异步的子进程返回一个`childProcess`类的实例

**创建**

`child_process.exec(command, options, cb(error, stdout, stderr))`

衍生一个shell并在shell中执行`command` 也就是执行某个命令,  `command`命令的参数, 以空格分割

通常使用`options`中的,  `options`用于自定义如何衍生进程
1. `cwd`子进程运行的工作目录
2. `env`环境变量键值对
3. `killSignal`父进程发送由 killSignal 属性标识的信号

`child_process.execFile(file, args, options, cb(error, stdout, stderr))`

衍生一个新的进程执行file

`file`可执行的文件或路径

`args`字符串参数列表

`child_process.fork(modulePath, args, options)`

与`exec`和`execFile`不同的是, `fork`会创建一个IPC通道。

`child_process.spawn(command, args, options)`

使用`command`和`args`创建一个新进程




## 同步进程

同步子进程会阻塞nodejs的事件循环, 持续到子进程结束

`child_process.execSync(command, options)`

`child_process.execFileSync(file,args, options)`

`child_process.spawnSync(comman, options)`

这里主要说一下`spwanSync`这个方法返回了一个对象。

```

{
  pid : 子进程的pid
  output: 输出
  stdout:
  stderr:
  status:
  signal:
  error
}

```


## childProcess

这里主要讲一些childProcess这个类, 因为每个异步进程返回的都是这个类的实例， 这个类代表衍生的子进程, 通过这个类我们可以监控子进程的运行

### message事件

子进程调用`process.send()`发送消息后, 会触发message。 一般在`childProcess.fork()`的文件中使用, 代表当前进程也就是子进程

**childProcess.send(message)**   只有拥有IPC通道的进程可以进行send方法交互

---

### error事件  

1. 向子进程发送信息失败
2. 无法创建子进程
3. 子进程无法被杀死

### close事件  

子进程的stdio流被关闭时触发， 监听函数`cb(code, signal)`执行 `code`退出码 `signal`退出信号

### exit事件

子进程关闭触发，和close的回调参数一样

**childProcess.kill(signal)** 向子进程发送一个信号。

**childProcess.killed** 表示子进程是否接受到信号

---

### disconnect事件

父进程或子进程显式的调用`disconnect()`后触发disconnect事件。

**childProcess.disconnect()** 关闭父子间的IPC通道

**childProcess.connected** 是否可以从一个子进程发送和接受数据

---

**childProcess.channel** 代表当前子进程的IPC通道的引用

**childProccess.pid** 子进程的进程号

---

##### stdin stderr stdout stdio

stdio = [stdin, stdout, stderr] 其中只有stdin是可写流(`stream.Writeable`), stdout和stderr是可读流(`stream.Readable`)

## 例子

说过了process和childProcess, 写一个例子来看看他们之间的交流

```
parent.js 文件

let {spawn} = require('child_process')

let grep = spwan('node', ['child.js'], {stdio: ['ipc', 'pipe', 'pipe']})

grep.send('bibibi')

grep.on('message', (message) => {
  console.log(message)
  grep.disconnect()
})

grep.on('disconnect', () => {
  console.log('parent disconnect')
})

```


```
child.js

let path = require('path')
let fs = require('fs')

process.on('message', (message) => {
  process.send(`子进程id${process.pid} 父进程id${process.ppid}`)
})

process.on('disconnect', () => {
  fs.writeFileSync(path.resolve(__dirname, 'a.js'), 'let a = 'a'')
  })

```
