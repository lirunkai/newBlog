## chalk

给你的命令行添加颜色

`const chalk = require('chalk')`

### 背景色

`console.log(chalk.bgRed('asdas'))`

`bgBlack bgRed bgGreen bgYellow bgBlue bgMagenta bgCyan`

`bgBlackBright bgRedBright bgGreenBright bgYellowBright`

### 字体颜色

`console.log(chalk.blue('asdasda'))`

`black red green yellow blue white gray cyan magenta`

`redBright greenBright yellowBright magenBright cyanBright whiteBright`

### 字体格式

`bold italic underline `

可嵌套以及链式调用

`console.log(chalk.blue.bgRed.underline('hellow', 'world'))`

### 自定义颜色

`chalk.rgb(255, 136, 0)`

`chalk.hex('#FF8800')`

`chalk.bgRgb(255,136,0)`

`chalk.bgHex('FF88000')`