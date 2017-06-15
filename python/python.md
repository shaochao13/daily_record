requests, lxml, SQLAlchemy, kivy, Ansible  
使用国内镜像安装package:         
`pip3 install scipy -i http://pypi.douban.com/simple/ --trusted-host pypi.douban.com` 豆瓣    
`pip3 install scipy -i https://pypi.tuna.tsinghua.edu.cn/simple` 清华

[**python 基础**](./python_base.md)

## 有用模块
[sys模块](./sys.md)

[os模块](./os.md)

[csv 模块](./csv.md)

[re 模块](./re.md)

[datetime 模块](./datetime.md)

[bisect 模块](./bisect.md)  用于对已排序好的列表进行查询或者插入数值非常棒(采用二分法进行)

[pickle ]

[queue ]

[multiprocessing ]

[heapq ]

[asyncio ]


[array 模块](./array.md) 数组模块，用于操作数值型的集合非常棒

[sqlite3 模块](./sqlite3.md)

`sqlalchemy`

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

