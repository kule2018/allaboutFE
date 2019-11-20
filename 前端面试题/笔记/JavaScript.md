## JavaScript是一种什么样的语言

JavaScript是一种基于对象和事件驱动并具有相对安全性的客户端脚本语言。同时也是一种广泛用于客户端web开发的脚本语言，常用来给HTML网页添加动态功能。它是一种动态、弱类型、基于原型的语言，内置支持类。

具有以下特点：动态、弱类型、单线程，内置支持类。

#### 优点

**一种可解释执行的脚本语言**

和其他脚本语言一样，JavaScript也是一种解释性语言，它提供了一个非常方便的开发过程。JavaScript的语言基本结构形式与C、C++、java十分类似。但是在使用前，不需要先编译，而是在执行过程中逐步的解释。JavaScript与HTML标识结合在一起，方便用户的使用。

**一种基于对象的脚本语言**

JavaScript也是一种面向对象的语言，这意味着JavaScript能运用其已经创建好的对象。因此，许多功能可以来自脚本环境中对象的方法与脚本的相互作用。

**一种简单弱类型脚本语言**

简单是JavaScript是一种基于java基本语句和控制流之上的简单而紧凑的设计，从而对于使用者来说学习C或者java语言是一种很好地过渡。JavaScript也非常容易上手，其次变量类型采用的是弱类型，并未使用严格的数据类型。

**一种相对安全脚本语言**

JavaScript语言不允许访问本地的硬盘，且不能将数据存入服务器，不允许对网络文档进行修改和删除。从而有效的防止数据的丢失或对系统非法访问。

**一种事件驱动的脚本语言**

> JavaScript对于用户的响应，是以事件驱动的方式进行的。在网页的执行中，用户的操作被称为"事件"。当事件发生后，可能会引起相应的事件响应，执行对应的脚本，这种机制叫"事件驱动"。

**一种跨平台性脚本语言**

> JavaScript依赖的是浏览器本身，与其操作环境无关，只要计算机能运行浏览器，并支持JavaScript的浏览器，就可以正确执行。

**JavaScript减少网络传输**

> JavaScript可以被嵌入HTML文件中。所以当一位使用者输入一项资料时，此资料不需要传送给服务器，而是直接在客户端的应用程序所处理。



#### 缺点

**安全性**： JavaScript被显示的添加到网页和客户浏览器，它可以利用客户系统，有风险的代码可能在客户机器上执行。

**浏览器支持**： JavaScript在不同的浏览器中有时进行不同的解释。不同层引擎对JavaScript有不同的渲染结果， 这都是因为不同的功能和接口的差异性。大部分JavaScript依赖浏览器DOM元素的操作。并且，不同的浏览器对对象的访问类型不一样，尤其是Internet Explorer。

**更多更好竞争对手**： JavaScript是机器上运行的非常老的脚本化语言，其实有其他的技术可以取代它做同样的事情。(如 JQuery )，并且更好更简单。

**关闭JavaScript**：如果关闭浏览器的JavaScript支持，整个JavaScript代码就不会运行了。

**文件下载**： JavaScript文件可以在客户端电脑下载，任何人都可以阅读并且可以重复利用。







## 引用类型与原始类型

https://www.cnblogs.com/chaoyuehedy/p/7894971.html0

#### 基本数据类型：

- 基本数据的值是不可以改变的

  ```javascript
  var name = "change";
  name = "change1";
  console.log(name)//change1
  ```

  这样看起来name的值“改变了”
  其实，var name = "change"，这里的基础类型是string，也就是"change",这里的"change"是不可以改变的，name只是指向"change"的一个指针，指针的指向可以改变，所以你可以name = "change1".此时name指向了"change1"，同理，这里的"change1"同样不可以改变

  也就是说这里你认为的改变只是“指针的指向改变”

- 基本数据类型不可以 添加属性和方法

- 基本数据类型赋值是简单的赋值

  ```javascript
  var a = 10;
  var b = a;
  a++;
  console.log(a)//11
  console.log(b)//10
  ```

  用a的值来初始化b时，b中也保存了值10.但b中的10和a中的10是完全独立的.b中的值知识a中值的一个副本.所以这两个变量可以参与任何操作而不会相互影响.

- 基本数据类型比较是值的比较

- 基本数据类型是存放在栈中的

