# 布局

## 两栏布局

1. 使用float和BFC

例如 左侧固定宽, 右侧自适应

```
<div class="box">
  <div class="left"></div>
  <div class="right"></div>
</div>

<style>

.left {
  float: left;
  margin-right: 10px;
}

.right {
  overflow: inline-block;
}

</style>

```
