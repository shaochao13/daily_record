requests, lxml, SQLAlchemy, kivy, Ansible  
使用国内镜像安装package:         
`pip3 install scipy -i http://pypi.douban.com/simple/ --trusted-host pypi.douban.com` 豆瓣    
`pip3 install scipy -i https://pypi.tuna.tsinghua.edu.cn/simple` 清华

[**python 基础**](./python_base.md)

[装饰器](./装饰器.md)
# 
## 科学计算和数据分析会用到：

NumPy：代表的是Numerical Python。NumPy最强大的功能是n维数组。该库还包含基本的线性代数函数，傅里叶变换，随机数函数和与其他底层语言(如Fortran，C和C ++)集成的工具。 

SciPy：代表的是Scientific Python。SciPy建立在NumPy基础上。它是离散傅里叶变换，线性代数，优化和稀疏矩阵等多种高级科学和工程模块最有用的库之一。

Matplotlib：用于绘制各种各样的图形，从直方图到线图、热力图。你可以使用ipython notebook中的Pylab功能(ipython notebook -pylab = inline)在线使用这些绘图功能。如果忽略内联选项，pylab将ipython环境转换为与Matlab非常相似的环境。还可以使用Latex命令在图像添加数学符号。

Pandas：用于结构化数据的运算和操作。广泛用于数据整理和预处理。相较而言，Pandas被添加到Python时间不久，其有助于提高Python在数据科学社区的使用。

Scikit：用于机器学习。该库建立在NumPy，SciPy和matplotlib基础上，包含许多有效的机器学习和统计建模工具，例如分类，回归，聚类和降维。

Statsmodels：用于统计建模。Statsmodels是一个Python中提供用户探索数据、估计统计模型和执行统计测试的模组。可用于不同类型数据的描述性统计，统计测试，绘图功能和结果统计。

Seaborn：用于数据可视化。Seaborn是一个用于在Python中制作有吸引力和翔实的统计图形库。它是基于matplotlib。Seaborn旨在使可视化成为探索和理解数据的核心组成。

Bokeh：用于在现代网络浏览器上创建交互式图表，仪表盘和数据应用程序。它赋予用户以D3.js的风格生成优雅简洁的图形。此外，它具有超大型或流式数据集的高性能交互能力。

Blaze：将Numpy和Pandas的能力扩展到分布式和流式传输数据集。它可以用于从众多来源(包括Bcolz，MongoDB，SQLAlchemy，Apache Spark，PyTables等)访问数据。与Bokeh一起，Blaze可以作为在巨型数据块上创建有效可视化和仪表盘的强大的工具。

Scrapy：用于网络爬虫。它是获取特定模式数据的非常有用的框架。它从网站首页url开始，然后挖掘网站内的网页内容来收集信息。

SymPy：用于符号计算。它具有从基本算术符号到微积分，代数，离散数学和量子物理学的广泛能力。另一个有用的功能是将计算结果格式化为LaTeX代码。

Requests：用于web访问。它类似于标准python库urllib2，但是代码更容易。

可能需要的额外的库：

os用于操作系统和文件操作 

networkx和igraph为基于图的数据操作

regular expressions用于在文本中查找特定模式的数据

BeautifulSoup用于网络爬虫。它不如Scrapy，因为它只是单个网页中提取信息。
# 

## 有用模块
[sys模块](./sys.md)

[os模块](./os.md)

[csv 模块](./csv.md)

[re 模块](./re.md)

[datetime 模块](./datetime.md)

[bisect 模块](./bisect.md)  用于对已排序好的列表进行查询或者插入数值非常棒(采用二分法进行)

[functools](./functools.md) *非常有用模块*

[itertools](./itertools.md)

[contextlib](./contextlib.md) *上下文管理模块*

