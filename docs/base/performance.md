## 性能优化

前端性能

1. 页面加载速度
2. 浏览时动态加载数据过多时的卡顿



怎么分析？

1. lighthouse 自动对网站做一个质量评估
2. Performance
3. Web pack 分析包`webpack-bundle-analyzer`
4. Source-map



怎么优化？

静态文件的终极优化策略：

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



网络层面

1. 增加缓存cache-control/last-modified/if-modified-since/etag/if-none-match

   1. Cache-control  和 max-age

      1. `no-cache` 不缓存
      2. `no-store` 禁止缓存
      3. `private` 仅UA缓存
      4. `public` 都可以缓存

   2.  `Etag` 和 `If-None-Match`

      `Etag` 表示资源的版本, 浏览器在发送请求时会带`If-None-Match`头字段, 来询问服务器该版本是否仍然可用。 可用则返回304状态码。

   3. `Last-Modified` 和 `If-Modified-Since` 检查修改时间

2. 减少cookie传输

3. 压缩文件`nginx 开启gzip`

4. 应用http2

   1. 首部压缩
   2. 多路复用
   3. 服务端推送
   4. 二进制分帧
   
5.  减少http请求

   1. 雪碧图
   2. 小图片使用base64
   3. 按需加载
   4. 懒加载图片



页面

1. 减少回流与重绘
2. 骨架屏
3. 只对可视区域进行渲染
4. 预加载preload/prefetch
   1. `<link rel="preload" as="script" href="">`
   2. `<link rel="dns-prefetch" href="//wq.test.com"/>` 提前解析dns
5. 懒加载



webpack

1. DllPlugin拆分基本不升级的包
2.  `babel-loader`
   1. `cache-directory: true`
   2. `exclude: /node_modules/`