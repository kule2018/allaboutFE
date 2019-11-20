#### vue中的$mount()与el

```javascript
new Vue({
     render: h => h(App),
   }).$mount('#app')

//vue的$mount()为手动挂载，在项目中可用于延时挂载(例如在挂载之前要进行其它的一些操作，判断等)，之后在手动挂载上。new vue时，el和$mount()没有本质区别。
```

