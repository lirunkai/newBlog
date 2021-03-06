### 加载

link or @import

Link: 页面会同步加载所引的 css,  可以通过js动态加载

@import:  所引用的css会等到页面加载完才加载

加载完成后解析为CSSOM, 解析过程中不会阻塞DOM的解析, 但是会阻塞DOM的渲染, 等到CSSOM和DOM都解析完成后, 共同构建Layout树, 进行渲染

说到渲染就了解下重绘和回流

## 重绘 | 回流

回流: 布局或者结构需要改变称为回流

重绘: 节点需要改变外观而不会对结构造成影响称为重绘


引起回流：
1. 改变窗口大小
2. 元素的添加和删除
3. 浮动

减少回流：
1. transition替代top, left的修改
2. visibility替代display:none
3. 动画实现的速度的选择，动画速度越快，回流次数越多，也可以选择使用 requestAnimationFrame
4. 不要使用 table 布局

## 动画

transition 过渡动画

```css
div:hover {
  transition: 2s;
  transform: translateX(100px);
}
```

animation

1. 通过`@keyframe`定义规则
2. 使用animation 规则

```css
@keyframes myfirst
{
0%   {background:red; left:0px; top:0px;}
25%  {background:yellow; left:200px; top:0px;}
50%  {background:blue; left:200px; top:200px;}
75%  {background:green; left:0px; top:200px;}
100% {background:red; left:0px; top:0px;}
}

animation: myfirst 2s;
```






### css选择器

+ id选择器
+ class选择器
+ 后代选择器 `ul li`
+ 相邻后代选择器`ul > li`
+ 兄弟选择器 `a~span`
+ 相邻兄弟选择器 `a+span`

CSS 选择符从右往左匹配查找，避免 DOM 深度过深

优先级

`!important`  > `内联` > `id`>  `类选择器 、属性选择器、伪类选择器`  > `元素选择器、关系选择器、伪元素选择器`  > `通配符选择器`

### css加载会造成阻塞么

css不会阻塞DOM解析，但会阻塞DOM渲染

css会阻塞js执行， 但不会阻塞js下载


### 盒模型

盒模型分为: content, padding, border, margin

w3c标准盒模型: 属性width和height只包含content，不包含padding， border

ie盒模型： width和height包含 content, padding, border

`box-sizing: content-box`

`box-sizing: border-box`

`box-sizing: margin-box`



### 伪类和伪元素

`:`  用于伪类
`::` 用于伪元素

伪类用于当已有元素处于的某个状态时，为其添加对应的样式，这个状态是根据用户行为而动态变化的。比如说，当用户悬停在指定的元素时，我们可以通过:hover来描述这个元素的状态。虽然它和普通的css类相似，可以为已有的元素添加样式，但是它只有处于dom树无法描述的状态下才能为元素添加样式，所以将其称为伪类。

伪元素用于创建一些不在文档树中的元素，并为其添加样式。比如说，我们可以通过:before来在一个元素前增加一些文本，并为这些文本添加样式。虽然用户可以看到这些文本，但是这些文本实际上不在文档树中


伪类的操作对象是文档树中已有的元素，而伪元素则创建了一个文档树外的元素。因此，伪类与伪元素的区别在于：**有没有创建一个文档树之外的元素。**

`elem:nth-child(n)` 选中父元素下的第 n 个子元素

`elem:last-child` 选中最后一个子元素

`elem:only-child` 如果 elem 是父元素下唯一的子元素，则选中之

`elem:first-of-type` 选中父元素下第一个 elem 类型元素

`elem:last-of-type` 选中父元素下最后一个 elem 类型元素

`elem:only-of-type` e 如果父元素下的子元素只有一个 elem 类型元素，则选中该元素

`elem:target` 选择当前活动的 elem 元素

`:not(elem)` 选择非 elem 元素的每个元素

`:enabled` 控制表单控件的禁用状态

`:disabled` 控制表单控件的禁用状态

`:checked` 单选框或复选框被选中

