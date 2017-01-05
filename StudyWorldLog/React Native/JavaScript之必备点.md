# JavaScript之必备点

> JavaScript是一种轻量级编程语言，非常流行的脚本语言，可以插入HTML中，一起在浏览器中运行。ECMA-262 是 JavaScript 标准的官方名称。

# JavaScript 用法

```
* JavaScript脚本必须位于<script>和<script>标签之间，可以放置在HTML页面的<body>和<head>标签中.

* 引入外部JavaScript文件，同上，只不过需要在 <script> 标签的 "src" 属性中设置该 .js 文件位置即可.

* JavaScript是脚本语言。浏览器会在读取代码时，逐行地执行脚本代码。而对于传统编程来说，会在执行前对所有代码进行编译。换句话说就是 JavaScript 语句向浏览器发出的命令，并执行。

```
# JavaScript 输出

JavaScript 没有任何打印或者输出的函数。但是可以用下面的方法来显示数据。

* 使用 window.alert() 弹出警告框。

* 使用 document.write() 方法将内容写到 HTML 文档中。如果在页面已完成加载后执行 document.write，整个 HTML 页面将被覆盖,比如点击事件触发的，就会把之前输出清空。

* 使用 innerHTML 写入到 HTML 元素。

* 使用 console.log() 写入到浏览器的控制台。

# JavaScript 语法

* JavaScript 中，常见的是驼峰法的命名规则，如 lastName (而不是lastname)。定义变量是通过关键字var.

```
var length = 16;                                  // Number 通过数字字面量赋值
var points = x * 10;                              // Number 通过表达式字面量赋值
var lastName = "Johnson";                         // String 通过字符串字面量赋值
var cars = ["Saab", "Volvo", "BMW"];              // Array  通过数组字面量赋值
var person = {firstName:"John", lastName:"Doe"};  // Object 通过对象字面量赋值

```

* 局部JavaScript变量：JavaScript函数内部声明的变量（使用 var）是局部变量，所以只能在函数内部访问它。

* 全局JavaScript变量：在函数外声明的变量是全局变量，网页上的所有脚本和函数都能访问它。

* 如果把值赋给尚未声明的变量，该变量将被自动作为全局变量声明。eg: carname="Volvo";

* JavaScript变量的生命周期：

  JavaScript变量的生命周期从它们被声明的时间开始。

  局部变量会在函数运行以后被删除。

  全局变量会在页面关闭后被删除。

* JavaScript严格模式:

 "use strict" 指令只运行出现在脚本或函数的开头。

* 常见的HTML事件如下:

|  事件         | 描述        |
| ----------:  |:----------:|
| onchange     | HTML 元素改变 |
| onclick 	   |用户点击 HTML 元素 |
| onmouseover  |	用户在一个HTML元素上移动鼠标 |
| onmouseout 	| 用户从一个HTML元素上移开鼠标 |
| onkeydown 	| 用户按下键盘按键 |
| onload 	| 浏览器已完成页面的加载 |

* JavaScript中typeof, null, 和 undefined区别:

  1. typeof 操作符来检测变量的数据类型。在JavaScript中，数组是一种特殊的对象类型。 因此 typeof [1,2,3,4] 返回 object

  2. null 表示 "什么都没有"。null是一个只有一个值的特殊类型。表示一个空对象引用。用 typeof 检测 null 返回是object。可以设置为 null 来清空对象。

  3. undefined 是一个没有设置值的变量。typeof 一个没有值的变量会返回 undefined。可以通过设置值为 undefined 来清空。类型为undefined.

* Undefined 和 Null 的区别:
  ```
   typeof undefined             // undefined
   typeof null                  // object
   null === undefined           // false
   null == undefined            // true

  ```

# JavaScript 正则表达式：

> 格式：/正则表达式主体/修饰符(可选)

eg:var patt = /runoob/i , runoob是一个正则表达式主体(用于检索),i 是一个修饰符 (搜索不区分大小写)。

在 JavaScript 中，正则表达式通常用于两个字符串方法 : search() 和 replace()。

search() 方法 用于检索字符串中指定的子字符串，或检索与正则表达式相匹配的子字符串，并返回子串的起始位置。

