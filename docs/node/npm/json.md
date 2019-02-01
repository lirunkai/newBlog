关于json的包

### parse-json

读取json, 拥有更好的报错信息

`const parseJson = require('parse-json')`

`parseJson({"a": 123})` 返回JSON.parse后的JSON

### read-pkg

读取某个文件夹下的package.json的内容

`readPkg({cwd: path})`    返回一个Promise, 参数是JSON

`readPkg.sync({cwd: path})`     返回JSON