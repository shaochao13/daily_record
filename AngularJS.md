# AngularJS 表达式
1. AngularJS 表达式写在双大括号内：{{ expression }}。
2. AngularJS 表达式把数据绑定到 HTML，这与 ng-bind 指令有异曲同工之妙。
3. AngularJS 将在表达式书写的位置"输出"数据。
4. AngularJS 表达式 很像 JavaScript 表达式：它们可以包含文字、运算符和变量。

## AngularJS 数字     
```html
<div ng-app="" ng-init="quantity=1;cost=5">
<p>总价： {{ quantity * cost }}</p>
</div>
```     
    使用 ng-bind 的相同实例：   
```html
<div ng-app="" ng-init="quantity=1;cost=5">
<p>总价： <span ng-bind="quantity * cost"></span></p>
</div> 
```

## AngularJS 字符串
```html
<div ng-app="" ng-init="firstName='John';lastName='Doe'">
<p>姓名： {{ firstName + " " + lastName }}</p>
</div>
```
    使用 ng-bind 的相同实例：
```html
<div ng-app="" ng-init="firstName='John';lastName='Doe'">
<p>姓名： <span ng-bind="firstName + ' ' + lastName"></span></p>
</div>
```

## AngularJS 对象
```html
<div ng-app="" ng-init="person={firstName:'John',lastName:'Doe'}">

<p>姓为 {{ person.lastName }}</p>

</div>
```
    使用 ng-bind 的相同实例：
```html
<div ng-app="" ng-init="person={firstName:'John',lastName:'Doe'}">

<p>姓为 <span ng-bind="person.lastName"></span></p>

</div>
```
## AngularJS 数组
```html
<div ng-app="" ng-init="points=[1,15,19,2,40]">

<p>第三个值为 {{ points[2] }}</p>

</div>
```
    使用 ng-bind 的相同实例：
```html
<div ng-app="" ng-init="points=[1,15,19,2,40]">

<p>第三个值为 <span ng-bind="points[2]"></span></p>

</div>
```
    - 类似于 JavaScript 表达式，AngularJS 表达式可以包含字母，操作符，变量。        
    - 与 JavaScript 表达式不同，AngularJS 表达式可以写在 HTML 中。        
    - 与 JavaScript 表达式不同，AngularJS 表达式不支持条件判断，循环及异常。      
    - 与 JavaScript 表达式不同，AngularJS 表达式支持过滤器。      

# AngularJS 指令
1. AngularJS 通过被称为 指令 的新属性来扩展 HTML。
2. AngularJS 通过内置的指令来为应用添加功能。
3. AngularJS 允许你自定义指令。
4. AngularJS 指令是扩展的 HTML 属性，带有前缀 ng-。   
    > ng-app 指令初始化一个 AngularJS 应用程序。  
    > ng-init 指令初始化应用程序数据。    
    > ng-model 指令把元素值（比如输入域的值）绑定到应用程序。  

[AngularJS 参考手册](http://www.runoob.com/angularjs/angularjs-reference.html) 
```html
<div ng-app="" ng-init="firstName='John'">
<!-- ng-app 指令告诉 AngularJS，<div> 元素是 AngularJS 应用程序 的"所有者"。 -->
  <p>在输入框中尝试输入：</p>
  <p>姓名：<input type="text" ng-model="firstName"></p>
  <p>你输入的为： {{ firstName }}</p>
</div>
```
一个网页可以包含多个运行在不同元素中的 AngularJS 应用程序。     
## 数据绑定
    AngularJS 中的数据绑定，同步了 AngularJS 表达式与 AngularJS 数据。   
    {{ firstName }} 是通过 ng-model="firstName" 进行同步。
```html
<div ng-app="" ng-init="quantity=1;price=5">

<h2>价格计算器</h2>

数量： <input type="number" ng-model="quantity">
价格： <input type="number" ng-model="price">
<p><b>总价：</b> {{ quantity * price }}</p>
</div>
```

## 重复 HTML 元素 
***ng-repeat*** 指令对于集合中（数组中）的每个项会 克隆一次 HTML 元素。     
***ng-repeat*** 指令会重复一个 HTML 元素：
```html
<div ng-app="" ng-init="names=['Jani','Hege','Kai']">
  <p>使用 ng-repeat 来循环数组,从而在页面上生成多个li</p>
  <ul>
    <li ng-repeat="x in names">
      {{ x }}
    </li>
  </ul>
</div>
```
***ng-repeat*** 指令用在一个对象数组上：
```html
<div ng-app="" ng-init="names=[
{name:'Jani',country:'Norway'},
{name:'Hege',country:'Sweden'},
{name:'Kai',country:'Denmark'}]">

<p>循环对象：</p>
<ul>
  <li ng-repeat="x in names">
    {{ x.name + ', ' + x.country }}
  </li>
</ul>
</div>
```
## ng-app 指令
1. ng-app 指令定义了 AngularJS 应用程序的 根元素。   
2. ng-app 指令在网页加载完毕时会自动引导（自动初始化）应用程序。 

## ng-model 指令
ng-model 指令 绑定 HTML 元素 到应用程序数据。
ng-model 指令也可以： 
> 为应用程序数据提供类型验证（number、email、required）。     
> 为应用程序数据提供状态（invalid、dirty、touched、error)。       
> 为 HTML 元素提供 CSS 类。    
> 绑定 HTML 元素到 HTML 表单。      

