# .Android Lambda 表达式

### 简介

在一般数学计算中，一个lambda表达式就是一个函数，它的定义是：为部分或者所有输入值指定一个输出值。Lambda表达式在java中是以函数语言的概念引入。在java中术语Lambdas可以理解为一种省略掉修改器，返回类型和参数类型的更紧凑，更好的匿名方法。

使用匿名内部类和lambda表达式对比分析：

> 匿名内部类存在着影响应用性能的问题

首先，编译器会为每一个匿名内部类创建一个类文件。创建出来的类文件的名称通常按照这样的规则 ClassName符合和数字。生成如此多的文件就会带来问题，因为类在使用之前需要加载类文件并进行验证，这个过程则会影响应用的启动性能。类文件的加载很有可能是一个耗时的操作，这其中包含了磁盘IO和解压JAR文件。

关于匿名内部类的种种会使得应用的内存占用增加。因此我们有必要引入新的缓存机制减少过多的内存占用，这也就意味着我们需要引入某种抽象层。

最重要的是一旦Lambda表达式使用了匿名内部类实现，就会限制了后续Lambda表达式实现的更改，降低了其随着JVM改进而改进的能力。

> Lambdas表达式和invokedynamic

为了解决前面提到的担心，Java语言和JVM工程师决定将翻译策略推迟到运行时。利用Java 7引入的invokedynamic字节码指令我们可以高效地完成这一实现。将Lambda表达式转化成字节码只需要如下两步：

1. 生成一个invokedynamic调用点，也叫做Lambda工厂。当调用时返回一个Lambda表达式转化成的函数式接口实例

2. 将Lambda表达式的方法体转换成方法供invokedynamic指令调用

> 语法， lambda的基本语法：

```
(parameters（参数）) -> expression(表达式)
或者
(parameters（参数）) -> { statements（状态）; }


```

例子：

1. (int x, int y) -> x + y 取两个整型数并返回他们的和
2. (x, y) -> x - y 取两个数字并返回他们的差
3. () -> 42 不取任何值直接返回42
4. (String s) -> System.out.println(s) 取一个字符串，在控制台中打印它的值，并什么也不返回
5. x -> 2 * x 取一个数字并返回它的倍数
6. c -> { int s = c.size(); c.clear(); return s; } 取一个集合，清空它，并返回清空前的大小


> Android 里面使用：

在build.gradle里面如下配置：

```
android {
  ...
  defaultConfig {
    ...
    jackOptions {
      enabled true
    }
  }
  compileOptions {
    sourceCompatibility JavaVersion.VERSION_1_8
    targetCompatibility JavaVersion.VERSION_1_8
  }
}

```

sync build.gradle 文件，如果还有其他问题，升级 buildToolsVersion即可.

如果你要用第三方的库，那么RetroLambda，推荐.

> 关于启用 Java 8 功能和 Jack 工具链

要使用新的 Java 8 语言功能，还需使用新的 Jack 工具链。新的 Android 工具链将 Java 源语言编译成 Android 可读取的 Dalvik 可执行文件字节码，且有其自己的 .jack 库格式，在一个工具中提供了大多数工具链功能：重新打包、压缩、模糊化以及 Dalvik 可执行文件分包。


以下是构建 Android Dalvik 可执行文件可用的两种工具链的对比：

* 旧版 javac 工具链：
 * javac (.java --> .class) --> dx (.class --> .dex)

* 新版 Jack 工具链：
 * Jack (.java --> .jack --> .dex)





比如，点击事件：

```
Button button = (Button)findViewById(R.id.button);
button.setOnClickListener(new View.OnClickListener() {
    @Override
    public void onClick(View v) {
        Toast.makeText(this, "Button clicked", Toast.LENGTH_LONG).show();
    }
});

```

用lambda表达你可以这样写：

```
Button button = (Button)findViewById(R.id.button);
button.setOnClickListener(v -> Toast.makeText(this, "Button clicked", Toast.LENGTH_LONG).show());

```

> 总结

1. 最新lambda 支持到API 9,官方是这样说：也在 API 级别 23 及更低版本中使用
2. 有性能上的提升
