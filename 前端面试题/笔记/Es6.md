## let、const和var的概念与区别

**一、var声明的变量会挂载在window上，而let和const声明的变量不会：**

```javascript
var a = 100;console.log(a,window.a);    // 100 100
```

**二、var声明变量存在变量提升，let和const不存在变量提升**

**三、let和const声明形成块作用域**

**四、同一作用域下let和const不能声明同名变量，而var可以**

**五、暂时性死区：**

**只要块级作用域内存在let，const命令，它所声明的变量就“绑定”（binding）这个区域，不再受外部的影响。**

**六、const：**

```
1、一旦声明必须赋值,不能使用null占位。
```

**2、声明后不能再修改**

```
2、声明后不能再修改
```

```
3、如果声明的是复合类型数据，可以修改其属性
```



## 变量提升与暂时性死区

如果区块中存在let和const命令，这个区块对这些命令声明的变量，从一开始就形成了封闭作用域。凡是在声明之前就使用这些变量，就会报错。

```javascript
if (true) {
  // TDZ开始
  tmp = 'abc'; // ReferenceError
  console.log(tmp); // ReferenceError

  let tmp; // TDZ结束
  console.log(tmp); // undefined

  tmp = 123;
  console.log(tmp); // 123
}
```



## 变量的结构赋值

#### 数组的解构赋值

```javascript
let arr = [0,1,2]
let [a,b,c] = arr
console.log(a) // 0
console.log(b) // 1
console.log(c) // 2

let arr = [,1,2]
let [a='我是默认值',b,c] = arr
console.log(a) // '我是默认值'
console.log(b) // 1
console.log(c) // 2

let a = [0,1,2]
let b = [3,4,5]
let c = a.concat(b)
console.log(c) // [0,1,2,3,4,5]

//组合数组
let d = [...a,...b]
console.log(d) // [0,1,2,3,4,5]

//数组的克隆
let a = [0,1,2,3]
let b = a
b.push(4)
console.log(a) // [0,1,2,3,4]
console.log(b) // [0,1,2,3,4]
//因为这只是简单的把引用地址赋值给b，而不是重新开辟一个内存地址，所以a和b共享了同一个内存地址，该内存地址的更改，会影响到所有引用该地址的变量那么用下面的方法，把数组进行克隆一份，互不影响.
let a=[0,1,2,3]
let b=[...a]
b.push(4)
console.log(a)  //[0,1,2,3]
console.log(b)  //[0,1,2,3,4]
```

#### 对象的解构赋值

对象的解构赋值和数组的解构赋值其实类似，但是数组的数组成员是有序的
而对象的属性则是无序的，所以对象的解构赋值简单理解是等号的左边和右边的结构相同

```javascript
let {name,age} = {name:"swr",age:28}
console.log(name) // 'swr'
console.log(age) // 28

// 这里可以看出，左侧的name和右侧的name，是互相匹配的key值
// 而左侧的name匹配完成后，再赋值给真正需要赋值的Name
let { name:Name,age } = { name:'swr',age:28 }
console.log(Name) // 'swr'
console.log(age) // 28

//变量已经声明的情况
let name,age
// 需要用圆括号，包裹起来
({name,age} = {name:"swr",age:28})
console.log(name) // 'swr'
console.log(age) // 2

//变量也能设置默认值
let {name="swr",age} = {age:28}
console.log(name) // 'swr'
console.log(age) // 28
// 这里规则和数组的解构赋值一样，当name = undefined时，则会使用默认值

let [a] = [{name:"swr",age:28}]
console.log(a) // {name:"swr",age:28}

let { length } = "hello swr"
console.log(length) // 9


```

#### 扩展运算符

