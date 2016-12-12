# Android studio之APK分析器

> 位置： Android studio → Build → Analyze APK.<br/>
  作用： 分析APK的文件结构，各个文件大小，或者与不同版本APK做比较，或者调试一些常用问题，包括APK大小和DEX的问题.

* Analyze APK可以在不需要特定源码的情况下，打开分析你本地的APK文件，这些APK可以是Android studio本地构建的也可以是从远程下载下的APK文件.

* Analyze APK一般用于分析Release版本的APK，如果是分析Debug版本，需要确保没有使用Instant Run，为了检测是否使用Instant Run，可以通过
  Android studio → Build → Build APK命令，然后查看归档文件里面是否包含instant-run.zip文件.


## 通过APK Analyzer减少APK大小

APK Analyzer 可以获取APK内部各个模块大小信息，在顶部可以看到原始文件大小以及对应的从Google Play下载该APK文件预估大小.
文件列表展示所有APK内包含文件，按大小从大到小排序展示。然后逐个分析，从大到小，开启APK的瘦身之旅吧....

## 通过APK Analyzer调试DEX问题

在这种情况下，差异来自于将我们的依赖项升级到较新版本并添加新库。Proguard和Multidex已经为我们的构建启用了，所以关于我们的DEX大小没有什么可以做的。不过，APK分析器是一个很好的工具，可以调试此设置的任何问题，特别是当您第一次为项目启用Multidex或Proguard时。

比如：DEX超过64k：ClassNotFoundException，可以通过分析，强制加入逐个类.

[原文地址](https://medium.com/google-developers/making-the-most-of-the-apk-analyzer-c066cb871ea2#.klndkutk8)
