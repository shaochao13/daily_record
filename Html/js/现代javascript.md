# JavaScript 基础知识

## Hello,World!

### script 标签

可以使用 &lt;script&gt; 标签将 javascript 程序插入到 html 文档中的任何位置。当浏览器遇到 &lt;script&gt; 标签时，代码会自动运行。

```html
<script>
  alert('Hello, World!');
  console.log('Hello, World!');
</script>
```

### 外部脚本

可以 &lt;script&gt; 标签的`src`属性来添加外部的 js 文件。

```html
<!-- js文件在网站内部的绝对路径 -->
<script src="/path/to/example.js"></script>

<!-- js文件在网站内部的相对路径 -->
<script src="../example.js"></script>
<!-- 加载外部的js文件,使用外部JS文件的完整的url地址 -->
<script
  src="https://unpkg.com/react@18/umd/react.development.js"
  crossorigin></script>
```

如果&lt;script&gt;设置了`src`属性的值，则标签内的内容将会被忽略。

```html
<script src="./example.js">
  // 此处编写的任何代码将会被忽略，因为提供了 src
  console.log('Hello, World!')
</script>
```

在&lt;script&gt;标签中，不要同时有 src 属性和内部包裹的代码。

## 代码结构

### 语句

语句是执行行为的语法结构和命令。
在代码中，可以编写任意数量的语句。 语句之间可以使用分号来进行分开。

```js {.line-numbers}
console.log('Hello, ');
console.log('World.');

// 尽量让每一条语句独占一行，提高代码的可读性
console.log('Hello, '); \ console.log('World.');
```

### 分号

在大多数情况下，当存在换行符时，语句后面的分号可以省略不写，此时，javascript 引擎会将换行符理解成”分号“，称为`自动分号插入（Automatic Semicolon Insertion）`。

在大多数情况下，换行意味着一个分号，但是并不是所有情况都是这样。

```js {.line-numbers}
// 此时虽然进行了换行，但并不表示需要插入一个分号
console.log('hello' +
  \  ','
  \ + 'world.');
```

“自动分号插入”并不是在所有情况下都 OK。

```js {.line-numbers}
//此时，程序只会输出 hello, 并且会报错
console.log('hello')
\ [(1, 2)].forEach(alert)

// javascript 引擎会将上面两句语句合并到一起：
console.log('hello')[1,2].forEach(alert)
```

所以，建议在语句之间都加上分号。

在 VS Code 中可以通过 setting.json 来设置自动添加分号：

- "javascript.format.semicolons"
  此属性有 3 个值(ignore, remove, insert)，默认为"ignore",
- "prettier.semi"
  此属性值为 true 时，安装了 prettier 时就会自动添加分号。

### 注释

- 单行注释
  以两个正斜杠字符 // 开始。
- 多行注释
  以一个正斜杠和星号开始 “/\*” 并以一个星号和正斜杠结束 “\*/”。
  多行注释不支持嵌套。可以在多行注释中插入单行注释。

### "use strict"

从`ES5`开始，增加了一些新的语言特性，并且修改了一些已经慧的特性。为了保证旧的功能能够使用，大部分的修改是默认不生效的。需要使用一个特殊的指令来激活这些新的特性：`"use strict"`。

- 在使用`"use strict"`时，必须确保它出现在文件的**最顶部**。

  ```js {.line-numbers}
  // 必须在文件的第一行，
  // 只有注释可以出现在它的前面
  'use strict';

  //其他的代码逻辑块
  ```

  ```js {.line-numbers}
  function example() {
    // 逻辑代码
  }

  ('use strict'); //此时不是在第一行，严格模式就没法启用
  ```

- 没有办法取消`"use strict"`

  一旦启用了严格模式，就没有后悔药可吃，没有办法使程序返回默认的模式。

- `"use strict"` 可以放在函数体的开头
  可以在一个函数体的开头加上`"use strict"`，此时只有这个函数启用了严格模式。但一般会让整个文件都启用严格模式。

  ```js {.line-numbers}
  function example() {
    'use strict';
    // 逻辑代码
  }
  ```

  - 在 `class`中`module`中，会自动启用`use strict`
    当代码都写在`class`和`module`中时，它们会自动启用严格模式，不需要手动添加`"use strict"`指令。

## 变量

`变量`是存储数据值的一个容器。
使用 `let` 关键字来定义一个变量。

```js {.line-numbers}
// 1. 声明（定义）一个变量msg
let msg;
// 2. 给变量msg赋值
msg = 'msg';

// 声明变量，并对其进行赋值
let msg2 = 'msg2';

// 也可以同时进行多个变量的声明和赋值
let name = 'Tom',
  age = 18,
  gender = 'F';
```

