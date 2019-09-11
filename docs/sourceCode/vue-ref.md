## vue-ref的源码

这里说的vue-ref是一个npm包



```javascript
"use strict";

Object.defineProperty(exports, "__esModule", {
	value: true
})

exports.default = {
	// vue插件经典install方法
	install: function install(Vue){
		var options = arguments.length > 1 && arguments[1] !== undefined ? arguments[1] : {};
		// 推断出使用时需要传入{name}
    var directiveName = options.name || 'ref';
		Vue.directive(directiveName, {
			bind: function(el, binding, vnode){
        // binding.value 指令的绑定值
        // 推断出绑定值为函数 参数为compoennt或者el，还有循环时的key
        binding.value(vnode.componentInstance || el, vnode.key)
      },
      update(el, binding, vnode, oldVnode){
        // vnode data为VNodeData类型, 指明绑定的component返回的directives,filters...
        if (oldVnode.data && oldVnode.data.directives) {
          // 获取到指令的绑定对象
          var oldBinding = oldVnode.data.directives.find(function (directive) {
            var name = directive.name;
            return name === directiveName;
          });
          if (oldBinding && oldBinding.value !== binding.value) {
            oldBinding && oldBinding.value(null, oldVnode.key);
            binding.value(vnode.componentInstance || el, vnode.key);
            return;
          }
        }
        // Should not have this situation
        if (vnode.componentInstance !== oldVnode.componentInstance || vnode.elm !== oldVnode.elm) {
          binding.value(vnode.componentInstance || el, vnode.key);
        }
      },
      unbind(el, binding, vnode){
        binding.value(null, vnode.key);
      }
		})
	}
}
```

回顾下vue指令的写法

`Vue.directive()`来声明全局指令

指令的声明周期

`bind`   只调用一次，指令第一次绑定到元素时调用, 可以设置一些初始化的任务

`inserted`     被绑定元素插入父节点时调用

`update`  所在组件的 VNode 更新时调用

`componentUpdate`  指令所在组件的 VNode **及其子 VNode** 全部更新后调用

`unbind` 只调用一次， 指令与元素解绑时调用



指令的参数

`el` 指令所绑定的元素， 可直接操作dom

`binding`   一个对象，包含

+ `name` 指令名
+ `value` 指令的绑定值
+ `oldValue` 绑定指令的前一个值
+ `expression` 字符串形式的指令表达式
+ `arg`  传递给指令的参数 `v-foo:bar`
+ `modifiers` 传递给指令的修饰符 `v-foo.bar`

`vnode`  [vnode](https://github.com/vuejs/vue/blob/dev/src/core/vdom/vnode.js)

`oldVnode`  仅在`update`和`componentUpdate`中传递

