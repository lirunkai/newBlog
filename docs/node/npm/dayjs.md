## dayjs

轻量的处理时间和日期的`JavaScript`库

### 下载

`npm i dayjs -S`

### 解析

`dayjs('2019-01-01')`

`dayjs()`

`dayjs(new Date(2018,8,18))`

`dayjs(123123123123)`

### 赋值

`dayjs().set(key, value)`

​	Key: ` date day month year hour minute second millisecond`

增加

`dayjs().add(value, key)`

减少

`dayjs().subtract(value, key)`

### 格式化

`dayjs().format('YYYY-MM-DD HH:mm:ss')`

### 查询

`dayjs().year()`   获取年, 返回number

`dayjs().month()` 获取月, 返回number

`dayjs().date()`    获取日, 返回number

`dayjs().day()`     获取星期, 返回number

`dayjs().hour()`

`dayjs().minute()`

`dayjs().second()`

`dayjs().millisecond()`

当前时间戳 `dayjs().valueOf()`       毫秒

当前时间戳 `dayjs().unix()`      秒

当前月的天数 `dayjs().daysInMonth()`

两个时间差 

```javascript
const date1 = dayjs('2019-01-25');
const date2 = dayjs('2018-06-05');
date1.diff(date2); // 20214000000
date1.diff(date2, 'month'); // 7
date1.diff(date2, 'month', true); // 7.645161290322581
date1.diff(date2, 'day'); // 233
```



### 验证

`dayjs().isValid()`  是否是一个有效时间, 返回Boolean



