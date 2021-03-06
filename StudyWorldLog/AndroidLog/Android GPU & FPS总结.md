# Android GPU & FPS总结

### Android 之 GPU

> Android设备开发者选项里面可以选择打开，GPU过度绘制,怎么使用呢？

* 显示GPU过度渲染，从最美到最差依次是: 蓝，绿，淡红，红

1. 没有颜色意味着没有透支。像素只画了一次

2. 蓝色 : 意味着透支1倍。像素绘制了2次

3. 绿色：意味着透支2倍。像素绘制了3次

4. 淡红：意味着透支3倍。像素绘制了4次

5. 红：意味着透支4倍。像素绘制了5次或者更多

我们的目标就是尽量减少红色的Overdraw，看到更多的蓝色区域。

Overdraw有时候是因为你的UI布局存在大量重叠的部分，还有的时候是因为非必须的重叠背景。例如某个Activity有一个背景，然后里面的Layout又有自己的背景，同时子View又分别有自己的背景。仅仅是通过移除非必须的背景图片，这就能够减少大量的红色Overdraw区域，增加蓝色区域的占比。这一措施能够显著提升程序性能。


### Android 之 FPS

> FPS（frames per second），对于Android而言，一个应用不仅要实现它的功能，还要有着良好的用户交互，何为良好？使用流畅，不感觉卡顿，不丢帧，不延迟。这既是 **60fps** 的基础要求。
![why 60fps?]()

> 在应用性能的世界里，你总能听见我们讨论60帧每秒和16毫秒的界限，但是你有么有停下来思考一下，为什么是这些数值？如果你是一个严格的程序员，那么这是一个值得研究的技术细节
，这些大部分都和硬件有关，人体硬件。人的眼睛和相机不同，你的眼睛并不会因为为了不让你装上新家具就向大脑发送这个世界的截图。相反，你的大脑会持续地处理你的眼睛传送可视图像。但是这里并没有帧和截图的概念。我们这种动作是有帧组合的概念。我们可以欺骗大脑，让他们以为眼前的帧就是动作。图像显示的速度的快慢直接影响着
动作的流畅性。至少24秒每帧，能基本让大脑认为他是一个动作，同时，24帧每秒对电影行业来说是个宝。因为他对展现动作来说已经足够了。同时价格也足够低，能满足电影制作的预算。
这也就是为什么过去50年你所看到的大部分电影都是24帧每秒的。现在30帧每秒对于电影来说已经足够了，但是没有华丽的影院效果。
>
事实上60帧每秒才是最棒的，不需要那些视觉效果，却依然精彩流畅。大部分人接受不了比这个更高的帧数。人的眼睛是很精确的，如果习惯了60帧，突然变成20帧，就会造成用户的紧张和不适。作为开发的你，你的目标就是保证你的应用在60帧每秒。并在用户体验期间，保持这个速度不变。

>现在60帧每秒就意味着身为开发者的你需要在16毫秒每帧的情况下完成所有的工作。包括输入，计算，网络工作和渲染。每一帧都要保持流畅。还有一大堆问题会导致你的帧超过16秒
为了找到问题并解决他们，这时候你就需要关注Android性能模式的内容了。


### 关于GPU以及FPS的渲染界面优化点

> 一般用户容易在UI执行动画或者滑动ListView，以及其他列表的时候感知到卡顿不流畅，是因为这里的操作相对复杂，容易发生丢帧的现象，从而感觉卡顿。有很多原因可以导致丢帧，也许是因为你的layout太过复杂，无法在16ms内完成渲染，有可能是因为你的UI上有层叠太多的绘制单元，还有可能是因为动画执行的次数过多。这些都会导致CPU或者GPU负载过重。 **我们可以通过一些工具来定位问题，比如可以使用HierarchyViewer来查找Activity中的布局是否过于复杂，也可以使用手机设置里面的开发者选项，打开Show GPU Overdraw等选项进行观察。你还可以使用TraceView来观察CPU的执行情况，更加快捷的找到性能瓶颈。**

**e袋洗项目优化点：**

> 为了减少过度绘制，首先我们要找到过度绘制根源：布局不合理，减少页面布局的层级，自定义view不合理等等，怎么检查呢？用Hierarchy viewer,Tracer 等工具，在'<sdk'>/tools/里面（这里注意Hierarchy viewer只能在非安全限制的工程机，平板电脑，和模拟器能够有效，如果正常的使用的商业机器，那你需要一个开源的库，然后引入到自己的项目中，即是ViewServer,开源地址：(https://github.com/romainguy/ViewServer)）.

1. Removing the window background：之所以这样做，是容易出现（multiple fullscreen backgrounds ：第一层是DecorView，Android系统生成的一个view，它的背景有主题设定），window的background是通过主题设置的，默认是invisible，设置主题的作用是为了预览布局文件的时候使用，你可以通过设置color / image来作为background，千万不要设置为null,除非你的应用是透明的.亦或在setContentView()之后设置getWindow().setBackgroundDrawable(null)来移除Activity默认来自Theme的背景，然后逐步检查其他层级的background，是否重复设置，移除它.

2. Flattening the view hierarchy：压缩view的层级，移除没有必要的view，优化ViewGroups的实现（LinearLayout的嵌套，用RelativeLayout替换实现相同效果），不仅能提高帧率还能减少内存的占用，启动时间等.

3. 相对于第一条而言，移除后，也可以通过选择Activity的不同Theme的主色调，从而有了默认背景颜色（一般就Light和Dark两种，即默认背景颜色为白，黑），然后布局文件不设置background，这样就不会因为background原因绘制多次.

4. 可以手动设置透明背景，从而减少过度绘制，比如ImageView加载完毕图片后，再手动设置他背景为透明：

 ```Java
Picasso.with(getContext()).load(chat.getAuthor().getAvatarId()).into(chat_author_avatar);
chat_author_avatar.setBackgroundColor(Color.TRANSPARENT);

 ```
同时也可以刻意把列表类的background移除掉，比如GridView，ListView,RecyclerView等的背景和他们Item的背景可能会设置重复，这时候就可以移除一个.当然如果遇见GridView需要根据自己和Item背景颜色不同，来展示分割线效果时候，这时候移除其中一个背景，就会看不到分割线效果了，这时候怎么办呢？难道不能移除了？当然可以，我们可以移除GridView的背景，保留Item的背景，然后Item的根布局用FrameLayout,然后设置4个高为1px的view来替代分割线的效果.
