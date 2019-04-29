## FormData

表单数据的键值对的构造方式, 添加完数据之后可以使用`XMLHttpRequest.send()` 方法发出.

```javascript
let formData = new FormData()
formData.append(key, value)
```

### 方法

**formData.append(name, value, [filename])**

添加一个新值到formData对象内的一个已存在的键中, 如果键不存在则创建该键

`name` 数据对应的表单名称

`value` 表单的值，可以是`Blob`或者`File`

`filename` 传给服务器的文件名称

**formData.delete(name)**  删除的键名字

**formData.set(name, value, filename)**

为name设置一个新的值，如果有值，覆盖之前的值

**formData.get(name)** 返回`formData`对象中和指定值相关的第一个值

**formData.getAll(name)** 返回`formData`指定key的所有值

**formData.has(name)** 返回一个布尔值, 表示该`FormData`中是否含有某个name

**formData.keys()**

**formData.values()**

**formData.entries()**
