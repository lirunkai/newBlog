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

---

#### 相关算法:

**1. 寻找字符串最长不重复的子串**

思路:  

1. 遍历所有子串, 找到最大的无重复子串
2. `/(.).*\1/`可以找到重复的子串
3. 从最大的子串开始查找, 如查找到不重复则返回。

实现

```javascript
let longChildLength = function(s){
  if(s == '') return 0;
  let slen = s.length;
  let l = slen;
  let reRepeat = /(.).*\1/; // （）== \1 
  while(l > 1){
    for(let i = 0; i<slen - l + 1; i++){
      let temp = s.substr(i, l);
      console.log(`l:${l} -- i:${i} -- temp:${temp} -- ${reRepeat.test(temp)}`)
      if(!reRepeat.test(temp)) return temp
    }
    l --;
  }
  if(l == 1) return 1;
}

longChildLength('baczbabccsz')
```

[jsbin实现输出](https://jsbin.com/xobejez/edit?js,console)

2 给一个只有`()[]{}`的字符串, 检测他们.

```javascript
Example 1:
Input: "()"
Output: true

Example 2:
Input: "()[]{}"
Output: true

Example 3:
Input: "(]"
Output: false

Example 4:
Input: "([)]"
Output: false

Example 5:
Input: "{[]}"
Output: true

```



思路：

使用栈遍历输入字符串, 如果是右括号, 查看栈顶是否是对应的左括号, 如果不是返回false, 如果是, 栈顶出栈继续循环。 

```javascript
function isValid(s){
  let valid = true;
  const stack = [];
  const mapObj = {
    '{': '}',
    '[': ']',
    '(': ')'
  }
  for(let i in s){
    const v = s[i];
    // 入栈
    if(['(', '[', '{'].indexOf(v) > -1){
      stack.push(v)
    } else {
      // 检测是否出栈和返回false
      const peak = stack.pop()
      if(v !== mapObj[peak]){
				 valid = false
      }
    }
  }
  if(stack.length > 0) return false;
  return valid;
}
```

3 给定一个字符串 `s`，找到 `s` 中最长的回文子串。你可以假设 `s` 的最大长度为 1000。

> 回文字符串： `aba` 正反读都一样的 

思路:

1. 回文字符串一定是对称的, 所以我们可以每次选择一个中心, 然后从中心向两边扩展判断左右字符是否相等
2. 中心点的选取有两种情况
   1. 长度为奇数时, 以单个字符为中心
   2. 长度为偶数时，以两个字符中间的空隙为中心

详解

1. 循环遍历字符串取得不同长度的子串
2. 通过定义好的中心扩展方法，选取奇数对称和偶数对称的中心
3. 通过比较选择两种组合较大的回文子串长度，然后对比之前的长度，判断是否更新起止为止
4. 全部遍历完成后，根据最后的起止为止的值， 截取最长回文子串

```javascript
var longestPalindrome = function (s) {
    if (!s || !s.trim()) return '';
    if (s.length === 1) return s;
    let start = 0;
  	let end = 0;
  	const expandFromCenter = (s, left, right) => {
      while(left >= 0 && right < s.length && s[left] == s[right]) {
        	left -= 1
        	right += 1
      }
      return right - left - 1
    }
    for(let i = 0; i < s.length; i ++) {
      	let len1 = expandFromCenter(s, i, i)
        let len2 = expandFromCenter(s, i, i+1)
        let len = Math.max(len1, len2)
        //	update
        if(len > end - start) {
          start = i - Math.floor((len - 1) / 2)
          end = i + Math.floor(len / 2)
        }
    }
  	return s.substring(start, end + 1)
}
```

4. 最长公共前缀

   编写一个函数来查找字符串数组中的最长公共前缀，如果不存在公共前缀, 返回空字符串

   思路:

   ​	查找 n 个字符串的最长公共前缀，可以拆分成两步: 1. 查找前 n-1 个字符串的最长公共前缀 m 2. 查找 m 与最后一个字符串的公共前缀

   详解:

   1. 获取数组中第一个字符串，当做最长公共前缀保存到变量commonPrefix
   2. 从数组中取出下一个字符串，与当前的最长公共前缀   对比，得到新的最长公共
      前缀存到 commonPrefix
   3. 重复第 2 步遍历完整个字符串，最后得到的即使数组中所有字符串的最长公共前缀

   ```javascript
   // ['flower', 'flow', 'flight']
   // 'fl'
   
   function findCommonPrefix(a, b) {
   	let i = 0;
   	while(i < a.length && i < b.length && a.charAt(i) === b.charAt(i)) {
   		i++
   	}
   	return i > 0 ? a.substring(0, i) : ''
   }
   
   function longestCommonPrefix(strs) {
   	if(strs.length > 0) {
   		let commonPrefix = strs[0]
   		for(let i = 1; i<strs.length; i++){
   			commonPrefix = findCommonPrefix(commonPrefix, strs[i])
   		}
   		return commonPrefix
   	}
   	return ''
   }
   ```

   

5. 验证回文字符串

   思路： 初始和结束位置一定相等

   ```javascript
   const isPalindrome = (s) => {
   	const arr = s.toLowerCase().replace(/[!A-Za-z0-9]/g, '').split('');
     let i = 0;
     let j = arr.length - 1;
     while(i < j) {
       if(arr[i] == arr[j]) {
         i += 1
         j -= 1
       } else {
         return false
       }
     }
     return true;
   }
   ```

   

6. 