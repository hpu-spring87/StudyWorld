#  1. python之开发工具，爬虫入门
## 1.1 开发工具
  **用sublime 2不能build，只好用IDE，这里是PyCharm CE 版本（选择社区版本功能就足够了）
  Mac 版本下载，安装即可。不需要配什么环境变量，废话结束.<https://www.jetbrains.com/pycharm/>
  **
  
## 1.2  正则匹配准备

Python 自1.5版本起增加了re 模块，它提供 Perl 风格的正则表达式模式。<br/>
re 模块使 Python 语言拥有全部的正则表达式功能。<br/>

Python编译器用‘\’（反斜杠）来表示字符串常量中的转义字符。<br/>

如果反斜杠后面跟着一串编译器能够识别的特殊字符，那么整个转义序列将被替换成对应的特殊字符（例如，‘\n’将被编译器替换成换行符）。<br />

但这给在Python中使用正则表达式带来了一个问题，因为在‘re’模块中也使用反斜杠来转义正则表达式中的特殊字符（比如*和+）。<br />

这两种方式的混合意味着有时候你不得不转义转义字符本身（当特殊字符能同时被Python和正则表达式的编译器识别的时候），但在其他时候你不必这么做（如果特殊字符只能被Python编译器识别）。<br />

与其将我们的心思放在去弄懂到底需要多少个反斜杠，我们可以使用原始字符串来替代。<br/>

原始类型字符串可以简单的通过在普通字符串的双引号前面加一个字符‘r’来创建。当一个字符串是原始类型时，Python编译器不会对其尝试做任何的替换。本质上来讲，你在告诉编译器完全不要去干涉你的字符串 **


** python 的‘re’模块提供了几个方法对输入的字符串进行确切的查询。我们将会要讨论的方法有：**

1. re.match()
2. re.search()
3. re.findall() 


**match()方法：** <br />
match()方法的工作方式是只有当被搜索字符串的开头匹配模式的时候它才能查找到匹配对象。<br />
比如：'dog cat dog'匹配dog会匹配，然而，匹配cat却不行，因为必须是开头匹配<br />

    import re
	print(re.match('www', 'www.runoob.com').span())  # 在起始位置匹配，span是获取匹配的位置
	print(re.match('com', 'www.runoob.com'))         # 不在起始位置匹配
	
	运行结果如下：
    (0, 3)
    None
	

**search()方法** <br />
search()方法会在它查找到一个匹配项之后停止继续查找，因此在我们的示例字符串中用searc()方法查找‘dog’只找到其首次出现的位置。

	import re
	print(re.search('www', 'www.runoob.com').span())  # 在起始位置匹配
	print(re.search('com', 'www.runoob.com').span())         # 不在起始位置匹配
	
	运行结果如下：
	(0, 3)
    (11, 14)

**findall()方法**<br />
在Python中使用的最多的查找方法是findall()方法。当我们调用findall()方法，我们可以非常简单的得到一个所有匹配模式的列表,not a object....

**使用 match.start 和 match.end 方法返回匹配字符串的位置，起始和终止位置**

正则表达式修饰符 - 可选标志<br />
正则表达式可以包含一些可选标志修饰符来控制匹配的模式。修饰符被指定为一个可选的标志。多个标志可以<br />通过按位 OR(|) 它们来指定。如 re.I | re.M 被设置成 I 和 M 标志：<br />
修饰符	描述<br />
1. re.I	使匹配对大小写不敏感<br />
2. re.L	做本地化识别（locale-aware）匹配<br />
3. re.M	多行匹配，影响 ^ 和 $<br />
4. re.S	使 . 匹配包括换行在内的所有字符<br />
5. re.U	根据Unicode字符集解析字符。这个标志影响 \w, \W, \b, \B.<br />
6. re.X	该标志通过给予你更灵活的格式以便你将正则表达式写得更易于理解。<br />



## 1.3  爬虫入门
**代码片：**

    import urllib2
    response = urllib2.urlopen("http://www.baidu.com")
    print response.read()
    
**urlopen(url, data, timeout)**

1. 第一个参数url即为URL
2. 第二个参数data是访问URL时要传送的数据
3. 第三个timeout是设置超时时间。
4. 第二三个参数是可以不传送的，data默认为空None，timeout默认为socket._GLOBAL_DEFAULT_TIMEOUT