```javascript
我们先看下代码，在以往，我们给函数传不确定参数数量时，是通过arguments来获取的
function sum() {
  console.log(arguments) // { '0': 1, '1': 2, '2': 3, '3': 4, '4': 5, '5': 6 }
                         // 我们可以看出，arguments不是一个数组，而是一个伪数组
  let total = 0
  let { length } = arguments
  for(let i = 0;i < length;i++){
    total += arguments[i]
  }
  return total
}

console.log(sum(1,2,3,4,5,6)) // 21

//接下来用扩展运算符
function sum(...args){ // 使用...扩展运算符
    console.log(args) // [ 1, 2, 3, 4, 5, 6 ] args是一个数组
    return eval(args.join('+'))
}
console.log(sum(1,2,3,4,5,6)) // 21


//要注意的一点
// 正确的写法 扩展运算符只能放在最后一个参数
function sum(a,b,...args){
    console.log(a) // 1
    console.log(b) // 2
    console.log(args) // [ 3, 4, 5, 6 ]
}

sum(1,2,3,4,5,6)


```

#### 扩展运算符的方便之处

```javascript
// 以往我们是这样拼接数组的
let arr1 = [1,2,3]
let arr2 = [4,5,6]
let arr3 = arr1.concat(arr2)
console.log(arr3) // [ 1, 2, 3, 4, 5, 6 ]
// 现在我们用扩展运算符看看
let arr1 = [1,2,3]
let arr2 = [4,5,6]
let arr3 = [...arr1,...arr2]
console.log(arr3) // [ 1, 2, 3, 4, 5, 6 ]
```

```javascript
// 以往我们这样来取数组中最大的值
function max(...args){
    return Math.max.apply(null,args)
}
console.log(max(1,2,3,4,5,6)) // 6

// 现在我们用扩展运算符看看
function max(...args){
    return Math.max(...args) // 把args [1,2,3,4,5,6]展开为1,2,3,4,5,6
}
console.log(max(1,2,3,4,5,6)) // 6
```

```jsx
// 扩展运算符可以把argument转为数组
function max(){
    console.log(arguments) // { '0': 1, '1': 2, '2': 3, '3': 4, '4': 5, '5': 6 }
    let arr = [...arguments]
    console.log(arr) // [1,2,3,4,5,6]
}

max(1,2,3,4,5,6)

// 但是扩展运算符不能把伪数组转为数组（除了有迭代器iterator的伪数组，如arguments）
let likeArr = { "0":1,"1":2,"length":2 }
let arr = [...likeArr] // 报错 TypeError: likeArr is not iterable

// 但是可以用Array.from把伪数组转为数组
let likeArr = { "0":1,"1":2,"length":2 }
let arr = Array.from(likeArr)
console.log(arr) // [1,2]

```

#### 对象使用扩展运算符

```javascript
// 以往我们这样合并对象
let name = { name:"邵威儒" }
let age = { age:28 }
let person = {}
Object.assign(person,name,age)
console.log(person) // { name: '邵威儒', age: 28 }

// 使用扩展运算符
let name = { name:"邵威儒" }
let age = { age:28 }
let person = {...name,...age}
console.log(person) // { name: '邵威儒', age: 28 }
```

需要注意的是，通过扩展运算符和Object.assign对对象进行合并的行为，是属于**浅拷贝**，那么我们在开发当中，经常需要对对象进行**深拷贝**，接下来我们看看如何进行**深拷贝**。

**方法一：利用JSON.stringify和JSON.parse**

```javascript
let swr = {
    name:"邵威儒",
    age:28,
    pets:['小黄']
}

let swrcopy = JSON.parse(JSON.stringify(swr))
console.log(swrcopy) // { name: '邵威儒', age: 28, pets: [ '小黄' ] }
// 此时我们新增swr的属性
swr.pets.push('旺财')
console.log(swr) // { name: '邵威儒', age: 28, pets: [ '小黄', '旺财' ] }
// 但是swrcopy却不会受swr影响
console.log(swrcopy) // { name: '邵威儒', age: 28, pets: [ '小黄' ] }
这种方式进行深拷贝，只针对json数据这样的键值对有效
对于函数等等反而无效，不好用，接着继续看方法二、三。
```



## Symbol概念及其作用

ES6 引入了一种新的原始数据类型Symbol，表示**独一无二**的值.

`Symbol`是一种基础数据类型，所以当我们使用`typeof`去检查它的类型的时候，它会返回一个属于自己的类型。

