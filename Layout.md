如何用CSS实现下面的情况（CSS LAYOUT）
===========================
左右布局(浮动布局)：
----------------
这种方法我采用的是左边浮动，右边加上一个margin-left值，让他实现左边固定，右边自适应的布局

* 代码
```
<!DOCTYPE html>
<html>
<head>
  <meta charset="utf-8">
  <title>JS Bin</title>
  <style type="text/css">
    	<style type="text/css">
			*{
margin: 0;
				padding: 0;
			}
			#left {
				float: left;
				width: 220px;
				background-color: green;
			}
			#content {
			  background-color: orange; 
              margin-left: 220px;
			}
		</style>
</head>
<body>
		<div id="left">Left sidebar</div>
		<div id="content">Main Content</div>
</body>
</html>
```
左中右布局（浮动布局）
------------------
通常html网页布局时候，三列布局比较多，以下是div布局的简单三列实现，采用float浮动实现三个div排一排，形成左中右结构布局。
*代码：
```
<!DOCTYPE html>
<html>
<head>
<meta http-equiv="Content-Type" content="text/html; charset=utf-8" />
<title>div三列布局</title>
  <style>
    #thinkcss{width:400px; overflow:hidden}
      .left-a{ float:left; width:120px; border:1px solid #F00}
      .left-b{ float:left; width:130px; border:1px solid #000; margin-left:7px}
      .right{ float:right; width:130px; border:1px solid #F00}
  </style>
</head>
<body>
   <div id="THREE">
     <div class="left-a">
      左
     </div>
     <div class="left-b">
      中
     </div>
     <div class="right">
      右
     </div>
   </div>
</body>
</html>
```
水平居中：
-------
元素主要分为块级元素和行内元素，所以对元素进行水平居中也分这两种情况来讨论，另外块级元素的实现比较复杂，将分情况讨论。
* 行内元素
常用行内元素为a/img/input/span 等，标签内的HTML文本也属于此类。对于此类情况，水平居中是通过给父元素设置 text-align:center来实现的。
HTML结构：
```
<body>
  <div class="txtCenter">
    Hello World!!!
  </div>
</body>
```
CSS样式：
```
<style>
  div.txtCenter{
    text-align:center;
  }
</style>
```
* 块级元素
常用块级元素为div/table/ul/dl/form/h1/p等。根据应用场景不同又分为定宽块级与不定宽块级两种情况，分别讨论。
  * 定宽块级元素
满足**定宽**和**块状**两个条件的元素是可以通过设置**“左右margin”值为“auto”**来实现居中的。
HTML结构：
```
<body>
  <div>
    Hello World!!!
  </div>
</body>
```
CSS样式：
```
<style>
  div{
    border:1px solid red;/*为了显示居中效果明显为 div 设置了边框*/
    width:500px;/*定宽*/
    margin:20px auto;/* margin-left 与 margin-right 设置为 auto */
  }
</style>
```
  * 不定宽块级元素
