# Android Style and Theme 总结

## Style简介

> Style：Android Style的思想来自于web设计中的级联样式表（cascading stylesheets）把设计和样式分离.
       在Android中Style是定义在XMl文件的一系列属性的集合，这些属性可以指定特定的外表和样式，可以作用于一个特定View
       或者一个window，比如定义：height, padding, font color等等.

示例：

```

使用Style：

<TextView
  style="@style/CodeFont"
  android:text="@string/hello" />

```

这样就可以把TextView的属性移到对应style文件里面.

### Style定义

1. 为了创建一系列的styles，需要在res/values/ 目录下定义一个XML文件，文件名字随意命名，但必须以.xml作为文件的后缀.

2. xml文件的根节点必须是'<resources'>.然后再在里面添加'<style'>节点即可

3. '<style'>元素必须包含name属性，然后就是可选的parent属性

4. 然后为'<style添加<item'>元素了,'<item'>包含键值对，属性名字以及对应的值

示例：

```

<?xml version="1.0" encoding="utf-8"?>
<resources>
    <style name="CodeFont" parent="@android:style/TextAppearance.Medium">
        <item name="android:layout_width">fill_parent</item>
        <item name="android:layout_height">wrap_content</item>
        <item name="android:textColor">#00FF00</item>
        <item name="android:typeface">monospace</item>
    </style>
</resources>

```

**注意：关于NameSpace,<item>里各个name属性需要androd:,当view引用的时候，则不需要android:,直接@style/stylename即可.**


### Theme简介

> Theme是Style的一种特殊形式，只是他的作用对象是Activity或者Application，而不是一个特定的View了.当style被用作Theme的时候，作用的Activity或者Application里面包含的View都会受到Theme里面样式的影响.

**维护兼容性**

一. 定义备用样式:

您可对您的应用进行配置，使应用能够在支持它的设备上使用材料主题，并且能够在运行早期版本 Android 的设备上还原至早期版本的主题：

1. 定义一个从 res/values/styles.xml 中的早期版本主题（例如 Holo）继承的主题。

2. 定义一个从 res/values-v21/styles.xml 中的材料主题继承且拥有相同名称的主题。

3. 在清单文件中将此主题设置为您的应用主题。

> 注意：如果您的应用使用材料主题，但没有以这方式提供备用主题，您的应用将无法在 Android 5.0 之前的 Android 版本上运行。

二. 提供备用布局:

如果您根据材料设计指导方针设计的布局使用 Android 5.0（API 级别 21）所推出的新 XML 属性，为了这些布局将能够在早期版本的 Android 上正常运行。

您可在 res/layout-v21/ 内创建用于 Android 5.0（API 级别 21）的布局文件，同时也可在 res/layout/ 内创建用于早期版本 Android 的备用布局文件。例如，res/layout/my_activity.xml 是 res/layout-v21/my_activity.xml 的备用布局。

为避免代码重复，请在 res/values/ 内定义您的风格，在 res/values-v21/ 内为新 API 修改风格，以及使用风格继承（即：在 res/values/ 内定义基础风格，然后在 res/values-v21/ 内继承这些风格）

三. 使用支持内容库

v7 支持内容库 r21 及更高版本包括下列材料设计功能：

1. 应用其中一个 Theme.AppCompat(兼容主题) 主题时可取得适用于一些系统小组件的材料设计风格.

2. Theme.AppCompat 主题中拥有配色工具主题属性，各种状态栏背景的设置.

3. 从图像萃取突出颜色的 Palette 类,也就是获取图片的主色调.

4. 显示数据集合的 RecyclerView 小组件.

5. 创建卡片的 CardView 小组件.

> RecyclerView 以及 CardView 小组件可通过 Android v7 支持内容库提供给早期版本 Android，但有如下限制：
1. CardView 使用额外边距返回编程阴影实现。
2. CardView 不会裁剪其与圆角相交的子视图。

如果要在 Android 5.0（API 级别 21）之前的 Android 版本中使用这些功能，请将 Android v7 支持内容库作为 Gradle 依赖项包括在您的项目中：

```
dependencies {
    compile 'com.android.support:appcompat-v7:21.0.+'
    compile 'com.android.support:cardview-v7:21.0.+'
    compile 'com.android.support:recyclerview-v7:21.0.+'
}

```

四. 检查系统版本

如果应用只是支持特定的版本的设备，或者为设备定制的，或者用户群的设备集中在某个特定的版本，这时候就可以硬编码到特定的版本.

比如：下列功能仅在 Android 5.0（API 级别 21）及更高版本中提供：
* 操作行为转换
* 触摸反馈
* 揭露动画
* 基于路径的动画
* 矢量图片
* 图片着色

如果要保留与早期版本 Android 的兼容性，需要在运行时检查系统 version，然后再为下列的任何一个功能调用 API：

```
// Check if we're running on Android 5.0 or higher
if (Build.VERSION.SDK_INT >= Build.VERSION_CODES.LOLLIPOP) {
    // Call some material design APIs here
} else {
    // Implement this feature without material design
}

```


**比如需要选择特定版本的Theme**

新版本的Android会增加额外的Theme，如果要使用还要兼容低版本的话，那就要多一套Style了：

比如要使用系统默认的light theme，在res/values/styles.xml路径下定义如下：

```
<style name="LightThemeSelector" parent="android:Theme.Light">
    ...
</style>

```

Api 11有另外一个light Theme，这时候 Api 11+就多一套style了，在res/values-v11路径下定义如下：

```

<style name="LightThemeSelector" parent="android:Theme.Holo.Light">
    ...
</style>

```

这时候，当设备为3.0（API 11+）时候就会用新增的light Theme，而不是默认Theme.

系统所有Theme如下：

https://android.googlesource.com/platform/frameworks/base/+/refs/heads/master/core/res/res/values/styles.xml
