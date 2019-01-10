# Cache

Cache 接口为缓存的 `Request/Response`对象提供存储机制.

一个域可以有多个命名Cache对象. 需要在脚本中处理缓存更新的方式.

除非明确的更新缓存, 否则缓存将不会被更新.

除非删除, 缓存不会过期

## methods

`Cache.match(request, options)` 返回Promise, resolve的结果是跟`Cache`对象匹配的第一个已经缓存的请求

`Cache.matchAll(request, options)` 返回一个Promise对象，resolve的结果是跟`Cache`对象匹配的所有请求组成的数组

`Cache.put(request, response)` 同时抓取一个请求及其响应，并将其添加到给定的cache。

`Cache.delete(request, options)` 搜索key值为request的`Cache`条目,找到删除, 返回一个resolve为true的Promise, 没找到返回一个resolve为false的Promise

`Cache.keys(request, options)`  返回一个Promise对象，resolve的结果是Cache对象key值组成的数组

# CacheStorage

表示Cache对象的存储， 维护一份字符串名称到相应`Cache`对象的映射。

通过`window.caches`可以访问 `CacheStorage`

## methods

`caches.open(cacheName)` 返回一个Promise, resolve为匹配的cacheName对象, 如果不存在就创建一个

`caches.match(request)` 检查给定的 Request 是否是 CacheStorage 对象跟踪的任何 Cache 对象的键，并返回一个resolve为该匹配的 Promise

`caches.has(cacheName)`  如果存在与`cacheName`匹配的`Cache`对象，则返回一个resolve为true的`Promise`.

`caches.delete(cacheName)`  查找匹配`cacheName`的`Cache`对象，如果找到，则删除`Cache`对象并返回一个resolve为true的`Promise`。如果没有找到`Cache`对象，则返回`false`.

`caches.keys()` 返回一个`Promise` ，它将使用一个包含与`CacheStorage`追踪的所有命名`Cache`对象对应字符串的数组来resolve. 使用该方法迭代所有`Cache`对象的列表

### 例子

```
const NOW_VERSION = 'lnb_v6'

// install done
this.addEventListener('install', function (event) {
  console.log('Service Worker install', NOW_VERSION);
});

// active 删除旧缓存
this.addEventListener('activate', function (event){
  console.log('Service Worker activate', NOW_VERSION)
  let cacheWhiteList = [NOW_VERSION];
  event.waitUntil(
    caches.keys().then(cacheNameList => {
      return Promise.all(cacheNameList.map(cacheName => {
        // 如果在缓存白名单里面没找到 删除
        if(cacheWhiteList.indexOf(cacheName) == -1){
          return caches.delete(cacheName)
        }
      }))
    })
  )
})


// fetch 任何被servic worker控制的资源被请求到时触发
this.addEventListener('fetch', function(event){
  console.log(event.request.url)
  function needFileFn(api){
    let needCacheList = ['css', 'js', 'pug', 'jpg', 'html', 'ico']
    return needCacheList.some(needCache => api.indexOf(needCache) !== -1)
  }
  event.respondWith(
    // 如果命中缓存, 使用缓存, 不然发起请求
    caches.open(NOW_VERSION)
    .then(cacheNowVersion => {
      return cacheNowVersion.match(event.request)
    })
    .then(resC => {
      return resC || fetch(event.request).then(res => {
        return caches.open(NOW_VERSION).then(cache => {
          let pointIndex = event.request.url.indexOf('.')
          let baseName = event.request.url.substring(pointIndex)
          if(pointIndex !== -1 && needFileFn(baseName)){
            cache.put(event.request, res.clone())
          }
          return res;
        })
      })
    })
  )
})


```
