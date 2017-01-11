# React之必备点

> React(别名：React.js 或 ReactJS)是一个为数据提供渲染为HTML视图的开源 JavaScript库。React视图通常采用包含以自定义HTML标记规定的其他组件的组件渲染。React为程序员提供了一种子组件不能直接影响外层组件("data flows down") 的模型，数据改变时对HTML文档的有效更新,和现代单页应用中组件之间干净的分离。使得构建用户界面变得更加高效，灵活简单。


# Why React ?

> React是Facebook和Instagram为了构建用户界面而设计一个JavaScript库，大部分人把它看做MVC中的V.它的设计主要是为了解决一个问题：随着时间推移构建越来越大的大型应用程序.

# 入门必备基础点

## ReactDOM.render()

> ReactDOM.render()是React的最基本的用法，用于把组件转换为HTML语言，并且插入指定的DOM节点，然后渲染出来可视化界面。

```
eg:
ReactDOM.render(
  <h1>Hello, world!</h1>,
  //example，即是待插入的DOM节点。
  document.getElementById('example')
);

```

##  JSX语法

> HTML语言直接和JavaScript混写，不加任何引号，这就是JSX语法一种展示，JSX的基本语法规则：遇到HTML标签（以<开头），就用HTML解析，遇到代码（以{开头}）就用JavaScript解析。

```
eg:
var names = ['Alice', 'Emily', 'Kate'];

ReactDOM.render(
  <div>
  {
    names.map(function (name) {
      return <div>Hello, {name}!</div>
    })
  }
  </div>,
  document.getElementById('example')
);

//JSX允许在模板里面直接插入JavaScript变量，如果这个变量是一个数组，则会展开这个数组的所有成员。
eg:

var arr = [
  <h1>Hello world!</h1>,
  <h2>React is awesome</h2>,
];
ReactDOM.render(
  <div>{arr}</div>,
  document.getElementById('example')
);

```


## 组件

> React允许将代码组装成组件（Component）然后像HTML标签那样插入网页里面，React.createClass方法就是为了生成组件的类。所有组件必须有自己的render方法，用于输出组件。

*注意： 组件类的名字第一个字母必须大写，否则会报错，为了避免与JavaScript代码命名冲突，组件类只能包含一个顶层标签，也即是只能有一个根节点。*

```
eg:
var HelloMessage = React.createClass({
  render: function() {
    return <h1>Hello {this.props.name}</h1>;
  }
});

ReactDOM.render(
  <HelloMessage name="John" />,
  document.getElementById('example')
);

//组件的用法与原声HTML基本一致，可以加入任意属性，比如上面name属性。组件属性可以通过this.props.name获取。

//特殊属性：class要写成className,for要写成htmlFor,因为class和for是JavaScript关键字。

```

## this.props.chilren

> this.props对象的属性与组件属性一一对应，除了this.props.children,它表示组件的所有子节点。

```
eg:
var NotesList = React.createClass({
  render: function() {
    return (
      <ol>
      {
        React.Children.map(this.props.children, function (child) {
          return <li>{child}</li>;
        })
      }
      </ol>
    );
  }
});

ReactDOM.render(
  <NotesList>
    <span>hello</span>
    <span>world</span>
  </NotesList>,
  document.body
);

//这里要注意，this.props.children的情况，如果 组件没有子节点，它就是undefined，如果有一个节点，数据类型是object，如果多个子节点，那就是array，处理要分情况处理。这时候就可以使用React.Children.map来遍历子节点，不用担心数据类型了。

```

## PropTypes

> 组件的属性可以接受任意类型的值，字符串，对象，函数等等，有时候需要验证组件的属性是否满足某些条件，这时候就用到了组件类的PropTypes属性。

```
eg:
var MyTitle = React.createClass({
  propTypes: {
    //title属性是必须的，并且是字符串
    title: React.PropTypes.string.isRequired,
  },

  render: function() {
     return <h1> {this.props.title} </h1>;
   }
});

//getDefaultProps可以用来设置组件的默认值

```


##  获取真实的DOM节点

> 组件并不是真实的DOM节点，而是存在于内存之中的一种数据结构，叫做虚拟DOM（Virtual DOM）,
只有它转换插入文档以后，才会变成真实的DOM，根据react的设计理念，所有的DOM变动，都先在虚拟DOM上发生，然后再将实际发生变动部分反映在真实DOM上，这种算法叫DOM diff，可以极大提高网页性能表现，但是有时候需要获取真实的DOM节点，这时候就用到了ref属性。

```
eg:
var MyComponent = React.createClass({
  handleClick: function() {
    this.refs.myTextInput.focus();
  },
  render: function() {
    return (
      <div>
        <input type="text" ref="myTextInput" />
        <input type="button" value="Focus the text input" onClick={this.handleClick} />
      </div>
    );
  }
});

ReactDOM.render(
  <MyComponent />,
  document.getElementById('example')
);

//上面代码中，组件MyComponent的子节点有一个文本输入框，用于获取用户的输入，这时候就必须获取真实的DOM 节点，虚拟DOM节点拿不到用户的输入，为了实现，文本框必须有一个ref属性，然后this.refs.[属性名字]就会返回真实的DOM节点。

```

## this.state

> 组件避免不了要与用户互动，React做了一大创新，就是将组件看成一个状态机，一开始有初始状态，然后用户交互，导致状态变化，从而触发重新渲染UI。

