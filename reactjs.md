# 组件的生命周期
组件的生命周期分成 三个 状态：
1. Mounting: 已插入真实DOM
2. Updating: 正在被重新渲染
3. Unmounting: 已移出真实DOM

React 为每个状态都提供了两种处理函数，`will` 函数在进入状态之前调用，`did` 函数在进入状态之后调用，三种状态共计五种处理函数:

```
componentWillMount()
componentDidMount()
componentWillUpdate(object nextProps, object nextState)
componentDidUpdate(object prevProps, object prevState)
componentWillUnmount()
```

React 还提供两种特殊状态的处理函数:

```javascript
componentWillReceiveProps(object nextProps)：//已加载组件收到新的参数时调用
shouldComponentUpdate(object nextProps, object nextState)：//组件判断是否重新渲染时调用
```

#

+ `this.props.children` 表示组件的所有子节点

    this.props.children 的值有三种可能：

        如果当前组件没有子节点，它就是 undefined ;
        如果有一个子节点，数据类型是 object ；
        如果有多个子节点，数据类型就是 array 。
    所以，处理 this.props.children 的时候要小心。


React 提供一个工具方法 `React.Children` 来处理 this.props.children 。我们可以用 React.Children.map 来遍历子节点，而不用担心 this.props.children 的数据类型是 undefined 还是 object。

```jsx
<script type="text/babel">
    var NotesList = React.createClass({
        render: function () {
        return (
            <ol>
            {
            React.Children.map(this.props.children, function (child) {
                return <li>{child}</li>
            })
            }
            </ol>
        );
        }
    });

    ReactDOM.render(
        <NotesList>
        <span>Hello</span>
        <span>world</span>
        </NotesList>,
        document.getElementById("example")
    );
</script>
```


+ `PropTypes` 属性

用来验证组件实例的属性是否符合要求。

+ `getDefaultProps()` 用来设置组件属性的默认值
```jsx
var MyTitle = React.createClass({
  getDefaultProps : function () {
    return {
      title : 'Hello World'
    };
  },

  render: function() {
     return <h1> {this.props.title} </h1>;
   }
});

ReactDOM.render(
  <MyTitle />,
  document.body
);
```

+ `ref` 属性 用于获取真实的DOM节点

```jsx
<script type="text/babel">
    var MyComponent = React.createClass({
    handleClick: function () {
        this.refs.myTextInput.focus();
    },
    render: function () {
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
    document.getElementById("example")
    );
</script>
```

+ `getInitialState()` 用于定义初始状态

+ `与运算符 &&`
在 JavaScript 中，`true && expression` 总是返回 `expression` ，而 `false && expression` 总是返回 `false`

```jsx
function Mailbox(props) {
  const unreadMessages = props.unreadMessages;
  return (
    <div>
      <h1>Hello!</h1>
      {unreadMessages.length > 0 &&
        <h2>
          You have {unreadMessages.length} unread messages.
        </h2>
      }
    </div>
  );
}

const messages = ['React', 'Re: React', 'Re:Re: React'];
ReactDOM.render(
  <Mailbox unreadMessages={messages} />,
  document.getElementById('root')
);
```