## Nginx

web服务器, 挂载web, 接口转发

`http`

+ `server`
  + `location` 
    + `/`  根具最长前缀来匹配location块
    + `~ = ` 带正则
      + `=` 完全匹配
      + `^~` 预先添加最长匹配前缀字符串
    + `proxy_pass` 将请求传递给使用配置的URL访问代理服务器
    +  `return 404` 返回状态码
    + `sub_filter` 定义要应用的重写
      + `sub_filter /blog/ /blog-staging/;`
    + `sub_filter_once` 
    + `error_page`  定义错误页面
    + `try_files` 检查指定的文件或目录是否存在并进行内部重定向，如果没有指定的文件或目录，则返回特定的状态代码
  + `listen`  监听端口号

`events`

`mail`

`stream`

### 控制nginx

`nginx -s signal`

+ `reload`  重启
+ `quit` 快速的关闭
+ `reopen` 重新打开日志
+ `stop`  立即关闭