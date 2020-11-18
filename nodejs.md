## 模块

在Nodejs中，每一个文件就是一个模块，而文件路径就是模块名。

### 模块初始化

一个模块中的js代码仅在模块第一次被使用时执行一次，并在执行过程中初始化模块的导出对象。之后，缓存起来的导出对象被重复利用。

### `require`

`require` 函数用于在当前模块中加载和使用别的模块，传入一个模块名，返回一个模块导出对象。

也可以使用它加载和使用json文件。

```javascript
var data = require('./data.json')
```

### `exports`

`exports` 对象是当前模块的导出对象，用于导出模块公有方法和属性。别的模块通过`require`函数使用当前模块时，得到的就是当前模块的`exports`对象。

### `module`

通过`module`对象可以访问到当前模块的一些相关信息，但最多的用途是替换当前模块的导出对象。 模块导出对象默认是一个普通对象，如果想改成一个函数的话，可以使用如下方式：

```javascript
module.exports = function() {
  console.log('Hello')
}
```



### `模块路径解析规则`

依次按照以下规则解析路径：

1. 内置模块

   如果传递给`require`函数的是Nodejs内置模块名称，不做路径解析，直接返回内部模块的导出对象。如`require('fs')`。

2. `node_modules`目录

   如，某个模块的绝对路径是`/home/user/hello.js` ，在这个js文件中使用`require('foo/bar')`方式加载模块时，则nodejs依次尝试使用以下路径：

   ```javascript
   /home/user/node_modules/foo/bar
   /home/node_modules/foo/bar
   /node_modules/foo/bar
   ```

3. `NODE_PATH`环境变量

   与`PATH`环境变量类似。



## 包(package)

把由多个子模块组成的大模块称做`包`，并把所有子模块放在同一个目录里。

1. `index.js`

当模块的文件名是`index.js`，加载模块时可以使用模块所在`目录的路径`代替`模块文件路径`。 

2. `package.json`

   如果想自定义入口 模块的文件名和存储位置，就需要在包目录下包含一个`package.json`文件，并在其中指定入口模块的路径。如：

   ```json
   {
     "name": "cat",
     "main": "./lib/main.js"
   }
   ```

   

## 文件操作

### 小文件拷贝

```javascript
var fs = require('fs')

function copy(src, dst) {
    fs.writeFileSync(dst, fs.readFileSync(src))
}

```

### 大文件拷贝

```javascript
var fs = require('fs')

function copy(src, dst){
  fs.createReadStream(src).pipe(fs.createWriteStream(dst))
}
```

### `Buffer`数据块

`Buffer` 用来提供对二进制数据的操作。

`Buffer`与字符串的一个重要区别：字符串是只读的，并字符串的任何修改得到的都是一个新字符串。`Buffer` 更像是可以做指针操作的C语言数组。可以用`[index]`方式直接修改某个位置的字节。

```javascript
var bin = new Buffer([0x68, 0x65, 0x6c, 0x6c, 0x6f])
//字符串转换为指定编码下的二进制数据
var bin = new Buffer('hello', 'utf-8')

//将二进制数据转化为指定编码的字符串
var str = bin.toString('utf-8')
//修改指定index位置的字节
bin[0] = 0x48
```

使用`.slice` 方法也不是返回一个新的Buffer,而是返回了指向原Buffer中间的某个位置的指针。因此对 `.slice`方法返回的`Buffer`的修改也会作用于原`Buffer`.

```javascript
var bin = new Buffer([ 0x68, 0x65, 0x6c, 0x6c, 0x6f ]);
var sub = bin.slice(2);

sub[0] = 0x65;
console.log(bin); // => <Buffer 68 65 65 6c 6f>
```

如果想要拷贝一份`Buffer`，得首先创建一个新的`Buffer`，并通过`.copy`方法把原`Buffer`中的数据复制过去。

```javascript
var bin = new Buffer([ 0x68, 0x65, 0x6c, 0x6c, 0x6f ]);
var dup = new Buffer(bin.length);

bin.copy(dup);//copy
dup[0] = 0x48;
console.log(bin); // => <Buffer 68 65 6c 6c 6f>
console.log(dup); // => <Buffer 48 65 65 6c 6f>
```



## `Stream` 数据流

`Stream` 基于事件机制工作，所有`Stream`的实例都继承于nodejs提供的 `EventEmitter`。

```javascript
var fs = require('fs')

function only_read_file_stream(src, dst) {
    var rs = fs.createReadStream(src)
    var ws = fs.createWriteStream(dst)

    rs.on('data', function (chunk) {
        //表示还在写中，暂停新数据中的读取，以防止缓存爆仓
        if (ws.write(chunk) === false) {
            rs.pause()
        }
    })
    //表示数据读取完成，同时也结束数据的写入
    rs.on('end', function () {
        ws.end()
    })

    //表示已经写入到了dst中，可以继续读取数据
    ws.on('drain', function () {
        rs.resume()
    })
}
//Nodejs直接提供了`.pipe`方法，可以直接实现上面方法的代码功能。
```



## File System(文件系统)

Nodejs提供了 `fs` 内置模块对文件的操作。



## `Path` 路径

Nodejs 提供了`path` 内置模块来简化路径相关的操作。

