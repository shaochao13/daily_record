## Javascript的组成
-  `ECMAScript`：Javascript的语法标准。
-  `DOM`：Document Object Model(文档对象模型)，Js操作页面上的元素的API。
-  `BOM`：Browser Object Model(浏览器对象模型)，Js操作浏览器部分功能的API。
通俗理解就是：ECMAScript 是 JS 的语法；DOM 和 BOM 是浏览器运行环境为 JS 提供的 API。

## Javascript的特点
- 解释型语言
- 单线程
- ECMAScript标准：ECMAScript 是一种由 ECMA 国际（前身为欧洲计算机制造商协会,英文名称是 European Computer Manufacturers Association）制定和发布的脚本语言规范。

## Javascript中的输出
### `alert()`语句
### `confirm()`语句（含确认/取消）
```js {.line-numbers}
var result = confirm('你确认吗？');
console.log(result);
```
### `prompt()`语句：弹出能够让用户输入的对话框。
```js {.line-numbers}
var a = prompt('请输入点什么东西');
console.log(a);
```
### `document.write()` 网页内容区域输出
### `console` 控制台输出
```js {.line-numbers}
console.log('1'); //普通打印
console.warn('2'); //警告打印
console.error('3'); //错误打印
```

## Javascript 语法基础
### 1. 常量与变量
#### 常量

ES6中通过`const`来自定义常量。
常量有下面这几种：
-   数字常量（数值常量）
-   字符串常量
-   布尔常量：在JS中用 true 和 false 来表达。
-   自定义常量

#### 变量

**本质**：变量是程序在内存中申请的一块用来存放数据的空间。
在ES5中使用`var`来声明一个变量。
在ES6中使用`const`来声明一个常量，使用`let`来声明一个变量。
一个变量如果没有进行初始化（只声明，不赋值），那么这个变量中存储的值是`undefined`。

**变量的命名规则**
-   只能由字母(A-Z、a-z)、数字(0-9)、下划线(_)、美元符( $ )组成。
-   不能以数字开头。必须以字母(A-Z、a-z)、下划线(_)或者美元符( $ )开头。变量名中不允许出现空格。尤其注意，变量名中不能出现**中划线**`-`。
-   严格区分大小写（JS 是区分大小写的语言）。
-   不能使用 JS 语言中保留的「关键字」和「保留字」作为变量名。下一篇文章会讲。
-   变量名长度不能超过 255 个字符。
-   汉语可以作为变量名。但是不建议使用，因为 low。

建议遵守：
-   命名要有可读性，方便顾名思义。
-   建议用驼峰命名法。比如 getElementById、getUserInfo、aaaOrBbbAndCcc等。


## 数据类型
JS 中一共有8种数据类型：
-   **基本数据类型（值类型）**：`String字符串`、`Number 数值`、`BigInt 大型数值`、`Boolean 布尔值`、`Null 空值`、`Undefined 未定义`、`Symbol`。
-   **引用数据类型（引用类型）**：Object 对象。
> 注意：内置对象 Function、Array、Date、RegExp、Error 等都是属于 Object 类型。也就是说，除了那七种基本数据类型之外，其他的，都称之为 Object 类型。
>
> BigInt 和 Symbol 是ES6中新增的类型。

JS中，所有的变量都是保存在栈内存中的。基本数据类型的值，直接保存在栈内存中。值与值之间是独立存在，修改一个变量不会影响其他的变量。
引用数据类型中的对象是保存到堆内存中的。每创建一个新的对象，就会在堆内存中开辟出一个新的空间；而变量保存了对象的内存地址（对象的引用），保存在栈内存当中。如果两个变量保存了同一个对象的引用，当一个通过一个变量修改属性时，另一个也会受到影响。

### String字符串
字符串型可以是引号中的任意文本，其语法为：双引号 "" 或者单引号 ''。

