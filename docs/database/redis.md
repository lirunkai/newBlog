Redis

NoSql数据库顶柱之一

### 优势

+ 性能极高， 读取性能110000次/s  写性能 81000次/s
+  数据类型丰富 String List Hashes Set
+  原子性， 只有成功或者失败
+  丰富  支持publish/subscribe
+  可以持久化到磁盘

安装

`brew  install redis@4.0`



启动

`brew services start redis@4.0`



连接

`redis-cli  -h 127.0.0.1 -p 6379`



关闭

`redis-cli shutdown`



杀死进程

`sudo kill redis-server`



默认有15个表 也就是说 0-15, 默认为0

通过`select index` 来切换数据库



设置key

`set key value [EX seconds] [PX milliseconds] NX | XX`

+ EX设置过期时间
+ PX 设置过期时间
+ NX 不存在才能设置成功
+ XX 



获取key

`get key`



查看已设置的key

`keys *`



getset key value

获取旧的key, 设置新的key



append key value

将值value插入到字符串键key已存储内容的末尾



strlen value

返回key的value的长度



setrange key index value

从index开始替换key当前的value



获取范围

getrange startindex endindex



增加数字的值

`INCREBY key int` 来增加整数值

`INCRBYFLOAT key float`  增加浮点数



减少数字的值

`DECRBY` 减少值



增加1 

`INCR key`

减少1

`DECR key`

---

node中redis的使用

### ioredis

安装 `yarn add ioredis`

使用

```javascript
const Redis = require('ioredis')
const redis = new Redis({
	port: 6379,
  host: '127.0.0.1',
  family: 4,
  db: 0
})

// string类型设置
redis.set('foo', 'bar')

async function getFoo() {
  const value = await redis.get('foo')
  console.log(value)
  return value
}

getFoo()

// Binary Data
redis.set("foo:binary", Buffer.from("bar"))

async function getFoo() {
  const value = await redis.getBuffer('foo:binary')
  console.log(value)
  return value
}

// set 设置过期时间
redis.set("key", 100, "EX", 10);
```