#### 引用类型

- 引用类型的值时可以改变的

- 引用类型的值可以添加属性和方法

- 引用类型的赋值是对象引用：引用对象保存在变量中的实际是保存在堆内存中的地址，当从一个变量向另一个变量赋值引用类型的值时，两个变量都保存了同一个对象地址，而这两个地址指向了同一个对象.因此，改变其中任何一个变量，都会互相影响。

- 引用类型的比较是引用的比较

  ```javascript
  ar person1 = {};
  var person2 = {};
  console.log(person1 == person2)//fale
  ```

  因为引用类型的比较是引用的比较，换句话说，就是比较两个对象保存在栈区的指向堆内存的地址是否相同，此时，虽然p1和p2看起来都是一个"{}"，但是他们保存在栈区中的指向堆内存的地址却是不同的，所以两个对象不相等

- 引用类型是同时保存在栈区和堆区中的



## JS判断数据类型

#### typeof

只能判断基本数据类型，例如function array 都返回object



#### instanceof

判断一个**对象**是否是另一个**对象**的实例  1 instanceof Number  返回false

例如：var a=[];console.log(a instanceof Array)   //返回来的值是true



#### constructor

console.log((2).constructor === Number);
console.log((true).constructor === Boolean);
console.log(('str').constructor === String);
console.log(([]).constructor === Array);

#### Object.prototype.toString.call

Object.prototype.toString.call(a)：[object Array]
Object.prototype.toString.call(b)：[object Null]
Object.prototype.toString.call(c)：[object Object]



## 类(伪)数组与数组的区别与转换

#### 区别：

1. 拥有length属性，其他属性（索引）为非负整数
2. 不具有数组所具备的方法
3. 类数组是一个普通对象，而真实的数组是一个Array类型

常见的类数组有: 函数的参数arugments, DOM对象列表(比如通过 document.querySelectorAll 得到的列表),jQuery 对象 (比如 $("div")).

#### 转化：

类数组可以转化为数组

```javascript
//第一种方法*
Array.prototype.slice.call(arrayLike, start);
*//第二种方法*
[...arrayLike];
*//第三种方法:*
Array.from(arrayLike);


```

​	

## 数组常见的API

####  every

```javascript
// 是否全部大于0
let a = [1,2,3,4].every(item => {
    return item > 0;
});
console.log(a); // true
```

#### some

```javascript
// 是否有部分大于3
let a = [1,2,3,4].some(item => {
    return item > 3;
});
console.log(a); // true,一旦找到对应的项，立即停止遍历数组。
```

#### filter

```javascript
const persons = [
    {name: 'Jim', age: 22},
    {name: 'Alen', age: 17},
    {name: 'Lily', age: 20}
]
 
let a = persons.filter(person => {
    return person.age > 20;
});
console.log(a)  // [{name: 'Jim', age: 22}],按条件过滤。注意：过滤结果是一个数组。

```

#### find

```javascript
const persons = [
    {id: 1, name: 'Jim', age: 22},
    {id: 2, name: 'Alen', age: 17},
    {id: 3, name: 'Lily', age: 20}
]
 
let a = persons.find(person => {
    return person.id === 2;
});
 
console.log(a) // {id: 2, name: 'Alen', age: 17}
//找出第一个符合条件的数组成员，没找到返回 undefined。

```

#### findIndex

```javascript

const persons = [
    {id: 1, name: 'Jim', age: 22},
    {id: 2, name: 'Alen', age: 17},
    {id: 3, name: 'Lily', age: 20}
]
 
let a = persons.findIndex(person => {
    return person.id === 2;
});
 
console.log(a) // 1
//找出第一个符合条件的数组成员的位置，没找到返回 -1。
```

#### include

```javascript
let a = [1,2,3].includes(3);
 
console.log(a) // true
//表示某个值是否在数组里，includes() 不接受函数参数。

```

#### map

#### reduce

#### forEach



## bind、call、apply的区别

在说区别之前还是先总结一下三者的相似之处：
1、都是用来改变函数的this对象的指向的。
2、第一个参数都是this要指向的对象。
3、都可以利用后续参数传参。

区别：

apply传递的是参数数组。

call和apply都是对函数的直接调用，而bind方法返回的仍然是一个函数，因此后面还需要()来进行调用才可以。



