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

