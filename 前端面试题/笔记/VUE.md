#### v-bind和v-model的区别

1.v-bind用来绑定数据和属性以及表达式，缩写为'：' 2.v-model使用在表单中，实现双向数据绑定的，在表单元素外使用不起作用

#### 什么是 mvvm？

MVVM 是 Model-View-ViewModel 的缩写。mvvm 是一种设计思想。Model 层代表数据模型，也可以在 Model 中定义数据修改和操作的业务逻辑；View 代表 UI 组件，它负责将数据模型转化成 UI 展现出来，ViewModel 是一个同步 View 和 Model 的对象。

在 MVVM 架构下，View 和 Model 之间并没有直接的联系，而是通过 ViewModel 进行交互，Model 和 ViewModel 之间的交互是双向的， 因此 View 数据的变化会同步到 Model 中，而 Model 数据的变化也会立即反应到 View 上。

ViewModel 通过双向数据绑定把 View 层和 Model 层连接了起来，而 View 和 Model 之间的同步工作完全是自动的，无需人为干涉，因此开发者只需关注业务逻辑，不需要手动操作 DOM, 不需要关注数据状态的同步问题，复杂的数据状态维护完全由 MVVM 来统一管理。

#### mvvm 和 mvc 区别？

mvc 和 mvvm 其实区别并不大。都是一种设计思想。主要就是 mvc 中 Controller 演变成 mvvm 中的 viewModel。mvvm 主要解决了 mvc 中大量的 DOM 操作使页面渲染性能降低，加载速度变慢，影响用户体验。和当 Model 频繁发生变化，开发者需要主动更新到 View 。

#### 你对 vue 生命周期的理解？

答：总共分为 8 个阶段创建前/后，载入前/后，更新前/后，销毁前/后。

- 创建前/后： 在 beforeCreate 阶段，vue 实例的挂载元素 el 还没有。
- 载入前/后：在 beforeMount 阶段，vue 实例的$el 和 data 都初始化了，但还是挂载之前为虚拟的 dom 节点，data.message 还未替换。在 mounted 阶段，vue 实例挂载完成，data.message 成功渲染。
- 更新前/后：当 data 变化时，会触发 beforeUpdate 和 updated 方法。
- 销毁前/后：在执行 destroy 方法后，对 data 的改变不会再触发周期函数，说明此时 vue 实例已经解除了事件监听以及和 dom 的绑定，但是 dom 结构依然存在



#### vue 的双向绑定的原理是什么(常考)

vue.js 是采用数据劫持结合发布者-订阅者模式的方式，通过 Object.defineProperty()来劫持各个属性的 setter，getter，在数据变动时发布消息给订阅者，触发相应的监听回调。

具体步骤： 第一步：需要 observe 的数据对象进行递归遍历，包括子属性对象的属性，都加上 setter 和 getter 这样的话，给这个对象的某个值赋值，就会触发 setter，那么就能监听到了数据变化

第二步：compile 解析模板指令，将模板中的变量替换成数据，然后初始化渲染页面视图，并将每个指令对应的节点绑定更新函数，添加监听数据的订阅者，一旦数据有变动，收到通知，更新视图

第三步：Watcher 订阅者是 Observer 和 Compile 之间通信的桥梁，主要做的事情是:

- 在自身实例化时往属性订阅器(dep)里面添加自己
- 自身必须有一个 update()方法
- 待属性变动 dep.notice()通知时，能调用自身的 update() 方法，并触发 Compile 中绑定的回调，则功成身退。

第四步：MVVM 作为数据绑定的入口，整合 Observer、Compile 和 Watcher 三者，通过 Observer 来监听自己的 model 数据变化，通过 Compile 来解析编译模板指令，最终利用 Watcher 搭起 Observer 和 Compile 之间的通信桥梁，达到数据变化 -> 视图更新；视图交互变化(input) -> 数据 model 变更的双向绑定效果。



#### Vuex

**State：**

vuex中的数据源，我们需要保存的数据就保存在这里，可以在页面通过 this.$store.state来获取我们定义的数据；

**Getters：**

Getter相当于vue中的computed计算属性，getter 的返回值会根据它的依赖被缓存起来，且只有当它的依赖值发生了改变才会被重新计算。

**Mutations：**

如果需要修改store中的值唯一的方法就是提交mutation来修改。Vuex 中的 mutation 非常类似于事件：每个 mutation 都有一个字符串的 **事件类型 (type)** 和 一个 **回调函数 (handler)**。

**Action** 

类似于 mutation，不同在于：

- Action 提交的是 mutation，而不是直接变更状态。
- Action 可以包含任意异步操作。





#### VUE生命周期

- 主要8个阶段，创建前/后，载入前/后，更新前/后，销毁前/后。 
- 创建前后: 在beforeCreated阶段，vue实例的挂载元素el和数据对象的data都为undefined，还未初始化。在created阶段，vue实例对象的data有了，但是el和数据对象的data都为undefined，还未初始化。在created阶段，vue实例对象的data有了，但是el和数据对象的data都为undefined，还未初始化。在created阶段，vue实例对象的data有了，但是el还没有。 
- 载入前后: 在beforeMount阶段，vue实例的$el和data都初始化了，但还是挂载之前的虚拟dom的节点。data的message还未替换。在mounted阶段，vue实例挂载完成，data.message成功渲染。 
- data变化后，触发beforeupdate和update方法。 
- 执行destory方法后，对data的改变不会再触发周期函数，说明此时vue实例已经解除了事件监听和dom的绑定，但是dom的结构依然存在。



#### VUE双向绑定

- vue采用数据监听和发布者-订阅模式。通过Object.defineProperty()来劫持各个属性的setter和getter，当数据变动时候发布消息给订阅者，触发相应回调。 
- 1.需要observer递归的遍历对象，包括对象的对象，给对象的某个值赋值或者改变，触发setter，那么监听到了数据的变化。 
- 2.complie解析各个v-的操作指令，将模板的变量替换成数据，初始化页面视图，并将每个指令对应的节点绑定更新函数，添加监听数据的订阅者，一旦有数据变动，接收通知，更新视图。 
- 3.watcher是observer和complie的桥梁，首先自身实例化向属性订阅器dep中添加自身，其次自身有一个update方法，在属性变动时，dep.notice()通知，调用自身的update方法，触发complie的回调。