前端数据存储

cookie, localStorage, sessionStorage

## cookie

cookie

cookie 的出现主要解决客户端与服务端会话状态的问题。

大小： 4kb

随 http 发送: 是

cookie 的设置

服务端设置

1. 客户端发送 http 请求到服务端
2. 服务端收到 http 请求，在响应头上添加 set-cookie 字段
3. 浏览器收到响应后保存 set-cookie 字段
4. 之后每次请求会自动携带 cookie

客户端设置

document.cookie

cookie 属性

name： 名称

value： 值

Domain： 指定了 Cookie 可以送达的主机名

Path

Expires： 过期时间

Size

HttpOnly 设置 HTTPOnly 属性可以防止客户端脚本通过 document.cookie 等方式访问 Cookie

Secure 只应通过被 HTTPS 协议加密过的请求发送给服务端

SameSite 可以让 Cookie 在跨站请求时不会被发送，从而可以阻止跨站请求伪造攻击（CSRF）

- Strict
- Lax
- None 维持之前的

Priority

## localStorage

浏览器内存中存储， 需手动清除

大小: 5m

随 http 发送： 否

API

设置 `localStorage.setItem(key, value)` value 存储的是字符串, 对象需要 JSON.stringify 一下

获取 `localStorage.getItem(key)`

移除 `localStorage.removeItem(key)`

清空 `localStorage.clear()`

事件 `window.onstorage`

事件在同一个域下的不同页面之间触发，即在 A 页面注册了 storge 的监听处理，只有在跟 A 同域名下的 B 页面操作 storage 对象，A 页面才会被触发 storage 事件

## sessionStorage

标签页内存储

标签页关闭， sessionStorage 销毁

大小: 5m

随 http 发送： 否

API 与 localStorage 一致