变量 msg 可以想象成一个标有“msg”标签的盒子，盒子里可以放入任何值，并且可以任意修改。

**一个变量只能被声明一次**，如果对一个变量进行重复声明，就会触发 `SyntaxError`。

```js {.line-numbers}
let msg = 'abc';
// 重复对msg进行“let”，会报错
let msg = 123;
```

### 变量命名

javascript 的变量命名的一些规则：

- 变量名称必须仅包括**字母**（允许非英文字母）、**数字**、美元符号 **$** 和下划线 **\_** 。
- **首字符**必须为**非数字**。
- 变量名**区分大小写**。
- javascript 中的**关键字**和**保留字**不能用于变量名。

如果命名时包括多个单词，通常采用**驼峰式命名法**（camelCase）。也就是除第一个单词外，其他的每个单词的首字符都**大写**。

```js {.line-numbers}
let myName;
let user123;
let $; // 使用 "$" 声明一个变量
let _; // 使用 "_" 声明一个变量
let myFullName; // 驼峰式命名

let 地球='earth';// 这样也是正确的，只是不建议使用


let 1abc; // 不能以数字开头
let first-name; // “-”不能用于变量名称中

let let = 'let是一个关键字'; // 不能用 "let" 来命名一个变量！
```

### 未使用`use strict`情况下赋值

一般情况下，都是先声明、赋值，再使用。但在早期，可以简单地通过赋值创建一个变量。

```js {.line-numbers}
// 没有使用严格模式"use strict"
name = 'Tom'; // 如果变量name不存在，就会被创建
console.log(name);
```

```js {.line-numbers}
'use strict';
name = 'Tom'; // 此时会报错， num 未定义
```

有时还会看到使用`var`来命名变量的写法。但在现代的 javascript 中，已经不再推荐使用它了。

### 常量

声明一个不变的变量，使用`const`。 使用`const`声明的变量称为“常量”，即它一旦赋值就不能被修改。并且声明和赋值须一起完成。

```js {.line-numbers}
const name = 'Tom';

name = 'Albert'; // 不能修改常量的值，会报错
```

对于在执行之前就已经已知的常量，通常会使用**大写字母**和**下划线**来进行命名。(大写命名的常量仅用作“**硬编码**（hard-coded）”值的别名)

```js {.line-numbers}
const MAIN_COLOR = '#343434';
```

## alert、prompt 和 confirm

alert、prompt 和 confirm 为与用户交互的 3 个浏览器的特定函数。它们弹出的窗口称为“**模态窗(modal)**”， 它们会暂停脚本的执行,并且用户不能与页面的其他部分进行交互，直到模态窗口关闭。

它们弹出的模态窗口：

- 模态窗口的确切位置由浏览器决定。通常在页面中心。
- 窗口的确切外观也取决于浏览器。我们不能修改它。

### alert

用来弹出一些提示信息。

```js {.line-numbers}
alert('Hello, World.');
```

### prompt

`prompt` 浏览器会显示一个带有文本消息的模态窗口，还有 `input` 框和确定/取消按钮。

```js {.line-numbers}
let result = prompt(title, [default]);
```

接收两个参数：

- `title`
  显示给用户的文本字符串
- `default`
  可选的第二个参数，指定 input 框的初始值。

```js {.line-numbers}
let result = prompt('abc', 123);

console.log(typeof result);
console.log(result === null);

// 按取消键： result 为 object 类型，值为 null
// 按确定键： result 为 string 类型，值为 输入的值或者初始值
```

在 IE 浏览器中，如果未提供第二个参数，它会默认将“undefined”插入到 prompt，所以最好每次都为 prompt 函数提供第二个参数。

### confirm

`confirm` 弹出显示信息等待用户点击确定或取消。点击确定返回 `true` ，点击取消或按下 Esc 键返回 `false` 。

```js {.line-numbers}
let result = confirm('Are you ok?');
```

## 数据类型

javascript 被称为“动态类型”（dynamically typed）的编程语言，意思是虽然语言中有不同的数据类型，但定义好的变量并不会在定义后，被限制为某一数据类型，会随时所赋值的数据类型而发生变化。

javascript 中的值都是具有特定类型的。

在 javascript 中有 8 种基本的数据类型（**7** 种原始类型和 **1** 种引用类型）。

### Number 类型

`number`类型代表**整数**和**浮点数**。

```js {.line-numbers}
let num = 100;
num = 1.2345;
```

除了常规的数字外，还包括几个“**特殊数值**”：`Infinity`、`-Infinity`和`NaN`。