#### 获取字符串的长度
通过字符串的`length`属性即可获取整个字符串的长度。
字符串的 `length` 属性，在判断字符串的长度时：
- 一个中文算一个字符，一个英文算一个字符
- 一个标点符号（包括中文标点、英文标点）算一个字符
- 一个空格算一个字符

#### 字符串拼接
拼接`语法`：
``` {.line-numbers}
字符串 + 任意数据类型 = 拼接之后的新字符串;
```
拼接规则：拼接前，会把与字符串相加的这个数据类型转成字符串，然后再拼接成一个新的字符串。

#### 字符串的不可变性
字符串里面的值不可被改变。虽然看上去可以改变内容，但其实是地址变了，内存中新开辟了一个内存空间。

#### 模板字符串（模板字面量）
ES6 中引入了模板字符串，让我们省去了字符串拼接的烦恼。
```js {.line-numbers}
var name = '张三';
var age = '30';

console.log('我是' + name + ',age:' + age); //传统写法
// 插入变量
console.log(`我是${name},age:${age}`); //ES6 写法。注意语法格式


const a = 5;
const b = 10;

// 插入表达式
console.log(`this is ${a + b} and not ${2 * a + b}.`);


// 模板字符串中可以换行
const result = {
    name: '张三',
    age: 30,
    sex: '男',
};

// 模板字符串支持换行
const html = `<div>
	<span>${result.name}</span>
	<span>${result.age}</span>
	<span>${result.sex}</span>
</div>`;

console.log(html); // 打印结果也会换行
```

#### 模板字符串中可以调用函数
```js {.line-numbers}
function getName() {
    return 'zhangsan';
}

console.log(`${getName()}`);
```

#### 模板字符串支持嵌套使用
```js {.line-numbers}
const nameList = ['张三', '李四', '王五'];

function myTemplate() {
    return `<ul>
	${nameList.map((item) => `<li>${item}</li>`).join('')}
	</ul>`;
}
console.log(myTemplate());
```

#### 常用方法
1. toUpperCase()/toLowerCase() 把字符串转变为大写/小写。
2. charAt() 返回指定位置的字符。
3. indexOf() 返回某个指定字符串值在字符串中的首次出现的位置。
> 语法：stringObject.indexOf(substring, startpos) 如果要检索的字符串值没有出现，则返回-1。
4. split() 将字符串分割为字符串数组，并返回此数组。
> 语法：stringObject.split(sparator, limit) 。如把空字符串("")用作separator,那stringObject中的每个字符之间都会被分割。
5. substring() 提取字符串中介于两个指定下标之间的字符。
> 语法：stringObject.substring(starPos, stopPos)
- 返回的内容是从 start开始(包含start位置的字符)到 stop-1 处的所有字符，其长度为 stop 减start。
- 如果参数 start 与 stop 相等，那么该方法返回的就是一个空串（即长度为 0 的字符串）。
- 如果 start 比 stop 大，那么该方法在提取子串之前会先交换这两个参数。

6. substr() 从字符串中提取从startPos位置开始的指定数目的字符串。
> 语法：stringObject.substr(startPos,length)。
>
**注意：**
- 如果参数startPos是负数，从字符串的尾部开始算起的位置。也就是说，-1 指字符串中最后一个字符，-2 指倒数第二个字符，以此类推。
- 如果startPos为负数且绝对值大于字符串长度，startPos为0。

### Boolean 布尔值类型
> 布尔型有两个值：true 和 false。
> 布尔型和数字型相加时， true 按 1 来算 ，false 按 0 来算。

### Number 数值型
> 在 JS 中**所有的数值**都是 Number 类型，包括整数和浮点数（小数）。

#### 数值范围
由于内存的限制，ECMAScript 并不能保存世界上所有的数值。
> 最大值：`Number.MAX_VALUE`，这个值为： 1.7976931348623157e+308
> 最小值：`Number.MIN_VALUE`，这个值为： 5e-324

> 如果使用 Number 表示的变量超过了最大值，则会返回 `Infinity。`
> 无穷大（正无穷）：`Infinity`
> 无穷小（负无穷）：`-Infinity`
**注意**：`typeof Infinity`的返回结果是 `number`。

