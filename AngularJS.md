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