---
title:'格式上下文'
subtitle:'Formatting Contexts'
date: 2016-11-29
author:'Binna'
catalog:true
header-img:
tags:
    - 前端开发
    - css
---

一直用`overflow:hidden`来清除浮动，但是一直不知道为什么可以使用它来清楚浮动的影响，查了一下资料，发现是BFC的原因。那么什么是BFC呢？BFC直译过来就是”块级格式上下文“，BFC元素的一个特性就是：计算BFC高度的时，浮动元素也参与计算。而给元素添加属性`overflow:hidden`就能定义一个BFC元素。

除了BFC这个高大上的术语，还有IFC、GFC、FFC。其实网页布局分为定位、浮动、流式布局，而流逝布局中有一些规则，就是IFC、GFC它们了，他们规定了box（盒式模型）的排版规则。BFC和IFC出现在CSS2.1中，CSS3中出现了FFC和GFC。

### 盒子模型

先从盒子模型开始总结，盒子模型是CSS基础中的基础，将盒子放到了合适的位置，盒子里面的内容（文字，图片等）也就放到了合适的位置。

<img src="https://ofw1nwn63.qnssl.com/Formatting-contenxts/boxModel.jpg" width="400px"/>

可以将盒子模型看成是一层层的，上面的层覆盖下面的层。盒子模型从上到下依次是content（内容）、padding（内边距）、border（边框）、background-img（背景图片）、background-color（背景颜色）、margin（外边距）。content是我们需要展示的内容，比如图片啊文字啊什么的；margin和padding都是间距，用来撑开容器，在没有背景图片和背景颜色的情况下，给盒子设置margin或者padding都能使相邻盒子之间保持一定的距离，但是在设置了背景了之后，仅设置padding后，相邻盒子是紧接着的。这就是margin和padding之间的区别，margin是同级盒子之间的距离，padding盒子内部一个不显示内容的距离，可以使content（内容）不从背景图片的左上角开始显示。

刚开始看盒子模型的时候，一般计算盒子模型的都有一个公式：

```
width = border-width + padding-width + content-width;
```

但是也会看到下面这种形式：

```
width = content-width;
```

实际使用中发现下面这种形式比较适用，但是试着改别人的代码的时候又会出现上面的情况，查阅资料发现，这是盒子模型的两种状态。在IE5.5（怪异模式）中是使用上面这种形式的，现代浏览器都是使用标准盒子模型的，但是有些浏览器也有可能使用这种怪异模式。为了解决这个问题，CSS添加了一个属性`box-sizing`，这个属性可以让我们自由选择使用哪种形式的盒子模型。

```css
-moz-box-sizing: border-box;     // FireFox3.5+
-o-box-sizing: border-box;       // Opera9.6(Presto内核)
-webkit-box-sizing: border-box;  // Safari3.2+
-ms-box-sizing: border-box;      // IE8
box-sizing: border-box;          // IE9+,Chrome10.0+,Safari5.1+,Opera10.6

//border-box采用IE盒子模型 
//content-box采用标准盒子模型
```

### BFC

BFC（Block Formatting Context），也就是块级格式上下文。这就是一个规则的名字，我们将一个盒子设置以下属性之后，这个盒子就是一个BFC盒子：

1. Float的值不为none
2. overflow的值不为visible
3. display的值为table-cell，table-caption，inline-block中的任何一个
4. position的值不为relative和static

一个BFC盒子就要遵守BFC盒子的规则：

1. 内部的Box会垂直方向，一个接一个地放置。
2. Box垂直方向的距离由margin决定。属于同一个BFC的两个相邻Box的margin会发生重叠。
3. 每个元素的margin box的左边，与包含块border box左边相接触（对于从左往右的格式化，否则相反）。即使存在浮动也是如此。
4. BFC的区域不会与float box重叠。
5. BFC就是页面上的一个隔离的独立容器，容器里面的子元素不会影响外面的元素。反之也如此。
6. 计算BFC高度时，浮动元素也参与计算。

接下来看一下BFC的这些规则：

#### 内部盒子垂直放置

```css
.div{
  background:#a1d664;
}
.div1{
  width:50px;
  height:50px;
  background:green;
}
.div2{
  width:50px;
  height:50px;
  background:#FF9800;
}
```

```html
<div class="div">
  <div class="div1">div1</div>
  <div class="div2">div2</div>
</div>
```

<img src="https://ofw1nwn63.qnssl.com/Formatting-contenxts/BFC-1.png"/>

