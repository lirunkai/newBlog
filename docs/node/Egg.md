Egg 大蛋

## Controller

在this上挂载的

`ctx  app config  service logger`

在ctx上挂载的

`headers`

+ `ctx.get(headerName)`  获取某个header值
+ `ctx.set(key, value)` 设置一个响应头
+ `ctx.set(object)` 设置多个响应头
+ 

`query`  获取`?a=1`之后的参数

`queries`  获取多个相同key值时, 用数组存储起来

`params`  获取egg中定义路由时的参数

`cookies`

+ `ctx.cookies.get(name)`
+  `ctx.cookies.set(name, value)`

`session`

`request` 

+ `body`   请求中的传参
+ `files`  请求中的文件

`body`  返回体

`status`