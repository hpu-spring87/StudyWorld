# Android Interview Questions

## 基础随问

### 1. What is Android?

Android is a stack of software for mobile devices which includes an Operating System, middleware and some key applications. The application executes within its own process and its own instance of Dalvik Virtual Machine.

> Android是用于移动设备的一系列软件，包括操作系统，中间件和一些关键应用程序。该应用程序在其自身的进程中执行，并且它自己的Dalvik虚拟机实例。

### 2.Describe Android application Architecture?

Android application architecture has the following components.They are as follows −

1.Services − It will perform background functionalities

2.Intent − It will perform the inter connection between activities and the data passing mechanism

3.Resource Externalization − strings and graphics

4.Notification − light,sound,icon,notification,dialog box,and toast

5.Content Providers − It will share the data between applications

>Android应用架构由以下组件构成：
1. Services：执行一些后台运行的功能
2. Intent：进行Activity和数据传递机制之间的关联，主要是传递数据机制
3. Resource Externalization：strings and graphics（图像资源，包括图片，视频等）
4. Content Providers ：主要在应用之间进行共享数据

### 3.What is An Activity?

Activity performs actions on the screen.If you want to do any operations, we can do with activity

>Activity主要用于应用程序与用户进行交互，如果需要一些交互操作，那么你可以使用Activity来实现

### 4.What is the APK format?

The Android packaging key is compressed with classes,UI's, supportive assets and manifest.All files are compressed to a single file is called APK.

>Android工程各个包里面Java文件被转换为class文件，UI，以及其他的辅助资源文件和manifest，这些文件一起被压缩为一个单一的文件即APK文件，类似zip,可以改后缀被解压

### 5.What is An Intent?

It is connected to either the external world of application or internal world of application ,Such as, opening a pdf is an intent and connect to the web browser.etc.

>它可以连接到外部应用程序，也可以连接到应用程序的内部，例如，打开pdf是一个Intent，连接到web browser等等

### 6.What is an explicit（明确的） Intent?

Android Explicit intent specifies the component to be invoked from activity. In other words, we can call another activity in android by explicit intent.

>Android Explicit Intent 指定要从Activity中调用的组件(这里指Activity)。换句话说，我们可以通过Explicit intent在android中调用另一个Activity

### 7.What is an implicit(隐式的) Intent?

Implicit Intent doesn't specifiy the component. In such case, intent provides information of available components provided by the system that is to be invoked.

>隐式的Intent不指定组件，这样一来，Intent提供由系统提供的可被调用的可用组件的信息。
例如，Intent只提供Intent Filter，让系统自动筛选那些组件符合要求，就调用那些组件。

### 8.What is An android manifest file?

Every application must have an AndroidManifest.xml file (with precisely that name) in its root directory. The manifest file presents essential information about your app to the Android system, information the system must have before it can run any of the app's code.

>每个应用程序必须在其根目录中具有一个AndroidManifest.xml文件（具有该名称）。 清单文件将您的应用程序的基本信息提供给Android系统，系统必须具有这些必要信息才能运行任何应用程序的代码。

### 9.What language does android support to develop an application?

Android applications has written using the Java，Scala，Kotlin(Android SDK) and C/C++(Android NDK).

### 10.What is viewGroup in android?

View group is a collection of views and other child views, it is an invisible part and the base class for layouts.

>...它是不可见的，是所有layouts的基类。

### 11.What is a service in android?

The Service is like as an activity to do background functionalities without UI interaction.

>Service类似于一个没有UI交互的在后台运行各种功能的Activity,一种特殊的Activity

### 12.What is a content provider in android?

A content provider component supplies data from one application to others on request. Such requests are handled by the methods of the ContentResolver class. A content provider can use different ways to store its data and the data can be stored in a database, in files, or even over a network.

>content provider组件根据请求将数据从一个应用程序提供给另外一个应用程序。 这些请求由ContentResolver类的方法处理。 content provider可以使用不同的方式存储其数据，并且数据可以存储在数据库，文件中，甚至存储在网络中。