- `path.normalize` 

  将传入的路径转换为标准路径，如除了解析路径中的`.`与`..`外，还能去掉多余的斜杠。

  用路径作为某些数据的索引，但又允许用户随意输入路径时，就需要使用该方法保证路径的唯一性。

  ```javascript
  var cache = {};
  
  function store(key, value) {
  	cache[path.normalize(key)] = value;
  }
  
  store('foo/bar', 1);
  store('foo//baz//../bar', 2);
  // 通过path.normailze对路径进行了标准路径处理，上面两个其实是对应同一个路径
  console.log(cache);  // => { "foo/bar": 2 }
  ```

  > 标准化之后的路径里的斜杠在Windows系统下是`\`，而在Linux系统下是`/`。如果想保证任何系统下都使用`/`作为路径分隔符的话，需要用`.replace(/\\/g, '/')`再替换一下标准路径。

- `path.join` 

  将传入的多个路径拼接为标准路径。并且能在不同系统下正确使用相应的路径分隔符。

  ```javascript
  path.join('foo/', 'baz/', '../bar'); // => "foo/bar"
  
  path.join('/foo', 'bar', 'baz/asdf', 'quux', '..');
  // Returns: '/foo/bar/baz/asdf'
  
  path.join('foo', {}, 'bar');
  // Throws 'TypeError: Path must be a string. Received {}'
  ```

- `path.extname`

  获取文件的扩展名

  ```javascript
  path.extname('foo/bar.js') // ===> '.js'
  ```

- `path.basename`

  获取文件名

  ```javascript
  path.basename('/foo/bar/baz/asdf/quux.html');
  // Returns: 'quux.html'
  
  path.basename('/foo/bar/baz/asdf/quux.html', '.html');
  // Returns: 'quux'
  ```



## 遍历目录

```javascript
var fs = require('fs')
var path = require('path')

//同步遍历方法
function travel(dir, callback) {
    fs.readdirSync(dir).forEach(function (file) {
        var pathname = path.join(dir, file)
        if (fs.statSync(pathname).isDirectory()) {
            travel(pathname, callback)
        }else{
            callback(pathname)
        }
    })
}

travel('/Users/kevin/Documents/gits/daily_record', function (pathname) {
    console.log(pathname)
})
```



## Nodejs程序退出

1. `process.exit()`

2. `process.kill(process.pid, 'SIGTERM')`

   `SIGKILL` 是告诉进程要立即终止的信号，理想情况下，其行为类似于 `process.exit()`。

   `SIGTERM` 是告诉进程要正常终止的信号。它是从进程管理者（如 `upstart` 或 `supervisord`）等发出的信号。



## 读取环境变量

`process.env` 属性承载了在启动进程时设置的所有环境变量。



## 库/模块

- `Chalk` 可以用来为控制台输出着色。

  ```javascript
  npm install chalk
  
  const chalk = require('chalk')
  console.log(chalk.yellow('Hello, World.'))
  ```

- `Progress` 创建进度条。

  ```javascript
  const ProgressBar = require('progress')
  
  const bar = new ProgressBar(':bar', { total: 10 })
  const timer = setInterval(() => {
    bar.tick()
    if (bar.complete) {
      clearInterval(timer)
    }
  }, 100)
  ```

- `readline` 逐行读取(nodejs 内置)

  ```javascript
  const readline = require('readline').createInterface({
    input: process.stdin,
    output: process.stdout
  })
  
  readline.question(`你叫什么名字?`, name => {
    console.log(`你好 ${name}!`)
    readline.close()
  })
  ```

  [`readline-sync`](https://www.npmjs.com/package/readline-sync) 如果需要密码，则最好不要回显密码，而是显示 `*` 符号。

  最简单的方式是使用 

  ```javascript
  var readlineSync = require('readline-sync');
   
  // Wait for user's response.
  var userName = readlineSync.question('May I have your name? ');
  console.log('Hi ' + userName + '!');
   
  // Handle the secret text (e.g. password).
  var favFood = readlineSync.question('What is your favorite food? ', {
    hideEchoBack: true // The typed text on screen is hidden by `*` (default).
  });
  console.log('Oh, ' + userName + ' loves ' + favFood + '!');
  ```

  `Inquirer`包提供了更完整、更抽象的解决方案。

  ```javascript
  npm i inquirer
  
  const inquirer = require('inquirer')
  
  var questions = [
    {
      type: 'input',
      name: 'name',
      message: "你叫什么名字?"
    }
  ]
  
  inquirer.prompt(questions).then(answers => {
    console.log(`你好 ${answers['name']}!`)
  })
  ```

- `events` 模块 用于处理事件。

  ```javascript
  const EventEmitter = require('events')
  const eventEmitter = new EventEmitter()
  
  // on用于添加回调函数
  eventEmitter.on('start', () => {
    console.log('Start....')
  })
  
  //emit用于触发事件
  eventEmitter.emit('start')
  
  //多个参数
  eventEmitter.on('start', (start, end) => {
    console.log(`从 ${start} 到 ${end}`)
  })
  
  eventEmitter.emit('start', 1, 100)
  ```

- `axios` 用于请求服务器数据的库

- `fs-extra` `fs`模块的直接代替者。



## npm install 慢的解决方法  

- 临时使用淘宝的镜像 ```npm install -g cordova --registry http://registry.npm.taobao.org```  
- 修改配置文件：```npm config set registry http://registry.npm.taobao.org```  或者直接打开C:\Users\用户名\.npmrc文件直接修改
```registry=http://registry.npm.taobao.org/``` 如果修改之后还不是使用最新的镜像，找了一下，把下载的临时文件目录
C:\Users\用户名\.cordova\lib\npm_cache里的文件全部删掉了，再运行就正常从镜像站下载了。

## 使用指定版本的npm

    ```
    npm i npm@4 -g
    ```


