# 编写个自己的cli

我们经常在命令行里面看到一些自定义的命令, 比如`vue create name` 或者 `npm init`， 这里的 `vue` `npm`就是自定义的命令。

## 最简单的可执行脚本

`#!/usr/bin/env node` 声明使用node来运行这个脚本

```
#!/usr/bin/env node
console.log('hello big boy')
```

在`package.json`里面添加`bin`字段

```
bin:{
  "big": "bin/big"
}
```

## 获取命令行参数

一般我们通过`process.argv`来获取参数, `process.argv`返回一个数组,  第一个参数是node的可执行的绝对路径,  第二个参数是执行脚本的绝对路径, 之后的参数就是我们输入的参数了.

```
#!/usr/bin/env node

console.log('argv', process.argv) // [node路径, 执行脚本路径, 参数, 参数]
```

## 处理命令行参数 commander模块

```
#!/usr/bin/env node

// 使用commander
const program = require('commander')
const shelljs = require('shelljs')
const chalk = require('chalk')

program
.version('v1.0.0')
.description('谁最帅')
.option('-p --pig <pig>', 'your name')
.parse(process.argv)

program
.command("sync <name>")
.description("同步下姓名")
.action((big) => {
  console.log(chalk.red(big))
})

console.log(program.pig)
console.log(chalk.blue(program.args))



program.parse(process.argv)


```



[源码](https://github.com/lirunkai/demo)
