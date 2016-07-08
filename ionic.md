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