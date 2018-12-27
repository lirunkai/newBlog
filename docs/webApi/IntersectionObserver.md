# IntersectionObserver

异步监听目标元素和其祖先元素或视窗是否交叉。 祖先元素与视窗(viewport)被称为根(root)。

[demo](http://www.aidoudou.com.cn/webApi/interesectionObserver)

## 使用

`let elViewObserver = new IntersectionObserver(cb, options)`

`IntersectionObserver`实例是一个观察器。

**cb(entries)**

在`element`元素可见度到达阀值的时候, 会回调`cb`。

`element`进入视窗之后`cb`会执行一次, 离开视窗之后`cb`还会执行一次

`entries` `IntersectionObserverEntry`实例的对象list集合.

**options**

`root` 监听元素的祖先对象的盒边界作为`viewport`

`threshold` 设置阀值, 观察元素与可视窗口的交叉区比例, 设置为0到1之间的数组.

开始观察 `elViewObserver.observe(element)`

停止观察 `elViewObserver.unobserve(element)`

关闭观察 `elViewObserver.disconnect()`

**IntersectionObserverEntry**

实例对象的属性

`target` 目标元素

`time` 目标元素进入视口区的时间 毫秒数

`intersectionRect` 目标元素与视口的交叉区域的信息

`intersectionRatio` 目标元素的可见比例

`rootBounds` 根元素的矩形区域信息

`boundingClientRect` 目标元素的矩形区域信息


实例 demo源码

```
<template lang="pug">
  div.intersectionObserver
    h3 intersectionObserver
    div
      p 演示下intersectionObserver的使用
    div.box
      section 撑开一点高
      section 撑开一点高
      section 撑开一点高
      section 撑开一点高
      section 撑开一点高
      section 撑开一点高
      section 撑开一点高
      section 撑开一点高
    main.showYourCode
      p intersectionObserver所在位置
      h2 可见度 {{opacityByMe * 100}} %

    div.box
      section 撑开一点高
      section 撑开一点高
      section 撑开一点高
      section 撑开一点高
      section 撑开一点高
      section 撑开一点高
      section 撑开一点高
      section 撑开一点高
</template>

<script>
export default {
  data(){
    return {
      io: null,
      opacityByMe: 0
    }
  },
  mounted(){
    this.io = new IntersectionObserver((entries) => {
      this.opacityByMe = entries[0].intersectionRatio
    }, {
      threshold: [0, 0.1, 0.2, 0.3, 0.4, 0.5, 0.6, 0.7, 0.8, 0.9, 1]
    })
    this.io.observe(document.querySelector('.showYourCode'))
  },
  methods: {

  },
  beforeDestroy(){
    this.io.unobserve(document.querySelector('.showYourCode'))
  },
  destroyed(){
    this.io.disconnect()
  }
}
</script>

<style lang="less" scoped>
 section {
   height: 100px;
   border-left: 3px solid rgb(255, 141, 141);
   padding: 4px;
   color: rgb(255, 141, 141);
 }
 .showYourCode{
   display: block;
   min-width: 500px;
   height: 500px;
   background: yellow;
   p {
     text-align: center;
   }
 }
</style>

```
