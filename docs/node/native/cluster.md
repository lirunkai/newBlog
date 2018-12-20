# cluster

集群, 使用一连串的进程去完成任务

由于工作进程是由`child_process.fork()`创建的, 所以可以与父进程进行通信, 也就拥有了child_process的事件和方法.

# Worker类

## 拥有的事件

`disconnect` 工作进程的IPC管道被断开后触发本事件

`exit` 任何一个工作进程关闭的时候触发 `handler(worker, code, signal)`

`error`

`message` cluster主进程接受到任意工作进程发送的消息后触发 `handler(worker, message, handle)`

`listening` 工作进程调用listen后触发 `handler(worker, address)`

`online` 工作进程运行的时候触发 `handler(worker)`

`fork` 新的工作进程被fork时触发 `handler(worker)`

## 属性

`worker.id` 工作进程的id

`worker.process` 由于工作进程是`child_process.fork()`创建的， 这个方法返回的对象保存在 `.process`这个对象上

## 创建Worker

`cluster.fork([env])`

衍生出一个新的工作进程, 但是只能在主进程使用.


### 主工作进程

`cluster.isMaster` 如果是主工作进程, 返回true

`cluster.workers` 获取Worker对象

`cluster.disconnect()` 通知子进程调用自身的disconnect方法

### 工作进程

`cluster.isWorker` 当进程不是主进程时, 返回true

`cluster.worker` 获取当前工作进程的worker对象

`cluster.disconnect()` 关闭server, 关闭IPC通道

`worker.isDead()` 工作进程退出, 返回true

`worker.isConnected()` 通过IPC连接到主进程, 返回true


### 杀掉工作进程

`worker.kill([signal])`  kill掉工作进程
