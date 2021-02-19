
Source Map

在调试时将产物代码显示回源代码



优化

+ Happypack 多进程编译
+ include和exclude限制loader范围
+ 缓存babel编译过的文件
+  tree shaking删除冗余代码
+ 按需加载，按需引入
+ DllWebpackPlugin-> webpack4(HardSourceWebpackPlugin) -> webpack5(内部支持)
+ `terser-webpack-plugin`压缩js文件



静态文件的编译

`file-loader` 

```javascript
module.exports = {
  module: {
    rules: [
      {
        test: /\.(png|jpe?g|gif)$/i,
        use: [
          {
            loader: 'file-loader',
            options: {
	            // 根据文件内容生成的hash， 如果没有修改不会变
            	name: '[contentHash].[ext]',
            	// 存储到images
            	outputPath: 'images'
            }
          },
        ],
      },
    ],
  },
};
```

babel缓存

```
module.exports = {
	module: {
		rules: [
			{
				test: /.js/,
				use: [
					{
						loader: 'babel-loader',
						options: {
							cacheDirectory: true
						}
					}
				]
			}
		]
	}
}
```



### 什么是浏览器的热更新？

浏览器的热更新，指的是我们在本地开发的同时打开浏览器进行预览，当代码文件发生变化时，浏览器自动更新页面内容的技术

这里的自动更新，表现上又分为自动刷新整个页面，以及页面整体无刷新而只更新页面的部分内容。

webpack是如何做到的？

webpack通过webpack-dev-server启动一个服务器, 创建了一个socket通道， 通过socket通道可以通知浏览器页面有更新。

这样修改后有个问题。 比如我点开一个弹框, 发现弹框内样式有问题, 我需要去编辑器里修改。当我修改完之后,浏览器更新 弹框丢失了。需要重新进行操作， 那我如何保存当前页面的状态？

### Hot Module Replacement

模块热替换

通过devServer的hot属性来开启HMR

HMR做了什么？

每次修改时发送hot-update.json 和 hot-update.js请求， 而不是之前的刷新页面重新获取所有请求

hot-update.js会被插入到head中解析处理本次更新内容