- `Infinity` 表示**无穷大(正无穷) ∞**，`-Infinity`表示**无穷小(负无穷)-∞**。

  ```js {.line-numbers}
  let n = 10 / 0; // 通过除以 0 ，可以得到 Infinity
  let n2 = Infinity; // 可以直接使用Infinity来进行赋值

  let n3 = -10 / 0; // 会得到-Infinity
  ```

- `NaN` 表示**计算错误**。 它是一个不正确或者一个未定义的数学操作所得到的结果。

  ```js {.line-numbers}
  let n3 = 'Tom' / 2;
  console.log(n3); // NaN
  console.log(NaN + 10); // NaN
  console.log(NaN * 10); // NaN
  ```

任何对 **NaN** 的数学运算都会返回 `NaN`，只有一个例外：**NaN \*\* 0 = 1**。

在 `javascript` 中做数学运算是安全的。脚本永远不会因为一个致命的数学运算而停止，最坏的情况，会得到 `NaN` 的结果。

### BigInt 类型

在 javascript 中，Number 类型无法安全表示大于 `2**53-1`(即 9007199254740991)，或小于`-(2**53-1)`的整数。

```js {.line-numbers}
// 所有大于2**53-1或者小于-(大于2**53-1)的奇数都不能用Number类型来存储和正常表示
console.log(9007199254740991 + 1);
console.log(9007199254740991 + 2); // 9007199254740992
console.log(9007199254740991 + 3);
console.log(9007199254740991 + 4); // 9007199254740996
console.log(9007199254740995); // 9007199254740996
console.log(9007199254740991 + 5);
console.log(-9007199254740995); // -9007199254740996
console.log(-9007199254740996);
```

在大多数情况下，使用 Number 类型是足够了，但在一些特殊的时候可能需要范围非常大的整数，比如用于密码学或者微秒精度的时间。
`BigInt`类型是新添加到 javascript 中的，用于表示任意长度的整数。通过在整数末尾添加 **n** 来表示 BigInt 值。

```js {.line-numbers}
// 尾部添加 "n" 表示这是一个 BigInt 类型
// 目前 Firefox/Chrome/Edge/Safari 已经支持 BigInt 了，但 IE 还没有。
const bigN = 90071992547409919007199254740991n;
```

### String 类型

在 javascript 中，有 3 种表示字符串的方式：

- 双引号： "Hello,World"。
- 单引号： 'Hello,World'。
- 反引号： \`Hello,World\`。

双引号和单引号没有什么区别。 `反引号`是 **功能扩展** 引号，通过它可以将变量或者表达式包装在`${...}`中，嵌入到字符串，方便字符串的操作。

```js {.line-numbers}
let firstName = 'Tom';
let lastName = 'Wu';
let fullName = `${firstName} ${lastName}`; // fullName = ："Tom Wu"

console.log(`1 + 2 = ${1 + 2}`); //输出：1 + 2 = 3
```

在 javascript 中没有 character 类型，一个字符串可以包含零个（为空）、一个或者多个字符。

### Boolean 类型

boolean 类型仅包含两个值： `true` 和 `false` 。

### Null 值

javascript 中的 `null` ，仅仅表示 “**无**” 、 “**空**” 或者 “**值未知**” 的特殊值，它不是一个“对不存在的 object 的引用” 或者 ”null 指针”。

```js {.line-numbers}
let name = null; // 表示name是未知的
```

### Undefined 值

`undefined` 表示 “**未被赋值**”。
如果一个变量已经被声明，但未被赋值，那么它的值就是 `undefined` 。

```js {.line-numbers}
let name;
console.log(name); // undefined
```

### Symbol 类型

symbol 类型用于创建对象的唯一标识符。

### Object 类型

`object` 类型用于储存数据集合和更为复杂的数据实体。
通过带有可选 **属性列表** 的 **花括号{...}** 来创建对象。 一个属性就是一个键值对（key:value），其中键 key 是一个字符串（属性名），值 value 可以是任何值。

创建一个空的对象：

```js
let o = new Object(); // "构造函数" 的语法
let o2 = {}; // "字面量" 的语法 （通常使用字面量语法）
```

### typeof 运算符

typeof 运算符 返回参数的类型。 typeof 是一个操作符，不是一个函数。

| typeof 的代码写法 | 返回结果  |
| :---------------- | :-------- |
| typeof 数字       | number    |
| typeof 字符串     | string    |
| typeof 布尔型     | boolean   |
| typeof 对象       | object    |
| typeof 方法       | function  |
| typeof null       | object    |
| typeof undefined  | undefined |
| typeof []         | object    |
| typeof {}         | object    |

```js {.line-numbers}
typeof undefined; // "undefined"
typeof NaN; // "number"   NaN 是一个特殊的数字
typeof null; // "object"  官方承认的 typeof 的错误，这个问题来自于 JavaScript 语言的早期阶段，并为了兼容性而保留了下来。null 绝对不是一个 object。null 有自己的类型，它是一个特殊值。typeof 的行为在这里是错误的。
typeof 100; // "number"
typeof 100n; // "bigint"
typeof false; // "boolean"
typeof 'Tom'; // "string"
typeof Symbol('example'); // "symbol"
typeof Math; // "object"  Math 是一个提供数学运算的内建 object
typeof console.log; // "function"
```

### 类型转换

在大多数情况下，运算符和函数会自动将赋予给它们的值转换为正确的类型。

#### 字符串转换

可以调用`String(value)`来将`value`转换为字符串类型

```js {.line-numbers}
let v = true;
let vStr = String(v); // "true"

