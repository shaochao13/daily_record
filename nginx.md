# 安装(centos 7 中安装nginx)
1. 准备工作
    ```bash
    yum install gcc-c++  
    yum install pcre pcre-devel  
    yum install zlib zlib-devel  
    yum install openssl openssl--devel 
    ```
2. 安装之前，最好检查一下是否已经安装有nginx

    ```bash
    find -name nginx 

    yum remove nginx # 如果系统已经安装了nginx，那么就先卸载
    ```
3. 下载最新的nginx ，解压。
```bash
./configure
make && make install
# 这样基本上就OK。
```


