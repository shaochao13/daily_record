更改pip源至国内镜像

+ linux下，修改 ~/.pip/pip.conf (没有就创建一个)
```bash
[global]
index-url = https://pypi.tuna.tsinghua.edu.cn/simple # 清华源
```

```bash
[global]
index-url = http://pypi.douban.com/simple/ # 豆瓣源
```


+ windows下，直接在user目录中创建一个pip目录，如：C:\Users\xx\pip，新建文件pip.ini
```bash
[global]
index-url = https://pypi.tuna.tsinghua.edu.cn/simple
```

# pipenv 使用国内源
通过添加环境变量的方法来处理：
```sh
export PIPENV_PYPI_MIRROR=https://pypi.tuna.tsinghua.edu.cn/simple


```

