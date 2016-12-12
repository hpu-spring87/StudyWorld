# Android Test总结

> 在Android中有2种单元测试:Local unit tests 和 Instrumented unit tests.

1. Local unit tests
> 所谓Local unit test只是在JVM环境下运行的测试用例，与操作系统无关，主要用于测试业务逻辑。

2. Instrumented unit tests
> 所谓Instrumented unit tests，可以依赖于物理设备或模拟器来调用Android的API 和一些 support api，例如 Android Testing Support Library。如果需要获取 instrumentation 信息（例如需要 app 的 context）或者需要 Android 框架里的一些组件（比如 Parcelable 或 SharedPreferences 对象），也可以使用Instrumented 单测,因此测试会花费更多的时间，主要用于测试与Android API相关的逻辑。

显然我们写测试用例有2种选择，至于选择哪一种，要根据具体的测试目标来判断，当然，尽可能的写Local unit tests。

## 测试环境搭建

* 首先看一下两种测试的包结构：

```
app/src/main/java — app source code.
app/src/test/java — local tests.
app/src/androidTest/java — instrumented tests.

```

* 如果由于种种原因Android Studio没有默认生成对应gradle配置，那么你需要手动添加以下代码：

```
app module 的gradle文件配置如下：

android {
   ...
   defaultConfig {
       ...
       testInstrumentationRunner "android.support.test.runner.AndroidJUnitRunner"
   }
   ...
}
dependencies {
   ...
   testCompile 'junit:junit:4.12'
}

```
另外，一种非常流行且常用的测试框架*[Mockito](http://site.mockito.org/)*你也是必须掌握的，它可以用来模拟对象，监听对象，并且支持工具检查.配置如下：

```
testCompile "org.mockito:mockito-core:1.+"

```

## Local tests in Android

下面列举简单的2个测试用例：

```
public class ExampleUnitTest {


   @Test
   public void addition_correct() throws Exception {
       assertEquals(4, 2 + 2);
   }


   @Test
   public void addition_isNotCorrect() throws Exception {
       assertEquals("Numbers isn't equals!", 5, 2 + 2);
   }
}

```
选中方法名，右键，Run，即可看到运行结果：

![images](https://stfalcon.com/uploads/images/58242e7b2a0f2.png)

看到运行结果，第一个执行结果是绿色通过，第二个，执行出现了异常.
可以给测试方法设置一个预期的异常,以及超时时间timeout（毫秒），如果超时期间内没有执行，被认为执行失败。

如下：

```
@Test(expected = NullPointerException.class，timeout = 1000)
public void nullStringTest() {
   String str = null;
   assertTrue(str.isEmpty());
}

```
也可以使用 Matchers机制：

```
assertThat(x, is(3));
assertThat(x, is(not(4)));
assertThat(list, hasItem("3"));

```

就像他们名字字面意思一样:
* is() 可以被描述为"is equal"
* is(not())可以描述为“isn’t equal“
* hasItem()可以描述为list里面是否包含对应元素


上面是基本的测试用例，如果用 Mockito 这个框架，则会写出更高效的测试用例，如下：

```
List mockedList = mock(List.class);

@Mock
List mockedList;

```
为了能够使用@Mock注解，需要在类上面加上@RunWith(MockitoJUnitRunner.class)注解，或者在 @Before 方法里面执行 MockitoAnnotations.initMocks(this);

```
@Before
public void init() {
   MockitoAnnotations.initMocks(this);
}

```

得到mocked对象以后，你就可以这样玩了：
比如：你想改一下APP的名称，你可以这样写：

```
when(mockContext.getString(R.string.app_name))
       .thenReturn("New Test name");

```
当你调用getString()方法的时候，你就会得到"New Test name"

```
SomeClass obj = new SomeClass(mockContext);
String result = obj.getAppName();

```

更多详细功能，查看[Mockito](http://site.mockito.org/)

## Instrumented tests in Android

> 使用这种类型的测试，我们可以访问真正的上下文，以及所有的Android API，除此之外，还有一个“上帝模式”，我们可以用来管理Activity的生命周期。要使测试被识别为Instrumented，应该使用相应的注解标记类：

```
@RunWith(AndroidJUnit4.class)
public class ExampleInstrumentedTest {
   ...
}

```

检测APP的包名是否与我们的应用一致，可以这样写：

```
@Test
public void useAppContext() throws Exception {
   Context appContext = InstrumentationRegistry.getTargetContext();
   assertEquals("com.stfalcon.demoapp", appContext.getPackageName());
}

```
用工具检测Activity的状态：

```
ActivityLifecycleMonitorRegistry.getInstance().addLifecycleCallback(new ActivityLifecycleCallback() {
   @Override
   public void onActivityLifecycleChanged(Activity activity, Stage stage) {
       //do some stuff
   }
});

```

或者管理他们的状态:
```
Instrumentation instrumentation = InstrumentationRegistry.getInstrumentation();
instrumentation.callActivityOnCreate(activity, bundle);

```

## 更多

[Junit4](http://junit.org/junit4/) &&
[Instrumented-unit-tests](https://developer.android.com/training/testing/unit-testing/instrumented-unit-tests.html)
