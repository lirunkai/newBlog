jest

测试框架

这里说一下写代码的逻辑： 先写测试用例 => 写代码 => 运行测试用例  => 通过上线

### 命令行

`jest`

### EXPECT

`.not` 确定不是某个值

```javascript
expect(1+1).not.toBe(3) => pass
```



### 匹配器

`toBeNull` 只匹配`null`

`toBeUndefined` 只匹配`undefined`

`toBeDefined` 和`toBeUndefined`相反

`toBeTruthy` 匹配任何if为真的情况

`toBeFalsy` 匹配任何if为假的情况

`toBe()` 精确匹配

`toEqual()` 递归检查对象或数组的每个字段

```javascript
let data = { one: 1}
data.two = 2
expect(data).toEqual({one: 1, two: 2})
```



`toMatch()` 检查正则表达式的字符串

`toContain()` 检查一个数组或可迭代对象是否包含某个特定项

数字相关的匹配器

`toBeGreaterThan(num)`

### 异步

**fetchData**

Promise

```
test('the data is peanut butter', () => {
  return fetchData().then(data => {
    expect(data).toBe('peanut butter');
  });
});
```

async

```
test('the data is peanut butter', async () => {
  const data = await fetchData();
  expect(data).toBe('peanut butter');
});

test('the fetch fails with an error', async () => {
  expect.assertions(1);
  try {
    await fetchData();
  } catch (e) {
    expect(e).toMatch('error');
  }
});
```

