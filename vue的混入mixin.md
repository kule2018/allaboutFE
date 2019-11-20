#### vue的混入mixin

##### 适用情况：

有两个相似的组件，基本功能是一样的，但它们又存在着足够的差异性，此时有两个选择：拆分成两个不同的组件，或者保留为一个组件，然后通过props传值来创造差异性从而进行区分。

然而两种方法都不好。前者当功能变动的时候可能要在两个文件中更新代码，违背了DRY的原则。后者，太多的props船只会很快变得混乱不堪，从而使维护者在使用组件的时候必须理解一大段上下文，效率降低。

##### 用法

按照自己喜欢的方式设置目录结构，可以新建一个mixins目录。创建的文件含有.js扩展名，且要输出对象。

![img](https://upload-images.jianshu.io/upload_images/8592917-b7d00f3ae3a285cf.jpg?imageMogr2/auto-orient/strip|imageView2/2/w/1112)

# 在.vue文件中这样使用

```js
 import Child from './Child'
    import { toggle } from './mixins/toggle'

    export default {
      name: 'modal',
      mixins: [toggle],
      components: {
        appChild: Child
      }
    }
```



##### 合并

当我们在组件上应用Mixin的时候，有可能组件与Mixin中都定义了相同的生命周期钩子，这时候钩子的执行顺序的问题凸显了出来。默认Mixin上会首先被注册，组件上的接着注册，这样我们就可以在组件中按需要重写Mixin中的语句。*组件拥有最终发言权*。当发生冲突并且这个组件就不得不“决定”哪个胜出的时候，这一点就显得特别重要，否则，所有的东西都被放在一个数组当中执行，Mixin将要被先推入数组，其次才是组件。

```jsx
 //mixin
  const hi = {
    mounted() {
      console.log('hello from mixin!')
    }
  }

  //vue instance or component
  new Vue({
    el: '#app',
    mixins: [hi],
    mounted() {
      console.log('hello from Vue instance!')
    }
  });

  //Output in console
  > hello from mixin!
  > hello from Vue instance!
```

如果这两个冲突了，我们看看 Vue实例或组件是如何决定输赢的：

```jsx
 //mixin
      const hi = {
        methods: {
          sayHello: function() {
            console.log('hello from mixin!')
          }
        },
        mounted() {
          this.sayHello()
        }
      }

      //vue instance or component
      new Vue({
        el: '#app',
        mixins: [hi],
        methods: {
          sayHello: function() {
            console.log('hello from Vue instance!')
          }
        },
        mounted() {
          this.sayHello()
        }
      })

      // Output in console
      > hello from Vue instance!
      > hello from Vue instance!
```

这有两个console.log而不是一个——这是因为第一个函数被调用时，没有被销毁，它只是被重写了。我们在这里调用了两次sayHello()函数。

也就是说，混入里面的方法可以被外面组件覆盖。当有更复杂的情况的时候，需要在组件里再定义下。