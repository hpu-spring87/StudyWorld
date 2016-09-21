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

2. xml文件的根节点必须是<resources>.然后再在里面添加<style>节点即可

3. <style>元素必须包含name属性，然后就是可选的parent属性

4. 然后为<style添加<item>元素了,<item>包含键值对，属性名字以及对应的值

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

**选择特定版本的Theme**

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
