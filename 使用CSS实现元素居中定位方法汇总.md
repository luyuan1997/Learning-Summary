由于自己最近在做自己的个人博客，不免会遇到各种各样的居中要求，所以就个人总结了一下现在常用的一些方法，欢迎大家补充，并指出其中的不足。
文中例子的源码地址为：Centering position.html

对于水平居中：
1.块级元素只需要左右margin设置为auto就能够完美解决；
2.行间元素就需要父级元素设置text-align:center，行内元素设置display:inline-block实现。

.child {
  display:inline-block;
  text-align:left;
}
.parent {
  text-align:center;
}
但是多个child div之间存在缝隙，但是不属于bug，这是属性的特性；
想要去掉空格，有下面的方法：
1）去除child元素的html之间的空格，<div></div><div></div><div></div>，紧接着写，不要分行；
2）child的margin设置为负值；
3）父元素的font-size设置为0；
4）设置父元素的 letter-spacing和word-spacing为负值，设置子元素的 letter-spacing和word-spacing为0；但是这种方式我没怎么用过；
对于垂直居中：
注：文中ex指代的是example，ele指代的是element。

1.计算偏移值实现定位居中

<div class="ex1">
    <div class="ele1"></div>
  </div>
.ex1 {
      position: relative;
      width: 200px;
      height: 200px;
}
.ex1 .ele1 {
      position: absolute; 
      left: 50%;
      top: 50%;
      width: 100px;
      height: 100px;
      margin-left: -50px; 
      margin-top: -50px; 
 }
这种方法需要对父级元素以及自身元素高度、宽度等尺寸十分清楚才可以，而且偏移值等等需要计算才能知道，比较麻烦
2.使用margin:auto实现定位居中

  <div class="ex2">
    <div class="ele2"></div>
  </div>
.ex2 {
  position: relative;
  width: 200px;
  height: 200px;
}
.ex2 .ele2 {
  position: absolute; 
  left: 0;
  top: 0;
  bottom: 0;
  right: 0;
  width: 100px;
  height: 100px;
  margin: auto;
}
这种方法可以很快将元素实现居中定位，但是需要将top/left/right/bottom的值设置为0；
3.使用transform实现定位居中

<div class="ex3">
  <div class="ele3"></div>
</div>
.ex3 {
  position: relative;
  width: 200px;
  height: 200px;
}
.ex3 .ele3 {
  position: absolute;
  left: 50%;
  top: 50%;
  width: 100px;
  height: 100px;
  transform: translate(-50%, -50%);
}
先将元素的左上顶点定位中心位置，使用transform: translate(-50%, -50%)偏移元素自身的50%尺寸就可以实现居中。但是IE8及之前浏览器不可用；
4.使用table实现定位居中

  <div class="table">
    <div class="inner">
        <div class="table_ele"></div>
    </div>
</div>
.table {
    display: table;
    width: 200px;
    height: 200px;
}
.table .inner {
    display: table-cell;
    vertical-align: middle;
    text-align: center;
    background-color: transparent;
}
.table .table_ele {
    display: inline-block;
    width: 100px;
    height: 100px;
    background-color: #ccc;
}
这种方法很好很强大，使用table-cell可以实现高度不同的元素的垂直居中......
5.使用inline实现定位居中

<div class="inline">
  <div class="inline_ele"> </div>
</div>
.inline {
    width: 200px;
    height: 200px;
    text-align: center;
    line-height: 200px;
}
.inline .inline_ele {
    display: inline;
    font-size: 0;
    padding: 50px;
}
可以很好地实现行内居中
6.使用伪元素before实现定位居中

<div class="before">
  <div class="before_ele"> </div>
</div>
.before {
    width: 200px;
    height: 200px;
    font-size: 0;
}
.before::before {
    display: inline-block;
    content: '';
    height: 100%;
    vertical-align: middle;
}
.before .before_ele {
    width: 100px;
    height: 100px;
    display: inline-block;
vertical-align: middle;
}
需要对before_ele元素中的font-size属性进行调节
7.使用box实现定位居中

<div class="box">
  <div class="box_ele"> </div>
</div>
.box {
    display: -webkit-box;
-webkit-box-pack: center;
-webkit-box-align: center;
    width: 200px;
    height: 200px;
}
.box .box_ele {
    width: 100px;
    height: 100px;
}
可以实现流体布局
8.使用flexbox实现定位居中

<div class="flexbox">
  <div class="flexbox_ele"> </div>
</div>
.flexbox {
    display: flex;
    justify-content: center;
    align-items: center;
    width: 200px;
    height: 200px;
}
.flexbox .flexbox_ele {
    width: 100px;
    height: 100px;
}
属性依旧很强大，建议大家从网上找一些专门的文件看看