### 13.What are the notifications available in android?

Toast Notification − It will show a pop up message on the surface of the window

Status Bar Notification − It will show notifications on status bar

Dialogue Notification − It is an activity related notification.

### 14.What is container in android?

The container holds objects,widgets,labels,fields,icons,buttons.etc.

>Container持有objects,widgets（小部件）,labels（标签，在xml文件布局的时候用标签）,fields,icons,buttons.etc.这里要说明一下container与layouts的区别：Containers是包含动态内容的Views比Layouts更特殊，它不必继承与Layout，有些间接继承与ViewGroup，比如Listview，也有不继承的如VideoView，Container label在Android studio中使用。Container实现更具体的更高级别的tasks，这就是为什么他们对能够接受多少和哪一种children有强烈要求的原因。其中一些甚至使用适配器类。Layouts全部是直接扩展ViewGroup的通用ViewGroup，一般后缀都是Layout，比如LinearLayout，RelativeLayout，他们没有要求他们可以管理的childen的种类。

### 15.What is ADB in android?

It is acts as bridge between emulator and IDE, it executes remote shell commands to run applications on an emulator

>它作为模拟器和IDE之间的桥梁，它可以执行远程shell命令以在模拟器上运行应用程序

### 16.What is ANR in android?

ANR stands for application is not responding, basically it is a dialog box that appears when the application is not responding.

>Application Not Responding(ANR)代表应用程序没有响应，基本上是一个对话框，当应用程序没有响应时出现。当应用程序的UI线程长时间阻塞的时候，会触发ANR，如果应用程序在前台运行，系统会弹出一个dialog，提示用户是否关强制关闭应用，或者继续等待。

