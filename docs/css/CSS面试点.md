### css选择器

+ id选择器
+ class选择器
+ 后代选择器 `ul li`
+ 相邻后代选择器`ul > li`
+ 兄弟选择器 `a~span`
+ 相邻兄弟选择器 `a+span`

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