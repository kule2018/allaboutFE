

JSON （JavaScript Object Notation）一种简单的数据格式，比xml更轻巧。 **JSON 是 JavaScript 原生格式**，这意味着在JavaScript 中处理 JSON 数据不需要任何特殊的 API 或工具包。JSON的规则很简单： 对象是一个无序的“名称/值”对集合。一个对象以“{”（左括号）开始，“}”（右括号）结束。每个“名称”后跟一个“:”（冒号）；“名称/值”对之间使用“,”（逗号）分隔。

它是一种严格的js对象的格式，JSON的属性名必须有双引号，如果值是字符串，也必须是双引号；

**JSON只是一种数据格式（或者叫数据形式）;**



```js
<script>
var obj2={};//这只是JS对象
var obj3={width:100,height:200};/*这跟JSON就更不沾边了,只是JS的 对象 */
var obj4={'width':100,'height':200};/*这跟JSON就更不沾边了,只是JS的对象 */
var obj5={"width":100,"height":200,"name":"rose"}; /*我们可以把这个称做：JSON格式的JavaScript对象 */
var str1='{"width":100,"height":200,"name":"rose"}';/*我们可以把这个称做：JSON格式的字符串 */
var a=[
 {"width":100,"height":200,"name":"rose"},
 {"width":100,"height":200,"name":"rose"},
 {"width":100,"height":200,"name":"rose"},
 ];
 /*这个叫JSON格式的数组，是JSON的稍复杂一点的形式 */
var str2='['+
 '{"width":100,"height":200,"name":"rose"},'+
 '{"width":100,"height":200,"name":"rose"},'+
 '{"width":100,"height":200,"name":"rose"},'+
 ']' ;
 /* 这个叫稍复杂一点的JSON格式的字符串 */
</script>
```

**JSON和JS对象区别对比表**



| **区别** | **Json**                                                     | **Javascript****对象**                                       |
| -------- | ------------------------------------------------------------ | ------------------------------------------------------------ |
| 含义     | 仅仅是一种数据格式                                           | 表示类的实例                                                 |
| 传输     | 可以跨平台数据传输，速度快                                   | 不能传输                                                     |
| 表现     | 1,键值对方式，键必须加**双**引号2,值不能是方法函数,不能是undefined/NaN | 1,键值对方式，键不加引号2,值可以是函数、对象、字符串、数字、boolean 等 |
| 相互转换 | Json转化为js对象：1,JSON.parse(jsonstring); (不兼容ie7)2,Jsobj=eval("("+jsonstring+")")；(兼容所有浏览器，但不安全，会执行json里面的表达式?) | Js对象转换为Json：JSON.stringify(jsobj);(不兼容ie7)          |
| 其他     | 调用json官网的js，实现parse 和 stringify 在各个浏览器的兼容：https://github.com/douglascrockford/JSON-js/blob/master/json2.js |                                                              |



总而言之你可以理解为JSON是JS下的一种数据格式，他从属于JS，并且在处理JSON数据时可直接使用JS内置API