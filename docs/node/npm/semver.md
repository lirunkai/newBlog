## semver

semver 语义化版本号

版本号 `x.y.z`

x 主版本号  (如果做了不兼容修改)

y 次版本号 (当你做了向下兼容的功能性新增)

z  修订号 

#### 下载

`npm i semver -S`

#### 使用

`semver.valid('1.2.3')`    返回已解析的版本, 无效返回null

`semver.clean('  1.2.3 a')`   

`semver.satisfies('1.2.3', '1.x || >= 2.5.0 || 5.0.0 - 7.2.3')`   满足验证条件 返回true或者false

`semver.coerce(string)` 强制将字符串转成semver

`semver.major(v)`	 返回主要版本号

`semver.minor(v)`    返回次要版本号

`semver.patch(v)`     返回补丁版本号



