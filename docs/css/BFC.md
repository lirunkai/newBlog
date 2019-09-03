# BFC

块级格式上下文， 是一个独立的渲染区域


**怎么会触发BFC呢?**

1. float值不是none
2. overflow值为 auto scroll hidden
3. display为  table-cell、table-caption 和 inline-block 其中的一个
4. position的值是 absolute 或者 fixed

解决了什么？？

垂直方向上的margin重叠

**BFC的布局规则，特征:**  

1. 内部的Box会在垂直方向, 一个接一个地放置。

2. Box的垂直方向由margin决定。属于同一BFC的两个相邻Box的margin会发生重叠

3. BFC的区域不会与float box重叠

4. BFC内部的元素不会受到外部元素的影响。 外部元素也不会受到BFC元素的影响。

5. 计算BFC高度时, 浮动元素也参与计算

> 饮用
> [关于CSS-BFC深入理解](https://juejin.im/post/5909db2fda2f60005d2093db#heading-16)
