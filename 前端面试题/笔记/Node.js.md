## I/O

线程在执行中若遇到磁盘读写或网络通信（统称为I/O操作），通常要耗费较长的时间，此时操作系统会剥夺这个线程的CPU控制权，使其暂停执行，同时将资源让渡给其他工作线程，这种线程调度的方式称为阻塞。
当I/O操作完毕后，操作系统将这个线程的阻塞状态解除，恢复其对CPU的控制权，令其继续执行。这种I/O模式即传统的同步式I/O（Synchronous I/O）或阻塞式I/O（Blocking I/O）。

异步式I/O（Asynchronous I/O）或非阻塞式I/O（Non-blocking I/O）则针对所有I/O操作不采用阻塞的策略。当线程遇到I/O操作时，不会阻塞的方式等待I/O操作的完成或数据的返回，而只是将I/O请求发送给操作系统，继续执行下一条语句。当操作系统完成I/O操作时，以事件的形式通知执行I/O操作的线程，线程会在特定时候处理这个事件。为了处理异步I/O，线程必须有事件循环，不断地检查有没有未处理的事件，依次予以处理。 



## Node.js是什么

Node.js是一个基于chrome V8引擎的JavaScript的运行环境

Node.js 使用了一个事件驱动，非阻塞I/O的模型。

Node.js 轻量又高效，能够使我们在本地运行 JavaScript。





## 服务器 Node.js 和 浏览器 js 的区别是什么？

node.js 是运行环境，一种平台；JavaScript 是一种编程语言；

node.js 是一个基于 Chrome JavaScript 运行时建立的平台，它是对 Google V8 引擎进行了封装的运行环境；

JavaScript 是客户端编程语言，需要浏览器的JavaScript 解释器进行解析执行；

node.js 就是把浏览器的解释器封装起来作为服务器运行平台，用类似JavaScript的结构语法进行编程，在node.js 上运行；




## Node.js 中的五大核心模块

模块	                                                         作用
HTTP	                          开启一个 web 服务，给浏览器提供服务
URL	               给浏览器发送请求用，还可以传递参数（GET）也就是获取用户发送的请求的相关信息
QueryString	   处理浏览器通过 GET / POST 发送过来的参数，把请求的参数字符串转为 js 对象
Path	                                              获取文件的路径
FileSystem                   	在服务器端读取文件使用，文件操作



## CommonJS规范、核心模块

![\color{red}{Node应用由模块组成，采用CommonJS模块规范。}](https://math.jianshu.com/math?formula=%5Ccolor%7Bred%7D%7BNode%E5%BA%94%E7%94%A8%E7%94%B1%E6%A8%A1%E5%9D%97%E7%BB%84%E6%88%90%EF%BC%8C%E9%87%87%E7%94%A8CommonJS%E6%A8%A1%E5%9D%97%E8%A7%84%E8%8C%83%E3%80%82%7D)

根据这个规范，每个文件就是一个模块，有自己的作用域。在一个文件里面定义的变量、函数、类，都是私有的，对其他文件不可见。

CommonJS规范规定，每个模块内部，module变量代表当前模块。这个变量是一个对象，它的exports属性（即module.exports）是对外的接口。加载某个模块，其实是加载该模块的module.exports属性。

```javascript
var x = 5;
var addX = function (value) {
  return value + x;
};
module.exports.x = x;
module.exports.addX = addX;
```

上面代码通过module.exports输出变量x和函数addX。

require方法用于加载模块。

```javascript
var example = require('./example.js');

console.log(example.x); // 5
console.log(example.addX(1)); // 6
```



#### 核心

```cpp
module对象：在每一个模块中，module对象代表该模块自身。
export属性：module对象的一个属性，它向外提供接口。
 缓存      如果多次引入一个模块，会缓存模块，不会重复执行
```

#### commonjs规范的优点(解决的问题)

```undefined
* CommonJS模块规范很好地解决变量污染问题，
* 每个模块具有独立空间，互不干扰，命名空间等方案与之相比相形见绌。
* CommonJS规范定义模块十分简单，接口十分简洁。
* CommonJS模块规范支持引入和导出功能，这样可以顺畅地连接各个模块，实现彼此间的依赖关系。
```

