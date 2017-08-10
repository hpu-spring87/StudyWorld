# Android DVM vs ART

来源：[https://android.jlelse.eu/closer-look-at-android-runtime-dvm-vs-art-1dc5240c3924](https://android.jlelse.eu/closer-look-at-android-runtime-dvm-vs-art-1dc5240c3924)
![](https://cdn-images-1.medium.com/max/2000/1*ClSMKlNwdXNTaLbRpHTqtg.jpeg)

### Runtime

用最简单的术语描述，它是由操作系统使用的系统，该系统负责将以高级语言编写的代码（如Java）转换为能被CPU/处理器理解的机器代码。Runtime包括在程序运行时执行的软件指令，即使它们本质上不是该软件特定的代码的一部分。

CPU或者更通俗的说我们的计算机只能理解机器语言（二进制代码），所以为了能在CPU上运行，代码必须转换为机器代码，这是由翻译器完成的。

翻译成机器码：

1.Assemblers（汇编）

它将汇编代码直接转换为机器代码，因此它非常快

2.Compilers（编译器）

它将代码转换为汇编代码，然后使用汇编器将代码翻译成二进制代码。 使用这个编译很慢，但执行速度很快。编译器最大的问题是所产生的机器代码与平台有关。 换句话说，在一台机器上运行的代码可能不会在不同的机器上运行。

3.Interpreters（翻译者）

它在执行代码时翻译代码。由于翻译发生在Runtime，执行速度很慢。

### How JAVA code execution works?

为了维护代码的平台独立性，Java开发了JVM，即Java虚拟机。开发的JVM每个平台都不一样，意味着JVM依赖于平台。Java编译器将.java文件编译成.class文件，即字节码，该字节码被JVM转换为机器码。这比解释速度更快，但比C ++编译慢。

### How Android code execution works?

在Android中，Java类被转换为DEX字节码。 DEX字节码格式通过ART或Dalvik运行时转换为本地机器代码。这里DEX字节码与设备架构无关。

Dalvik是一个JIT（Just in time）基于编译的引擎。 使用Dalvik有缺点，因此从Android 4.4（kitkat）ART被引入作为Runtime和从Android 5.0（Lollipop）它完全取代了Dalvik。 Android 7.0为Android Runtime（ART）添加了一个just-in-time（JIT）编译器和代码分析功能，可以在运行时不断提高Android应用的性能。

**要点：Dalvik使用JIT（Just in time）编译，而ART则使用AOT（Ahead of time）编译。**

以下解释了Dalvik虚拟机和Java虚拟机之间的区别:

![https://cdn-images-1.medium.com/max/1600/1*kWHICeg5bjl5Av1u-wzx3w.png](https://cdn-images-1.medium.com/max/1600/1*kWHICeg5bjl5Av1u-wzx3w.png)

### Just In Time (JIT)

用Dalvik JIT编译器，每次运行应用程序的时候，都会动态的把一部分Dalvik字节码转换为机器码，
随着执行的进行，更多的字节码被编译和缓存。由于JIT仅编译一部分代码，因此它具有较小的内存占用并且在设备上使用较少的物理空间。

### Ahead Of Time (AOT)

ART配备了Ahead-of-Time编译器。在应用程序的安装阶段，它将DEX字节码静态地转换为机器代码并存储在设备的存储中。这是在应用程序安装在设备上时发生的一次性事件。不需要JIT编译，代码执行得更快。

由于ART直接（本地执行）运行应用程序机器代码，因此它不会像Dalvik上的just-in-time代码编译一样关心CPU的占用。由于较少的CPU使用量导致更少的电池耗尽。

![DVM vs ART](https://cdn-images-1.medium.com/max/1600/1*pRQ0ygtGiskGSsiHrCROrw.png)

ART跟Dalvik使用相同的DEX字节码。使用ART编译的应用程序在安装应用程序时需要额外的时间进行编译，并占用更多的空间来存储编译的代码。

### Why Android use Virtual Machine?

Android使用虚拟机作为其运行时环境，以便运行Android特有的APK格式的应用程序。以下是优点：

* ·应用代码与核心操作系统隔离。所以即使任何代码包含一些恶意代码也不会直接影响系统文件。它使Android操作系统更加稳定可靠。

* ·它提供交叉兼容性或平台独立性。这意味着即使应用程序在诸如PC的平台上编译，仍然可以在使用虚拟机的移动平台上执行。

### Benefits of ART

* ·应用程序运行速度更快，因为DEX字节码转换在安装过程中完成。

* ·减少启动时间，因为本地代码直接执行了，不用编译了。

* ·提高电池性能，因为逐行解码字节码的功率被节省。

* ·改进的垃圾收集器。

* ·改进开发者工具。

### Drawbacks（缺点） of ART

* ·由于在安装过程中将DEX字节码转换为机器代码，App安装需要更多时间。

* ·由于在安装时生成的本地机器代码存储在内部存储器中，因此需要更多的内部存储。

### Conclusion

ART是通过执行DEX文件，专门为Android设计的字节码格式，针对最小的内存占用进行了优化而编写的，用于在低内存设备上运行多个虚拟机。 它使UI感觉更流畅。 