v = null;
vStr = String(v); // "null"
```

#### 数字型转换

可以调用`Number(value)`来将`value`转换为 number 类型

```js {.line-numbers}
let str = '   100   ';
let n = Number(str); // 100

str = '';
n = Number(str); // 0

str = undefined;
n = Number(str); // NaN

str = null;
n = Number(str); // 0

str = true;
n = Number(str); // 1

str = '100abcd';
n = Number(str); // NaN
```

**Number()** 类型转换规则：

| 值            | 转换之后的结果                                                                                                                                                                           |
| :------------ | :--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| undefined     | NaN                                                                                                                                                                                      |
| null          | 0                                                                                                                                                                                        |
| true 和 false | 1 和 0                                                                                                                                                                                   |
| string        | 去掉首尾空白字符（空格、换行符 \n、制表符 \t 等）后的纯数字字符串中含有的数字。如果剩余字符串为空，则转换结果为 0。否则，将会从剩余字符串中“读取”数字。当类型转换出现 error 时返回 NaN。 |

#### 布尔型转换

可以调用`Boolean(value)`来将`value`转换为 boolean 类型

转换规则：

- 直观上为“空”的值（0、空字符串、null、undefined、NaN）将变为`false`
- 其他值变成`true`

```js {.line-numbers}
console.log(Boolean(1)); // true
console.log(Boolean(0)); // false
console.log(Boolean('Tom')); // true

console.log(Boolean('')); // false
console.log(Boolean(' ')); // true

console.log(Boolean('0')); // true
```

## 基础运算符，数学运算

### 术语

- 运算元
  `运算远`是运算符应用的对象。比如除法运算 `12 / 4` ，有两个运算元：左运算元 `12` 和右运算元 `4` 。
- 一元运算符
  如果一个运算符只对应一个运算元，则称它为一元运算符，如：`-2`中的一元负号运算符。
- 二元运算符
  如果一个运算符对应两个运算元，则称它为二元运算符
  ```js {.line-numbers}
  let x = 10;
  let y = 20;
  console.log(x + y);
  ```

### 数学运算

javascript 支持的数学运算：`加法+`、`减法-`、`乘法\*`、`除法/`、`取余%`、`求幂\*\*`。

```js {.line-numbers}
let n = 9 ** (1 / 2); // 3 ｜ 9的平方根
```

### 用二元运算符 "+" 连接字符串

用二元运算符 "+" 连接字符串时的执行顺序：首先按照各运算符的优先级进行各自的运算，然后再按照数学运算`从左至右`进行计算，在逐个运算过程中，一旦有一个运算元是字符串类型的，则进行字符串的拼接，得到一个字符串类型的“数字”，如果后面还有“+”，则进行拼接，如果是其他的运算符，则会将字符串型的“数字”转换成 数字之后参与运算。

```js {.line-numbers}
console.log('1' + 2); // 12
console.log(1 + '2'); // 12
console.log(1 + 2 + '3'); // 33 不是 123
console.log('1' + 2 + 3); // 123 不是 15
console.log('1' + 2 + 3 * 4); // 1212
console.log('1' + 2 + 3 * 4 - 2); // 1210
console.log('1' + 2 + 3 * 4 - '2'); // 1210
```

**只有二元运算符“+”支持字符串的拼接，其他算术运算符只对数字起作用，并且总是将其运算元转换为数字。**

### 数字转化，一元运算符“+”

在一个字符串前加上一个“+”，它会执行 Number(value)相同字符串转数字的规则。

```js {.line-numbers}
console.log(+''); // 0
console.log(+'tom'); // NaN
console.log(+'123z'); // NaN
console.log(+null); // 0
console.log(+undefined); // NaN
console.log(+true); // 1
console.log(+'2' + +'3'); // 5
```

### 运算符的优先级

**圆括号**拥有最高优先级。
如果优先级相同，则按照由左至右的顺序执行。
[具体的优先级>>](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Operators/Operator_Precedence)

### 自增/自减

- `自增/自减` 可以置于变量前，也可以置于变量后

  ```js {.line-numbers}
  let counter = 1;
  counter++;
  --counter;
  ```

  置于变量前，先执行变量值的自增或自减运算，再返回新值。
  置于变量后，是先返回原值，再执行变量值的自增或自减运算。

  ```js {.line-numbers}
  let counter = 100;
  let result = counter--;
  console.log(result); // 100
  console.log(counter); // 99

  let counter2 = 100;
  let result2 = ++counter2;
  console.log(result2); // 101
  console.log(counter2); // 101
  ```

- `自增/自减` 只能应用于**变量**
  ```js {.line-numbers}
  100++; // 作用于数值上，会报错
  ```

### 位运算符

位运算符把运算元当做 32 位整数，并在它们的二进制值上进行操作。

javascript 支持的位运算符：`按位与(&)`、`按位或(|)`、`按位异或(^)`、`按位非(~)`、`左移(<<)`、`右移(>>)`、`无符号右移(>>>)`。

### 逗号运算符

逗号运算符能将多个语句用`,`分开，每个语句都会执行，但是只有最后的语句的结果会被返回。

```js {.line-numbers}
let num = (10 + 20, 30 + 40); // num = 70
```

逗号运算符的优先级非常低，比赋值运算符 = 还要低。

## 值的比较

### 字符串比较

当两个值都为字符串时，是按字符（母）逐个进行比较。

```js {.line-numbers}
console.log('B' > 'A'); // true
console.log('Black' > 'Blue'); // false
console.log('Back' > 'Ba'); // true
```

### 不同类型间的比较

当不同类型的值进行比较时，javascript 首先会将其转化为 **数字(Number)** ，再进行比较大小。

```js {.line-numbers}
console.log('1' > 1); // false
console.log('01' == 1); // true
```

对于布尔类型值: `true` 会被转化为 `1`、`false` 转化为 `0`。

### 严格相等 ===

严格相等运算符 `===` 在进行比较时，不会做任何的类型转换。
相等运算符`==` 在进行比较时，如果是不同类型的数据，首先会其进行类型转换。

```js {.line-numbers}
console.log(false === 0); //  false
console.log(false == 0); //  true
```

### null 和 undefined

```js {.line-numbers}
// 当使用非严格相等 == 比较二者时
console.log(null == undefined); //true

