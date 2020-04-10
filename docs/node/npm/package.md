收录下npm中使用过的包

CLI（command line interface）开发命令行会使用的包

`commander`

`chalk`

`inquier`



`ora`

```javascript
const ora = require('ora')
const spinner = ora('正在下载')
spinner.start() //开始展示loding
spinner.stop() // 结束loding
```



`dotenv`  获取env文件的配置

```javascript
let dotenv = require('dotenv')
let path = require('path')
let config = dotenv.config({
  path: path.resolve(__dirname, '.env'),
  encoding: 'utf8'
})

console.log(config.parsed); // return a object
```



`cross-env`  兼容mac和windows package.json中关于scripts的NODE_ENV设置

```javascript
{
  "scripts": {
    "build": "cross-env NODE_ENV=production webpack --config build/webpack.config.js"
  }
}
```





创建唯一ID 

`nanoid`  

```
import { nanoid } from 'nanoid';
model.id = nanoid()
```



计算库

`number-precision`

在js计算的过程中会出现浮点数计算不符合我们预期的情况.



操作时间

`dayjs`

`moment`



爬虫

`puppeteer`







操作数据库

`sequelize`

`mongoose`

`ioredis`