## 创建自定义的指令
使用 .directive 函数来添加自定义的指令。  
要调用自定义指令，HTML 元素上需要添加自定义指令名。        

    使用驼峰法来命名一个指令， runoobDirective, 但在使用它时需要以 - 分割, runoob-directive:
```html
<body ng-app="myApp">
<runoob-directive></runoob-directive>
<script>
var app = angular.module("myApp", []);
app.directive("runoobDirective", function() {
    return {
        template : "<h1>自定义指令!</h1>"
    };
});
</script>
</body>
```
- 通过***元素名***调用
```html
<!DOCTYPE html>
<html>
<head>
<meta charset="utf-8">
<script src="http://apps.bdimg.com/libs/angular.js/1.4.6/angular.min.js"></script> 
</head> 
<body ng-app="myApp">
<runoob-directive></runoob-directive>
<script>
var app = angular.module("myApp", []);
app.directive("runoobDirective", function() {
    return {
        template : "<h1>自定义指令!</h1>"
    };
});
</script>
</body>
</html>
```
- 通过***属性***调用
```html
<!DOCTYPE html>
<html>
<head>
<meta charset="utf-8">
<script src="http://apps.bdimg.com/libs/angular.js/1.4.6/angular.min.js"></script> 
</head>
<body ng-app="myApp">
<div runoob-directive></div>
<script>
var app = angular.module("myApp", []);
app.directive("runoobDirective", function() {
    return {
        template : "<h1>自定义指令!</h1>"
    };
});
</script>
</body>
</html>
```
- 通过***类名***调用
```html
<!DOCTYPE html>
<html>
<head>
<meta charset="utf-8">
<script src="http://apps.bdimg.com/libs/angular.js/1.4.6/angular.min.js"></script> 
</head>
<body ng-app="myApp">
<div class="runoob-directive"></div>
<script>
var app = angular.module("myApp", []);
app.directive("runoobDirective", function() {
    return {
        restrict : "C",
        template : "<h1>自定义指令!</h1>"
    };
});
</script>
<p><strong>注意：</strong> 你必须设置 <b>restrict</b> 的值为 "C" 才能通过类名来调用指令。</p>
</body>
</html>
```
- 通过***注释***调用
```html
<!DOCTYPE html>
<html>
<head>
<meta charset="utf-8">
<script src="http://apps.bdimg.com/libs/angular.js/1.4.6/angular.min.js"></script> 
</head>
<body ng-app="myApp">
<!-- directive: runoob-directive -->
<script>
var app = angular.module("myApp", []);
app.directive("runoobDirective", function() {
    return {
        restrict : "M",
        replace : true,
        template : "<h1>自定义指令!</h1>"
    };
});
</script>
<p><strong>注意：</strong> 我们需要在该实例添加 <strong>replace</strong> 属性， 否则评论是不可见的。</p>
<p><strong>注意：</strong> 你必须设置 <b>restrict</b> 的值为 "M" 才能通过注释来调用指令。</p>
</body>
</html>
```
## 限制使用
    通过添加 ***restrict*** 属性,来设置指令只能通过特定的方式来调用:  
    restrict 默认值为 EA, 即可以通过元素名和属性名来调用指令。    
    ***restrict*** 值可以是以下几种:
    > E 只限元素名使用     
    > A 只限属性使用      
    > C 只限类名使用      
    > M 只限注释使用      
