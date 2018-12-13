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

*参数解析*

`.option()`方法用来定义带选项的 commander. 下面的例子会解析来自 process.argv 指定的参数和选项，没有匹配任何选项的参数将会放到 program.args 数组中

```
#!/usr/bin/env node
var program = require('commander');

program
  .version('0.0.1')
  .option('-p, --peppers', 'Add peppers')
  .option('-P, --pineapple', 'Add pineapple')
  .option('-b, --bbq-sauce', 'Add bbq sauce')
  .option('-c, --cheese [type]', 'Add the specified type of cheese [marble]', 'marble')
  .parse(process.argv);

console.log('you ordered a pizza with:');
if (program.peppers) console.log('  - peppers');
if (program.pineapple) console.log('  - pineapple');
if (program.bbqSauce) console.log('  - bbq');
console.log('  - %s cheese', program.cheese);

```

*添加命令*

`command(name [name])`  添加一个command命令, 并且在之后添加action方法来处理command命令的回调
`[]`里的name是选填的, 如果写了会传入action内的回调


*命令的行为*

`action(cb(command的可传入参数))`  command命令触发后,执行action进行逻辑代码编写。

*解析参数*

`parse(process.argv)` 解析输入的参数, 如果不进行解析， action中不会传入参数。


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
.action((name) => {
  console.log(chalk.red(name))
})

console.log(program.pig)
console.log(chalk.blue(program.args))



program.parse(process.argv)


```


[源码](https://github.com/lirunkai/demo)
