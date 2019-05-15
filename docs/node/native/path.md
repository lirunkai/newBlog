# path

## 拼接路径, 生成路径

`path.resolve([...paths])` path从右到左处理, 如果构建出绝对路径就返回

`path.relative(from, to)` 返回从from到to的相对路径

`path.join([...paths])` 组合paths返回生成后的相对路径, 会处理`..`

`path.normalize(path)`  规范化 path，并处理 '..' 和 '.' 片段

### **根据路径获取信息**

`path.dirname(path)` 返回上一级的目录路径。 如果没有上一级目录, 返回'.'

`path.basename(path, 扩展名)` 返回`path`的最后一部分, 如果写了扩展名, 返回的时候去除扩展名

`path.extname(path)` 返回path的扩展名, 没有'.'，或者第一个字符是'.'返回空字符串

### **判断**

`path.isAbsolute()` 判断是否是绝对路径