每个Symbol实例都是唯一的。因此，当你比较两个Symbol实例的时候，将总会返回`false`

```javascript
let s1 = Symbol()
let s2 = Symbol('another symbol')
let s3 = Symbol('another symbol')
 
s1 === s2 // false
s2 === s3 // false
```



```javascript
let obj = {
   [Symbol('name')]: '一斤代码',
   age: 18,
   title: 'Engineer'
}
 
Object.keys(obj)   // ['age', 'title']
 
for (let p in obj) {
   console.log(p)   // 分别会输出：'age' 和 'title'
}
 
Object.getOwnPropertyNames(obj)   // ['age', 'title']
```

由上代码可知，Symbol类型的key是不能通过`Object.keys()`或者`for...in`来枚举的，它未被包含在对象自身的属性名集合(property names)之中。所以，利用该特性，我们可以把一些不需要对外操作和访问的属性使用Symbol来定义。

也正因为这样一个特性，当使用`JSON.stringify()`将对象转换成JSON字符串的时候，Symbol属性也会被排除在输出内容之外：

```javascript
JSON.stringify(obj)  // {"age":18,"title":"Engineer"}
```

获取symbol的一些API

```javascript
// 使用Object的API
Object.getOwnPropertySymbols(obj) // [Symbol(name)]
 
// 使用新增的反射API
Reflect.ownKeys(obj) // [Symbol(name), 'age', 'title']
```



##  Set和Map数据结构

#### Set

新的数据结构 Set。它类似于数组，但是成员的值都是唯一的，没有重复的值。

用set完成数组去重

```javascript
 const s = new Set();
 [2, 3, 5, 4, 5, 2, 2].forEach(x => s.add(x)); //此时set为{2，3，5，4}
 for (let i of s) {
           console.log(i);
 }
 // 2 3 5 4

Array.from方法可以将 Set 结构转为数组。
 const items = new Set([1, 2, 3, 4, 5]);
 const array = Array.from(items);

数组去重
 function dedupe(array) {
   return Array.from(new Set(array));
 }
 dedupe([1, 1, 2, 3]) // [1, 2, 3]

```

**遍历操作**

Set 结构的实例有四个遍历方法，可以用于遍历成员。

- `keys()`：返回键名的遍历器
- `values()`：返回键值的遍历器
- `entries()`：返回键值对的遍历器
- `forEach()`：使用回调函数遍历每个成员

```javascript
set = new Set([1, 4, 9]);
 set.forEach((value, key) => console.log(key + ' : ' + value))
 // 1 : 1
 // 4 : 4
 // 9 : 9
```



#### Map

由于对象只接受字符串作为键名,为了解决这个问题，ES6 提供了 Map 数据结构。

它类似于对象，也是键值对的集合，但是“键”的范围不限于字符串，各种类型的值（包括对象）都可以当作键。也就是说，Object 结构提供了“字符串—值”的对应，Map 结构提供了“值—值”的对应.

```javascript
const m = new Map();
const o = {p: 'Hello World'};

m.set(o, 'content')
m.get(o) // "content"

m.has(o) // true
m.delete(o) // true
m.has(o) // false
```

```javascript
const map = new Map([
  ['name', '张三'],
  ['title', 'Author']
]);

map.size // 2
map.has('name') // true
map.get('name') // "张三"
map.has('title') // true
map.get('title') // "Author"
```

注意，只有对同一个对象的引用，Map 结构才将其视为同一个键。这一点要非常小心。

```javascript
const map = new Map();
 
 map.set(['a'], 555);
 map.get(['a']) // undefined
//上面代码的set和get方法，表面是针对同一个键，但实际上这是两个值，内存地址是不一样的，因此get方法无法读取该键，返回undefined。
```



## promise

#### promise的三种状态

- pending（进行中）
- fulfilled（已成功）
- rejected（已失败）

resolve(已定型)

**Promise 不论成功或失败都会调用 then 然而catch() 只有当 promise 失败时才会调用**所以当失败的时候既执行了then又执行了catch，只不过reject只会将参数传递给catch方法,并不传递then方法所以顺序写反失败后then就输出了undefined，而catch是正常输出结果