如果加号两边都是 Number 类型，此时是数字相加。否则，就是连字符（用来连接字符串）。

#### NaN
> `NaN`：是一个特殊的数字，表示 Not a Number，非数值。

**注意**：
> `typeof NaN`的返回结果是 `number` 。
> `Undefined` 和任何数值计算的结果为 `NaN`。 `NaN` 与任何值都不相等，包括 `NaN` 本身。

#### 隐式转换
`"2"+1` 得到的结果其实是`字符串`，但是`"2"-1`得到的结果却是数值`1`，这是因为计算机自动帮我们进行了“隐式转换”。
```js {.line-numbers}
var a = '4' + 3 - 6;
console.log(a);
// 输出：37
```

#### 浮点数的运算
> 在 JS 中，整数的运算基本可以保证精确；但是小数的运算，可能会得到一个不精确的结果。所以，千万不要使用 JS 进行对精确度要求比较高的运算。

处理数学运算的精度问题:
- 如果只是一些简单的精度问题，可以使用 `toFix()` 方法进行小数的截取。
- 在实战开发中，关于浮点数计算的精度问题，往往比较复杂。市面上有很多针对数学运算的开源库，比如`decimal.js`、 `Math.js`。这些开源库都比较成熟，可以直接拿来用。
- Math.js：属于很全面的运算库，文件很大，压缩后的文件就有 500kb。如果你的项目涉及到大型的复杂运算，可以使用 Math.js。
- decimal.js：属于轻量的运算库，压缩后的文件只有 32kb。大多数项目的数学运算，使用 decimal.js 足够了。


## `Null` 空对象 与 `Undefined` 未定义类型
### `Null`

null 专门用来定义一个空对象。
- `null` 虽然是一个单独的数据类型，但 `null` 相当于是一个 `object` ，只不过地址为空（空指针）而已。
- Null 类型的值只有一个，就是 `null` 。比如 let a = null。
- 使用 `typeof` 检查一个 `null` 值时，会返回 obj`ect 。

### `Undefined`
- Undefined 类型的值只有一个，就是 undefind。比如 let a = undefined。
- 使用 typeof 检查一个 undefined 值时，会返回 undefined。

#### 为`undefined`的几种情景：
- 变量已声明，未赋值时
```js {.line-numbers}
let name;
console.log(name); // 打印结果：undefined
console.log(typeof name); // 打印结果：undefined
```
- 变量未声明（未定义）时
```js {.line-numbers}
// 如果从未声明一个变量，就去使用它，则会报错（这个大家都知道）；
// 如果用 typeof 检查这个变量时，会返回 undefined。

onsole.log(typeof a); // undefined
console.log(a); // 打印结果：Uncaught ReferenceError: a is not defined
```
- 函数无返回值时

```js {.line-numbers}
//如果一个函数没有返回值，那么，这个函数的返回值就是 undefined。
function foo() {}
console.log(foo()); // 打印结果：undefined
```
- 调用函数时，未传参

```js {.line-numbers}
//调用函数时，如果没有传参，那么，这个参数的值就是 undefined。
function foo(name) {
    console.log(name);
}

foo(); // 调用函数时，未传参。执行函数后的打印结果：undefined
```

```js {.line-numbers}
//实际开发中，如果调用函数时没有传参，我们可以根据需要给形参设置一个默认值
function foo(name) {
    name = name || 'Zhangsan';
}

//ES6
function foo(name = 'Zhangsan') {}

