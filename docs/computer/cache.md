# 浏览器缓存

浏览器第一次请求

![](https://aidoudou.top/_media/first_request.png)

浏览器之后请求

![](https://aidoudou.top/_media/second_request.png)

首先说说我们为什么要用缓存吧.

1. 提升用户体验

2. 减缓服务器压力

---------------------------------------------

## 强缓存

`Cache-Control` 和 `expires`属于强缓存, 如果强缓存没有过期, 不发送请求, 直接从本地获取缓存.

## 协商缓存

强缓存失效之后, 发送请求至服务器, 服务器根据`Request Headers`里的`Etag/If-None-Match, Last-Modified/if-Modified-Since`来判断是否返回文件, 或者协商返回304, 使用缓存文件.

当资源过期时（使用Cache-Control标识的max-age），发现资源具有Etage声明，则再次向web服务器请求时带上头If-None-Match （Etag的值）。web服务器收到请求后发现有头If-None-Match 则与被请求资源的相应校验串进行比对：
如果相同，则返回304
如果不同，则返回200和资源文件


缓存的控制主要通过`HTTP Response Header` 也就是我们常说的响应头

控制缓存的响应头:

  1. `Cache-Control`

    1. `public` 响应被缓存, 并且在多用户之间共享

    2. `private` 默认值, 响应只能当前用户使用, 不能多用户共享

    3. `no-cache` 不使用本地缓存。需要使用缓存协商，与服务器确认返回的响应是否被更改，如果之前的响应中存在ETag，那么请求的时候会与服务端验证，如果资源未被更改，则可以避免重新下载。

    4. `no-store` 缓存不应存储有关客户端请求或服务器响应的任何内容

    5. `max-age` 请求时间开始到过期的秒数

    6. `must-revalidate` 缓存在使用之前必须验证旧资源的状态, 过期资源不可使用

  `Cache-Control` 使用一个响应的时间， 根据第一次请求的时间和控制的相对时间来判断当前的缓存是否过期

  2.  `Expires` 描述的是一个绝对的时间, 通过`Response Headers`头返回.

    (当下次再次请求这个资源时，浏览器以请求的时间与这个Expires中的时间比对， 如果小于这个时间，说明未过期，直接从本地缓存中获取)

    尽量不要使用, 因为返回的是服务端的时间, 前端的时间不可控.

  3. `Last-Modified` 标识资源的最后修改时间 (服务端) **响应时返回**

  4. `If-Modified-Since` 标识资源的最后修改时间 （客户端）**请求时提交**

      根据`If-Modified-Since`携带的时间和服务端的文件修改时间进行比对, 如果时间小于服务端修改的时间, 则文件改动， 返回200和文件。 如果没有变化 返回304和空响应体

  5. `Etag` 资源的唯一标示  **响应时返回**

  6. `If-None-Match`  Etag的值, **请求时提交**

## 缓存位置

1. Service Worker
2. Memory Cache 内存
3. Disk Cache 磁盘