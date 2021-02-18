## 性能优化

影响页面渲染的因素

1. 网络延迟
2. 资源体积过大
3. 重复加载资源
4. 加载脚本时，渲染内容阻塞



怎么分析？

1. lighthouse 自动对网站做一个质量评估
2. Performance
   1. js中的`window.performance.timing`对象上有各个阶段的耗时
3. Web pack 分析包`webpack-bundle-analyzer`
4. Source-map



##### 静态文件的终极优化策略：

1. 缓存 => 配置超长时间的缓存,节省带宽, 提高性能
   1. `http响应头`
      1. `cache-control: max-age | no-cache | no-store | public | private`
      2. `expire`
      3. `etag`
      4. `last-modified`
   2. `http请求头`
      1. `If-None-Match`
      2. `If-Modified-Since`
2. 采用内容摘要作为缓存更新依据 => 精确控制缓存更新策略
   1. `webpack中file-loader`解析时配置`filename: [contentHash].[ext]`
   2. 输出到同一文件夹配置`output`
3. 静态资源CDN部署 => 优化网络请求
4. 资源发布实现非覆盖发布 => 平滑升级



#### 怎么优化？

##### 资源加载优化

+ 减少http请求

  + 缓存cache-control/last-modified/if-modified-since/etag/if-none-match

    + Cache-control  和 max-age

      + `no-cache` 不使用前置缓存，检查协商缓存
      + `no-store` 禁止缓存
      + `private` 仅UA缓存
      + `public` 都可以缓存

    + `Etag` 和 `If-None-Match`

      `Etag` 表示资源的版本, 浏览器在发送请求时会带`If-None-Match`头字段, 来询问服务器该版本是否仍然可用。 可用则返回304状态码。

    + `Last-Modified` 和 `If-Modified-Since` 检查修改时间

  + 懒加载

  + 按需加载

  + 合并请求

    + 雪碧图
    + 小图片使用base64 

+ 提高响应速度

  + cdn
  + DNS Prefetch
  + 应用http2
    + 首部压缩
    + 多路复用
    + 服务端推送
    + 二进制分帧

+ 减少资源大小

  + 代码压缩
  + 代码拆分
  + 图片压缩

+ 优化资源加载方式

  + ssr



##### 页面渲染优化

+ 优化html
  + js外链放在底部
  + css外链放在顶部
  + 减少dom层级
+ 优化js/css
  + 减少重绘，重排
  + 降低css选择器复杂性
  + 缓存dom查找
  + 通过class名方式修改元素样式
+ 优化动画
  + 使用requestAnimationFrame
  + 使用绝对定位或者固定定位

webpack

1. DllPlugin拆分基本不升级的包
2.  `babel-loader`
   1. `cache-directory: true`
   2. `exclude: /node_modules/`