// 当使用严格相等 === 比较二者时
console.log(null === undefined); // false
```

- 在进行相等性检查`==`时，`null`和`undefined`不会进行任何的类型转换。
- 在进行普通的比较运算`>`、`<`、`>=`、`<=`检查时，`null`会转化为 `0` ， `undefined` 会转换为 `NaN`。
- 在进行相等性检查`==`时，`undefined` 只与 `null` 相等，不与其他任何值相等。

```js {.line-numbers}
console.log(null == 0); //  false
console.log(null >= 0); //  true

console.log(undefined == 0); // false
console.log(undefined >= 0); // false  此时undefined会转换为NaN
```

## 逻辑运算符

javascript 中有四个逻辑运算符：`||(或)`、`&&(与)`、`!(非)`、`??(空值合并运算符)`

在传统的编程中，逻辑运算符仅能操作布尔值， 并且返回的结果也是布尔值。
但在 javascript 中，逻辑运算符可以操作任意类型。如果操作也是布尔值，那么与传统的编程中一样，如果操作的不是布尔值，则返回的就是按各个逻辑运算符的规则进行返回相应的初始值。

```js {.line-numbers}
// 操作的参数都是布尔值时，与其他编程语言中一样的逻辑
console.log(true || false); // true
console.log(false && false); // false
console.log(!false); // true
```

### 逻辑或 `||`

`逻辑或||`它的任务就是**寻找第一个真值**。
简单来说：**一个或运算 `||` 的链，将返回第一个"真值"，如果不存在"真值"，就返回该链的最后一个值**。

```js {.line-numbers}
let result = value1 || value2 || value3;
```

- 从左至右依次计算各个参数。
- 处理每一个操作数时，都将其转化为布尔值，如果结果是 `true` ，就停止计算，并返回这个操作数的初始值。
- 如果所有的操作数都被计算了，则返回最后一个操作数的初始值。
- 返回的值是操作数的初始形式，不会做布尔转换。

```js {.line-numbers}
console.log(0 || 1); // 1
console.log(null || 10); // 10
console.log(0 || null || undefined); // undefined 返回最后一个数
console.log(null || 'tom'); // tom

