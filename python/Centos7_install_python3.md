安装步骤

+ 编译环境准备

    安装 gcc-c++
    ```bash
    yum install gcc-c++ sqlite-devel
    ```

    如果安装过程中，还报错，再安装如下：
    ```bash
    yum install zlib-devel bzip2-devel openssl-devel ncurese-devel
    ```

    如果还有错，可以安装:
    ```bash
    yum groupinstall 'Development Tools'
    ```

 
+ 编译

    下载源码编译:
    ```bash
    tar Jxvf Python-3.5.1.tar.xz
    cd Python-3.5.1
    ./configure --prefix=/usr/local/python3
    make && make install
    ```

    Python3.5.1 安装编译安装时会默认安装 pip 如果出现：
    `Ignoring ensurepip failure: pip 1.5.6 requires SSL/TLS`
    未安装编译环境，重新安装该编译环境并重新编译 Python3.5.1
    ```bash
    yum install zlib-devel bzip2-devel openssl-devel ncurese-devel
    ```

+ 更换系统默认 Python 版本

    备份旧版本 Python
    ```bash
    mv /usr/bin/python /usr/bin/python2.7
    ```
    新建指向新版本 Python 以及 pip 的软连接
    ```bash
    ln -s /usr/local/python3/bin/python3.5 /usr/bin/python
    ln -s /usr/local/python3/bin/pip3 /usr/bin/pip
    ``` 

+ 更新 yum 相关设置

    vi /usr/bin/yum
    打开文件，修改第一行为：
    `#!/usr/bin/python2.7`

    若执行 yum 时出现以下错误：
    File "/usr/libexec/urlgrabber-ext-down", line 28
    执行以下更改,打开该文件并修改首行为：
    #!/usr/bin/python2.7

+ 其他

    执行 yum 时，若出现以下 Error:
    Error: Delta RPMs disabled because /usr/bin/applydeltarpm not installed.
    执行以下安装可解决：
    ```bash
    yum install deltarpm
    ```

+ 版本共存

    如果你希望同时使用多版本 Python ，例如在保持系统原有版本 Python2.x 不变的情况下使用 Python 3.x,可以考虑使用 virtualenv 构建合适版本的虚拟环境：

    python2.7 环境下搭建 python3.x 环境

    1) 安装 pip
    ```bash
    yum install python-setuptools
    easy_install pip
    #安装virtualenv
    pip install virtualenv
    ```

    2) 在当前文件夹下构建虚拟环境
    ```bash
    virtualenv -p /usr/local/python3/bin/python3 venv
    #启动虚拟环境
    source venv/bin/activate 
    #退出虚拟环境
    deactivate
    ``` 


+ `【ModuleNotFoundError: No module named ‘_ctypes’ make: *** [install] Error 1】解决方式`
```sh
#yum install libffi-devel -y    《-安装这个就能解决
```
