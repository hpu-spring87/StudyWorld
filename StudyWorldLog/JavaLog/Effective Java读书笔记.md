# Effective Java 读书笔记

### 适当考虑静态工厂方法代替构造器

对于获取一个类的实例最简单也是最常见的方法，就是给他一个构造器，然后new一个对象，其实也有另外一种实现方法，那就是静态工厂。

Talk is cheap ,show the code :

```
public static Boolean valueOf(boolean b){
  return b ? Boolean.TRUE : Boolean.FALSE;
}

```
基础包里面的Boolean类以及其他常用基本数据类型这种写法很常见。

下面列一下这样写的优点：

* 第一：静态工厂方法有自己的名字（即方法名字，可以随便自定义），而构造器的名字是固定的，只有一个。
* 第二：相对于构造器，静态工厂方法不用每次调用的时候都实例化一个对象。
* 第三：相对于构造器，静态工厂方法可以返回原返回类型的任何子类型的对象（更灵活，安全，设计API时候可以返回对象，同时又不会让对象变成公有的）
* 第四：在创建参数化实例的时候，静态工厂方法使代码变得更加简洁(1.7以后已经不算优点了，默认构造就可以这样实现了)

这点不太好理解，实际就是类型推导：

Talk is cheap ,show the code :

```
public static <K,V> HashMap<K,V> newInstance(){
  return new HashMap<K<V>();
}

```

事物总有两面性，优点总是伴随着缺点来的：

* 类如果不含有公有的或者受保护的构造器，那么类就不能被实例化
* 静态工厂方法与其他静态方法实际上没有任何区别

### 遇到多个构造器参数时候考虑用构建器

当一个类实例化需要多个参数的时候，我们需要在构造器里面都声明好，但是当某一个参数缺少或者为空的时候，我们也必须传入一个默认值，只有这样才能
实例化成功，但是，当参数多的时候，就要哭了，每个参数即使不需要也要有个默认值。

这时候你可能会想，用JavaBean来实现，用get,set方法动态的设置某个属性的参数，这样导致的一个问题就是线程不安全，可能获取到的参数不一致。

怎么办呢？Builder模式（构建器）就是最好的解决方案：

Talk is cheap ,show the code :

```
public class BuildPattern{
  private final int input;

  public static class Builder{
    private final int input;

    public Builder(int input){
      this.input = input;
    }

    public BuildPattern build(){
      return new BuildPattern(this);
    }

  }

  private BuildPattern (Builder builder){
    input = builder.input;
  }
}

```

简而言之，当构造器或者静态工厂方法里面有多个参数，并且参数是可选的时候，这时候构建器无疑是最好的选择。