[addict](https://github.com/mewwts/addict) 用于简化对dict的操作 *非常好用*

[pickle ]

[shelve 模块] 简单的数据存储方案

[queue ]

[multiprocessing ]

[heapq ]

[asyncio ]

[aiohttp]

[Flask](./Flask.md)
[消息分发组件 blinker](http://pythonhosted.org/blinker/)

[array 模块](./array.md) 数组模块，用于操作数值型的集合非常棒

[sqlite3 模块](./sqlite3.md)

`sqlalchemy`

[`celery` 分布式任务队列](http://docs.jinkan.org/docs/celery/)

[tornado](http://www.tornadoweb.cn/documentation)

[arrow](https://github.com/crsmithdev/arrow) *更好的 Python 日期时间操作类库*

### 与函数式编程相关模块：
[functools]

[operator]

## 科学应用:     
   
Numba 加速Python科学计算  
Anaconda(工具) 

[Matplotlib](./matplotlib.md) 提供了一个类似 Matlab 的画图工具。

[NumPy](./numpy.md) 提供了 ndarray 对象，可以进行快速的向量化计算。

***numexpr***  numpy 加速包，非常简单易用

[Scipy](./scipy.md) 是 Python 中进行科学计算的一个第三方库，以 Numpy 为基础。

Pandas 是处理时间序列数据的第三方库，提供一个类似 R 语言的环境。

StatsModels 是一个统计库，着重于统计模型。

Scikits 以 Scipy 为基础，提供如 scikits-learn 机器学习和scikits-image 图像处理等高级用法。

## 其他模块
[Charder 统一字符编码侦测包](https://pypi.python.org/pypi/chardet)

[inspect]

[abc 用于处理抽象类](./abc.md)

[fileinput] 可以对一个或多个文件中的内容进行迭代、遍历等操作.

#

## [图像处理](./图像处理.md)    



## XML解析:  

    untangle

    xmltodict

## 密码学:    
> Cryptography 提供了加密方法（recipes）和基元（primitives）    
```python
from cryptography.fernet import Fernet  
key = Fernet.generate_key() 
cipher_suite = Fernet(key)  
cipher_text = cipher_suite.encrypt(b"A really    secret message. Not for prying eyes.")
plain_text = cipher_suite.decrypt(cipher_text)  
```

PyCrypto 提供安全的哈希函数和各种加密算法   
```python
from Crypto.Cipher import AES
# Encryption
encryption_suite = AES.new('This is a key123', AES.MODE_CBC, 'This is an IV456')
cipher_text = encryption_suite.encrypt("A really secret message. Not for prying eyes.")

# Decryption
decryption_suite = AES.new('This is a key123', AES.MODE_CBC, 'This is an IV456')
plain_text = decryption_suite.decrypt(cipher_text)
```

## 虚拟环境:    
virtualenv          

`pip install virtualenv`    

1. 为一个工程创建一个虚拟环境    
```
$ cd my_project_folder          
$ virtualenv venv
```

virtualenv venv 将会在当前的目录中创建一个文件夹，包含了Python可执行文件，以及 pip 库的一份拷贝，这样就能安装其他包了。虚拟环境的名字（此例中是 venv ）可以是任意的；若省略名字将会把文件均放在当前目录.   

可以选择使用一个Python解释器:  
```
$ virtualenv -p /usr/bin/python2.7 venv
```
2. 要开始使用虚拟环境，其需要被激活 
```
$ source venv/bin/activate
```
3. 如果你在虚拟环境中暂时完成了工作，则可以停用它  
```
$ deactivate
```

运行带 --no-site-packages 选项的 virtualenv 将不会包括全局安装的包。这可用于保持包列表干净，以防以后需要访问它。

```
$ pip freeze > requirements.txt
//这将会创建一个 requirements.txt 文件，其中包含了当前环境中所有包及各自的版本的简单列表。

$ pip install -r requirements.txt
//这能帮助确保安装、部署和开发者之间的一致性。
```

---------

+ 判断一个数是否为2的幂:
    ```python
    def is_pow2(n):
        return (n & (n - 1)) == 0
    ```