```

### null 和 undefind 区别
- `null == undefined` 的结果为 `true`。
- `null === undefined` 的结果为 `false`。
- `10 + null` 结果为 10。
- `10 + undefined` 结果为 `NaN`。

> 规律总结：
> 任何值和 `null` 运算，`null` 可看做 `0` 运算。
> 任何数据类型和 `undefined` 运算都是 NaN。

## `typeof` 和 数据类型转换

### `typeof` 
`typeof` 这个运算符的返回结果就是变量的类型:

|typeof 的代码写法|返回结果
|:----|:----|
typeof 数字 |   number
typeof 字符串   | string
typeof 布尔型   |   boolean
typeof 对象 |   object
typeof 方法 |   function
typeof null |   object
typeof undefined    |   undefined
typeof []   |   object
typeof {}   |   object
|||
> `typeof null` 的返回值也是 object 呢？因为 null 代表的是空对象。     
> `typeof NaN` 的返回值是 number，上一篇文章中讲过，NaN 是一个特殊的数字。     
> `空数组`、`空对象`都是引用数据类型 Object。       

### 类型转换

1.调用toString()方法   

语法：
```javascript
//该方法不会影响到原变量，它会将转换的结果返回。
变量.toString();
var result = 变量.toString();
// 
```
`null` 和 `undefined` 这两个值*没有* `toString()` 方法，所以它们不能用 toString() ,如果调用，会报错。       

Number 类型的变量，在调用 toString()时，可以在方法中传递一个整数作为参数。此时它会把数字转换为指定的进制，如果不指定则默认转换为 10 进制。
```Javascript
var a = 100;
// 转换为二进制的字符串
a = a.toString(2);  // 1100100
```
2.使用String()函数  

语法：
```javascript
String(变量);
```
- 对于 `Number`、`Boolean`、`Object` 而言，本质上就是调用 toString()方法。
- 但是对于 `null` 和 `undefined`，则不会调用 toString()方法。它会将 null 直接转换为 "null"。将 undefined 直接转换为 "undefined"。

3.使用 `Number()` 函数

(1) 字符串 ---> 数字
- 如果字符串中是纯数字，则直接将其转换为数字。
- 如果字符串是一个`空串`或是一个`全是空格`的字符串，则转换为`0`。
- 如果字符串中包含了其他非数字的内容（`小数点` 按数字来算, 只能包含一个`小数点`），则转换为`NaN`。

(2) 布尔 ---> 数字
- `true`  ---> `1` 
- `false` ---> `0`

(3) null、undefind ---> 数字
- `null` ---> `0`
- `undefind` ---> `NaN`

> 任何值做+a、-a运算时， 内部调用的是 Number() 函数。不会改变原数值。

4.使用 `parseInt()` 函数

`parseInt()`：将传入的数据当作字符串来处理，从左至右提取数值, 一旦遇到非数值就立即停止；停止时如何还没有提取到数值, 那么就返回`NaN`。`parseInt`是数据转换为10进制的数字！
- 如果字符串是一个`空串`或者是一个`全是空格`的字符串，转换时会`报错`。
- `Boolean` --> 数字，结果为： `NaN`
- `Null` --> 数字，结果为： `NaN`
- `Undefined` --> 数字，结果为： `NaN`

`Number()` 函数和 `parseInt()` 函数的区别：
- Number() ：千方百计地想转换为数字；如果转换不了则返回 NaN。
- arseInt()/parseFloat() ：先将其转换为 String 然后再操作,提取出最前面的数字部分；没提取出来，那就返回 NaN。
- 带两个参数时，表示在转换时，包含了进制转换。无论 parseInt() 里面的进制参数是多少，最终的转换结果是`十进制`。

```javascript
var a = '110';

var num = parseInt(a, 16); // 【重要】将 a 当成 十六进制 来看待，转换成 十进制 的 num

console.log(num);
```

```javascript
var a = 168.23;
console.log(parseInt(a)); //打印结果：168  （因为是先将 a 转为字符串"168.23"，然后然后再操作）

var b = true;
console.log(parseInt(b)); //打印结果：NaN （因为是先将 b 转为字符串"true"，然后然后再操作）

var c = null;
console.log(parseInt(c)); //打印结果：NaN  （因为是先将 c 转为字符串"null"，然后然后再操作）

var d = undefined;
console.log(parseInt(d)); //打印结果：NaN  （因为是先将 d 转为字符串"undefined"，然后然后再操作）

