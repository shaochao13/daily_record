## JavaScript 基础知识

### Hello,World!

#### script 标签

可以使用 &lt;script&gt; 标签将 javascript 程序插入到 html 文档中的任何位置。当浏览器遇到 &lt;script&gt; 标签时，代码会自动运行。

```html
<script>
  alert('Hello, World!');
  console.log('Hello, World!');
</script>
```

#### 外部脚本

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

### 代码结构

#### 语句

语句是执行行为的语法结构和命令。
在代码中，可以编写任意数量的语句。 语句之间可以使用分号来进行分开。

```js
console.log('Hello, ');
console.log('World.');

// 尽量让每一条语句独占一行，提高代码的可读性
console.log('Hello, '); \ console.log('World.');
```

#### 分号

在大多数情况下，当存在换行符时，语句后面的分号可以省略不写，此时，javascript 引擎会将换行符理解成”分号“，称为`自动分号插入（Automatic Semicolon Insertion）`。

在大多数情况下，换行意味着一个分号，但是并不是所有情况都是这样。

```javascript
// 此时虽然进行了换行，但并不表示需要插入一个分号
console.log('hello' +
  \  ','
  \ + 'world.');
```

“自动分号插入”并不是在所有情况下都 OK。

```javascript
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

#### 注释

- 单行注释
  以两个正斜杠字符 // 开始。
- 多行注释
  以一个正斜杠和星号开始 “/\*” 并以一个星号和正斜杠结束 “\*/”。
  多行注释不支持嵌套。可以在多行注释中插入单行注释。

#### "use strict"

从`ES5`开始，增加了一些新的语言特性，并且修改了一些已经慧的特性。为了保证旧的功能能够使用，大部分的修改是默认不生效的。需要使用一个特殊的指令来激活这些新的特性：`"use strict"`。

- 在使用`"use strict"`时，必须确保它出现在文件的**最顶部**。

  ```js
  // 必须在文件的第一行，
  // 只有注释可以出现在它的前面
  'use strict';

  //其他的代码逻辑块
  ```

  ```js
  function example() {
    // 逻辑代码
  }

  ('use strict'); //此时不是在第一行，严格模式就没法启用
  ```

- 没有办法取消`"use strict"`

  一旦启用了严格模式，就没有后悔药可吃，没有办法使程序返回默认的模式。

- `"use strict"` 可以放在函数体的开头
  可以在一个函数体的开头加上`"use strict"`，此时只有这个函数启用了严格模式。但一般会让整个文件都启用严格模式。

  ```js
  function example() {
    'use strict';
    // 逻辑代码
  }
  ```

  - 在 `class`中`module`中，会自动启用`use strict`
    当代码都写在`class`和`module`中时，它们会自动启用严格模式，不需要手动添加`"use strict"`指令。

### 变量

`变量`是存储数据值的一个容器。
使用 `let` 关键字来定义一个变量。

```js
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

```js
let msg = 'abc';
// 重复对msg进行“let”，会报错
let msg = 123;
```

#### 变量命名

javascript 的变量命名的一些规则：

- 变量名称必须仅包括**字母**（允许非英文字母）、**数字**、美元符号 **$** 和下划线 **\_** 。
- **首字符**必须为**非数字**。
- 变量名**区分大小写**。
- javascript 中的**关键字**和**保留字**不能用于变量名。

如果命名时包括多个单词，通常采用**驼峰式命名法**（camelCase）。也就是除第一个单词外，其他的每个单词的首字符都**大写**。

```js
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

#### 未使用`use strict`情况下赋值

一般情况下，都是先声明、赋值，再使用。但在早期，可以简单地通过赋值创建一个变量。

```js
// 没有使用严格模式"use strict"
name = 'Tom'; // 如果变量name不存在，就会被创建
console.log(name);
```

```js
'use strict';
name = 'Tom'; // 此时会报错， num 未定义
```

有时还会看到使用`var`来命名变量的写法。但在现代的 javascript 中，已经不再推荐使用它了。

#### 常量

声明一个不变的变量，使用`const`。 使用`const`声明的变量称为“常量”，即它一旦赋值就不能被修改。并且声明和赋值须一起完成。

```js
const name = 'Tom';

name = 'Albert'; // 不能修改常量的值，会报错
```

对于在执行之前就已经已知的常量，通常会使用**大写字母**和**下划线**来进行命名。(大写命名的常量仅用作“**硬编码**（hard-coded）”值的别名)

```js
const MAIN_COLOR = '#343434';
```
