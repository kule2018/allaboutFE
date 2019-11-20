##### less中的注释

以//开头的注释不会编译到css文件中

以/**/开头的注释会被编译到css文件中



##### less中的变量

###### 使用@开头声明一个变量

```less
//这是less文件
@color：pink;
div{
    background-color:@color
}

//编译成css文件
div{
    background-color:pink;
}

//这是less文件
@nice-blue: #5B83AD;
@light-blue: @nice-blue + #111;
#header {
  color: @light-blue;
}

//这是编译之后的css文件
#header {
  color: #6c94be;
}
```

如果将属性名或者选择元素作为变量名的话，使用的时候要用@{}

```less
@m:margin;
div{
    @{m}:0;
}
//输出为
div{
    margin:0;
}

@selector:#app;
@{selector}{
    margin:0
}
//输出为
#app{
    margin:0;
}
```

###### 变量的延迟加载

```less
@var:0;
.class{
    @var:1;
    .brass{
        @var:2;
        three:@var;  /*less中的变量都是延迟加载的，会等到作用域内的变量解析完*/   
        @var:3;
    }
    one:@var;
}
//输出为
.class{
    one:1
}
.class .brass{
    three:3;
}
```



###### less中的嵌套规则之&的使用

在less文件采用嵌套，若不使用&则会自动编译成父子关系（ `&`代表当前选择器父对象 ）。

```less
div{
    margin:0;
    .wrap{
       width:100px;
        background:pink
        &:hover{
            background:black;
        }
    }
}
//输出为
div{
    margin:0;
}
div .wrap{
    width:100px;
    background:pink;
}
div .wrap:hover{
    background:black;
}
```



###### less中的混合

混合就是就是将一系列属性从一个规则集引入到另一个规则集的方式。

1.普通混合

```less
.my-mixin {
  color: black;
}
.class {
  .my-mixin;
}
//输出为
.my-mixin {
  color: black;
}
.class {
  color:black;
}
```

2.不带输出的混合

```less
.my-mixin {
  color: black;
}
.my-other-mixin() {
  background: white;
}
.class {
  .my-mixin;
  .my-other-mixin;
}

//输出为
.my-mixin {
  color: black;
}
.class {
  color: black;
  background: white;
}
```

3.带参数的混合

```less
.app(@c,@w,@h){
    background:@c;
    width:@w;
    height:@h;
}
div{
    .app(red,100px,200px)
}
//输出
div {
  background: red;
  width: 100px;
  height: 200px;
}

```

4.带有默认值的参数混合

```less
.app(@c:pink,@w:15px,@h:25px){
    background:@c;
    width:@w;
    height:@h;
}
.first{
    .app(red,100px,200px)
}
.second{
    .app()
}
//输出
.first {
  background: red;
  width: 100px;
  height: 200px;
}
.second {
  background: pink;
  width: 15px;
  height: 25px;
}

```

5.命名参数混合

```less
.app(@c:pink,@w:15px,@h:25px){
    background:@c;
    width:@w;
    height:@h;
}
.first{
    .app(red,100px,200px)
}
.second{
    .app(@w:35px)
}
//输出为
.first {
  background: red;
  width: 100px;
  height: 200px;
}
.second {
  background: pink;
  width: 35px;
  height: 25px;
}

```

6.@arguments

```less
.box-shadow(@x: 0; @y: 0; @blur: 1px; @color: #000) {
  -webkit-box-shadow: @arguments;
     -moz-box-shadow: @arguments;
          box-shadow: @arguments;
}
.big-block {
  .box-shadow(2px; 5px);
}
//输出为
.big-block {
  -webkit-box-shadow: 2px 5px 1px #000;
     -moz-box-shadow: 2px 5px 1px #000;
          box-shadow: 2px 5px 1px #000;
}
```



###### less的运算

 mixin中定义的变量可以用作其返回值。这使我们可以创建可以像函数一样使用的mixin 

```less
.average(@x,@y){
    @average:((@x+@y)/2)
}
div{
    .average(16px,18px);
    padding:@average
}
//输出为
div {
  padding: 17px;
}

```



##### less函数

###### 逻辑功能

```less
@some: foo;

div {
    margin: if((2 > 1), 0, 3px);
    color:  if((iscolor(@some)), @some, black);
}
输出为：
div {
    margin: 0;
    color:  black;
}
```

###### 布尔值

```less
@bg: black;
@bg-light: boolean(luma(@bg) > 50%);

div {
  background: @bg; 
  color: if(@bg-light, black, white);
}

输出为
div{
    background:black;
    color:white;
}
```

