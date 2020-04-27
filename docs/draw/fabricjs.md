Fabric

安装

`npm install fabric`

### Canvas

```javascript
import { fabric } from 'fabric'

let canvas = new fabric.Canvas(document.getElementById('main'), {
	width: 100,
	height: 100,
})
```

属性

+ `backgroundColor`  背景色
+ `setBackgroundColor（）`
+ `backgroundImage`
+  `overlayColor` 覆盖一层颜色
+  `setOverlayColor()`

通过fabric.Canvas会创建两个canvas， 一静一动， 我们所做的操作都是映射到



### StaticCanvas