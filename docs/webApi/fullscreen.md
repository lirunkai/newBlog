# 全屏API

全屏展示某个元素

## 设置为全屏

**requestFullscreen**

目前这个方法有兼容性问题, 所以我们考虑写个兼容

```
function setFullScreen(dom){
  if(dom.requestFullscreen){
    dom.requestFullscreen()
  } else if(dom.msRequestFullscreen){
    dom.msRequestFullscreen()
  } else if(dom.mozRequestFullScreen){
    dom.mozRequestFullScreen()
  } else if(dom.webkitRequestFullscreen){
    dom.webkitRequestFullscreen()
  }
}

```


## 退出全屏

`dom.exitFullscreen()`


### 其他信息

`document.fullscreen` 当前是否是全屏模式

`document.fullscreenElement` 目前全屏的元素

`document.fullscreenEnabled` 当前文档是否允许进入全屏模式
