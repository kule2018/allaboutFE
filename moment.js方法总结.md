#### moment.js方法总结

引入moment

```javascript 
//require引入方式
var moment=require('moment')

//import引入方式
import moment from 'moment'
```

##### 设定moment区域为中国

```javascript
moment.locale('zh-cn')
```

##### 格式化时间类型

 1.取当天时间，以YYYY年MM月DD日形式显示 

```javascript
var now=moment().format("YYYY年MM月DD日");
```

 2.任意时间戳格式化，以YYYY-MM-DD HH:mm:ss形式显示 

```javascript
var t1=moment(1411641720000).format('YYYYY-MM-DD HH:mm:ss')
```

3.获取前一天日期，格式以YYYY-MM-DD形式显示

```javascript
var t11=moment().day(0).format('YYYY-MM-DD')
```

4.获取本周五日期，格式以YYYY-MM-DD形式显示

```javascript
var t12=moment().weekday(5).format('YYYY-MM-DD')
```

5.获取上周五日期，格式以YYYY-MM-DD形式显示

```javascript
var t13=momeny().weekday(-3).format('YYYY-MM-DD')
```

 可以简单理解为上周倒数第几天，上周倒数第三天就是上周五了，和当天日期无关 

6.获取当前**年份、月份、日期**

```javascript
var t14=moment().year();
var t15=moment().month();  //此处月份从0开始，当前月要+1
var t16=moment().data();  //注意这个地方，日期不是.day()/days()
```

7.获取上个月今天的日期，格式以YYYY-MM-DD显示

```javascript
var t17=moment().substact(1,'months').format('YYYY-MM-DD')
```

8.获取前一天日期，格式以YYYY-MM-DD显示

```javascript
var t18=moment().substract(1,'days').format('YYYY-MM-DD')
```

9.获取去年今天的日期，格式以YYYY-MM-DD显示

```javascript
var t19=moment().substract(1,'year').format('YYYY-MM-DD')
```

10.获取两个小时之后的时间

```javascript
var t20=moment().add(2,'hours').format('YYYY-MM-DD HH:mm:ss')
```

11.获取五天前的日期

```javascript
var t21=moment().subtract(5,'days').format('YYYY-MM-DD')
```

