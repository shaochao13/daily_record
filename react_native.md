# 问题解决方案
1. ":CFBundleIdentifier", Does Not Exist

    `解决方法：`在创建项目时，指定 `--version` 参数，且值为 `0.44.3`
    ```
    react-native init DemoApp --version 0.44.3
    ```
    

# key word:
- flex 
- flexDirection ---> 'column' | 'row'
- justifyContent ---> 'flex-start' | 'flex-end' | 'space-between' | 'space-around'
- alignItems ----> 'flex-start' | 'flex-end' | 'center' | 'stretch'
- alignSelf ---> 'flex-end' | 'flex-start' | 'center'
- flexWrap ---> 'nowrap' | 'wrap'

- react-navigation



# 组件的生命周期
![](./images/RN组件生命周期.png)
*Mounting(装载)*

当组件实例被创建并将其插入 DOM 时，这些方法将被调用：

    constructor()
    componentWillMount()
    render()
    componentDidMount()

*Updating*

改变 props 或 state 可以触发更新事件。 在重新渲染组件时，这些方法将被调用：

    componentWillReceiveProps(nextProps)
    shouldComponentUpdate(nextProps, nextState)
    componentWillUpdate(nextProps, nextState)
    render()
    componentDidUpdate(prevProps, prevState)

*Unmounting(卸载)*

当一个组件从 DOM 中删除时，这个方法将被调用：

    componentWillUnmount()


有用的网址:
- reat.parts/native 用于第三方库的搜索

有用的模块：
- lodash js工具库
- speakeasy 可以用来生成一些加密的随机值
- [Bluebird](https://github.com/petkaantonov/bluebird) (Promise实现)
- xss 用来防止XSS攻击
---RN 特有---

- react-native-video 视频播放
- react-native-button 
- react-native-swiper 轮播 
- [react-native-sk-countdown](https://github.com/shigebeyond/react-native-sk-countdown) 倒计时 
- react-native-image-picker 本地相册
- react-native-propgress 进度条