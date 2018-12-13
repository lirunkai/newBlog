# puppeteer

puppeteer是一个node包, 通过DevTools协议来控制chrome, 通过puppeteer可以实现一些自动化的流程, 爬虫以及全页面截图

## 启动浏览器

`puppeteer.launch(options)` 返回一个promise，代表启动了的浏览器

options
  1. headless 以无头模式运行浏览器。 默认为true
  2. defaultViewport 为每个页面设置一个默认视口大小  width, heigth

```
const browser = await puppeteer.launch({
  headless: false,
  defaultViewport: {
    width: 300,
    height: 400
  }
  });

```  

### 关闭浏览器

`browser.close()`

### 开启页面

`browser.newPage()`

```
const page = await browser.newPage()
```

### 等待

`page.waitFor(number)`

### 跳转到某个url

`page.goto(url， options)`

options
  1. timeout 跳转等待时间
  2. waitUntil 满足什么条件认为页面跳转完成
    1.  `load` 页面的load事件触发时
    2. `domcontentloaded` domcontentloaded事件触发时
    3. `networkidle0` 不再有网络连接时触发
    4. `networkidle2` 只有2个网络请求时触发

### 表单

`page.type(selector, text, {delay: 100})`   文本类的表单

`page.select(selector, ...values)`  选择器



### 截图

`page.screenshot(options)`

options

  1. path
  2. type 截图的格式 jpeg or png
  3. fullPage 如果设置为true，则对完整的页面


### 关于选择器

`page.$(selector)` 在页面内执行 document.querySelector

`page.$$(selector)`  在页面内执行 document.querySelectorAll

`page.$eval(selector, fn, ...args)` 在页面内执行 document.querySelector，然后把匹配到的元素作为第一个参数传给 pageFunction, args是你代码里的参数可以传入

`page.$$eval(selector, fn, ...args)` 把匹配到的元素数组作为第一个参数传给 pageFunction。


### 切换tab

`page.bringToFront()`

### 获取当前的browser

`page.browser()`


### 点击

`page.click(selector, options)`

options

 1. clickCount  点击次数
 2. delay  mousedown 和 mouseup 之间停留的时间，单位是毫秒

点击页面的元素 注意如果点击触发了一个跳转会有`page.waitForNavigation()`来等待跳转完成


### 页面内容

`page.content()` 返回页面完成的html代码


### 在页面中执行方法

`page.evaluate(fn, ...args)`
