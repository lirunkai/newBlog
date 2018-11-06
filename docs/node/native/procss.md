# process

`process` 提供当前Node进程的相关信息, 也就是Node启动之后, 可以通过`process`这个全局变量来获取一些信息. 当然`process`能做的还有控制当前的进程,比如杀死当前的进程等等, 来详细了解下

## 获取信息

`process.cwd()` 获取当前执行文件的目录, 通过`process.env.PWD`也可以访问

`process.version` 通常用来对node版本进行检查, 有一些属性在低版本node下是不支持的, 可以通过这个api来进行判断

### 画重点 经常使用的

`process.argv` 

`process.execArgv`


## 可以做什么