#### 元素的margin-box的左边与包含块border-box的左边相接触

代码类似，给内部元素设置`margin-left:50px`，给包含块设置`border-left:50px`

<img src="https://ofw1nwn63.qnssl.com/Formatting-contenxts/BFC-2.png"/>

#### BFC区域不会和float-box重叠

其实很好理解，设置了浮动之后，这个box就是个BFC元素，BFC元素对外是独立的，所以也就不会其他BFC盒子有关系了（不重叠）。给div1的盒子设置浮动，使div2的盒子变成BFC元素。

```css
.div{
  background:#a1d664;
}
.div1{
  width:50px;
  height:50px;
  background:green;
  float:left;
}
.div2{
  width:50px;
  height:50px;
  margin:30px 0;
  overflow:hidden;
}
```

```html
<div class="div">
  <div class="div1">div1</div>
  <div class="div2">div2</div>
</div>
```

<img src="https://ofw1nwn63.qnssl.com/Formatting-contenxts/BFC-3.png"/>

#### 浮动元素参与BFC盒子高度计算

在不知道BFC之前，我一直是用`overflow:hidden`或者`clear:both`来清楚浮动的，一直以为是为浮动元素特别规定的方法，使用BFC是控制浮动元素高度的一种方法。

####  margin collapsing

margin重叠，在布局中表现为两个相邻盒子（可能是兄弟，也可能是祖先关系）的外边距结合为一个，这种现象有个名字，叫做折叠。

1. 折叠结果的计算方法

    * 如果相邻的两个外边距是正数，取它们中较大的值
    * 如果相邻的两个外边距是负数，取两者绝对值的较大值
    * 如果相邻的两个外边距是一正一反，取两个的和
2. 折叠产生的条件
    * 必须处于标准文档流的排版中（非浮动和非定位）的块级盒子中，长生折叠的对象处于同一个BFC中。
    * 两个产生折叠的对象之间没有空隙（clear:both），没有行级盒子，没有padding或者border。
    * 文档上说是次排列方向上，那一般就是垂直方向才会出现塌方的现象。
    * 元素的margin-top与其第一个子元素的margin-top；如果height:auto，那么最后一个子元素的margin-bottom也会和该元素的margin-bottom发生折叠。
    * 元素的margin-bottom与其相邻的同级元素的margin-top。
    * 块级自身发生collapsing，即元素本身padding和height为0，该元素自身的margin-top和margin-bottom会发生塌方。
3. 避免折叠的方法
    * 为某元素设置BFC，那么能够使它不与第一个（或者最后一个子元素）的margin 发生塌方。
    * 浮动元素不与任何元素发生折叠。
    * 绝对定位不与任何元素发生折叠。
    * inline-block不与任何元素元素发生折叠。
    * 某个元素的margin-bottom和它的下一个相邻元素的margin-top发生折叠，可以通过（clear:both）来产生间隙；如果情况允许，也可以使用浮动、定位、设置inline-block


先来解释一下浮动、绝对定位、inline-block不与任何元素发生折叠的原因：由于浮动元素和绝对定位元素会脱离标准文档流，而BFC是标准文档流的一个排版规则，所以也就不会发生折叠了；而inline-block是个行级块，是个特殊的东西，有点不满足块级元素，虽然能设置高宽，但是还是有行级元素的特性的，所以就不会和相邻元素折叠了。

**注意：**有个概念的理解，首先BFC是标准文档流的布局规则，其次浮动和绝对定位的元素会脱离标准文档流（也就是说浮动和绝对定位的元素不满足建立BFC的大前提：标准文档流），但是建立BFC的方法中有提到浮动和绝对定位 => 我的理解是浮动和绝对定位的元素另起炉灶，自身内部布局规则是BFC。

举个栗子：

```css
body{
  background:#00c0ff;
}
.div{
  background:#a1d664;
}
.div1{
  width:50px;
  height:50px;
  margin:30px 0;
  background:green;
}
.div2{
  width:50px;
  height:50px;
  margin:30px 0;
  background:#FF9800;
}
```

```html
<div class="div">
  <div class="div1">div1</div>
  <div class="div2">div2</div>
</div>
```

这是一个既有父元素和子元素折叠，又有子元素之间折叠的情况！背景色是天蓝色，最外面的盒子是浅绿色的，div1和div2都设置了margin-top和margin-bottom，结果两者之间只显示了一个，div1和div2也紧贴着父元素。

<img src="https://ofw1nwn63.qnssl.com/Formatting-contenxts/BFC-4.png"/>



