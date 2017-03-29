requests, lxml, SQLAlchemy, kivy, Ansible  
使用国内镜像安装package:         
`pip3 install scipy -i http://pypi.douban.com/simple/ --trusted-host pypi.douban.com` 豆瓣    
`pip3 install scipy -i https://pypi.tuna.tsinghua.edu.cn/simple` 清华
## 科学应用:     
   
Numba 加速Python科学计算  
Anaconda(工具) 

[Matplotlib](./matplotlib.md) 提供了一个类似 Matlab 的画图工具。

[NumPy](./numpy.md) 提供了 ndarray 对象，可以进行快速的向量化计算。

[Scipy](./scipy.md) 是 Python 中进行科学计算的一个第三方库，以 Numpy 为基础。

Pandas 是处理时间序列数据的第三方库，提供一个类似 R 语言的环境。

StatsModels 是一个统计库，着重于统计模型。

Scikits 以 Scipy 为基础，提供如 scikits-learn 机器学习和scikits-image 图像处理等高级用法。


## 图像处理:    

+ PIL(Python Imaging Library)使用**Pillow**分支;  `pip install Pillow`
    ```python
    from PIL import Image, ImageFilter
    #读取图像
    im = Image.open( 'image.jpg' )
    #显示图像
    im.show()

    #过滤图像
    im_sharp = im.filter( ImageFilter.SHARPEN )
    #保存过滤过的图像到文件中
    im_sharp.save( 'image_sharpened.jpg', 'JPEG' )

    #分解图像到三个RGB不同的通道（band）中。
    r,g,b = im_sharp.split()

    #显示被插入到图像中的EXIF标记
    exif_data = im._getexif()
    exif_data
    ```
    
+ OpenCV (OpenSource Computer Vision)  
    *在Python中，使用OpenCV进行图像处理是通过使用 cv2 与 NumPy 模块进行的*

    ```python
    from cv2 import *
    import numpy as np
    #读取图像
    img = cv2.imread('testimg.jpg')
    #显示图像
    cv2.imshow('image',img)
    cv2.waitKey(0)
    cv2.destroyAllWindows()

    #Applying Grayscale filter to image 作用Grayscale（灰度）过滤器到图像上
    gray = cv2.cvtColor(img, cv2.COLOR_BGR2GRAY)

    #保存过滤过的图像到新文件中
    cv2.imwrite('graytest.jpg',gray)
    ```

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

### import的原理机制  
import modu 语句将 寻找合适的文件，即调用目录下的 modu.py 文件（如果该文件存在）。如果没有 找到这份文件，Python解释器递归地在 “PYTHONPATH” 环境变量中查找该文件，如果仍没 有找到，将抛出ImportError异常。    

### 整数与不同进制的字符串的转化   
+ 十进制 --> 十六进制: 
```python
hex(255)    //'0xff'
```
+ 十六进制 --> 十进制:
```python
int('FF', 16)   //255
```
+ 十进制 --> 八进制:  
```python
oct(255)    //'0377'
```
+ 八进制 --> 十进制:
```python
int('377', 8)   //255
```
+ 十进制 --> 二进制:  
```python
bin(255)    //0b11111111
```
+ 二进制 --> 十进制:
```python
int('11111111', 2)   //255
```

### 集合(set)
并(union):

    两个集合的并，返回包含两个集合所有元素的集合（去除重复）。可以用方法 a.union(b) 或者操作 a | b 实现。

交(intersection):

    两个集合的交，返回包含两个集合共有元素的集合。可以用方法 a.intersection(b) 或者操作 a & b 实现。

差(difference): 
    
    a 和 b 的差集，返回只在 a 不在 b 的元素组成的集合,可以用方法 a.difference(b) 或者操作 a - b 实现。

对称差(symmetric_difference):

    a 和b 的对称差集，返回在 a 或在 b 中，但是不同时在 a 和 b 中的元素组成的集合。可以用方法 a.symmetric_difference(b) 或者操作 a ^ b 实现（异或操作符）。

包含关系(issubset):

    要判断 b 是不是 a 的子集，可以用 b.issubset(a) 方法，或者更简单的用操作 b <= a 

add 方法向集合添加单个元素

update 方法向集合添加多个元素

remove 方法移除单个元素 (从集合s中移除元素ob，如果不存在会报错)

discard 方法移除单个元素 (但是当元素在集合中不存在的时候不会报错)

pop方法弹出元素   (pop 方法删除并返回集合中任意一个元素，如果集合中没有元素会报错)

#### 不可变集合(frozen set)

不可变集合的一个主要应用是用来作为字典的键，例如用一个字典来记录两个城市之间的距离。  

```python
flight_distance = {}
city_pair = frozenset(['Los Angeles', 'New York'])
flight_distance[city_pair] = 2498
flight_distance[frozenset(['Austin', 'Los Angeles'])] = 1233
flight_distance[frozenset(['Austin', 'New York'])] = 1515
```

不可变集合也是不分顺序的，所以如下两种取到同一值：
```python
flight_distance[frozenset(['New York','Austin'])]
flight_distance[frozenset(['Austin','New York'])]
```


------

1. while 和 for 循环后跟else语句：
    + 要和break一起连用。
    + 当循环正常结束时，循环条件不满足，else被执行。
    + 当循环被break结束时，循环条件仍然满足，else不执行。

    ```python
    # 不执行else
    values = [7, 6, 4, 7, 19, 2, 1]
    for x in values:
        if x <= 10:
            print 'Found:', x
            break
    else:
        print 'All values greater than 10'
    ```

    ```python
    # 执行else
    values = [11, 12, 13, 100]
    for x in values:
        if x <= 10:
            print 'Found:', x
            break
    else:
        print 'All values greater than 10'
    ```

2. map 方法

    其用法为：
    `map(aFun, aSeq)`

    将函数 aFun 应用到序列 aSeq 上的每一个元素上，返回一个列表，不管这个序列原来是什么类型。

    ```python
    def sqr(x): 
        return x ** 2

    a = [2,3,4]
    print map(sqr, a)
    ```
    输出： `[4, 9, 16]`

    根据函数参数的多少，map 可以接受多组序列，将其对应的元素作为参数传入函数:

    ```python
    def add(x, y): 
        return x + y

    a = (2,3,4)
    b = [10,5,3]
    print map(add,a,b)
    ```
    输出：`[12, 8, 7]`

3. `__name__` 属性  
    只有当文件被当作脚本执行的时候， `__name__`的值才会是 `__main__`
    ```python
    # ex2.py
    def test():
        w = [0,1,2,3]
        assert(sum(w) == 6)
        print 'test passed.'
        
    if __name__ == '__main__':
        test()
    # 当执行python ex2.py 时,会执行test()
    # 当着模块导入时import ex2时，不会执行test()
    ```
