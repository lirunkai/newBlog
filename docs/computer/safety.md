# 安全

Web安全的三个目标: 机密性， 完整性, 可用性。

机密性:  在未验证状态下信息不能被用户获取。

完整性： 完整性表示，经过验证的用户访问数据时，数据没有发生过任何改动，是原生的数据。

可用性: 可用性指被验证过的用户可以轻易获得信息

## 攻击

### XSS

Cross-Site Scripting 跨站脚本攻击,  是一种代码注入攻击. 

1. 非持久型XSS（反射型XSS）

   一般是通过别人发送带有恶意脚本代码参数的URL， 当URL地址被打开时，恶意代码参数被HTML解析，执行

   比如`https://xxx.com/xxx?default=<script>alert(document.cookie)</script>`

   **预防:**

   + web页面渲染的所有内容或者渲染的数据都是来自于服务端
   + 尽量不要从`URL`, `document.forms`等DOM API中获取数据直接渲染
   + 尽量不使用可执行字符串的方法，比如`eval`
   + 如果一定要使用，必须对DOM渲染的方法传入的字符串参数做转义

2. 持久性XSS(存储型XSS)

   一般存在于Form表单提交等交互功能，如文章留言，提交文本信息。通过将内容经正常功能提交进入数据库持久保存，当前端页面获得后端从数据库中读出的注入代码时，恰巧将其渲染执行

   **预防：**

   + CSP, `Content-Security-Policy` 建立白名单, 明确告诉浏览器哪些外部资源可以加载和执行。
   + 转义字符。 用户的输入永远不可信，对输入输出进行转义
   + HttpOnly `Set-Cookie`时，将其属性设为`HttpOnly`， 可避免该网页的cookie被客户端恶意javascript窃取,

### CSRF

`Cross Site Request Forgery`跨站请求伪造. 利用用户已经登陆的身份，在用户不知情的情况下， 以用户的名义完成非法操作。

- 用户已经登录了站点 A，并在本地记录了 cookie
- 在用户没有登出站点 A 的情况下（也就是 cookie 生效的情况下），访问了恶意攻击者提供的引诱危险站点 B (B 站点要求访问站点A)。
- 站点 A 没有做任何 CSRF 防御

防御:

+ `Get`请求不对数据进行修改
+ 不让第三方网站请求到用户Cookie
+ 请求时附带验证信息，比如验证码或者Token

### URL跳转漏洞

借助未验证的URL跳转，将应用程序引导到不安全的第三方区域，从而导致的安全问题

预防：

+ 有效性验证Token， 保证生成的链接都是有一定的时效性token，避免生成的链接被利用
+ referer限制

### 点击劫持

点击劫持是一种视觉欺骗的攻击手段。攻击者将需要攻击的网站通过 iframe 嵌套的方式嵌入自己的网页中，并将 iframe 设置为透明，在页面中透出一个按钮诱导用户点击

防御：

`X-FRAME-OPTIONS`是一个 HTTP 响应头，在现代浏览器有一个很好的支持。这个 HTTP 响应头 就是为了防御用 iframe 嵌套的点击劫持攻击

该响应头有三个值可选，分别是

- DENY，表示页面不允许通过 iframe 的方式展示
- SAMEORIGIN，表示页面可以在相同域名下通过 iframe 的方式展示
- ALLOW-FROM，表示页面可以在指定来源的 iframe 中展示

### SQL注入

SQL注入是一种常见的Web安全漏洞，攻击者利用这个漏洞，可以访问或修改数据，或者利用潜在的数据库漏洞进行攻击

防御：

+ **严格限制Web应用的数据库的操作权限**
+ **所有的查询语句建议使用数据库提供的参数化查询接口**

## 防御:

**CSP**

`Content Security Policy` 内容安全策略检查

原理： CSP通过指定有效域——即浏览器认可的可执行脚本的有效来源——使服务器管理者有能力减少或消除XSS攻击所依赖的载体, 一个CSP兼容的浏览器将会仅执行从白名单域获取到的脚本文件，忽略所有的其他脚本

主要目标是减少和报告 XSS 攻击 , XSS 攻击利用了浏览器对于从服务器所获取的内容的信任

比如 只允许加载自己域的图片

`<meta http-equiv="Content-Security-Policy" content="img-src 'self';">`

或者服务器返回时添加响应头 `Content-Security-Policy: default-src 'self' aidoudou.com.cn; img-src *`



**SRI**

`Subresource Integrity `

允许浏览器检查其获得的资源是否被篡改

原理： 通过验证获取文件的哈希值是否与提供的哈希值一样来判断资源是否被篡改

使用：`<script href="" integrity="sha256"></script>`

使用 base64 编码过后的文件哈希值写入你所引用的 [``](https://developer.mozilla.org/zh-CN/docs/Web/HTML/Element/script) 或 [``](https://developer.mozilla.org/zh-CN/docs/Web/HTML/Element/link) 标签的 **integrity**属性值中即可启用子资源完整性功能。

integrity 值分成两个部分，第一部分指定哈希值的生成算法（目前支持 sha256、sha384 及 sha512），第二部分是经过 base64 编码的实际哈希值，两者之间通过一个短横（-）分割。

