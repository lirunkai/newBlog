## jest

Jest测试包

### 匹配器

```
test('two plus two is four', () => {
    expect(2 + 2).toBe(4)
})
```

`toBe`  检查是否匹配（Object.is()）

`toEqual`    递归检查对象或数组的每个字端

`toBeNull` 匹配null

`toBeUndefined`    匹配undefined

`toBeDefined`     与`toBeUndefined`相反

`toBeTruthy`     匹配if语句为真

`toBeFalsy`	 匹配if语句为假

`toBeCloseTo()` 匹配浮点数

`toMatch()` 匹配正则

`toContain()`   检查数组，是否包含

#### 处理异步