replace() 方法 用于在字符串中用一些字符替换另一些字符，或替换一个与正则表达式匹配的子串。


* 正则表达式修饰符:

| 修饰符  |	描述 |
|------: |:-------:|
|i 	  | 执行对大小写不敏感的匹配。|
|g   	| 执行全局匹配（查找所有匹配而非在找到第一个匹配后停止）。|
|m   	| 执行多行匹配。|

* 正则表达式模式

| 表达式 |	描述 |
|-----:|:-------:|
|[abc] 	| 查找方括号之间的任何字符。|
|[0-9] 	| 查找任何从 0 至 9 的数字。|
|(x竖线y) 	| 查找任何以 竖线 分隔的选项。 |

元字符是拥有特殊含义的字符：

| 元字符 |	描述 |
|------:|:------:|
| \d |	查找数字。|
| \s 	| 查找空白字符。|
| \b 	| 匹配单词边界。|
| \uxxxx 	| 查找以十六进制数 xxxx 规定的 Unicode 字符。|

量词:

| 量词 |	描述 |
|-----:|:-----:|
|n+ 	| 匹配任何包含至少一个 n 的字符串。|
|n* 	| 匹配任何包含零个或多个 n 的字符串。|
|n? 	| 匹配任何包含零个或一个 n 的字符串。|

* 使用 RegExp 对象：
  1. test() 方法用于检测一个字符串是否匹配某个模式，如果字符串中含有匹配的文本，则返回 true，否则返回 false。

  2. exec() 方法用于检索字符串中的正则表达式的匹配。该函数返回一个数组，其中存放匹配的结果。如果未找到匹配，则返回值为 null。

# JavaScript JSON

> JSON 英文全称 JavaScript Object Notation,JSON 使用 JavaScript 语法，但是 JSON 格式仅仅是一个文本。文本可以被任何编程语言读取及作为数据格式传递。

* JSON.parse(): 用于将一个 JSON 字符串转换为 JavaScript 对象。

* JSON.stringify(): 用于将 JavaScript 值转换为 JSON 字符串。

# Javascript:void(0)

> void 是 JavaScript 中非常重要的关键字，该操作符指定要计算一个表达式但是不返回值。

** href="#"与href="javascript:void(0)"的区别 **

* href="#"包含了一个位置信息，默认的锚是#top 也就是网页的上端。在页面很长的时候会使用 # 来定位页面的具体位置，格式为：# + id。

* javascript:void(0), 仅仅表示一个死链接。如果你要定义一个死链接请使用 javascript:void(0) 。

# JavaScript 函数

* 匿名函数：

```
函数表达式可以存储在变量中：
var x = function (a, b) {return a * b};
在函数表达式存储在变量后，变量也可作为一个函数使用：
var x = function (a, b) {return a * b};
var z = x(4, 3);
以上函数实际上是一个 匿名函数 (函数没有名称)。
函数存储在变量中，不需要函数名称，通常通过变量名来调用。

```

* Function() 构造函数:

```
在以上实例中，我们了解到函数通过关键字 function 定义。
函数同样可以通过内置的 JavaScript 函数构造器（Function()）定义。

var myFunction = new Function("a", "b", "return a * b");

var x = myFunction(4, 3);

等价于：

var myFunction = function (a, b) {return a * b}

var x = myFunction(4, 3);

* 在 JavaScript 中，很多时候，你需要避免使用 new 关键字。

```

* Arguments对象：

```
JavaScript 函数有个内置的对象 arguments 对象。
argument 对象包含了函数调用的参数数组。
可以在函数中这样使用：


x = sumAll(1, 123, 500, 115, 44, 88);

function sumAll() {
    var i, sum = 0;
    for (i = 0; i < arguments.length; i++) {
        sum += arguments[i];
    }
    return sum;
}


```


# JavaScript 类

* JavaScript 是面向对象的语言，但 JavaScript 不使用类。

* 在 JavaScript 中，不会创建类，也不会通过类来创建对象（就像在其他面向对象的语言中那样）。

* JavaScript 基于 prototype，而不是基于类的。
