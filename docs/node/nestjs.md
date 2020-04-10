nestjs



装饰符

在`@nestjs/common`包中的装饰符

`@HttpCode(204)`。自定义状态码

`@Post()`

@Headers('Cache-Control', 'none')`  自定义响应头

`@Get()`

```typescript
@Post()
@Header('Cache-Control', 'none')

create() {
  return 'This action adds a new cat';
}
```



方法参数装饰器

`@Request()`  对应Express的req对象

`@Response()`  对应Express的res对象

`@Next()` 对应Express的next对象

`@Session()` 对应res.session

`@Body(param)`  

`@Redirect()`

`@Query(param)`

`@Param(param)`    动态参数

```typescript
@Get(':id')
findOne(@Param('id') id):string {
	return `This action returns a #${id} cat`
}
```

`@Global()`     使模块成为全局作用naug

`@ValidationPipe`