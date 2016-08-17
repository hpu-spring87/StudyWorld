# .VectorDrawable（矢量图）

### 简介

Android L（5.0）开始提供了新的API VectorDrawable 可以使用SVG类型的资源，也就是矢量图。

** 小提示：**
为了提升重绘的性能，会为每个VectorDrawable 创建一个bitmap cache，因此，相同的VectorDrawable会共享同一个bitmap cache，当大小发生变化的时候，bitmap cache会发生重建和重绘，总而言之：如果一个VectorDrawable被用于不同的size，最高效的做法就是创建多个bitmap cache为多个不同的size.

### 创建

> 首先必须科普（Viewport）是个什么鬼.字面意思，视口，观察孔。在web开发中，是这样解释viewport的：
1. Viewport就是移动设备浏览器上(也可能是一个app中的webview)用来显示网页的一块“画布”，也可能是矢量图（VectorDrawable）中定义的绘制图的一块“画布”.
2. 移动设备的浏览器都有viewport元标签，而引入viewport的目的就是用于解决PC页面能在手机上正常显示，不会因屏幕变小而挤压布局导致页面排版混乱的问题。
3. 在引入了Viewport概念并做如下规定后，就不会破坏那些没有针对手机浏览器优化的PC网页的布局，用户可以通过平移和缩放来看网页的其他部分。
4. [PPK](http://www.quirksmode.org/mobile/metaviewport/#t10)大神对于移动设备上的viewport有着非常多的研究，他认为移动设备上有三个viewport：layout viewport 、 visual viewport 和 ideal viewport
 1. layout viewport(布局视口): 这是移动设备引入的第一个Viewport。
 2. visual viewport(可视视口): 因为浏览器可视区域(visual viewport)的宽度比这个layout viewport的宽度要小，带来的后果就是浏览器会出现横向滚动条，所以我们还需要一个viewport来代表浏览器可视区域的大小，ppk把这个viewport叫做 visual viewport.
 3. ideal viewport(理想视口)： ideal viewport的宽度 = 屏幕的逻辑像素宽度
5. 矢量图里面的画布

VectorDrawable 可以通过 XML 文件创建，通过 < vector > element.

1. < vector > 用于创建一个矢量图（vector drawable）
 1. android:name： 定义这个矢量图的名字
 2. android:width： intrinsic(固有) size of the drawable,定义矢量图固有的宽度，支持各种格式的单位，常用是dp.
 3. android:height：同上
 4. android:viewportWidth：用来定义viewport的宽度，所谓viewport就是主要绘制路径的虚拟画布，无限大的画布. Viewport is basically the virtual canvas where the paths are drawn on.单位px.
 5. android:viewportHeight：同上
 6. android:tint：这个颜色值是是为矢量图着色的，没有默认设置的着色值
 7. android:tintMode：[着色模式](http://www.cnblogs.com/spring87/p/5779201.html)，默认src_in
 8. android:autoMirrored：表明矢量图是否需要反射，当他所在布局是RTL (right-to-left).
 9. android:alpha：不透明度

2. < group > 定义一组path路径或者数组，变形信息，变形信息跟Viewport一样通过坐标定义，变形适用于顺序，缩放，旋转和平移
 1. android:name ：这组的名字
 2. android:rotation：旋转的角度
 3. android:pivotX ：执行各种动画的中心轴的x坐标，缩放和旋转的中心轴的x坐标，在Viewport里面定义.
 4. android:pivotY ：同上
 5. android:scaleX ：在x坐标上的缩放比例大小
 6. android:scaleY ：同上
 7. android:translateX ：在x坐标上的平移大小，在Viewport里面定义.
 8. android:translateY ：同上

3. < path > 定义绘制的路径
 1. android:name ： path的名字
 2. android:pathData ：定义路径的data，格式类似于矢量图（SVG）的属性’d’，定义在Viewport距离.
 3. android:fillColor ：定义填充路径的颜色，可以是一个色值，对于 SDK 24+, 可以是 color state list or a gradient color.如果这个属性被动画属性设置，值都会覆盖原来的值 ，如果没有定义，则不会设置.
 4. android:strokeColor ：定义路径轮廓线的颜色，其他同上
 5. android:strokeWidth ：路径轮廓的宽度
 6. android:strokeAlpha ：路径轮廓的透明度
 7. android:fillAlpha ： 填充路径的不透明度
 8. android:trimPathStart ：从开始部分小部分修剪，范围0-1
 9. android:trimPathEnd ： 同上
 10. android:trimPathOffset ：修剪平移部分 ，范围0-1
 11. android:strokeLineCap ：设置轮廓结束时候线帽: butt, round, square.
 12. android:strokeLineJoin :设置两条线交汇处的图形: miter,round,bevel.
 13. android:strokeMiterLimit ：交点处限制
 14. android:fillType ：相当于SVG的"fill-rule"属性，[详见](https://www.w3.org/TR/SVG/painting.html#FillRuleProperty)

4. < clip-path > 定义当前剪切路径，只运用于当前group和它的children.

下面是一个简单VectorDrawable，vectordrawable.xml 的实例：

```

<vector xmlns:android="http://schemas.android.com/apk/res/android"
     android:height="64dp"
     android:width="64dp"
     android:viewportHeight="600"
     android:viewportWidth="600" >
     <group
         android:name="rotationGroup"
         android:pivotX="300.0"
         android:pivotY="300.0"
         android:rotation="45.0" >
         <path
             android:name="v"
             android:fillColor="#000000"
             android:pathData="M300,70 l 0,-70 70,70 0,0 -70,70z" />
     </group>
 </vector>

```

### 主要语法

SVG Path Data：
主要有以下一些命令

* M： move to 移动绘制点
* L：line to 直线
* Z：close 闭合
* C：cubic bezier 三次贝塞尔曲线
* Q：quatratic bezier 二次贝塞尔曲线
* A：ellipse 圆弧

每个命令都有大小写形式，大写代表后面的参数是绝对坐标，小写表示相对坐标。参数之间用空格或逗号隔开

命令详解：

* M (x y) 移动到x,y
* L (x y) 直线连到x,y，还有简化命令H(x) 水平连接、V(y)垂直连接
* Z，没有参数，连接起点和终点
* C(x1 y1 x2 y2 x y)，控制点x1,y1 x2,y2，终点x,y
* Q(x1 y1 x y)，控制点x1,y1，终点x,y
* A(rx ry x-axis-rotation large-arc-flag sweep-flag x y)
rx ry 椭圆半径
* x-axis-rotation x轴旋转角度
* large-arc-flag 为0时表示取小弧度，1时取大弧度
* sweep-flag 0取逆时针方向，1取顺时针方向

有个图解：

![](http://www.w3.org/TR/SVG11/images/paths/arcs02.svg)

这些语法基本不常用，直接用工具就可以把svg格式图片装换成VectorDrawable了，可以直接使用了.

### 项目使用

由于VectorDrawable是在5+ (Lollipop; API Level 21+)以后才支持的新API，所以为了兼容低版本的设备，就需要使用一些封装好的第三方库来进行开发了，如果应用群体设备分布在5.0+，那就基本不用考虑兼容性问题了，毕竟现在5.0+设备分布还是很多的。

Android (推荐下面两个第三方库):

SVG: https://github.com/trello/victor

Vector Drawables: https://github.com/telly/MrVector



参考：https://medium.com/@webalys/die-png-die-how-to-use-vector-icons-in-your-apps-d884c9c63e93#.bhnmmsd3f