`Promise`也有一些缺点。首先，无法取消`Promise`，一旦新建它就会立即执行，无法中途取消。其次，如果不设置回调函数，`Promise`内部抛出的错误，不会反应到外部。第三，当处于`pending`状态时，无法得知目前进展到哪一个阶段（刚刚开始还是即将完成）。



#### promise实例

```javascript
const promise = new Promise(function(resolve, reject) {
  // ... some code

  if (/* 异步操作成功 */){
    resolve(value);
  } else {
    reject(error);
  }
});
```

#### then方法

`Promise`实例生成以后，可以用`then`方法分别指定`resolved`状态和`rejected`状态的回调函数。

```javascript
promise.then(function(value) {
  // success
}, function(error) {
  // failure
});
```

`then`方法可以接受两个回调函数作为参数。第一个回调函数是`Promise`对象的状态变为`resolved`时调用，第二个回调函数是`Promise`对象的状态变为`rejected`时调用。其中，第二个函数是可选的，不一定要提供。这两个函数都接受`Promise`对象传出的值作为参数。



Promise 新建后就会立即执行。

```javascript
let promise = new Promise(function(resolve, reject) {
  console.log('Promise');
  resolve();
});

promise.then(function() {
  console.log('resolved.');
});

console.log('Hi!');

// Promise
// Hi!
// resolved
```

上面代码中，Promise 新建后立即执行，所以首先输出的是`Promise`。然后，`then`方法指定的回调函数，将在当前脚本所有同步任务执行完才会执行，所以`resolved`最后输出。

#### 一些API

- `Promise.all`

`Promise.all`方法用于将多个 Promise 实例，包装成一个新的 Promise 实例。

- `Promise.race`

`Promise.race`方法同样是将多个 Promise 实例，包装成一个新的 Promise 实例。



## Iterator和for...of（Iterator遍历器的实现）

遍历器（Iterator）就是这样一种机制。它是一种接口，为各种不同的数据结构提供统一的访问机制。任何数据结构只要部署 Iterator 接口，就可以完成遍历操作（即依次处理该数据结构的所有成员）。

Iterator 的作用有三个：一是为各种数据结构，提供一个统一的、简便的访问接口；二是使得数据结构的成员能够按某种次序排列；三是 ES6 创造了一种新的遍历命令`for...of`循环，Iterator 接口主要供`for...of`消费。



#### for ...of

JavaScript 原有的`for...in`循环，只能获得对象的键名，不能直接获取键值。ES6 提供`for...of`循环，允许遍历获得键值。

```javascript
var arr = ['a', 'b', 'c', 'd'];

for (let a in arr) {
  console.log(a); // 0 1 2 3
}

for (let a of arr) {
  console.log(a); // a b c d
}
```

`for...of`循环调用遍历器接口，数组的遍历器接口只返回具有数字索引的属性。这一点跟`for...in`循环也不一样。

```javascript
let arr = [3, 5, 7];
arr.foo = 'hello';

for (let i in arr) {
  console.log(i); // "0", "1", "2", "foo"
}

for (let i of arr) {
  console.log(i); //  "3", "5", "7"
}
//上面代码中，for...of循环不会返回数组arr的foo属性。
```



Set 和 Map 结构也原生具有 Iterator 接口，可以直接使用`for...of`循环。

```javascript
var engines = new Set(["Gecko", "Trident", "Webkit", "Webkit"]);
for (var e of engines) {
  console.log(e);
}
// Gecko
// Trident
// Webkit

var es6 = new Map();
es6.set("edition", 6);
es6.set("committee", "TC39");
es6.set("standard", "ECMA-262");
for (var [name, value] of es6) {
  console.log(name + ": " + value);
}
// edition: 6
// committee: TC39
// standard: ECMA-262
```



## 循环语法比较及使用场景（for、forEach、for...in、for...of）

**forEach:**无法中途跳出`forEach`循环，`break`命令或`return`命令都不能奏效。