## new的实现原理

1. 创建一个新的对象
2. 将构造函数的作用域赋值给这个新的对象（因此this指向了这个新的对象）
3. 执行构造函数中的代码（为这个新对象添加属性）
4. 返回新对象



## 如何正确判断this

#### 全局环境：

无论是否在严格模式下，在全局执行环境中（在任何函数体外部）this 都指向全局对象。

#### 函数（运行内）环境：

1. 单调用（此调用未设置this）
   非严格模式下，this 的值默认指向全局对象。
   在严格模式下，this将保持他进入执行环境时的值。如果 this 没有被执行环境（execution context）定义，那它将保持为 undefined。
   当一个函数在其主体中使用 this 关键字时，可以通过使用函数继承自Function.prototype 的 call 或 apply 方法将 this 值绑定到调用中的特定对象。（如果传递给 this 的值不是一个对象，JavaScript 会尝试使用内部 ToObject 操作将其转换为对象。）
2. bind方法
   ES5 引入了 Function.prototype.bind。调用f.bind(someObject)会创建一个与f具有相同函数体和作用域的函数，在这个新函数中，this将永久地被绑定到了bind的第一个参数，无论此函数是如何被调用的。
3. 箭头函数
   在箭头函数中，this与封闭词法环境的this保持一致。在全局代码中，它将被设置为全局对象。
4. 作为对象的方法
   当函数作为对象里的方法被调用时，它们的 this 是调用该函数的对象。（此概念适用于原型链中的this和getter 与 setter 中的 this）
5. 作为构造函数
   当一个函数用作构造函数时（使用new关键字），它的this被绑定到正在构造的新对象。（手动返回其他对象时，则绑定到返回的这个对象上）
6. 作为一个DOM事件处理函数
   当函数被用作事件处理函数时，它的this指向触发事件的元素（一些浏览器在使用非addEventListener的函数动态添加监听函数时不遵守这个约定）。
7. 作为一个内联事件处理函数
   当代码被内联on-event 处理函数调用时，它的this指向监听器所在的DOM元素。



## 闭包

闭包就是能够读取其他函数内部变量的函数。

#### 闭包用途

1、读取函数内部的变量
2、让这些变量的值始终保持在内存中。不会调用后被自动清除。
3、方便调用上下文的局部变量。利于代码封装。

#### 缺点

1.由于闭包会使得函数中的变量都被保存在内存中，内存消耗很大，所以不能滥用闭包，否则会造成网页的性能问题，在IE中可能导致内存泄露。解决方法是，在退出函数之前，将不使用的局部变量全部删除。
2.闭包会在父函数外部，改变父函数内部变量的值。所以，如果你把父函数当作对象（object）使用，把闭包当作它的公用方法（Public Method），把内部变量当作它的私有属性（private value），这时一定要小心，不要随便改变父函数内部变量的值。



## 原型和原型链

我们创建的每个函数都有一个 prototype （原型）属性，这个属性是一个指针，这个属性是一个对象数据类型的值，指向一个原型对象，而这个原型对象中拥有的属性和方法可以被所有实例共享。

