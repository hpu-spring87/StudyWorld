# Flex布局之必备点

> 浏览器的布局，传统解决方案是基于盒狀模型，依赖display属性+position属性+float属性，它对于一些特殊布局非常不方便，比如垂直居中就不容易实现。这时候W3C提出了一种新的解决方案：Flex布局，它基于css3,可以简便，完整，响应式地实现各种网页布局.

* Flex官方名字：CSS Flexible Box Layout Module，意为弹性布局，用来为盒狀模型提供最大的灵活性，它可以更高效的展示items的排列，方向，以及顺序，尽管size未知，或者动态的变化。flex容器的主要特征：它可以灵活的在不同尺寸的屏幕上的可用区域内改变子条目的宽高，从而以最合适的方式展现各个item。Flex比较适用于一个应用的组件和小规模的布局，Gird适用于大规模布局。

## Basics & Terminology （基础术语）

* 由于Flex是一个完整的module，而不是一个属性，它涉及到一系列的属性，作用于容器（盛放其他子条目（flex items））也即是flex container。

* 常规布局基于block和inline flow directions（块域和线性方向），flex layout基于flex-flow directions（灵活方向）

如图：

![一图胜千言](/images/flexbox_basics.png)

一般情况下，items将会按照main axis（from main-start to main-end）或者cross axis(from cross-start to cross-end)二者中一个轴线布局显示.

* main axis:容器的主线，items就按照这个主线进行布局，要注意：它不一定是水平的，它由flex-directions属性决定。

* main-start|main-end:items在容器内布局的起始点和终止点。

* main size: 单个item所占的主轴线的长（如图）。

* cross axis:十字轴线，与主线互相垂直，它的方向也不一定是竖直的，它的fang'xiang
方向由主线决定。

* cross-start|cross-end：items在容器内十字轴线方向的起始点和终止点。

* cross-size: 单个item所占的十字轴线长（如图）。

## Usage
### display

为了能使用flex layout，需要设置**display**属性，如下：

```
/* 任何容器都可以设置为flex布局 */
.container {
  display: flex;
}

/* 行内元素也可以设置为flex布局 */
.container{
  display: inline-flex;
}

/* Webkit内核浏览器，需要加上-webkit前缀  */
.container{
  display: -webkit-flex; /* Safari */
  display: flex;
}

```
**注意：CSS columns对flex container没有效果.子元素的float，clear，vertical-align属性失效.**

### FlexBox container properties

** flex-direction **

该属性定义flex items布局的方向，比如： row horizontally或者columns vertically

```
/* 可以设置如下值：
            row ：（默认值）主轴为水平方向，起点在左端。
            row-reverse ：主轴为水平方向，起点在右端。
            column ：主轴为竖直方向，起点在上面。
            column-reverse：主轴为竖直方向，起点在底部。
  */
.flex-container {
  -webkit-flex-direction: row; /* Safari */
  flex-direction:         row;
}

```

如下：

![一图胜千言](/images/flexbox_direction.png)

** flex-wrap **

默认情况下，item都在一条轴线上，该属性的定义是，如果一条轴线排不了，如何换行？可以不换行，换行(第一行在上方)，换行(第一行在下方)。

```
/*
nowrap(default): single-line / left to right in ltr; right to left in rtl
wrap: multi-line / left to right in ltr; right to left in rtl
wrap-reverse: multi-line / right to left in ltr; left to right in rtl
 */
.flex-container {
  -webkit-flex-wrap: wrap-reverse; /* Safari */
  flex-wrap:         wrap-reverse;
}

```

![一图胜千言](/images/flex_wrap.png)

** flex-flow **

flex-flow属性是flex-direction和flex-wrap属性的简写形式.

```
/* 默认值是row nowrap */
.flex-container {
  -webkit-flex-flow: <flex-direction> || <flex-wrap>; /* Safari */
  flex-flow:         <flex-direction> || <flex-wrap>;
}

```

** justify-content **

justify-content属性定义了，item在容器主轴上的对齐方式。

```
/*
它可以取5个值：
      * flex-start(默认值):左对齐
      * flex-end:右对齐
      * center：居中
      * space-between：两端对齐，item之间间隔相等
      * space-around:每个item之间间隔相等，所以，item之间间隔比item与边框的间隔大一倍
 */
.flex-container {
  -webkit-justify-content: flex-start; /* Safari */
  justify-content:         flex-start;
}

```

