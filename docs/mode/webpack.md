# webpack

webpack是一个现代js的静态文件打包工具，当webpack处理程序时, 会在内部构建一个**依赖图**,依赖图会映射项目依赖的每个模块.

通过entry配置入口, output配置出口文件, loader来解析特定文件, plugin可以在任意阶段影响webpack的编译.

可以零配置,但是一般不推荐, 还是我们按项目自定义变量比较好.

## entry 入口

单个入口 字符串

多个入口 对象

## output 输出

**path**

**filename**

## module

**rules**

use

option

loader

loader是用来加载处理各种形式的资源,本质上是一个函数, 接受文件作为参数,返回转化后的结构。

##  mode

模式， 指明现在是`development`开发模式还是`production`生产模式。

`development`特性

1. 浏览器调试工具

2. 快速和优化的增量构建机制

3. 错误日志和提示

`production`特性

1. 开发所有的优化

2. 更小的bundle大小

3. 去除掉只在开发阶段运行的代码

## plugins

在webpack的每个运行期间都可以进行操作. 通常用来做loader做不到的事情

## optimization

## 更多优化

`happypack`插件, 多核运行webpack

### 打包后：

查看不使用的包:

`webpack-bundle-analyzer` 分析

[删除不使用的包](https://mp.weixin.qq.com/s?__biz=MzU0Nzk1MTg5OA==&mid=2247484701&idx=1&sn=14f88b419ead65742f93ab46ea99e566&chksm=fb47c168cc30487e15359c1d4ab49797009676fabd1886cb1d0b1f16418b52a76668c181f534&scene=21#wechat_redirect)
