## vue-electron

在vue的代码中使用electron

```vue
import VueElectron from 'vue-electron';

Vue.use(VueElectron)

// 在其他.vue文件内可以通过

this.$electron访问electron包的API
this.$electron.remote.app.getName()
```

源码

```javascript
  
const electron = require('electron')

module.exports = {
  install: function (Vue) {
    Object.defineProperties(Vue.prototype, {
      $electron: {
        get () {
          return electron
        },
      },
    })
  },
}

or

module.exports = {
  install: function(Vue){
    Vue.prototype.$electron = electron;
  }
}
```

