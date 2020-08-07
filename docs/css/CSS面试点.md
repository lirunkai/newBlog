### css选择器优先级

`!important`  > `内联` > `id`>  `类选择器 、属性选择器、伪类选择器`  > `元素选择器、关系选择器、伪元素选择器`  > `通配符选择器`

### css加载会造成阻塞么

css不会阻塞DOM解析，但会阻塞DOM渲染

css会阻塞js执行， 但不会阻塞js下载


### 盒模型

`box-sizing: content-box`

`box-sizing: border-box`

`box-sizing: margin-box`



### 伪类和伪元素

伪类用于当已有元素处于的某个状态时，为其添加对应的样式，这个状态是根据用户行为而动态变化的。比如说，当用户悬停在指定的元素时，我们可以通过:hover来描述这个元素的状态。虽然它和普通的css类相似，可以为已有的元素添加样式，但是它只有处于dom树无法描述的状态下才能为元素添加样式，所以将其称为伪类。

伪元素用于创建一些不在文档树中的元素，并为其添加样式。比如说，我们可以通过:before来在一个元素前增加一些文本，并为这些文本添加样式。虽然用户可以看到这些文本，但是这些文本实际上不在文档树中



伪类的操作对象是文档树中已有的元素，而伪元素则创建了一个文档树外的元素。因此，伪类与伪元素的区别在于：**有没有创建一个文档树之外的元素。**



### CSS3新增的属性

`transition`       `transform`      `animation`

`border-radius`       `box-shadow`       `border-image`

`background-clip`         `background-origin`        `background-size`       `background-break`

`word-wrap`         `text-overflow`       `text-shadow`       `text-decoration`    `text-fill-color`          

 `text-stroke-color`       `text-stroke-width`

`@font-face`         `box-sizing`         `outline-offset`



去除select的默认样式

`appearance : none`



### H5标签

`section`

`nav`

`menu`

`article`

`aside`

`header` `footer` `main`

`time`

`embed` 代表一个*嵌入* 的外部资源，如应用程序或交互内容。

`video` `audio` 媒体资源

 `source`  指定*媒体源*

`track` 元素指定*文本轨道*

`canvas` 代表*位图区域* ，可以通过脚本在它上面实时呈现图形，如图表、游戏绘图等。

`svg`  定义一个嵌入式*矢量图* 。

`progress` 进度条

`meter` 滑动条

``