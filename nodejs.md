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

   



## npm install 慢的解决方法  

- 临时使用淘宝的镜像 ```npm install -g cordova --registry http://registry.npm.taobao.org```  
- 修改配置文件：```npm config set registry http://registry.npm.taobao.org```  或者直接打开C:\Users\用户名\.npmrc文件直接修改
```registry=http://registry.npm.taobao.org/``` 如果修改之后还不是使用最新的镜像，找了一下，把下载的临时文件目录
C:\Users\用户名\.cordova\lib\npm_cache里的文件全部删掉了，再运行就正常从镜像站下载了。

## 使用指定版本的npm

    ```
    npm i npm@4 -g
    ```


