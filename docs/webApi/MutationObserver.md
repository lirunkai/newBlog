# MutationObserver

提供了监控对DOM树所做更改的能力, 如果Dom节点有任何变动, 都会通知这个API

`MutationObserver()`

创建并返回一个新的 MutationObserver 它会在指定的DOM发生变化时被调用

```
let bodyObserver = new MutationObserver(callback)

function callback(mutations){
   // mutations 变动数组 (MutationRecord)
}
```

`observe(dom, options)`

observe配置DOM的哪些options改动了触发MutationObserver。

*options*

1. `childList` 子节点的增加或者删除

2. `attributes` 属性的更改

3. `characterData` 节点内容或节点文本的变动

4. `subtree` 是否用于后代所有节点

5. `attributeOldValue` 记录改变前的值

6. `attributeFilter` 观察特定的属性

`disconnect()`

阻止MutationObserver实例继续接受通知

`takeRecords()`

清空变动的记录

## MutationRecord 变动记录

Dom每次发生变化后, 就会生成一条记录, MutationObserver实例的回调函数中处理的就是MutationRecord

拥有以下属性

1. `type`  变动的类型 `childList`   `attribute`

2. `target`  变动的节点

3. `addedNodes` 新增的节点

4. `removedNodes` 删除的节点

5. `attributeName` 发生变动的属性

6. `oldValue` 原来的值
