## Ideal 中的 Mybatis Plugin 插件破解方法
参考 http://blog.csdn.net/u011410529/article/details/54098067 

1. 打开IDEA ， preference -> plugins-> browse repository到达下面页面先安装 Mybatis Plugin 插件。
2. 从 https://github.com/myoss/profile 上下载破解文件。

3. MAC上的破解：

    使用find命令在你的用户目录下查找mybatis_plus.jar这个文件：
    ```bash
    find ~ -name "mybatis_plus.jar"
    ```
    然后进入找到的文件夹中，做如下操作：
    ```bash
    #创建一个文件夹
    mkdir m
    #进去 
    cd m
    #拷贝到m文件夹中 
    cp ../mybatis_plus.jar .
    #解压jar包
    jar xf mybatis_plus.jar 
    #从第2步下载下来的文件中找到ideal中的mybatis相关的文件夹中，复制com文件夹到这里   路径根据你情况而定，版本号也根据你情况而定
    cp -r ~/Workspace/github/mybatis_plus/idea/plugin/MybatisPlugin/v2.7\~v2.83/com .
    #重新打为jar包
    jar cf mybatis_plus.jar *
    #复制到m的上层目录
    cp mybatis_plus.jar ../
    ```

4. restart IDEA!


