# npm install 慢的解决方法  
- 临时使用淘宝的镜像 ```npm install -g cordova --registry http://registry.npm.taobao.org```  
- 修改配置文件：```npm config set registry http://registry.npm.taobao.org```  或者直接打开C:\Users\用户名\.npmrc文件直接修改
```registry=http://registry.npm.taobao.org/``` 如果修改之后还不是使用最新的镜像，找了一下，把下载的临时文件目录
C:\Users\用户名\.cordova\lib\npm_cache里的文件全部删掉了，再运行就正常从镜像站下载了。

