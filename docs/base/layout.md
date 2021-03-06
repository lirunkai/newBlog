# 布局

flex布局

## 水平居中

1. parent `text-align: center ` child `display: inline-block`

2. child `display: table; margin: 0 auto;`

3. parent `position: relative;` child `position: absolute; left: 50%; transform: translateX(-50%)`

4. parent `display: flex; justify-content: center;`

## 垂直局中

1. parent `display: table-cell;  vertical-align: middle;`

2. parent `position: relative; ` child `position: absolute; top: 50%; transform: translateY(-50%)`

3. parent `display: flex; align-items: center;`

## 水平垂直都居中

1. parent `display: table-cell; text-align: center; vertical-align: middle;` child: `display: inline-block`

2. parent `position: relative` child: `position: absolute; top: 50%; left: 50%; transform: translate(-50%, -50%)`

3. parent `display: flex; justify-content: center; align-items: center;`

4. parent `display: grid;` child: `justify-self: center; align-self: center;`

## 两栏布局

1. 使用float和BFC (块级格式上下文` Block Formatting Context`)

```
.left {
  margin-right: 10px;
  float: left;
  width: 40px;
}

.right {
  overflow: hidden;
}
```

2. flex布局

```
.parent {
  display: flex;
}

.left {
  width: 100px;
  padding-right: 20px;
}

.right {
  flex: 1;
}
```

## 多列定宽， 一列不定布局

1. float 和 BFC

```
.left, .center {
  float: left;
  width: 300px;
  margin-right: 10px;
}

.right {
  overflow: hidden;
}

```

2. flex

```
.parent{
	display: flex;
}
.left,.center{
	width: 100px;
	padding-right: 20px;
}
.right{
	flex: 1;
}

```

## 一列不定宽 一列自适应

1. float + BFC

```
.left{
	float: left;
	margin-right: 20px;
}
.right{
	overflow: hidden;
}

```

2. flex

```
.parent{
	display: flex;
}
.left{
	margin-right: 20px;
}
.right{
	flex: 1;
}
```

## 上下固定， 中间自适应

绝对定位
```css
header {
  position: absolute;
  top: 0;
  width: 100%;
  height: 100px;
  background: red;
}
.container {
  position: absolute;
  top: 100px;
  bottom: 100px;
  width: 100%;
  background: green;
}
.footer {
  position: absolute;
  bottom: 0;
  height: 100px;
  width: 100%;
  background: red;
}
```

flex布局
```css
body {
  height: 100%;
}

body {
  display: flex;
  padding: 0;
  margin: 0;
  flex-direction: column;
}

.header {
  height: 100px;
  background: red;
}
.container {
  flex-grow: 1;
  background: green;
}
.footer {
  height: 100px;
  background: red;
}
```
