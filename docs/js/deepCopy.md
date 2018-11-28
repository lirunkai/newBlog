# 深拷贝 浅拷贝

为什么要把深拷贝和浅拷贝拉出来说？ 因为工作上很多问题都是因为这两个东西的理解不到位导致的.

## 深拷贝实现

1. JSON

```
let newObj = JSON.parse(JSON.stringify(obj))
```

2. 