**for...in:**可以遍历数组的键名，但会以字符串命名。主要是为遍历对象而设计的，不适用于遍历数组。

**for...of:**

- 有着同`for...in`一样的简洁语法，但是没有`for...in`那些缺点。
- 不同于`forEach`方法，它可以与`break`、`continue`和`return`配合使用。
- 提供了遍历所有数据结构的统一操作接口。



## Generator及其异步方面的应用

Generator 函数是一个普通函数，但是有两个特征。一是，`function`关键字与函数名之间有一个星号；二是，函数体内部使用`yield`表达式，定义不同的内部状态（`yield`在英语里的意思就是“产出”）。

```javascript
function* helloWorldGenerator() {
  yield 'hello';
  yield 'world';
  return 'ending';
}

var hw = helloWorldGenerator();
```

   

ES6 诞生以前，异步编程的方法，大概有下面四种。

- 回调函数
- 事件监听
- 发布/订阅
- Promise 对象

```javascript
function* asyncJob() {
  // ...其他代码
  var f = yield readFile(fileA);
  // ...其他代码
}
```

上面代码的函数`asyncJob`是一个协程，它的奥妙就在其中的`yield`命令。它表示执行到此处，执行权将交给其他协程。也就是说，`yield`命令是异步两个阶段的分界线。

协程遇到`yield`命令就暂停，等到执行权返回，再从暂停的地方继续往后执行。它的最大优点，就是代码的写法非常像同步操作，如果去除`yield`命令，简直一模一样。



## async函数

前文有一个 Generator 函数，依次读取两个文件。

```javascript
const fs = require('fs');

const readFile = function (fileName) {
  return new Promise(function (resolve, reject) {
    fs.readFile(fileName, function(error, data) {
      if (error) return reject(error);
      resolve(data);
    });
  });
};

const gen = function* () {
  const f1 = yield readFile('/etc/fstab');
  const f2 = yield readFile('/etc/shells');
  console.log(f1.toString());
  console.log(f2.toString());
};
```

上面代码的函数`gen`可以写成`async`函数，就是下面这样。

```javascript
const asyncReadFile = async function () {
  const f1 = await readFile('/etc/fstab');
  const f2 = await readFile('/etc/shells');
  console.log(f1.toString());
  console.log(f2.toString());
};
```

一比较就会发现，`async`函数就是将 Generator 函数的星号（`*`）替换成`async`，将`yield`替换成`await`，仅此而已。



`async`函数对 Generator 函数的改进，体现在以下四点。

（1）内置执行器。

Generator 函数的执行必须靠执行器，所以才有了`co`模块，而`async`函数自带执行器。也就是说，`async`函数的执行，与普通函数一模一样，只要一行。

```javascript
asyncReadFile();
```

上面的代码调用了`asyncReadFile`函数，然后它就会自动执行，输出最后结果。这完全不像 Generator 函数，需要调用`next`方法，或者用`co`模块，才能真正执行，得到最后结果。

（2）更好的语义。

`async`和`await`，比起星号和`yield`，语义更清楚了。`async`表示函数里有异步操作，`await`表示紧跟在后面的表达式需要等待结果。

（3）更广的适用性。

`co`模块约定，`yield`命令后面只能是 Thunk 函数或 Promise 对象，而`async`函数的`await`命令后面，可以是 Promise 对象和原始类型的值（数值、字符串和布尔值，但这时会自动转成立即 resolved 的 Promise 对象）。

（4）返回值是 Promise。

`async`函数的返回值是 Promise 对象，这比 Generator 函数的返回值是 Iterator 对象方便多了。你可以用`then`方法指定下一步的操作。

进一步说，`async`函数完全可以看作多个异步操作，包装成的一个 Promise 对象，而`await`命令就是内部`then`命令的语法糖。





## 几种异步方式的比较

虽然 **Promise** 的写法比回调函数的写法大大改进，但是一眼看上去，代码完全都是 Promise 的 API（`then`、`catch`等等），操作本身的语义反而不容易看出来。



