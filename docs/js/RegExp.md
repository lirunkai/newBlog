## 正则

#### 特殊字符

`\`      在非特殊字符之前的反斜杠表示下一个字符是特殊的

`^`       匹配输入的开始

`$ `         匹配输入的结束

`*`   匹配前一个表达式0次或多次 

`?`      匹配0次或1次

`+`     匹配1次或多次

`.`     匹配除换行符之外的任何单个字符

`(x)`   匹配且捕获

`(?:x)` 匹配不捕获

`x(?=y)`    正向肯定查找， 匹配x后紧跟着y

`x(?!y)`    正向否定查找,  匹配x后面不跟着y

`x|y`    匹配x或者y

`[xyz]` 一个字符集合，匹配方括号中的任意字符, 特殊符号在一个字符集里面没有任何意义.

`[^xyz]` 非这个集合内的

`\d`    匹配一个数字

`\D `    匹配一个非数字

`\w`     匹配字母、数字或者下划线

`\W`     匹配非字母、数字或者下划线

`\n`   `n`是一个正整数。一个反向引用（back reference），指向正则表达式中第 n 个括号（从左开始数）中匹配的子字符串   eg `\1 \2`

标志

`g`    全局搜索

`i`    不区分大小写

`m`    多行匹配

`y`

#### regexp.exec(str)

在一个指定字符串中执行一个搜索匹配, 找到匹配项返回一个结果数组,额外有两个属性input和index, 没找到或者null

当exec有全局标记(g)时， 每次调用exec()方法会返回一个匹配信息

没有全局标记(g)时, 无论调用多少次exec()，也只会返回第一个匹配信息

```javascript
const regex1 = RegExp('foo*', 'g');
const str1 = 'table football, foosball';
let array1;

while ((array1 = regex1.exec(str1)) !== null) {
  console.log(`Found ${array1[0]}. Next starts at ${regex1.lastIndex}.`);
}
```



#### regexp.test(str)

如果正则表达式与指定的字符串匹配 ，返回`true`；否则`false`。

#### str.match(regexp)

不包含g， 返回和exec一样, [sourceString, childString, index, input]

包含g, 返回匹配的所有子字符串组成的数组， 没有匹配到返回null

#### string.replace(regexp, function(args))

替换匹配到的字符串.  

函数的参数:

1. match     匹配的子串
2. p1,p2....pn     第n个括号匹配的字符串
3. offset   匹配到的子字符串的索引
4. string   原字符串 

### replace

```javascript
// foo => foo1
// foo2 => foo3
// foo0001 => foo0002
function incrementString(input) {
	if(isNaN(Number(input[input.length - 1]))) return input + '1';
    return input.replace(/(0*)([0-9]+$)/, function(match, $1, $2){
        var up = parseInt($2) + 1;
        return up.toString().length > $2.length ? $1.slice(0, -1) + up : $1 + up;
    })
}
```

---



## **捕获组**

#### 捕获组

RegExp最多可以存储9个捕获组的匹配项，通过`$1-$9`访问

```javascript
let text = 'this has been a short summer'
let pattern = /(..)or(.)/g
if(pattern.test(text)) {
  console.log(RegExp.$1)
  console.log(RegExp.$2)
}
```



#### 命名捕获组

在`()`里面使用`?<name>`标识

```javascript
const reDate = /(?<year>[0-9]{4})-(?<month>[0-9]{2})/
let match = reDate.exec('2018-09')
console.log(match.groups.year)
console.log(match.groups.month)
```

所有的命中组的匹配结果, 可以在结果对象的`groups`属性中获得

*在replace*中的使用

```javascript
const
  reDate = /(?<year>[0-9]{4})-(?<month>[0-9]{2})/,
  d      = '2018-04-30',
  usDate = d.replace(reDate, '$<month>-$<year>');
```

