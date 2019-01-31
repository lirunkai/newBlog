# npm

介绍下这款明星工具, npm

目前最活跃的javascript软件包管理系统, 可以快速安装第三方包.

### 使用别人写好的npm包

#### 安装npm包

`npm install xxx -g ` 全局安装

`npm install xxx -save` 本地安装

`npm install xxx -S`   本地项目依赖的包

`npm install xxx -D`  本地工具包 不需要打包到项目文件里

#### 更新npm包

`npm update xxx`

#### 卸载npm包

`npm uninstall xxx`

### 自己编写npm包

创建一个npm包, 首先需要创建一个package.json文件, 这个文件需要严格的JSON格式

`npm init` 可以动态创建一个package.json的文件

如果不想一直回车可以添加`-y` 使用默认配置

`npm init -y`



### 发布你的npm包

1. 首先你需要在[npm](https://www.npmjs.com.cn/)的官网去注册一个npm账号.

2. 在终端登陆 `npm login`

3. `npm publish`去发布你完成的包

一般这样就结束了.

如果要发私有包：也就是npm包的name是`@yourname/npmname`就需要添加一些可选参数了.

`npm publish` 可选参数 `--access=public` 每个人都可以使用这个模块

说一些好玩的scripts里面的配置， 这里的npm内置配置都会自动调用

`prepare` 在npm包发布之前会自动调用

`publish` 在npm包发布之后自动调用

`preinstall` 在npm包install之前调用

`install` 在npm包install之后调用

```
{
	"scripts": {
        "prepare": "npm version patch", //在npm包发布之前会自动调用更新npm包版本
	}
}
```

### 更新你的npm包

当你更新你的npm包文件之后, 需要使用npm的一些命令来更新你的npm包版本号

`npm version patch` 将会基于你当前的版本号加1  `eg v1.0.1 -> v1.0.2` 小版本

`npm version major` 更新一个大的版本 `eg v1.0.0 => v2.0.0`

`npm version minor` 升级小版本号 `eg v1.0.0 => v1.1.0`



### 测试自己的包

在完成的包中使用`npm install . -g`来安装自己的包到全局

或者使用`npm link` 来测试自己的包, npm link的使用有两步，

1. cd进入到包所在的目录， npm link
2. 在使用npm包的项目中, npm link 包名字

### npm配置





### package.json的小世界

```
{
    "name": "包名字",
    "version": "v1.0.0",
    "description": "描述",
    "main": "index.js", // 程序的入口
    "scripts": {    // 可以定义一系列脚本
        "build": "webpack" // 可以通过 npm run build 来使用
    },
    "keywords": ["console"], //关键字
    "author": "作者名字",
    "license": "ISC",
    "homepage": "主页,可以在这里介绍你的包",
    "dependencies": {},  // 你的包依赖的其他包  使用-S安装到这里 -S是--save的简写
    "devDependencies": {}, //工具包, 用来打包,测试你的包, 使用-D安装到这里 -D是--save-dev简写
}
```
