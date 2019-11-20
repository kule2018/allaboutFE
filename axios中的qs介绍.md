#### axios中的qs介绍

##### 1.qs.parse()可以将url解析成对象的形式

```javascript
const Qs = require('qs');
let url = 'method=query_sql_dataset_data&projectId=85&appToken=7d22e38e-5717-11e7-907b-a6006ad3dba0';
Qs.parse(url);
console.log(Qs.parse(url));
```

##### 2.qs.stringify()可以将对象解析成url的形式，以&符号拼接

```javascript
const Qs = require('qs');
let obj= {
     method: "query_sql_dataset_data",
     projectId: "85",
     appToken: "7d22e38e-5717-11e7-907b-a6006ad3dba0",
     datasetId: " 12564701"
   };
Qs.stringify(obj);
console.log(Qs.stringify(obj));
```

```javascript
//默认情况下，它们给出明确的索引
qs.stringify({ a: ['b', 'c', 'd'] });   //a[0]=b&a[1]=c&a[2]=d

//修改默认方式
qs.stringify({ a: ['b', 'c', 'd'] }, { indices: false }); //a=b&a=c&a=d

//通过ArrayFormat选项进行格式化输出
qs.stringify({ a: ['b', 'c'] }, { arrayFormat: 'indices' })  //a[0]=b&a[1]=c
qs.stringify({ a: ['b', 'c'] }, { arrayFormat: 'brackets' }) //a[]=b&a[]=c
qs.stringify({ a: ['b', 'c'] }, { arrayFormat: 'repeat' })   //a=b&a=c

```

这里要注意，JSON也有stringify()方法，但两者之间有明显的的区别。

```javascript
{"uid":"cs11","pwd":"000000als","username":"cs11","password":"000000als"} //JSON.stringify(param)处理

uid=cs11&pwd=000000als&username=cs11&password=000000als
//QS.stringify(param)处理

```