console.log(parseInt('2017在公众号上写了6篇文章')); //打印结果：2017

console.log(parseInt('2017.01在公众号上写了6篇文章')); //打印结果仍是：2017   （说明只会取整数）

console.log(parseInt('aaa2017.01在公众号上写了6篇文章')); //打印结果：NaN （因为不是以数字开头）
```

5.`parseFloat()` 函数

parseFloat() 的作用是：将字符串转换为浮点数。`parseFloat()`和 `parseInt()`的作用类似，不同的是，parseFloat()可以获得`小数部分`。
```javascript
var a = '123.456.789px';
console.log(parseFloat(a)); // 打印结果：123.456
```

6.转换为 `Boolean` 类型

> 其他的数据类型都可以转换为 Boolean 类型。

- 数字 --> 布尔。 `0` 和 `NaN` 是 false，其余的都是 true。
- 字符串 ---> 布尔。`空串`是false，其余的都是 true。全是空格的字符串，转换结果也是 true。字符串'0'的转换结果也是 true。
- `null` 和 `undefined` 都会转换为 false。
- 引用数据类型会转换为 true。注意，`空数组[]`和`空对象{}`，转换结果也是 true。
- 使用 `!!` 可以显式转换为 Boolean 类型。eg: `!!5` 的结果是 true。
- 使用 `Boolean()` 函数可以显式转换为 Boolean 类型。




#



#




#



## Date对象
1. *get/setFullYear()* 返回/设置年份，用**四位**数表示。
2. *getDay()* 返回星期，返回的是*0-6*的数字，**0**表示星期天。
3. *get/setTime()* 返回/设置时间，单位**毫秒数**，计算从*1970年1月1日零时*到日期对象所指的日期的毫秒数。
> 例如：如果将目前日期对象的时间推迟1小时：
```javascript
<script type="text/javascript">
  var mydate=new Date();
  document.write("当前时间："+mydate+"<br>");
  mydate.setTime(mydate.getTime() + 60 * 60 * 1000);
  document.write("推迟一小时时间：" + mydate);
</script>
```



## Math对象
1. ceil() 向上取整，语法：Math.ceil(x),返回的是大于或者等于x,并且与x最接近的整数。 floor()方法与ceil()相反，它为向下取整。
2. round() 把一个数字四舍五入为最接近的整数。  语法：Math.round(x)
    - 返回与x最接近的整数。
    - 对于0.5,将进行上舍入。（5.5将舍入为6）
    - 如果x与两侧整数同等接近，则结果接近*正无穷大*方向的数字值。

## Array 数组对象
数组对象是一个对象的集合，里边的对象可以是不同类型的。

1. concat() 用于连接两个或多个数组，此方法返回一个新数组，不改变原来的数组。
    > 语法：
     arrayObject.concat(array1,array2,...,arrayN);

2. join() 用于把数组中的所有元素通过指定的分隔符放入一个字符串。
    > 语法：
     arrayObject.join(分隔符);  //如果省略“分隔符”， 则使用逗号作用分隔符。

3. reverse() 用于颠倒数组中元素的顺序。
    > 语法：
     arrayObject.reverse()  会改变原来的数组，而不会创建新的数组。

4. slice() 切片函数，与python中的切片功能一样。
    > 语法：
     arrayObject.slice(start,end);

5. sort() 排列。默认情况下会调用每个数组项的toString()转型方法，然后比较得到的字符串，从而确定如何排序。***即默认情况下是按字符串进行排序的***
    > 语法：
     arrayObject.sort(方法函数);  // “方法函数”可以没有。

6. 栈方法(LIFO后进先出):
   > push() & pop()

7. 队列方法(FIFO先进先出):
   > shift()：从数组前端取出一项
     push()
     unshift() 在数组前端添加任意个项并返回新数组的长度。

## Function 类型(函数类型)
1. 没有重载概念。
2. arguments 主要用途是保存函数参数。但 其中有一个名叫***callee***的属性，该属性是一个指针，指向拥有这个arguments对象的函数。
```js {.line-numbers}
function factorial(num){
    if(num<=1){
        return 1;
    } else{
        return num * arguments.callee(num -1);
    }
}
```

caller 保存着调用当前函数的函数的引用，如果是在全局作用域中调用当前函数，它的值为null。
```js {.line-numbers}
function outer(){
    inner();
}
function inner(){
    alert(arguments.callee.caller);
}
outer();
````
3. 每个函数都包含: ***length***    表示函数希望接收的命名参数的个数。
```js {.line-numbers}
function sayName(name){
    alert(name);
}
function sum(num1, num2){
    return num1 + num2;
}
function sayHi(){
    albert("hi");
}

albert(sayName.length); //1
albert(sum.length);     //2
albert(sayHi.length);   //0
```
4. 每个函数都包含两个非继承而来的方法：apply() & call()
    - apply() 方法接收两个参数：一个是在其中运行函数的作用域， 另一个是参数数组。

