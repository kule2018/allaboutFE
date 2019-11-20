##### 作用

 export和export default实现的功能相同，即：可用于导出（暴露）常量、函数、文件、模块等，以便其他文件调用。 

##### 区别

1.export导出多个对象，export default只能导出一个。

2.export导出对象需要用{ }，export default不需要{ }，如：

```javascript
export {A,B,C};

export default A;
```

3.

(1) 输出单个值，使用export default

(2)输出多个值，使用export

(3)export default和普通的export不要同时使用。

```javascript
1.export
//a.js
export const str = "blablabla~";
export function log(sth) { 
  return sth;
}

对应的导入方式：
//b.js
import { str, log } from 'a'; //也可以分开写两次，导入的时候带花括号

2.export default
//a.js
const str = "blablabla~";
export default str;
其实此处相当于为str变量值"blablabla"起了一个系统默认的变量名default，自然default只能有一个值，所以一个文件内不能有多个export default。

对应的导入方式： 
//b.js 
import str from 'a'; //导入的时候没有花括号

本质上，a.js文件的export default输出一个叫做default的变量，然后系统允许你为它取任意名字。所以可以为import的模块起任何变量名，且不需要用大括号包含
```