ANR具体描述以及避免方法参考[https://developer.android.com/topic/performance/vitals/anr.html](https://developer.android.com/topic/performance/vitals/anr.html)

### 17.What is an Adapter in android?

The Adapter is used to create child views to represent the parent view items.

>Adapter用于创建子视图，来代表父视图的条目。

### 18.What is shared preferences in android?

Shared preferences are the simplest mechanism to store the data in XML documents.

>Shared preferences是将数据存储在XML文件中的最简单的机制。

### 19.What are the key components（构件）in android architecture?

* Linux Kernel
* Libraries
* Android Framework
* Android applications.

### 20.What is a Sticky Intent in android?

Sticky Intent is also a type of intent which allows the communication between a function and a service for example,sendStickyBroadcast() is perform the operations after completion of intent also.

An intent that is used with sticky broadcast, is called as sticky intent. This intent will stick with android system for future broadcast receiver requests.

>Sticky Intent是一种可以在函数和service之间通信的Intent，例如：sendStickyBroadcast()在Intent完成之后执行对应的操作。

>在sticky broadcast里使用的Intent被叫做sticky intent，它会与系统一起存在，以便将来广播接收器请求。

### 21.Why can't you run java byte code on Android?

Android uses DVM (Dalvik Virtual Machine ) or ART rather using JVM(Java Virtual Machine), if we want, we can get access to .jar file as a library.

>由于Android是基于DVM（ART）运行应用，而不是JVM，所以不能直接调用byte code，如果需要使用，可以把byte code封装为jar包进行调用。

### 22.How does android track the application on process（进程）?

Android provides a Unique ID to all applications is called as Linux ID,this ID is used to track each application.

>Android为每个应用提供一个唯一ID作为Linux ID，可以用这个ID去追踪每个应用。

### 23.What is fragment in android?

Fragment is a piece of activity, if you want to do turn your application 360 degrees, you can do this by fragment.

>Fragment是Activity的一部分，如果需要构建旋转360度的应用，那么可以使用Fragment来实现。

### 24.What is sleep mode in android?

Sleep mode mean CPU will be sleeping and it doesn't accept any commands from android device except Radio interface layer and alarm.

>Sleep mode模式下，CPU将会休眠，不接受来自Android设备的任何指令，除了无线界面层（RIL）和闹铃。
扩展：Android的RIL层主要分成两个部分：RIL Daemon和Vendor RIL。RIL Daemon由C/C++写成，负责透过socket承接来自于Java框架的请求，并且将请求找到对应的函数后转往Vendor RIL。另外也负责将来自Vendor RIL的回应回报给Java框架。Vendor RIL为各数据芯片的供应商所提供，RIL Daemon和Vendor RIL有一个统一的函式接口，定义于RIL Daemon，如此可以使Android系统轻松抽换底层的硬件。Vendor RIL负责承接来自于RIL Daemon的指令，将之转换成调制解调器可以接受的海斯命令集指令后，传递到数据芯片所对应到专属的频道。另外，也会负责监听各数据频道以获得调制解调器回应的指令，并将之做简单的解析后传回到RIL Daemon。

## 必要15问

### 1.There are four Java classes related to the use of sensors on the Android platform. List them and explain the purpose of each.

The four Java classes related to the use of sensors on the Android platform are:

* Sensor: Provides methods to identify which capabilities are available for a specific sensor.（提供确认哪些功能可用于特定传感器的方法）

* SensorManager: Provides methods for registering sensor event listeners and calibrating sensors.（提供用于注册传感器事件监听和校准传感器的方法。）

* SensorEvent: Provides raw sensor data, including information regarding accuracy.（提供原始传感器数据，包括有关精度的信息。）

* SensorEventListener: Interface that defines callback methods that will receive sensor event notifications.（定义将接收传感器事件通知的回调方法的接口）

### 2.What is a ContentProvider and what is it typically used for?

A ContentProvider manages access to a structured set of data. It encapsulates the data and provide mechanisms for defining data security. ContentProvider is the standard interface that connects data in one process with code running in another process.(ContentProvider管理对结构化数据集的访问。 它封装了数据并提供了定义数据安全性的机制。 ContentProvider是将一个进程中的数据与另一进程中运行的代码相连接的标准接口。)

### 3.Under what condition could the code sample below crash your application? How would you modify the code to avoid this potential problem? Explain your answer.

```
    Intent sendIntent = new Intent();
    sendIntent.setAction(Intent.ACTION_SEND);
    sendIntent.putExtra(Intent.EXTRA_TEXT, textMessage);
    sendIntent.setType(HTTP.PLAIN_TEXT_TYPE); // "text/plain" MIME type
    startActivity(sendIntent);
```

隐式Intent指定可以调用设备上能够执行该操作的任何应用程序的操作。 当你的应用程序无法执行操作但其他应用程序可能可以使用隐式Intent时很有用。 如果有多个注册的应用程序可以处理此请求，系统将提示用户选择要使用哪个应用程序来执行该Intent。

但是，也有可能没有可以处理该Intent的应用程序。 在这种情况下，调用startActivity（）时，应用程序将会崩溃。 为了避免这种情况，在调用startActivity（）之前，应首先确保系统中至少有一个可以处理该Intent的应用程序。 要做到这一点，可以使用intent的resolveActivity（）方法来确认非空：

```
  // Verify that there are applications registered to handle this intent
  // (resolveActivity returns null if none are registered)
    if (sendIntent.resolveActivity(getPackageManager()) != null) {
        startActivity(sendIntent);
    } 
```

### 3.The last callback in the lifecycle of an activity is onDestroy(). The system calls this method on your activity as the final signal that your activity instance is being completely removed from the system memory. Usually, the system will call onPause() and onStop() before calling onDestroy(). Describe a scenario(场景), though, where onPause() and onStop() would not be invoked.

如果在onCreate()里面调用finish()方法，那么onPause()和onStop()将不会调用，这种情况是可能发生的，例如，在onCreate()出现错误的时候触发finish()方法，这种情况下，在onPause()和onStop()里做的一些释放一些不需要的资源的操作都不会执行。

尽管onDestroy()是在Activity的生命周期最后被调用的，但是这里要注意一下，它并不是每次都会被调用的，尽量避免在onDestroy()里面执行释放资源的操作，建议的做法，是在
OnStart()和OnResume里面执行获取资源的操作，在OnStop()和OnPause()里面进行引用资源的释放。

### 4.Describe three common use cases for using an Intent.

Common use cases for using an Intent include:

* To start an activity: You can start a new instance of an Activity by passing an Intent to startActivity() method.

* To start a service: You can start a service to perform a one-time operation (such as download a file) by passing an Intent to startService().

* To deliver a broadcast: You can deliver a broadcast to other apps by passing an Intent to sendBroadcast(), sendOrderedBroadcast(), or sendStickyBroadcast().

### 5.Suppose that you are starting a service in an Activity as follows:

```
Intent service = new Intent(context, MyService.class);             
startService(service);
```
where MyService accesses a remote server via an Internet connection.
If the Activity is showing an animation that indicates some kind of progress, what issue might you encounter and how could you address it?

由于网路延迟，负载，远程service处理和响应请求所需的时间等其他原因，远程service通过Internet响应通常需要一些时间，因此，如果发生这样的延迟，当客户端等待服务响应的时候，在Activity中的动画，或者更糟糕的整个UI线程可能阻塞，这是因为该service是在UI线程启动的，为了避免这种情况，可以在后台线程中启动service，或者业务逻辑允许，可以异步响应。

### 6. 通常情况下当屏幕方向改变的时候，Android会销毁前台页面，重置，重置后会恢复之前页面布局的所有值，但是，有时候有些View没有被恢复，如何确认这个View？

这时可以通过判断该View是否有id来判断，因为系统还原Activity状态的时候，每个View都是通过id进行恢复的，对应布局的android:id属性。

### 7.What is difference between Serializable and Parcelable ? Which is best approach in Android ?

Serializable是一个标准的Java接口，可以通过实现这个接口，来简单的标记一个类序列化，Java会在某些情况下自动序列化它。

Parcelable是一个特殊的Android接口，可以自己实现序列化，它比Serializable更高效，并且解决了Java默认序列化方案的一些问题。

### 8.What are “launch modes”? What are the two mechanisms by which they can be defined? What specific types of launch modes are supported?

“Launch Modes”是将新启动的Activity与当前task进行关联的方式。

“Launch Modes”可以使用以下两种机制之一进行来定义：

1. “Manifest file”，当定义一个Activity的时候，可以在“Manifest里面定义该Activity与task如何关联，有以下四种值可以设置。

* standard（默认值），该模式下面，Activity可以有多个实例，这些实例可以在同一个task中，也可以在不同的task中，这是应用里面最常见的启动模式。

* singleTop，与standard不同的是，如果Activity实例已经存在当前的task的顶部，并且系统的路由Intent是关联到该Activity，则不会创建新的实例，因为此时会触发onNewIntent()方法而不是新建一个实例。

* singleTask，会新建一个task，同时实例化一个Activity作为该task的root。但是，如果在任意task中，如果已经存在该Activity的实例的话，系统路由将会通过onNewIntent()方法把Intent与该实例进行关联。在此种模式下，Activity实例可以存在同一task，此模式适用于作为入口的Activity。

*singleInstance，与singleTask类似，不能在singleInstance实例的task里面推入其他Activity实例，因此，具有此种启动模式的Activity一般都是在一个单独的task中，这是一种非常特殊的模式，一般应用于单个Activity作为整个应用。

2. “Intent flags”. 调用startActivity()的时候，可以在Intent里面添加一个Flag用来声明Activity与当前task如何关联。支持以下值：

* FLAG_ACTIVITY_NEW_TASK. 与singleTask一样。 

* FLAG_ACTIVITY_SINGLE_TOP. 与singleTop一样。

* FLAG_ACTIVITY_CLEAR_TOP. 如果该Activity已经启动并且在当前task运行，则不会创建新的实例，所有其他在该Activity顶部的都将会被销毁，并将此Intent通过onNewIntent()关联到该恢复的实例（现在在task顶部）中，方法一在Manifest声明不能实现此种效果。此种Flag的适用场景是异地登录，登陆成功进入首页的时候，会把所有页面清空，并且复用之前的首页场景。

**未完待续...**







