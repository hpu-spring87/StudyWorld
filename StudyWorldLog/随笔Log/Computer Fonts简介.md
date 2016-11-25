# Computer Fonts
> Computer Fonts是一系列以特殊文件格式存储的文件的简称，它包含字形，字符，特殊符号等。

三种常见基础字体格式：

- **位图字体：** 位图字体的外形和尺寸由每个字形的图像的点或像素的矩阵组成。
- **矢量字体：** 矢量字体使用贝塞尔曲线，绘图指令和数学公式来描述每个字形，这使字符轮廓可扩展到任何大小。通用标准是（仍然是）Adobe PostScript。常见的是PostScript类型1和类型3字体，Truetype字体（ttf）和OpenType字体（otf）。
- **笔画字体:** 笔画字体使用一系列指定的笔画和附加信息来定义特定展示的轮廓或线的大小和形状，这些字体一起描述字形的外观。

位图字体在计算机代码中更快更容易使用，但不可扩展，每个大小需要单独的字体。矢量和笔画字体可以使用单个字体调整大小，并用不同的测量替换每个字形的组件，但在屏幕上比位图字体更复杂，因为它们需要额外的计算机代码将轮廓渲染为位图以显示屏幕或打印。虽然所有类型都仍在使用，但在计算机上看到和使用的大多数字体是矢量字体。

光栅图像可以以不同的大小显示，只有一些失真，但快速渲染;矢量和笔画图像格式是可调整大小的，但是需要更多的时间来渲染，因为每次显示时必须从头开始绘制像素。

字体可以是等宽的（即，每个字符被绘制成与前一个字符的恒定距离，它在下一个绘制时）或者比例（每个字符具有其自己的宽度）。然而，特定的字体处理应用程序可以影响间距，特别是当做对齐时。

## 1.矢量字体格式
### Type 1 and Type 3 fonts

>Type 1和Type 3字体由Adobe开发用于专业数字排版。使用PostScript，字形是用三次贝塞尔曲线描述的轮廓字体。 Type 1字体仅限于PostScript语言的一个子集，并且使用Adobe的提示系统，以前非常昂贵。类型3允许不受限制地使用PostScript语言，但不包括任何提示信息，这可能导致低分辨率设备（例如计算机屏幕和点阵打印机）上的可见渲染伪像。

### TrueType font
>即是简称.ttf的字体，TrueType字体在20世纪80年代由Apple和Microsoft创建，作为在两个不同操作系统和大多数打印机之间通用的字体解决方案。它旨在替换Type 1字体，其中许多人觉得太贵了。与类型1字体不同，TrueType字形用二次贝塞尔曲线描述。它目前非常流行，所有主要操作系统都存在实现。

### OpenType font
>即是简称.otf的字体，OpenType是由Adobe和Microsoft设计的smartfont系统。Opentype字体扩展了可用字符的数量（每个字体可以容纳多达65,000！），并支持连字，小帽，替代字符，花边等附加功能。 OpenType字体包含TrueType或Type 1（实际上是CFF）格式的大纲以及大量的元数据。

## 2.笔画字体格式
>METAFONT使用不同类型的字形描述。像TrueType一样，它是一个矢量字体描述系统。它使用通过沿着由立方贝塞尔样条和直线段制成的路径移动由多边形近似的多边形或椭圆笔而产生的笔划，或通过填充这样的路径来绘制字形。虽然当敲击路径时，笔划的包络从未实际生成，但是该方法不会导致精度或分辨率的损失。

## OTF VS TTF

> (OpenType Fonts) VS (TrueType Font)

总而言之，OTF继承自TTF，允许更多的排版特性和特殊字符，导致我们相信，如果你是一个设计师购买字体，OTF可能是更好的方式，OTF的功能包括连字和替代字符（也称为字形），存在给设计师更多的选择。如果你需要一个基本的日常字体，TTF可能是你的选择。如果你需要最高水平的字体再现质量可能，试验和真正的PostScript字体将是最有益的。

## Android中Font

> Android中可以为了TextView展示不同风格的页面而使用各种各样字体，放在assets目录引用即可。这里不再多说。

### Android利用字体定义格式化的icon

* 自己定义一套ttf或者otf的字体，字体里面导入对应的格式化的矢量图片，如下：
![添加图片到字体](http://images2015.cnblogs.com/blog/535280/201611/535280-20161125100446659-1890232534.jpg)

* 编辑对应icon字体信息，如下：
![编辑字体信息](http://images2015.cnblogs.com/blog/535280/201611/535280-20161125100521534-1550842832.jpg)

* 在代码中使用这个字体中对应矢量图icon，如下：
用TextView的setText设置图标， setTextSize设置大小， 用TextColor设置图标颜色 ，只要能显示String的控件，都可以用。

```

<?xml version="1.0" encoding="utf-8"?>
<LinearLayout xmlns:android="http://schemas.android.com/apk/res/android"
    android:layout_width="match_parent"
    android:layout_height="match_parent"
    android:orientation="vertical"
    android:padding="10dp"
    xmlns:app="http://schemas.android.com/apk/res-auto"
    >

   <android.support.v7.widget.AppCompatTextView
       android:layout_width="match_parent"
       android:layout_height="wrap_content"
       android:layout_marginTop="10dp"
       android:drawableLeft="@drawable/shopping_res"
       android:text="测试"/>

     <com.github.johnkil.print.PrintView
       android:id="@+id/icon"
       android:layout_width="wrap_content"
       android:layout_height="wrap_content"
       android:layout_gravity="center"
       android:contentDescription="@string/ic_adb_description"
       app:print_iconColor="@color/icon"
       app:print_iconSize="180dp"
       app:print_iconText="@string/ic_material_access_alarms" />

</LinearLayout>

```

下面附上:

[Android-Icon-Fonts](https://github.com/johnkil/Android-Icon-Fonts)