true || console.log('为false时才会执行console.log函数');
```

### 逻辑与 `&&`

`逻辑与&&`它的任务就是**寻找第一个假值**。
简单来说：**一个与运算 `&&` 的链，将返回第一个"假值"，如果不存在"假值"，就返回该链的最后一个值**。

```js {.line-numbers}
let result = value1 || value2 || value3;
```

- 从左至右依次计算各个操作数。
- 处理每一个操作数时，都将其转化为布尔值，如果结果是 `false` ，就停止计算，并返回这个操作数的初始值。
- 如果所有的操作数都被计算了，则返回最后一个操作数的初始值。
- 返回的值是操作数的初始形式，不会做布尔转换。

```js {.line-numbers}
console.log(0 && 1); // 0
console.log(null && 10); // null
console.log(0 && null && undefined); // 0
console.log(null && 'tom'); // null
console.log(1 && 'tom' && undefined); // undefined 返回最后一个数

true && console.log('为 true 时才会执行console.log函数');
```

**`与运算&&` 的优先级比`或运算||` 要高**:

```js {.line-numbers}
// 建议加上圆括号
console.log((10 && 50) || (null && 20)); // 50
console.log((null && 20) || (10 && 50)); // 50
```

### 逻辑非`!`

逻辑非`!` 运算符接受一个参数，并将操作数转化布尔类型（true/false），然后返回相反的值。

```js {.line-numbers}
console.log(!false); // true
console.log(!0); // true
console.log(!null); // true
console.log(!undefined); // true
```

使用两个非运算`!!`，可以将值转为其对应的布尔类型，与 Boolean(value) 一样的效果：

```js {.line-numbers}
console.log(!!'Tom'); // true
console.log(!!null); // false
console.log(!!undefined); // false
console.log(!!NaN); // false
```

非运算符`!` 的优先级在所有逻辑运算符里面`最高`，总是在 `&&` 和 `||` 之前执行。

### 空值合并运算符`??`

空值合并运算符`??` 是新添加到 javascript 中的特性，如果旧老浏览器中使用它，可能需要 `polyfills`。

```js {.line-numbers}
let result = value1 ?? value2;

// 与上面同逻辑
let result = value1 !== null && value1 !== undefined ? value1 : value2;
```

如果 `value1` 不是 `null` 和 `undefined` ，则返回 `value1`, 否则就返回 `value2` 。

`??` 常见的使用场景是用来提供`默认值`。

```js {.line-numbers}
let name;
// let name = 'John';
console.log(name ?? 'Tom');
```

`??`与`||`的区别：

- `||` 无法区分 `false`、`0`、空字符串"" 和 `null` / `undefined`, 它们都一样为“假值”。
- `??` 只针对 `null` / `undefined`。
- 使用`??`时，如果没有明确添加括号，不能将其与 `||` 或 `&&` 一起使用。

## 条件分支：if 和 "?"

`?`它被称为“三元运算符”。

```js {.line-numbers}
let result = condition ? value1 : value2;
// 计算条件结果，如果结果为真，则返回 value1，否则返回 value2。
```

```js {.line-numbers}
let age = prompt('请问你多大了？', '');
if (age >= 18) {
  alert('恭喜你，已成年');
} else {
  alert('对不起，你还未成年，不能进入。');
}

// 使用 ？重写
let result = age > 18 ? '恭喜你，已成年' : '对不起，你还未成年，不能进入。';
```

```js {.line-numbers}
let age = prompt('请问你多大了？', '');
if (age < 3) {
  alert('你还是一个小baby呢');
} else if (age < 18) {
  alert('你还是一个青少年呢');
} else if (age < 70) {
  alert('你还很年轻呢');
} else {
  alert('老头，一起打牌不');
}

// 使用 ？重写
let result =
  age < 3
    ? '你还是一个小baby呢'
    : age < 18
    ? '你还是一个青少年呢'
    : age < 70
    ? '你还很年轻呢'
    : '老头，一起打牌不';
```

## 循环： while 和 for

### while

语法：

```js {.line-numbers}
// 当 condition 为真时， 执行循环体的代码
while (condition) {
  //循环体
}
```

```js {.line-numbers}
let n = 1;
while (n < 10) {
  console.log(n);
  n++; // 需要能改变循环条件的语句
}
```

### do...while

`do...while`循环语句的循环体至少会执行一次。

语法：

```js {.line-numbers}
do {
  //循环体
} while (condition);
// 当condition为真时，重复执行循环体中的代码
```

```js {.line-numbers}
let n = 1;
do {
  console.log(n);
  n++; // 需要能改变循环条件的语句
} while (n < 10);
```

### for

语法：

```js {.line-numbers}
for (begin; condition; step) {
  // 循环体
}
// begin，condition，step可以进行省略