### CSS3新增的属性

`transition`       `transform`      `animation`

`border-radius`       `box-shadow`       `border-image`

`background-clip`         `background-origin`        `background-size`       `background-break`

`word-wrap`         `text-overflow`       `text-shadow`       `text-decoration`    `text-fill-color`          

 `text-stroke-color`       `text-stroke-width`

`@font-face`         `box-sizing`         `outline-offset`



去除select的默认样式

`appearance : none`

### 使用css创建三角形的原理

相邻边框连接处的均分原理

将元素的宽高设为 0，只设置border ，把任意三条边隐藏掉（颜色设为transparent），剩下的就是一个三角形。

### 实现一个自适应正方形

```css
.square {
  width: 10vw;
  height: 10vw;
  background: red;
}

// pandding和margin的百分比是参照父元素的width属性
.square {
  width: 20%;
  height: 0;
  padding-top: 20%;
  background: orange;
}
```

### 实现一个自适应长方形

```css
.box {
  position: absolute;
  top: 0;
  right: 0;
  left: 0;
  bottom: 0;
  margin: auto;
  width: 10%;
  height: 0;
  padding-top: 20%;
  background: tomato;
}
```



### 文本溢出

```css
// 单行
.text{
	overflow: hidden;
	text-overflow: ellipsis; (省略号)
	white-space: nowrap; (不换行)
}
// 多行
.text {
  display: -webkit-box;
  overflow: hidden;
  -webkit-line-clamp: 2;
  -webkit-box-orient: vertical;
  text-overflow: ellipsis;
}
```


## BFC

块级格式上下文， 是一个隔离的独立容器。

它决定了元素如何对其内容进行定位以及与其他元素的关系和相互作用


**怎么会触发BFC呢?**

1. float值不是none
2. overflow值为 auto scroll hidden
3. display为  inline-block flex  inline-flex table-cell
4. position的值是 absolute 或者 fixed

解决了什么？？

+ 垂直方向上的margin合并
+ 自适应两栏布局
+ 清除浮动

**BFC的布局规则，特征:**  

1. 内部的Box会在垂直方向, 一个接一个地放置。

2. Box的垂直方向由margin决定。属于同一BFC的两个相邻Box的margin会发生重叠

3. BFC的区域不会与float box重叠

4. BFC内部的元素不会受到外部元素的影响。 外部元素也不会受到BFC元素的影响。

5. 计算BFC高度时, 浮动元素也参与计算

> 饮用
> [关于CSS-BFC深入理解](https://juejin.im/post/5909db2fda2f60005d2093db#heading-16)



#### z-index的层级关系

+ 只有设置了`position为relative, absolute, fixed`才有作用
+ 对比时需要先对比父级别的`z-index`

`z-index`的层级关系只有在同一父级元素下才有意义， 也就是说跨父级别的子元素对比z-index没有意义， 应该先找到同一层级下的父元素对比其`z-index`。



#### 定位的相对位置

`postion:relative`是相对于元素的正常位置，但没有脱离文档流。宽高不变，设置偏移量不会影响其他元素的位置

`position:absolute`是相对于最近已定位的祖先元素，如果没有，就相对于body做偏移。 脱离文档流。



#### flex布局的相关属性

`flex`是 `flex-grow,flex-shrink,flex-basis`

`flex-direction`

`flex-wrap`

`jusitify-content`

`align-items`

`align-self`



#### 项目中对css的处理

+ 前缀
  + `postcss-loader` 
  
    ```javascript
    module.exports = {
      module: {
        rules: [
          {
            test: /\.css$/i,
            use: [
              'style-loader',
              'css-loader',
              {
                loader: 'postcss-loader',
                options: {
                  postcssOptions: {
                    plugins: [
                      require('autoprefixer')
                    ]
                  }
                }
              }
            ]
          }
        ]
      }
    }
    ```
  
+  压缩`css-minimizer-webpack-plugin`

+ `mini-css-extract-plugin`
