# .Android View官方文档

### Using Views
<font color="#768909">Note: The Android framework is responsible for measuring,laying out and drawing views. You should not call methods that perform these actions on views yourself unless you are actually implementing a ViewGroup.</font>
```
Android framework层会负责对View的测量，放置和绘制，自己不需要手动
设置它的位置，除非是自定义ViewGroup.

```
### Implementing a Custom View

To implement a custom view, you will usually begin by providing overrides for some of the standard methods that the framework calls on all views. You do not need to override all of these methods. **In fact, you can start by just overriding onDraw(android.graphics.Canvas)**.

### IDs

View IDs need not be unique throughout the tree, but it is good practice to ensure that they are at least unique within the part of the tree you are searching.

### Position

The geometry(几何) of a view is that of a rectangle（矩形）. A view has a location, expressed as a pair of left and top coordinates（坐标）, and two dimensions（大小）, expressed（表达） as a width and a height. The unit for location and dimensions is the pixel.
```
getLeft() and getTop()
获取标示这个view的矩形的left或者X坐标
获取标示这个view的矩形的top或者Y坐标
这些坐标都是相对于他们父View的.
当然也有 getRight() and getBottom()
此时：getRight()  =  getLeft() + getWidth()；

```
### Size, padding and margins
关于Size，View对应两组大小的width和heigh：

1.第一组就是我们所说的 measured width and measured height，他们的大小定义一个view在父view中的大小，可以通过下面两个方法获取他们大小：
```

getMeasuredWidth() and getMeasuredHeight().

```
2.第二组就是我们所说的width and height, 或者叫drawing width and drawing height.这个大小是这个view在屏幕，以及绘制过程和在布局中的实际大小，与上面区别开，可以通过下面方法获取他们大小：
```
 getWidth() and getHeight().

```
**上面两组不同宽度之所以存在差别应该主要在于padding导致的.**

尽管View可以定义padding，但是它不支持margins，好在Viewgroup对margins提供支持，可以通过view的setLayoutParams来间接设置margins.

### Layout
<p>
Layout(布局) is a two pass process: a measure pass and a layout pass. The measuring pass is implemented in measure(int, int) and is a top-down（自顶向下） traversal（遍历） of the view tree. Each view pushes dimension specifications down the tree during the recursion（递归）. At the end of the measure pass, every view has stored its measurements（测量值）. The second pass happens in layout(int, int, int, int) and is also top-down. During this pass each parent is responsible for positioning all of its children using the sizes computed in the measure pass.
</p>

<p>
The measure pass uses two classes to communicate dimensions. The **View.MeasureSpec** class is used by views to tell their parents how they want to be measured and positioned. The base **LayoutParams** class just describes how big the view wants to be for both width and height. For each dimension, it can specify one of:
</p>

*  an exact number
*  MATCH_PARENT, which means the view wants to be as big as its parent (minus padding)
*  WRAP_CONTENT, which means that the view wants to be just big enough to enclose its content (plus padding).

###  Drawing

The tree is largely recorded and drawn in order, with parents drawn before (i.e., behind) their children, with siblings drawn in the order they appear in the tree. If you set a background drawable for a View, then the View will draw it before calling back to its onDraw() method. The child drawing order can be overridden with custom child drawing order in a ViewGroup, and with setZ(float) custom Z values} set on Views.

To force a view to draw, call **invalidate()**.


### Event Handling and Threading

View基础循环如下：

1.一个event触发然后分发给恰当的view，这个view处理event以及对应的各种监听.

2.如果在处理event的过程中，view的边界可能变化，这时候会调用方法： requestLayout().

3.如果在处理event的过程中，view展示可能发生变化，需要重绘，这时候会调用方法：invalidate().

4.requestLayout()和invalidate()其中之一被调用的时候，framework会适当的 measuring, laying out, and drawing the tree

<p><font color="#768909">
Note: The entire view tree is single threaded. You must always be on the UI thread when calling any method on any view. If you are doing work on other threads and want to update the state of a view from that thread, you should use a Handler.<font></p>

```
整个View树是一个线程，必须在UI线程中进行，如果调用view的方法，如果在非UI线程，可以用Handler处理.

```

### Focus Handling

framework通过处理焦点的移动来处理与用户的交互，比如：view移除或者隐藏会改变view的焦点，新的view获取焦点，焦点的移动基于最近方向上的相邻的view的算法，默认的算法可能满足不了开发者的需求，这时候可以在XML中手动设置一些属性：
```
nextFocusDown
nextFocusLeft
nextFocusRight
nextFocusUp

```
### Security

可以过滤恶意程序的一些操作：
onFilterTouchEventForSecurity(MotionEvent) method to implement your own security policy.

# .Android ViewGroup官方文档

###
