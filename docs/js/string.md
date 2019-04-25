# String

基础知识, 列一下api, 然后记录下一些巧妙的用法, 以及一些容易出错的地方.

## 不会对字符串进行修改

`str.slice(start, end)`

提取字符串的一部分, 原字符串保持不变

`split(分割符, limit)`

将一个字符串用分割符分割成一个数组, limit用来限制数组的长度. **返回一个数组, 不会对字符串进行修改**

`str.padEnd(总长度, 填充字符串)`

将字符串填充到总长度,  **返回填充后的新字符串**

`str.padStart(总长度, 填充字符串)`

`str.repeat(num)`

返回重复了num次的字符串

`str.replace(regexp|substr， newSubStr|function)`

返回一个由替换值替换一些或所有匹配的模式后的新字符串

`str.substring(start, end)`

提取从start到end的字符串, 不包含end， `如果任一参数小于 0 或为 NaN，则被当作 0` `如果 indexStart 大于 indexEnd, start和end对换提取`

`str.substr(start, length)`

提取从`start`开始的指定数目的字符

`str.trim()`

`str.toLowerCase()` 将所有字母进行小写转换

|  lodash    _.lowerFirst(string) 将首字母进行小写，返回转换后的字符串

`str.toUpperCase()`    将所有字母进行大写转换

| lodash   _.upperFirst(string)  将首字母大写, 返回转换后的字符串

|  lodash  _.capitalize(string)  首字母大写, 其他字母小写, 返回转换后的字符串

### 无索引

`str.endsWith(searchString, position)`

查询子字符串是否在字符串的末尾, position可以设置字符串的长度 **返回true或者false**

`str.startsWidth(searchString, position)`

查询子字符串是否在字符串的开头, position可以设置字符串从什么地方开始 **返回true或者false**

`str.includes(searchString, position)`

查询字符串中是否包含子字符串, 从position开始 **返回true或者false**

`str.match(regexp)`

没regexp 返回空字符串数组

有g, 返回匹配的子字符串组成的数组, 没有匹配到, 返回null

没g 返回一个数组, 包含input（解析的原始字符串）




### 有索引

`str.indexOf(searchString, position)`

查询子字符串在字符串中**第一次出现**的位置, 如果存在返回所在位置, 不存在返回-1

`str.lastIndexOf(searchString, position)`

`str.search(regexp)`

返回首次匹配到的索引, 没匹配到返回-1

## 其他

`str.charCodeAt()` 返回unicode码

```
有意思的题
// "a" = 1 "b"=2
// alphabet_position("The sunset sets at twelve o' clock.")  => 20 8 5 19 21 14 19 5 20 19 5 20 19 1 20 20 23 5 12 22 5 15 3 12 15 3 11

function alphabet_position(text){
  return text.toUpperCase().match(/[a-z]/gi)
    .map(item => item.charCodeAt - 64)
    .join(' ')

}
```