```
eg:
var LikeButton = React.createClass({
  getInitialState: function() {
    return {liked: false};
  },
  handleClick: function(event) {
    this.setState({liked: !this.state.liked});
  },
  render: function() {
    var text = this.state.liked ? 'like' : 'haven\'t liked';
    return (
      <p onClick={this.handleClick}>
        You {text} this. Click to toggle.
      </p>
    );
  }
});

ReactDOM.render(
  <LikeButton />,
  document.getElementById('example')
);

//getInitialState 方法用于定义初始状态,也就是一个对象，这个对象可以通过 this.state 属性读取。当用户点击组件，导致状态变化，this.setState 方法就修改状态值，每次修改以后，自动调用 this.render 方法，再次渲染组件。


```

**由于 this.props 和 this.state 都用于描述组件的特性，可能会产生混淆。一个简单的区分方法是，this.props 表示那些一旦定义，就不再改变的特性，而 this.state 是会随着用户互动而产生变化的特性。**

## 表单

> 表单填入的内容，属于用户跟组件的互动，所以不能用 this.props，这时候需要定义一个 onChange 事件的回调函数，通过 event.target.value 读取用户输入的值。

```
eg:
var Input = React.createClass({
  getInitialState: function() {
    return {value: 'Hello!'};
  },
  handleChange: function(event) {
    this.setState({value: event.target.value});
  },
  render: function () {
    var value = this.state.value;
    return (
      <div>
        <input type="text" value={value} onChange={this.handleChange} />
        <p>{value}</p>
      </div>
    );
  }
});

ReactDOM.render(<Input/>, document.body);

```


## 组件的生命周期

**组件的生命周期分成三个状态：**

* Mounting：已插入真实 DOM
* Updating：正在被重新渲染
* Unmounting：已移出真实 DOM

React为每个状态都提供了处理函数，will 函数在进入状态之前调用，did 函数在进入状态之后调用，三种状态共计五种处理函数：

* componentWillMount()
* componentDidMount()
* componentWillUpdate(object nextProps, object nextState)
* componentDidUpdate(object prevProps, object prevState)
* componentWillUnmount()

此外，React还提供了两种特殊状态的处理函数：

* componentWillReceiveProps(object nextProps)：已加载组件收到新的参数时调用
* shouldComponentUpdate(object nextProps, object nextState)：组件判断是否重新渲染时调用

```

eg:
var Hello = React.createClass({
  getInitialState: function () {
    return {
      opacity: 1.0
    };
  },

  componentDidMount: function () {
    this.timer = setInterval(function () {
      var opacity = this.state.opacity;
      opacity -= .05;
      if (opacity < 0.1) {
        opacity = 1.0;
      }
      this.setState({
        opacity: opacity
      });
    }.bind(this), 100);
  },

  render: function () {
    return (
      <div style={{opacity: this.state.opacity}}>
        Hello {this.props.name}
      </div>
    );
  }
});

ReactDOM.render(
  <Hello name="world"/>,
  document.body
);

//上面代码在hello组件加载以后，通过componentDidMount方法设置一个定时器，每隔100毫秒，就重新设置组件的透明度，从而触发重新渲染。另外注意，style的属性设置不要写成：
style="opacity:{this.state.opacity};"
要写成如下：
style={{opacity: this.state.opacity}}
这是因为React组件样式是一个对象，所以第一个大括号标识JavaScript语法，第二个大括号标识样式对象。

```

##  Ajax

> 组件的数据来源，通常是通过Ajax请求服务器完成的，可以使用componentDidMount,方法设置Ajax请求，等到请求成功，再用this.setState方法重新渲染UI。

```
eg:
var UserGist = React.createClass({
  getInitialState: function() {
    return {
      username: '',
      lastGistUrl: ''
    };
  },

  componentDidMount: function() {
    $.get(this.props.source, function(result) {
      var lastGist = result[0];
      if (this.isMounted()) {
        this.setState({
          username: lastGist.owner.login,
          lastGistUrl: lastGist.html_url
        });
      }
    }.bind(this));
  },

  render: function() {
    return (
      <div>
        {this.state.username}'s last gist is
        <a href={this.state.lastGistUrl}>here</a>.
      </div>
    );
  }
});

ReactDOM.render(
  <UserGist source="https://api.github.com/users/octocat/gists" />,
  document.body
);

//上面代码使用jQuery完成Ajax请求，为了说明，React本身么有任何依赖，完全可以不使用jQuery，而使用其他库。
我们甚至可以把一个Promise对象传入组件：

ReactDOM.render(
  <RepoList
    promise={$.getJSON('https://api.github.com/search/repositories?q=javascript&sort=stars')}
  />,
  document.body
);

//上面代码把获取数据，将Promise对象作为属性，传给组件。如果Promise对象正在抓取数据（pending状态），组件显示正在加载，如果Promise对象报错（rejected状态），组件显示报错信息，如果Promise对象抓取数据成功（fulfilled状态），组件显示获取的数据。

var RepoList = React.createClass({
  getInitialState: function() {
    return { loading: true, error: null, data: null};
  },

  componentDidMount() {
    this.props.promise.then(
      value => this.setState({loading: false, data: value}),
      error => this.setState({loading: false, error: error}));
  },

  render: function() {
    if (this.state.loading) {
      return <span>Loading...</span>;
    }
    else if (this.state.error !== null) {
      return <span>Error: {this.state.error.message}</span>;
    }
    else {
      var repos = this.state.data.items;
      var repoList = repos.map(function (repo) {
        return (
          <li>
            <a href={repo.html_url}>{repo.name}</a> ({repo.stargazers_count} stars) <br/> {repo.description}
          </li>
        );
      });
      return (
        <main>
          <h1>Most Popular JavaScript Projects in Github</h1>
          <ol>{repoList}</ol>
        </main>
      );
    }
  }
});

```

## 参考

[https://zh.wikipedia.org/wiki/React](https://zh.wikipedia.org/wiki/React)

[http://www.ruanyifeng.com/blog/2015/03/react.html](http://www.ruanyifeng.com/blog/2015/03/react.html)
