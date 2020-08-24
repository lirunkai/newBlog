## jsx

描述当前组件内容的数据结构

JSX在运行时的返回结果（即React.createElement()的返回值）都是React Element

---
1. 为什么每个jsx文件中都必须显示声明React?

因为`jsx`被`@babel/plugin-transform-react-jsx`解析时会被解析成`React.createElement`，如果没有显示声明React，在模块运行时该模块内会报**未定义变量React**的错误

2. 为什么需要key?

需要通过key来查询两棵树是否有同一节点

+ 在两个树对比过程中, 如果没有key, 节点交换位置的时候会直接销毁这两个节点， 而不是复用

3. react的Diff算法？

完全diff的话很慢。

react对diff做了3层限制:

  1. 只对同级Diff
  2. 两个不同类型的元素会产生不同的树
  3. 开发者可以通过 key prop来暗示哪些子元素在不同的渲染下能保持稳定