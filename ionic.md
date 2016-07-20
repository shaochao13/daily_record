[ionic图标](http://ionicons.com/)

# 安装
1. 需要先安装node.js环境,从官网下载最新的安装包进行安装，不要使用brew进行安装。
2. 如果没有安装Andriod \ IOS 模拟器，需要先进行安装。     
    mac下需要安装Xcode，或者执行` xcode-select --install`,然后再执行：      
    ```
    $ npm install -g ios-sim    
    $ npm install -g ios-deploy
    ```
3. 安装最新版本的 cordova 和 ionic :    
    ```
    sudo npm install -g cordova ionic
    ```
4. 如果出现报权限问题，可以执行如下命令：  
    ```
    npm config set unsafe-perm true
    ```
5. 添加Android平台
    ```
    cd myApp
    ionic platform add android //这行可能会报错
    ionic build android
    ionic emulate android
    ```
    添加android的时候可能会报错,解决的方法很简单，将ionic换成cordova即可:
    ```
    cd myApp
    cordova platform add android //这行可能会报错
    cordova build android
    cordova emulate android
    ```
6. ngCordova安装      
    ngCordova是在Cordova Api基础上封装的一系列开源的AngularJs服务和扩展，让开发者可以方便的在HybridApp开发中调用设备能力，即可以在AngularJs代码中访问设备能力Api。        
    - 进入到工程目录，使用bower工具安装
        ```
        bower install ngCordova
        ```
    - 然后将ng-cordova.js或者ng-cordova.min.js添加到index.html中的cordova.js引入之前，例如：
        ```html
        <script src="lib/ngCordova/dist/ng-cordova.js"></script>
        <script src="cordova.js"></script>
        ```
    - 然后再angular中添加ngCordova依赖，
        ```javascript
        angular.module('myApp', ['ngCordova'])
        ```

[ionic图标](http://ionicons.com/)

# ionic工具类API和配置
- ***$ionicConfigProvider***
    ```javascript
    var myApp = angular.module('reallyCoolApp', ['ionic']);

    myApp.config(function($ionicConfigProvider) {
    $ionicConfigProvider.views.maxCache(5);
    //配置android平台的缓存
    $ionicConfigProvider.platform.android.views.maxCache(5);

    // note that you can also chain configs
    $ionicConfigProvider.backButton.text('Go Back').icon('ion-chevron-left');
    });
    ```
    1. views.transition(transition/string)     
    设置视图之间的过渡切换效果，默认是platform，可选值如下：
        > platform: 根据平台动态选择相应的过渡效果，如果不是android或者ios，则默认是ios.   
        ios: iOS过渡效果.   
        android: Android过渡效果.   
        none: 无过渡效果.    

    2. views.maxCache(maxNumber/number)     
    设置DOM中缓存的最大视图数目，如果超过限制，则移除最长时间没有显示的视图。DOM缓存中的视图会缓存scope和当前状态以及滚动的位置。缓存中的scope并不在 $watch 监听生命周期中，当视图重新显示的时候，会重新进入 $watch。如果 maximum cache 设置为 0, 离开的view会被立即从dom中移除, 下次再显示这个view的时候, 就会重新编译, 附加到dom上, 重新绑定到对应的元素.相当于是禁用缓存.

    3. views.forwardCache(value/boolean)    
    默认情况下，最近访问的视图会被缓存，当导航回到某个已经访问过的视图的时候，相同实例的数据和dom元素会被重新引用到。然而，当回退到上一个视图的时候，刚刚前进的视图会被清除掉，如果你再次前进到这个视图，就会创建一个新的DOM节点元素和控制器实例。基本上任何一个前进访问的视图每次都会被重置。这个设置选项中设置为true的时候就会缓存前进的视图，而且不会每次加载的时候不会重置。

    4. scrolling.jsScrolling(value/boolean) 
    配置是使用js的scroll滚动还是使用原生的滚动。如果设置为false和在每个 ion-content中设置overflow-scroll=’true’一样的效果。

    5. backButton.icon(value/string)    
    设置返回按钮的图标。

    6. backButton.text(value/string)    
    设置返回按钮的文字。

    7. backButton.previousTitleText(value/boolean)  
    设置是否将上一个view视图的title设置成返回按钮的文字，iOS是默认的true。
    8. form.checkbox(value/string)  
    设置Checkbox的样式. Android 默认是方形square，iOS 默认是圆形circle.

    9. form.toggle(value/string)    
    设置Toggle元素的样式. Android默认是small，iOS默认是large.

    10. spinner.icon(value/string)  
    设置默认的spinner图标。可以是: android, ios, ios-small, bubbles, circles, crescent, dots, lines, ripple, or spiral.

    11. tabs.style(value/string)    
    设置tab的样式。 Android 默认是striped and iOS 默认是standard。可选的值是striped and standard.

    12. tabs.position(value/string) 
    设置Tab的位置. Android tab的位置默认在顶部，iOS 默认是在底部.可选的值是 top 和 bottom.

    13. templates.maxPrefetch(value/integer)    
    设置根据在$stateProvider.state中定义的模板url预取的模板数量。 如果设置为 0,当导航到新的页面时候用户必须等待加载到该页面. 默认是 30.

    14. navBar.alignTitle(value)    
    设置导航条的标题的对其方式。 默认是center。可选值如下：      
        > platform: 根据平台动态选择标题的样式，ios默认显示为center，android默认是left，如果不是ios或android，则默认显示center。  
        left: 导航条标题显示在左边    
        center: 导航条标题显示在中间  
        right: 导航条标题显示在右边   

    15. navBar.positionPrimaryButtons(value/string) 
    设置导航条中主导航按钮的对其位置，默认是 left.

    16. platform: 根据平台动态选择标题的样式，ios默认显示为left，android默认是right，如果不是ios或android，则默认显示left。      
        > left: Left align the primary navBar buttons in the navBar   
        right: Right align the primary navBar buttons in the navBar.    

    17. navBar.positionSecondaryButtons(value/string)       
    设置导航条中次导航按钮的对其位置，默认是 left.

    18. platform: 根据平台动态选择标题的样式，ios默认显示为right，android默认是left，如果不是ios或android，则默认显示right。    
        > left: Left align the primary navBar buttons in the navBar   
        right: Right align the primary navBar buttons in the navBar.

- ***ionic.Platform平台相关接口***
    ```javascript
    angular.module('PlatformApp', ['ionic'])
    .controller('PlatformCtrl', function($scope) {

    ionic.Platform.ready(function(){
        // will execute when device is ready, or immediately if the device is already ready.
    });

    var deviceInformation = ionic.Platform.device();

    var isWebView = ionic.Platform.isWebView();
    var isIPad = ionic.Platform.isIPad();
    var isIOS = ionic.Platform.isIOS();
    var isAndroid = ionic.Platform.isAndroid();
    var isWindowsPhone = ionic.Platform.isWindowsPhone();

    var currentPlatform = ionic.Platform.platform();
    var currentPlatformVersion = ionic.Platform.version();

    ionic.Platform.exitApp(); // stops the app
    });
    ```

    1. ready(callback)  
    设备准备就绪后触发回调函数, 如果设备本来已经就绪会立即触发回调函数。该方法可以在任何地方运行，不用包装在方法中。当APP中有WebView (Cordova), 设备就绪时就会调用回调。如果app是在web browser中, 会在window.load之后调用回调函数。 需要注意Cordova features (Camera, FileSystem, etc) 在web浏览器中都不会起作用。

    2. setGrade(grade)  
    Set the grade of the device: ‘a’, ‘b’, or ‘c’. ‘a’ is the best (most css features enabled), ‘c’ is the worst. By default, sets the grade depending on the current device.

    3. device() 
    Return the current device (given by cordova).returns: object The device object.

    4. isWebView()  
    Returns: boolean Check if we are running within a WebView (such as Cordova).

    5. isIPad()     
    Returns: boolean Whether we are running on iPad.

    6. isIOS()  
    Returns: boolean Whether we are running on iOS.

    7. isAndroid()  
    Returns: boolean Whether we are running on Android.

    8. isWindowsPhone()     
    Returns: boolean Whether we are running on Windows Phone.

    9. platform()   
    Returns: string The name of the current platform.

    10. version()   
    Returns: number The version of the current device platform.

    11. exitApp()   
    Exit the app.

    12. showStatusBar(shouldShow/boolean)   
    Shows or hides the device status bar (in Cordova). Requires cordova plugin add org.apache.cordova.statusbar

    13. fullScreen([showFullScreen/boolean], [showStatusBar/boolean])   
    Sets whether the app is fullscreen or not (in Cordova).

- ***ionic.Platform属性***

    1. boolean isReady  
    Whether the device is ready.

    2. boolean isFullScreen     
    Whether the device is fullscreen.

    3. Array(string) platforms      
    An array of all platforms found.

    4. string grade     
    What grade the current platform is.

[ionic图标](http://ionicons.com/)

# [CSS组件](http://www.ionic.wang/css_doc-index.html)
- Header \ Footer
- Button
- List
- card卡片
- 表单
- Toggle选择
- checkbox
- radio
- range范围选择
- select下拉选框
- tabs组件
- color定制   
    ---*可以修改ionic.css，由于使用的sass，可以修改_variables.scss文件来扩展或修改配色。*
- padding   
    ***padding***:  Adds padding around every side.    
    ***padding-vertical***: Adds padding to the top and bottom.   
    ***padding-horizontal***: Adds padding to the left and right.     
    ***padding-top***: Adds padding to the top.       
    ***padding-right***: Adds padding to the right.       
    ***padding-bottom***: Adds padding to the bottom.     
    ***padding-left***:  Adds padding to the left. 
- 动画样式    
- grid系统    
    ---*ionic的网格系统采用的是 [CSS Flexible Box Layout Module标准](https://www.w3.org/TR/css-flexbox-1/)，所有支持ionic的设备都支持flexbox。可以用row样式指定行，用col样式指定列。*
    1. 列宽  
    2. 偏移量
    3. 响应式grid
 
|指定列宽class 名称  |   偏移量class 名称          |    所占比例    |
|-----------------:|:-------------------------:|:--------------|
|.col-10           |.col-offset-10             |10%            |
|.col-20           |.col-offset-20             |20%            |
|.col-25	       |.col-offset-25             |25%            |
|.col-33	       |.col-offset-33             |33.3333%       |
|.col-50	       |.col-offset-50             |50%            |
|.col-67	       |.col-offset-67             |66.6666%       |
|.col-75	       |.col-offset-75             |75%            |
|.col-80	       |.col-offset-80             |80%            |
|.col-90	       |.col-offset-90             |90%            | 
|                  |                           |               |


|Responsive Class   |	 Break when roughly         |
|------------------:|:------------------------------|
|.responsive-sm		|Smaller than landscape phone   |
|.responsive-md		|Smaller than portrait tablet   |
|.responsive-lg		|Smaller than landscape tablet  |
|                   |                               |
 
 
# javascript UI库
- Tabs  
    1. 通过tab栏切换不同的page，注意：不要将ion-tabs放在ion-content里面，会导致一个css错误。   
    2. android和ios在默认样式上有一些不同的地方，官方文档中都有说明，tab位置，***$ionicConfigProvider***.tabs.position(value) 。     
    3. Android 默认是顶部(top)，Ios是底部 (bottom) 。
    ```javascript
    var myApp = angular.module('reallyCoolApp', ['ionic']);
    myApp.config(function($ionicConfigProvider) {
    $ionicConfigProvider.views.maxCache(5);
    // note that you can also chain configs
    $ionicConfigProvider.tabs.position("bottom");
    });
    ```
    ```html
    <ion-tabs class="tabs-positive tabs-icon-only">
        <ion-tab title="Home" icon-on="ion-ios7-filing" icon-off="ion-ios7-filing-outline">
            <!-- Tab 1 content -->
        </ion-tab>
        <ion-tab title="About" icon-on="ion-ios7-clock" icon-off="ion-ios7-clock-outline">
            <!-- Tab 2 content -->
        </ion-tab>
        <ion-tab title="Settings" icon-on="ion-ios7-gear" icon-off="ion-ios7-gear-outline">
            <!-- Tab 3 content -->
        </ion-tab>
    </ion-tabs>
    ```
    4. ion-tab      
    作为ion-tabs的tab项，用于切换选择tab的内容，只有当tab被选中时，其对应的内容content才会存在。每个ion tab都有自己的查看历史。   
    ```html
    <!--用法-->
    <ion-tab
        title="Tab!"
        icon="my-icon"
        href="#/tab/tab-link"
        on-select="onTabSelected()"
        on-deselect="onTabDeselected()">
    </ion-tab>
    ```
    ion-tab的属性如下：       
    
|属性                    |	类型        | 	描述               |
|----------------------:|---------------|------------------------|
|title	                |   string	    |   The title of the tab.|
|href(optional)         |	string      |	The link that this tab will navigate to when tapped.|
|icon(optional)         |	string      |	The icon of the tab. If given, this will become the default for icon-on and icon-off.|
|icon-on(optional)      |	string      |	The icon of the tab while it is selected.|
|icon-off(optional)     |	string      |	The icon of the tab while it is not selected.|
|badge(optional)        |	expression  |	The badge to put on this tab (usually a number).|
|badge-style(optional)	|expression	    |   The style of badge to put on this tab (eg tabs-positive).|
|on-select(optional)    |expression     |	Called when this tab is selected.|
|on-deselect(optional)  |	expression  |	Called when this tab is deselected.|
|ng-click(optional)|	expression      |	By default, the tab will be selected on click. If ngClick is set, it will not. You can explicitly switch tabs using $ionicTabsDelegate.select().|
||||        
    
5. ***$ionicTabsDelegate***     
    是ion-tabs的一个api参数，通过这个可以选择切换不同的tab,可以通过$getByHandle 方法获取不同的tab的实例  
             
    ```html
    <body ng-controller="MyCtrl">
    <ion-tabs>
        <ion-tab title="Tab 1">
        Hello tab 1!
        <button ng-click="selectTabWithIndex(1)">Select tab 2!</button>
        </ion-tab>
        <ion-tab title="Tab 2">Hello tab 2!</ion-tab>
    </ion-tabs>
    </body>
    ```
    ```javascript
    function MyCtrl($scope, $ionicTabsDelegate) {
        $scope.selectTabWithIndex = function(index) {
            $ionicTabsDelegate.select(index);
        }
    }
    ```
- ***ion-side-menus***        
    是一个带有边栏菜单的容器，可以通过点击按钮或者滑动屏幕来展开菜单。在js中可以通过 ***$ionicSideMenuDelegate*** 来获取该组件对应的实例。为了自动关闭已打开的menu，可以通过在ion-side-menu-content中的按钮或link添加menu-close样式。
    ```html
    <ion-side-menus>
    <!-- Center content -->
    <ion-side-menu-content ng-controller="ContentController">
    </ion-side-menu-content>

    <!-- Left menu -->
    <ion-side-menu side="left">
    </ion-side-menu>

    <!-- Right menu -->
    <ion-side-menu side="right">
    </ion-side-menu>
    </ion-side-menus>
    ```
    ```javascript
    function ContentController($scope, $ionicSideMenuDelegate) {
        $scope.toggleLeft = function() {
            $ionicSideMenuDelegate.toggleLeft();
        };
    }
    ```     

    1. ***ion-side-menu-content*** 展示主要内容的容器。可以通过滑动屏幕来展开menu     
    ```html
    <ion-side-menu-content
        edge-drag-threshold="true"
        drag-content="true">
    </ion-side-menu-content>
    ```

    2. ***ion-side-menu*** 存放侧边栏的容器     
    ```html
    <!--
        side	                string	    Which side the side menu is currently on. Allowed values: ‘left’ or ‘right’.
        is-enabled(optional)	boolean	    Whether this side menu is enabled.
        width(optional)	        number      How many pixels wide the side menu should be. Defaults to 275.
    -->
    <ion-side-menu
    side="left" 
    width="myWidthValue + 20"
    is-enabled="shouldLeftSideMenuBeEnabled()">
    </ion-side-menu>
    ```

    3. ***menu-toggle*** 用于切换显示侧边栏菜单    
    ```html
    <ion-view>
    <ion-nav-buttons side="left">
    <button menu-toggle="left" class="button button-icon icon ion-navicon"></button>
    </ion-nav-buttons>
    ...
    </ion-view>
    ```     

    4. ***menu-close*** 关闭当前打开的menu   
    下面的例子是在一个menu栏里面的一项菜单，点击可以关闭menu    
    ```html
    <a menu-close href="#/home" class="item">Home</a>
    ```

    5. ***$ionicSideMenuDelegate***   用于指定控制 ionSideMenus 的实例,其有很多的方法，可以查看API   
    ```html
    <body ng-controller="MainCtrl">
    <ion-side-menus>
        <ion-side-menu-content>
        Content!
        <button ng-click="toggleLeftSideMenu()">
            Toggle Left Side Menu
        </button>
        </ion-side-menu-content>
        <ion-side-menu side="left">
        Left Menu!
        <ion-side-menu>
    </ion-side-menus>
    </body>
    ```
    ```javascript
    function MainCtrl($scope, $ionicSideMenuDelegate) {
    $scope.toggleLeftSideMenu = function() {
        $ionicSideMenuDelegate.toggleLeft();
    };
    }
    ```

# 问题处理集