for (;;) {
  // 无限循环模式
  // 两个 ; 必须存在，否则会出现语法错误。
}
```

```js {.line-numbers}
for (let i = 0; i < 10; i++) {
  console.log(i);
}
```

### 跳出循环 break

`break` 用于终止当前循环。

```js {.line-numbers}
for (let i = 0; i < 10; i++) {
  if (i % 2 == 0) {
    break;
  }
  console.log(i);
}
```

### 继续下一次迭代 continue

`continue` 用于停止当前这一次的迭代，强制启动新一轮的循环迭代。

```js {.line-numbers}
for (let i = 0; i < 10; i++) {
  if (i % 2 == 0) {
    continue;
  }
  console.log(i);
}
```

### 标签 label

使用标签，可以让代码跳转至标签处执行

```js {.line-numbers}
for (let i = 0; i < 3; i++) {
  for (let j = 0; j < 3; j++) {
    console.log(`i:${i},j:${j}`);
    if (j == 1) break; // 此时只会跳出结束内层的for循环，外层的for循环还会继续进行迭代
  }

  console.log(`i:${i}`);
}

outer: for (let i = 0; i < 3; i++) {
  for (let j = 0; j < 3; j++) {
    console.log(`i:${i},j:${j}`);
    if (j == 1) break outer; // 此处通过指定跳转至标签处，则会跳至外层循环，结束两个for循环
  }

  console.log(`i:${i}`);
}
```

## switch 语句

`switch`语句 可以代替多个`if`判断。

语法：
switch 语句至少有一个 `case` 代码块和一个可选的 `default` 代码块。

```js {.line-numbers}
switch (v) {
  case value1: // 表示 if (v === value1)
    // 逻辑代码
    break;
  case value2:
    // 逻辑代码
    break;
  //...
  case valueN:
    // 逻辑代码
    break;
  default:
    // 逻辑代码
    break;
}
```

- `switch` 语句进行的是 `严格相等` 比较，不会进行类型转换，被比较的值必须是相同的类型才能进行匹配。

  ```js {.line-numbers}
  let n = 10;
  switch (n) {
    case 10:
      console.log(n);
      break;
    case '10': // 因为类型不对，所以永远都不会执行到此处的case中去
      console.log(n);
      break;
    default:
      break;
  }
  ```

- 每个 case 和 default 代码块中，最后都有一个 break 语句。如果没有 break 话，就会执行完一个 case 代码块后，接着进入下一个 case 代码块的执行。
- 如果想让几个 case 执行同样的代码逻辑，就可以对它们进行“分组”
  ```js {.line-numbers}
  let n = 10;
  switch (n) {
    case 5:
    case 10:
    case 15:
      console.log(n);
      break;
    case 20:
      console.log(20);
      break;
    default:
      console.log(n);
      break;
  }
  ```

## 函数 Function

函数是程序的主要“构建模块”，函数可以使一段代码重复执行，避免代码重复。

### 函数声明

函数以 function 关键字开头，然后是函数的名称，然后是括号之间的“参数”，各个“参数”之间使用逗号分隔。

```js {.line-numbers}
function funcName(parameter1, parameter2,..., parameterN) {
  // 函数体
}
```

### 局部变量

在函数中声明的变量只在该函数体内为可见，也称为局部变量。

```js {.line-numbers}
function showMsg() {
  let msg = 'Hello, World.'; // 局部变量
  console.log(msg);
}

showMsg(); // 执行函数， 输出： Hello, World.

console.log(msg); // 错误！ msg 是 showMsg中的局部变量，外部不能访问
```

### 外部变量（全局变量）

函数对外部变量拥有全部的访问权限。可以对外部变量进行修改。

```js {.line-numbers}
let msg = 'Hello, World.';
function showMsg() {
  msg = 'Hello, javascript';
  console.log(msg);
}

// 函数执行之前
console.log(msg); // Hello, World.
// 执行函数
showMsg(); // Hello, javascript
// 外部变量msg的值被函数修改
console.log(msg); // Hello, javascript
```

函数只有在没有与外部变量同名的局部变量时，才会使用外部变量。如果存在同名的局部变量，则会忽略掉外部变量。

```js {.line-numbers}
let msg = 'Hello, World.';

function showMsg() {
  let msg = 'Hello, javascript';
  console.log(msg);
}

// 函数执行之前
console.log(msg); // Hello, World.
// 执行函数
showMsg(); // Hello, javascript
// 外部变量未被修改
console.log(msg); // Hello, World.
```

### 参数

可以通过参数的形式，将任意数据传递给函数。

```js {.line-numbers}
let firstName = 'John';
let lastName = 'Li';

function getFullName(firstName, lastName) {
  // 此处的firstName,lastName为函数参数中的变量，它们的值为通过执行函数传入的变量的一个局部副本，
  // 它们在函数内部的改变，不会影响到外部变量的值
  // 对于引用类型的数据，有时会改变外部变量的值
  let fullName = `${firstName} ${lastName}`;
  return fullName;
}

