# Android Fragment简介

## Fragment有两种实现方式：
* **framework version：** framework's 通过静态库实现Fragment，主要为了运行在Android 3.0以及以上的平台.
* ** support version：** 通过support包里面实现的Fragment.

二者主要区别：
* 如果用support里面的fragment，activity必须继承于FragmentActivity

* 如果用support里面的fragment，必须通过getSupportFragmentManager() 来获取 FragmentManager实例.

![生命周期](http://static.open-open.com/lib/uploadImg/20160513/20160513154759_455.png)

相对于Activity，Fragment的生命周期有以下几点不同：

onAttach(Activity)

当Fragment与Activity发生关联时调用

onActivityCreated(Bundle)

当Activity的onCreate方法返回时调用

onDetach()

与onAttach相对应，当Fragment与Activity关联被取消时调用

**注意：除了onCreateView，其他的所有方法如果你重写了，必须调用父类对于该方法的实现**

Activity中有个FragmentManager，其内部维护fragment队列，以及fragment事务的回退栈。

当Activity因为配置发生改变（屏幕旋转）或者内存不足被系统杀死，造成重新创建时，需要对fragment做判空处理，我们的fragment会被保存下来，但是会创建新的FragmentManager，新的FragmentManager会首先会去获取保存下来的fragment队列，重建fragment队列，fragment manager可能会尝试通过反射机制重新创建这个fragment类的实例，从而恢复之前的状态。

**Fragment事务（FragmentTransaction）**

Fragment事务使得你可以执行一系列fragment操作，不幸的是，提交事务是异步的，而且是附加在主线程handler队列尾部的。当你的app接收到多个点击事件或者配置发生变化时，将处于不可知的状态。

**FragmentPagerAdapter：** 对于不再需要的fragment，选择调用detach方法，仅销毁视图，并不会销毁fragment实例。

**FragmentStatePagerAdapter：** 会销毁不再需要的fragment，当当前事务提交以后，会彻底的将fragmeng从当前Activity的FragmentManager中移除，state标明，销毁时，会将其onSaveInstanceState(Bundle outState)中的bundle信息保存下来，当用户切换回来，可以通过该bundle恢复生成新的fragment，也就是说，你可以在onSaveInstanceState(Bundle outState)方法中保存一些数据，在onCreate中进行恢复创建。

如上所说，使用FragmentStatePagerAdapter当然更省内存，但是销毁新建也是需要时间的。一般情况下，如果你是制作主页面，就3、4个Tab，那么可以选择使用FragmentPagerAdapter，如果你是用于ViewPager展示数量特别多的条目时，那么建议使用FragmentStatePagerAdapter。

## Fragment常见异常

```
java.lang.IllegalStateException: Can not perform this action after onSaveInstanceState
at android.app.FragmentManagerImpl.checkStateLoss(FragmentManager.java:1331)
at android.app.FragmentManagerImpl.enqueueAction(FragmentManager.java:1349)
at android.app.BackStackRecord.commitInternal(BackStackRecord.java:735)
at android.app.BackStackRecord.commit(BackStackRecord.java:711)
at com.dighammer.kisson.testfragment.MainActivity$1.run(MainActivity.java:30)
at android.os.Handler.handleCallback(Handler.java:739)
at android.os.Handler.dispatchMessage(Handler.java:95)
at android.os.Looper.loop(Looper.java:135)
at android.app.ActivityThread.main(ActivityThread.java:5273)
at java.lang.reflect.Method.invoke(Native Method)
at java.lang.reflect.Method.invoke(Method.java:372)
at com.android.internal.os.ZygoteInit$MethodAndArgsCaller.run(ZygoteInit.java:908)
at com.android.internal.os.ZygoteInit.main(ZygoteInit.java:703)

当程序界面显示出来后，按home键，过接近5秒后，就会出现该奔溃日志。
原因是FragmentTransaction中的commit方法必须在onSaveInstanceState之前调用。
那么如何解决了？在FragmentTransaction中提供了commitAllowingStateLoss方法，通过调用该方法就不用关心Activity的状态是否保存。

```


```
Fragment中套有另一个Fragment，当第二次进入父Fragment时或者由Fragment创建的界面时会抛异常，大致意思是子Fragment的Id或Tag重复了。如果你在layout中给子fragment加了id或者tag，那么一定会遇到此异常。

在添加Fragment时都可以为Fragment指定一个Id或者Tag用以标识这个Fragment。因为每个Activity所附带的Fragment都是放在一个对象池中，在Activity的生命周期里，Fragment仍然在池中，即使是把某一个Fragment从Activity中detach掉（也即用FragmentManager pop掉），这个池是由FragmentManager来管理的。当你再次要以某个id或者Tag添加Fragment时，FragmentManager会在池中检索，如果发现已经存在Fragment对象带有此Id或者Tag时，就会抛此异常并报怨Id重复。这么做的目的就是减少对象的创建，尽可以的复用对象。

如何破解：
在布局中写fragment时，不要添加id或者tag；
如果非要添加id或者tag，就在代码中添加fragment，如使用Id或者Tag时，先到FragmentManager中查找对象是否存在，不存在时再创建。

```

fragment销毁只是界面的销毁，他的数据还是会保留在内存中的，当fragment进行切换的时候，前一个fragment的ui会销毁掉，但是数据不会丢失。所以当一个fragment不再需要的时候尽量的把数据也清空。
