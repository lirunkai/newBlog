# performance

性能的优化

## CRP

CRP `Critical Rendering Path` 关键路径渲染

 1. `script`添加`async`不让js程序阻止解析器的运行

 2. `css` 应该更早的被处理 放在head里面

 3. 避免在css中使用@import来引入css规则

 减少`reflow` 和 `repaint`

  1. 使用`DocumentFragment`来一次性创建DOM

> DocumentFragment接口表示没有父级的最小文档对象。它被用作轻量级版本Document以像标准文档一样存储由节点组成的文档结构的片段。关键区别在于，由于文档片段不是实际DOM结构的一部分，它是一个虚拟的dom节点，存在于内存中，所以对片段所做的更改不会影响文档，导致回流，或者在进行更改时可能会发生任何性能影响

  2. 使用`visibility`来替代`display`

  3. 不使用`table`

  4. resize时进行节流和防抖

 引起`reflow`

  1. 删除, 增加, 修改DOM节点

  2. 移动DOM的位置

  3. 修改css样式，改变元素的大小, 位置会引起重排  使用`display:none`

  4. 修改网页默认字体

  5. resize窗口大小

  6. 激活伪类

引起 `repaint`  

  1. 修改css颜色

  2. 使用`visibility:hidden`

`opacity` 和 `transform` 不会触发reflow repaint

## Preload

`<link rel="preload" as="script" href="aaa.js">`  预加载js文件

`<link rel="preload" as="style" href="aaa.css">`  预加载css文件

`<link rel="">`

## 服务端渲染


## 网络

### 减少http请求

1. 合并图片, css,js。 
2. 小图片使用Base64
3. 缓存
4. 图片延迟加载
5. 响应式图片
6. 降低图片质量
7. css特效代替图片
10. 通过webpack按需加载文件, 提取第三方库文件

### 使用CDN

cnd是一组分散在不同地理位置的web服务器，用来给用户更高效地发送内容。

### 静态资源不携带cookie， 使用不同的域名

### 使用http2

### 使用缓存, 不重复加载相同资源

## 大小

### 使用Gzip



静态文件的终极优化策略：

1. 缓存 => 配置超长时间的缓存,节省带宽, 提高性能
2.  采用内容摘要作为缓存更新依据 => 精确控制缓存更新策略
3.  静态资源CDN部署 => 优化网络请求
4.  资源发布实现非覆盖发布 => 平滑升级