let fullName = getFullName(firstName, lastName);
```

两个参数要搞清楚：

- 参数（**parameter**），是函数声明中括号内列出的变量，它是函数声明时的术语
- 参数（**argument**），是函数调用时传递给函数的值，它是函数调用时的术语。

### 默认值

在调用函数时，如果有参数 argument 未被提供，那么相应的值就会变成 `undefined` 。
可以通过在函数声明时，使用 `=` 为参数指定一个“默认”值。

```js {.line-numbers}
// 如果未传递msg的值，则会使用默认的“Javascript”
function showMsg(msg = 'Javascript') {
  console.log(`Hi, ${msg} !`);
}

showMsg('Python'); // Hi, Python !
showMsg(); // Hi, Javascript !
```

默认值可以是更为复杂的表达式，并且只有在当缺少参数时，表达式才会被计算和使用。

```js {.line-numbers}
function showMsg(msg = anotherFun()) {
  //函数体
}
// 此处的anotherFun()只有在执行 showMsg()函数时，msg参数缺少的情况下被执行
```

检查参数是否传递了值:

```js {.line-numbers}
function showMsg(msg) {
  if (msg === undefined) {
    // msg 未传递
  }
  // ...
}

function showMsg(msg) {
  msg = msg || 'no msg given';
  // ...
}
// 使用||时，下面函数调用需要注意！！！！！！
showMsg(0); // no msg given
showMsg(null); // no msg given
showMsg(NaN); // no msg given

function showMsg(msg) {
  // 使用 ?? 更能表示参数是否传递了
  msg = msg ?? 'no msg given';
  // ...
}
```

### 返回值

函数可以将一个值返回到调用它的代码处。

```js {.line-numbers}
function sum(a, b) {
  return a + b;
}

let result = sum('1', '2'); // 12
console.log(result);

result = sum(1, 2); // 3
console.log(result);
```

如果函数体中没有 return 或者 return 后未跟任何返回值，此时函数的返回值为 **undefined** 。

```js {.line-numbers}
function doSomething() {
  // 函数体中没有 return
}

console.log(doSomething() === undefined); // true

function doSomething2() {
  // 函数体中的 return 后没有带任何值
  return;
}
console.log(doSomething2() === undefined); // true
```

### 函数的命名

函数其实就是执行一些行为。所以一种普遍的做法就是用`动词前缀`来开始一个函数，如：

- "get…" —— 返回一个值 , getFullName(...)
- "calc…" —— 计算某些内容 , calcSum(...)
- "create…" —— 创建某些内容, createForm(...)
- "check…" —— 检查某些内容并返回 boolean 值, checkPermission(...)

### 函数表达式

另一种创建函数的语法称为 **函数表达式**

```js {.line-numbers}
//注意： function 关键字后面没有函数名
let showMsg = function () {
  console.log('Hello, javascript');
};

showMsg();
```

在 javascript 中，函数是一个**值**

```js {.line-numbers}
// 创建
function showMsg() {
  console.log('Say, Hello.');
}

let func = showMsg; // 将showMsg赋值给 func变量

func();
showMsg();
```

- 函数表达式是在代码执行到达时才被创建，并且仅从那一刻起才可用。
- 严格模式下，当一个函数声明在一个代码块内时，它在该代码块内的任何位置都是可见的。但在代码块外不可见。

### 回调函数

可以将函数作为值来传递

```js {.line-numbers}
function isPermission(isPermission, yes, no) {
  if (isPermission) {
    yes();
  } else {
    no();
  }
}

isPermission(
  true,
  // 匿名函数
  function () {
    console.log('我已经有权限了');
  },
  function () {
    console.log('对不起，我的权限暂时不够');
  }
);
```

### 箭头函数 =>

```js {.line-numbers}
// 创建了一个箭头函数 func，它接受参数 arg1..argN个参数，然后使用参数对右侧的 expression 求值并返回其结果。
let func = (arg1, arg2, ..., argN) => expression;

// 与上面等同
let func = function (arg1, arg2, ..., argN){
  return expression;
}
```

- 如果只有一个参数，可以省略掉参数外的圆括号

```js {.line-numbers}
let getDouble = (n) => n * 2;

getDouble(10); // 20
```

- 如果没有参数，圆括号必须保留

```js {.line-numbers}
let showMsg = () => console.log('Hello,javascript');

showMsg();
```

- 如果箭头函数的函数体，不止一行语句时，需要把函数体放在花括号中

```js {.line-numbers}
let sum = (a, b) => {
  let result = a + b;
  return result;
};

sum(10, 20); // 30
```
