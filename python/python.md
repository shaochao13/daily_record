requests, lxml, SQLAlchemy, kivy, Ansible       

## 科学应用:     

    NumPy   
    SciPy   
    Matplotlib  
    Pandas  
    Numba 加速Python科学计算  
    Anaconda(工具)

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

1. import的原理机制  
    import modu 语句将 寻找合适的文件，即调用目录下的 modu.py 文件（如果该文件存在）。如果没有 找到这份文件，Python解释器递归地在 “PYTHONPATH” 环境变量中查找该文件，如果仍没 有找到，将抛出ImportError异常。    