我们经常会遇到不定宽度块级元素的使用，如分页导航，因为分页的数目不定，所以不能用宽度限制住。此时对元素进行水平居中主要有三种方式：
•	加入 table 标签
•	设置 display;inline 方法
•	设置 position:relative 和 left:50%;
2.1加入 table 标签
第一步：为需要设置的居中的元素外面加入一个 table 标签 ( 包括 <tbody>、<tr>、<td> )。
第二步：为这个 table 设置“左右 margin:auto”（这个和定宽块状元素的方法一样）。
HTML结构：
```
<div>
  <table>
    <tbody>
      <tr><td>
        <ul>
          <li><a href="#">1</a></li>
          <li><a href="#">2</a></li>
          <li><a href="#">3</a></li>
        </ul>
      </td></tr>
    </tbody>
  </table>
</div>
```
CSS样式：
```
<style>
  table{
    margin:0 auto;
  }
  ul{list-style:none;margin:0;padding:0;}
  li{float:left;display:inline;margin-right:8px;}
</style>
```
**这种方法的缺点是增加了无语义的HTML标签，增加了嵌套深度
2.2设置 display;inline 方法
改变块级元素的 dispaly 为 inline 类型，然后使用 text-align:center 来实现居中效果。
HTML结构：
```
<body>
  <div class="container">
    <ul>
      <li><a href="#">1</a></li>
      <li><a href="#">2</a></li>
      <li><a href="#">3</a></li>
    </ul>
  </div>
</body>
```
CSS样式：
```
<style>
  .container{
    text-align:center;
  }
  .container ul{
    list-style:none;
    margin:0;
    padding:0;
    display:inline;
  }
  .container li{
    margin-right:8px;
    display:inline;
  }
</style>
```
这种方法的缺点是将块级元素的display设置为inline，于是少了很多功能，比如盒子模型
2.3设置 position:relative 和 left:50%;
通过给父元素设置 float，然后给父元素设置 position:relative 和 left:50%，子元素设置 position:relative和 left:-50% 来实现水平居中。
HTML结构：
```
<body>
  <div class="container">
    <ul>
      <li><a href="#">1</a></li>
      <li><a href="#">2</a></li>
      <li><a href="#">3</a></li>
    </ul>
  </div>
</body>
```
CSS样式：
```
<style>
  .container{
    float:left;
    position:relative;
    left:50%
  }
  .container ul{
    list-style:none;
    margin:0;
    padding:0;
    position:relative;
    left:-50%;
  }
  .container li{float:left;display:inline;margin-right:8px;}
</style>
```
这种方法可以保留块状元素仍以 display:block 的形式显示，优点不添加无语议表标签，不增加嵌套深度，但它的缺点是设置了 position:relative，带来了一定的副作用。

垂直居中：
--------

根据不同情况，使用的垂直居中方式各异：针对块级元素与行级元素的垂直居中不同。

行级元素

* 1.1 行内包含特殊元素
  * 如果行内包含特殊元素：图片、input输入框、inline-block元素或者粗体
  * 使用verticle-align: middle;设置对齐方式即可垂直居中。text-bottom/text-top 为下对齐/上对齐
  * 兼容性很好：IE4

* 1.2 设置line-height
  * 设置line-height与height值相等，可以实现行级元素或者纯文本的块级元素的垂直居中
  * 兼容性好IE4

块级元素

* 2.1flex和align-items
  * 设置容器元素display: flex; align-items: center;即可，其内的子元素在容器中垂直居中
  * 缺点： 使用flex布局，并且使用CSS3的align-items属性，兼容性较差：IE11

* 2.2 flex和align-self
  * 设置容器元素display: flex; ，子元素设置align-self: center;
  * align-self属性允许单个项目有与其他项目不一样的对齐方式，可覆盖align-items属性。默认值为auto，表示继承父元素的align-items属性，如果没有父元素，则等同于stretch
  * 同样兼容性较差：IE11

* 2.3 绝对定位
  * 父元素设置相对定位position: relative;
  * 子元素设置绝对定位postion: absolute; top: 0; left:0; bottom: 0; right: 0; margin: auto;
  * 关键在于设置top: 0; left:0; bottom: 0; right: 0; margin: auto表示水平、垂直4个方向的margin值都通过计算获取
  * 兼容性IE7

```
<div class="wrap">
<div class="child"></div>
</div>
<style type="text/css">
* {margin: 0; padding: 0;}
.wrap {position: relative; 100vw; height: 100vh;}  /* 注意清除margin和padding，否则100vh不对*/
.child {
position: absolute;
top: 0;	
bottom: 0;
right: 0;
left: 0;
margin: auto;
width: 200px;
height: 100px;
background: lightgreen;
}
```
* 2.4 display: table-cell
  * 表格元素可以设置verticle-align: middle;实现垂直居中
  * 为容器添加display: table-cell; verticle-align: middle;
  * 缺点是不能设置百分比宽度，可以设置固定像素值
  * 兼容向IE8

* 2.5 绝对定位
  * 利用父元素相对定位，子元素绝对定位，并且处置、水平方向个偏移50%
  * 子元素利用负值margin偏移自身宽度、长度的一半
  * 缺点是需要固定子元素的宽高
  * 兼容性IE7

* 2.6 绝对定位使用translate()属性
  * position: absolute; top: 50%; left: 50%;中，50%是相对容器的宽度
  * transform: translate(-50%, 50%)是相对于元素自身的宽度，无需再用负的margin值
  * 父元素设置{ position: relative; }
  * 子元素设置{ position: absolute; top: 50%; left: 50%; transform: translate(-50%, 50%) }