如下：

![](/images/flex_justify_content.png)

** align-items **

定义item在交叉轴上如何对齐

```
/*
它可以取5个值：
    flex-start:交叉轴的起点对齐
    flex-end:交叉轴的终点对齐
    center:交叉轴的中点对齐
    baseline：item的第一行文字对齐
    stretch(默认值)：如果item高度设置为auto，将占满整个容器高度
 */
.flex-container {
  -webkit-align-items: flex-end; /* Safari */
  align-items:         flex-end;
}

```
如图：

![](/images/flex_align.png)

** align-content **

该属性定义了多根轴线的对齐方式，如果item只有一根轴线，那么该属性不起作用。

```
/*
它可以取5个值：
        flex-start:与交叉轴的起点对齐
        flex-end:与交叉轴的终点对齐
        center:与交叉轴的中点对齐
        space-between:与交叉轴两端对齐，轴线之间的间隔平均分布
        space-around:每根轴线两侧间隔相等，所以，轴线之间间隔比轴线与边框间隔大一倍
        stretch（默认值）:轴线占满整个交叉轴
 */
.flex-container {
  -webkit-align-content: stretch; /* Safari */
  align-content:         stretch;
}

```

如图：

![flex_align_center](/images/flex_align_center.png)


**注意：**
1. 所有column-*属性都对flex-container不起作用。

2. ::first-line和::first-letter等伪元素不能应用于flex containers

### FlexBox item properties

** order **

该属性定义项目的排列顺序，数值越小越靠前，默认值为0。如果没有该属性，item按照代码顺序进行布局

```

.flex-item {
  -webkit-order: <integer>; /* Safari */
  order:         <integer>;
}

```

如图：
![](/images/flex_order.svg)

** flex-grow **

该属性定义item的放大比例，默认为0，即如果存在剩余空间，也不放大。

```
/*
默认值为0,负值无效
*/
.flex-item {
  -webkit-flex-grow: <number>; /* Safari */
  flex-grow:         <number>;
}

```
如果所有项目的flex-grow属性都为1，则他们等分剩余空间，如果一个item的属性为2，其他item都为1，则前者占据的剩余空间将比其他item多一倍。

如图：
![](/images/flex_grow.png)

** flex-shrink **

该属性定义了项目的缩小比例，默认为1。如果所有item属性都为 1，当空间不足，都将等比例缩小，如果一个item的flex-shrink属性为0，其他item都为1，则空间不足时，前者将缩小。

```
/*
默认值1，负值无效
*/
.flex-item {
  -webkit-flex-shrink: <number>; /* Safari */
  flex-shrink:         <number>;
}

```

** flex-basis **

该属性定义了在分配多余剩余空间之前，item占据的主轴空间，浏览器根据这个属性计算主轴是否有多余空间，它的默认值为auto，即item原来大小。它可以设为跟width和height属性一样值（100px）,则项目将占据固定空间.

```
.flex-item {
  -webkit-flex-basis: auto | <width>; /* Safari */
  flex-basis:         auto | <width>;
}

```

** flex **

flex属性是flex-grow,flex-shrink,flex-basis的简写，默认值为0 1 auto，后两者属性可选。


```
/*
有两个快捷键值：
auto (1 1 auto)
none (0 0 auto)
W3C建议优先写快捷键值，而不是单独写3个属性值，因为浏览器会推算相关值
*/
.flex-item {
  -webkit-flex: none | auto | [ <flex-grow> <flex-shrink>? || <flex-basis> ]; /* Safari */
  flex:         none | auto | [ <flex-grow> <flex-shrink>? || <flex-basis> ];
}

```

** align-self **

该属性允许单个项目有与其他项目不一样的对齐方式，可覆盖align-items属性，默认值为auto，表示继承父元素的align-items属性，如果没有父元素，则等同于stretch.

```
/*
该属性可以取6个值，除了auto，其他都与align-items属性完全一致
*/
.flex-item {
  -webkit-align-self: auto | flex-start | flex-end | center | baseline | stretch; /* Safari */
  align-self:         auto | flex-start | flex-end | center | baseline | stretch;
}

```

**注意：**

1. float,clear,vertical-align对flex item无效。
