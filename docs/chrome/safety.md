# 安全

Web安全的三个目标: 机密性， 完整性, 可用性。

机密性:  在未验证状态下信息不能被用户获取。

完整性： 完整性表示，	经过验证的用户访问数据时，数据没有发生过任何改动，是原生的数据。

可用性: 可用性指被验证过的用户可以轻易获得信息

## 攻击

### XSS

Cross-Site Scripting 跨站脚本攻击,  是一种代码注入攻击. 通过注入一段可执行脚本。通过脚本去获取用户的信息, cookie



### CSRF





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

`<script href="" integrity="sha256"></script>`

