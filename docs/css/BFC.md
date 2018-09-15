# BFC

块级格式上下文

特征:

1. 不会影响到外部元素

2. margin不会重叠


怎么会触发BFC呢?

1. float值不是none

2. overflow值为 auto scroll hidden

3. display为  table-cell、table-caption 和 inline-block 其中的一个

4. position的值是 absolute 或者 fixed
