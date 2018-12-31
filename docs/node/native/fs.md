# fs

说一些对fs的理解, fs操作文件的一个api。 比如获取文件的信息, 对文件进行操作, 新增, 添加， 修改。

## 监听文件的变动

### FSWatcher

这个类是EventEmitter的实力， 拥有`change`  `close` `error`三个事件, `fs.watch()`会创建这个类的实例

**change**  

`eventType`  事件的类型

`filename` 修改的文件名


`fs.watch(path, option{recursive监视子目录, encoding, }, cb(eventType, filename))`

开始监听一个文件夹

`watcher.close()`

停止监听

```
let watcher = fs.watch(__dirname, (eventType, filename) => {

})

setTimeout(() => {
  watcher.close()
}, 3000)


```

## fs.Stats类

这个类里面主要是获取文件的信息，比如创建的时间, 大小.

```
Stats {
  dev: 2114,       文件所在的设备的标识。
  ino: 48064969,    文件的索引节点
  mode: 33188,      文件类型与模式的位域
  nlink: 1,          文件的硬链接数
  uid: 85,          文件所有者的用户标识
  gid: 100,         文件所在组的群组标识。
  rdev: 0,          特殊文件的设备标识。
  size: 527,          文件的字节大小。
  blksize: 4096,      用于 I/O 操作的内存块的大小
  blocks: 8,            分配给文件的内存块的数量
  atimeMs: 1318289051000.1, 最后一次访问文件的时间
  mtimeMs: 1318289051000.1, 最后一次修改文件的时间
  ctimeMs: 1318289051000.1, 最后一次改变文件状态的时间
  birthtimeMs: 1318289051000.1, 创建文件的时间
  atime: Mon, 10 Oct 2011 23:24:11 GMT,  最后一次访问文件的时间
  mtime: Mon, 10 Oct 2011 23:24:11 GMT,   最后一次修改文件的时间
  ctime: Mon, 10 Oct 2011 23:24:11 GMT, 最后一次改变文件状态的时间
  birthtime: Mon, 10 Oct 2011 23:24:11 GMT  创建文件的时间
}
```


## fs.ReadStream类

fs.ReadStream是可读流   `fs.createReadStream(path, options{flags, encoding, fd, mode, autoclose, start, end, highWaterMark})`会创建fs.ReadStream

拥有 `close`  `open` `ready` 事件

`readstream.bytesRead` 已读字节数

`readstream.path` 正在读取文件的path

## fs.WriteStream类

可写流 `fs.createWriteStream(path, options{flags, encoding, mode, autoclose, start, end, highWaterMark, fd})`

拥有 `close` `open` `ready` 事件

`writeStream.bytesWritten` 已写入的字节数

`writeStream.path` 正在写入文件的path

## 复制

`fs.copyFile(src, dest, [flags], cb(err))`

异步将src复制到dest。

flags   `fs.constants.COPYFILE_EXCL` 如果 dest 已存在，则拷贝失败
        `fs.constants.COPYFILE_FICLONE` 拷贝时会创建写时拷贝
        `fs.constants.COPYFILE_FICLONE_FORCE` 拷贝时会创建写时拷贝链接

## 读

`fs.read(fd, buffer, offset, length, position, cb(err, bytesRead, buffer))`

异步读取文件

`fs.readdir(path, [options], cb(err, files文件名))`

读取目录的内容

`fs.readFile(path, options{encoding, flag}, cb(err, data))`

异步读取文件的内容

## 写

`fs.mkdir(path, [options{recursive 是否创建父目录}], cb(err))`

异步的创建目录

`fs.write(fd, string, position, encoding, cb(err, written, string))`

异步写入数据

`fs.writeFile(file, data, [options{encoding, mode, flag}], cb(err))`

异步将数据写入文件，如果文件存在, 覆盖文件

`fs.appendFile(path, data, [option{encoding, mode, flag}], cb(err))`

异步追加数据到文件，如果文件不存在, 创建文件

## 删

`fs.rmdir(path, cb(err))`

移除目录

`fs.unlink(path, cb(err))`

移除文件

## 打开

`fs.open(path, flags, mode, cb(err))`

异步打开文件

## 权限

`fs.access(path, mode, callback(err))`

检查 path 指定的文件或目录的用户权限

mode `F_OK`文件可见  `R_OK`文件可读  `W_OK`文件可写  `X_OK` 文件可执行， mode每次可使用多个

```
fs.access(path, fs.constants.R_OK | fs.constants.W_OK, (err) => {

})
```

`fs.chmod(path, mode, cb(err))`

异步的修改文件的权限

mode `S_IRUSR` 所有者可读 `S_IWUSR` 所有者可写 `S_IXUSR` 所有者可执行

     `S_IRGRP` 群组可读   `S_IWGRP` 群组可写   `S_IXGRP` 群组可执行

     `S_IROTH` 其他人可读  `S_IWOTH` 其他人可写 `S_IXOTH` 其他人可执行

这个记着比较麻烦， 可以记一个数字的顺序 765 7最左侧的数字代表文件所有者的权限， 中间的数字代表群组的权限, 最右侧的数字代表其他人的权限

从7到0, 权限        7 可读 可写 可执行
                   6 可读 可写
                   5 可读 可执行
                   4 只读
                   3 可写 可执行
                   2 只写
                   1 只可执行
                   0 没权限
## 判断

`fs.existsSync(path)`

判断文件是否存在


## 好用的npm包

### fs-extra

对原生`fs`进行再次封装, 支持promise, 支持async

安装 `npm i fs-extra -D`

**copy**   `fse.copy(src, dest, [option, callback])`

`option`

   1. `overwrite` *Boolean* 如果复制的目标位置已有同名文件, 则覆盖


**emptyDir**   `fse.emptyDir(dir, cb)`

确保某个dir是空的, 如果之前有这个dir, 则清空dir内部的文件，如果没有则创建

**ensureFile** `fse.ensureFile(file, cb)`

确保某个file是存在的. 如果不存在则创建, 存在不处理

**ensureDir** `fse.ensureDir(dir, cb)`

确保某个dir是存在的

**ensureLink** `fse.ensureLink(srcPath, dstPath, cb)`

确保链接是存在的

**ensureSymlink** `fse.ensureSynlink(srcPath,dstPath, [type, cb])`

**outputFile** `fse.outputFile(file, data, [option, cb])`

将data写入文件,如果文件不存在则创建.

**outputJSON** `fse.outputJSON(file, object, [option, cb])`

将object写入一个json文件

`options`

    1. `spaces` json文件的缩进

**readJSON** `fse.readJSON(file， cb(err,obj))`

读取一个json的文件

**pathExists**    `fse.pathExists(filepath, cb(exists))`

查看文件是否存在, cb中的exists表示是否存在

**remove** `fse.remove(path,cb)`

### chokidar
