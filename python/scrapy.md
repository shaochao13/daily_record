## 部署

+ 安装 scrapyd
```bash
pip install scrapyd
pip install scrapyd-client # 上传工具(scrapyd-client)
```

+ 发布
    1) 拷贝scrapyd-deploy到爬虫目录下

    2) 修改爬虫的scapy.cfg文件

        1、去掉url前的注释符号，这里url就是你的scrapyd服务器的网址； 

        2、deploy:127表示把爬虫发布到名为127的爬虫服务器上，deploy:后的名字可以自己定义；
    
    3) 上传scrapy到scrapyd


## 保存数据到文件
可以使用 `JSON Lines` 格式 进行 保存 ， `JSON Lines` 格式会按“流”的方式进行数据保存。
```bash
scrapy crawl quotes -o quotes.jl # 这样能保证每次启动时的数据会往文件后面添加 ，也不会覆盖文件重新添加。
```

## 算法：
深度优先算法-> 递归

广度优先算法-> 队列


# css 选择器
![](./images/css_1.png)
![](./images/css_2.png)
![](./images/css_3.png)