![img](https://upload-images.jianshu.io/upload_images/3174701-18a76d28c0a9ea1b?imageMogr2/auto-orient/strip|imageView2/2/w/521/format/webp)

每一个对象数据类型(普通的对象、实例、prototype......)也天生自带一个属性__proto__，属性值是当前实例所属类的原型(prototype)。原型对象中有一个属性constructor, 它指向函数对象。



其基本思想是利用原型让一个引用类型继承另一个引用类型的属性和方法。然后层层递进，就构成了实例与原型的链条，这就是所谓原型链的基本概念。

在JavaScript中，对象和对象之间也有关系，并不是孤立存在的。对象之间的继承关系，在JavaScript中是通过prototype对象指向父类对象，直到指向Object对象为止，这样就形成了一个原型指向的链条，专业术语称之为原型链。



##  prototype与_proto_的关系与区别

__proto__是每个对象都有的一个属性，而prototype是函数才会有的属性!!!
使用Object.getPrototypeOf()代替__proto__!!!



## 继承的方式和比较

1、原型链：让需要子类型原型对象等于超类型的实例。

优点：原型链很强大；

缺点：最主要的问题是如果有包含引用值类型的原型，则其属性会被所有实例共享；其次，在创建子类型的实例时，不能向超类型的构造函数中传参数。

2、借用构造函数：在子类型构造函数的内部调用超类型构造函数。

优点：可以在子类型构造函数中向超类型构造函数传递参数；

缺点：方法都在构造函数中定义，函数复用无从谈起；而且在超类型的原型中定义的方法，对子类型而言也是不可见的，结果所有类型都只能使用构造函数模式。

3、组合继承(伪经典继承)：将原型链和借用构造函数的技术组合到一块。

优点：避免了原型链和借用构造函数的缺陷，并且融合了它们的优点；

缺点：需要调用两次超类型的构造函数。

4、原型式继承：先创建一个临时性的构造函数，然后传入的对象作为这个构造函数的原型，最后返回一个临时类型的新实例。

优点：在没有必要兴师动众地创建构造函数，而只想让一个对象与另一个对象保持类似的情况，原型式继承完全可以胜任；

缺点：包含引用类型值的属性始终都会共享相应的值。

5、寄生式继承：与原型式继承紧密相关，实现与工厂模式类似，即创建一个仅用于封装继承过程的函数，该函数在内部以某种方式来增强对象，最后再像真地是它做了所有工作一样返回对象。

优点：在主要考虑对象而不是自定义类型和构造函数的情况下，有用；

缺点：不能做到函数复用。

6、寄生组合式继承：通过借用构造函数来继承属性，通过原型链的混成形式来继承方法。

优点：只调用了一次超类型的构造函数，同时原型链还能保持不变，能够正常使用instanceof和isPrototypeOf()；

缺点：暂无。



## 深拷贝与浅拷贝

#### 实现深拷贝

```javascript
function deepClone(obj){
    let objClone = Array.isArray(obj)?[]:{};
    if(obj && typeof obj==="object"){
        for(key in obj){
            if(obj.hasOwnProperty(key)){
                //判断ojb子元素是否为对象，如果是，递归复制
                if(obj[key]&&typeof obj[key] ==="object"){
                    objClone[key] = deepClone(obj[key]);
                }else{
                    //如果不是，简单复制
                    objClone[key] = obj[key];
                }
            }
        }
    }
    return objClone;
}  
//let a=[1,2,3,4],
  //  b=deepClone(a);
//a[0]=2;
//console.log(a,b);
```

```javascript
function deepClone(obj){
        objClone = JSON.parse(JSON.stringify(obj));
    return objClone
}  

```

```javascript
//解构赋值
let aa = {
    age: 18,
    name: 'aaa',
    address: {
        city: 'shanghai'
    }
}

let bb = {
    ...aa,
    address: {...aa.address}
};

bb.address.city = 'shenzhen';

console.log(aa.address.city);  // shanghai
```



## 防抖和节流

#### 防抖：

**所谓防抖，就是指触发事件后在 n 秒内函数只能执行一次，如果在 n 秒内又触发了事件，则会重新计算函数执行时间。**

#### **节流：**

**所谓节流，就是指连续触发事件但是在 n 秒中只执行一次函数。**





##  作用域和作用域链、执行期上下文

#### 作用域

作用域就是变量和函数的可访问范围，控制着变量和函数的可见性与生命周期，换句话说，作用域决定了代码区块中变量和其他资源的可见性。在JavaScript中变量的作用域有全局作用域和局部作用域。JavaScript采用词法作用域(lexical scoping)，也就是静态作用域。

#### 作用域链

#### 执行期上下文

作用域(scope) 是指变量的可访问性，上下文(context)是指this在同一作用域内的值。我们也可以使用call()、apply()、bind()、箭头函数等改变上下文。在浏览器中在全局作用域(scope)中上下文中始终是Window对象。在Node.js中在全局作用域(scope)中上下文中始终是Global 对象。



## DOM常见操作

1.查找节点

document.getElementById('id属性值'); 返回拥有指定id的第一个对象的引用

document/element.getElementsByClassName('class属性值'); 返回拥有指定class的对象集合

document/element.getElementsByTagName('标签名'); 返回拥有指定标签名的对象集合

document.getElementsByName('name属性值'); 返回拥有指定名称的对象结合

document/element.querySelector('CSS选择器'); 仅返回第一个匹配的元素

document/element.querySelectorAll('CSS选择器'); 返回所有匹配的元素

document.documentElement; 获取页面中的HTML标签

document.body; 获取页面中的BODY标签

document.all['']; 获取页面中的所有元素节点的对象集合型

2.创建节点

document.createElement('元素名'); 创建新的元素节点

document.createAttribute('属性名'); 创建新的属性节点

document.createTextNode('文本内容'); 创建新的文本节点

document.createComment('注释节点'); 创建新的注释节点

document.createDocumentFragment( ); 创建文档片段节点

3.删除节点

parentNode.removeChild( existingChild );删除已有的子节点，返回值为删除节点

element.removeAttribute('属性名');删除具有指定属性名称的属性，无返回值

element.removeAttributeNode( attrNode );删除指定属性，返回值为删除的属性

4.修改节点

parentNode.replaceChild( newChild, existingChild );用新节点替换父节点中已有的子节点

element.setAttributeNode( attributeName );若原元素已有该节点，此操作能达到修改该属性值的目的

element.setAttribute( attributeName, attributeValue );若原元素已有该节点，此操作能达到修改该属性值的目的

5.插入节点

parent.appendChild( element/txt/comment/fragment );向父节点的最后一个子节点后追加新节点

parent.insertBefore( newChild, existingChild );向父节点的某个特定子节点之前插入新节点

element.setAttributeNode( attributeName );给元素增加属性节点

element.setAttribute( attributeName, attributeValue );给元素增加指定属性，并设定属性值

6.设置样式

ele.style.styleName = styleValue;设置ele元素的CSS样式



##  Ajax的请求过程

**Ajax 是一种异步请求数据的一种技术，对于改善用户的体验和程序的性能很有帮助。**

```html
    (1)创建`XMLHttpRequest`对象,也就是创建一个异步调用对象.

    (2)创建一个新的`HTTP`请求,并指定该`HTTP`请求的方法、`URL`及验证信息.

    (3)设置响应`HTTP`请求状态变化的函数.

    (4)发送`HTTP`请求.

    (5)获取异步调用返回的数据.

    (6)使用JavaScript和DOM实现局部刷新.
```



## JS的垃圾回收机制

#### 变量的生命周期

当一个变量的生命周期结束之后它所指向的内存就应该被释放。局部变量的生命周期在函数执行过后就结束了，此时便可将它引用的内存释放（即垃圾回收），但全局变量生命周期会持续到浏览器关闭页面。

#### JS垃圾回收方式

JS执行环境中的垃圾回收器怎样才能检测哪块内存可以被回收有两种方式：标记清除（mark and sweep）、引用计数(reference counting)。

#### 标记清除（mark and sweep）

大部分浏览器以此方式进行垃圾回收，当变量进入执行环境（函数中声明变量）的时候，垃圾回收器将其标记为“进入环境”，当变量离开环境的时候（函数执行结束）将其标记为“离开环境”，在离开环境之后还有的变量则是需要被删除的变量。

垃圾收集器给内存中的所有变量都加上标记，然后**去掉环境中的变量以及被环境中的变量引用的变量的标记**。在此之后再被加上的标记的变量即为需要回收的变量，因为环境中的变量已经无法访问到这些变量。

#### 引用计数(reference counting)

这种方式常常会引起内存泄漏，低版本的IE使用这种方式。机制就是跟踪一个值的引用次数，当声明一个变量并将一个引用类型赋值给该变量时该值引用次数加1，当这个变量指向其他一个时该值的引用次数便减一。当该值引用次数为0时就会被回收。



## addEventListener和onClick()的区别

#### onclick

优点： 
- 简洁 
- 处理事件的this关键字指向当前元素 
缺点： 
- 不能对事件捕获或事件冒泡进行控制，只能使用事件冒泡，无法切换成事件捕获 
- 一次只能对一个元素绑定一个事件处理程序，当使用window.onload属性时，会覆盖采用相同方法所绑定的事件代码

#### addEventListener

优点： 
- 可以支持事件处理的捕获阶段，也可以支持时间处理的冒泡阶段，两个阶段都是通过addEventListener最后一个参数设置为false(默认值，表示事件冒泡)或者true(表示事件捕获)来切换 
- 事件处理 this与onclick一样 
- 事件处理函数中，event对象总是作为第一个可用参数 
- 你可以为某个元素绑定多个事件而不会覆盖之前绑定的处理程序 （按照顺序执行） 
缺点： 
- IE8以下不支持



## new和Object.create的区别

| 比较     | new                     | Object.create           |
| -------- | ----------------------- | ----------------------- |
| 构造函数 | 保留原构造函数属性      | 丢失原构造函数属性      |
| 原型链   | 原构造函数prototype属性 | 原构造函数/（对象）本身 |
| 作用对象 | function                | function和object        |

使用`create`创建的对象，没有任何属性，显示`No properties`，我们可以把它当作一个非常**纯净**的map来使用，我们可以自己定义`hasOwnProperty`、`toString`方法，不管是有意还是不小心，我们完全不必担心会将原型链上的同名方法覆盖掉。

使用`for..in`循环的时候会遍历对象原型链上的属性，使用`create(null)`就不必再对属性进行检查了，当然，我们也可以直接使用`Object.keys[]`。

**总结：**

1. 你需要一个非常干净且高度可定制的对象当作数据字典的时候；
2. 想节省`hasOwnProperty`带来的一丢丢性能损失并且可以偷懒少些一点代码的时候



## location对象

Location 对象包含有关当前 URL 的信息。

Location 对象是 Window 对象的一个部分，可通过 window.location 属性来访问。

https://www.jianshu.com/p/bd0866de3621





## 浏览器从输入URL到页面渲染的整个流程

https://blog.csdn.net/sinat_23880167/article/details/78882766



## 跨域、同源策略及跨域实现方式和原理

![img](https://img2018.cnblogs.com/blog/1726543/201907/1726543-20190704090704027-953668455.png)





## 浏览器的回流（Reflow）和重绘（Repaints）

1. 当render tree中的一部分(或全部)因为元素的规模尺寸，布局，隐藏等改变而需要重新构建。这就称为回流。每个页面至少需要一次回流，就是在页面第一次加载的时候。
2. 当render tree中的一些元素需要更新属性，而这些属性只是影响元素的外观，风格，而不会影响布局的，比如background-color。则就叫称为重绘。

注：回流必将引起重绘，而重绘不一定会引起回流。

 一次的dom更改或者css几何属性更改，都会引起一次浏览器的重排/重绘过程，而如果是css的非几何属性更改，则只会引起重绘过程。

**触发重排：**

（1）页面第一次渲染：在页面发生首次渲染的时候，所有组件都要进行首次布局，这是开销最大的一次重排

（2）浏览器窗口尺寸改变

（3）元素位置和尺寸（宽、高、内外边距、边框等）发生改变的时候

（4）增加或删除DOM节点

（5）内容发生改变（文字数量或图片大小等等）

（6）元素字体大小变化

（7）激活CSS伪类（例如：:hover） 

（8）增加或修改样式，设置style属性

（9）查询某些属性或调用某些方法，如：调用getComputedStyle方法，或者IE里的currentStyle时，也会触发重排

（10）display:none（重排并重绘）

**触发重绘：**

（1）visibility

（2）outline

（3）背景颜色：color、background-color

（4）visibility:hidden（重排）



##  JavaScript中的arguments

argument是JavaScript中的一个关键字，用于指向调用者传入的所有参数。即使不定义参数，也可以取到调用者的参数。

https://www.cnblogs.com/lcr-smg/p/10065877.html



##  EventLoop事件循环

https://www.cnblogs.com/hanzhecheng/p/9046144.html

**第一轮：宏任务的同步代码，微任务的同步代码（promise的then)**

**第二轮：宏任务的异步代码，微任务**

宏任务一般是：包括整体代码script，setTimeout，setInterval。

微任务：Promise，process.nextTick。



##  JavaScript中常用的BOM对象（属性、方法）

1. #### window对象

   1. 定义：

      1. 一个浏览器窗口实例
      2. 与窗口有关的信息（应用程序编程接口）　　
      3. ECMAScript规定的Global对象

   2. 方法

      1. open（url）,返回标识符 引用 即将打开窗口的。（**调用该引用对象的close方法 即可关闭该窗口**）

      2. 间歇调用setInterval（函数，time）。**clearInterval（）**

      3. 超时调用 setTimeout（函数，time）;**表示在多久后把代码注入消息队列（如果队列是空的那么会立即执行，否则等待前面的代码执行完毕后再执行） clearTimeout（）**

      4.  

         系统对话框

         1. alert（字符串）
         2. confirm（表示提示的文字）；**返回** **true / false** 
         3. prompt （提示文字信息，提前键入的文字）；**返回输入的信息 或者** **null**

2. #### location对象

   1. 定义：　　

      1. 保存着与当前文档有关的信息。
      2. 将URL解析为独立的片段方便开发者 进行访问。
      3.  **window.location === document.location**

   2. 方法

      1. location.assign（新url）,打开新url,并在记录中创建一条新记录
      2.  location.reload（true/false）：刷新当前页面.
      3. location.replace（url）：用传入的url代替当前记录的url，不在记录中创建新的记录。
      4. **window.location = 新url、location.href = 新url  与 location.assign（新url）效果一样**

   3. #### 属性

      1.  href：完整的url
      2.   host：主机或域名
      3.   hostname：返回不带端口号的主机或域名。
      4.   pathname:返回url中的目录和文件名。
      5.   hash:返回hash值（‘#target’）
      6.   search：返回查询字符串（‘？name=fafa&sex="mae"’）

3. #### history对象

   1.  定义：保存着用户上网的历史记录。
   2.  方法：
      1. go（数字）
         1. 数字：**数字 -1 页面后退一个记录，+1前进一个记录**　
      2. back（）:后退一个记录
      3. forward（）：前进一个记录



## JS的map()和reduce()方法

**map**是映射的意思，即原数组被映射成新的数组，而这个数组是由原数组中的每个元素调用一个特定的方法返回值组成的新数组。

```javascript
var arr1 = [1, 2, 3, 4, 5, 6];
var arr11 = arr1.map(x => {
    return x * x;
});
console.log(arr11);

//将数组中的数字转化为字符串
var arr2 = [1, 2, 3, 4, 5];
var arr22 = arr2.map(String);
//console.log(arr22);
```

**reduce（）方法** 把函数执行后的结果再进行累加执行，这个函数必须接收两个参数，第一个参数是一个callback，用于针对数组项的操作；第二个参数则是传入的初始值，这个初始值用于单个数组项的操作。reduce()把结果继续和序列的下一个元素做累积计算。最终计算出一个值。

```javascript
// 利用 reduce进行数组求和 

var arr3 = [1, 2, 3, 4, 5, 6];
var arr33 = arr3.reduce((x, y) => {
    return x + y;
})
console.log(arr33);
```



## “==”和“===”的区别

当进行双等号比较时候： 先检查两个操作数数据类型，如果相同， 则进行===比较， 如果不同， 则愿意为你进行一次类型转换， 转换成相同类型后再进行比较， 而===比较时， 如果类型不同，直接就是false.



## setTimeout用作倒计时为何会产生误差？

定时器是属于 **宏任务(macrotask)** 。如果当前 **执行栈** 所花费的时间大于 **定时器** 时间，那么定时器的回调在 **宏任务(macrotask)** 里，来不及去调用，所有这个时间会有误差。



## 强制缓存和协商缓存

| 缓存     | 获取资源形式 | 状态吗              | 发送请求到服务器                     |
| -------- | ------------ | ------------------- | ------------------------------------ |
| 强缓存   | 从缓存取     | 200（from cache）   | 否，直接从缓存取                     |
| 协商缓存 | 从缓存取     | 304（not modified） | 是，通过服务器告知浏览器缓存是否可用 |



## 解构赋值

```javascript
let aa = {
    age: 18,
    name: 'aaa',
    address: {
        city: 'shanghai'
    }
}

let bb = {
    ...aa,
    address: {...aa.address}
};

bb.address.city = 'shenzhen';

console.log(aa.address.city);  // shanghai
```



## eval

```javascript
//实现数组求和
var arr=[1,2,3];
console.log(eval(arr.join('+')))  //6
```



## URL地址转化为对象

```javascript
let str = "http://localhost:3000/index.html？phone=12345678901&pwd=123123";
let arr = str.split("?")[1].split("&");   //先通过？分解得到？后面的所需字符串，再将其通过&分解开存放在数组里
let obj = {};
for (let i of arr) {
  obj[i.split("=")[0]] = i.split("=")[1];  //对数组每项用=分解开，=前为对象属性名，=后为属性值
}
console.log(obj);
```

