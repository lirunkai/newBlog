
Source Map

在调试时将产物代码显示回源代码



优化

+ Happypack 多进程编译
+ include和exclude限制loader范围
+ 缓存babel编译过的文件
+  tree shaking删除冗余代码
+ 按需加载，按需引入



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



第三方库

```
new webpack.DllReferencePlugin({
  manifest: resolve(__dirname, "dll/manifest.json"),
}),
```