```js {.line-numbers}
function sum(sum1, sum2){
    return num1 + num2;
}
function callSum1(num1, num2){
    return sum.apply(this, arguments);  //传入arguments对象
}
function callSum2(num1, num2){
    return sum.apply(this, [num1, num2]);   //传入数组
}
alert(callSum1(10,10)); //20
alert(callSum2(10,10)); //20
```

    - call() 一个参数也是作用域，其余参数都直接传递给函数。传递给函数的参数必须逐个列举出来。

```js {.line-numbers}
function sum(sum1, sum2){
    return num1 * num2;
}
function callSum(num1, num2){
    return sum.call(this, num1, num2);
}
albert(callSum(10,10)); //20
```

apply() & call()真正的用武之地，是能够扩充函数赖以运行的用途域,这样对象不需要与函数有任何耦合关系。

```js {.line-numbers}
window.color = 'red';
var o = {color: 'blue';}
function sayColor(){
    alert(this.color);
}
sayColor();     //red
sayColor.call(this);    //red
sayColor.call(window);  //red
sayColor.call(o);       //blue
```


-----

### 操作符之间的优先级（高到低）：
> 算术操作符 --> 比较操作符 --> 逻辑操作符 --> “=” 赋值符号



##
---

- 对 对象彻底冻结

```js {.line-numbers}
var constantize = (obj) => {
    Object.freeze(obj);
    Object.keys(obj).forEach((key, i) => {
        if(typeof obj[key] === 'object') {
            constantize(obj[key]);
        }
    });
}
```

- 变量解析赋值时， 默认值的条件是 `对象的属性值严格等于 undefined `

```javascript {.line-numbers}
let [x = 1] = [undefined];
x // 1

let [x = 1] = [null];
x // null


var {x = 3} = {x: undefined};
x // 3

var {x = 3} = {x: null};
x // null
//如果x属性等于null，就不严格相等于undefined，导致默认值不会生效。
```

- 测试 一个字符由两个字节还是由四个字节组成
```javascript {.line-numbers}
function is32Bit(c) {
    //返回true,表示为由四个字节组成的字符
  return c.codePointAt(0) > 0xFFFF;
}

is32Bit("𠮷") // true
is32Bit("a") // false
```


- 正确返回字符串长度

```javascript {.line-numbers}
function codePointLength(text) {
  var result = text.match(/[\s\S]/gu);
  return result ? result.length : 0;
}
```

- `Number.EPSILON` 用来设置“能够接受的误差范围”

    `Number.EPSILON` 的实质是一个可以接受的最小误差范围

```javascript {.line-numbers}
function withinErrorMargin (left, right) {
  return Math.abs(left - right) < Number.EPSILON * Math.pow(2, 2);
}

0.1 + 0.2 === 0.3 // false
withinErrorMargin(0.1 + 0.2, 0.3) // true

1.1 + 1.3 === 2.4 // false
withinErrorMargin(1.1 + 1.3, 2.4) // true
```