**Generator：**必须有一个任务运行器，自动执行 Generator 函数

 Generator 函数的写法。

```javascript
function chainAnimationsGenerator(elem, animations) {

  return spawn(function*() {
    let ret = null;
    try {
      for(let anim of animations) {
        ret = yield anim(elem);
      }
    } catch(e) {
      /* 忽略错误，继续执行 */
    }
    return ret;
  });

}
```

必须有一个任务运行器，自动执行 Generator 函数，它返回一个 Promise 对象，而且必须保证`yield`语句后面的表达式，必须返回一个 Promise。

最后是 async 函数的写法。

```javascript
async function chainAnimationsAsync(elem, animations) {
  let ret = null;
  try {
    for(let anim of animations) {
      ret = await anim(elem);
    }
  } catch(e) {
    /* 忽略错误，继续执行 */
  }
  return ret;
}
```

可以看到 Async 函数的实现最简洁，最符合语义，几乎没有语义不相关的代码。它将 Generator 写法中的自动执行器，改在语言层面提供，不暴露给用户，因此代码量最少。如果使用 Generator 写法，自动执行器需要用户自己提供。



## class语法

JavaScript 语言中，生成实例对象的传统方法是通过构造函数。下面是一个例子。

```javascript
function Point(x, y) {
  this.x = x;
  this.y = y;
}

Point.prototype.toString = function () {
  return '(' + this.x + ', ' + this.y + ')';
};

var p = new Point(1, 2);
```



ES6 提供了更接近传统语言的写法，引入了 Class（类）这个概念，作为对象的模板。通过`class`关键字，可以定义类。

基本上，ES6 的`class`可以看作只是一个语法糖，它的绝大部分功能，ES5 都可以做到，新的`class`写法只是让对象原型的写法更加清晰、更像面向对象编程的语法而已。上面的代码用 ES6 的`class`改写，就是下面这样。

```javascript
class Point {
  constructor(x, y) {
    this.x = x;
    this.y = y;
  }

  toString() {
    return '(' + this.x + ', ' + this.y + ')';
  }
}
```

上面代码定义了一个“类”，可以看到里面有一个`constructor`方法，这就是构造方法，而`this`关键字则代表实例对象。也就是说，ES5 的构造函数`Point`，对应 ES6 的`Point`类的构造方法。

`Point`类除了构造方法，还定义了一个`toString`方法。注意，定义“类”的方法的时候，前面不需要加上`function`这个关键字，直接把函数定义放进去了就可以了。另外，方法之间不需要逗号分隔，加了会报错。

ES6 的类，完全可以看作构造函数的另一种写法。



## 模块加载方案比较（CommonJS和ES6的Module）

- CommonJS 模块输出的是一个值的拷贝，ES6 模块输出的是值的引用。
- CommonJS 模块是运行时加载，ES6 模块是编译时输出接口。



##  **Es6中箭头函数与普通函数的区别？**

普通function的声明在变量提升中是最高的，箭头函数没有函数提升

箭头函数没有属于自己的this，arguments

箭头函数不能作为构造函数，不能被new，没有property

call和apply方法只有参数，没有作用域

不可以使用 yield 命令，因此箭头函数不能用作 Generator 函数

不可以使用 new 命令，因为：没有自己的 this，无法调用 call，apply

​                                                    没有 prototype 属性 ，而 new 命令在执行时需要将构造函数的 prototype 赋值给新的对象的 `__proto__`



## Symbol

- 主要防止了键名的冲突，两个symbol不相等，包括==和===。 
- symbol不可以和其他类型的值进行运算。但是可以转换为布尔值(默认true)。 
- 调用toString方法，返回symbol对象。 
- 无法被for in. for of 比那里，也不会被Object.keys()返回。



##  Promise.all()和Promise.race() 

- Promise.all(),参数是一个数组，每个数组里面是Promise对象，当数组所有的promise对象都fullfilled，然后返回每个pormise的resolve的数据。 
- Promise.race(),参数也是一个数组，每个数组是Promise对象，当有一个Promise对象resolve了，然后便执行，返回第一个resolve的数据。