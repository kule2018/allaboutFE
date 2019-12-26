## <a></a>标签全部作用

1.超链接
2.锚点
3.打电话
4.发邮件
5.协议限定符



## 用CSS画三角形

![img](https://images2015.cnblogs.com/blog/1191953/201707/1191953-20170715233951697-1518652311.bmp)

想得到一个三角形的时候，不能单独设置一个边框，只设置一条边框的时候，它只是一条只有宽度没有高度的线，在页面中无法显示；

因此还是要同时设置4条边框或者给两个相邻的边框设置宽度，只给其中一个边框添加颜色即可：

设置四条边：

![img](https://images2015.cnblogs.com/blog/1191953/201707/1191953-20170715234345884-1608288026.bmp)

设置两条边：

![img](https://images2015.cnblogs.com/blog/1191953/201707/1191953-20170715235412165-1786308789.bmp)



## 水平元素居中

<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>未知宽高元素水平垂直居中</title>
</head>
<style>
```css
.parent1{
    display: table;
    height:300px;
    width: 300px;
    background-color: #FD0C70;
}
.parent1 .child{
    display: table-cell;
    vertical-align: middle;
    text-align: center;
    color: #fff;
    font-size: 16px;
}
</style>
<body>
    <div class="parent1">
        <div class="child">hello world-1</div>
    </div>
</body>
</html>

```



​```css
.child{
    position: absolute;
    top: 50%;
    left: 50%;
    color: #fff;
    transform: translate(-50%, -50%);
}
```



```css
div.box{

weight:200px;

height:400px;

 <!--把元素变成定位元素-->

position:absolute;

<!--设置元素的定位位置，距离上、左都为50%-->

left:50%;

top:50%;

<!--设置元素的左外边距、上外边距为宽高的负1/2-->

margin-left:-100px;

margin-top:-200px;

}
```

```css
div.box{

width:200px;

height:400px;

<!--把元素变成定位元素-->

position:absolute;

<!--设置元素的定位位置，距离上、下、左、右都为0-->

left:0;

right:0;

top:0;

bottom:0;

<!--设置元素的margin样式值为 auto-->

margin:auto;

}

 
```

```css
.main{
  display：flex;
  flex:1;
  align-items:center;
  justify-content:center;
}
```



## 两栏布局

#### 左固定宽度，右边自适应

```css
html

	<div class="left">left</div>
	<div class="right">right</div>

css

	body,div{padding: 0 ;margin:0;}
	.left,.right{height: 200px;}
	.left{float: left;width: 200px;background-color:skyblue;}
	.right{margin-left: 200px; background-color: greenyellow;}

//因为块级元素有流体特性，即默认会填充满外部容器，所以只需要设置margin，不需要设置width就可以让content填满剩余的部分。

```

```css
html

	<div class="left">left</div>
	<div class="right">right</div>

css

	body,div{padding: 0 ;margin:0;}
	.left,.right{height: 200px;}
	.left{float: left;width: 200px;background-color:skyblue;}
	.right{overflow:hidden; background-color: greenyellow;}

右侧设置的overflow:hidden会触发块级格式化上下文（BFC）。
具有BFC特性的元素可以看作是隔离了的独立容器，容器里面的元素不会在布局上影响外面的元素，并且BFC具有普通元素没有特性：如下边距不发生折叠；可以清除浮动；可以阻止元素被覆盖。
正因为有了这些特性，所以右边可以用触发BFC的元素来清除左边浮动的影响。

触发了BFC的元素仍然保持流体特性，也就是说BFC元素虽然不与浮动交集，自动退避浮动元素宽度的距离，但本身作为普通元素的流体特性依然存在，反映在布局上就是自动填满除去浮动内容以外的剩余空间。

```

```css
利用绝对定位
<div class="wrap">
		<div class="left">left</div>
		<div class="right">right</div>
	</div>

css

.wrap{position : relative; }
.left{ width: 200px; }
.right{ position: absolute; top: 0; left: 200px; right: 0}

//通过设置right:0；来限制右边块级元素的宽度

```

#### 一栏不定宽，一栏自适应

```css
	<div class="left">我是left</div>
	<div class="right">我是right</div>
1
2
	body,div{padding: 0 ;margin:0;}
	.left,.right{height: 200px;padding: 10px;}
	.left{float: left;background-color:skyblue;}
	.right{overflow:hidden;background-color: yellow;}

```

```css
<div class="wrap">
		<div class="left">我是left</div>
		<div class="right">我是right</div>
	</div>
1
2
3
4
        body,div{padding: 0 ;margin:0;}
		.wrap{display:flex;}
		.left,.right{height: 200px;padding: 10px;}
		.left{background-color:skyblue;}
		.right{flex:1;background-color: yellow;}

```

 



## 三栏布局

### 1. float布局

```css
    <style>
      .left {
        float: left;
        width: 100px;
        height: 200px;
        background-color: red;
      }
    
      .right {
        float: right;
        width: 100px;
        height: 200px;
        background-color: yellow;
      }
    
      .main {
        background-color: green;
        height: 200px;
        margin-left: 120px;
        margin-right: 120px;
      }
    
      .container {
        border: 1px solid black;
      }
    
      <div class="container">
      <div class="left"></div>
      <div class="right"></div>
      <div class="main"></div>
      </div>

我们知道对于float元素，其会脱离文档流，其他盒子也会无视这个元素。（但其他盒子内的文本依然会为这个元素让出位置，环绕在周围。）所以此时只需在container容器内添加一个正常的div，其会无视left和right，撑满整个container，只需再加上margin为left right流出空间
```

### 2. BFC 规则

```css
BFC(块格式化上下文)规则规定：BFC不会和浮动元素重叠。所以如果将main元素设定为BFC元素即可： 
<style>
      .left {
        float: left;
        width: 100px;
        height: 200px;
        background-color: red;
      }
    
      .right {
        float: right;
        width: 100px;
        height: 200px;
        background-color: yellow;
      }
    
      .main {
        background-color: green;
        height: 200px;
        overflow: hidden;
      }
    
      <div class="container">
        <div class="left"></div>
        <div class="right"></div>
        <div class="main"></div>
      </div>
```

#### 3. 圣杯布局

https://www.jianshu.com/p/8b308d63fe23

#### 4. 双飞翼布局

https://www.jianshu.com/p/8b308d63fe23

### 5. flex布局

### 6. 绝对定位



## 元素的分类

| 块级元素 | 描述                                | 行内元素 | 描述                           |
| -------- | ----------------------------------- | -------- | ------------------------------ |
| div      | 常用的块级容器                      | span     | 常用的行内元素，定义文本内区块 |
| h1~h6    | 主标题、二级子标题、三级子标题..... | a        | 锚点、超链接                   |
| hr       | 水平分割线                          | b        | 文字内容加粗                   |
| menu     | 菜单列表                            | strong   | 文字内容加粗强调               |
| ol       | 有序列表                            | i        | 文字内容斜体                   |
| ul       | 无序列表                            | em       | 文字内容斜体强调               |
| li       | 列表项                              | br       | 强制换行                       |
| dl       | 定义列表                            | input    | 文本输入框                     |
| table    | 表格                                | textarea | 多行文本输入框                 |
| p        | 段落                                | img      | 引入图片                       |
| form     | 交互表单                            | select   | 下拉列表                       |

 



## margin塌陷及合并

#### **塌陷**

原理:父子嵌套元素在垂直方向的margin,父子元素是结合在一起的,他们两个的margi会取其中最大的值.

正常情况下,父级元素应该相对浏览器进行定位,子级相对父级定位.

但由于margin的塌陷,父级相对浏览器定位.而子级没有相对父级定位,子级相对父级,就像坍塌了一样.

解决方法：触发BFC。

改变父级的渲染规则有以下四种方法,给父级盒子添加

(1)position:absolute/fixed

(2)display:inline-block;

(3)float:left/right

(4)overflow:hidden

这四种方法都能触发bfc,但是使用的时候都会带来不同的麻烦,具体使用中还需根据具体情况选择没有影响的来解决margin塌陷

#### 合并

两个兄弟结构的元素在垂直方向上的margin是合并的

解决：触发BFC

1. 第二个div加上一个父元素，并设置overflow:hidden
2. 两个都加上一个父元素再触发bfc







## 浮动模型及清除浮动的方法

#### 浮动：使元素脱离文档流。

1.所有的元素都可以浮动。
2.具有 float 属性元素在父标签中是不占空间的。 3.float 能解决标签之间有间隙的问题。

**float 对行内属性标签的影响：**
　　1、 float 之后可以设置 width 和 height 属性。
　　2、并支持 margin 和 padding 属性。

**float 对块属性标签的影响**
　　1、在没有设置宽高的情况下浮动后，内容撑开宽度高度。
　　2、可以使块属性元素并排排列。

#### 清除浮动

**1、clear 应用的原理是清除元素两侧浮动元素带来的影响。**

clear: left; 左侧不允许有浮动元素（本身起作用），邻后的元素需清除左侧浮动元素带来的影响则可以用 clear:left； 进行清除。
　　clear: right; 右侧不允许有浮动元素（本身起作用），邻后的元素需清除右侧浮动元素带来的影响则可以用 clear:right；进行清除。
　　clear: both;清除元素两侧浮动影响。原理：添加一个空 div，利用 css 的 clear:both 清除浮动，让父级 div 能自动获取到高度。

**2、overflow: hidden;超出内容隐藏**
(父级下的子元素都是浮动状态，父级添
　　 overflow:hidden;属性解决子元素浮动造成父级高度塌陷现象，父级的相邻元素正常显示。)
　　 overflow: visible：显示超出内容，不剪切内容也不添加滚动条 

​        overflow: auto：如果内容被修剪，则浏览器会显示滚动条以便查看其余的内容。
　　overflow: scroll：内容会被修剪，但是浏览器会显示滚动条以便查看其余的内容
**3、after 伪类清除浮动**
　　 .clearfix:after {content:""; display:block;clear:both; }
　　 .clearfix { zoom:1; }//IE 清除浮动



##  display及相关属性

| 值           | 描述                                                         |
| :----------- | :----------------------------------------------------------- |
| table-cell   | 此元素会作为一个表格单元格显示（类似 <td> 和 <th>）          |
| none         | 此元素不会被显示。                                           |
| block        | 此元素将显示为块级元素，此元素前后会带有换行符。             |
| inline       | 默认。此元素会被显示为内联元素，元素前后没有换行符。         |
| table        | 此元素会作为块级表格来显示（类似 <table>），表格前后带有换行符。 |
| inline-block | 行内块元素。（CSS2.1 新增的值）                              |



## flex布局

Flex是Flexible Box的缩写，顾名思义为“弹性布局”，用来为盒装模型提供最大的灵活性。

任何一个容器都可以指定为Flex 布局。

需要注意的是，设为flex布局以后，子元素的float、clear和vertical-align属性将失效

以下6个属性设置在容器上。

- flex-direction
- flex-wrap
- flex-flow
- justify-content
- align-items
- align-content

https://www.cnblogs.com/dreamperson/p/9367008.html



## px、em、rem的区别

Px表示“绝对尺寸”（并非真正的绝对），实际上就是css中定义的像素（此像素与设备的物理像素有一定的区别，后续详细说明见文末说明1），利用px设置字体大小及元素宽高等比较稳定和精确。Px的缺点是其不能适应浏览器缩放时产生的变化，因此一般不用于响应式网站。

em表示相对尺寸，其相对于当前对象内文本的font-size（如果当前对象内文本的font-size计量单位也是em，则当前对象内文本的font-size的参考对象为父元素文本font-size）。使用em可以较好的相应设备屏幕尺寸的变化，但是在进行元素设置时都需要知道父元素文本的font-size及当前对象内文本的font-size，如有遗漏可能会导致错误。

rem也表示相对尺寸，其参考对象为根元素<html>的font-size，因此只需要确定这一个font-size。



## transition translate transform

**transform 和 translate**

transform的中文翻译是变换、变形，是css3的一个属性，和其他width，height属性一样

translate 是transform的属性值，是指元素进行2D变换，2D变换就是指，元素以当前位置（0,0）按照x轴的方向移动多少，按照y轴的方向移动多少 

例如：

transform：translate(0,100%) 表示从元素的当前位置延y轴方向，向下移动整个元素高度的距离

transform：translate(-20px,0) 表示从元素的当前位置延x轴方向，向左移动20px

transform 有很多其它属性值，translate3D（3D变换）,scale（2D缩放）等其他的变换方式

 

**transition**  

transition  在一定时间之内，一组css属性变换到另一组属性的动画展示过程。可以用来实现动态效果，css3的属性

语法 transition：需要变换的属性 变换需要的时间 控制动画速度变化 延期多少时间后开始执行 

transition属性写在最初的样式里，而不是放在结束的样式里，即定义动画开始之前的元素外观的样式。只需要给元素设置一次transition，浏览器就会负责以动画展示从一个样式到另一个样式。

例如：

transition:width 2s; 

transition:translate 2s;

transtion:all 2s;



## BFC和IFC

### BFC

Block Formatting Context 块级格式化上下文。

#### bfc是什么

由css2提出，具有规定的渲染，定位等规则的块级元素；大家都知道盒子box，一个布局中，可以同时存在很多的盒子boxes，而盒子只是容器而已，这也是其不同之处，可以说成是其升级版，具有一些规则和渲染方式之后就可以变成一个BFC，当然也只有块级元素能参与转化成BFC。

#### BFC布局规则

1. 内部的Box会在垂直方向，一个接一个的放置
2. 同一个BFC内，垂直方向的盒子上下margin会重叠
3. 每个元素的margin box的左边，与包含块border box的左边连接（对于从右往左的布局，则相反）即使存在浮动也是如此
4. 子BFC的区域不会与float box重叠
5. BFC就是页面上的一个隔离的独立容器，容器里面的子元素不会影响到外面的元素，反之也如此。
6. 计算BFC的高度时，浮动元素也参与计算（故也可以达到所谓清除浮动的效果，只要将包裹层转变为BFC）

#### 如何将块级元素转换成BFC

1. 具有除了float:none的其他浮动属性
2. 定位为absolute或者fixed
3. dispaly为block、inline-block、table-cell、table-caption、flex、inline-flex
4. overflow不为visible（除非该值已经传播到视口，入html body会将overflow的值传播到视口，故此情况下，该属性不能建立BFC）

### IFC

Inline Formatting Context 内敛格式化上下文。

#### ifc是什么

IFC的line box（线框高度由其包含行内元素中最高的实际高度计算而来（不受到竖直方向的padding/margin影响）

IFC的inline box一般左右都贴紧整个IFC，但是因为float元素二扰乱。float元素会位于IFC与line box之间，使得line box宽度缩短。同个IFC下的多个line box高度会不同。IFC中不可能有块级元素，当插入块级元素时（如p中插入div）会产生两个匿名快与div分隔开，即产生两个IFC，每个IFC对外表现为块级元素，与div垂直排列。

#### 作用

水平居中：当一个块要在环境中水平居中时候，设置其为inline-block则会在外层产生IFC，通过text-align:center则可以使其水平居中。

垂直居中：创建一个IFC，用其中一个元素撑开父元素的高度，然后设置其vertical-align:middle,其他行内元素则可以在此父元素下垂直居中。



## 媒体查询

如果文档宽度小于 300 像素则修改背景颜色(background-color):

@media screen and (max-width: 300px) {
    body {
        background-color:lightblue;
    }
}



#### 媒体类型

| 值         | 描述                                                         |
| :--------- | :----------------------------------------------------------- |
| all        | 用于所有设备                                                 |
| aural      | 已废弃。用于语音和声音合成器                                 |
| braille    | 已废弃。 应用于盲文触摸式反馈设备                            |
| embossed   | 已废弃。 用于打印的盲人印刷设备                              |
| handheld   | 已废弃。 用于掌上设备或更小的装置，如PDA和小型电话           |
| print      | 用于打印机和打印预览                                         |
| projection | 已废弃。 用于投影设备                                        |
| screen     | 用于电脑屏幕，平板电脑，智能手机等。                         |
| speech     | 应用于屏幕阅读器等发声设备                                   |
| tty        | 已废弃。 用于固定的字符网格，如电报、终端设备和对字符有限制的便携设备 |
| tv         | 已废弃。 用于电视和网络电视                                  |

#### 媒体功能

| 值                      | 描述                                                         |
| :---------------------- | :----------------------------------------------------------- |
| aspect-ratio            | 定义输出设备中的页面可见区域宽度与高度的比率                 |
| color                   | 定义输出设备每一组彩色原件的个数。如果不是彩色设备，则值等于0 |
| color-index             | 定义在输出设备的彩色查询表中的条目数。如果没有使用彩色查询表，则值等于0 |
| device-aspect-ratio     | 定义输出设备的屏幕可见宽度与高度的比率。                     |
| device-height           | 定义输出设备的屏幕可见高度。                                 |
| device-width            | 定义输出设备的屏幕可见宽度。                                 |
| grid                    | 用来查询输出设备是否使用栅格或点阵。                         |
| height                  | 定义输出设备中的页面可见区域高度。                           |
| max-aspect-ratio        | 定义输出设备的屏幕可见宽度与高度的最大比率。                 |
| max-color               | 定义输出设备每一组彩色原件的最大个数。                       |
| max-color-index         | 定义在输出设备的彩色查询表中的最大条目数。                   |
| max-device-aspect-ratio | 定义输出设备的屏幕可见宽度与高度的最大比率。                 |
| max-device-height       | 定义输出设备的屏幕可见的最大高度。                           |
| max-device-width        | 定义输出设备的屏幕最大可见宽度。                             |
| max-height              | 定义输出设备中的页面最大可见区域高度。                       |
| max-monochrome          | 定义在一个单色框架缓冲区中每像素包含的最大单色原件个数。     |
| max-resolution          | 定义设备的最大分辨率。                                       |
| max-width               | 定义输出设备中的页面最大可见区域宽度。                       |
| min-aspect-ratio        | 定义输出设备中的页面可见区域宽度与高度的最小比率。           |
| min-color               | 定义输出设备每一组彩色原件的最小个数。                       |
| min-color-index         | 定义在输出设备的彩色查询表中的最小条目数。                   |
| min-device-aspect-ratio | 定义输出设备的屏幕可见宽度与高度的最小比率。                 |
| min-device-width        | 定义输出设备的屏幕最小可见宽度。                             |
| min-device-height       | 定义输出设备的屏幕的最小可见高度。                           |
| min-height              | 定义输出设备中的页面最小可见区域高度。                       |
| min-monochrome          | 定义在一个单色框架缓冲区中每像素包含的最小单色原件个数       |
| min-resolution          | 定义设备的最小分辨率。                                       |
| min-width               | 定义输出设备中的页面最小可见区域宽度。                       |
| monochrome              | 定义在一个单色框架缓冲区中每像素包含的单色原件个数。如果不是单色设备，则值等于0 |
| orientation             | 定义输出设备中的页面可见区域高度是否大于或等于宽度。         |
| resolution              | 定义设备的分辨率。如：96dpi, 300dpi, 118dpcm                 |
| scan                    | 定义电视类设备的扫描工序。                                   |
| width                   | 定义输出设备中的页面可见区域宽度。                           |



## VH和VW

```javascript
vw = view width

vh = view height
```

视口单位：在桌面端，指的是浏览器的可视区域；在移动端，它涉及3个视口：Layout Viewport（布局视口），Visual Viewport（视觉视口），Ideal Viewport（理想视口）。

视口单位中的“视口”，桌面端指的是浏览器的可视区域；移动端指的就是Viewport中的Layout Viewport。

#### vh/vw与%区别

| 单位 | 解释                   |
| ---- | ---------------------- |
| vw   | 1vw = 视口宽度的1%     |
| vh   | 1vh = 视口高度的1%     |
| vmin | 选取vw和vh中最小的那个 |
| vmax | 选取vw和vh中最大的那个 |

比如：浏览器视口尺寸为370px,那么 `1vw = 370px * 1% = 6.5px`(浏览器会四舍五入向下取7)

vh/vw与%区别在于

| 单位  | 解释           |
| ----- | -------------- |
| %     | 元素的祖先元素 |
| vh/vw | 视口的尺寸     |



## H5的语义化标签

Header：

   不用多说，就是定义头部，可以多个。

Footer：

   底部，不一定是文档最底部，可以多个。

Nav：

   导航栏标签，定义导航栏。

Article：

   独立内容区域，与session类似，用于文章等。

Aside：

   页面侧边栏所使用。

Time:

   时间标签，主要用于搜索引擎和其它一些内容引擎特殊的解析和展示。

Section：

   节的意思，主要是区分开内容，文档中的节或者是文章的节。

Video：

   视频，现在大部分不支持自动播放了，微信能处理，其他还没见过能自动播放。

Audio：

   音频，也就是音乐，也不支持自动播放。



## Web Worker和Web Socket

Web Worker让JS有了多线程的能力，可以将复杂耗时的操作都交付给Worker线程处理。WebSocket让web端与服务端维持一个有效的长连接，实现服务端主动推送数据。将二者一结合，业务系统信息流转通知功能完全就可以剥离出来。



## CSS动画

https://www.w3school.com.cn/cssref/pr_animation.asp



## CSS画圆

```css
圆圈
.circle{
width:100px;
height:100px;
border-radius:50px;          //width,height的有一半
border:1px solid red;
}
实心圆
.circle{
width:100px;
height:100px;
border-radius:50px;          //width,height的有一半
background:blue;
border:1px solid red;
}

```

