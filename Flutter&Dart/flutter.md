## Widget

在Flutter中几乎所有的对象都是一个Widget。**Widget只是UI元素的一个配置数据，并且一个Widget可以对应多个`Element`**。

- Widget实际上就是`Element`的配置数据，Widget树实际上是一个配置树，而真正的UI渲染树是由`Element`构成；
- 一个Widget对象可以对应多个`Element`对象。

### 1. StatelessWidget

`StatelessWidget`用于不需要维护状态的场景，它通常在`build`方法中通过嵌套其它Widget来构建UI，在构建过程中会递归的构建其嵌套的Widget。

#### 查找父级widget的方法

```dart
class ContextRoute extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return Scaffold(
      appBar: AppBar(
        title: Text("查找父级widget的方法"),
      ),
      body: Container(
        child: Builder(builder: (context) {
          // 在Widget树中向上查找最近的父级`Scaffold` widget
          Scaffold scaffold = context.findAncestorWidgetOfExactType<Scaffold>();
          return (scaffold.appBar as AppBar).title;
        }),
      ),
    );
  }
}
```



### 2. StatefulWidget

#### State

一个 StatefulWidget 类会对应一个**State**类，**State** 表示与其对应的 StatefulWidget 要维护的状态。

State中的保存的状态信息可以：

1. 在widget 构建时可以被同步读取。
2. 在widget生命周期中可以被改变，当State被改变时，可以手动调用其`setState()`方法通知Flutter framework状态发生改变，Flutter framework在收到消息后，会重新调用其`build`方法重新构建widget树，从而达到更新UI的目的。

#### State生命周期

- `initState`：当Widget第一次插入到Widget树时会被调用，对于每一个State对象，Flutter framework只会调用一次该回调，所以，通常在该回调中做一些一次性的操作，如状态初始化、订阅子树的事件通知等。

- `didChangeDependencies()`：当State对象的依赖发生变化时会被调用；典型的场景是当系统语言Locale或应用主题改变时，Flutter framework会通知widget调用此回调。

- `build()`：此回调读者现在应该已经相当熟悉了，它主要是用于构建Widget子树的，会在如下场景被调用：

  1. 在调用`initState()`之后。
  2. 在调用`didUpdateWidget()`之后。
  3. 在调用`setState()`之后。
  4. 在调用`didChangeDependencies()`之后。
  5. 在State对象从树中一个位置移除后（会调用deactivate）又重新插入到树的其它位置之后。

- `reassemble()`：此回调是专门为了开发调试而提供的，在热重载(hot reload)时会被调用，此回调在Release模式下永远不会被调用。

- `didUpdateWidget()`：在widget重新构建时，Flutter framework会调用`Widget.canUpdate`来检测Widget树中同一位置的新旧节点，然后决定是否需要更新

- `deactivate()`：当State对象从树中被移除时，会调用此回调。

- `dispose()`：当State对象从树中被永久移除时调用；通常在此回调中释放资源。

  ![flutter_live](/Users/kevin/Documents/gits/shaochao13/daily_record/Flutter&Dart/img/flutter_live.png)







## 路由管理

### 1. MaterialPageRoute

`MaterialPageRoute`继承自`PageRoute`类，`PageRoute`类是一个抽象类，表示占有整个屏幕空间的一个模态路由页面，它还定义了路由构建及切换时过渡动画的相关接口及属性。`MaterialPageRoute` 是Material组件库提供的组件，它会根据不同平台，实现与平台页面切换动画风格一致的路由切换动画。

```dart
MaterialPageRoute({
    WidgetBuilder builder, // 回调函数，作用是构建路由页面的具体内容，返回值是一个widget。
    RouteSettings settings, // 包含路由的配置信息，如路由名称、是否初始路由（首页）
    bool maintainState = true, // 默认情况下，当入栈一个新路由时，原来的路由仍然会被保存在内存中，如果想在路由没用的时候释放其所占用的所有资源，可以设置maintainState为false
    bool fullscreenDialog = false, // 表示新的路由页面是否是一个全屏的模态对话框
  })
```



### 2. Navigator

`Navigator` 是用来管理路由的一个组件。它通过栈来管理活动路由集合。并提供了一系列的方法来进行操作路由栈。

最常用的是`push`、`pushNamed`、`pop`。



### 3. 命名路由

`onGenerateRoute`



## package管理



## 资源管理



## 状态管理

最常见的方法：

- Widget管理自己的状态。
- Widget管理子Widget状态。
- 混合管理（父Widget和子Widget都管理状态）。

一些原则可以帮助你做决定：

- 如果状态是用户数据，如复选框的选中状态、滑块的位置，则该状态最好由父Widget管理。
- 如果状态是有关界面外观效果的，例如颜色、动画，那么状态最好由Widget本身来管理。
- 如果某一个状态是不同Widget共享的则最好由它们共同的父Widget管理。

全局状态管理器来处理这种相距较远的组件之间的通信。目前主要有两种办法：

1. 实现一个全局的事件总线，将语言状态改变对应为一个事件，然后在APP中依赖应用语言的组件的`initState` 方法中订阅语言改变的事件。当用户在设置页切换语言后，我们发布语言改变事件，而订阅了此事件的组件就会收到通知，收到通知后调用`setState(...)`方法重新`build`一下自身即可。
2. 使用一些专门用于状态管理的包，如Provider、Redux。







